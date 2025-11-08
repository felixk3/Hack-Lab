Vamos analisar a arquitetura de aplicações web para explicar como as condições de corrida são possíveis.

Modelo Cliente-Servidor
As aplicações web seguem um modelo cliente-servidor:

Cliente : O cliente é o programa ou aplicativo que inicia a solicitação de um serviço. Por exemplo, quando navegamos em uma página da web, nosso navegador solicita a página (arquivo) de um servidor web.
Servidor : O servidor é o programa ou sistema que fornece esses serviços em resposta a solicitações recebidas. Por exemplo, o servidor web responde a uma solicitação HTTP GET recebida e envia uma página HTML (ou arquivo) para o navegador web solicitante (cliente).
De maneira geral, o modelo cliente-servidor funciona em uma rede. O cliente envia sua solicitação pela rede, e o servidor a recebe e a processa antes de enviar de volta o recurso solicitado.

Aplicação Web típica
Uma aplicação web segue uma arquitetura de múltiplas camadas. Essa arquitetura separa a lógica da aplicação em diferentes camadas ou níveis. O design mais comum utiliza três camadas:

Camada de apresentação : Em aplicações web, esta camada consiste no navegador web do lado do cliente. O navegador web renderiza o código HTML, CSS e JavaScript.
Camada de aplicação : Esta camada contém a lógica de negócios e a funcionalidade da aplicação web. Ela recebe as requisições do cliente, as processa e interage com a camada de dados. É implementada utilizando linguagens de programação do lado do servidor, como Node.js e PHP , entre muitas outras.
Camada de dados : Esta camada é responsável por armazenar e manipular os dados da aplicação. As operações típicas de banco de dados incluem criar, atualizar, excluir e pesquisar registros existentes. Geralmente, isso é feito usando um sistema de gerenciamento de banco de dados (SGBD); exemplos de SGBD incluem MySQL e PostgreSQL.
Um navegador web acessando um servidor web. O servidor web está conectado a um banco de dados na nuvem.

Estados
Antes de nos aprofundarmos, vamos analisar alguns exemplos de lógica de negócios. Consideraremos os seguintes exemplos:

Validar e realizar transferências de dinheiro.
Validar códigos de cupom e aplicar descontos
Validação e realização de transferência de dinheiro
Considere o exemplo de transferir dinheiro para um amigo ou para sua outra conta. O programa se desenvolverá da seguinte forma:

O usuário clica no botão “Confirmar Transferência”.
O aplicativo consulta o banco de dados para confirmar se o saldo da conta é suficiente para cobrir o valor da transferência.
O banco de dados responde à consulta.
Se o valor estiver dentro dos limites da conta, o aplicativo realiza a transação.
Se o valor ultrapassar os limites da conta, o aplicativo exibirá uma mensagem de erro.
Fluxograma de um programa responsável por transferências de dinheiro.

Em um cenário ideal, o código acima leva a dois estados do programa:

Valor não enviado
Valor enviado
Diagrama de estados para um programa responsável por transferências monetárias; mostra dois estados.

Validar códigos de cupom e aplicar descontos
Vamos considerar o exemplo de aplicação de um cupom de desconto. O usuário acessa o carrinho de compras e adiciona um cupom para obter o desconto. Os passos podem ser algo como o seguinte:

O usuário insere um código de cupom.
O aplicativo consulta o banco de dados para determinar se o código do cupom é válido e se existem restrições.
O banco de dados responde com validade e restrições.
O desconto será aplicado se o código for válido e não houver restrições quanto à sua utilização para este usuário.
Uma mensagem de erro é exibida se o código for inválido ou se houver restrições à sua aplicação para este usuário.
Exemplo de fluxograma do código responsável por aplicar um cupom de desconto.

O código acima leva a alguns estados do programa:

Cupom não aplicado
Cupom aplicado
Diagrama de estados do código responsável por aplicar um cupom de desconto; ele mostra dois estados.

Dois estados? Pense bem.
Vamos continuar nossa análise da aplicação de um cupom de desconto. Idealmente, esperamos dois estados: Cupom não aplicado e Cupom aplicado . No entanto, isso é muito simplista para representar cenários complexos da vida real. Podemos adicionar um estado intermediário: Verificando a aplicabilidade do cupom .

Um diagrama de estados para o código responsável por aplicar um cupom de desconto; ele mostra três estados.

Dependendo de como o aplicativo for desenvolvido, podemos esperar mais estados. Por exemplo, a verificação da aplicabilidade do cupom pode envolver dois estados: Verificação da validade do cupom e Verificação das restrições do cupom . Um cupom pode ser válido, mas restrições existentes impedem sua aplicação. Da mesma forma, o cupom aplicado pode ser dividido em dois estados, um dos quais é o recálculo do total .

Um diagrama de estados para o código responsável por aplicar um cupom de desconto; ele mostra cinco estados.

Por que isso é importante para as condições da corrida?

No diagrama de estados acima, podemos ver que passamos por vários estados antes que o cupom seja marcado como aplicado. Vamos representar os estados em um eixo temporal, como mostrado abaixo.

Cronologia mostrando os diferentes estágios pelos quais o aplicativo passa ao aplicar um cupom de desconto.

Existe um intervalo de tempo entre o instante em que tentamos adicionar um cupom e o instante em que o cupom é marcado como aplicado e não pode ser aplicado novamente. Enquanto o cupom não estiver marcado como aplicado, provavelmente não haverá nenhum controle impedindo que ele seja aceito repetidamente. Podemos até conseguir aplicá-lo várias vezes durante esse intervalo de tempo.

Essa situação é semelhante ao considerarmos os estados do programa que realiza uma transferência de dinheiro. Embora o ideal fossem dois estados, considerando a lógica de negócios, podemos facilmente atualizar o diagrama para incluir três estados. Isso porque esperamos que algum tempo seja gasto verificando o saldo e os limites da conta; embora esse tempo possa ser breve, não é zero. Se analisarmos mais a fundo, podemos descobrir estados "ocultos" adicionais.

Diagrama de estados do programa responsável por transferências monetárias; mostra três estados.

Contudo, mesmo que a aplicação web seja vulnerável, ainda temos um desafio a superar: o tempo. Mesmo em aplicações vulneráveis, essa "janela de oportunidade" é relativamente curta; portanto, explorá-la exige que nossas requisições cheguem ao servidor simultaneamente. Na prática, nosso objetivo é fazer com que nossas requisições repetidas cheguem ao servidor com apenas milissegundos de intervalo.
