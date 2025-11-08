A aba Target no Burp Suite oferece mais do que apenas controle sobre o escopo dos nossos testes. Ela consiste em três sub-abas:

Mapa do site : Esta subguia permite mapear os aplicativos web que estamos visando em uma estrutura de árvore. Cada página visitada enquanto o proxy estiver ativo será exibida no mapa do site. Este recurso permite gerar automaticamente um mapa do site simplesmente navegando pelo aplicativo web. No Burp Suite Professional, também podemos usar o mapa do site para realizar rastreamento automatizado do alvo, explorando links entre páginas e mapeando o máximo possível do site. Mesmo com o Burp Suite Community, ainda podemos utilizar o mapa do site para coletar dados durante as etapas iniciais de enumeração. É particularmente útil para mapear APIs, pois quaisquer endpoints de API acessados ​​pelo aplicativo web serão capturados no mapa do site.

Definições de problemas : Embora o Burp Community não inclua todas as funcionalidades de varredura de vulnerabilidades disponíveis no Burp Suite Professional, ainda temos acesso a uma lista de todas as vulnerabilidades que o scanner procura. A seção Definições de problemas fornece uma lista extensa de vulnerabilidades web, completa com descrições e referências. Este recurso pode ser valioso para referenciar vulnerabilidades em relatórios ou auxiliar na descrição de uma vulnerabilidade específica que possa ter sido identificada durante testes manuais.

Configurações de escopo : Essa configuração permite controlar o escopo do teste no Burp Suite . Ela possibilita incluir ou excluir domínios/ IPs específicos para definir o escopo do teste. Ao gerenciar o escopo, podemos nos concentrar nos aplicativos web que estamos visando especificamente e evitar a captura de tráfego desnecessário.

De forma geral, a aba "Alvo" oferece recursos que vão além do escopo, permitindo mapear aplicativos da web, refinar o escopo do alvo e acessar uma lista abrangente de vulnerabilidades da web para fins de referência.

Desafio
Dê uma olhada no site http://MACHINE_IP/— usaremos isso bastante ao longo do módulo. Visite todas as outras páginas que estão linkadas na página inicial e, em seguida, verifique o mapa do site — um dos endpoints deve se destacar por ser muito incomum!
