Desenvolvedores mais experientes em segurança e cientes dos riscos das vulnerabilidades SSRF podem implementar verificações em seus aplicativos para garantir que o recurso solicitado atenda a regras específicas. Geralmente, existem duas abordagens para isso: uma lista de bloqueio ou uma lista de permissão.



Lista de bloqueio

Uma lista de bloqueio é uma lista onde todas as solicitações são aceitas, exceto para recursos especificados na lista ou que correspondam a um padrão específico. Uma aplicação web pode usar uma lista de bloqueio para proteger endpoints sensíveis, endereços IP ou domínios do acesso público, permitindo, ao mesmo tempo, o acesso a outros locais. Um endpoint específico para restringir o acesso é o localhost, que pode conter dados de desempenho do servidor ou outras informações sensíveis; portanto, nomes de domínio como localhost e 127.0.0.1 apareceriam em uma lista de bloqueio. Ataques podem contornar uma lista de bloqueio usando referências alternativas para o localhost, como 0, 0.0.0.0, 0000, 127.1, 127.*.*.*, 2130706433, 017700000001 ou subdomínios que possuem um registro DNS que resolve para o endereço IP 127.0.0.1, como 127.0.0.1.nip.io.



Além disso, em um ambiente de nuvem, seria benéfico bloquear o acesso ao endereço IP 169.254.169.254, que contém metadados do servidor em nuvem implantado, incluindo informações possivelmente sensíveis. Um invasor pode contornar isso registrando um subdomínio em seu próprio domínio com um registro DNS que aponte para o endereço IP 169.254.169.254.



Lista de permissões

Uma lista de permissões é um mecanismo no qual todas as solicitações são negadas, a menos que constem em uma lista ou correspondam a um padrão específico, como uma regra que exige que uma URL usada em um parâmetro comece com  https ://website.thm .  Um atacante poderia contornar essa regra rapidamente criando um subdomínio em seu próprio domínio, como https://website.thm.domínio-do-atacante.thm . A lógica do aplicativo permitiria essa entrada, possibilitando ao atacante controlar a solicitação HTTP interna.



Abrir redirecionamento

Se as estratégias acima não funcionarem, o atacante ainda tem mais um truque na manga: o redirecionamento aberto. Um redirecionamento aberto é um ponto de extremidade no servidor onde o visitante do site é automaticamente redirecionado para outro endereço de site. Considere, por exemplo, o link https://website.thm/link? url =https://tryhackme.com. Esse ponto de extremidade foi criado para registrar o número de vezes que os visitantes clicaram nesse link para fins de publicidade/marketing. Mas imagine que exista uma vulnerabilidade SSRF com regras rigorosas que permitam apenas URLs que comecem com https://website.thm/ . Um atacante poderia utilizar esse recurso para redirecionar a requisição HTTP interna para um domínio de sua escolha.

