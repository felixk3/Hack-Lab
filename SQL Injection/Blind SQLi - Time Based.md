Baseado no tempo



Uma injeção SQL cega baseada em tempo é muito semelhante à injeção baseada em booleanos descrita acima, pois as mesmas requisições são enviadas, mas desta vez não há indicador visual de que suas consultas estão corretas ou incorretas. Em vez disso, o indicador de uma consulta correta é baseado no tempo que ela leva para ser concluída. Esse atraso é introduzido usando métodos internos, como  SLEEP(x),  juntamente com a instrução UNION. O método SLEEP() só será executado após uma instrução UNION SELECT bem-sucedida. 



Assim, por exemplo, ao tentar determinar o número de colunas em uma tabela, você usaria a seguinte consulta:



admin123' UNION SELECT SLEEP(5);--



Se não houver pausa no tempo de resposta, sabemos que a consulta não foi bem-sucedida, então, como nas tarefas anteriores, adicionamos outra coluna:



admin123' UNION SELECT SLEEP(5),2;--



Essa carga útil deveria ter produzido um atraso de 5 segundos, confirmando a execução bem-sucedida da instrução UNION e a existência de duas colunas.



Agora você pode repetir o processo de enumeração da  injeção SQL baseada em booleanos , adicionando o método SLEEP() à  instrução UNION SELECT  .
Se você estiver com dificuldades para encontrar o nome da tabela, a consulta abaixo pode te ajudar:


referrer=admin123' UNION SELECT SLEEP(5),2 where database() like 'u%';--
