XSS armazenado

Como o nome sugere, o código malicioso XSS é armazenado na aplicação web (em um banco de dados, por exemplo) e executado quando outros usuários visitam o site ou a página web.

Exemplo:

Um blog que permite aos usuários publicar comentários. Infelizmente, esses comentários não são verificados quanto à presença de JavaScript ou filtrados para remover qualquer código malicioso. Se publicarmos um comentário contendo JavaScript, ele será armazenado no banco de dados e todos os outros usuários que visitarem o artigo terão o JavaScript executado em seus navegadores.




Impacto potencial:

O JavaScript malicioso pode redirecionar os usuários para outro site, roubar o cookie de sessão do usuário ou executar outras ações no site, agindo como o usuário visitante.

Como testar vulnerabilidades XSS armazenadas :

Você precisará testar todos os possíveis pontos de entrada onde os dados parecem ser armazenados e exibidos em áreas acessíveis a outros usuários; um pequeno exemplo disso poderia ser:

Comentários em um blog
Informações do perfil do usuário
Listagens de sites
Às vezes, os desenvolvedores pensam que limitar os valores de entrada no lado do cliente é uma proteção suficiente, então alterar os valores para algo que o aplicativo web não esperaria é uma boa fonte para descobrir XSS armazenado , por exemplo, um campo de idade que espera um número inteiro de um menu suspenso, mas, em vez disso, você envia a solicitação manualmente em vez de usar o formulário, permitindo que você tente executar payloads maliciosos. 

Depois de encontrar alguns dados armazenados na aplicação web, você precisará confirmar se consegue executar com sucesso o seu código JavaScript; o código que você usar dependerá de onde ele está inserido na aplicação (você aprenderá mais sobre isso na tarefa 6).
