# Semana do Arquiteto - 3 DevOps e SRE

Objetivo: Como pensar de forma estrategia um sistema que suporte multiplos deploys diarios com automação e confiança.

Deploy antigamente:

- Fazia upload dos novos arquivos via FTP e a empresa precisava parar seu funcionamento para subir a nova versão.
- Grandes empresas tinham data-centers em que rodavam a suas aplicações, porém eles normalmente ficavam na mesma região
- Programadores debugavam as aplicações diretamente nos mainframes em produção
- Não tinha metricas de software, apenas de hardware

Antigamenta Separação de Dev e Infra:

- Dev: implementava todas os requisitos mandava para teste e depois enviava para a pessoa especializada de infra para subir para produção
- Infra: Recebia o software em produção e mantinha métricas em relação a infraestrutura

Briga de Dev e Infra: Essa divisão causava briga, pois o código do desenvolvedor sempre tornava o ambiente instável. Quando acontecia um erro um culpava o outro, ao invés de focar no processo. E o desenvolvedor não tinha acesso a logs para debuggar o erro.

Cultura de DevOps: Aproximação de desenvolvedores e profissionais de infra para diminuir o processo de delpoy. Isso depois se viu tão importanto que pessoas começaram a assumir esse papel

Cargo Devops:

- Pode ser especializado como dev ou infra
- Tem conhecimento do processo de entrega de um software
- Conhece ferramentas para automatização de processos
- Define os processos de

SRE(Site Reliability Engineering): Criar processos de confiabilidade para manter as aplicações rodando. E para isso precisa olhar todo o ecosistema do software, tudo o que pode afeta-lo e começar arquitetar soluções para resolver os problemas, tentando garantir uma funcionalidade perfeita do software.

DevOps X SRE: O SRE está necessariamente ligada a área de DevOps, já que ele precisa saber dos procedimentos de deploy para fazer seu trabalho, mas o DevOps não está ligado ao SRE.

Métricas para SRE:

- SRA(Service Level Agreement): Acordo entre empresa e cliente sobre a disponibilidade do sistema
- SLO (Service Level Objective): Objetivos internos de métricas da disponibilidade do sistema, que sempre deve estar acima do SRA.
- SLI (Service Level Indicator): Indicatores para medir os SLO's
- Error Budget: A quantidade de tempo que um serviço pode estar indisponível sem quebrar o SLO

DORA Metrics: Conjunto de métricas para medir performance das equipes de desenvolvimento em relação a entrega de software com rapidez e qualidade.

- Lead time for changes: Tempo que uma equipe leva desde o incio do desenvolvimento de uma mudança até o seu deploy. Quanto menor melhor
- Deployment Frequency: Frequência dos deploys. Quanto maior, normalmente maior é a maturidade do time.
- Mean Time to Recovery: Tempo médio para restaurar um serviço
- Change Failure Rate: Porcentagem das falhas que sobem para produção

Principio de registro de Processo: É necessario de artefatos para serem utilizados nas empresas para elas analisarem os deploys e poderem julgar os seus processos, principalmente quando dão falhas.

Documento Post Mortem: Descreve o processo de um erro e sua solução, é muito importante para empresas resolver problemas em seus processos.

Escalabilidade: Não é só subir maquinas e diminui-las.

- Picos de Acesso:
- Entendimento do Négocio: Exige alta leitura ou Alta gravação
- Memória vs CPU para escalar: Criar maquinas com os recursos certos baseado na sua aplicação
- Node Pools: Criar pools baseado no tipo de recursos: Pols com maquina com mais memória ou com mais CPU
- Banco de Dados: O maior problema é a quantidade de conexões, não é lidar com processamento
- Solução do banco:
  - Conexões: Criar um pool de conexões para não ficar abrindo e fechando conexões diretamento no banco
  - Criar replicas para leitura e escrita.
  - Criar replicas por região e fazer um sharding.
- Cache: Criar in memory cache para não precisar fazer leituras no banco toda hora
- Esquentar o cache: Rodar scripts para preencher o cache com dados antes de um pico de requisição para não deixar que muitas requisições simultâneas acessem o banco

Plataform Engineering: Papel de profissional que cria uma plataforma profissional que abstrai todas as complexidades de escalabilidade: Manter varias maquinas, fazer sharding de banco de dados, definir Cloud provider, deixando o desenvolvedor focar em desenvolver a solução e fazer o deploy da forma mais fluída possível. Isso também garante uma padronização muito grande, o que garante a confiabilidade e uma flexibilidade para tomar decisões.
