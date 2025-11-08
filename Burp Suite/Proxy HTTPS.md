Observação: O AttackBox já está configurado para resolver o problema apresentado nesta tarefa. Se você utiliza o AttackBox e não deseja ler as informações aqui, pode pular para a próxima tarefa.

Ao interceptar tráfego HTTP , podemos encontrar um problema ao navegar para sites com TLS habilitado. Por exemplo, ao acessar um site como https://google.com/, podemos receber um erro indicando que a Autoridade Certificadora ( CA ) do PortSwigger não está autorizada a proteger a conexão. Isso ocorre porque o navegador não confia no certificado apresentado pelo Burp Suite .



Para contornar esse problema, podemos adicionar manualmente o certificado da Autoridade Certificadora (CA) PortSwigger à lista de autoridades certificadoras confiáveis ​​do nosso navegador. Veja como fazer:

Baixe o certificado da CA : Com o Burp Proxy ativado, acesse http ://burp/cert. Isso fará o download de um arquivo chamado cacert.der. Salve este arquivo em algum lugar do seu computador.

Para acessar as configurações de certificado do Firefox: Digite about:preferenceso endereço na barra de endereços do Firefox e pressione Enter . Isso o levará à página de configurações do Firefox. Procure por "certificados" na página e clique no botão "Exibir certificados " .



Importe o certificado da CA : Na janela Gerenciador de Certificados, clique no botão Importar . Selecione o cacert.derarquivo que você baixou na etapa anterior.

Configurar a confiança no certificado da CA : Na janela seguinte, marque a caixa que diz "Confiar nesta CA para identificar sites" e clique em OK.



Ao concluir esses passos, adicionamos o certificado da Autoridade Certificadora (CA) da PortSwigger à nossa lista de autoridades certificadoras confiáveis. Agora, devemos conseguir acessar qualquer site com TLS habilitado sem encontrar o erro de certificado.

Você pode assistir ao vídeo a seguir para uma demonstração visual de todo o processo de importação de certificados:



Seguindo estas instruções, você pode garantir que seu navegador confie no certificado CA do PortSwigger e se comunique com segurança com sites habilitados para TLS por meio do Burp Suite Proxy .
