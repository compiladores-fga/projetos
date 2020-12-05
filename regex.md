Motor de expressões regulares
=============================

Crie um compilador de expressões regulares que realize todas as etapas necesárias para processamento de expressões regulares, até a criação de um motor simples baseado em autômatos para identificação de strings que pertençam à linguagem regular definida. Este trabalho utiliza várias competências e pode ser entregue de forma incompleta, com soluções para apenas alguns dos problemas apresentados na criação de um motor de expressões regulares completo.

Se realizado até o final, espera-se um código que funcione de forma similar ao exemplo abaixo:

```python

from modulo_regex import Regex

# Compila a expressão regular
re = Regex(r"a(b|c)*d")

# Verifica se as strings pertencem à linguagem proposta
re.test("abbccd")    # -> True
re.test("ad")        # -> True
re.test("aabbccdd")  # -> False
```

O trabalho entregue deve implementar a arquitetura de um compilador tradicional, com várias etapas de processamento:

1. Começamos com a análise léxica e sintática das expressões regulares para obter uma representação na forma de uma árvore sintática. Esta etapa pode utilizar uma biblioteca como o Lark.
2. A etapa seguinte consiste em transformar a árvore sintática em um NFA-e utilizando a construção de Thompson. 
3. Posteriormente, fazemos a conversão do autômato correspondente para um autômato DFA (ou NFA sem transições epsilon). 
4. Finalmente, executa-se o autômato para verificar se uma string de entrada faz parte da linguagem regular definida. 
   
Cada etapa mencionada e os critérios de avaliação estão descritos abaixo.


## Etapa 1: Análise léxica e sintática

Para fins deste trabalho, é necessário implementar apenas um subconjunto das expressões regulares válidas. Primeiramente, assumimos que o alfabeto de entrada corresponde apenas às letras e números do alfabeto (sem considerar acentos). Você pode ampliar este conjunto se quiser, mas não é necessário.

A linguagem para expressões regulares também precisa incluir apenas os operadores de alternativas (ex.: `a|b`), de repetições (ex.: `a*`), de concatenação (ex: `ab`) e de agrupamento (ex.: `(ab|c)*`). Lembre-se que a precedência destes operadores segue as regras usuais para expressões regulares: o operador de repetição possui maior precedência, seguido da concatenação e finalmente a alternativa. Assim, uma expressão como `a|bc*` deve ser interpretada como `a|(b(c*))`.

As produções vazias (geralmente representadas pelo símbolo ε) são representadas por uma alternativa vazia no operador `|`. Assim, uma regra que seria representada como `a|ε` viraria simplesmente `a|`. Lembre-se que o ε só é relevante acompanhado por um operador de alternativas já que concatenções e repetições com ε podem ser simplesmente omitidas (por exemplo: `aε*` vira `a`, já que uma string não é alterada se for concatenada com várias strings vazias).

Alguns operadores comuns não precisam ser implementados já que podem ser redefinidos a partir destes operadores básicos de expressões regulares. No entanto, você pode implementá-los se preferir. Alguns exemplos disto são: símbolos opcionais como `a?` que podem simplemente serem escritos como `(a|)` e `a+` que vira `aa*`. 

### Competências

[re-ler], [re-criar], [re-prog], [re-pat]. [lex-ler], [lex-re], [cfg-classicas], [cfg-bnf], [cfg-op], [cfg-ast]

Implemente o lexer ou o analisador sintático manualmente para obter competências adicionais como [lex-prog*] ou [rd-prog]. 


## Etapa 2: Construção de Thompson

Nesta etapa, convertemos a árvore sintática abstrata em um autômato NFA-e de acordo com a construção de Thompson. Um nó de árvore sintática como `Tree(alt, ["a", "b"])` viraria um autômato com as regras de transição dadas abaixo: 

```python
start = {0}
accept = {5}
delta = {
    1: {"a": {3}},
    2: {"b": {4}},
}
epsilons = {
    0: {1, 2},
    3: {5},
    4: {6},
}
states = {0, 1, 2, 3, 4, 5}
```

Crie uma representação adequada para um autômato NFA-e, lembrando-se de especificar as regras de transição, os estados iniciais,
os estados finais, as transições epsilon e o conjunto completo de estados. 

### Competências

[dfa-repr], [nfa-repr], [nfa-thompson]


## Etapa 3: Simplificação do autômato

Crie um código para eliminação das transições epsilon para obter um NFA. A partir deste ponto, você deve decidir se vai converter este NFA em um DFA. A escolha reflete na etapa em que deseja-se aumentar a complexidade do código: na parte de análise ou na parte de execução. 

Aqui devemos formalizar os argumentos para eliminação das transições episilon. No caso acima, poderíamos eliminar a primeira transição epsilon de 0 para 1 fazendo as seguintes mudanças no autômato

```python
start = {0, 1}
accept = {5}
delta = {
    0: {"a": {3}},
    1: {"a": {3}},
    2: {"b": {4}},
}
epsilons = {
    0: {2},
    3: {5},
    4: {6},
}
states = {0, 1, 2, 3, 4, 5}
```

### Competências

[nfa-epsilon], [nfa-dfa]

Algumas simplificações como a eliminação de estados não-ligados a nenhum estado inicial ou final são simples de realizar de maneira informal, mas relativamente complicadas de implementar em código. Para isto, precisamos de técnicas de travessia de grafos que nem sempre possuem implementações muito óbvias. Implemente estas simplificações básicas para receber uma medalha de [mestre-dos-grafos*].


## Etapa 4: Execução do autômato

Implemente o método "test(str) -> bool" do autômato, que recebe uma string de entrada e executa o autômato para decidir se a string faz parte da linguagem regular considerada ou não. 

### Competências

[dfa-prog], [comp-org], [proj-comp*], [proj-dsl-gramatica*]

