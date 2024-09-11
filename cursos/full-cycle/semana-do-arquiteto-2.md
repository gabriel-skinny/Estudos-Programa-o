# Estudo - Semana do Arquiteto - 2

Arquitetura de Solução X Arquitetura de Software: Aquela propõe uma solução tecnlogica de ponta a ponta de forma global e generalista, esta propõe a solução à nível desenvolvimento. Mas as duas areas se cruzam.

Lei de Conway: A estrutura do sotfware refle a estrutura da empresa. O seu software é totalmente mutável e dependente do ambiente em que vive. Então nunca uma solução de arquitetura poderá ser replicada exatamente em outra empresa.

Arquitetura: É a relação entre os objetivos do négocio e suas retrições com os componentes a serem criados visando a sua evolução. Sempre o software que está sendo desenvolvido precisa ser pensado no ambiente em que está sendo desenvolvido.

Papel do Arquiteto:

- Transformar os requisitos do negócio em padrões arquiteturais:
- Orquestrar desenvolvedores e experts de domínio
- Entende de forma profunda conceitos e modelos arquiteturais
- Auxilia na tomada de decisão nos momentos de crise
- Reforça boas práticas de desenvolvimento

Arquitetura e Desing de Software: Andam juntas, porém as decisões de design não devem refletir na arquitetura.

- Arquitetura: Escopo global (Define banco de dados)
- Design: Escopo Local (Patterns, algoritimos)

Problema de arquitetura: Precisamos de um arquitetura sólida que seja implementada da forma mais rápida possível. Então não podemos ter uma alta complexidade nem deixar muito desorganizado, é preciso um meio termo.

Como economizar 80% no inicio do desenvolvimento de um software:

- Fazer o deploy de Crud um mais simples possível para o usuario conseguir usar
- A parte mais crítica da aplicação você gasta tempo pensando em arquitetura e boas praticas. Esse será o coração do sistema e ela é normalmente a parte mais estável do sistema, então você faz ela da melhor forma possível
- As pontas da aplicação são voluveis, então não importa se elas são feitas de modo desleixado, elas estão constatantemente sendo reescritas.

Principio de Monolith First do Martin Fowler: Fui estipulado em 2015 quando a maiorias das aplicações eram monolitos, então desenvolvedor tinham pouca experiência com micro-serviços.

Principio mais importante de micro-serviços: Entender protocolos de comunicação e como eles acontecem.

Quando Não devemos começar com microserviços:

- Baixo conhecimento sobre o domínio
- Empresa em consolidação em seu modelo de negocio
- Imaturidade da equipe: Não conhecem principios de desacoplamento, regras de comunicação, desacustumados a fazer deploy
- Processos de Deploy não consolidados
- Observabilidade
- SRE(Site realability enginering): Ele precisa dar confiabilidade na aplicação inteira, em todos os micro-serviços

Quando podemos começar com microserviços:

- Clareza no que deve ser desenvolvido
- Modelos validados dentro da própria empresa
- Princípio da familiaridade: Facilmente aprendível a qualquer pessoas que entrar na equipe
- Toolkits internos: Padronizações para criar novos serviços prontas
- Infraestrutura adequada
- Tem uma cultura clara de Devops e SRE
- Observabilidade

Lei de Lehman

- Lei da Mudança Contínua: O Software vai sempre precisar estar em mudança, se ele não mudar ele não conseguirá acompanhar o negócio
- Lei do Crescimento da Complexidade: Conforme o software cresce ele necessariamente ficará mais complexos, menos que você trabalhe ativamente para simplifica-lo, e isso acontece parando de expandi-lo para refator as partes já desenvolvidas
- Lei da Conservação da Familiridade: Quanto mais familiar menos esforço é necessario para manter um software
- Lei da Conservação do Esforço: Quanto mais o software cresce mais esforço é necessario para adicionar novas features

Acomplamento: É necessario até certo ponto, porém sua excessão torna necessario muito código ser reescrito, aumenta sua complexidade e aumenta os erros.

Acomplamento Eferente: Um serviço depende de outro de forma unilateral, de modo que se esse componente cai, ele também o faz.

Acoplamento Aferente: Serviço que recebe dependencia de outros

Medir o acoplamento dos seus serviços é importante até para saber quem alocar para alterar suas partes, pois não alocaremos junior para alterar serviços que tem muitos acomplamentos aferentes. Quanto mais critico o acoplamento, mais senior a pessoa precisa ser para mexe-lo.

Não existe reecrever um sistema do zero em uma empresa seria, é preciso ir desacoplando os serviços aos poucos.

As vezes uma solução de software não funciona pois estamos muito focados em pensar nos detalhes de desenvolvimento e não buscamos entender o negocio para fazer o software com a melhor arquitetura possível.
