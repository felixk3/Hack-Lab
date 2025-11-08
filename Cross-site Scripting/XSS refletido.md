XSS refletido

O XSS refletido ocorre quando dados fornecidos pelo usuário em uma solicitação HTTP são incluídos no código-fonte da página da web sem qualquer validação.


Cenário de exemplo:

Um site onde, se você inserir dados incorretos, uma mensagem de erro é exibida. O conteúdo da mensagem de erro é obtido do parâmetro de erro na string de consulta e incorporado diretamente ao código-fonte da página.





O aplicativo não verifica o conteúdo do parâmetro de erro , o que permite ao atacante inserir código malicioso.







A vulnerabilidade pode ser explorada conforme o cenário ilustrado na imagem abaixo:



Impacto potencial:

O atacante poderia enviar links ou incorporá-los em um iframe em outro site, contendo um código JavaScript malicioso, para que as vítimas em potencial executem o código em seus navegadores, o que pode revelar informações de sessão ou do cliente.

Como testar XSS refletido :

Você precisará testar todos os pontos de entrada possíveis; estes incluem:

Parâmetros na string de consulta da URL
Caminho do arquivo URL
Às vezes, os cabeçalhos HTTP (embora seja improvável que sejam exploráveis ​​na prática)
Depois de encontrar alguns dados que estão sendo refletidos no aplicativo web, você precisará confirmar se consegue executar com sucesso seu código JavaScript; o código que você usar dependerá de onde ele está inserido no aplicativo (você aprenderá mais sobre isso na tarefa 6).
