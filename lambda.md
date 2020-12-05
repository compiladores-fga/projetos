Lambda
======

Lambda é uma linguagem de programação funcional minimalista que envolve números e funções e é baseado em um modelo de computação importante conhecido como cálculo lambda. A linguagem possui apenas alguns construtos simples:

```
// Isto é um comentário!

// Declarações de variáveis
x = 42;

// Definição de funções
fn = λ x . add x 1;

// Função auto aplicada (aplica um argumento imediatamente após a definição da função).
res = add x 1 | x = 2;

// Isto é o mesmo que  (λ x . add x 1) 2, mas é mais legível quando queremos definir 
// variáveis após utilizá-las em uma expressão
cinco = add x y 
        | x = mul 2 y 
        | y = 2;

// Aplicação de funções
res = fn 42;

// Imprimimos resultados colocando uma exclamação antes do valor a ser impresso
res = !x;

// O "if" é feito como o operador ternário em C
// O número zero é tratado como "Falso" e todos os outros números como "Verdadeiro".
cond = gt res 10;
then = 10;
else = res;
x = cond? then: else;

// Para fazer laços, utilize recursão. O código abaixo implementa o fatorial
fat = λ n . n? mul n (fat (sub n 1)): 1;
main = !(fat 5);

// Lambda não possui strings, então não dá para criar o Hello World!
// O resultado da execução de um módulo Lambda é o valor atribuído à variável "main"
```

Em Lambda, a aplicação de funções é associativa a esquerda. Assim, `add 1 2` é interpretado como `(add 1) 2`, onde `add` é uma função que recebe um argumento e retorna uma função que soma seu argumento no argumento da primeira. Em Python, seria implementada como 

```python
def add(x):
    def fn(y):
        return x + y
    return fn
```

ou na forma mais compacta `add = lambda x: lambda y: x + y`. A linguagem Lambda possui funções numéricas análogas como `add, sub, mul, div` e `mod`, além de funções de comparação como `eq, ne, gt, ge, lt, le`.

Nomes de variáveis podem ser formados por letras, números e underscore e números podem ser escrito com parte decimal ou não e sinal opcional (ex.: 42, -3.14). Todos números são interpretados como floats. A ordem de precedência confere maior precedência ao comando de imprimir, seguido de aplicação de funções, operador ternário, função auto-aplicada e finalmente a definição de funções. Desta forma, a expressão `λ x . λ y . gt x y ? a : b | a = !add x y | b = sub !x y` é interpretada como 

```
λ x . 
(
    λ y . 
    (
        (
            ( 
                ((gt x) y) ? a : b 
            ) 
            | a = ((!add) x) y
        ) 
        | b = (sub (!x)) y
    )
)
```

Crie um interpretador ou compilador de Lambda. Normalmente, a solução envolve as etapas abaixo, cada uma associada a um determinado conjunto de competências:

1. **Analisador léxico e sintático da linguagem**, que recebe uma string de código em Lambda e retorna árvores sintáticas abstratas [?], [?]. A implementação pode utilizar uma biblioteca auxiliar como o Lark. Caso prefira criar um analisador léxico ou sintático a partir do zero, inclua também as competências correspondentes a depender da técnica utilizada.
2. **Interpretador** Crie a função `eval()` do interpretador que recebe uma árvore sintática abstrata e um contexto de execução mapeando nomes de variáveis aos seus valores e executa um código Lambda. Módulos que não definem a variável "main" retornam o valor de zero.
3. **Compilador** Crie uma transformação que recebe uma árvore sintática representando um código Lambda e produz código equivalente em outra linguagem de programação como Python ou Javascript.
4. **Análise semântica**: As expressões de Lambda podem ser verificadas por um algoritmo relativamente simples conhecido como Hindley-Milner que verifica se uma expressão da linguagem é válida. O algoritmo funciona mesmo sem precisar de declarações de tipos como em linguagens staticamente tipadas como C. Esta etapa é totalmente opcional e confere uma medalha de [mestre-dos-tipos*] 