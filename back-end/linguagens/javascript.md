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
- Array: É um objeto porém tem a propriedade length que é atualizada toda vez que se adciona um elemento
- null
- undefined

Definições de Variaveis:

- Var (Sem escopo)
- let e const (Com escopo)

## Orientação a objetos em Javascript

Class: São funções que precisam ser instanciatadas com o operador new, que retorna um objeto contendo os metodos e propridades da classe.

This: Usado para se referenciar contexto em que uma função foi criada. Se usado de forma global, se refere ao contexto global
New: Cria um objeto vazio e executa a função a que está atribuido com o this
Prototype: É um objeto compartilhado por todas as intanscias de um objeto, o que lhe permite adicionar novos métodos a um objeto em tempo de execução

Clousure: Uma função que retorna outra função. Elas permitem que você guarde os parametros criados na primeira função enquanto você não chamada a segunda função, pois o Garbage collector mantem a referencia dessas variaveis em um objecto de escopo.

this:

- Function Context: É definido quando o body da função é evaluated pelo javascript, é como uma variavel escondida que é preenchida quando chamada pelo seu contexto, como seus argumentos. O This muda baseado em como a função foi chamada.
- Arrow Function: Cria uma closure com o this do outer-scope, a linguagem não altera seu binding.
- Constructor: O This é o objeto retornado pelo New.

## Funções

Definição: São first-class objetcs, isso significa que elas podem ser asinaladas por variaveis, passadas como argumento para outras funções, e retornada de outras funções.

Tipos:

- Normais: Definidas pela keyword "function" e com um nome
- Anonymous function: Definies pela keywork "function" mas sem nome, e podem ser asinaladas a variaveis em runtime
- Arrow functions: Não tem o seu proprio this, arguments, super, ou new.target e são sempre anonymous. São usadas quando não queremos definir um this pelo contexto, e sim usar o this definido no parent scope.

Clousure: Uma função que possui um enviroment definido pelo seu scopo, que fecha todas as suas variaveis para o outer-scope e possui as variaveis das funções que a contem.

Scope-Chain: As variaveis das funções mais externas tem menos prioridade para formar as clousers das funções internas, de modo que são sobreescritas as variaveis definidas dentro das innerfunctions.

Inner functions: Funções podem ser declaradas dentro de funções, e possuem acesso as variaveis declaradas no escopo da função pai e global.
