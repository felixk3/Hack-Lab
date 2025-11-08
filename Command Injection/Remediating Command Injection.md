A injeção de comandos pode ser evitada de diversas maneiras. Isso inclui desde o uso mínimo de funções ou bibliotecas potencialmente perigosas em uma linguagem de programação até a filtragem de entradas sem depender da interação do usuário. Detalhei esses pontos um pouco mais abaixo. Os exemplos a seguir são da linguagem de programação PHP ; no entanto, os mesmos princípios podem ser estendidos a muitas outras linguagens.



Funções Vulneráveis

Em PHP , muitas funções interagem com o sistema operacional para executar comandos via shell; entre elas estão:

Executivo
Passagem
Sistema


Considere o trecho de código abaixo como exemplo. Nele, o aplicativo aceitará e processará apenas números inseridos no formulário. Isso significa que comandos como `\n` whoaminão serão processados.



O aplicativo aceitará apenas um padrão específico de caracteres (os dígitos de 0 a 9).
A aplicação então prosseguirá apenas com a execução desses dados, que são todos numéricos.


Essas funções recebem entradas como uma string ou dados do usuário e executam o que for fornecido pelo sistema. Qualquer aplicação que utilize essas funções sem as devidas verificações ficará vulnerável a injeção de comandos.



sanitização de entrada

Sanitizar qualquer entrada de um usuário que um aplicativo utilize é uma ótima maneira de prevenir injeção de comandos. Trata-se de um processo que especifica os formatos ou tipos de dados que um usuário pode enviar. Por exemplo, um campo de entrada que aceita apenas dados numéricos ou remove quaisquer caracteres especiais como vírgulas >e  &espaços /.

No trecho de código abaixo, a função filter_input PHP é usada para verificar se os dados enviados por meio de um formulário de entrada são números ou não. Se não forem números, a entrada é considerada inválida.





Ignorando filtros

Os aplicativos empregam diversas técnicas para filtrar e higienizar os dados inseridos pelo usuário. Esses filtros restringem o uso a tipos específicos de dados; no entanto, podemos explorar a lógica do aplicativo para contorná-los. Por exemplo, um aplicativo pode remover aspas; podemos, em vez disso, usar o valor hexadecimal delas para obter o mesmo resultado.

Ao ser executado, embora os dados fornecidos estejam em um formato diferente do esperado, eles ainda podem ser interpretados e produzirão o mesmo resultado.

