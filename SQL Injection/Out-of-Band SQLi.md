A injeção de SQL fora de banda não é tão comum, pois depende de recursos específicos habilitados no servidor de banco de dados ou da lógica de negócios da aplicação web, que realiza algum tipo de chamada de rede externa com base nos resultados de uma consulta SQL

. Um ataque fora de banda é caracterizado por ter dois canais de comunicação distintos: um para lançar o ataque e outro para coletar os resultados. Por exemplo, o canal de ataque pode ser uma requisição web, e o canal de coleta de dados pode ser o monitoramento de requisições HTTP / DNS feitas a um serviço que você controla.

1) Um atacante faz uma solicitação a um site vulnerável a injeção de SQL com um payload de injeção.

2) O site faz uma consulta SQL ao banco de dados, que também transmite o código malicioso do hacker.

3) A carga útil contém uma solicitação que força uma requisição HTTP de volta para a máquina do hacker, contendo dados do banco de dados.



