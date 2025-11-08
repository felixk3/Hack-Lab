XSS cego

O XSS cego é semelhante ao XSS armazenado (que abordamos na tarefa 4), pois o payload é armazenado no site para que outro usuário o visualize. No entanto, neste caso, você não consegue ver o payload em funcionamento nem testá-lo por conta própria.

Exemplo de cenário:

um site possui um formulário de contato onde você pode enviar mensagens para um membro da equipe. O conteúdo da mensagem não é verificado em busca de código malicioso, o que permite que o atacante insira o que quiser. Essas mensagens são então transformadas em tickets de suporte que a equipe visualiza em um portal web privado.

Impacto potencial:

usando o payload correto, o JavaScript do atacante poderia fazer chamadas de retorno para o site do atacante, revelando a URL do portal da equipe, os cookies do membro da equipe e até mesmo o conteúdo da página do portal que está sendo visualizada. Agora, o atacante poderia potencialmente sequestrar a sessão do membro da equipe e ter acesso ao portal privado.
Como testar a presença de XSS cego :



Ao testar vulnerabilidades de XSS cego , você precisa garantir que seu payload tenha um callback (geralmente uma requisição HTTP ). Dessa forma, você saberá se e quando seu código está sendo executado.



Uma ferramenta popular para ataques Blind XSS é o XSS Hunter Express . Embora seja possível criar sua própria ferramenta em JavaScript, esta ferramenta captura automaticamente cookies, URLs, conteúdo de páginas e muito mais.
