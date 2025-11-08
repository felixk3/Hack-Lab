Vamos colocar em prática o que aprendemos sobre SSRF em um cenário fictício.



Durante uma análise de conteúdo no site de suporte de TI da Acme , encontramos dois novos endpoints   . O primeiro é  /private , que exibe uma mensagem de erro informando que o conteúdo não pode ser visualizado a partir do nosso endereço IP. O segundo é uma nova versão da página de conta do cliente em  /customers/new-account-page,  com um novo recurso que permite aos clientes escolher um avatar para sua conta.



Comece clicando no  botão Iniciar Máquina  para abrir o  site de suporte de TI da Acme  . Depois de aberto, acesse o endereço  https://LAB_WEB_URL.p.thmlabs.com  e siga as instruções abaixo para obter a flag.



Primeiro, crie uma conta de cliente e faça login. Depois de fazer login, acesse  https://LAB_WEB_URL.p.thmlabs.com/customers/new-account-page para visualizar o novo recurso de seleção de avatar. Ao visualizar o código-fonte da página do formulário de avatar, você verá que o valor do campo de avatar contém o caminho para a imagem. O estilo background-image confirma isso no elemento DIV acima, conforme a captura de tela abaixo:







Se você escolher um dos avatares e clicar no  botão Atualizar Avatar  , verá o formulário mudar e, acima dele, exibir o avatar selecionado.








Ao visualizar o código-fonte da página, você verá que seu avatar atual é exibido usando o esquema URI de dados e que o conteúdo da imagem está codificado em base64, conforme a captura de tela abaixo.







Agora, vamos tentar fazer a solicitação novamente, mas alterando o valor do avatar para  privado  , na esperança de que o servidor acesse o recurso e ultrapasse o bloqueio de endereço IP. Para fazer isso, primeiro, clique com o botão direito do mouse em um dos botões de opção no formulário do avatar e selecione Inspecionar :







Em seguida, edite o valor do botão de opção para "privado":





Certifique-se de selecionar o avatar que você editou e clique no botão Atualizar Avatar . Infelizmente, parece que o aplicativo web possui uma lista de bloqueio e está impedindo o acesso ao endpoint /private.







Como você pode ver na mensagem de erro, o caminho não pode começar com /private, mas não se preocupe, ainda temos um truque na manga para contornar essa regra. Podemos usar um truque de travessia de diretório para alcançar o endpoint desejado. Tente definir o valor do avatar para  x/../private






Você verá que agora contornamos a regra e o usuário atualizou o avatar. Esse truque funciona porque, quando o servidor web recebe a solicitação para x/../private , ele sabe que a  string ../  significa subir um diretório, o que agora traduz a solicitação para apenas  /private .



Ao visualizar o código-fonte da página do formulário de avatar, você verá que o avatar atualmente definido contém o conteúdo do  diretório /private  em codificação base64. Decodifique esse conteúdo e ele revelará uma flag que você pode inserir abaixo.

