
SQLi cego

Ao contrário da injeção SQL em banda , onde podemos ver os resultados do nosso ataque diretamente na tela, a injeção SQL cega ocorre quando recebemos pouco ou nenhum feedback para confirmar se as consultas injetadas foram, de fato, bem-sucedidas ou não. Isso acontece porque as mensagens de erro são desativadas, mas a injeção ainda funciona. Pode ser surpreendente saber que tudo o que precisamos é desse pequeno feedback para enumerar com sucesso um banco de dados inteiro.



Bypass de autenticação

Uma das técnicas mais diretas de injeção SQL cega consiste em burlar métodos de autenticação, como formulários de login. Nesse caso, não estamos interessados ​​em recuperar dados do banco de dados; queremos apenas passar pela tela de login. 



Os formulários de login conectados a um banco de dados de usuários geralmente são desenvolvidos de forma que o aplicativo web não esteja interessado no conteúdo do nome de usuário e da senha, mas sim em verificar se os dois formam um par correspondente na tabela de usuários. Em termos básicos, o aplicativo web está perguntando ao banco de dados : "Você tem um usuário com o nome de usuário 'bob' e a senha 'bob123'?" O banco de dados responde com 'sim' ou 'não' (verdadeiro/falso) e, dependendo dessa resposta, determina se o aplicativo web permite que você prossiga ou não. 



Levando em consideração as informações acima, não é necessário enumerar um par de nome de usuário/senha válido. Basta criar uma consulta ao banco de dados que retorne "sim" ou "verdadeiro".



Prático:

O segundo nível dos exemplos de injeção de SQL mostra exatamente este exemplo. Podemos ver na caixa rotulada como " Consulta SQL " que a consulta ao banco de dados é a seguinte:



select * from users where username='%username%' and password='%password%' LIMIT 1;



Observação: Os  valores de %username%  e  %password%  são obtidos dos campos do formulário de login. Os valores iniciais na caixa de consulta SQL estarão em branco, pois esses campos estão vazios no momento.



Para transformar isso em uma consulta que sempre retorne verdadeiro, podemos inserir o seguinte no campo de senha:



' OR 1=1;--



O que transforma a consulta SQL no seguinte:



select * from users where username='' and password='' OR 1=1;



Como 1=1 é uma afirmação verdadeira e usamos um  operador OR  , a consulta sempre retornará verdadeiro, o que satisfaz a lógica da aplicação web de que o banco de dados encontrou uma combinação válida de nome de usuário/senha e que o acesso deve ser permitido.
