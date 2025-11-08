Nesta tarefa, forneceremos uma breve visão geral dos seguintes termos:

Programa
Processo
Fio
Multithreading
Programas
Um programa é um conjunto de instruções para realizar uma tarefa específica. Você precisa executar o programa para alcançar o que deseja. A menos que você o execute, ele não fará nada e permanecerá como um conjunto de instruções estáticas.

Pense nisso como uma receita; você acabou de baixar uma nova receita de café que inclui uma variedade de ervas, como cardamomo e canela. Estas são as instruções:

1. Combine brewed coffee, cardamom, cinnamon, and cloves (if using) in a saucepan.
2. Heat the mixture over low heat for 5 minutes, stirring occasionally. Do not boil.
3. Strain the coffee into your mug.
4. Add milk if desired, and sweeten to taste with honey or sugar.
A menos que alguém execute as instruções acima, nenhum café será servido!

Compare isso ao nosso servidor minimalista "Olá, Mundo!" em Flask (Python). O código abaixo determina que o aplicativo ficará escutando na porta 8080 e responderá com uma página HTML de saudação minimalista contendo "Olá, Mundo!". No entanto, precisamos executar essas instruções (programa) antes de esperarmos receber qualquer página de saudação.

Observe que o código Flask abaixo é mostrado apenas para fins demonstrativos. Não fornecemos um ambiente para executá-lo, pois está fora do escopo desta sala.

# Import the Flask class from the flask module
from flask import Flask

# Create an instance of the Flask class representing the application
app = Flask(__name__)

# Define a route for the root URL ('/')
@app.route('/')
def hello_world():
    # This function will be executed when the root URL is accessed
    # It returns a string containing HTML code for a simple web page
    return '<html><head><title>Greeting</title></head><body><h1>Hello, World!</h1></body></html>'

# This checks if the script is being run directly (as the main program)
# and not being imported as a module
if __name__ == '__main__':
    # Run the Flask application
    # The host='0.0.0.0' allows the server to be accessible from any IP address
    # The port=8080 specifies the port number on which the server will listen
    app.run(host='0.0.0.0', port=8080)
Processos
Certa tarde, você decide experimentar uma nova receita de café que baixou da internet. Você começa a seguir a receita passo a passo. Você está no processo de preparar o café. Enquanto está "executando" as "instruções", você pode ser interrompido por uma ligação urgente. Ou pode estar trabalhando em outra tarefa enquanto espera a água esquentar. Interrupções e esperas são geralmente inevitáveis. O ato de seguir as instruções da receita para fazer café é semelhante ao processo de executar instruções de um programa.

Um processo é um programa em execução. Em algumas publicações, você pode encontrar o termo " tarefa" . Ambos os termos se referem à mesma coisa, embora o termo "processo" tenha substituído o termo "tarefa". Ao contrário de um programa, que é estático, um processo é uma entidade dinâmica. Ele possui vários aspectos fundamentais, em particular:

Programa : O código executável relacionado ao processo.
Memória : Armazenamento temporário de dados
Estado : Um processo geralmente alterna entre diferentes estados. Após estar no estado Novo, ou seja, recém-criado, ele passa para o estado Pronto, ou seja, pronto para ser executado assim que receber tempo de CPU . Assim que a CPU aloca tempo para ele, ele entra no estado Executando. Além disso, ele pode estar no estado Aguardando, aguardando a conclusão de E/S ou de um evento. Ao ser finalizado, ele passa para o estado Terminado.
Diagrama de estados mostrando os 5 estados de um processo: Novo, Pronto, Em Execução, Aguardando e Terminado.

Se você executar o código Flask acima, um processo será criado e ficará aguardando conexões de entrada na porta 8080. Em outras palavras, ele passará a maior parte do tempo no estado de espera (Waiting). Quando receber uma requisição HTTP GET / , ele mudará para o estado pronto (Ready), aguardando sua vez de executar, de acordo com o agendamento da CPU . Uma vez no estado em execução (Running), ele enviará a página HTML para o cliente e retornará ao estado de espera.

Do ponto de vista do servidor, o aplicativo atende os clientes sequencialmente, ou seja, as solicitações dos clientes são processadas uma de cada vez. (Observe que o Flask é multithread por padrão desde a versão 1.0. Usamos o argumento --without-threadspara forçá-lo a executar em thread única.)

Observe que o comando Flask mostrado abaixo é apenas para fins demonstrativos.

terminal
$ flask run --without-threads --host=0.0.0.0
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://192.168.0.104:5000
Press CTRL+C to quit
127.0.0.1 - - [16/Apr/2024 23:34:46] "GET / HTTP/1.1" 200 -
127.0.0.1 - - [16/Apr/2024 23:34:48] "GET / HTTP/1.1" 200 -
127.0.0.1 - - [16/Apr/2024 23:35:11] "GET / HTTP/1.1" 200 -
Fios
Vamos finalizar com outra analogia do café! Considere o caso de uma máquina de expresso comercial em uma cafeteria. Digamos que ela tenha dois porta-filtros. No início do expediente, o barista liga a máquina de expresso e, sempre que um cliente pede um expresso, um dos porta-filtros é usado para preparar a dose. Outro cliente pede um expresso? Sem problemas, o segundo porta-filtro entra em ação! A máquina de expresso aquecida representa o processo; cada novo pedido recebe um porta-filtro; essa é a analogia para este tópico.

Uma máquina de café expresso com 1 porta-filtro e 3 xícaras na fila versus uma máquina de café expresso com 2 porta-filtros, onde as 2 xícaras são preenchidas simultaneamente.

Uma thread é uma unidade de execução leve. Ela compartilha diversas partes da memória e instruções com o processo.

Em muitos casos, precisamos replicar o mesmo processo repetidamente. Pense em um servidor web servindo a mesma página (ou uma página personalizada) para milhares de usuários. Podemos adotar uma das duas abordagens principais:

Serial: Um processo está em execução; ele atende um usuário após o outro sequencialmente. Novos usuários são enfileirados.
Paralelo: Um processo está em execução; ele cria uma thread para atender cada novo usuário. Novos usuários só são enfileirados depois que o número máximo de threads em execução for atingido.
O aplicativo anterior pode ser executado com quatro threads usando o Gunicorn. O Gunicorn, também chamado de "Unicórnio Verde", é um servidor HTTP WSGI para Python . WSGI significa Web Server Gateway Interface, que faz a ponte entre servidores web e aplicações web em Python. Em particular, o Gunicorn pode criar múltiplos processos de trabalho para lidar com requisições recebidas simultaneamente. Ao executar gunicorncom a --workers=4opção `--thread`, especificamos que queremos quatro processos de trabalho prontos para lidar com as requisições dos clientes; além disso, `--thread` --threads=2indica que cada processo de trabalho pode criar duas threads.

Observe que o comando Gunicorn mostrado abaixo é apenas para fins demonstrativos. Não fornecemos um ambiente para executá-lo, pois está fora do escopo desta sala.

terminal
gunicorn --workers=4 --threads=2 -b 0.0.0.0:8080 app:app
[2024-04-16 23:35:59 +0300] [507149] [INFO] Starting gunicorn 21.2.0
[2024-04-16 23:35:59 +0300] [507149] [INFO] Listening at: http://0.0.0.0:8080 (507149)
[2024-04-16 23:35:59 +0300] [507149] [INFO] Using worker: gthread
[2024-04-16 23:35:59 +0300] [507150] [INFO] Booting worker with pid: 507150
[2024-04-16 23:35:59 +0300] [507151] [INFO] Booting worker with pid: 507151
[2024-04-16 23:35:59 +0300] [507152] [INFO] Booting worker with pid: 507152
[2024-04-16 23:35:59 +0300] [507153] [INFO] Booting worker with pid: 507153
Vale a pena destacar o seguinte:

É impossível executar mais de uma cópia desse processo, pois ele se vincula à porta TCP 8080. Uma porta TCP ou UDP só pode ser vinculada a um processo.
O processo pode ser configurado com qualquer número de threads, e as solicitações HTTP que chegam à porta 8080 serão enviadas para as diferentes threads.
