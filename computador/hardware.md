# Estudo - Hardware

Definição de Computador: Maquina que transforma um input realizando varias operações em um output.

Divisão do Hardware:

- CPU (Unidade central de Processamento): Parte do computador que executa instruções
- Memoria: Componente que fornece dados para a CPU utilizar
- Dipostivos I/O: Toda entrada e saída do computador (Mouses, teclados, Monitor)
- BUS de comunicação: Placa Mãe

- Dipositivos de Input: Teclado, Mouse
- Dispostiviso de Output: Monitor
- Unidade de Controle: Controla os componentes do computador através de instruções e manipulações
- ALU (Unidade aritimética e lógica): Realiza operações aritimeticas básicas
- Registradores: Noção mais básica de memória, onde são guardadas as instruções
- CPU (Unidade de central de processamento): Combinação de ALU com registradores
- Memória: Uma lista de celulas nas quais bits são gravados.

Arquitetura de Von Newman:

- Unidade de Processamento: Com uma Unidade Lógica e Aritimética, e registradores de processamento
- Unidade de Controle: Com um registrador de instrução e um registrador Program Counter
- Memória Externa:
- Mecanismos de Input e Output

## CPU

Definição: Um componente eletrônico que executa operações lógicas, aritiméticas, de controle e operações de input e output.

Divisão da CPU:

- ALU (Unidade lógica e Aritimética): Executa operações lógicas e aritiméticas
- UC(Unidade de controle): Decodifica instruções, controla o ponto de execução, direciona o fluxo de dados entre a CPU e outros dispositivos. A maioria dos recursos do computador são gerenciadas por ela.
- Registradores: Amarmazenam dados que serão variaveis usadas nas instruções

Clico de instrução:

- Busca: Busca a instrução na Memória do programa através do Registrador PC(Program Counter) que contém o endereço da instrução, que depois de retornar soma o tamanho da sua ocupação para pegar a proxima instrução.
- Decodificação: Um decodificador binário traduz a instrução para operações que a CPU precisa executar
- Execução: Sinais de controler habilitam ou desabilitam varias partes da CPU, e o output é escrito em um registrador ou colocado na memória principal.
- Repetição:

Cache da Cpu: Usado para guardar dados que são retornados mais rapidamente do que se forem pegos da memória principal(RAM).

Core: A unidade de processamento da CPU que recebe e processa instruções.

Tipos de Registradores:

- PC (Program Counter): Contem o endereço de memória da instrução a ser executada
- Stack pointer: Registrado que contém o endereço da memória do topo da stack corrente
- PSW(Program Status Word): Contém uma seríes de control bits que indicam varios dados que são usados em verificações como: O modo(kernel ou user), a prioridade da CPU, e etc.

## Memoria

Tipos de Memorias:

- Primaria (Volatil): Permite acesso rápido a dados, e só existe enquanto o computador está ligado. (Ex: RAM, ROM)
- Secundária (Não volatil): Prove acesso de longo termo aos dados (Ex:HD, SSD)

MMU(Unidade de Manjamento de Memória): Age como um mediador entre a CPU e a RAM durante a execução de um programa, traduzindo um endereço virtual criado em um endereço físico de uma memória.

RAM: Contem os dados que a CPU está processando e podem ser acessados ou de maneira ordenada ou randômica. Recebe um número em bits de endereço e retorna o dado para CPU que está contido naquele endereço. Os dados na RAM são bits, que podem representar um número, letra, instrução ou um Endereço de Memória. Não contem em si a semântica dos dados, esses são definidos pela UC(Unidade de Controle).

Idealização de Memória:

- Extremamente rápida, pelo menos mais rapida que executar uma instrução com a CPU
- Grande armazenamento
- Barata

Hierarquização de Memória (Da mais rápida e pequena, até a mais demorada e grande)

- Registradores (1nsec, 1Kb)
- Cache (2nsec, 4MB)
- Memória Principal (10nsec, 1-8GB)
- Disco (10msec, 1-4TB)
