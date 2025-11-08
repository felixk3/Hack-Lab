Baseado em Booleanos

A injeção de SQL baseada em valores booleanos refere-se à resposta que recebemos de nossas tentativas de injeção, que pode ser verdadeiro/falso, sim/não, ligado/desligado, 1/0 ou qualquer resposta que só possa ter dois resultados possíveis. Esse resultado confirma se nossa carga útil de injeção de SQL foi bem-sucedida ou não. À primeira vista, você pode achar que essa resposta limitada não fornece muitas informações. No entanto, com apenas essas duas respostas, é possível enumerar toda a estrutura e o conteúdo de um banco de dados.



Prático:

No terceiro nível da máquina de exemplos de injeção de SQL , você verá um navegador simulado com a seguinte URL:



https://website.thm/checkuser ?username = admin



O corpo da requisição do navegador contém   {"taken":true} . Este endpoint da API replica um recurso comum encontrado em muitos formulários de cadastro, que verifica se um nome de usuário já está registrado para solicitar que o usuário escolha um nome de usuário diferente. Como o  valor de " taken "  está definido como  "true" , podemos presumir que o nome de usuário "admin" já está registrado. Podemos confirmar isso alterando o nome de usuário na barra de endereços do navegador simulado de  "admin"  para  "admin123" e, ao pressionar Enter, você verá que o valor de  "taken"  agora mudou para  "false" .



A consulta SQL processada tem a seguinte aparência:



select * from users where username = '%username%' LIMIT 1;



A única entrada que controlamos é o nome de usuário na string de consulta, e precisaremos usá-la para realizar nossa injeção  de SQL . Mantendo o nome de usuário como admin123 , podemos começar a adicionar informações a ele para tentar fazer com que o banco de dados confirme valores verdadeiros, alterando o estado do campo "taked" de falso para verdadeiro.



Assim como nos níveis anteriores, nossa primeira tarefa é determinar o número de colunas na tabela de usuários, o que podemos fazer usando a instrução UNION. Altere o valor do nome de usuário para o seguinte:



admin123' UNION SELECT 1;-- 



Como o aplicativo web respondeu com o valor  "taked  " como falso, podemos confirmar que este é o valor incorreto para o número de colunas. Continue adicionando mais colunas até obtermos o  valor "taked "  como  verdadeiro . Você pode confirmar que a resposta é três colunas definindo o nome de usuário com o valor abaixo:



admin123' UNION SELECT 1,2,3;-- 



Agora que definimos o número de colunas, podemos trabalhar na enumeração do banco de dados. Nossa primeira tarefa é descobrir o nome do banco de dados. Podemos fazer isso usando o  método `database()` da função integrada  e, em seguida, usando o  operador `like`  para tentar encontrar resultados que retornem o valor `true`.

Experimente o nome de usuário abaixo e veja o que acontece:



admin123' UNION SELECT 1,2,3 where database() like '%';--



Obtemos uma resposta verdadeira porque, no operador "like", temos apenas o valor "  %" , que corresponde a qualquer coisa, já que é um valor curinga. Se alterarmos o operador curinga para  "%" , você verá que a resposta volta a ser falsa, o que confirma que o nome do banco de dados não começa com a letra "  a" . Podemos percorrer todas as letras, números e caracteres como "-" e "_" até encontrarmos uma correspondência. Se você enviar o código abaixo como valor do nome de usuário, receberá uma  resposta verdadeira  que confirma que o nome do banco de dados começa com a letra  "s" .



admin123' UNION SELECT 1,2,3 where database() like 's%';--



Agora você passa  para o próximo caractere do nome do banco de dados até encontrar outra resposta verdadeira, por exemplo, 'sa%', 'sb%', 'sc%', etc. Continue com esse processo até descobrir todos os caracteres do nome do banco de dados, que é  sqli_three .



Já definimos o nome do banco de dados, que agora podemos usar para enumerar os nomes das tabelas usando um método semelhante, aproveitando o banco de dados information_schema. Tente definir o nome de usuário com o seguinte valor:



admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'a%';--



Esta consulta procura resultados no  banco de dados information_schema  , na  tabela tables  , onde o nome do banco de dados corresponde  a sqli_three e o nome da tabela começa com a letra a. Como a consulta acima resulta em uma  resposta falsa  , podemos confirmar que não há tabelas no banco de dados sqli_three que comecem com a letra a. Como anteriormente, você precisará percorrer letras, números e caracteres até encontrar uma correspondência positiva.



Você acabará descobrindo uma tabela no banco de dados sqli_three chamada users, que você pode confirmar executando o seguinte payload de nome de usuário:



admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name='users';--



Por fim, precisamos agora enumerar os nomes das colunas na  tabela de usuários  para que possamos pesquisá-la corretamente em busca de credenciais de login. Novamente, podemos usar o banco de dados information_schema e as informações que já obtivemos para consultá-lo em busca dos nomes das colunas. Usando o payload abaixo, pesquisamos a  tabela columns  onde o banco de dados é igual a sqli_three, o nome da tabela é users e o nome da coluna começa com a letra a.



admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%';



Novamente, você precisará percorrer letras, números e caracteres até encontrar uma correspondência. Como você está procurando por vários resultados, terá que adicionar isso à sua carga útil cada vez que encontrar um novo nome de coluna para evitar descobrir a mesma. Por exemplo, depois de encontrar a coluna chamada  "id" , você a anexará à sua carga útil original (como mostrado abaixo).



admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%' and COLUMN_NAME !='id';



Repetindo esse processo três vezes, você poderá descobrir o ID, o nome de usuário e a senha das colunas. Agora você pode usar essas informações para consultar a  tabela de usuários  e obter as credenciais de login. Primeiro, você precisará descobrir um nome de usuário válido, o que pode ser feito usando o payload abaixo:



admin123' UNION SELECT 1,2,3 from users where username like 'a%



Depois de percorrer todos os caracteres, você confirmará a existência do nome de usuário  "admin" . Agora que você tem o nome de usuário, pode se concentrar em descobrir a senha. O código abaixo mostra como encontrar a senha:



admin123' UNION SELECT 1,2,3 from users where username='admin' and password like 'a%



Ao percorrer todos os caracteres, você descobrirá que a senha é 3845.



Agora você pode usar o nome de usuário e a senha que descobriu através da vulnerabilidade de injeção SQL cega no formulário de login para acessar o próximo nível.
