# Estudo - Design

Divisão do Design:

- Micro
- Intermediario (Design Patterns)
- Macro (Arquitetura)
- Paradigma

#### Design Patterns

Definição: Soluções de Design para resolver problemas comuns.

#### Macro (Arquitetura)

Tipos de Arquiteturas:

- Monolito: Uma aplicação que contem toda lógica do negocio
- Micro-Serviço: Serviços desacoplados que cuidam de uma funcionalidade da aplicação e comunicam-se entre si
- SOA(Service Oriented): Define uma maneira de manter serviços reusaveis por interfaces
- Serverless: Maneira de desenvolver uma aplicação sem implementar uma infraestrutura e manejar servidores
- Service Mesh: Serviço que serve como proxy em uma comunicação entre micro-serviços para monitora-lo e garantir a sua comunicação

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
