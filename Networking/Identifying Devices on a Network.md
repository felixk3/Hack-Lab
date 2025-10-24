Para se comunicar e manter a ordem, os dispositivos precisam ser identificáveis ​​e identificáveis ​​em uma rede. De que adianta se você não sabe com quem está falando no final das contas?

Os dispositivos em uma rede são muito semelhantes aos humanos no fato de que temos duas maneiras de sermos identificados:

Nosso nome
Nossas impressões digitais
Agora podemos mudar nosso nome por meio de escritura pública, mas não podemos, no entanto, mudar nossas impressões digitais. Cada ser humano possui um conjunto individual de impressões digitais, o que significa que, mesmo que mude de nome, ainda há uma identidade por trás dele. Os dispositivos têm a mesma função: dois meios de identificação, sendo um deles permeável. São eles:

Um endereço IP
Um endereço de controle de acesso de mídia (MAC) — pense nisso como algo semelhante a um número de série.

Endereços IP
Resumidamente, um endereço IP (ou endereço de Protocolo de Internet ) pode ser usado como forma de identificar um host em uma rede por um período de tempo, onde esse endereço IP pode então ser associado a outro dispositivo sem que o endereço IP seja alterado. Primeiro, vamos detalhar o que é um endereço IP no diagrama abaixo:



Um endereço IP  é um conjunto de números divididos em quatro octetos. O valor de cada octeto será resumido como o endereço IP do dispositivo na rede. Esse número é calculado por meio de uma técnica conhecida como endereçamento IP e sub-redes, mas isso fica para outro dia. O importante é entender que os endereços IP podem mudar de dispositivo para dispositivo, mas não podem estar ativos simultaneamente mais de uma vez na mesma rede.

Os endereços IP seguem um conjunto de padrões conhecidos como protocolos. Esses protocolos são a espinha dorsal das redes e forçam muitos dispositivos a se comunicarem na mesma linguagem, algo que abordaremos em outra ocasião. No entanto, devemos lembrar que os dispositivos podem estar em redes privadas e públicas. A localização deles determinará o tipo de endereço IP que possuem: um endereço IP público ou privado.

Um endereço público é usado para identificar o dispositivo na internet, enquanto um endereço privado é usado para identificar um dispositivo entre outros. Veja a tabela e a captura de tela abaixo como exemplo. Aqui, temos dois dispositivos em uma rede privada:


Nome do dispositivo	Endereço IP	Tipo de endereço IP
DESKTOP-KJE57FD	192.168.1.77	Privado
DESKTOP-KJE57FD	86.157.52.21	Público
CMNatic-PC	192.168.1.74	Privado
CMNatic-PC	86.157.52.21
Público

https://assets.tryhackme.com/additional/cmn-aoc2020/day-8/1.png
Esses dois dispositivos poderão usar seus endereços IP privados para se comunicar. No entanto, quaisquer dados enviados para a internet a partir de qualquer um desses dispositivos serão identificados pelo mesmo endereço IP público. Os endereços IP públicos são fornecidos pelo seu Provedor de Serviços de Internet ( ou ISP ) mediante uma taxa mensal (sua conta!).

https://assets.tryhackme.com/additional/cmn-aoc2020/day-8/2.png

À medida que mais e mais dispositivos se conectam, torna-se cada vez mais difícil obter um endereço público que ainda não esteja em uso. Por exemplo, a Cisco, gigante do setor de redes, estimou que haveria aproximadamente 50 bilhões de dispositivos conectados à internet até o final de 2021. (Cisco., 2021) . Eis as versões de endereços IP. Até agora, discutimos apenas uma versão do esquema de endereçamento do Protocolo de Internet (IPv4), que utiliza um sistema de numeração de 2^32 endereços IP (4,29 bilhões) — então você pode entender por que há tanta escassez!

O IPv6 é uma nova iteração do esquema de endereçamento do Protocolo de Internet para ajudar a resolver esse problema. Embora pareça mais desafiador, ele apresenta algumas vantagens:

Suporta até 2^128 endereços IP (mais de 340 trilhões), resolvendo os problemas enfrentados com IPv4
Mais eficiente devido às novas metodologias
A captura de tela abaixo compara um endereço IPv6 e um endereço IPv4.



Endereços MAC

Todos os dispositivos em uma rede terão uma interface de rede física, que é uma placa de microchip encontrada na placa-mãe do dispositivo. Essa interface de rede recebe um endereço exclusivo na fábrica em que foi construída, chamado de endereço MAC ( Media Access Control ). O endereço MAC é um número hexadecimal de doze caracteres ( um sistema de numeração de base dezesseis usado em computação para representar números ) dividido em dois e separado por dois pontos. Esses dois pontos são considerados separadores. Por exemplo, a4:c3:f0:85:ac:2d . Os seis primeiros caracteres representam a empresa que fez a interface de rede e os seis últimos são um número exclusivo.




No entanto, um aspecto interessante sobre endereços MAC é que eles podem ser falsificados ou "spoofados" em um processo conhecido como spoofing. Esse spoofing ocorre quando um dispositivo em rede finge se identificar como outro usando seu endereço MAC. Quando isso ocorre, muitas vezes pode violar projetos de segurança mal implementados que pressupõem que os dispositivos que se comunicam em uma rede são confiáveis. Considere o seguinte cenário: um firewall está configurado para permitir qualquer comunicação de e para o endereço MAC do administrador. Se um dispositivo fingisse ou "spoofing" esse endereço MAC, o firewall pensaria que está recebendo comunicação do administrador, quando na verdade não está.

Locais como cafés, cafeterias e hotéis costumam usar o controle de endereço MAC ao usar suas redes Wi-Fi "para Convidados" ou "Pública". Essa configuração pode oferecer serviços melhores, ou seja, uma conexão mais rápida por um preço, se você estiver disposto a pagar a taxa por dispositivo. O laboratório interativo anexado a esta tarefa foi criado para replicar esse cenário!

Prático

Os laboratórios interativos simulam uma rede Wi-Fi de hotel onde você tem que pagar pelo serviço. Você notará que o roteador não está permitindo que os pacotes de Bob (azul) cheguem ao site TryHackMe e os está colocando na lixeira, mas os pacotes de Alice (verde) estão passando normalmente porque ela pagou pelo Wi-Fi. Tente alterar o endereço MAC de Bob para o mesmo de Alice para ver o que acontece.
