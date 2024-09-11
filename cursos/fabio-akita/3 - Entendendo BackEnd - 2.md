# Entendendo BackEnd 2

Tema: Uso de Blibiotecas. Evolução do desenvolvimento de programas ate sistemas distribuidos

Programação Orientada a Objetos: Com o advento das inteface gráficas, o conceito de componentização começou a se popularizar, então as linguagens começaram a adotar o paradigma de Programção Orientada a Objetos para melhor representar esses componentes. Java o fez, mas Smalltalk o fez mais propriamente

Blibiotecas: Começou a se comercializar esse componentes que alteravam as interfaces graficas.

Database primitivo: No começo era um arquivo de texto que ficava na maquina de alguem, com uma estrutura de dados simples. Depois esse arquivo foi colocado em uma pasta compartilhada na internet, que outros programas podiam acessar. Porém só um programa poderia escrever no arquivo por vez, os outros precisavam ficar esperando.

Stream: É Modo de ler um arquivo aos poucos até chegar a parte que quer e aí pode fecha-lo ou acessar já de um posto determinado e ler um pouco do arquivo, ao invés de le-lo todo.

Servidor de banco de dados: Evoluindo de um sistema de client e servidor primitivo com um arquivo compartilhado na rede, começou a se usar um programa que controla o uso do banco, então o cliente não se conecta mais diretamente ao arquivo na rede compartilhada, mas a outro programa que serve como mediador do arquivo, executando as operações fornecidas pelos clientes. E como só ele abre e escreve no arquivo as chances de corrompe-lo são menores. É como a conexão que acontece na web, do Browser com um servidor via TCP, mas antes era via um protocolo de rede local chamdo TPX.

Storage Procedures: Com a evolução dos servidores de banco de dados, criou-se linguagens que tornaram possível colocar regras de negocio neles, tornando muito mais facil a modificação, pois não era preciso recompilar o binario que executava no computador do usuario. Mas isso ficava muito pesado para o servidor do banco de dados

Arquitetura 3 tiers: Começou a se popularizar essa arquitetura, em que se tiha um midleware que executava regras de negocio antes de chegar ao servidor do banco de dados.

Interface entre programas: Para os programas conhecerem as funções e os protocolos que os servidores de aplicações usavam, eram necessário terem uma interface com suas funções, que era feito com o IIOP.

Web: Agora o cliente não se conectava a um servidor intermediario local, mas através do browser através de internet se conectava a um web-server, que recebia inputs, mandava pro servidor do banco de dados e retornava o HTML para ser interpretado.

Alan Turing e Lamba: Lambda

Ruby e Lamba: Trouxe o conceito da lamba para o mundo web, podendo criar clousure e callbacks com funções anonimas. Inagurando o conceito de meta-lingaugem, em que se pode manipular a sua linguagem de programação para usa-la do jeito que você quiser. Tornando o paradigma imperativo atratativo novamente.

Mudanças de perspectiva dado a evolução do Hardware: Antigamente se escrevia código tentando tirar o máximo do computador, hoje como temos muito mais recursos de modo muito mais barato podemos pensar em tornar o código o mais agradável e simples possível sem se preocupar tanto em performance.

Pausa: 30 minutos
