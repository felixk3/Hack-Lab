Um exercício útil para realizar ao tentar encontrar vulnerabilidades de autenticação é criar uma lista de nomes de usuário válidos, que usaremos posteriormente em outras tarefas.



As mensagens de erro do site são ótimos recursos para coletar essas informações e construir nossa lista de nomes de usuário válidos. Temos um formulário para criar uma nova conta de usuário na página de cadastro do site de suporte de TI da Acme ( http://10.10.155.180/customers/signup ) .



Se você tentar inserir o nome de usuário  "admin"  e preencher os outros campos do formulário com informações falsas, verá que recebemos o erro "  Já existe uma conta com este nome de usuário" . Podemos usar a existência dessa mensagem de erro para gerar uma lista de nomes de usuário válidos já cadastrados no sistema usando a ferramenta ffuf abaixo. A ferramenta ffuf usa uma lista de nomes de usuário comuns para verificar se há correspondências.



Enumeração de nomes de usuário com ffuf
user@tryhackme$ ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.155.180/customers/signup -mr "username already exists"
No exemplo acima, o -wargumento seleciona a localização do arquivo no computador que contém a lista de nomes de usuário que vamos verificar. O argumento -Xespecifica o método da requisição; por padrão, será uma requisição GET, mas em nosso exemplo, é uma requisição POST. O -dargumento especifica os dados que vamos enviar. Em nosso exemplo, temos os campos username, email, password e cpassword. Definimos o valor do campo username como FUZZ . Na ferramenta ffuf, a palavra-chave FUZZ indica onde o conteúdo da nossa lista de palavras será inserido na requisição. O -Hargumento é usado para adicionar cabeçalhos adicionais à requisição. Neste caso, estamos definindo o cabeçalho Content-Type para que o servidor web saiba que estamos enviando dados de formulário. O -uargumento especifica a URL para a qual estamos fazendo a requisição e, finalmente, o -mrargumento é o texto na página que estamos procurando para validar se encontramos um nome de usuário válido.

A ferramenta ffuf e a lista de palavras vêm pré-instaladas no AttackBox ou podem ser instaladas localmente fazendo o download em https://github.com/ffuf/ffuf .

Crie um  arquivo chamado valid_usernames.txt e adicione os nomes de usuário que você encontrou usando o ffuf; eles serão usados  ​​na Tarefa 3.
