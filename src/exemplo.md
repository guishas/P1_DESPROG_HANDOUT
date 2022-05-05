Sprint 2
======

Primeira ideia
-------------

Vamos primeiro imaginar que temos um conjunto de palavras separadas, como o dicionário abaixo. Agora, imagine que queremos saber se um conjunto de caracteres, como a string abaixo, consegue ser segmentado em uma sequência de palavras desse nosso dicionário separadas por espaço. 

``` py
dicionario = {"i", "like", "ice", "cream", "icecream", "sam", "sung", "samsung"}
string = "ilikeicecream"
```

??? Checkpoint

Pense um pouco e responda, no exemplo acima, você acha que é possível segmentar a string em uma sequência 
de palavras do nosso dicionário?

::: Gabarito
Sim! É possível segmentar a nossa string em um conjunto de palavras presentes no dicionário. As sequências de palavras seriam:

``` py 
i like ice cream
i like icecream
```

Perceba que podemos formar duas sequências de palavras! Não apenas uma.

:::

???

<!-- Normalmente, a saída do algoritmo vai nos retornar verdadeiro (**True**), se for possível formar pelo menos uma sequência de palavras, ou falso (**False**) se não for possível formar uma sequência. -->

Mas espera, batendo o olho assim é fácil responder mas como o computador vai saber responder esse problema se ele não é capaz de olhar? O que é preciso fazer para chegar na resposta?

??? Checkpoint

Tente elaborar uma lógica **simples** para solucionar o problema.

::: Gabarito

De forma bem simples, tudo que devemos fazer é percorrer a string de entrada e checar se o sufixo, que sempre começa sendo o primeiro caractere da string, está presente no dicionário, se ele estiver e o resto da string pode ser quebrada em palavras do dicionário retornamos `md True`, caso o loop termine e não tenha retornado true, é porque não foi possível separar a string de entrada em palavras do dicionário e por isso retornamos `md False`.

``` py 
enquanto existem caracteres não checados
    se sufixo está no dicionário e o resto da string pode ser quebrada em palavras do dicionário
        retorna verdadeiro
    
se acabar o loop, retorna falso
```

Se não entendeu, não se desepere, vamos destrinchar essa ideia mais pra frente.

:::

???

Para facilitar o entendimento, vamos implementar nossa ideia inicial em Python.

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    for i in range(1, tamanho):
        if string[0:i] in dicionario and resto da string pode ser quebrada em palavras do dicionário:
            return True
        
    return False
```

??? Checkpoint

Como vocês podem ver, o código está incompleto, qual código em python deve ser escrito para substituir `md resto da string pode ser quebrado em palavras do dicionário`?

::: Gabarito

Nesse caso, devemos usar recursividade! Para saber se o resto da string pode ser quebrada em palavras do dicionário precisamos simplesmente chamar a função wordBreak passando como parâmetro de string de entrada o nosso prefixo (restante da string)! O código em python ficaria:

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    for i in range(1, tamanho):
        if string[0:i] in dicionario and wordBreak(string[i:tamanho], dicionario):
            return True
        
    return False
```

:::

???

Pronto, então temos o código do nosso algoritmo que resolve o problema!

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    for i in range(1, tamanho):
        if string[0:i] in dicionario and wordBreak(string[i:tamanho], dicionario):
            return True
        
    return False
```

??? Checkpoint

Err... quase, o código acima possui dois erros. Quais?

::: Gabarito

1. O primeiro erro é sobre a função range(). Em python, a função range() recebe como segundo parâmetro onde devemos parar, porém esse número não está incluso, por isso devemos adicionar 1 no tamanho da string para poder percorrer ela até o final!

2. O segundo erro é que a nossa função nunca vai acabar, porque não temos uma condição para acabar com a recursividade. Para resolver esse problema, podemos colocar uma checagem se a string de entrada for vazia, pois no final do loop, a variável `md i` vai ser igual ao tamanho da string e por isso tentaremos passar para a função a string de entrada `md string[tamanho:tamanho]`, e isso é uma string vazia `md ''`. Caso essa checagem seja verdadeira, retornamos `md True`.

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    if (string == '') {
        return True
    }

    for i in range(1, tamanho+1):
        if string[0:i] in dicionario and wordBreak(string[i:tamanho], dicionario):
            return True
        
    return False
```

:::

???

Algoritmo Recursivo
--------

Agora sim! Temos nosso algoritmo pronto.

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    if (string == '') {
        return True
    }

    for i in range(1, tamanho+1):
        if string[0:i] in dicionario and wordBreak(string[i:tamanho], dicionario):
            return True
        
    return False
```

Basicamente, o que a função `md wordBreak` está fazendo é:

1. Percorre pelos índices da string de entrada

2. Acessa o primeiro índice

3. Guarda o tamanho da string de entrada

4. Checa se o prefixo está no dicionário e recursivamente checa se o sufixo pode ser quebrado em palavras do dicionário

5. Se sim, retorna True e a função acaba

6. Se não, volta para o passo 2 porém acessa o próximo índice e repete os passos até que a função acabe

Explicação

??? Exemplo

* Input: **"code"**

* Dicionário: **{c, od, e, x}**

::: Output
![](recursive/recursive1.png)


{green}(*True*)
:::

???


Usando a árvore recursiva do exercício anterior como exemplo, podemos calcular a complexidade no tempo do algoritmo recursivo. O **primeiro passo** será olhar para a árvore e contar quantas chamadas da função onde temos uma string não vazia. 

:recursive

A string orginal ("code") possui 4 caracteres (c, o, d, e). Logo: $$n = 4$$

A quantidade de chamadas recursivas não vazias, a qual depende de n, pode ser expressa da seguinte forma: $$Chamadas = 2^{n-1}$$

Dessa forma, para **n** diferentes, temos:


| **n**       | **Chamadas** |
|--------------|--------------|
| **1**        | **1**        |
| **2**        | **2**        |
| **3**        | **4**        |
| **4**        | **8**        |
| **5**        | **16**       |
| **6**        | **32**       |
| **...**      | **...**  |

Aplicações
--------

O algoritmo é interessante pois permite que algumas aplicações sejam otimizadas:

* Motor de pesquisa/busca

  Ao fazer uma pesquisa no [Google](https://www.google.com.br/) ou outros mecanismos de busca, mesmo que a frase esteja errada, incompleta ou sem espaços, o algoritmo entende o que você gostaria de pesquisar. Mas você ja pensou em como isso pode ser feito? 

??? Exemplo
![](exemplo-google.png)
???

   O nosso algoritmo seria uma maneira alternativa de chegar no mesmo resultado do Google!  

* Identificador de plágio

    Outro exemplo de aplicação possível seria usar o algoritmo para construir um identificador de plágio. Mas como isso funcionaria?
    
    Primeiro, separamos as palavras do texto original e a definimos como o dicionário fixo. Em seguida, passamos a sequência de caracteres do texto que desejamos verificar. 
    
    Com base na proporção das respostas, chegamos à uma conclusão se o texto foi de fato plagiado ou não. Algumas situações onde essa aplicação se tornaria útil: Correções textuais de escolas/faculdades, citações de textos cíentificos, etc. 

??? Curiosidade

:::

O algoritmo é um dos mais requiridos em entrevistas de software de grandes empresas como Google, Facebook, Amazon, etc. Fica a dica!

:::

???

Comparando o algoritmo recursivo com o algoritmo dinâmico
------------

|--------------------------------|----------|
| **Recursivo**        | {red}(**$$O(2^n)$$**)   | 
| **Dinâmico**         | {green}(**$$O(n)$$**)     |

??? Exercício 1

Dado o dicionário e a string de entrada abaixo, o que seria printado no terminal?

``` py 
dicionario = {'quero', 'não', 'comer', 'lápis', 'bolo', 'cadeira', 'de', 'chá'}
string = 'nãoquerocomerbolodecadeira'

print(wordBreak(string, dicionario))
```

::: Gabarito

Seria printado `md True`, pois é possível separar a string de entrada em "não quero comer bolo de cadeira".

```
True
```

:::

???

??? Exercício 2

Dado o dicionário abaixo, o que seria printado no terminal?

``` py 
dicionario = {'quero', 'não', 'comer', 'lápis', 'bolo', 'cadeira', 'de', 'chá', 'querobo'}

print(wordBreak('querolápisdechá', dicionario))
print(wordBreak('comercomerbolo', dicionario))
print(wordBreak('nãonãonãonãonão', dicionario))
print(wordBreak('querocadeiradchá', dicionario))
print(wordBreak('', dicionario))
print(wordBreak('querolápiss', dicionario))
print(wordBreak('querobolodechá', dicionario))
```

::: Gabarito

```
True
True
True
False
True
False
False
```

!!! Cuidado
Repare que na útlima chamada, a palavra `md querobo` presente no dicionário faz com que a função retorne `md False` pois o sufixo `md lodechá` não satisfaz as checagens da função.
!!!

:::

???

??? Desafio 1

É possível modificar o algoritmo recursivo para nos retornar todas as possíveis separações da string de entrada ao invés de retornar `md True` ou `md False`. Tente implementar essa modificação.

::: Gabarito

Essa modificação recebe o nome de [backtracking](https://www.geeksforgeeks.org/word-break-problem-using-backtracking/), pois nós sempre voltamos para o começo da string e fazemos o processo todo de novo.

``` py 
def backtrackingWordBreak(string, resultado, dicionario):

    tamanho = len(string)

    for i in range(1, tamanho+1):

        if string[0:i] in dicionario: # Se o prefixo estiver no dicionário, checa o resto da string recursivamente

            if tamanho == i: # Se acabou a string, printa
                resultado += string[0:i]
                print(resultado)
                return 

            backtrackingWordBreak(string[i:tamanho], resultado+string[0:i]+" ", dicionario)

dicionario = {"mobile", "samsung", "sam", "sung", "man", "mango",
"icecream", "and", "go", "i", "love", "ice", "cream"}
string = "iloveicecreamandmango"

backtrackingWordBreak(string, "", dicionario)
```

A saída desse programa seria:

```
i love ice cream and man go
i love ice cream and mango
i love icecream and man go
i love icecream and mango
```

:::

???

Você também pode criar

1. listas;

2. ordenadas,

assim como

* listas;

* não-ordenadas

e imagens. Lembre que todas as imagens devem estar em uma subpasta *img*.

![](logo.png)

Para tabelas, usa-se a [notação do
MultiMarkdown](https://fletcher.github.io/MultiMarkdown-6/syntax/tables.html),
que é muito flexível. Vale a pena abrir esse link para saber todas as
possibilidades.

| coluna a | coluna b |
|----------|----------|
| 1        | 2        |

Ao longo de um texto, você pode usar *itálico*, **negrito**, {red}(vermelho) e
[[tecla]]. Também pode usar uma equação LaTeX: $f(n) \leq g(n)$. Se for muito
grande, você pode isolá-la em um parágrafo.

$$\lim_{n \rightarrow \infty} \frac{f(n)}{g(n)} \leq 1$$

Para inserir uma animação, use `md :` seguido do nome de uma pasta onde as
imagens estão. Essa pasta também deve estar em *img*.

:bubble

Você também pode inserir código, inclusive especificando a linguagem.

``` py
def f():
    print('hello world')
```

``` c
void f() {
    printf("hello world\n");
}
```

Se não especificar nenhuma, o código fica com colorização de terminal.

```
hello world
```


!!! Aviso
Este é um exemplo de aviso, entre `md !!!`.
!!!


??? Exercício

Este é um exemplo de exercício, entre `md ???`.

::: Gabarito
Este é um exemplo de gabarito, entre `md :::`.
:::

???
