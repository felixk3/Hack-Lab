Nesta tarefa, vamos nos aprofundar um pouco mais em LFI . Discutimos algumas técnicas para contornar o filtro dentro da função include.

#3. Nos dois primeiros casos, analisamos o código do aplicativo web e, assim, soubemos como explorá-lo. No entanto, neste caso, estamos realizando testes de caixa preta, nos quais não temos acesso ao código-fonte. Nesse caso, os erros são cruciais para entendermos como os dados são transmitidos e processados ​​no aplicativo web.

Neste cenário, temos o seguinte ponto de entrada: http://webapp.thm/index.php?lang=EN. Se inserirmos um valor inválido, como THM , receberemos o seguinte erro.

Warning: include(languages/THM.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12
A mensagem de erro revela informações importantes. Ao inserir THM como entrada, uma mensagem de erro mostra como a função include se parece: include(languages/THM.php);.

Se você observar o diretório atentamente, podemos ver que a função inclui arquivos no diretório de idiomas adicionando .php ao final da entrada. Assim, a entrada válida será algo como: index.php?lang=EN, onde o arquivo EN está localizado dentro do diretório de idiomas especificado e tem o nome EN.php.

Além disso, a mensagem de erro revelou outra informação importante sobre o caminho completo do diretório da aplicação web, que é /var/www/html/THM-4/.

Para explorar isso, precisamos usar o ../truque, conforme descrito na seção de travessia de diretórios, para sair da pasta atual. Vamos tentar o seguinte:

http://webapp.thm/index.php?lang=../../../../etc/passwd

Note que usamos 4 ../porque sabemos que o caminho tem quatro níveis /var/www/html/THM-4. Mas ainda recebemos o seguinte erro:

Warning: include(languages/../../../../../etc/passwd.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12
Parece que poderíamos sair do diretório PHP , mas mesmo assim, a função include lê a entrada com um caractere nulo .phpno final! Isso nos indica que o desenvolvedor especificou o tipo de arquivo a ser passado para a função include. Para contornar esse cenário, podemos usar o byte nulo, que é %00.

O uso de bytes nulos é uma técnica de injeção que consiste em utilizar uma representação codificada em URL, como %00 ou 0x00 em hexadecimal, com dados fornecidos pelo usuário para finalizar strings. Pode-se pensar nisso como uma tentativa de enganar o aplicativo web para que ele ignore tudo o que vier depois do byte nulo.

Ao adicionar o byte nulo ao final da carga útil, instruímos a função de inclusão a ignorar tudo o que estiver após o byte nulo, que pode ter a seguinte aparência:

include("languages/../../../../../etc/passwd%00").".php");que é equivalente ainclude("languages/../../../../../etc/passwd");

Observação: o truque do %00 foi corrigido e não funciona com o PHP 5.3.4 e versões superiores.

Agora, aplique o que mostramos no Laboratório #3 e tente ler os arquivos em /etc/passwd. Responda à pergunta #1 abaixo.

#4. Nesta seção, o desenvolvedor decidiu filtrar palavras-chave para evitar a divulgação de informações confidenciais! O arquivo /etc/passwd está sendo filtrado. Existem dois métodos possíveis para contornar o filtro. Primeiro, usando o NullByte %00 ou o truque do diretório atual no final da palavra-chave filtrada. /..O exploit será semelhante a http://webapp.thm/index.php?lang=/etc/passwd/. Também poderíamos usar http://webapp.thm/index.php?lang=/etc/passwd%00.

Para ficar mais claro, se tentarmos esse conceito no sistema de arquivos usando cd ..`cd`, ele nos levará um passo para trás; no entanto, se fizermos `cd` cd ., ele permanecerá no diretório atual. Da mesma forma, se tentarmos `cd` /etc/passwd/.., o resultado será `cd` /etc/, e isso ocorre porque movemos um passo para a raiz. Agora, se tentarmos `cd` /etc/passwd/., o resultado será `cd`, /etc/passwdjá que o ponto se refere ao diretório atual.

Agora aplique essa técnica no Laboratório #4 e descubra como ler o arquivo /etc/passwd.

#5. Em seguida, nos cenários a seguir, o desenvolvedor começa a usar a validação de entrada filtrando algumas palavras-chave. Vamos testar e verificar a mensagem de erro!

http://webapp.thm/index.php?lang=../../../../etc/passwd

Recebemos o seguinte erro!

Warning: include(languages/etc/passwd): failed to open stream: No such file or directory in /var/www/html/THM-5/index.php on line 15
Se verificarmos a mensagem de aviso na include(languages/etc/passwd)seção, saberemos que a aplicação web substitui o valor ../por uma string vazia. Existem algumas técnicas que podemos usar para contornar isso.

Primeiro, podemos enviar a seguinte carga útil para contorná-lo: ....//....//....//....//....//etc/passwd.

Por que isso funcionou?

Isso funciona porque o filtro PHP só encontra e substitui o primeiro subconjunto de strings ../que corresponde, sem fazer uma segunda verificação, resultando no que é mostrado abaixo.


Experimente o Laboratório #5 e tente ler o arquivo /etc/passwd e contornar o filtro!

#6. Finalmente, discutiremos o caso em que o desenvolvedor força a inclusão a ler de um diretório definido! Por exemplo, se o aplicativo da web solicitar uma entrada que inclua um diretório como: http://webapp.thm/index.php?lang=languages/EN.phpentão, para explorar isso, precisamos incluir o diretório no payload da seguinte forma: ?lang=languages/../../../../../etc/passwd.
