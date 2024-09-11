# Estudo - Kafka

Definição: Software que lida com a comunicação de eventos entre aplicações

Funcionamento interno: É um sistema distribuido que possui um Servidores e um Clientes que se comunicam via protocolo TCP. Os servidores rodam em um cluster e os que foram a storage layer, são chamados de Brokers. Os clientes são os códigos que escrevemos usando alguma blibioteca que implementa as funções do Kafka em nossa linguagem de programação.

Evento: É uma sinalização de algo que aconteceu no mundo real

Dados de um Evento:

- Key
- Value
- Timestamp
- Metadata

Producers: Quem emite um evento
Consumer: Quem consome um evento

Topic:

- Definição de uma pasta onde todos os eventos de um mesmo tipo serão enviados pelo Producer.
- São salvos em disco.
- Um ou mais consumer podem se inscrever em um topic, sendo esse agnostico entre producers e consumers
- Diferentemente de mensagens, um evento pode ficar quanto tempo for definido no seu Topic para ser consumido
- Os topics são particionados em Brokers diferentes, permitindo com um producer publique eventos do mesmo topic em Brokers diferentes.
- Os brokers mantem sempre 3 copias de uma partição de um Topic para nunca perder dados.
- Os eventos podem ser consumidos como streams, de modo que os consumers podem ir recebendo os dados em tempo real.

Broker: Camada do servidor que salva todos Topic com seus eventos

Kafka Connect Api: É possivel produzir um evento baseado na mudança de um dado de uma aplicação que não tenha o kafa implementado por meio dessa api, como a mudança de um valor no banco de dados, e etc.

Usos:

- Muito usado para empresas que lidam com streaming data
