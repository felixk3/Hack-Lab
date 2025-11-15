O Repeater é particularmente adequado para tarefas que exigem o envio repetitivo de solicitações semelhantes, geralmente com pequenas modificações. Isso é especialmente útil para atividades como testes manuais de vulnerabilidades de injeção de SQL (que serão abordadas em uma tarefa futura), tentativas de burlar filtros de firewall de aplicativos da web ou ajuste de parâmetros em um formulário enviado.

Vamos começar com um exemplo extremamente simples: Utilizando o Repeater para modificar os cabeçalhos de uma requisição enviada a um destino.

Capturar uma solicitação http://MACHINE_IP/no módulo Proxy e enviá-la para o Repeater.

Envie a solicitação uma vez a partir do Repeater  —  você deverá ver o código-fonte HTML da página solicitada na visualização de Resposta.

Tente visualizar isso em uma das outras opções de exibição (por exemplo, Hexadecimal).

Usando o Inspector (ou manualmente, se preferir), adicione um cabeçalho chamado FlagAuthorisede defina o valor dele como True, conforme mostrado abaixo:

Cabeçalho com FlagAuthorised adicionado
GET / HTTP /1.1
Host: MACHINE_IP 
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:80.0) Gecko/20100101 Firefox/80.0
Aceitar: text/html,application/xhtml+ xml ,application/ xml ;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Conexão: fechar
Solicitações de atualização inseguras: 1
FlagAuthorised: True

