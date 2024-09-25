# Entendendo BackEnd 2

Tema: Uso de Blibiotecas. Evolução do desenvolvimento de programas ate sistemas distribuidos

## Evolução da Arquitetura de Software

Programação Orientada a Objetos: Com o advento das inteface gráficas, o conceito de componentização começou a se popularizar, então as linguagens começaram a adotar o paradigma de Programção Orientada a Objetos para melhor representar esses componentes. Java o fez, mas Smalltalk o fez mais propriamente

Blibiotecas: Começou a se comercializar esse componentes que alteravam as interfaces graficas.

Database primitivo: No começo era um arquivo de texto que ficava na maquina de alguem, com uma estrutura de dados simples. Depois esse arquivo foi colocado em uma pasta compartilhada na internet, que outros programas podiam acessar. Porém só um programa poderia escrever no arquivo por vez, os outros precisavam ficar esperando.

Stream: É Modo de ler um arquivo aos poucos até chegar a parte que quer e aí pode fecha-lo ou acessar já de um posto determinado e ler um pouco do arquivo, ao invés de le-lo todo.

Servidor de banco de dados: Evoluindo de um sistema de client e servidor primitivo com um arquivo compartilhado na rede, começou a se usar um programa que controla o uso do banco, então o cliente não se conecta mais diretamente ao arquivo na rede compartilhada, mas a outro programa que serve como mediador do arquivo, executando as operações fornecidas pelos clientes. E como só ele abre e escreve no arquivo as chances de corrompe-lo são menores. É como a conexão que acontece na web, do Browser com um servidor via TCP, mas antes era via um protocolo de rede local chamdo TPX.

Storage Procedures: Com a evolução dos servidores de banco de dados, criou-se linguagens que tornaram possível colocar regras de negocio neles, tornando muito mais facil a modificação, pois não era preciso recompilar o binario que executava no computador do usuario. Mas isso ficava muito pesado para o servidor do banco de dados

Arquitetura 3 tiers: Começou a se popularizar essa arquitetura, em que se tiha um midleware que executava regras de negocio antes de chegar ao servidor do banco de dados.

Interface entre programas: Para os programas conhecerem as funções e os protocolos que os servidores de aplicações usavam, eram necessário terem uma interface com suas funções, que era feito com o IIOP.

Web: Agora o cliente não se conectava a um servidor intermediario local, mas através do browser através de internet se conectava a um web-server, que recebia inputs, mandava pro servidor do banco de dados e retornava o HTML para ser interpretado.

## Conceitos trazido das linguagens

Ruby e Lamba: Trouxe o conceito da lamba para o mundo web, podendo criar clousure e callbacks com funções anonimas. Inagurando o conceito de meta-programação, em que se pode manipular a sua linguagem de programação para usa-la do jeito que você quiser. Tornando o paradigma imperativo atratativo novamente.

Mudanças de perspectiva dado a evolução do Hardware: Antigamente se escrevia código tentando tirar o máximo do computador, hoje como temos muito mais recursos de modo muito mais barato podemos pensar em tornar o código o mais agradável e simples possível sem se preocupar tanto em performance. Isso fez com que linguagens que implementavam lambda calculos voltarem a ativa

Erlang: Linguagem que roda em uma VM e possui um garbage collector, e não implementa inteireimente programação funcional, nem programação orientada a objeto, é flexivel e fica no meio termo. Ao invés de ter classes e objetos, tem modulos e actores. Ele tem um supervisor que funciona como um daemon, que cuida do seu ciclo de vida. Ele é um sistema operacional inteiro, não é igual ao interpretadores de Python ou Ruby, que foram feitos para iniciar rapido e terminar. O ideal é subir um processo de Erlang e deixar que ele utilize o recursos da maquina, ele foi criado para ficar em pé 99% do tempo sem ficar reinicializando, até com novos deploys.

Tipagens: A definição de tipo é importante para o compilador saber quanta memória será usada para armazenar certo de tipo de dados.

- Dinâmica: São definidos pelo interpretador no runtime do código, porém é ruim quando o interpretrador erra o tipo que você quer usar e você so descobre quando roda seu código.
- Estatica: Definir staticamente o programador precisa gastar muito tempo definindo e ele pode errar o tipo que utilizará.
- Inferencia: São inferidas pelo compilador em tempo de compilação, e o bytecode já possui os tipos certos do seu código. Typescript, Rust o fazem.

Estudar tipos é importante pois o compilador ou interpretador vai sempre precisar de ajudar para definir o tipo certo.

Gerenciamento de Dependencias: É uma coisa muito importante, pois sem elas o seu projeto não roda. É preciso ter a versão das blibiotecas certas, e ter um modo de baixa-las facilmente no ambiente de deploy. Também é preciso atualizar as blibiotecas que precisam ser atualizadas, alterar o seu código que as manipula e trocar de blibioteca caso ela esteja descontinuada. O Java começou com o gerenciado de dependencias chamado Maven que baixava os binários das suas dependencias baseado no que foi definido em um XML que tem as dependencias e suas versões, o javascript tem o NPM que também o faz.

Compilação e Dependencias em GOLang: É uma linguagem como C++, pois não é tão baixo-nivel quanto C, porém compila para um binário nativo. E também usa compilação statica, podendo move-lo de um lugar para outro e ele irá funcionar sem problemas, e sempre terá um programa rodando sem problemas depois que foi compilado. Ele baixa os códigos fontes do github, e depois compila tudo junto, ao invés de baixa-las já compiladas. Em java o que se tem no Mave são os jars, binários compilados das blibiotecas, pois o compilador do Java é muito lendo para ficar compilando tudo. Por ter compiladores mais velozes, Go, python e Ruby, com o advento do movimento de código aberto, preferem baixar o código fonte e compilar tudo de uma vez só.

Elixir: Como escrever Erlang é muito ruim, porém sua performance, principalmente para soluções de comunicação, é muito boa, então criaram o elixir que roda em cima da VM do Erlang, mas com uma sintaxe e um conjunto de blibiotecas que aumentam muito a produtividade.

Evolução das Linguagens: Não existe linguagem perfeita, porém cada uma foi trazendo inovações que foram sendo implementadas por outras linguagens, fazendo todas evoluirem. Elas resolvem problemas especificos de épocas especificas, e precisam estar constantemente trazendo novas features e melhorias.
