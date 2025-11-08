Para usar o proxy do Burp Suite , precisamos configurar nosso navegador local para redirecionar o tráfego através do Burp Suite . Nesta tarefa, vamos nos concentrar em configurar o proxy usando a extensão FoxyProxy no Firefox.

Observe que as instruções fornecidas são específicas para o Firefox. Se você estiver usando um navegador diferente, talvez precise encontrar métodos alternativos ou usar o TryHackMe AttackBox.

Aqui estão os passos para configurar o Burp Suite Proxy com o FoxyProxy:

Instale o FoxyProxy: Baixe e instale a extensão FoxyProxy Basic .

Observação: o FoxyProxy já está instalado no AttackBox.

Acesse as opções do FoxyProxy: Após a instalação, um botão aparecerá no canto superior direito do navegador Firefox. Clique no botão do FoxyProxy para acessar a janela de opções do FoxyProxy.



Criar configuração de proxy do Burp : Na janela de opções do FoxyProxy, clique no botão Opções . Isso abrirá uma nova aba do navegador com as configurações do FoxyProxy. Clique no botão Adicionar para criar uma nova configuração de proxy .



Adicionar detalhes do proxy : Na página "Adicionar proxy ", preencha os seguintes valores:

Título: Burp(ou qualquer nome de sua preferência)
IP do proxy :127.0.0.1
Porta:8080



Salvar configuração: Clique em Salvar para salvar a configuração do Burp Proxy .

Ativar configuração de proxy : Clique no ícone do FoxyProxy no canto superior direito do navegador Firefox e selecione a Burp configuração. Isso redirecionará o tráfego do seu navegador através do FoxyProxy 127.0.0.1:8080. Observe que o Burp Suite precisa estar em execução para que seu navegador faça requisições quando essa configuração estiver ativada.



Ative a interceptação de proxy no Burp Suite : Alterne para o Burp Suite e certifique-se de que a interceptação esteja ativada na guia Proxy .



Teste o proxy : Abra o Firefox e tente acessar um site, como a página inicial de [nome da empresa] http://MACHINE_IP/. Seu navegador ficará travado e o proxy exibirá a requisição HTTP . Parabéns, você interceptou com sucesso sua primeira requisição!

Lembre-se do seguinte:

Quando a configuração de proxy está ativa e a interceptação está habilitada no Burp Suite , seu navegador ficará travado sempre que você fizer uma requisição.
Tenha cuidado para não deixar a interceptação ativada sem querer, pois isso pode impedir que seu navegador faça qualquer solicitação.
Clicar com o botão direito do mouse em uma solicitação no Burp Suite permite realizar várias ações, como encaminhar, descartar, enviar para outras ferramentas ou selecionar opções no menu de contexto (clique com o botão direito do mouse).
