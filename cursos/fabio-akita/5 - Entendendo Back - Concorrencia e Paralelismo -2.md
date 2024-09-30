# 5 - Entendendo Back - Concorrencia e Paralelismo - Parte 2

Como escolher linguagem: Não devemos pegar as linguagens por números sem contexto, e sim analisar o seu uso em um contexto especifico e ver se faz sentido usar na nossa situação.

Dicas para inciantes: Não devemos virar fans de tecnlogia e ter metas fora da realidade. Precisamos entender como elas funcionam.

O aspecto mais importante de Multi-Threading: É achar a maneira mais barata e eficiente de coordenar as threads entre si. Não importa quantas cpus temos para rodar threads em paralelo se não conseguimos faze-las comunicar e rodar isoladamente de forma segura e eficiente.

Programação é transformação de dados.

Forma mais simples de cordenação de processos: Linux pipes, ligar o stdout de um processo no stdin de outro processo.

Formas de Comunicação:

- Sinais do OS
- Pipes: Comunicação so flui em uma direção
- Named Pipe: FIFO implementado pelo OS, que é quase um arquivo. Comunicação flui em uma direção. E cada client precisará de um named-pipe
- Sockets: Uma porta aberta pelo servidor, em que um ou mais clientes se conectam para ler ou escrever dados nesse socket. Na Web isso é feito pelo socket Ip. Para processos o linux tem o Unix sockets, esse é a melhor maneira de comunicação entre processos. Assim que são feitas as coordenação de workers de processos pelo NGNIX.
- Compartilhamento de Arquivos

MicroServiços: Na pratica são processso que se comunicam via sockets IP, com o protocolo HTTP.

Diferença de Protocolos Binários e De Texto como HTTP: Para representar um Char em binário normalmente é preciso de 2 bytes, o que dobra o tamanho da requisição. Hoje não pensamos muiot nisso, mas em sistemas que trafegam milhares de bits por hora cada bit importa.

Serialização do conteúdo do Socket: Para mandar mensagem em um socket o client precisa serializar a mensagem no formato certo, e o sevidor precisa deserializar também para consumi-la. Aqui está um dos maiores problemas de comunicação entre micro-serviços.

Comunicação entre Threads: É mais simples e menos custoso pois as threads tem acesso a memória compartilhada de um processo.

Criar Processos e Threads é sempre muito custoso e gasta muita memória

Python e Ruby: São single threading, pois o interpretador cria threads reais no sistema operacional, mas não é thread-safe.

Beneficios do Event-Loop: É bom para aplicações que tem muito I/O, e não para programas que são CPU bound, que podem travar o event-loop. Isso é muito bom para aplicações web.

Coroutina: Pausar uma função que está rodando para executar outra. Isso elimina a criação de threads e fazer context-switching. O Nome disso é Fiber ou Generator. Trabalha com yield e resume, a função do generator pode transferir o controle de volta para a função que a chamou. É a implementação a nivel código da implementação de cooperação de processo não preemptiva.

Programação assicrona evolução:

- callbacks:
- Defered/Futures/Promises:
- Fibers e Generators: A execução da função principal é delegada para a Fiber, que a retoma pelo yield. É o jeito mais legivel de se fazer programação async

Linguagens que Implementão Reactor Pattern: Ruby e Python o fazem, porém a maioria das blibiotecas são sync, então não é muito util. Porem Nodejs já foi criado pensando nisso, então a maioria das suas blibiotecas são async. Podendo assim utilizar esse pattern para alcançar algum paralelismo

Thread Pools: Em linaguagnes que tem acesso a criar varias threads, elas podem criar algumas threads com limite, o ideal seria um thread por core da maquina. E a pool é orquestrada como um workbalancer, as taks chegam em uma fila, e um orquestrador decide a thread disponivel para pega-la. Se precisarmos de threads sempre devemosar usar Pools, Queues, e Tasks.

Conceito de Pool: É usado em todo recurso custoso. Ele cria de antemão os recursos disponiveis, e cria uma abstração para fornce-los. Em banco de dados temos as connections pools.

Solução que resolve a maioria dos Problemas: Ter workers iniciados, que podem ser processos, threads ou funções, que escutam uma fila de jobs para executar. Porém ainda dá para fazer algo mais eficiente no mesmo processo.

Green Therds: Threads em User-land são muito mais baratas do que criar threads no Kernel Space. Porém elas não podem usufruir dos cores da CPU, e, portanto, não tera paralelismo.

Paralelismo em Green Threads: Criar um pool de threads reais, e criar um scheduler em user-land para alocar as milhares de green-threads criadas, para executar nelas. Isso dá para fazer em Scala, Go e Elixir.

Solução do ErLang: Tem um scheduler para cada thread real do sistema operacional. Ele implementa coortinas reais, e esse scheduler é preemptivo, então pode pausar quando quiser a execuação da uma função. Cada thread, ou função, no Erlang tem o nome de processo, pois possui uma memória propria que não é compartilhada, o compartilhamento com outras funções se da por um socket. E cada processo possui um garbage collector. Então um processo, ou green-thread, nunca corrompe a memória do processo em que roda. E é tão barato em termos de memória criar threads em user-land que vale a pena faze-lo, então podemos voltar a criar uma thread por conexão, e com o scheduler do Erlang temos paralelismo de verdade.

Go: Tem as goroutinas que são como processos de Erlang, e trafega mensagens por meio de channels, que são como Pipes do Linux. Porém isso faz com que tenhamos que pensar em Mutex e DeadLocks. O Scheduler do Go é cooperativo, ele espera certos eventos acontecerem em uma coorotina para passar para outra, isso é mais leve e mais previsivel, tornando-o mais poderoso que Nodejs e mais simples de programar códigos complexos.

Scheduler UserLand Vs Reactor: Em linguagens que não tem acesso a threads reais, o pattern de Reactor é a melhor solução para concorrência.

Elixir possui as melhores abstrações de concorrência.

Javascript: É a mais simples das linguagens. Sua unica forma de concorrência é com generators e fibers, e na falta do Scheduler, ele usa o event-loop. Mas da para fazer fork com outros processos, ele prefere trocar perfomance por uso de memória. Apesar de ser rápido, é uma das linguagens mais rudimentares que temos.
