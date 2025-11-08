A carga útil é o código JavaScript que queremos executar no navegador de outro usuário ou como prova de conceito para demonstrar uma vulnerabilidade em um site.

Sua carga útil pode ter várias intenções, desde simplesmente exibir uma caixa de alerta em JavaScript para provar que podemos executar JavaScript no site alvo até extrair informações da página da web ou da sessão do usuário.

A forma como sua carga útil em JavaScript se reflete no código do site alvo determinará a carga útil que você precisa usar. Para entender melhor, clique no botão verde "Iniciar Máquina" à direita e, quando a máquina carregar, abra o link abaixo em uma nova aba.

https://LAB_WEB_URL.p.thmlabs.com


O objetivo de cada nível será executar a função JavaScript alert com a string THM , por exemplo:

<script>alert('THM');</script>

Nível Um:

Será apresentado um formulário onde você deverá inserir seu nome e, após digitá-lo, ele será exibido em uma linha abaixo, por exemplo:



Se você visualizar o código-fonte da página, verá seu nome refletido no código:



Em vez de digitar seu nome, vamos tentar inserir o seguinte código JavaScript: <script>alert('THM');</script>

Agora, ao clicar no botão Enter, você verá um alerta com a string THM e o código-fonte da página ficará assim:




Em seguida, você receberá uma mensagem de confirmação informando que sua carga útil foi enviada com sucesso, com um link para o próximo nível.

Nível Dois:

Assim como no nível anterior, você deverá inserir seu nome novamente. Desta vez, ao clicar em Enter, seu nome será exibido em um campo de entrada:




Ao visualizar o código-fonte da página, você pode ver seu nome refletido no atributo `value` da tag de entrada:



Não funcionaria se você tentasse usar o código JavaScript anterior, pois não é possível executá-lo de dentro da tag de entrada. Em vez disso, precisamos escapar a tag de entrada primeiro para que o código possa ser executado corretamente. Você pode fazer isso com o seguinte código:"><script>alert('THM');</script>

A parte importante da carga útil é o ">que fecha o parâmetro de valor e, em seguida, fecha a tag de entrada.

Agora, isso fecha corretamente a tag de entrada e permite que o código JavaScript seja executado:



Agora, ao clicar no botão Enter, você verá uma janela de alerta com a string THM. Em seguida, você receberá uma mensagem de confirmação informando que sua carga útil foi enviada com sucesso, com um link para o próximo nível.


Nível Três:

Você se depara com outro formulário solicitando seu nome e, assim como no nível anterior, seu nome é exibido dentro de uma tag HTML, desta vez a tag textarea.



Teremos que escapar a tag textarea de uma maneira um pouco diferente da tag input (no Nível Dois), usando a seguinte carga útil:</textarea><script>alert('THM');</script>

Isso transforma isto em:



Nisto:



A parte importante da carga útil acima é </textarea>, que faz com que o elemento textarea se feche para que o script seja executado.

Agora, ao clicar no botão Enter, você verá uma janela de alerta com a string THM. Em seguida, você receberá uma mensagem de confirmação informando que sua carga útil foi enviada com sucesso, com um link para o próximo nível. Nível Quatro:



Ao inserir seu nome no formulário, você o verá refletido na página. Este nível é semelhante ao nível um, mas ao inspecionar o código-fonte da página, você verá que seu nome é refletido em um código JavaScript.



Você precisará escapar do comando JavaScript existente para poder executar seu código; você pode fazer isso com o seguinte payload, ';alert('THM');//  que, como você verá na captura de tela abaixo, executará seu código. O `\ 'n` fecha o campo que especifica o nome, o `\n` ;indica o fim do comando atual e o `\n` //no final transforma tudo o que vier depois dele em um comentário, em vez de código executável.



Agora, ao clicar no botão Enter, você verá uma janela de alerta com a string THM. Em seguida, você receberá uma mensagem de confirmação informando que sua carga útil foi enviada com sucesso, com um link para o próximo nível.


Nível Cinco:

Agora, este nível parece igual ao nível um, e seu nome também aparece no mesmo lugar. Mas se você tentar executar o <script>alert('THM');</script>payload, não funcionará. Ao visualizar o código-fonte da página, você entenderá o motivo.



A palavra script  é removida da sua carga útil porque existe um filtro que elimina quaisquer palavras potencialmente perigosas.

Quando uma palavra é removida de uma string, existe um truque útil que você pode tentar.

Carga útil original:
<sscriptcript>alert('THM');</sscriptcript>

Texto a ser removido (pelo filtro):
<sscriptcript>alert('THM');</sscriptcript>

Carga útil final (após passar pelo filtro):
<script>alert('THM');</script>


Tente inserir o payload <sscriptcript>alert('THM');</sscriptcript>e clique no botão Enter. Você receberá um alerta com a string THM . Em seguida, você receberá uma mensagem de confirmação informando que o payload foi inserido com sucesso, com um link para o próximo nível.

Nível Seis:


Semelhante ao nível dois, onde tivemos que escapar do atributo `value` de uma tag `input`, podemos tentar usar `\value` "><script>alert('THM');</script> , mas isso não parece funcionar. Vamos inspecionar o código-fonte da página para ver por que isso não funciona.



Você pode ver que os caracteres < e > são filtrados do nosso conteúdo, impedindo-nos de escapar da tag IMG. Para contornar o filtro, podemos aproveitar os atributos adicionais da tag IMG, como o evento onload. O evento onload executa o código de sua escolha assim que a imagem especificada no atributo src for carregada na página da web.

Vamos alterar nosso conteúdo para refletir isso /images/cat.jpg" onload="alert('THM');e, em seguida, visualizar o código-fonte da página. Você verá como isso funciona.



Ao clicar no botão Enter, você verá um alerta com a string THM . Em seguida, receberá uma mensagem de confirmação informando que o envio do payload foi bem-sucedido; como este é o último nível, você receberá um indicador que poderá ser inserido abaixo.

Poliglotas:



Um poliglota XSS é uma sequência de texto capaz de escapar de atributos, tags e contornar filtros, tudo em um só. Você poderia ter usado o poliglota abaixo em todos os seis níveis que acabou de concluir, e o código teria sido executado com sucesso.



jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e



