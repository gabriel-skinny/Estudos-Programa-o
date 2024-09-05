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

## Processos e Threads

Modo de execução de Programas:

- Kernel Mode: As Instruções conseguem falar diretamente com o Hardware. Aqui fica o sistema operacioanl
- User Mode: Apenas instruções que se comunicam indiretamente com o sistema opeacional. Aqui fica os softwares do usuario

- System call: Funções que possibilitam o software do usuario entrar no Kernel Mode e falar direto com o hardware.

Processo: Um programa em execução. Todo processo possui range de endereços de memoria que poderá utilizar, e também possui todas as informações para ele rodar: Processos relacionados, arquivos abertos e etc.

Process Table: Contem todas as informações para rodar um processo, que poderão ser utilizadas para traze-lo de volta à memória quando interrompido.

Interprocess Comunication: Um processo pode criar outro processo para fazer alguma tarefa, o que chamamos de Child-Process, e eles precisam conseguir comunicar-se entre si.

Sistema Time-Sharing: Um programa pode ficar muito tempo esperando um input e a CPU vai ficar parada enquanto poderia estar executando outra coisa. O sistema operacional pode fazer a CPU executar varias tarefas ao mesmo tempo, alterando-se entre si, de modo tão rapido que o usuario nem percebe. Esse tipo de sistema é muito usado quando se tem varios usuarios fazendo tarefas que acabam rapidamente.

Pipe: Sistemas UNIX possuem um modo de comunicação entre processos em que um processo produz um output, o escreve em uma specie de Pseudoarquivo chamado Pipe, que é usado como input por outro programa.

## Gerenciamento de Memória

Memória Virtual: Um dos recursos que o sistema operacional faz é abstrair os endereços físicos da memoria para endereços virtuais. Isso permite que o sistema operacional consiga fornecer a um programa mais memória do que existe no computador e isola-lo de usar a memória de outros programas.
