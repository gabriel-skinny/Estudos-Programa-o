# História do FrontEnd

DNS: Servidor que transforma a url que digitamos em um browser em um endereço de IP. É para onde a configuraçao de rede de nosso computador está apontando. Ela é como uma lista telefonica que transforma nome em números.

Os roteadores e Provedores conectam nosso navegador ao servidor inputado pelo DNS.

A internet só funciona pois os computadores se comunicam por um protocolo comum, que é o TCP/IP.

Web Server: É um programa que se liga a uma porta e fica escutando mensagens que chegam por ela. Sua forma mais simples e essencial é um programa que dá acesso a um arquivo da maquina, que pode ser um html que o navegador pode interpretrar e mostrar na tela.

Client: O navegador é o cliente que vai requisitar dados para o web-server através da porta exposta que é encontrada pelo DNS.

WWW: Nasce quando as pessoas começam a disponibilizar arquivos de textos para serem visualizados, e link para acessarem outras paginas

Compleficação do Web Server: Ao invés de apenas retornar um texto em HTML que será interpretrado pelo navegador, ele começou a poder retornar binários nativos, mas ele não devolvia eles desse modo, pois o navegador não saberia executa-lo, então ele o intepretava e o executava, e o resultado em texto HTML retornava ao navegador. Assim nasce os sites dinâmicos, já que seu resulltado muda a depender do que o executável faz. Antigamente isso era feito com C através de um padrão chamado CGI, mas isso era muito desnecessário, então começaram a usar uma linguagem mais adptada para lidar com "strings", o Perl, que usava REGEX.

HTML: Foi feito para fazer documentos governamentais, e para marcar estilizações que seriam definidas pela impressora ou pelo programa que o interpretava.

CSS: Foi criado para estilizar mais propriamente um texto de HTML. É uma linguagem declarativa, ela declara regras que são cascateadas para regras menores. É

Aplicações Web: Nascem quando os binários executados pelo web-server não apenas manipulavam strings e cuspiam um HTML, mas recebiam inputs, se conectavam a um banco de dados e salvavam a informação. É o que chamamos de server-side.

PHP: Foi criado para ser usado no servidor web, Apache, que o fazia para não ter que chamar um programa externo. O php está dentro do nucleo do Apacha

Servidor Web X Servidor de Aplicação: Aquele somente cospe um HTML da maquina, esse executa um binário que retorna um HTML.

GMAIL: Marca o inicio de uma revolução: A parada de usar sistema operacionais para usar paginas webs que executam um programa. Ele o foi por substituir com sucesso o aplicativo mais importante do sistema operacional, o cliente de email.

Estrutura de Arvore: Quase toda a web é baseada na estrutura de arvore. Os elementos de HTML e as estilizações do CSS o são. Sites são arvores de conteúdos que linkam outras paginas.

Frameworks: Foram criados tardiamente e servem para deixar prontas estruturas comuns como autenticação, segurança e forneciam uma estrutura base para construir o código. Criam abstrações para realizar tarefas de forma mais rapida, seguindo o conceito de Agil.

Framework javascript: Criado para os navegadores conseguirem interpretar códigos para tornar a pagina mais dinâmica, e tirar o monopolio de execução do lado do servidor.

Java: A microsoft quis um jeito de executar apenas código java nos navegadores, deixando o HTML e CSS. E para que o navegador não tivesse acesso aos recursos da maquina, o executava em um sandbox que tinha menos acessos. Isso fez com que pudesse ser feita animações avançadas na web. Daí nasce o Flash, um plugin para gerar animações, e que eram necessário para rodar vídeos.

Evolução do HTML: A Apple desenvolveu tags de videos para o HTML matando a necessidade do Flash para roda-los.

JQuery: Se tornou necessário em meados de 2008 onde a web estava em transição e mudando constantmente, e os navegadores estavam se adequando as especifiações de HTML, CSS e Javascript, tornado impossível escreve um código que funcionasse em todos os navegadores. O jquery resolvia isso, sendo uma linguagem comum que resolvia o CSS para cada navegador.

Javascript e Transpilers: Volta a evoluir quando o Flash morre, e nasce o conceitos de linguagens transpiladas, que não são códigos que serão compilados em um binário nativo de uma maquina real ou virtual, mas que são traduzidas de uma linguagem para outra linguagem, que um programa pode executar.

SASS: Pre-Processadores de CSS que torna possível aplicar lógica de programção a estilização

BootStrap: Nasce para abstrair certos estilos que estavam tornando comum na web, é construido em cima do SASS. Ninguem precisa reinventar a roda e ficar redesenhando algo já feito.

Assets e Minificação: Um navegador para executar um HTML precisa baixar todos os seus assets, e com os adventos dos frameworks, os assets começaram a se tornar cada vez mais pesados, demorava mais para enviar tantos dados pela rede. Daí que nasce o conceito de minifição, copiando as otimizações que um compilador faz do código, ele tira todas as partes desnecessárias, usadas para tornar o código legível e entendivel, e junta todos os assets e cria um arquivo só com todo o conteúdo necessário. Então para chegar nos arquivos finais otimizados, era necessário transpilar todos os frameworks, de Sass à Css, coffeScript à Javascript, isso foi chamado de Asset Pipeline. Hoje o que faz isso é o WebPack, como o Babel. O que ficou menos necessário desde que evoluimos para HTTP/2

Componentes Javascript: Ao invés de manter toda a lógica dinamica do lado do servidor, e carregar um HTML de uma pagina, começou a pensar em manipular os componentes de uma pagina e colocar a sua lógica do lado do navegador, dai que surgem frameworks javascript como Angular, React. Cada componente carrega um estado e pode afetar outro componentes. Daí nasce o conceito de uma pagina só que carrega todos esses componentes e assets, sem precisar mudar de pagina para atualizar cada estado, usando AJAX por baixo, nascendo O SAP.

Virtual DOM: Criado pelo Facebook com Reactjs, que ao invés de redesenhar toda arvore da DOM, ele modifica apenas o que precisa

Desktop e Mobile: Com o aumento da CPU e memória ram e o avançdo do EC6, podemos começar a usar a stack web, Html, CSS e Javascript, para fazer aplicativos mobile. Como o são o spotify, visual studio code. Usam de uma fina camada de javascript para se conectar com o hardware.

Dicas para estudo:

- Para entender um tecnologia é preciso saber sua hístoria, o porque ela foi desenvolvida, a que problemas ela foi desenhada para resolver, quem são as empresas por detrás dela, existem soluções melhores? Essas perguntas te darão o norte de como estudar.
- Encontra problemas para resolver e vai na tentativa e erro procurando as melhores soluções. Busque projetos open-source no github

## Linha do Tempo

- Web server fornecendo paginas estáticas em HTML
- Web server rodando binário nativo e cuspindo HTML dinâmico
- Web server fornecendo código minificado que será interpretado pelo Navegador
- Navegador executando uma pagina HTML e controlando seus componentes dinâmicamente

## Conceitos

Web:
Browser: Programa que se conecta na internet e interpreta uma linguagem para o hardware entender.
Web Server:
Navegador:

Web hoje:

- Front-End(Cliente): Busca produzir o código mais reutilizável e limpo em componentes, e com a versão mais minificada para rodar no navegador, e suas atualizações dinamicas feitas da forma mais perfomatica possível com a virtua DOM.
- Back-End(Servidor): Fornece a recebe alguns dados inputados pelo usuario nesses componentes por uma APi, que está totalmente isolada do código do front-end.

## Exercicios Praticos

- Desenvolver um código em REACT, e estudar o seu arquivo final e as manipulações que ocorrem no Browser
- Subir um Web-Serve com NGNIX, com esse arquivo.
