# Entendendo BACKEND

- CPU: Entende algumas instruções para manipular dados em registradores
- Registradores: São onde são armazenadas variaveis

Assembly: Linguagem que fala diretamente com o hardware

Sistema operacional: Abstrai funções mais complexas que o hardware oferece

Compilador: Transforma o código escrito em uma linguagem de programação, fazendo varias otimizações, em um binário executável para aquela maquina especifica

Uso de Blibiotecas em programas:

- Link statico: Junta os códigos em um unico binário. É melhor para transportar para outra maquina que não tem as blibiotecas instaladas. A linguagem GO faz isso.
- DDL(): Declara as funções que vão ser utilizadas de uma blibioteca por um arquivo Header, e linka ao binário já instalado na sua maquina

Intepretador: Não transforma seu programa em binário nativo, mas é um programa que vai executando um arquivo de texto escrito em uma linguagem que ele entende. Linguagens intepretadas: Perl, Php, Pyhton, Ruby e Javascript. Ele incialmente foi feito para rodar scripts que iniciavam e terminavam rapidamente.

Processo: Toda vez que iniciamos um programa o sistema operacional aloca bits em memória e cria uma entidade chamada processo, podendo incia-lo, pausa-lo e finalizado. Um processo não sabe de outros processos que estão ao redor, ele se sente como a unica coisa rodando na maquina, ao menos se perguntar ao sistema operacional.

Threads: Uma linha de execução em paralelo dentro de um processo.

Memória: São paginas do nosso HD e seu tamanho é definido pelo computador podendo ser de 32 bits ou 64 bits.

Memória Virtual: Cada processo tem acesso ao seu espaço na memória virtual, que é apontada para um endereço de memória físico, o que faz com que nenhum processo consiga invadir a memória de outro processo.

Process Fork vs Threads: Como as threads estão no mesmo processo elas tem acesso a toda memória virtual do processo e elas podem invadir a memória uma da outra. Para escrever bom programas multi-threas precisamos garantir que o código de uma thread não pise na memória de outra thread que está executando em paralelo.

Servidor Web: São processos que para atender requisições precisam criar um fork do seu processo, o que é feito com CGI, porém no windows isso é muito caro, então era feito com ISAP

Scheduler: A CPU possui um Scheduler que define o tempo de execução das threads. Mas ele só pode rodar algumas threads ao mesmo tempo, então ele fica pausando algumas threads por alguns critérios e executa outras que estavam pausadas.

Maquina Virtual: É uma evolução de um intepretador, que não quer apenas executar uma linguagem de programação, mas abstrair o proprio sistema operacional. É o que o Java fez com sua JVM. Então o compilador do Java gera um binário nativo para a JVM executar, como um intepretador. E isso faz com que sua inicialização seja extremamente lenta. Então idealmente a JVM vai rodar como um processo executando varios processos em Java, e eles para rodarem em paralelo terão que usar threads. É preciso que toda a maquina seja dada a JVM para que se ganhe o melhor beneficio.

JVM: A JVM faz uma técnica chamada JIT, que vai otimizando o binário em tempo de execução, a vantagem é que é possível compilar mais rapidamente, deixando as otimizações para serem realizadas. Alguns navegadores fazem isso também com o javascript. A vantagem da JVM é sua portabilidade, podendo rodar em qualquer sistema operacional com o mesmo código, eles só precisam baixa-las. As linguagens intepretradas dependem muito de chamar por baixo dos panos chamadas do sistema operacional, a JVM abstrai tudo isso em Java. A linguagens modernas como Perl, Php, Ruby fazem binding de blibiotecas já instaladas no sistema operacional, o que pode ser ruim se a blibioteca não for thread safe, impedindo do programa rodar threads em paralelo. Então os interpretadores que foram criados em linux funcionam melhor em sistema unix, por terem suas blibiotecas open-sources, as suas funções não serão as mesmas no Windows.

Diferença de Java e .NET: Embora sejam as duas maquinas virtuais e compilem para byte-codes, o Java tem com o objetivo a portabilidade para todos os sitemas operacionais, e o .NET só em windows, fazendo binding de funções que só existem no windows, o que a faz ganhar mais performance do que o Java, que reescreve todas as suas funcionalidades.

### Principios de desenvolvimento:

- Temos que escrever o código para outros programadores ler, o compilador vai se encarregar de fazer as otimizações de performance para a maquina executar
- Programação é sobre fazer escolhas entre opções que são definidas pelo contexto, nenhuma é totalmente errada em todas as situações. É como uma arte, é sobre escolhar a solução certa no lugar certo.
