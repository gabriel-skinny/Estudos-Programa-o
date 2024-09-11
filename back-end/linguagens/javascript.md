# Javascript

Definição: É uma linguagem interpretada de scrip, baseada em prototipo, e é multi-paradigmatica e dinâmica, podendo ser escrita tanto em OPP, imperativo e funcional. JavaScript é uma linguagem de scripting dinâmica que suporta a construção de objetos baseada em protótipos. Sua sintaxe vem de Java e C.

Objetivo: Foi criado para ser uma liguagem de script sem funcionalidade de input e ouput, isso é implementado por terceiros. Sua implementação mais comum é na Web com engines como V8 ou SpiderMonkery, e no servidor com NodeJs.

Diferenças principais do javascript

- Classes: Javascript não possui classes, a sua funcionalidade é realizada por prototipos de objetos.
- Funções são Objetos: Isso permite que as funções a capacidade para armazenar código executável e serem passadas como parametro para qualquer outro objeto.

Sistema de Tipos do Javascript:

- Numero: Valores de precisão Dupla
- String: Sequencia de Caracteres UNICODE de 16 bits cada um,
- Booleano,
- Objeto (Funções, Arrays, Date, Ragex): Coleções de pares nome-valor. É uma Hash-table do C
- null
- undefined

Definições de Variaveis:

- Var (Sem escopo)
- let e const (Com escopo)

Orientação a objetos em Javascript
This: Usado para se referenciar ao objeto do contexto. Se usado de forma global, se refere ao contexto global
New: Cria um objeto vazio e executa a função a que está atribuido com o this
Prototype: É um objeto compartilhado por todas as intanscias de um objeto, o que lhe permite adicionar novos métodos a um objeto em tempo de execução

Clousure: Uma função que retorna outra função. Elas permitem que você guarde os parametros criados na primeira função enquanto você não chamada a segunda função, pois o Garbage collector mantem a referencia dessas variaveis em um objecto de escopo.
