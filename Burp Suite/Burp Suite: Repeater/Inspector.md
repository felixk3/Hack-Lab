O Inspector é um recurso complementar às visualizações de Requisição e Resposta no módulo Repeater. Ele também é usado para obter uma análise visual organizada das requisições e respostas, bem como para experimentar e verificar como as alterações feitas usando o Inspector de nível superior afetam as versões originais equivalentes.

O Inspector pode ser utilizado tanto no módulo Proxy quanto no módulo Repeater. Em ambos os casos, ele está localizado no canto direito da janela, apresentando uma lista de componentes dentro da requisição e da resposta:



Dentre esses componentes, as seções referentes à requisição geralmente podem ser modificadas, permitindo a adição, edição e remoção de itens. Por exemplo, na seção Atributos da Requisição , podemos alterar elementos relacionados à localização, ao método e ao protocolo da requisição. Isso inclui modificar o recurso desejado para recuperação, alterar o método HTTP de GET para outra variante ou trocar o protocolo de HTTP /1 para HTTP /2.

Mudando o protocolo de HTTP/1 para HTTP/2

Outras seções disponíveis para visualização e/ou edição incluem:

Parâmetros de consulta da requisição: Referem-se aos dados enviados ao servidor através da URL. Por exemplo, em uma requisição GET como https://admin.tryhackme.com/?redirect=false, o parâmetro de consulta redirect tem o valor "false".
Parâmetros do corpo da requisição: Semelhantes aos parâmetros de consulta, mas específicos para requisições POST. Quaisquer dados enviados como parte de uma requisição POST serão exibidos nesta seção, permitindo que modifiquemos os parâmetros antes de reenviá-los.
Solicitar cookies: Esta seção contém uma lista modificável de cookies enviados com cada solicitação.
Cabeçalhos de Requisição: Permitem visualizar, acessar e modificar (incluindo adicionar ou remover) quaisquer cabeçalhos enviados com nossas requisições. Editar esses cabeçalhos pode ser valioso ao examinar como um servidor web responde a cabeçalhos inesperados.
Cabeçalhos de Resposta: Esta seção exibe os cabeçalhos retornados pelo servidor em resposta à nossa solicitação. Ela não pode ser modificada, pois não temos controle sobre os cabeçalhos retornados pelo servidor. Observe que esta seção só fica visível após o envio de uma solicitação e o recebimento de uma resposta.
