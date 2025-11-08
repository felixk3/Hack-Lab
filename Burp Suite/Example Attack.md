Após termos visto como configurar e instalar nosso proxy , vamos analisar um exemplo simplificado do mundo real.

Começaremos por analisar o formulário de suporte em http://MACHINE_IP/ticket/:



Em um teste de penetração de uma aplicação web real, testaríamos isso para uma variedade de coisas, uma das quais seria Cross-Site Scripting (ou XSS ). Se você ainda não se deparou com XSS , pode-se pensar nisso como a injeção de um script do lado do cliente (geralmente em Javascript) em uma página web de forma que ele seja executado. Existem vários tipos de XSS – o tipo que estamos usando aqui é chamado de XSS "Refletido" , pois afeta apenas a pessoa que faz a requisição web.

Passo a passo
Tente digitar: <script>alert("Succ3ssful XSS")</script>, no campo "E-mail de contato". Você verá que existe um filtro no lado do cliente que impede a adição de caracteres especiais não permitidos em endereços de e-mail.

 

GIF demonstrando o filtro do lado do cliente

Felizmente para nós, os filtros do lado do cliente são absurdamente fáceis de contornar. Existem várias maneiras de desativar o script ou simplesmente impedir que ele seja carregado.

Por enquanto, vamos nos concentrar em simplesmente ignorar o filtro.

Primeiro, certifique-se de que seu Burp Proxy esteja ativo e que a interceptação esteja habilitada.

Agora, insira alguns dados válidos no formulário de suporte. Por exemplo: "pentester@example.thm " como endereço de e-mail e "Test Attack" como consulta.

Envie o formulário  —  a solicitação deverá ser interceptada pelo proxy .

Com a requisição capturada no proxy , podemos agora alterar o campo de e-mail para o nosso payload simples, como mostrado acima. <script>alert("Succ3ssful XSS")</script>Após colar o payload, precisamos selecioná-lo e, em seguida, codificá-lo em URL com o Ctrl + Uatalho para torná-lo seguro para envio. Esse processo é mostrado no GIF abaixo:

GIF demonstrando o processo explicado de interceptação e codificação de URL da carga útil colada.

Por fim, pressione o botão "Encaminhar" para enviar a solicitação.

Você deverá encontrar uma caixa de alerta no site indicando um ataque XSS bem-sucedido!

