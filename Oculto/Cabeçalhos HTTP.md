Cabeçalhos HTTP

Quando fazemos requisições ao servidor web, ele retorna vários cabeçalhos HTTP . Esses cabeçalhos podem conter informações úteis, como o software do servidor web e possivelmente a linguagem de programação/script em uso. No exemplo abaixo, podemos ver que o servidor web é o NGINX versão 1.18.0 e executa o PHP versão 7.4.3. Usando essas informações, podemos encontrar versões vulneráveis ​​de software em uso. Tente executar o comando curl abaixo contra o servidor web, onde a opção -v habilita o modo detalhado, que exibirá os cabeçalhos (pode haver algo interessante!).

curl site.com -v  ISSO e para ver o cabecalho http
