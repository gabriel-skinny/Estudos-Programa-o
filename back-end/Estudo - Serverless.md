# Estudo - Serverless

Definição: Maneira de desenvolver uma aplicação sem implementar uma infraestrutura e manejar servidores, deixando esse trabalho para um serviço de cloud(CPS).

Vantagens:

- A maior vantagem é ter custos baseados nas requisições para o servidor, pois o CPS cuida da demanda de requisição e altera as configurações das maquinas em função dela.

Servless e Arquitetura movida por Eventos: A estrategia de serveless é muito usado em serviçoes EDA, pois o serviço que processa certo tipo de evento não precisa estar ativo e gastando CPU enquanto não chegar o evento que o ative.

Disvantagens:

- Menos Controle sobre o servidor
- Lento Start-up
- Testes e Deubg mais complexos: O desenvolvedor não tem acesso aos processos que estão rodando o código
- Mais custo para rodar aplicações que executam código por um longo período de tempo

Casos de Uso:

- Micro-serviços
- Back-end de Mobile
- Processamento de dados e eventos
