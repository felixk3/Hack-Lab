Detecção
Detectar condições de corrida da perspectiva do dono da empresa pode ser um desafio. Se alguns usuários resgatarem o mesmo cartão-presente várias vezes, isso provavelmente passará despercebido, a menos que os registros sejam verificados ativamente em busca de certos comportamentos. Considerando que as condições de corrida podem ser usadas para explorar vulnerabilidades ainda mais sutis, fica claro que precisamos da ajuda de testadores de penetração e caçadores de bugs para tentar descobrir essas vulnerabilidades e relatar suas descobertas.

Os testadores de penetração precisam entender como o sistema se comporta em condições normais quando os controles são aplicados. Esses controles podem ser: usar uma vez, votar uma vez, avaliar uma vez, limitar para equilibrar e limitar a uma ação a cada 5 minutos, entre outros. O próximo passo seria tentar contornar esse limite explorando condições de corrida. Compreender os diferentes estados do sistema pode nos ajudar a fazer estimativas fundamentadas sobre as janelas de tempo em que uma condição de corrida pode ser explorada. Ferramentas como o Burp Suite Repeater podem ser um ótimo ponto de partida.

Mitigação
Listaremos algumas técnicas de mitigação.

Mecanismos de sincronização : As linguagens de programação modernas fornecem mecanismos de sincronização, como bloqueios (locks). Apenas uma thread pode adquirir o bloqueio por vez, impedindo que outras acessem o recurso compartilhado até que ele seja liberado.
Operações Atômicas : Operações atômicas referem-se a unidades de execução indivisíveis, um conjunto de instruções agrupadas e executadas sem interrupção. Essa abordagem garante que uma operação possa ser concluída sem ser interrompida por outra thread.
Transações de banco de dados : Transações agrupam múltiplas operações de banco de dados em uma única unidade. Consequentemente, todas as operações dentro da transação são concluídas com sucesso como um grupo ou falham como um grupo. Essa abordagem garante a consistência dos dados e evita condições de corrida resultantes de múltiplos processos modificando o banco de dados simultaneamente.
