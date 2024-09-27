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
