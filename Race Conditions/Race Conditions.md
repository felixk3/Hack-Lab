Analogia com o mundo real
Imagine a seguinte situação: você liga para um restaurante para reservar uma mesa para um importante almoço de negócios. Você conhece o restaurante e sua estrutura. Uma mesa em particular, a de número 17, é a sua preferida, pois tem uma bela vista e é relativamente reservada. Você liga para fazer a reserva da mesa 17; o recepcionista confirma que ela está livre, pois não há nenhuma etiqueta de "Reservada" nela. Ao mesmo tempo, outro cliente está conversando com outro recepcionista e fazendo uma reserva para a mesma mesa.

Duas recepcionistas em um restaurante. Elas estão conversando ao telefone e ambas olham para a mesma mesa. A mesa em questão tem o número 17.

Quem realmente reservou a mesa? Isso é uma condição da corrida.

Por que isso aconteceu? Essa situação infeliz ocorreu porque mais de um anfitrião estava aceitando reservas; além disso, o anfitrião levou alguns minutos para pegar a etiqueta de "Reservado" e colocá-la na mesa após atualizar o livro de reservas diário. Há uma janela de pelo menos um minuto para que outro cliente reserve uma mesa que já estava reservada.

Da mesma forma, quando uma thread verifica um valor para executar uma ação, outra thread pode alterar esse valor antes que a ação ocorra.

Exemplo A
Vamos considerar o seguinte cenário:

Uma conta bancária possui 100 dólares.
Duas threads tentam sacar dinheiro ao mesmo tempo.
O usuário Thread 1 verifica o saldo (vê $100) e retira $45.
Antes que a Thread 1 atualize o saldo , a Thread 2 também verifica o saldo (enxergando incorretamente $100) e retira $35.
Não podemos ter 100% de certeza de qual thread atualizará o saldo restante primeiro; no entanto, vamos supor que seja a Thread 1. A Thread 1 definirá o saldo restante para US$ 55. Posteriormente, a Thread 2 poderá definir o saldo restante para US$ 65, caso não seja tratada adequadamente. (A Thread 2 calculou que US$ 65 deveriam permanecer na conta após o saque, pois o saldo era de US$ 100 quando a Thread 2 verificou.) Em outras palavras, o usuário fez dois saques, mas o saldo da conta foi deduzido apenas no segundo saque, porque a Thread 2 assim o determinou!

Exemplo B
Vamos considerar outro cenário:

Uma conta bancária possui 75 dólares.
Duas threads tentam sacar dinheiro ao mesmo tempo.
O usuário Thread 1 verifica o saldo (vê $75) e retira $50.
Antes que a Thread 1 atualize o saldo , a Thread 2 verifica o saldo (encontrando incorretamente $75) e retira $50.
A segunda thread prosseguirá com o saque, embora tal transação devesse ter sido recusada.

Os exemplos A e B demonstram uma vulnerabilidade de tempo de verificação para tempo de uso (TOCTOU).

Código de exemplo
Considere o seguinte código Python com duas threads simulando a conclusão de uma tarefa em incrementos de 10%.

import threading

x = 0  # Shared variable

def increase_by_10():
    global x
    for i in range(1, 11):
        x += 1
        print(f"Thread {threading.current_thread().name}: {i}0% complete, x = {x}")

# Create two threads
thread1 = threading.Thread(target=increase_by_10, name="Thread-1")
thread2 = threading.Thread(target=increase_by_10, name="Thread-2")

# Start the threads
thread1.start()
thread2.start()

# Wait for both threads to finish
thread1.join()
thread2.join()

print("Both threads have finished completely.")
Essas duas threads iniciam juntas; elas não fazem nada além de imprimir um valor na tela. Consequentemente, seria de se esperar que elas terminassem simultaneamente, ou pelo menos que o resultado fosse consistente. No entanto, no programa acima, não há garantia de qual thread terminará primeiro e quão cedo isso ocorrerá. Abaixo está a saída da primeira execução:

terminal
python t3_race_to_100.py
...
Thread Thread-1: 40% complete, x = 10
Thread Thread-2: 70% complete, x = 11
Thread Thread-1: 50% complete, x = 12
Thread Thread-2: 80% complete, x = 13
Thread Thread-1: 60% complete, x = 14
Thread Thread-1: 70% complete, x = 16
Thread Thread-2: 90% complete, x = 15
Thread Thread-2: 100% complete, x = 17
Thread Thread-1: 80% complete, x = 18
Thread Thread-1: 90% complete, x = 19
Thread Thread-1: 100% complete, x = 20
Both threads have finished completely.
Abaixo segue o resultado de uma segunda execução:

terminal
python t3_race_to_100.py 
...
Thread Thread-1: 70% complete, x = 10
Thread Thread-2: 40% complete, x = 11
Thread Thread-1: 80% complete, x = 12
Thread Thread-2: 50% complete, x = 13
Thread Thread-1: 90% complete, x = 14
Thread Thread-2: 60% complete, x = 15
Thread Thread-1: 100% complete, x = 16
Thread Thread-2: 70% complete, x = 17
Thread Thread-2: 80% complete, x = 18
Thread Thread-2: 90% complete, x = 19
Thread Thread-2: 100% complete, x = 20
Both threads have finished completely.
Executar este programa várias vezes levará a resultados diferentes. Na primeira tentativa, a Thread-2 atingiu 100 primeiro; no entanto, na segunda tentativa, a Thread-2 atingiu 100 em segundo lugar. Não temos controle sobre a saída. Se a segurança da nossa aplicação depende de uma thread terminar antes da outra, então precisamos implementar mecanismos para garantir a proteção adequada. Considere os dois exemplos a seguir para entender melhor a gravidade dos bugs quando deixamos as coisas ao acaso.

No AttackBox, você pode salvar o código Python acima e executá-lo várias vezes para observar o resultado. Por exemplo, se você o salvou como race.py, pode executar o script usando o python race.pycomando.

Causas
Como vimos no programa anterior, duas threads estavam alterando a mesma variável. Sempre que uma thread recebia tempo de CPU , ela se apressava em incrementá-la xem 1. Consequentemente, essas duas threads estavam "competindo" para incrementar a mesma variável. Este programa mostra um exemplo simples que ocorre em um único host.

De modo geral, uma causa comum de condições de corrida reside em recursos compartilhados. Por exemplo, quando várias threads acessam e modificam simultaneamente os mesmos dados compartilhados. Exemplos de dados compartilhados são um registro de banco de dados e uma estrutura de dados em memória. Existem muitas causas sutis, mas mencionaremos três das mais comuns:

Execução paralela : Servidores web podem executar múltiplas requisições em paralelo para lidar com interações simultâneas de usuários. Se essas requisições acessarem e modificarem recursos compartilhados ou estados da aplicação sem a devida sincronização, isso pode levar a condições de corrida e comportamentos inesperados.
Operações de banco de dados : Operações simultâneas em bancos de dados, como sequências de leitura-modificação-escrita, podem introduzir condições de corrida. Por exemplo, dois usuários tentando atualizar o mesmo registro simultaneamente podem resultar em dados inconsistentes ou conflitos. A solução reside na aplicação de mecanismos de bloqueio adequados e isolamento de transações.
Bibliotecas e serviços de terceiros : Atualmente, os aplicativos da web frequentemente se integram a bibliotecas, APIs e outros serviços de terceiros. Se esses componentes externos não forem projetados para lidar adequadamente com o acesso simultâneo, podem ocorrer condições de corrida quando várias solicitações ou operações interagirem com eles ao mesmo tempo.
