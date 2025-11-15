Na tarefa anterior, demonstramos o uso do Repeater adicionando um cabeçalho e enviando uma requisição. Isso serviu como um exemplo ilustrativo de como utilizar o Repeater. Agora, é hora de um desafio mais simples!

Para começar, certifique-se de que a interceptação esteja desativada no seu módulo Proxy e navegue até http://MACHINE_IP/products/. Em seguida, tente clicar em alguns dos links "Ver mais" .

Observe que você será redirecionado para um endpoint numérico (por exemplo, /products/3).

O objetivo é validar o ponto de extremidade, confirmando a existência do número para o qual você deseja navegar e garantindo que ele seja um número inteiro válido. No entanto, considere o que pode ocorrer se esse ponto de extremidade não for validado adequadamente.
