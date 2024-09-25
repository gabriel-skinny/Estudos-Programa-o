# 4 - Entendendo BackEnd - Concorrencia e Paralelismo - 1

Evolução do Hardware no Mundo de Hoje: Estamos em um mundo massivamente paralelo, com CPU com mais de 48 threads.

## História da Computação

Jobs e Batches: Cada fita de um programa era um job para ser executado pela CPU, que os rodava em batches, um fila que os executava um atrás do outro.

Inicio do Paralelismo time-sharing com context-switching: Começaram a usar o tempo que a maquina usava para escrever o output ou ler uma fita, para executar outro job. Para isso era preciso salvar o contexto de cada Job e alterna-los rapidamente, de modo que parecia que um Job estava sozinho executando. A maquina vai dando um time-slice de execução para cada job, e vai alternando entre eles.

Multitarefa comperativa em 1 core: Era usada no começo do windows, porém quando um programa travava e não dava a vez para outros programas, eles todos ficavam travados.

Multitarefa preemptiva: O Sistema operacional linux começou a criar processos que tem um contexto de memória protegida, e um scheduler que se responsabilizava para desalocar processos segundo um time-slice e colocar outros.

Multhithreading: Thread é um trecho de código, e em um CPU de um core, só pode ser executado um por vez. O scheduler continua tendo que alternar entre as threads. Porém elas possuem a memória compartilhada do processo, não precisando de um context-switching muito caro.

Problema de Multithreading race-condition: Uma thread usando o mesmo recurso que outra thread está usando.

Lock e Dead-Lock: Lock é uma trava colocada para um thread usar um recurso compartilhado. O dead-lock acontece quando uma thread acaba de usar um recurso mas esquece ou não consegue tirar o lock dele, deixando todas as outras threads que dele dependem paradas infinitamente.

Cpus modernas: Todos foram feitas para executarem threads, o seu contexto fica nos registradores. O ideal é ter o mesmo número de threads do que o número de Cores da CPU. Porém não é porque você tem 2 cores e 2 threads que elas vão rodar da forma mais eficiente, pois elas podem estar compartilhando o mesmo recurso, e uma thread precisará ficar esperando essa acabar. Então o número ideal de threads é por tentativa e erro.

Processos: O sistema operacional precisa fazer muitas coisas para criar processos. Em linux é muito mais rapido que em Windows, e o seu sitema de fork também é mais pesado. O desenvolvimento de Windows recomenda criar um processo e varias threads dentro deles para ter paralelismo.

Processos vs Threads: Threads ocupam bem menos memória pois compartilham a memória do processo, porém o processo tem boundaries de memória seguras, garantidas pelo sistema operacional, então não existem race-conditions e dead-locks, e a segurança é mais garantida.

Principio da Programação: É sempre se comprometer a perder uma coisa para ganhar outra.

Fork do Processo: É uma copia de tudo o que um processo tem na memória no momento do Fork, e cria-se outro processo isolado, e apartir dai cada um teria sua vida independente. Mas no linux existe o CoW(Copy on Write), em que um novo processo não usa nenhuma memória adicional, mas ele fica apontando para memória do processo original, e só coisas que o segundo processo começa a grava é que ficará na memória desse processo, isso tirá a necessidade de mutex, pois cada processo possui sua propria copia da memória. No windows o fork duplica a memória.

Scheduler do Linux CFS(Completly Fair Scheduler): Ele dá preferencias para aplicativos interativos

I/O: É qualquer dispositivo de Entrada e Saída. Se o barramento de I/O estiver limitado, não adianta ter 500 thraeds executando, se cada uma só consegue usar um barramento de I/O por vez. Isso são operações Blocking I/O. Conexões de Rede também são bloqueantes, uma thread trava o output e input de um barramento de I/O.

Asyncronous I/O: Uma thread indica que quer escrever algo no disco e o sistema operacional envia um evento quando terminou de escrever. Isso é programação orientada a eventos extendida a operações de I/O.

Soluções para responder requisições:

- Fork de Processo: Criar um fork para servir uma requisição. É muito caro para a memória
- Thread: Criar uma thread por requisição, o problema é gerenciar sua comunicação, e também context-switching não é tão barato de se ficar fazendo.
- I/O Assincrono com uma Treadh: Uma treahd envia multiplas requisições de I/O para o sistema operacional sem ficar bloqueado para receber outras requisições. O sistema operacional vai notifcando a thread conforme vai terminando.

NGNIX: Servidor Web mais escalável e rapido que temos até hoje. Ele tem um processo master que organiza seus workers, que normalmente são 1 por core da CPU, e cada worker consegue gerenciar milhares de sockets de conexão de navegadores requisitando paginas web, chamando a função epoll do linux para cadastrar a requisições, e executa um loop de eventos, que checka se eventos de termino chegaram. Assim o NGNIX consegue servir milhões de requisições simultaneamente sem precisar gastar memória criando processos ou CPU fazendo context-switching de threads.

Concorrência: São tarefas que se alternam entre si mas nunca rodam ao mesmo tempo

Paralelismo: Quando duas ou mais tarefas estão rodando ao mesmo tempo. Isso so é possivel em Cpus com mais de 1 core.

Resolução do Problema de Concorrencia e Paralelismo: Nunca tem resposta pronta, as 3 soluções cada uma tem seus pros e contras, que devem ser ponderados para resolver um problema especifico.
