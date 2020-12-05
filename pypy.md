PyPy
====

PyPy é uma implementação do interpretador de Python em Python. Talvez de forma surpreendente, a versão em http://pypy.org é cerca de 4 vezes mais rápida que a implementação tradicional em C. A nossa será **muitas vezes mais lenta** e contemplará apenas uma fração relativamente pequena da linguagem. 

Crie um interpretador de Python em Python. Python é uma linguagem complexa e uma implementação completa como trabalho de disciplina é inviável. Seu projeto deve implementar apenas uma funcionalidade mínima:

* Reconhecer inteiros, floats e strings nas suas versões mais simples.
* Operações matemáticas básicas (+, -, *, @, /, %, //, **)
* Operadores de comparação (possivelmente proibindo comparações compostas como a > b > c).
* Laços while e for.
* Condicionais com if/elif/else.
* Declaração de variáveis.
* Declaração de funções com argumentos posicionais.
* Chamada de funções com argumentos posicionais.

É possível acrescentar um integrante a mais ao grupo sem dividir as competências, se ambos implementarem as seguintes funcionalidades adicionais:

* Listas, conjuntos e dicionários. 
* Operadores bitwise (^, |, &, ~).
* Comparações compostas: `a > b < c` é interpretado como `a > b and b < c`
* Declaração de lambdas.
* Comando import (`import mod` e `from mod import a, b, c`)  

Para incluir um terceiro membro, precisamos de algumas funcionalidades a mais:

* Compreensão de listas, conjuntos e dicionários de um único laço
* Tuplas
* Indexação simples (ex.: `lst[1], d["key"]`)
* Atribuição de índices (ex.: `lst[1] = 1`)
* Comando with.

Lembre que tuplas são definidas pelo operador `,`, exceto a tupla vazia, definida como `()`.

