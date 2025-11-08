O Burp Proxy é uma ferramenta fundamental e crucial dentro do Burp Suite . Ele permite a captura de requisições e respostas entre o usuário e o servidor web de destino. Esse tráfego interceptado pode ser manipulado, enviado para outras ferramentas para processamento posterior ou explicitamente autorizado a continuar até seu destino.

Pontos-chave para entender sobre o Burp Proxy
Interceptação de Requisições: Quando requisições são feitas através do Burp Proxy , elas são interceptadas e retidas, impedindo que cheguem ao servidor de destino. As requisições aparecem na aba Proxy , permitindo ações adicionais como encaminhamento, descarte, edição ou envio para outros módulos do Burp.  Para desativar a interceptação e permitir que as requisições passem pelo proxy sem interrupção, clique no botão. Intercept is on 



Assumindo o controle: A capacidade de interceptar solicitações permite que os testadores obtenham controle total sobre o tráfego da web, tornando-se indispensável para testar aplicativos da web.

Captura e registro: O Burp Suite captura e registra as requisições feitas através do proxy por padrão, mesmo quando a interceptação está desativada. Essa funcionalidade de registro pode ser útil para análises e revisões posteriores de requisições anteriores.

Suporte a WebSocket: O Burp Suite também captura e registra a comunicação WebSocket, fornecendo assistência adicional na análise de aplicações web.

Registros e histórico: As solicitações capturadas podem ser visualizadas nas  subguias Histórico HTTP  e Histórico WebSocket , permitindo análises retrospectivas e o envio das solicitações para outros módulos do Burp, conforme necessário.



As opções específicas do proxy podem ser acessadas clicando no botão Configurações do Proxy . Essas opções oferecem amplo controle sobre o comportamento e a funcionalidade do proxy . Familiarize-se com essas opções para otimizar o uso do Burp Proxy .

Algumas funcionalidades notáveis ​​nas configurações de proxy .
Interceptação de respostas: Por padrão, o proxy não intercepta as respostas do servidor, a menos que isso seja explicitamente solicitado para cada requisição. A caixa de seleção "Interceptar respostas com base nas seguintes regras", juntamente com as regras definidas, permite uma interceptação de respostas mais flexível.



Correspondência e Substituição: A seção "Correspondência e Substituição" nas configurações de Proxy permite o uso de expressões regulares (regex) para modificar solicitações de entrada e saída. Esse recurso possibilita alterações dinâmicas, como modificar o agente do usuário ou manipular cookies.
