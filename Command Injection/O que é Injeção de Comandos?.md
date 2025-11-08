
Nesta sala, vamos abordar a vulnerabilidade web conhecida como injeção de comandos . Depois de entendermos o que é essa vulnerabilidade, demonstraremos seu impacto e o risco que ela representa para uma aplicação.

Em seguida, você poderá colocar esse conhecimento em prática, ou seja:

Como descobrir a vulnerabilidade de injeção de comandos
Como testar e explorar essa vulnerabilidade usando payloads projetados para diferentes sistemas operacionais.
Como prevenir essa vulnerabilidade em um aplicativo
Por fim, você terá a oportunidade de aplicar a teoria na prática, em uma atividade prática ao final da aula.
Para começar, vamos entender o que é injeção de comando . Injeção de comando é o abuso do comportamento de um aplicativo para executar comandos no sistema operacional, usando os mesmos privilégios com os quais o aplicativo está sendo executado no dispositivo. Por exemplo, conseguir injeção de comando em um servidor web executado como um usuário chamado `username` joeexecutará comandos sob esse joeusuário e, portanto, obterá todas as permissões que ele joepossui.

A injeção de comandos também é conhecida como "Execução Remota de Código" ( RCE , na sigla em inglês) devido à capacidade de executar código remotamente dentro de um aplicativo. Essas vulnerabilidades costumam ser as mais lucrativas para um atacante, pois permitem que ele interaja diretamente com o sistema vulnerável. Por exemplo, um atacante pode ler arquivos de sistema ou de usuário, dados e outros itens semelhantes.

Por exemplo, a capacidade de abusar de um aplicativo para executar o comando whoamique lista qual conta de usuário o aplicativo está usando é um exemplo de injeção de comando .

A injeção de comandos foi uma das dez principais vulnerabilidades relatadas no relatório de inteligência AppSec da Contrast Security em 2019 ( Contrast Security AppSec, 2019 ). Além disso, o framework OWASP constantemente propõe vulnerabilidades dessa natureza como uma das dez principais vulnerabilidades de uma aplicação web ( OWASP framework ).
