Se as tarefas anteriores pareceram excessivamente complexas, fique tranquilo, este tópico será muito mais simples.

Além de modificar nosso navegador web padrão para funcionar com o proxy , o Burp Suite também inclui um navegador Chromium integrado que já vem pré-configurado para usar o proxy sem nenhuma das modificações que acabamos de fazer.

Para iniciar o navegador Burp, clique no Open Browserbotão na aba proxy . Uma janela do Chromium será aberta e todas as requisições feitas nesse navegador passarão pelo proxy .



Observação: Existem várias configurações relacionadas ao Burp Browser nas opções do projeto e nas opções do usuário. Certifique-se de explorá-las e personalizá-las conforme necessário.

No entanto, se você estiver executando o Burp Suite no Linux como usuário root (como é o caso do AttackBox), poderá encontrar um erro que impede a inicialização do Burp Browser devido à impossibilidade de criar um ambiente sandbox .

Existem duas soluções simples para isso:

Opção inteligente: Crie um novo usuário e execute o Burp Suite com uma conta de privilégios limitados para permitir que o Burp Browser seja executado sem problemas.
Opção fácil: Acesse Settings -> Tools -> Burp's browsere marque a Allow Burp's browser to run without a sandbox opção. Habilitar essa opção permitirá que o navegador seja iniciado sem um ambiente isolado (sandbox) . No entanto, esteja ciente de que essa opção está desabilitada por padrão por motivos de segurança. Se optar por habilitá-la, tenha cautela, pois comprometer o navegador pode conceder a um invasor acesso a toda a sua máquina. No ambiente de treinamento do AttackBox, é improvável que isso represente um problema significativo, mas use-o com responsabilidade.
