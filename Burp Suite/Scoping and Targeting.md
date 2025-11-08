Finalmente, chegamos a um dos aspectos mais importantes do uso do Burp Proxy : o escopo .

Capturar e registrar todo o tráfego pode rapidamente se tornar algo complexo e inconveniente, especialmente quando queremos nos concentrar apenas em aplicativos da web específicos. É aí que entra o escopo.

Ao definir um escopo para o projeto, podemos definir o que será interpolado e registrado no Burp Suite . Podemos restringir o Burp Suite para testar apenas os aplicativos web específicos que desejamos. A maneira mais fácil de fazer isso é alternar para a Targetaba, clicar com o botão direito do mouse no alvo na lista à esquerda e selecionar " Add To ScopeInterromper escopo". O Burp então solicitará que escolhamos se queremos interromper o registro de tudo o que não estiver no escopo e, na maioria dos casos, devemos selecionar "Interromper escopo" yes.



Para verificar nosso escopo, podemos acessar a subguia Configurações de Escopo dentro da guia Alvo .

A janela de configurações de Escopo permite controlar o escopo de destino, incluindo ou excluindo domínios/ IPs . Esta seção é poderosa e vale a pena dedicar um tempo para se familiarizar com ela.

No entanto, mesmo que desativemos o registro de tráfego fora do escopo, o proxy ainda interceptará tudo. Para evitar isso, precisamos acessar a subguia Configurações do ProxyAnd URL Is in target scope e selecionar a opção "Interceptar solicitações do cliente".



Habilitar essa opção garante que o proxy ignore completamente qualquer tráfego que não esteja dentro do escopo definido, resultando em uma visualização de tráfego mais limpa no Burp Suite .
