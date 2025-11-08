Analisar e editar os cookies definidos pelo servidor web durante sua sessão online pode ter várias consequências, como acesso não autenticado, acesso à conta de outro usuário ou privilégios elevados. Se precisar relembrar o que são cookies, consulte a sala HTTP em Detalhe na tarefa 6.



Texto simples

O conteúdo de alguns cookies pode estar em texto simples, e é óbvio o que eles fazem. Veja, por exemplo, se estes fossem os cookies definidos após um login bem-sucedido:

Definir cookie: logado=true; Idade máxima=3600; Caminho=/
Definir cookie: admin=false; Idade máxima=3600; Caminho=/

Vemos um cookie (logged_in), que parece controlar se o usuário está conectado ou não, e outro (admin), que controla se o visitante tem privilégios de administrador. Usando essa lógica, se alterássemos o conteúdo dos cookies e fizéssemos uma requisição, poderíamos alterar nossos privilégios.

Primeiro, vamos começar simplesmente solicitando a página desejada:

Solicitação Curl 1
user@tryhackme$ curl http://10.10.155.180/cookie-test
Podemos ver que recebemos a mensagem: Não conectado

Agora enviaremos outra solicitação com o cookie logged_in definido como verdadeiro e o cookie admin definido como falso:

Solicitação Curl 2
user@tryhackme$ curl -H "Cookie: logged_in=true; admin=false" http://10.10.155.180/cookie-test
Recebemos a mensagem: Logado como usuário

Por fim, enviaremos uma última solicitação definindo os cookies logged_in e admin como verdadeiros:

Solicitação Curl 3
user@tryhackme$ curl -H "Cookie: logged_in=true; admin=true" http://10.10.155.180/cookie-test
Isso retorna o resultado: Logado como administrador, além de um indicador que você pode usar para responder à primeira pergunta.

Hashing

Às vezes, os valores dos cookies podem parecer uma longa sequência de caracteres aleatórios; esses são chamados de hashes, que são uma representação irreversível do texto original. Aqui estão alguns exemplos que você pode encontrar:

Corda original
Método Hash
Saída
1
md5
c4ca4238a0b923820dcc509a6f75849b
1
sha-256
6b86b273ff34fce19d6b804eff5a3f5747ada4eaa22f1d49c01e52ddb7875b4b
1
sha-512	4dff4ea340f0a823f15d3f4f01ab62eae0e5da579ccb851f8db9dfe84c58b2b37b89903a740e1ee172da793a6e79d560e5f7f9bd058a12a280433ed6fa46510a
1
sha1
356a192b7913b04c54574d18c28d46e6395428ab
Como você pode ver na tabela acima, o resultado do hash gerado a partir da mesma string de entrada pode variar significativamente dependendo do método de hash utilizado. Embora o hash seja irreversível, o mesmo resultado é produzido sempre, o que é útil para nós, já que serviços como  https://crackstation.net/  mantêm bancos de dados com bilhões de hashes e suas strings originais.

Codificação

A codificação é semelhante ao hashing, pois cria o que parece ser uma sequência de texto aleatória, mas, na verdade, a codificação é reversível. Isso levanta a questão: qual é a utilidade da codificação? A codificação nos permite converter dados binários em texto legível por humanos, que pode ser transmitido com facilidade e segurança por meios que suportam apenas caracteres ASCII de texto simples.

Os tipos de codificação mais comuns são o Base32, que converte dados binários nos caracteres A-Z e 2-7, e o Base64, que converte usando os caracteres az, A-Z, 0-9, +, / e o sinal de igual para preenchimento.

Considere os dados abaixo como exemplo, que são definidos pelo servidor web ao fazer login:

Definir cookie: sessão=eyJpZCI6MSwiYWRtaW4iOmZhbHNlfQ==; Idade máxima=3600; Caminho=/

Essa string decodificada em base64 tem o valor  {"id":1,"admin": false}.  Podemos então codificá-la novamente em base64, mas definindo o valor "admin" como verdadeiro, o que nos dá acesso de administrador.
