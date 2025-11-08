Remediação

Por mais impactantes que sejam as vulnerabilidades de injeção de SQL , os desenvolvedores têm uma maneira de proteger seus aplicativos da web contra elas, seguindo as dicas abaixo:



Instruções Preparadas (Com Consultas Parametrizadas):

Em uma consulta preparada, a primeira coisa que um desenvolvedor escreve é ​​a consulta SQL , e então quaisquer entradas do usuário são adicionadas como parâmetros posteriormente. Escrever instruções preparadas garante que a estrutura do código SQL não mude e que o banco de dados possa distinguir entre a consulta e os dados. Como benefício adicional, isso também torna seu código muito mais limpo e fácil de ler.



Validação de entrada:

A validação de entrada é fundamental para proteger os dados inseridos em uma consulta SQL . O uso de uma lista de permissões pode restringir a entrada a determinadas strings, ou um método de substituição de strings na linguagem de programação pode filtrar os caracteres que você deseja permitir ou bloquear. 



Escapando da entrada do usuário:

Permitir a entrada de dados do usuário contendo caracteres como ' " $ \ pode fazer com que as consultas SQL falhem ou, pior ainda, como aprendemos, torná-las vulneráveis ​​a ataques de injeção. Escapar a entrada do usuário é o método de adicionar uma barra invertida ( \ ) antes desses caracteres, o que faz com que sejam interpretados como uma string normal e não como um caractere especial.
