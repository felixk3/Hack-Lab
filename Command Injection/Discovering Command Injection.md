Essa vulnerabilidade existe porque os aplicativos frequentemente usam funções em linguagens de programação como PHP , Python e NodeJS para passar dados e fazer chamadas de sistema no sistema operacional da máquina. Por exemplo, ao receber dados de um campo e buscar uma entrada em um arquivo. Veja o trecho de código abaixo como exemplo:

Neste trecho de código, o aplicativo recebe dados que um usuário insere em um campo de entrada chamado$title Para pesquisar o título de uma música em um diretório, vamos dividir isso em algumas etapas simples.



1. O aplicativo armazena arquivos MP3 em um diretório contido no sistema operacional.

2. O usuário insere o título da música que deseja pesquisar. O aplicativo armazena essa entrada na $titlevariável.

3. Os dados contidos nesta $titlevariável são passados ​​para o comando grepque busca em um arquivo de texto chamado songtitle.txt a entrada que o usuário deseja pesquisar.

4. O resultado desta busca no arquivo songtitle.txt determinará se o aplicativo informa ao usuário que a música existe ou não.

Normalmente, esse tipo de informação seria armazenado em um banco de dados; no entanto, este é apenas um exemplo de como um aplicativo recebe dados do usuário para interagir com o sistema operacional do aplicativo.

Um atacante poderia explorar essa aplicação injetando seus próprios comandos para que a aplicação os executasse. Em vez de usar a função greppara buscar uma entrada em um arquivo songtitle.txt, ele poderia solicitar que a aplicação lesse dados de um arquivo mais sensível.

Abusar de aplicativos dessa forma é possível independentemente da linguagem de programação utilizada. Desde que o aplicativo processe e execute o comando, pode resultar em injeção de comandos . Por exemplo, o trecho de código abaixo é de um aplicativo escrito em Python.



Observe que não se espera que você entenda a sintaxe por trás desses aplicativos. No entanto, para fins de compreensão, descrevi os passos de funcionamento deste aplicativo em Python.

O pacote "flask" é usado para configurar um servidor web.
Uma função que utiliza o pacote "subprocess" para executar um comando no dispositivo.
Usamos uma rota no servidor web que executará o que for fornecido. Por exemplo, para executar , precisaríamos whoamiacessar http ://flaskapp.thm/whoami
