# Estudo - Subind Aplicações Web Em Produção

- Um software nunca está pronto, ele precisa estar constantemente sendo repensado, 

- Deploy antigamente: Acessava uma maquina via SSH, e configurava tudo manualmente: Baixava mysql, instalava php, copiava os arquivos da aplicação via SFTP e a rodava

- Hoje em dia é a pior forma possível de colocar uma aplicação no Ar precisar alterar o código via FTP e configurar tudo manualmente

Heroku: Trabalha com build packs e não com containers. Ele precede o docker, e foi sua inspiraçao para criar todo seu ecosistema: docker-compose e kubernets

Dyno: 

Load-Balancer: Um processo que fica no meio da requisição do cliente a um de seus servidores web, decidindo que maquina vai receber a requisição, funcionando como um reverse-proxy 


A heroku já possui um load-balancer que determina que Dyno vai lidar com a requisição que está chegando


Gerenciamento de Dependencias: É uma das coisas mais importantes pois se uma aplicação baixa uma versão errada e ela esta quebrada o código em produção quebra. Por isso existe arquivos de lock nos gerenciadores de dependencias das linguagens, como o package.lock.json no npm 

Ideal fluxo de deploy: Integração com Github, e automatização de deploys para matar as maquinas, e controle integral sobre as instancias que estão rodando as aplicações
