# FrankenPy

Existem algumas linguagens que usam (aproximadamente) a sintaxe de uma linguagem e a semântica da outra. Normalmente isto é feito traduzindo o código de uma linguagem para a outra. Alguns exemplos interessantes incluem Pyjamas (sintaxe do Python, mas roda Javascript), Coffescript (sintaxe inspirada em Ruby, mas executa em Javascript), dogelang (sintaxe parecida com Haskell, mas roda em Python) além de várias outras.

Crie seu Frankenstein de linguagens. Minha sugestão é usar uma sintaxe inspirada em C ou Javascript para escrever código Python, mas qualquer combinação entre linguagens é válida. Você pode implementar um compilador ou um interpretador. 

Caso seu FrankenPy utilize Python como a linguagem de destino, utilize as regras da atividade anterior adaptando a sintaxe para ficar com um "sabor" mais parecido com a linguagem de origem. Se, por exemplo, utilizar C, adapte os comandos para ficar mais parecido com a linguagem (ex.: "import math" poderia virar "#include<math>")


-------------------------------------------------------------------------------

# BDFL

Invente sua linguagem de programação. A avaliação desta atividade depende muito do escopo proposto. É uma linguagem genérica ou de uso específico? A linguagem implementa comandos esperados de uma linguagem moderna como declaração de funções, condicionais, etc? Qual o modelo de execução adotado? O quão sofisticada é a gramática?

Para termos de comparação, utilize as classificações propostas para as atividades acima como guia. Caso a linguagem tenha um uso interessante ou apresente idéias novas, sintaxe interessante, modelos de computação diferentes, ganhe uma medalha de [bdfl*].


-------------------------------------------------------------------------------

# Esolangs

Implemente um compilador ou interpretador de linguagem esotérica (http://esolang.org/). As competências variam muito de linguagem para linguagem, mas aqui vai uma lista das mais comuns.

* Brainfuck:
* Befunge:
* Rockstar:
* ArnoldC:

Você pode utilizar as linguagens apenas como inspiração e criar a própria esolang. Neste caso, a atividade corresponderia à atividade BDFL mostrada acima.


-------------------------------------------------------------------------------

## WebAssembly

Crie uma implemenetação Python do padrão WebAssembly: https://developer.mozilla.org/en-US/docs/WebAssembly/Understanding_the_text_format. WebAssembly é uma tecnologia bastante promissora que define uma espécie de código de máquina para a web e permite a implantação de aplicações muito rápidas rodando direto no navegador. Faríamos uma versão simplificada do WebAssembly rodando em Python. 

Do ponto de vista da sintaxe, o formato em texto da linguagem lembra uma variante de LISP, também utilizando listas de elementos entre parênteses como o principal elemento sintático. A implementação não precisa ser completa, mas deve ser capaz de realizar operações básicas como definir função, operações matemáticas com os tipos básicos e declaração de módulos.

-------------------------------------------------------------------------------

