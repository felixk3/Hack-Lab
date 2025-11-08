O que é SQL Injection?
O ponto em que uma aplicação web que utiliza SQL pode se tornar vulnerável a SQL Injection é quando dados fornecidos pelo usuário são incluídos na consulta SQL .

Como isso se parece?
Considere o seguinte cenário: você encontrou um blog online, e cada postagem possui um número de ID exclusivo. As postagens podem ser públicas ou privadas, dependendo se estão prontas para publicação. A URL de cada postagem pode ser algo como:

https://website.thm/blog?id=1

A partir da URL acima, você pode ver que a postagem selecionada vem do parâmetro `id` na string de consulta. O aplicativo web precisa recuperar o artigo do banco de dados e pode usar uma instrução SQL semelhante a esta:

SELECT * from blog where id=1 and private=0 LIMIT 1;

Com base no que você aprendeu na tarefa anterior, você deve ser capaz de deduzir que a instrução SQL acima está procurando na tabela do blog um artigo com o número de ID 1 e a coluna `private` definida como 0, o que significa que ele pode ser visualizado publicamente e limita os resultados a apenas uma correspondência.

Como mencionado no início desta tarefa, a injeção de SQL ocorre quando a entrada do usuário é inserida na consulta do banco de dados. Neste caso, o parâmetro `id` da string de consulta é usado diretamente na consulta SQL .

Vamos supor que o artigo com ID 2 ainda esteja bloqueado como privado, portanto não pode ser visualizado no site. Podemos então acessar a URL:
 
https://website.thm/blog?id=2;--

Que, por sua vez, produziria a seguinte instrução SQL:

SELECT * from blog where id=2;-- and private=0 LIMIT 1;

O ponto e vírgula na URL indica o fim da instrução SQL , e os dois hífens fazem com que tudo o que vier depois seja tratado como um comentário . Fazendo isso, você está, na verdade, executando a consulta:

SELECT * from blog where id=2;--

Que retornará o artigo com ID 2, independentemente de estar definido como público ou não.

Este foi apenas um exemplo de uma vulnerabilidade de injeção de SQL do tipo In-Band ; existem três tipos no total: In-Band, Blind e Out-of-Band, que discutiremos nas próximas tarefas.
