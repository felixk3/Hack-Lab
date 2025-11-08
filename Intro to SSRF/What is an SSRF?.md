Descrição do quarto

Nesta sala, você aprenderá o que é um SSRF , que tipo de impacto ele pode causar, verá alguns exemplos de ataques SSRF , como descobrir vulnerabilidades a SSRF , como contornar regras de entrada e, em seguida, faremos um exercício para você testar suas novas habilidades.



O que é um SSRF ?

SSRF significa Server-Side Request Forgery (Falsificação de Requisição do Lado do Servidor). É uma vulnerabilidade que permite que um usuário malicioso faça com que o servidor web envie uma requisição HTTP adicional ou modificada para o recurso escolhido pelo atacante.



Tipos de SSRF

Existem dois tipos de vulnerabilidade SSRF : o primeiro é o SSRF regular, onde os dados são retornados para a tela do atacante. O segundo é a vulnerabilidade SSRF cega, onde ocorre um SSRF , mas nenhuma informação é retornada para a tela do atacante.

Qual o impacto?
Um ataque SSRF bem-sucedido pode resultar em qualquer um dos seguintes: 

Acesso a áreas não autorizadas.
Acesso a dados de clientes/organizacionais.
Capacidade de expansão para redes internas.
Revelar tokens/credenciais de autenticação.
