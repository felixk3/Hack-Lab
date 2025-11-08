Se você não está acostumado a trabalhar com bancos de dados ou a explorá-los, provavelmente terá que se familiarizar com alguns termos novos. Portanto, vamos começar com alguns conceitos básicos sobre como os bancos de dados são estruturados e como funcionam.



O que é um banco de dados?

Um banco de dados é uma forma de armazenar eletronicamente coleções de dados de maneira organizada. Um banco de dados é controlado por um SGBD, sigla para Sistema de Gerenciamento de Banco de Dados. Os SGBDs se dividem em duas categorias: relacionais e não relacionais; o foco desta aula será em bancos de dados relacionais; alguns dos mais comuns que você encontrará são MySQL, Microsoft SQL Server, Access, PostgreSQL e SQLite. Explicaremos a diferença entre bancos de dados relacionais e não relacionais ao final desta atividade, mas primeiro, é importante aprender alguns termos.


Em um SGBD (Sistema de Gerenciamento de Banco de Dados), você pode ter vários bancos de dados, cada um contendo seu próprio conjunto de dados relacionados. Por exemplo, você pode ter um banco de dados chamado " loja ". Nesse banco de dados, você deseja armazenar informações sobre produtos disponíveis para compra , usuários que se cadastraram em sua loja online e informações sobre os pedidos recebidos. Você armazenaria essas informações separadamente no banco de dados usando algo chamado tabelas. As tabelas são identificadas com um nome exclusivo para cada uma. Você pode ver essa estrutura no diagrama abaixo, mas também pode observar como uma empresa pode ter outros bancos de dados separados para armazenar informações da equipe ou do departamento financeiro.




O que são tabelas?

Uma tabela é composta por colunas e linhas; uma maneira útil de imaginar uma tabela é como uma grade, com as colunas dispostas horizontalmente na parte superior, da esquerda para a direita, contendo o nome da célula, e as linhas dispostas de cima para baixo, com cada uma contendo os dados propriamente ditos.







Colunas:

Cada coluna, também chamada de campo, possui um nome único por tabela. Ao criar uma coluna, você também define o tipo de dados que ela conterá, sendo os tipos mais comuns números inteiros, strings (texto padrão) ou datas. Alguns bancos de dados podem conter dados muito mais complexos, como dados geoespaciais, que incluem informações de localização. Definir o tipo de dados também garante que informações incorretas não sejam armazenadas, como a string "hello world" em uma coluna destinada a datas. Se isso acontecer, o servidor de banco de dados geralmente exibirá uma mensagem de erro. Uma coluna que contém um número inteiro também pode ter o recurso de autoincremento ativado; isso atribui a cada linha de dados um número único que aumenta (incrementa) a cada linha subsequente. Isso cria o que é chamado de campo -chave ; um campo-chave precisa ser único para cada linha de dados, o que pode ser usado para encontrar essa linha específica em consultas SQL .



Linhas:

As linhas ou registros contêm linhas individuais de dados. Quando você adiciona dados à tabela, uma nova linha/registro é criada; quando você exclui dados, uma linha/registro é removido.





Bancos de Dados Relacionais vs. Não Relacionais:
Um banco de dados relacional armazena informações em tabelas e, frequentemente, as tabelas compartilham informações entre si; elas usam colunas para especificar e definir os dados armazenados e linhas para armazenar os dados propriamente ditos. As tabelas geralmente contêm uma coluna com um ID único (chave primária), que será usada em outras tabelas para referenciá-la e estabelecer um relacionamento entre elas, daí o nome banco de dados relacional .



Bancos de dados não relacionais, também chamados de NoSQL, são qualquer tipo de banco de dados que não utiliza tabelas, colunas e linhas para armazenar os dados. Não é necessário construir um layout específico para o banco de dados, de modo que cada linha de dados pode conter informações diferentes, o que proporciona mais flexibilidade em comparação com um banco de dados relacional. Alguns exemplos populares desse tipo de banco de dados são MongoDB, Cassandra e Elasticsearch .



Agora que você aprendeu o que é um banco de dados, vamos aprender como podemos interagir com ele usando SQL .
