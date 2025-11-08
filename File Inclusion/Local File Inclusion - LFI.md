Inclusão de Arquivo Local ( LFI )
Ataques LFI contra aplicações web são frequentemente causados ​​pela falta de conhecimento em segurança por parte dos desenvolvedores. Em PHP , o uso de funções como `include` , ` require` , `include_once` e `require_once` muitas vezes contribui para a vulnerabilidade das aplicações web. Nesta sessão, focaremos no PHP , mas vale ressaltar que vulnerabilidades LFI também ocorrem em outras linguagens, como ASP, JSP ou até mesmo em aplicações Node.js. Os exploits LFI seguem os mesmos princípios da exploração de caminhos (path traversal).

Nesta seção, vamos apresentar vários  cenários de LFI (Infração  de Baixa Infraestrutura) e como explorá-los.

#1. Suponha que o aplicativo web ofereça dois idiomas e que o usuário possa escolher entre inglês (  EN)  e  árabe (AR).

<?PHP 
	include($_GET["lang"]);
?>
 
O código PHP acima utiliza uma requisição GET através do parâmetro de URL `lang` para incluir o arquivo da página. A chamada pode ser feita enviando a seguinte requisição HTTP : http://webapp.thm/index.php?lang=EN.phppara carregar a página em inglês ou http://webapp.thm/index.php?lang=AR.phppara carregar a página em árabe, onde os arquivos `EN.php` e ` AR.php` existem  no mesmo diretório.

Teoricamente, podemos acessar e exibir qualquer arquivo legível no servidor a partir do código acima, desde que não haja validação de entrada. Digamos que queremos ler um /etc/passwdarquivo que contenha informações confidenciais sobre os usuários do sistema operacional Linux; podemos tentar o seguinte:http://webapp.thm/get.php?file=/etc/passwd

Neste caso, funciona porque não há um diretório especificado na função include e nenhuma validação de entrada.

Agora, aplique o que discutimos e tente ler o arquivo /etc/passwd. Além disso, responda à pergunta nº 1 abaixo.

#2.  Em seguida, no código a seguir, o desenvolvedor decidiu especificar o diretório dentro da função.

 

<?PHP 
	include("languages/". $_GET['lang']); 
?>
No código acima, o desenvolvedor decidiu usar a   função  include para chamar páginas PHP  no  diretório languages  ​​somente através de  parâmetros lang  .

Se não houver validação de entrada, o atacante pode manipular a URL substituindo o  parâmetro `lang`  por outros arquivos sensíveis ao sistema operacional, como  `/etc/passwd` .

Novamente, a carga útil parece semelhante à de um  ataque de travessia de diretório , mas a função `include` nos permite incluir quaisquer arquivos chamados na página atual. A seguir, o exploit:

http ://webapp.thm/index.php ? lang = .. /../../../etc/ passwd

Agora, aplique o que discutimos, tente ler arquivos dentro do servidor e descubra o diretório especificado na função include para responder à pergunta nº 2 abaixo.
