SQL (Structured Query Language) é uma linguagem rica em recursos usada para consultar bancos de dados. Essas consultas SQL são melhor denominadas instruções.



O mais simples dos comandos que abordaremos nesta tarefa é usado para recuperar (selecionar), atualizar, inserir e excluir dados. Embora sejam um tanto semelhantes, alguns servidores de banco de dados têm sua própria sintaxe e pequenas diferenças no funcionamento. Todos esses exemplos são baseados em um banco de dados MySQL. Após aprender as lições, você poderá facilmente pesquisar online por sintaxes alternativas para os diferentes servidores. Vale ressaltar que a sintaxe SQL não diferencia maiúsculas de minúsculas.



SELECIONAR
O primeiro tipo de consulta que aprenderemos é a consulta SELECT, usada para recuperar dados do banco de dados. 

 

select * from users;



eu ia
nome de usuário
senha
1
jon
passe123
2
administrador
p4ssword
3
Martin
secret123
A primeira palavra, SELECT, indica ao banco de dados que queremos recuperar alguns dados; o * indica que queremos receber todas as colunas da tabela. Por exemplo, a tabela pode conter três colunas (id, nome de usuário e senha). "from users" indica ao banco de dados que queremos recuperar os dados da tabela chamada users. Finalmente, o ponto e vírgula no final indica ao banco de dados que esta é a conclusão da consulta.  



A próxima consulta é semelhante à anterior, mas desta vez, em vez de usar o * para retornar todas as colunas da tabela do banco de dados, estamos solicitando apenas os campos de nome de usuário e senha.



select username,password from users;



nome de usuário
senha
jon
passe123
administrador
p4ssword
Martin
secret123
A consulta a seguir, assim como a primeira, retorna todas as colunas usando o seletor *, e a cláusula "LIMIT 1" força o banco de dados a retornar apenas uma linha de dados. Alterar a consulta para "LIMIT 1,1" força a consulta a ignorar o primeiro resultado, e "LIMIT 2,1" ignora os dois primeiros resultados, e assim por diante. É importante lembrar que o primeiro número indica ao banco de dados quantos resultados você deseja ignorar, e o segundo número indica quantas linhas retornar.



select * from users LIMIT 1;



eu ia
nome de usuário
senha
1
jon
passe123
Por fim, vamos utilizar a cláusula WHERE; é assim que podemos selecionar com precisão os dados exatos de que precisamos, retornando dados que correspondam às nossas cláusulas específicas:



select * from users where username='admin';



eu ia
nome de usuário
senha
2
administrador
p4ssword
Isso retornará apenas as linhas em que o nome de usuário é igual a "admin".



select * from users where username != 'admin';



eu ia
nome de usuário
senha
1
jon
passe123
3
Martin
secret123

Isso retornará apenas as linhas em que o nome de usuário  NÃO é  igual a "admin".



select * from users where username='admin' or username='jon';



eu ia
nome de usuário
senha
1
jon
passe123
2
administrador
p4ssword

Isso retornará apenas as linhas em que o nome de usuário for igual a  admin  ou j em . 



select * from users where username='admin' and password='p4ssword';



eu ia
nome de usuário
senha
2
administrador
p4ssword
Isso retornará apenas as linhas em que o nome de usuário é igual a  admin  e a senha é igual a  p4ssword .



A cláusula LIKE permite especificar dados que não sejam uma correspondência exata, mas que comecem, contenham ou terminem com determinados caracteres, escolhendo onde colocar o caractere curinga representado pelo sinal de porcentagem %.



select * from users where username like 'a%';



eu ia
nome de usuário
senha
2
administrador
p4ssword
Esta função retorna todas as linhas cujo nome de usuário começa com a letra "a".



select * from users where username like '%n';



eu ia
nome de usuário
senha
1
jon
passe123
2
administrador
p4ssword
3
Martin
secret123

Esta função retorna todas as linhas cujo nome de usuário termina com a letra n.



select * from users where username like '%mi%';



eu ia
nome de usuário
senha
2
administrador
p4ssword

Esta função retorna todas as linhas cujo nome de usuário contenha os caracteres  "mi"  .



UNIÃO

A instrução UNION combina os resultados de duas ou mais instruções SELECT para recuperar dados de uma ou mais tabelas. As regras para essa consulta são que a instrução UNION deve recuperar o mesmo número de colunas em cada instrução SELECT, as colunas devem ser de tipos de dados semelhantes e a ordem das colunas deve ser a mesma. Isso pode não parecer muito claro, então vamos usar a seguinte analogia. Digamos que uma empresa queira criar uma lista de endereços de todos os clientes e fornecedores para enviar um novo catálogo. Temos uma tabela chamada clientes com o seguinte conteúdo:



eu ia
nome
endereço
cidade
código postal
1
Senhor John Smith
Rua Falsa 123
Manchester
M2 3FJ
2
Sra. Jenny Palmer
99 Green Road
Birmingham
B2 4KL
3
Senhorita Sarah Lewis
15 Fore Street
Londres
NW12 3GH
E outra chamada fornecedores com o seguinte conteúdo:



eu ia
empresa
endereço
cidade
código postal
1
Widgets Ltd
Unidade 1a, Newby Estate
Bristol
BS19 4RT
2
A Empresa de Ferramentas
75 Estrada Industrial
Norwich
N22 3DR
3
Fabricantes de machados Ltda.
2b Makers Unit, Market Road
Londres
SE9 1KK
Utilizando a seguinte instrução SQL, podemos reunir os resultados das duas tabelas e colocá-los em um único conjunto de resultados:



SELECT name,address,city,postcode from customers UNION SELECT company,address,city,postcode from suppliers;



nome
endereço
cidade
código postal
Senhor John Smith
Rua Falsa 123
Manchester
M2 3FJ
Sra. Jenny Palmer
99 Green Road
Birmingham
B2 4KL
Senhorita Sarah Lewis
15 Fore Street
Londres
NW12 3GH
Widgets Ltd	Unidade 1a, Newby Estate	Bristol	BS19 4RT
A Empresa de Ferramentas	75 Estrada Industrial	Norwich	N22 3DR
Fabricantes de machados Ltda.	2b Makers Unit, Market Road	Londres	SE9 1KK
INSERIR

A  instrução INSERT  informa ao banco de dados que desejamos inserir uma nova linha de dados na tabela.  "into users"  indica ao banco de dados em qual tabela desejamos inserir os dados,  "(username,password)"  fornece as colunas para as quais estamos fornecendo dados e, em seguida,  "values ​​('bob','password');"  fornece os dados para as colunas especificadas anteriormente.



insert into users (username,password) values ('bob','password123');



eu ia
nome de usuário
senha
1
jon
passe123
2
administrador
p4ssword
3
Martin
secret123
4
prumo
senha123
ATUALIZAR
A  instrução UPDATE  informa ao banco de dados que desejamos atualizar uma ou mais linhas de dados em uma tabela. Você especifica a tabela que deseja atualizar usando " update %tablename% SET " e, em seguida, seleciona o(s) campo(s) que deseja atualizar como uma lista separada por vírgulas, como " username='root',password='pass123' ". Finalmente, de forma semelhante à instrução SELECT, você pode especificar exatamente quais linhas atualizar usando a cláusula WHERE, como " where username='admin; ".



update users SET username='root',password='pass123' where username='admin';



eu ia
nome de usuário
senha
1
jon
passe123
2
raiz
passe123
3
Martin
secret123
4
prumo
senha123
EXCLUIR
A  instrução DELETE  informa ao banco de dados que desejamos excluir uma ou mais linhas de dados. Além de não incluir as colunas que você deseja retornar, o formato dessa consulta é muito semelhante ao da instrução SELECT. Você pode especificar precisamente quais dados excluir usando a  cláusula WHERE  e o número de linhas a serem excluídas usando a  cláusula LIMIT  .


delete from users where username='martin';

eu ia
nome de usuário
senha
1
jon
passe123
2
raiz
passe123
4
prumo
senha123
delete from users;



Como nenhuma cláusula WHERE foi usada na consulta, todos os dados foram excluídos da tabela.

eu ia
nome de usuário
senha
