O que é Descoberta Automatizada?

A descoberta automatizada é o processo de usar ferramentas para descobrir conteúdo em vez de fazê-lo manualmente. Esse processo é automatizado porque geralmente envolve centenas, milhares ou até milhões de solicitações a um servidor web. Essas solicitações verificam se um arquivo ou diretório existe em um site, dando-nos acesso a recursos cuja existência desconhecíamos anteriormente. Esse processo é possível graças a um recurso chamado listas de palavras.



O que são listas de palavras?

Listas de palavras são simplesmente arquivos de texto que contêm uma longa lista de palavras de uso comum; elas podem abranger muitos casos de uso diferentes. Por exemplo, uma lista de palavras para senhas incluiria as senhas mais usadas, enquanto que, no nosso caso, estamos procurando conteúdo, então precisaríamos de uma lista contendo os nomes de diretórios e arquivos mais comuns. Um excelente recurso para listas de palavras, pré-instalado no THM AttackBox, é  o https://github.com/danielmiessler/SecLists  , mantido por Daniel Miessler.



Ferramentas de automação

Embora existam muitas ferramentas de descoberta de conteúdo disponíveis, cada uma com seus recursos e falhas, vamos abordar três que já vêm pré-instaladas em nossa máquina de ataque: ffuf, dirb e gobuster .

