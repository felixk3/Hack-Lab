Alguns subdomínios nem sempre são hospedados em resultados de DNS publicamente acessíveis , como versões de desenvolvimento de um aplicativo web ou portais de administração. Em vez disso, o registro DNS pode ser mantido em um servidor DNS privado ou registrado nas máquinas do desenvolvedor em seu arquivo /etc/hosts (ou c:\windows\system32\drivers\etc\hosts para usuários do Windows), que mapeia nomes de domínio para endereços IP. 

Como os servidores web podem hospedar vários sites em um único servidor, quando um site é solicitado por um cliente, o servidor sabe qual site o cliente deseja acessar através do cabeçalho Host. Podemos utilizar esse cabeçalho Host modificando-o e monitorando a resposta para verificar se descobrimos um novo site.

Assim como no ataque de força bruta de DNS , podemos automatizar esse processo usando uma lista de palavras com subdomínios comumente usados.

Inicie o AttackBox e, em seguida, tente o seguinte comando contra a máquina do Suporte de TI da Acme para descobrir um novo subdomínio.

 

ffuf
user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.144.207
O comando acima usa a opção -w para especificar a lista de palavras que vamos usar. A opção -H adiciona/edita um cabeçalho (neste caso, o cabeçalho Host), temos a palavra-chave FUZZ no espaço onde normalmente estaria um subdomínio, e é aqui que vamos testar todas as opções da lista de palavras.

Como o comando acima sempre produzirá um resultado válido, precisamos filtrar a saída. Podemos fazer isso usando o resultado do tamanho da página com a opção -fs . Edite o comando abaixo, substituindo {size} pelo valor de tamanho mais frequente do resultado anterior e teste-o no AttackBox.

ffuf
user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.144.207 -fs {size}
Este comando tem uma sintaxe semelhante à do primeiro, exceto pela opção -fs , que instrui o ffuf a ignorar quaisquer resultados que tenham o tamanho especificado.

O comando acima deveria ter revelado dois resultados positivos que não tínhamos encontrado antes.
