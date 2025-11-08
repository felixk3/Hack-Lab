Antes de usar o Burp Suite Repeater, vamos nos familiarizar com sua finalidade e funcionalidade.

Em essência, o Burp Suite Repeater nos permite modificar e reenviar requisições interceptadas para um alvo de nossa escolha. Ele nos permite pegar requisições capturadas no Burp Proxy e manipulá-las, enviando-as repetidamente conforme necessário. Alternativamente, podemos criar requisições manualmente do zero, de forma semelhante ao uso de uma ferramenta de linha de comando como o cURL.

A capacidade de editar e reenviar solicitações várias vezes torna o Repeater indispensável para a exploração e teste manual de endpoints. Ele oferece uma interface gráfica amigável para a criação de payloads de requisição e diversas visualizações da resposta, incluindo um mecanismo de renderização para representação gráfica.

A interface do Repeater consiste em seis seções principais, conforme ilustrado no diagrama anotado abaixo:

Exibindo uma solicitação de exemplo no repetidor do Burp Suite.

Lista de solicitações : Localizada no canto superior esquerdo da aba, exibe a lista de solicitações do Repeater. Várias solicitações podem ser gerenciadas simultaneamente, e cada nova solicitação enviada ao Repeater aparecerá aqui.

Controles de Requisição : Localizados diretamente abaixo da lista de requisições, esses controles permitem enviar uma requisição, cancelar uma requisição pendente e navegar pelo histórico de requisições.

Visualização de Requisição e Resposta : Ocupando a maior parte da interface, esta seção exibe as visualizações de Requisição e Resposta . Podemos editar a requisição na visualização de Requisição e, em seguida, encaminhá-la, enquanto a resposta correspondente será exibida na visualização de Resposta.

Opções de layout : Localizadas no canto superior direito da visualização de Solicitação/Resposta, essas opções permitem personalizar o layout das visualizações de Solicitação e Resposta. A configuração padrão é um layout lado a lado (horizontal), mas também é possível escolher um layout vertical ou combiná-las em guias separadas.

Inspector : Localizado no lado direito, o Inspector permite analisar e modificar requisições de forma mais intuitiva do que usando o editor padrão. Exploraremos esse recurso em uma tarefa posterior.

Alvo : Localizado acima do Inspector, o campo Alvo especifica o endereço IP ou domínio para o qual as solicitações são enviadas. Quando solicitações são enviadas ao Repeater a partir de outros componentes do Burp Suite , este campo é preenchido automaticamente.
