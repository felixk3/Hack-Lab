Onde eles estão localizados?
O endpoint vulnerável que você está visando pode não ser necessariamente algo que você vê na barra de endereços. Pode ser conteúdo carregado pelo seu navegador por meio de uma requisição AJAX ou algo referenciado em um arquivo JavaScript. 



Às vezes, os endpoints podem ter um parâmetro não referenciado que pode ter sido útil durante o desenvolvimento e acabou sendo implementado em produção. Por exemplo, você pode notar uma chamada para  /user/details  exibindo suas informações de usuário (autenticado por meio de sua sessão). Mas, por meio de um ataque conhecido como mineração de parâmetros, você descobre um parâmetro chamado user_id que pode ser usado para exibir as informações de outros usuários, por exemplo, /user/details?user_id=123 .
