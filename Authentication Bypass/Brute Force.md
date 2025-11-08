Usando o arquivo valid_usernames.txt que geramos na tarefa anterior, podemos agora tentar um ataque de força bruta na página de login ( http ://10.10.155.180/customers/login ).

Observação: Se você criou seu arquivo valid_usernames redirecionando a saída do ffuf diretamente, poderá ter dificuldades com esta tarefa. Limpe seus dados ou copie apenas os nomes para um novo arquivo.



Um ataque de força bruta é um processo automatizado que tenta uma lista de senhas comuns contra um único nome de usuário ou, como no nosso caso, contra uma lista de nomes de usuário.



Ao executar este comando, certifique-se de que o terminal esteja no mesmo diretório que o arquivo valid_usernames.txt.



Força bruta com ffuf
user@tryhackme$ ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.155.180/customers/login -fc 200
Este comando ffuf é um pouco diferente do anterior, da Tarefa 2. Anteriormente, usamos a palavra-chave FUZZ para selecionar onde, na requisição, os dados das listas de palavras seriam inseridos. No entanto, como estamos usando várias listas de palavras, precisamos especificar nossa própria palavra-chave FUZZ. Neste caso, escolhemos `<nome_de_usuário>` W1para nossa lista de nomes de usuário válidos e `<senha>` W2para a lista de senhas que tentaremos. As múltiplas listas de palavras são especificadas novamente com o -wargumento `<lista_de_palavras>`, mas separadas por vírgula. Para uma correspondência positiva, usamos o -fcargumento `<código_de_status>` para verificar se o código de status HTTP é diferente de 200.
