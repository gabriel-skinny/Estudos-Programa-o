# Estudo - Docker
Definição: Criado para garantir compatibilidade, portabilidade e igualdade de comportamento para programas desenvolvidos em ambiente diversos

Container: Uma unidade de software que enpacota seu código a todas suas dependências o isolando de um ambiente especifico.

Image: Definições das dependencias necessarias para rodar uma aplicação

Conteitos da Imagem:
- Imutabilidade: Uma vez criada, são imutaveis, só poderão ser modificadas se criar outras imagens em cima dela
- São constituidas de Layers: Cada layer representa uma modificação no sistema de arquivos: adicionando, removendo ou alterando arquivos

Container image: Um processo isolado que contem todas as dependencias para rodar uma aplicação, o codigo, runtime, ferramentas do sistema, blibiotecas e configurações. O que pode ser importado para qualquer maquina e rodar do mesmo jeito 

VM vs Container: O primeiro virtualiza o hardware, o segundo o sistema operacional. Uma VM possui um sistema operacional inteiro com seu proprio kernel, hardware drivers, programas e aplicações. Subir uma VM para isolar uma aplicação utilizaria muitos recursos. Enquanto um container é só um processo isolado com todas as dependências necessarias para rodar o seu projetos, se valendo do kernel do sistema operacional

Registry: Um lugar centralizado que ficam imagens criadas de uma aplicação


Docker-compose: Usado para explicitar a comunicação e infraestrutura de seus containeres. Faz toda a configuração de uma infraestrutura de uma aplicação e a relação dos containers para funcionar a sua aplicação 


Kubernetes: Software que gerencia os seus containers, ele te oferece uma estrutura para rodar os seus sitemas distribuídos conteinerizados, contendo um load balancer, controlar os conteneirs de forma controlada, utilizar melhor os recursos da maquina por conteiner, reiniciar containers que falharam.
