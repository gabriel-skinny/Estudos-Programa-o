# Estudo - Sistema Operacional

Definição: É um software que funciona como uma inteface entre o usuario e o hardware do computador. Ele fornece as bases para se escrever softwares em alguma linguagem de programação. Ele não faz nada por si mesmo, só fornece o ambiente para que outros programas consigam fazer seu trabalho. Ele também cuidade de como os recursos do computador serão utilizados por um programa, funcionando como uma alocador de recursos.

Duas funções

- Abstrair operações do Hardware
- Controlar os recursos do Hardware: Gerenciamento de Processos e de Memória

Abstrações do Sistema Operacional

- Processos e Threads: Abstrai a execução da CPU
- Gerenciamento de Memória: Abstrai o uso da memória principal
- Sistema de Arquivos: Abstrai o uso do Disco rigido e algumas operações de I/O
- Proteção
-

## Overview da Abstração dos elementos de Hardware feitos pelo OS

Definição: A principal função do sistema operacional é oferecer interfaces abstratas para se comunicar com o hardware, mas ele não faz liberalmente, e sim por uma regra de segurança.

Modo de execução de Programas:

- Kernel Mode: As Instruções conseguem falar diretamente com o Hardware. Aqui fica o sistema operacioanl
- User Mode: Apenas instruções que se comunicam indiretamente com o sistema opeacional. Aqui fica os softwares do usuario

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
- Virtual Machine: Um kernel que lida com multiprogramação e gera maquinas virtuas, que são uma copia exata do seu hardware. Então cada maquina virtual pode ter seu sistema operacional que interage com esse hardware virtual. Hoje se usa muito maquinas virtuais para rodar varios servidores em um ambiente isolado, porém na mesma maquina fisica.

## Processos e Threads

### Processos

Processo: Uma abstração de um programa em execução. Todo processo possui range de endereços de memoria que poderá utilizar, e também possui todas as informações para ele rodar: Processos relacionados, arquivos abertos e etc. Ele é como uma copia virtual de uma CPU, contendo todos os valores, Program counter e instruções que precisa para rodar

Processos em Unix:

- Text Segment: O Código de execução do programa
- Data Segment: As variaveis globais, que cresce para cima na memória
- Stack Segment: Contexto de execução que contém variaveis locais, parametros da função e o seu retorno, que cresce para baixo na memória
- Heap Segment: Memória alocada dinamicamente em tempo de execução.

Interprocess Comunication: Um processo pode criar outro processo para fazer alguma tarefa, o que chamamos de Child-Process, e eles precisam conseguir comunicar-se entre si.

Sistema Time-Sharing: Um programa pode ficar muito tempo esperando um input e a CPU vai ficar parada enquanto poderia estar executando outra coisa. O sistema operacional pode fazer a CPU executar varias tarefas ao mesmo tempo, alterando-se entre si, de modo tão rapido que o usuario nem percebe. Esse tipo de sistema é muito usado quando se tem varios usuarios fazendo tarefas que acabam rapidamente.

Criação de Processo:

- Deamons rodando em background iniciados pelo sistema
- Child processes criados para um processo completar sua execução
- Usuario requsita a criação de um processo

Terminação de Processo:

- Normal exit: Sinalização ao sistema operacional pelo exit System Call
- Error exit: Erro detectado pelo progama, sai e coloca e chama exit com código de erro
- Fatal error: Quando tem um bug no programa e ele acessa recursos que não pode
- Killed by another process: Outro processo com permisão chama o System call kill

O Sistema operacional cuida das seguintes atividades no gerenciamento de processos:

- Agenda processos e threads na CPU
- Cria e deleta processos do sistema e do usuario
- Suspende e continua processos
- Provê mecanismo para a sicronização de processos
- Provê mecanismo para a comunicação de processos

Hierarquia de Processos: Em unix temos um grupo de processos, que é todos os child-processes de um processo e seus descendentes. Então o primeiro processo criado, init em Unix, é o pai de todos os processos, e todos eles são derivados dele.

Pipe: Sistemas UNIX possuem um modo de comunicação entre processos em que um processo produz um output, o escreve em uma specie de Pseudoarquivo chamado Pipe, que é usado como input por outro programa.

Status do processo:

- Rodando: Sendo executado pela CPU
- Pronto: Executável, porém está esperando outro processo que está sendo executado pela CPU
- Bloqueado: Não está executável pois está esperando um evento externo acontecer

Process Table: Contem todas as informações para rodar um processo, que poderão ser utilizadas para traze-lo de volta à memória quando interrompido.

Queues de execução:

- Ready: Os processos com status "Pronto" são colocado em uma fila para serem executados pela CPU
- I/O device: Processos stopados esperando receber o input de algum I/O device
- Child Process: Iniciou um child-process e está esperando ele terminar de execuar para receber seu output

Scheduler: Define qual processo será executado pela CPU, pegando suas informações da process table, e colocando na fila certa.

Multiprogramming: Apesar da CPU conseguir executar uma instrução por vês, ela pode ir se alternando entre processos, trocando seu Program counter virtual por um program counter físico, que roda os processos em sequencia, de forma alternada.

### Thread

Definição: Um mini processo dentro de um processo, que se refere a uma linha de execução. Um processo pode ter mais de uma linha de execução, podendo ele mesmo ser um scheduler e definir quando rodar e alocar suas execuções. A principal diferença de um processo é que as threads possuem memória compartilhada entre si.

Beneficio de Threads: Sem threads teriamos que criar um processo para cada função que quissesemos executar em parelelo e ser agendada pelo scheduler, porém não conseguiriamos fazer uma mudança global na aplicação, já que as funções estariam dividias em seus processos isolados. Com threads podemos definir as linhas de execução do nosso programa, e da-las ao scheduler, para conseguir executa-las em "paralelo" e ter o beneficio de conseguir fazer mudanças rapidamente na aplicação inteira.

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
- Assincronamente(Finite-state machine): Fazer operações non-blocking de I/O e guardar as operações em tabelas, e altera-las conforme chegam eventos.

Implementação de Threads

- User Level: O Sistema operacional não conhece que existem threads, elas são implementadas por uma blibioteca externa que possui sua propria lógica para lidar internamente com threads dentro de um processo e deixão uma tabela de threads na memória do processo. Tem melhor performance por não precisar fazer system-calls porém perde seu sentido quando tem chamadas I/O que bloqueiam a execução de uma thread, pois o processo será bloqueado pelo sistema operacional e nenhuma thread poderá rodar
- Kernel Level: A tabela de threads é colocada no kernel e o sistema operacional implementa o agendamento das threads, permitindo que um mesmo processo seja bloqueado em uma thread mas não pare de rodar pois o sistema começou a executar outra thread disponível desse mesmo processo. O problema é o custo das sistem calls.
- Multiplex user-threads: O programador escolhe quantas threads serão lidadas pelo sistema operacional e quais serão por uma blibioteca user-level, podendo ter uma ou mais threads relacionadas a um thread criada pelo kernel.

Problemas de Multi-Threading:

- Variaveis globais que são alteradas por varias threads
- Blibiotecas que podem ser chamada duas vezes por threads diferentes causando comportamentos inesperados
- Sinais que são mandados pelo sistema operacioanal que não pode sinalizar diretamente para threads user-levels

## Gerenciamento de Memória

Memória: Um array de bytes em que cada valor tem um endereço especifico, que é acessado pela CPU e dispostivos de I/O, de forma rápida.

O sistema operacional faz as seguintes operacões para o gerenciamento de memória:

- Guarda o registro de quais partes da memória estão sendo acessados e por quem
- Decide que processos e dados para tira-lo ou coloca-lo em memória
- Alocar e desalocar espaço da memória conforme a necessidade

Memória Virtual: Um dos recursos que o sistema operacional faz é abstrair os endereços físicos da memoria para endereços virtuais. Isso permite que o sistema operacional consiga fornecer a um programa mais memória do que existe no computador e isola-lo de usar a memória de outros programas.

## Sistema da Arquivos

Arquivo: Buffer de bytes que representam algum valor que é guardado na memória.

Tipos de Arquivo em UNIX:

- Arquivos de Execução(Programas)
- Arquivos de Texto
- Arquivos de Diretorio
- Arquivos Especiais(Especial Files): Pipes, ou arquivos de configuração de I/O

Diretorios em Unix: Uma tabela contendo o i-number, id do arquivo, e o seu nome.
