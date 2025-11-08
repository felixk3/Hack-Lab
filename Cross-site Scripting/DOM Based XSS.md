XSS baseado em DOM

O que é o DOM?
DOM significa Document Object Model ( Modelo de Objeto de Documento ) e é uma interface de programação para documentos HTML e XML . Ele representa a página, permitindo que os programas alterem a estrutura, o estilo e o conteúdo do documento. Uma página da web é um documento, e esse documento pode ser exibido na janela do navegador ou como código-fonte HTML. Um diagrama do DOM HTML é mostrado abaixo:



Se você quiser aprender mais sobre o DOM e obter uma compreensão mais profunda, o site w3.org oferece um excelente recurso.

Explorando o DOM

XSS baseado em DOM ocorre quando a execução de JavaScript acontece diretamente no navegador, sem que novas páginas sejam carregadas ou dados sejam enviados para o código do servidor. A execução acontece quando o código JavaScript do site reage a uma entrada ou interação do usuário.


Exemplo de cenário:

o JavaScript do site obtém o conteúdo do window.location.hash parâmetro e o insere na página, na seção que está sendo visualizada. O conteúdo do hash não é verificado em busca de código malicioso, permitindo que um atacante injete JavaScript de sua escolha na página.


Impacto potencial:

links maliciosos podem ser enviados para vítimas em potencial, redirecionando-as para outro site ou roubando conteúdo da página ou da sessão do usuário.

Como testar XSS baseado em DOM :



Testar ataques XSS baseados em DOM pode ser um desafio e exige certo conhecimento de JavaScript para analisar o código-fonte. É necessário procurar por partes do código que acessam variáveis ​​que um atacante pode controlar, como parâmetros como " window.location.x ".



Depois de encontrar esses trechos de código, você precisará ver como eles são tratados e se os valores são alguma vez gravados no DOM da página da web ou passados ​​para métodos JavaScript inseguros, como eval() .
