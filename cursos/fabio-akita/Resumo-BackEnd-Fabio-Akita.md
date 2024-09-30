# Resumo Back-End - Fabio Akita

CPU:
Registradores:

Sistema Operacional: abstração do hardware.

Instrução Assembly
Instrução do Sistema Operacional: Syscall.

Binário Nativo: Instruções para maquina e para o sistema operacional

Compiladores: Traduz um código escrito em uma linguagem de programação para linguagem de maquina, podendo traduzi-la para qualquer tipo de CPU. Além de traduzir faz diversas otimizações

Linker: Liga o seu programa com as blibiotecas que ele usa.

Linkagem Estática: Mesclar o binário da blibioteca com o binário do seu programa. É melhor para compatibilidade, pois o binário contém o programa e todas suas blibiotecas, de modo que só precisamos copia-lo.
Linkagem Dinâmica: Por uma definição em um arquivo headers que define as funções expostas de uma blibioteca, seu programa aponta para essas funções no binário da blibioteca, ao invés de carrega-lo. Isso, apesar da dor de cabeça de baixar as blibiotecas, é mais leve e mais flexivel.

Interpretador: É uma programa que traduz o seu código em linguagem de máquina. O que depende de você ter instalada com o código fonte, pois ele sempre terá que o interpretar. Ele forem incialmente criados para rodar scripts de linha de comando que começam e terminam rapidamente.

Interpretrador e binding de Blibiotecas Nativas: Por binding os interpretrador mapeiam uma funcionalidade e a memória de uma blibioteca nativa que está instalada no seu sistema operacional. Eles foram feitos para depender do sistema operacional que estão rodando.

Maquina Virtual: É uma evolução dos interpretadores, pois ele é um programa que subistitui o seu sistema operacional, e compila o seu código para um binário que é executa no seu ambiente, chamado Bytecode. Você precisa deixar ele parasitar sua maquina, e para executar código em paralelo, criar threads dentro dele.

Compilador JIT(Just-In-Time): Compilador que vai otimizando o seu código em runtime. Isso acontece pois otimizar em tempo de compilação fará com que demore muito a compilação. Java o faz e Javascript também.

## Processo e Threads

Processo: Abstração do sistema operacional para rodar o seu programa
Thread: Uma linha de execução do seu programa que está dentro do seu processo.

Criar Processos vs Threads: É mais custoso criar processos pois gasta mais memória, porém ele o sistema operacional cuida de coisas como alocação de recursos e memória, o que não acontece em threads, o programador fica responsável por gerenciar a memória do prcesso entre threads.
