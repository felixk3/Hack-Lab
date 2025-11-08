Em essência, o Burp Suite é um framework baseado em Java projetado para servir como uma solução abrangente para a realização de testes de penetração em aplicações web. Tornou-se a ferramenta padrão da indústria para avaliações práticas de segurança de aplicações web e mobile, incluindo aquelas que dependem de interfaces de programação de aplicações ( APIs ) .

Em termos simples, o Burp Suite captura e permite a manipulação de todo o tráfego HTTP /HTTPS entre um navegador e um servidor web. Essa capacidade fundamental forma a espinha dorsal da estrutura. Ao interceptar as requisições, os usuários têm a flexibilidade de encaminhá-las para vários componentes dentro da estrutura do Burp Suite , que exploraremos nas próximas seções. A capacidade de interceptar, visualizar e modificar requisições web antes que elas cheguem ao servidor de destino, ou mesmo manipular as respostas antes que sejam recebidas pelo navegador, torna o Burp Suite uma ferramenta indispensável para testes manuais de aplicações web.


O Burp Suite está disponível em diferentes edições. Para os nossos propósitos, vamos nos concentrar na edição Community do Burp Suite , que é de acesso gratuito para uso não comercial dentro dos limites legais. No entanto, vale ressaltar que o Burp Suite também oferece as edições Professional e Enterprise, que incluem recursos avançados e exigem licenciamento.

O Burp Suite Professional é uma versão sem restrições do Burp Suite Community. Ele inclui recursos como:

Um scanner de vulnerabilidades automatizado.
Um fuzzer/brute-forcer que não possui limitação de taxa.
Salvar projetos para uso futuro e gerar relatórios.
Uma API integrada que permite a integração com outras ferramentas.
Acesso irrestrito para adicionar novas extensões e obter maior funcionalidade.
Acesso ao Burp Suite Collaborator (que efetivamente fornece um captador de requisições exclusivo, hospedado localmente ou executado em um servidor de propriedade da Portswigger).

Resumindo, o Burp Suite Professional é uma ferramenta extremamente poderosa, o que o torna a escolha preferida dos profissionais da área.

O Burp Suite Enterprise , diferentemente das edições Community e Professional, é utilizado principalmente para varredura contínua. Ele possui um scanner automatizado que verifica periodicamente aplicações web em busca de vulnerabilidades, de forma similar a ferramentas como o Nessus, que realizam varreduras automatizadas de infraestrutura. Ao contrário das outras edições, que permitem ataques manuais a partir de uma máquina local, o Burp Suite Enterprise reside em um servidor e verifica constantemente as aplicações web alvo em busca de potenciais vulnerabilidades.

Prévia do Burp Suite Enterprise

Devido à necessidade de licença para as edições Professional e Enterprise, focaremos no conjunto de recursos principais oferecidos pela Burp Suite Community Edition.
