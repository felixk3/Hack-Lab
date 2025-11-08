O que é inclusão de arquivos?

Esta sala tem como objetivo fornecer o conhecimento essencial para explorar vulnerabilidades de inclusão de arquivos, incluindo Inclusão de Arquivo Local ( LFI ), Inclusão de Arquivo Remoto ( RFI ) e travessia de diretório. Também discutiremos o risco dessas vulnerabilidades caso sejam encontradas e as medidas corretivas necessárias. Forneceremos exemplos práticos de cada vulnerabilidade, bem como desafios práticos.

Em alguns cenários, os aplicativos da web são desenvolvidos para solicitar acesso a arquivos em um determinado sistema, incluindo imagens, texto estático e assim por diante, por meio de parâmetros. Os parâmetros são strings de consulta anexadas à URL que podem ser usadas para recuperar dados ou executar ações com base na entrada do usuário. O diagrama a seguir detalha as partes essenciais de uma URL.



 

 
Por exemplo, parâmetros são usados ​​na busca do Google, onde  requisições GET  passam os dados inseridos pelo usuário para o mecanismo de busca.  https://www.google.com/search?q=TryHackMe . Se você não estiver familiarizado com o assunto, pode consultar o  módulo Como a Web Funciona  para entender o conceito.  

Vamos analisar um cenário em que um usuário solicita acesso a arquivos de um servidor web. Primeiro, o usuário envia uma requisição  HTTP para o servidor web, incluindo o arquivo a ser exibido. Por exemplo, se um usuário deseja acessar e exibir seu currículo dentro da aplicação web, a requisição pode ser semelhante a esta: http://webapp.thm/get.php ? file = userCV.pdf , onde " file " é o parâmetro e " userCV.pdf" é o arquivo que se deseja acessar.



Por que ocorrem vulnerabilidades de inclusão de arquivos?
Vulnerabilidades de inclusão de arquivos são comumente encontradas e exploradas em diversas linguagens de programação para aplicações web, como PHP  , que são mal escritas e implementadas. O principal problema dessas vulnerabilidades é a validação de entrada, na qual os dados inseridos pelo usuário não são higienizados ou validados, e o usuário os controla. Quando a entrada não é validada, o usuário pode passar qualquer dado para a função, causando a vulnerabilidade.
 
Qual o risco de inclusão do arquivo?
Por padrão, um atacante pode explorar vulnerabilidades de inclusão de arquivos para vazar dados, como código, credenciais ou outros arquivos importantes relacionados ao aplicativo web ou ao sistema operacional. Além disso, se o atacante conseguir gravar arquivos no servidor por qualquer outro meio, a inclusão de arquivos poderá ser usada em conjunto para obter execução remota de comandos ( RCE ).
