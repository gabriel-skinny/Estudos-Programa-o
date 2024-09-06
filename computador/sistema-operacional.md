# Estudo - Sistema Operacional

Definição: É um software que funciona como uma inteface entre o usuario e o hardware do computador. Ele fornece as bases para se escrever softwares em alguma linguagem de programação. Ele não faz nada por si mesmo, só fornece o ambiente para que outros programas consigam fazer seu trabalho. Ele também cuidade de como os recursos do computador serão utilizados por um programa, funcionando como uma alocador de recursos.

Duas funções

- Abstrair operações do Hardware
- Controlar os recursos do Hardware

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
- Data Segment: As variaveis, que cresce para cima na memória
- Stack Segment: Contexto de execução, que cresce para baixo na memória

Process Table: Contem todas as informações para rodar um processo, que poderão ser utilizadas para traze-lo de volta à memória quando interrompido.

Interprocess Comunication: Um processo pode criar outro processo para fazer alguma tarefa, o que chamamos de Child-Process, e eles precisam conseguir comunicar-se entre si.

Multiprogramming: Apesar da CPU conseguir executar uma instrução por vês, ela pode ir se alternando entre processos, trocando seu Program counter virtual por um program counter físico, que roda os processos em sequencia, de forma alternada.

Sistema Time-Sharing: Um programa pode ficar muito tempo esperando um input e a CPU vai ficar parada enquanto poderia estar executando outra coisa. O sistema operacional pode fazer a CPU executar varias tarefas ao mesmo tempo, alterando-se entre si, de modo tão rapido que o usuario nem percebe. Esse tipo de sistema é muito usado quando se tem varios usuarios fazendo tarefas que acabam rapidamente.

Pipe: Sistemas UNIX possuem um modo de comunicação entre processos em que um processo produz um output, o escreve em uma specie de Pseudoarquivo chamado Pipe, que é usado como input por outro programa.

Criação de Processo:

- Deamons rodando em background iniciados pelo sistema
- Child processes criados para um processo completar sua execução
- Usuario requsita a criação de um processo

Terminação de Processo:

- Normal exit: Sinalização ao sistema operacional pelo exit System Call
- Error exit: Erro detectado pelo progama, sai e coloca e chama exit com código de erro
- Fatal error: Quando tem um bug no programa e ele acessa recursos que não pode
- Killed by another process: Outro processo com permisão chama o System call kill

Hierarquia de Processos:

### Thread

## Gerenciamento de Memória

Memória Virtual: Um dos recursos que o sistema operacional faz é abstrair os endereços físicos da memoria para endereços virtuais. Isso permite que o sistema operacional consiga fornecer a um programa mais memória do que existe no computador e isola-lo de usar a memória de outros programas.

## Sistema da Arquivos

Arquivo: Buffer de bytes que representam algum valor que é guardado na memória.

Tipos de Arquivo em UNIX:

- Arquivos de Execução(Programas)
- Arquivos de Texto
- Arquivos de Diretorio
- Arquivos Especiais(Especial Files): Pipes, ou arquivos de configuração de I/O

Diretorios em Unix: Uma tabela contendo o i-number, id do arquivo, e o seu nome.
