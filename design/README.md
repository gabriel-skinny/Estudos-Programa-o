# Estudo - Design

Divisão do Design:

- Micro
- Intermediario (Design Patterns)
- Macro (Arquitetura)
- Paradigma

#### Design Patterns

Definição: Soluções de Design para resolver problemas comuns.

#### Macro (Arquitetura)

Conceitos de Design System:
- Performance
- Escalabilidade
- Latencia
- Tempo de Resposta
- Avaliabilidade
- Consistência

Tipos de Arquiteturas:

- Monolito: Uma aplicação que contem toda lógica do negocio
- Micro-Serviço: Serviços desacoplados que cuidam de uma funcionalidade da aplicação e comunicam-se entre si
- SOA(Service Oriented): Define uma maneira de manter serviços reusaveis por interfaces
- Serverless: Maneira de desenvolver uma aplicação sem implementar uma infraestrutura e manejar servidores
- Service Mesh: Serviço que serve como proxy em uma comunicação entre micro-serviços para monitora-lo e garantir a sua comunicação

Estrategias de Database 

- Escalonamento Vertical: Adicionar mais RAM, CPU e Disko ao servidor do Database
- Index: Adicionar uma tabela de indices em algumas colunas do database para facilitar o READING, porém prejudica o WRITING
- Sharding: Amazenar pequenas partes de dados em um servidor com um Database decicado
- Particionamento Vertical: Dividir uma tabela que possui muitas colunas e varias tabelas para facilitar as queries e aliviar o aglomerado de dados
- Caching: Salvar em memória os dados mais acessados para não precisar verificar o banco de dados
- Replicação: Ter uma copia do banco de dados em mais de um servidor, sendo replicado do database primario. Essa replicação pode ser feita de modo sincrono, espera a replicação acontecer para fechar a transação do database primario, ou assincrona, fecha a transação e depois atualiza as replicas 
- Data denormalization: Juntar em uma tabela dados que estão em tabelas diferentes, que são frequentemente acessados por querie complexas com joins
- Federation: Separar grandes tabelas e entidades do database em databases isolados

Boas práticas de SaSS -> Twelve Factor Apps

- Codebase: There should be a single codebase for the application, with multiple deployments.
- Dependencies: The application should explicitly declare and isolate its dependencies.
- Config: The application should store configuration in the environment.
- Backing services: The application should treat backing services as attached resources.
- Build, release, run: The application should be built, released, and run as an isolated unit.
- Processes: The application should be executed as one or more stateless processes.
- Port binding: The application should expose its services through port binding.
- Concurrency: The application should scale out by adding more processes, not by adding threads.
- Disposability: The application should be designed to start and stop quickly.
- Dev/prod parity: The development, staging, and production environments should be as similar as possible.
- Logs: The application should treat logs as event streams.
- Admin processes: The application should run admin/maintenance tasks as one-off processes.
