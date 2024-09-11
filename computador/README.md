# Funcionamento do Computador

Definição: Fazem essencialmente a mesma coisa, recebem inputs, os manipulam e geram um output, só o fazem subindo seu nível de abstração.

- 1 Estrutura do Computador
- 2 Sistema operacional
- 3 Linguagem de Programação

## Estrutura do Computador

Definição: É uma maquina que possuem programas que recebem inputs e os transformam por operações aritimeticas.

Divisão do Computador:
1 - Hardware
2 - Sistema Operacional: Abstração dos perifericos de Hardware, fornecendo funções para manipula-los
3 - Software: Programas que manipulam dado um input do usuário

Divisão do Hardware:

- CPU (Unidade central de Processamento):
- Memoria:
- Dipostivos I/O: Toda entrada e saída do computador (Mouses, teclados, Monitor)

- Dipositivos de Input: Teclado, Mouse
- Dispostiviso de Output: Monitor
- Unidade de Controle: Controla os componentes do computador através de instruções e manipulações
- ALU (Unidade aritimética e lógica): Realiza operações aritimeticas básicas
- Registradores: Noção mais básica de memória, onde são guardadas as instruções
- CPU (Unidade de central de processamento): Combinação de ALU com registradores
- Memória: Uma lista de celulas nas quais bits são gravados.

## Linguagem de Programação

Definição: Um sistema de notações feitos para usar o computador. O seu código é um simples txt que precisa ser implementado por um compilador ou transiplador para ser executado na maquina. Uma linguagem contém sua sintaxe, semântica

Sintaxe: Regras de escritas da linguagem, que determinam quais combinações textuais produzem um significado semântico, que é uma instrução que o computador entenda.

Semântica: Determina os valores das construções textuais. Pode ser Statica ou Dinâmica

- Statica: Fazer determinações em tempo de compilação que ainda não se referem a instruções, mas que vão alem da sintaxe, que é verificar se uma variável foi citada antes de ser inicializada, funções tem os argumentos certos e etc. -
- Dinâmica: Determina como o programa vai executar as instruções nos dados determinados pela semântica statica.
  Compilador:

Sistema de Tipos:

Compilador: Um programa escrito em uma linguagem intermediaria que traduz os textos escritos definidos pela linguagem de programação compilada para código de maquina

Interpretrador: Transforma cada linha do código escrito em linguagem de maquina antes de executar, pode fazer isso de duas formas: Parseia o código e o executa, ou o traduz para uma linguagem intermediaria e o executa. Foram criadas para serem linguagens de script, que executam rapidamente e acabam. Tem a desvantagem de executar de forma mais lenta, porém economiza tempo na hora do desenvolvimento por não ter que ficar compilando o código a cada alteração. Porém muitas linguagens modernas não usam apenas um intepretador mais mesclam as duas estrategias.
