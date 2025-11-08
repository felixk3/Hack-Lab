Como desenvolvedor, é importante estar ciente das vulnerabilidades de aplicações web, como encontrá-las e os métodos de prevenção. Para prevenir vulnerabilidades de inclusão de arquivos, algumas sugestões comuns incluem:

Mantenha o sistema e os serviços, incluindo as estruturas de aplicativos da web, atualizados com a versão mais recente.
Desative os erros do PHP para evitar o vazamento do caminho do aplicativo e outras informações potencialmente reveladoras.
Um firewall de aplicações web (WAF) é uma boa opção para ajudar a mitigar ataques a aplicações web.
Desative alguns recursos do PHP que causam vulnerabilidades de inclusão de arquivos se seu aplicativo web não precisar deles, como allow_url_fopen e allow_url_include .
Analise cuidadosamente a aplicação web e permita apenas os protocolos e wrappers PHP que forem necessários.
Nunca confie cegamente na entrada do usuário e certifique-se de implementar uma validação de entrada adequada para a inclusão de arquivos.
Implemente listas de permissão para nomes e locais de arquivos, bem como listas de bloqueio.
