# Estudo - Sistema Operacional

Definição: É um software que funciona como uma inteface entre o usuario e o hardware do computador. Ele fornece as bases para se escrever softwares em alguma linguagem de programação. Ele não faz nada por si mesmo, só fornece o ambiente para que outros programas consigam fazer seu trabalho. Ele também cuida de como os recursos do computador serão utilizados por um programa, funcionando como um alocador de recursos.

Duas funções

- Abstrair operações do Hardware
- Controlar os recursos do Hardware: Gerenciamento de Processos e de Memória

Como fornece as duas funções/Quando o sistema operacional roda

- Através de Sistem Calls
- Através de um sinal emitido por um timer no hardware que roda o Interrupt handler do Sistema operacional, fazendo ele ganhar controle sobre a CPU

Abstrações do Sistema Operacional

- Processos e Threads: Abstrai a execução da CPU
- Gerenciamento de Memória: Abstrai o uso da memória principal
- Sistema de Arquivos: Abstrai o uso do Disco rigido e algumas operações de I/O

Dois Objetivos do Sistema operacional

- Garantir um controle sobre o hardware, deixando o minimo possível para o usuario
- Garantir máxima eficiência do Hardware

TradeOff Controle Geral X Performance: Quanto mais regras tem o OS para controlar o hardware, mais espcifica são suas soluções, piorando a performance para os casos gerais

## Overview da Abstração dos elementos de Hardware feitos pelo OS

Definição: A principal função do sistema operacional é oferecer interfaces abstratas para se comunicar com o hardware, mas ele não faz liberalmente, e sim por uma regra de segurança.

Modo de execução de Programas:

- Kernel Mode: As Instruções conseguem falar diretamente com o Hardware. Aqui fica o sistema operacioanl
- User Mode: Apenas instruções que se comunicam indiretamente com o sistema opeacional. Aqui fica os softwares do usuario. Toda e qualquer operação que altera no hardware é travada por ele mesmo.

- System call: Funções que possibilitam o software do usuario entrar no Kernel Mode e falar direto com o hardware.

Funcionamento de SystemCall:

- Implementação feita em Assembly
- Imeplemtanação do Código chamando essa função
- TRAP funcion passa o controle para o Kernel
- Kernel encontra a instrução referida
- Kernel passa de volta o controle da execução para UserMode e retorna o valor
- Função retorna

POSIX: Definições de interfaces que precisam ser implementadas pelos sistemas operacionais para manter compatibilidade entre si.

Algumas funções do POSIX:

- Processos:fork, exit
- Files: open, close, read, write, lseek, stat
- Diretorios: mkdir, rmdir, link, unlink, mount, umount
- Outras: chdir, chmod, kill, time

Design interno das interfaces de um Sistema Operacional:

- Monolito: Um binário que contem todas as funções para se comunicar com o hardware
- Layers: Cada layers tem uma responsabilidade e rodam em kernel mode
- Microkernel: Apenas um pequeno modulo de funções que roda em Kernel mode e contral o acesso ao hardware, e outro modulos com menos privilegio que rodam coisas como Drivers e o File-System. Um bug em um dos modulos não causa um bug total no sistema, mas apenas na aquele modulo.
- Modulos:
- Virtual Machine: Um kernel que lida com multiprogramação e gera maquinas virtuas, que são uma copia exata do seu hardware. Então cada maquina virtual pode ter seu sistema operacional que interage com esse hardware virtual. Hoje se usa muito maquinas virtuais para rodar varios servidores em um ambiente isolado, porém na mesma maquina fisica.

Design de modulos do Kernel do Linux:

- I/O Component: Terminal, Sockets, Network, File System, I/O Scheduler, Block device
- Memory mgt component: Virtual Memory, Paging, page, page cache
- Process mgt component: Signal Handlging, Process/Thread control, CPU scheduling

## Processos e Threads

### Processos

Processo: Uma abstração de um programa em execução. Todo processo possui range de endereços de memoria que poderá utilizar, e também possui todas as informações para ele rodar: Processos relacionados, arquivos abertos e etc. Ele é como uma copia virtual de uma CPU, contendo todos os valores, Program counter e instruções que precisa para rodar. Essa abstração existe para o sistema operacional conseguir rodar mais de um programa em uma CPU.

Objetivo do Processo: Virtualizar a CPU para abstrari seu uso e permitir execução em "Paralelo", permitindo seu melhor uso.

Problemas centrais da Virtualização: Faze-lo de modo eficiente e perfomático, mas matendo um controle sobre o sistema.

O Sistema operacional cuida das seguintes atividades no gerenciamento de processos:

- Agenda processos na CPU e os controla, criando, suspendendo e deletando
- Provê mecanismo para a sicronização de processos
- Provê mecanismo para a comunicação de processos

#### O que são Processos

Process Table: Contem todas as informações para rodar um processo, que poderão ser utilizadas para traze-lo de volta à memória quando interrompido.

Process table:

- PID(Indentificador unico)
- Status
- Estado:
- Accounting: Informações de performance
- Files: Arquivos abertos
- Parent
- Childs
- Endereço de Memória

Imagem da Memória de Processos em Unix:

- Text Segment: O Código de execução do programa
- Data Segment: As variaveis globais, que cresce para cima na memória
- Stack Segment: Contexto de execução que contém variaveis locais, parametros da função e o seu retorno, que cresce para baixo na memória
- Heap Segment: Memória alocada dinamicamente em tempo de execução.

Criação de Processo:

- Deamons rodando em background iniciados pelo sistema
- Child processes criados para um processo completar sua execução:
  - Duplicação do processo pai com a mesma imagem de memória
  - Roda um novo programa pela system call EXEC
- Usuario requsita a criação de um processo

Terminação de Processo:

- Normal exit: Sinalização ao sistema operacional pelo exit System Call
- Error exit: Erro detectado pelo progama, sai e coloca e chama exit com código de erro
- Fatal error: Quando tem um bug no programa e ele acessa recursos que não pode
- Killed by another process: Outro processo com permisão chama o System call kill

Hierarquia de Processos: Em unix temos um grupo de processos, que é todos os child-processes de um processo e seus descendentes. Então o primeiro processo criado, init em Unix, é o pai de todos os processos, e todos eles são derivados dele.

#### Agendamento de Processos

Scheduler: Define a execução dos processos pela CPU. É preciso usa-lo para que os processos iniciados tenham cada um tempo justo de execução na CPU. Ele torna possível um certo parelelismo, pois a CPU pode ficar alterando varios processos de modo tão rapido que parece estar rodando em paralelo.

Multiprogramming: Apesar da CPU conseguir executar uma instrução por vês, ela pode ir se alternando entre processos, trocando seu Program counter virtual por um program counter físico, que roda os processos em sequencia, de forma alternada.

Quando o Scheduler toma decisão Roda:

- Quando um processo é criado
- Quando um processo é terminado
- Quando um processo é bloqueado esperando I/O
- Quando um processo foi desebloqueado
- Roda seu algoritimo a cada clock interrupt

Status de um processo:

- Rodando: Sendo executado pela CPU
- Pronto: Executável, porém está esperando outro processo que está sendo executado pela CPU
- Bloqueado: Não está executável pois está esperando um evento externo acontecer

Queues de execução:

- Ready: Os processos com status "Pronto" são colocado em uma fila para serem executados pela CPU
- I/O device: Processos stopados esperando receber o input de algum I/O device
- Child Process: Iniciou um child-process e está esperando ele terminar de execuar para receber seu output

Dispatcher e Context-Switching: O Dispatcher é o modulo do scheduler que lida com a troca dos processos em execução. Ele faz isso por um processo chamado Context-Switchin, que consiste em: entrar em kernel-mode, atualizar a PCB do processo atual e rescrever todo mapa de memória com o processo que está entrando em execução.

Objetivos de um algoritimo de Scheduler para sistemas interativos:

- Justiça: Dar a cada processo o seu tempo de CPU sendo a sua natureza
- Garantir a política: Verificar se a política imposta está sendo seguida pelos processos
- Balanceamento: Ter todas as partes do sistema ocupadas
- Tempo de Resposta: Responder rapidamente aos usuarios
- Proporcionalidade: Atender às expectativas do usuario

Métrica Importantes:

- Turnaround Time: Tempo que um processo demora para terminar assim que chega à fila de pronto
- Response Time: Tempo que um processo demora para responder algo
- Fairness: Porcentagem em que um processo roda em um ciclo total de execução

Algoritimos de decisão do Scheduler:

- Não preemptivo: Deixa um processo usar a CPU até ser bloqueado. É mais usado em batch-sistems, em que se tem uma rotina para rodar do começo até o fim, sem muitas interações.

  - First-Come, First Served: Os processos em "ready" são colocados em uma fila e o primeiro começa rodar até terminar ou ser bloqueado, e quando bloqueado, o proximo processo começar a executar, e aquele quando volta vai para o final da fila.
  - Shortest Job First: Os procesosos tem seu tempo predefinido, e com a mesma importância são priorizados os que tem menor tempo de execução. Isso faz com que o Turnaround time diminua. Porém isso implica que todos os processos estarão disponiveis ao mesmo tempo. É o melhor algoritimo para TurnAround time

- Preemptivo: Deixa um processo rodar por um tempo máximo definido, que é informado por um clock interrupt. É o mais usado em sistemas interativos e servidores que servem muitos usuarios, já que é necessario ficar trocando de processo para servi-los e não deixar que um bug em um processo acabe com a execução da CPU.

  - Shortest Remaining Time Next: Versão do Shortest Job first, porém que compara o tempo atual do processo que está rodando, com o tempo de um novo processo inserido em "ready", se o tempo para terminar o processo atual for maior ele o interrompe e executa o novo processo.
  - Round-Robin: Cada processo é colocado em uma fila e todos tem seu quantum, tempo de execução, defindo, e se ele rodar sem ser bloqueado até o fim do seu quantum ele é interrompido e colocado no ultimo lugar da fila. Um problema é o custo de fazer o context-switch entre os processos, quanto menor for o quantum, mas tempo a CPU gastará o fazendo. Porém se o quantum for muito alto, o tempo de reposta será menor, pois os processos no final da fila demorarão muito tempo para poder rodar. Esse é melhor algoritimo quando se trata de response time, porém o pior se considerado o turnaround time, tempo que um processo leva para terminar assim que é colocado na fila, uma FIFO nesse caso é bem melhor.

  - Priority: Todos os processos tem uma prioridade e o de maior prioridade é colocado a rodar. E para processos de alta prioridade não rodarem indefinidamente, o scheduler pode ir diminuindo sua prioridade até ela ficar menor que um processo da fila, que então é colocada para executar. Ou cada processo ter um quantum para ser interrompido. A definição de prioridade é também importante, é bom colocar processos I/O bound para serem executados rapidamente, para serem bloqueados e saírem da memória. É bem ter classes de prioridades e usar round-roubin em cada classe, de modo que a classe de maior prioridade é primeiro esvaziada, se alternando segundo seu quantum, depois o proximo em prioridade, assim sucessivamente.
  - Multi-Level FeedBack Queue: Filas de prioridades em que os processos são alternados com Round-Robin segundo um quantum. A prioridade é definida pelo tempo de execução dos processos, que conforme usam CPU vai caindo na fila. É um dos algoritimos mais usados em sistemas modernos
  - Multiplas filas: Processos são colocados em filas em que quanda uma tem um quantum indo do maior ao menor, e conforme ela roda segundo esse quantum, ela desce de lugar para a fila de baixo. Isso permite que processos I/O bound sejam resolvidos rapidamente e CPU bound ganhem bastante tempo de execução conforme desce na fila, minimizando o context-switching

  - Shortest Process Next: Executa o processo com menor tempo de execução. O problema está em estimar o tempo do processo, o que pode ser feito fazendo a media do histórico de tempo de execução do processo. Usando a tecnica aging, o ultimo tempo de execução tem prioridade em relação aos tempo antigos.

Fair Sharness Algoritimhs: São mais usados quando sabe quais processos vão rodar e qual sua importancia de ante mão, por exemplo em ambientes virtuais e data-centers. E também quando se tem mais operações CPU bound do que I/O bound.

- Guaranteed Scheduling: Cada processo ganha um tempo justo de execução na CPU, que é calculado e balanceado conforme os processos vão rodando.
- Lotery Tickets: Cada processo ganha tickets que podem ser sorteados para ganhar certo tempo de execução. A vantagem é que um processo pode ser seus tickets para outro processo de que ele depende, asssim esse provavelmente vai ganhar a loteria e executar, resolvendo o seu bloqueio, depois esse servido pode devolver os seus tickets a esse. O seu objetivo é atingir fairness na execução dos processos, o que acontece quanto mais tempo os processos rodam, pois a randomização fica mais certa.
- Completly Fairness(Linux): Cada processo possui um virtual runtime, que é definido pelo runtime real \* peso do processo, definido pelo usuario. O processo que roda é o que tem menos vruntime. Para melhorar a performance do scheduler, ele armazena os processos rodando em um red-black-tree, tornando as operações em O(log n). É o algoritimo baseado em fairness mais usado nos dias de hoje.

Principio de separação do Scheduling Mechanism e Scheduling Policy: Todos os algoritimos acima descritos para definir quem rodará o processo não levam em consideração a opinião de um processo sobre a execução de seus child-processes, o que faz com que a maioria das decisões que ele tome sejam ruins. Por isso muitos sistemas operacionais disponibilizam system calls para um processo dar um input para o algoritimo de scheduler ponderar na sua decisão. A politica é definida por um user-process porém o mecanismo de decisão está no kernel.

Scheduler do Linux:

- Algoritimo de Prioridade de Grupos
  - Range de 1 a 100: Tasks de Real-Time com quantum de 200ms
  - Range de 100 a 140: Outras tasks com quantum de 10ms

LoadBalancing em Multiprocessadores: Em computadores de mais de uma CPU o scheduler pode precisar balancear os processos entre as CPU's, tirando processos em uma CPU muito opcupado e os colocando em uma CPU nova

#### Interprocess Comunication

Interprocess Comunication: Um processo pode criar outro processo para fazer alguma tarefa, o que chamamos de Child-Process, e eles precisam conseguir comunicar-se entre si.

Problemas de Comunicação entre processos:

- Corrupção de dados compartilhado
- Sincronização das suas operações

Tipos de Comunição entre processos:

- Memória Compartilhada: Os processos concordam em tirar a restrição de compartilhar sua memória e controlam entre si o acesso a pontos compartilhados. É mais rapido pois os processos para pegarem os dados que necessitam só precisam acessar o lugar compartilhado da memória. É uma imlpementação de compartilhamento muito baixo nivel, que não pode ser replicada em sistemas distribuidos cada um com sua memória.
- Mensagem: Um processo envia uma mensagem que pode ou dever ser lida por um ou mais processos

###### Memória compartilhada entre processos:

Problema de Race condition: Um ou mais processos estão lendo e escrevendo em um recurso compartilhado
Soluções:

- Mutual exclusion para acessar uma critical section, uma região compartilhada
- RCU(Read-Copy-Update): Deixar uma versão antiga para leitura, e em operações de adição adicionar o novo dado, porém de forma que não altere a estrutura antiga, quando todas as leituras tiverem ocorridas, aí é atualizado a estrutura antiga para a nova.

Implementações de Mutual exclusion:

- Disabilitar os interuptores quando um processo acessar uma região critica, não permitindo que ele tenha seu status alterado
- Variaveis de Lock: Quando um processo entra em uma região critica ele seta o lock variable para 1. Mas ainda tem o problema da race condition, pois ler o lock é uma operação
- Strick Alternation: Um processo fica em busy waiting verificando se uma variavel foi alterada, e outro processo fica vendo se essa variavel foi alterada com o valor invertido. Funciona porém gasta muita CPU.
- Peterson's Alogrithm: Um processo chama uma função para entrar na região e seta o seu turno, a função verifica se outro processo está rodando e deixa um loop bloqueando esse processo de entrar, quando o processo anterior chamar uma função para sair da região e tirar o turno, o processo 1 pode entrar na região.
- Instrulçao assembly TSL(Test and Set Lock): Solução de Hardware em que a CPU guarda em um registrador um ponto da memória bloqueado e bloqueia o bus de acesso para qualquer outra CPU. É uma solução para multiplos processadores.
- Sleep and Wakeup: Um processo coloca outro para dormir enquanto ele não pode acessar uma região compartilhada e precisa esperar esse processo executar. Como em uma situação de producer-consumer. Isso elimina o busy-waiting e do processo que está esperando gastar tempo de CPU. Porém tem o problema de ter sinais de wakeup perdidos, fazendo com que um processo fique dormindo para sempre
- Semaforos: Resolvem o problema do lost-wakeup, fazendo com que a mudança no estado de um semafóro seja feita de forma atomica: leitura, alteração do seu valor e colocar processos para dormir são feitos em uma operação, que não pode ser interrompida por nenhum outro processo. Isso é feito desligando os interuptores para essas instruções, e, se tiver mais de uma CPU, colocando a variavél do semaforo lockada com a intrução TSL. E elimina o busy-waiting pois um processo só fica lockado enquanto outro está mudando o semaforo, que são poucas instruções, depois ele é colocado a dormir, não ocupando tempo de CPU.
- Mutex: São semaforos de 1 bit, que só indicam que uma critical section está bloqueada.
- Monitor's: Modulos escritos em uma linguagem que possui funções e estrutura de dados proprias que só podem ser chamadas e não alteradas internamente. Por ser uma função o compilador consegue reconhecer suas chamadas e bloquear um acesso por um ou mais processos, escondendo técnicas de mutex e semafóro do programador.

##### Comunicação por mensgem:

Tipos de mensagens:

- Comunicação direta: Um processo manda um buffer passando o nome do processo que ira recebe-lo
- Comunicação indireta: Um processo manda um buffer para um mailbox ou port, que pode ter o dono sendo um processo, que terá controle para quem poderá escrever nela, ou o sistema operacional, que deverá fornecer system calls para processos poderem criar, deletar e se ler uma mailbox.
- Sincrono: Um receiver espera que sua mensagem seja enviada e fica bloqueado para qualquer operação, e o consumer também fica bloqueado esperando uma mensagem
- Assincrono: Um receiver envia uma mensagem e continua suas operações, o consumer lê uma mensagem ou recebe null e continua suas operações

Tipos de buffering na fila:

- Zero capacidade: Uma fila que não tem capacidade, então o sender deve ficar bloqueado ate o recebedor ler a mensagem. É chamado de no-buffering message system
- Com capacidade limitada: Uma fila que tem N capacidade, então o sender recebe um ponteiro quando envia uma mensagem e continua sua execução, e deve verificar antes de enviar se existe um espaço disponivel.
- Com capacidade ilimitada: A fila é potencialmente infinita e o sender não precisa ficar bloqueado esperando um espaço ser liberado

Comunicação Cliente-Servidor entre processos:

- Socket: Um endpoint para comunicação
- RPC(Remote Procedure Call): Um processo ou thread chama uma função de outra aplicação
- Pipes:
  - Ordinary: Permite comunicação de processos parentes e arquivo temporario é deletado
  - Named: Permite comunicação de processos não relacionados e cria um arquivo no file system que persiste mesmo tendo finalizado o processo

### Thread

Definição: Um mini processo dentro de um processo, que se refere a uma linha de execução. Um processo pode ter mais de uma linha de execução, podendo ele mesmo ser um scheduler e definir quando rodar e alocar suas execuções. A principal diferença de um processo é que as threads possuem memória compartilhada entre si.

Beneficio de Threads: Sem threads teriamos que criar um processo para cada função que quissesemos executar em parelelo e ser agendada pelo scheduler, porém não conseguiriamos fazer uma mudança global na aplicação, já que as funções estariam dividias em seus processos isolados. Com threads podemos definir as linhas de execução do nosso programa, e da-las ao scheduler, para conseguir executa-las em "paralelo" e ter o beneficio de conseguir fazer mudanças rapidamente na aplicação inteira. Também o context-switching de Threads é muito menos custoso em memória e CPU, e não tem problema de comunicação recursos entre Threads já que elas estão no mesmo processo.

Dados de uma thread:

- Program Counter
- Registradores com variaveis locais
- Stack que contem um histórico de execução e um frame para cada chamada de função não retornada
- Status

Thread X Processo:

- Processo: Abstração de agrupamento de recursos do sistema para execução de um programa
- Thread: Abstração de Entidades agendadas para serem executadas pela CPU

Modos de executar um programa:

- Sequencialmente com uma thread: Bloqueam a linha de execução e não pode rodar em paralelo
- Sequencialmente com Multi-Threading: Roda em paralelo
- Assincronamente(Finite-state machine): Fazer operações non-blocking de I/O e guardar as operações em tabelas, e altera-las conforme chegam eventos. Essa é a forma mais complexa

Problemas de Multi-Threading:

- Variaveis globais que são alteradas por varias threads
- Blibiotecas que podem ser chamada duas vezes por threads diferentes causando comportamentos inesperados
- Sinais que são mandados pelo sistema operacioanal que não pode sinalizar diretamente para threads user-levels

Implementação de Threads

- User Level: O Sistema operacional não conhece que existem threads, elas são implementadas por uma blibioteca externa que possui sua propria lógica para lidar internamente com threads dentro de um processo e deixão uma tabela de threads na memória do processo. Tem melhor performance por não precisar fazer system-calls porém perde seu sentido quando tem chamadas I/O que bloqueiam a execução de uma thread, pois o processo será bloqueado pelo sistema operacional e nenhuma thread poderá rodar. Também não conseguem usufruir de multiprocessadores, pois apenas uma thread, a criada em kernel-level, consegue acessar o kernel.
- Kernel Level: A tabela de threads é colocada no kernel e o sistema operacional implementa o agendamento das threads, permitindo que um mesmo processo seja bloqueado em uma thread mas não pare de rodar pois o sistema começou a executar outra thread disponível desse mesmo processo. O problema é o custo das sistem calls para criar threads no kernel.
- Multiplex user-threads: O programador escolhe quantas threads serão lidadas pelo sistema operacional e quais serão por uma blibioteca user-level, podendo ter uma ou mais threads relacionadas a um thread criada pelo kernel.

Thread-Pool: Criar uma ou mais thread quando um processo inicia.

Quando usar os dois tipos de Implementação:

- User-Level:
  - Deve ser usada para uma aplicação especifica, pois o controle do scheduler fica do lado do aplicativo, e ele pode definir a priorida de execução das threads.
  - Quando é preciso de um context-switching mais leve
  - Quando se tem apenas um processo rodando na maquina, de modo que não importa se ele é bloqueado.
- Kenel-Level:
  - Quando

Schedules dos tipos tipos de Implementação:

- PCS (Process-Contention-Scope): Threads User-Level competem dentro do contexto de um processo, e esse ou um LWP que é agendado pelo schduler do kernel na CPU real
- SCS(System-Contention-Scope): Threads Kernel-Level competem com todas as threads do sistema. Esse modelo é usado em todos os sistemas operacionais.

Beneficios da Thread-Pool:

- Isso faz com que não se crie threads infinitas para cada nova execução, e sim um numero limitado e conhecido, ficando mais seguro para aplicações que não toleram tantas threads
- Não se perca tempo criando novas threads para executar um código, pois as threads já estão criadas

Threads em Linux: Em linux processos e threads são conceitos que não existem muito bem definidos, por isso são contidos em um conceito abrangente chamado tasks. Linux possui dois system cals para criar novas tasks fork(), que seria como que criar um processo, e clone, que recebe algumas variaveis do conteúdo que irá copiar da task que esta o invocando, sendo mais parecido com a criação de uma thread.

## Gerenciamento de Memória

Memória: Um array de bytes em que cada valor tem um endereço especifico, que é acessado pela CPU e dispostivos de I/O, de forma rápida.

O sistema operacional faz as seguintes operacões para o gerenciamento de memória:

- Guarda o registro de quais partes da memória estão sendo acessados e por quem
- Decide que processos e dados para tira-lo ou coloca-lo em memória
- Aloca e desaloca espaço da memória conforme a necessidade

Memória Virtual: Um dos recursos que o sistema operacional faz é abstrair os endereços físicos da memoria para endereços virtuais. Isso permite que o sistema operacional consiga fornecer a um programa mais memória do que existe no computador e isola-lo de usar a memória de outros programas.

Memória e Processos: Os processos que estão rodando ficam em memória, pois seria muito custoso ficar puxando do disco para fazer um context-switch.

Blueprint de um Process em Memória:

- Program Code: Segmento fixo onde está as instruções do código
- Heap: Dados alocados dinamicamente, vai crescendo para cima no espaço livre. São normalmente lidadas pelo programador ou por linguagens que tem Garbage Collector.
- Free: Espaço para ser preenchido enquanto o programa roda
- Stack: Variaveis locais, argumentos de funções e seus retornos, cresce para baixo na memória livre. São normalmente lidadas pelo compilador mesmo em linguagem de baixo nível

Objetivos da abstração da Memória Virtual feita pelo OS:

- Transparencia: Deixar isolada a lógica da memória e as especifiações do hardware para o programador
- Eficiência: Usar do modo mais eficiente possível a memória disponível no sistema
- Proteção: Não deixa um processo alterar a memória de outro processo

System calls de Memoria

- brk: Estende o espaço da memória livre do programa
- mmap: Cria um novo mapping da memória virtual do processo

### Implementação da Virtualização

Mecanismo do Hardware:

- Registradores Base and Bound para determinar grupo da memória de um processo
- Registradores para determinar o tipo de segmeento do registrador Base, Bound: Code, Heap ou Stack
- Bit para saber se a memória cresce para cima ou para baixo
- Bit para determinar se o espaço na memória é Writable, Redable e Exectuable
- Estorar uma excessão quando usuario acessar uma memória outofbounds

Macanismo do OS:

- Alocar memória para o processo na sua criação e marca-la como "em uso"
- Deslocar memória quando um processo morre e marca-lo como "livre"
- Setar os registradores base/bound quando tiver um context switch
- Lidar com excessões out of bounds enviadas pelo HardWare, setando em Boottime o código para lidar com essa excessão.

Soluções de Virtualização:

- Base and Bound ou Dynamic Alocation: O Hardware possui dois registradores Base e Bound, onde os OS preenche como sendo o endereço de memória do processo. Então o hardware sempre quando recebe uma instrução para pegar da memória de um programa, soma ao registrador base para pegar o endereço fisíco. E se o endereço virtual passado pelo processo for maior que o endereço colocado no Bound, a CPU estora um erro. Isso é adicionado na MMU. O Problema dessa solução é que não é flexivel, sempre blocos de memória continuos são ocupados, e também fica um espaço vazio enorme entre a stack e o heap bloqueada de ser alocado, pois pode ser usado pelo programa.
- Segmentation: Criar um base and size para cada segmento de um processo, code, stack e heap, fazendo com que eles possam ser alocados individualmente em qualquer lugar da memória. O Hardware pode achar o segmento de modo explicito: em um endereço de 14 bits, os dois primeiros dizem para o hardware qual tipo de segmento é, e quais registradores ele deve usar; ou de modo implicito: Analisar qual instrução está enviando o endereõ, é uma instrução vinda do program counter, pega do code; ou stack pointer, pega da stack; e os outros do heap.

## Sistema da Arquivos

Arquivo: Buffer de bytes que representam algum valor que é guardado na memória.

Tipos de Arquivo em UNIX:

- Arquivos de Execução(Programas)
- Arquivos de Texto
- Arquivos de Diretorio
- Arquivos Especiais(Especial Files): Pipes, ou arquivos de configuração de I/O

Diretorios em Unix: Uma tabela contendo o i-number, id do arquivo, e o seu nome.
