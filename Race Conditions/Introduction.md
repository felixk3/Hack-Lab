Digamos que nossa tarefa seja testar a segurança de um aplicativo de compras online. Muitas perguntas surgem. Podemos reutilizar um único cartão-presente de US$ 10 para pagar por um item de US$ 100? Podemos aplicar o mesmo desconto ao nosso carrinho de compras várias vezes? A resposta é: talvez ! Se o sistema for suscetível a uma vulnerabilidade de condição de corrida, podemos fazer tudo isso e muito mais.

Esta sala aborda a vulnerabilidade de condição de corrida. Uma condição de corrida é uma situação em programas de computador onde o momento em que os eventos ocorrem influencia o comportamento e o resultado do programa. Isso geralmente acontece quando uma variável é acessada e modificada por múltiplas threads. Devido à falta de mecanismos de bloqueio adequados e sincronização entre as diferentes threads, um atacante pode abusar do sistema e aplicar um desconto várias vezes ou realizar transações financeiras além do seu saldo.

Objetivos de aprendizagem
Após concluir esta sala, você aprenderá sobre o seguinte:

vulnerabilidade às condições de corrida
Utilizando o Burp Suite Repeater para explorar condições de corrida.
Ao longo do caminho, você também aprenderá sobre:

Threads e multithreading
Diagramas de estado
Pré-requisitos de aprendizagem
Para acompanhar esta sala, recomendamos familiaridade com o protocolo HTTP , aplicações web e Burp Suite . As salas e módulos a seguir são recomendados para preencher quaisquer lacunas de conhecimento.

Como funciona a Web
Pacotes e Molduras
Burp Suite : O Básico
