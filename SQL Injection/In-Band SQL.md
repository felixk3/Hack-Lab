 

Injeção de SQL em banda

A injeção de SQL em banda é o tipo mais fácil de detectar e explorar; "em banda" refere-se simplesmente ao uso do mesmo método de comunicação para explorar a vulnerabilidade e também para receber os resultados, por exemplo, descobrir uma vulnerabilidade de injeção de SQL em uma página da web e, em seguida, ser capaz de extrair dados do banco de dados para a mesma página.

 

Injeção de SQL baseada em erros
Esse tipo de injeção de SQL é o mais útil para obter facilmente informações sobre a estrutura do banco de dados, pois as mensagens de erro do banco são exibidas diretamente na tela do navegador. Isso pode ser usado para enumerar um banco de dados inteiro. 

 

Injeção de SQL baseada em união
Esse tipo de injeção utiliza o operador UNION do SQL juntamente com uma instrução SELECT para retornar resultados adicionais à página. Esse método é a forma mais comum de extrair grandes quantidades de dados por meio de uma vulnerabilidade de injeção de SQL .

 

Prático:
Clique no botão verde "Iniciar Máquina" para usar o laboratório prático de exemplo de injeção de SQL . Cada nível contém um navegador simulado, além de caixas de consulta SQL e de erro para ajudar você a criar consultas/payloads corretos. Pode ser necessário atualizar esta página da web após a inicialização da máquina caso você receba um erro 502 Bad Gateway.


O primeiro nível do laboratório prático contém um navegador e um site simulados, apresentando um blog com diferentes artigos, que podem ser acessados ​​alterando o número de identificação na string de consulta.

 

A chave para descobrir a injeção de SQL baseada em erros é quebrar a consulta SQL do código , tentando certos caracteres até que uma mensagem de erro seja produzida; estes são mais comumente apóstrofos simples ( ' ) ou aspas ( " ).

 

Tente digitar um apóstrofo (  '  ) após id=1 e pressione Enter. Você verá que isso retorna um erro SQL informando sobre um erro de sintaxe. O fato de você ter recebido essa mensagem de erro confirma a existência de uma vulnerabilidade de injeção de SQL . Agora podemos explorar essa vulnerabilidade e usar as mensagens de erro para aprender mais sobre a estrutura do banco de dados. 

 

A primeira coisa que precisamos fazer é retornar dados para o navegador sem exibir uma mensagem de erro. Primeiramente, vamos tentar o operador UNION para que possamos receber um resultado extra, caso o selecionemos. Tente definir o parâmetro `id` do navegador simulado para:

 

1 UNION SELECT 1

 

Essa instrução deve gerar uma mensagem de erro informando que a instrução UNION SELECT possui um número diferente de colunas em comparação com a consulta SELECT original. Portanto, vamos tentar novamente, adicionando mais uma coluna:

 

1 UNION SELECT 1,2

 

O mesmo erro ocorre novamente, então vamos repetir adicionando outra coluna:

 

1 UNION SELECT 1,2,3

 

Sucesso! A mensagem de erro desapareceu e o artigo está sendo exibido, mas agora queremos exibir nossos dados em vez do artigo. O artigo é exibido porque o código pega o primeiro resultado retornado em algum lugar do código do site e o mostra. Para contornar isso, precisamos que a primeira consulta não produza resultados. Isso pode ser feito simplesmente alterando o ID do artigo de 1 para 0.

 

0 UNION SELECT 1,2,3

 

Agora você verá que o artigo é composto apenas pelo resultado da consulta UNION, retornando os valores das colunas 1, 2 e 3. Podemos começar a usar esses valores retornados para obter informações mais úteis. Primeiro, vamos obter o nome do banco de dados ao qual temos acesso:

 

0 UNION SELECT 1,2,database()

 

Agora você verá onde o número 3 era exibido anteriormente; agora ele mostra o nome do banco de dados, que é  sqli_one .

 

Nossa próxima consulta coletará uma lista das tabelas presentes neste banco de dados.

 

0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'sqli_one'

 

Há algumas novidades para aprender nesta consulta. Primeiro, o método  `group_concat()`  obtém a coluna especificada (no nosso caso, `table_name`) de várias linhas retornadas e a coloca em uma única string separada por vírgulas. Em seguida, temos o  banco de dados `information_schema`  ; todo usuário do banco de dados tem acesso a ele, e ele contém informações sobre todos os bancos de dados e tabelas aos quais o usuário tem acesso. Nesta consulta específica, estamos interessados ​​em listar todas as tabelas do  banco de dados `sqli_one`  , que são `article` e `staff_users`. 

 

Como o primeiro nível visa descobrir a senha de Martin, a tabela staff_users é o que nos interessa. Podemos utilizar novamente o banco de dados information_schema para encontrar a estrutura dessa tabela usando a consulta abaixo.

 

0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name = 'staff_users'

 

Esta consulta é semelhante à consulta SQL anterior . No entanto, a informação que queremos recuperar mudou de `table_name` para  `column_name` , a tabela que estamos consultando no banco de dados `information_schema` mudou de `tables` para  `columns` , e estamos procurando por quaisquer linhas onde a  coluna `table_name`  tenha o valor `  staff_users` .

 

Os resultados da consulta fornecem três colunas para a tabela staff_users: id, password e username. Podemos usar as colunas username e password na consulta a seguir para recuperar as informações do usuário.

 

0 UNION SELECT 1,2,group_concat(username,':',password SEPARATOR '<br>') FROM staff_users

 

Novamente, usamos o método `group_concat` para retornar todas as linhas em uma única string, facilitando a leitura. Também adicionamos  `:`  para separar o nome de usuário da senha. Em vez de usar vírgulas, optamos pela tag HTML `  <br>`  , que força cada resultado a ficar em uma linha separada, facilitando a leitura.

 

Agora você deve ter acesso à senha de Martin para entrar e passar para o próximo nível.

 
