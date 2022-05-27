Sprint 2
======

Primeira ideia
-------------

Vamos primeiro imaginar que temos um conjunto de palavras separadas, como o dicionário abaixo. Agora, imagine que queremos saber se um conjunto de caracteres, consegue ser segmentado em uma sequência de palavras desse nosso dicionário separadas por espaço. 

``` py
dicionario = {"i", "like", "ice", "cream", "icecream", "sam", "sung", "samsung"}
```

??? Exemplo 1 

Pense um pouco e responda, usando o dicionário acima, você acha que é possível segmentar a string abaixo em uma sequência 
de palavras do nosso dicionário?

``` py
string = "ilikeicecream"
```

::: Gabarito
Sim! É possível segmentar a nossa string em um conjunto de palavras presentes no dicionário. As sequências de palavras seriam:

``` py 
i like ice cream
i like icecream
```

Perceba que podemos formar duas sequências de palavras! Não apenas uma.

:::

???

??? Exemplo 2

Mantendo o mesmo dicionário, mas agora uma string diferente, você acha que é possível segmentá-la em uma sequência 
de palavras?

``` py
string = "ilikecake"
```

::: Gabarito
Não! Embora partes da palavra estão presentes no dicionário, "cake" não está. Ou seja, não é possível segmentar essa string em um conjunto de palavras presentes no dicionário. 

:::


???

??? Exemplo 3

Você já deve ter pegado a ideia, mas para verificar com um último exemplo. Usando o mesmo dicionário, você acha que é possível segmentar a string abaixo em um conjunto de palavras do dicionário?

``` py
string = "ilikesamssung"
```

::: Gabarito

Não! Se você pensou que era possível, cuidado! O fato de existir o "s" entre "sam" "sung", que são palavras do dicionário, impede que essa string possa ser segmentada. 

:::

???


Aplicações
----------

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

Com base na proporção das respostas, chegamos à uma conclusão se o texto foi de fato plagiado ou não. Algumas situações onde essa aplicação se tornaria útil: correções textuais de escolas/faculdades, citações de textos cíentificos, etc. 

??? Curiosidade

::: Clique aqui

O algoritmo/problema é um dos mais requiridos em entrevistas de software de grandes empresas como Google, Facebook, Amazon, etc. Fica a dica!

:::

???


Algoritmo Ingênuo
--------

lógica simples aqui

abordar o algoritmo de uma forma ingênua, pequenos passos para o usúario ir percebendo que aqui caberia uma recursividade



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

Mas calma, nosso algoritmo ainda não está 100% pronto, ele possui dois erros:

1. O primeiro erro é sobre a função range(). Em python, a função range() recebe como segundo parâmetro onde devemos parar, porém esse número não está incluso, por isso devemos adicionar 1 no tamanho da string para poder percorrer ela até o final!

2. O segundo erro é que a nossa função nunca vai acabar, porque não temos uma condição para acabar com a recursividade. Para resolver esse problema, podemos colocar uma checagem se a string de entrada for vazia, pois no final do loop, a variável `md i` vai ser igual ao tamanho da string e por isso tentaremos passar para a função a string de entrada `md string[tamanho:tamanho]`, e isso é uma string vazia `md ''`. Caso essa checagem seja verdadeira, retornamos `md True`.

Algoritmo Recursivo
--------

Agora sim! Temos nosso algoritmo recursivo para o problema da quebra em palavras.

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    if string == '':
        return True

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

??? Como a recursividade funciona

``` py 
string = 'code'
dicionario = {'c', 'od', 'e', 'x'}

wordBreak(string, dicionario)
```

::: Árvore de recursividade
![](recursive/1.png)



:::

???


Usando a árvore recursiva acima, podemos calcular a complexidade no tempo do algoritmo recursivo. O **primeiro passo** será olhar para a árvore e contar quantas chamadas da função onde temos uma string não vazia. 

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

Portanto, a complexidade no tempo do algoritmo recursivo é **O($2^n$)**.

Ingenuidade
-----------

Claramente, a complexidade desse algoritmo recursivo é horrível, basta visualizar a árvore de chamadas recursivas acima. Essa visualização evidencia o motivo da ineficiência: redundância de chamadas. É possível perceber que fazemos **duas** chamadas iguais de **WB(de)** e **quatro** chamadas iguais de **WD(e)**. A imagem abaixo deixa isso visível para vocês.

![](redundance.png)

O algoritmo melhorado
---------------------

Para resolver a ineficiência acima, podemos fazer uma modificação muito simples: manter um *cache* que armazena o resultado das chamadas já feitas. Esse cache pode ser, por exemplo, uma lista `md wb[tamanho]`, onde `md tamanho` é o tamanho da string de entrada + 1. 

A ideia é armazenar em cada índice `md i` o retorno do algoritmo usando a string de entrada `md string[0:i]`. Inicialmente, todo elemento da lista `md wb[tamanho]` é inicializado com algum valor inválido, digamos `md False`, indicando que o valor `md wb[string[0:i]` ainda não foi calculado. Depois dessa inicialização, basta rodar uma versão modificada da recursão, que simplesmente devolve o resultado pronto se ele já foi calculado antes.

Essa estratégia é conhecida como [memoização](https://en.wikipedia.org/wiki/Memoization).

Mas calma! Isso significa que, para resolver o problema, precisamos apenas preencher a lista. E aí temos o pulo do gato: não precisamos de um algoritmo recursivo para fazer isso. Esse preenchimento pode ser feito por um algoritmo interativo!

Vamos usar essa sacada para reescrever nosso algoritmo, escondendo a recursão.

??? O algoritmo melhorado

::: Descubra!

``` py 
def dynamicWordBreak(string, dicionario):
    tamanho = len(string)

    if tamanho == 0:
        return True

    # Cria lista com tamanho posições e cada posição com o valor -1
    wb = [False]*(tamanho+1)

    for i in range(1, tamanho+1):
        
        # Se wb[i] for False, checamos se o prefixo está no dicionário
        if wb[i] == False and string[0:i] in dicionario:
            wb[i] = True
        
        # Se wb[i] for True, checamos todas as substrings começando de i+1
        # e guarda os resultados
        if wb[i] == True:

             # Chegou no último índice, retorna True
            if i == tamanho:
                return True
            
            for j in range(i+1, tamanho+1):

                # Atualiza wb[j] se for False e está no dicionário
                if wb[j] == False and string[i:j] in dicionario:
                    wb[j] = True

                # Chegou no último caractere
                if j == tamanho and wb[j] == True:
                    return True
    
    # Se checamos todos os índices e não retornou True
    # Retorna False e termina
    return False
```

Esse algoritmo melhorado pode parecer confuso, mas não é tão difícil quanto parece. (Falta explicação aqui).

:::

???

Essa estratégia é conhecida como [programação dinâmica](https://en.wikipedia.org/wiki/Dynamic_programming) e  por conta dela a complexidade desse algoritmo é $O(n)$. Esse algoritmo acima é chamado de [Algoritmo de Programação Dinâmica para o Problema da Quebra em Palavras](https://www.geeksforgeeks.org/word-break-problem-dp-32/)! Bonito né?

Agora podemos comparar a eficiência dos dois algoritmos!

| Algoritmo            |  Complexidade       |
|----------------------|---------------------|
| **Recursivo**        | {red}(**$O(2^n)$**) | 
| **Dinâmico**         | {green}(**$O(n)$**) |


??? Exercício 1

Dado o dicionário abaixo e a string de entrada, quais seriam as possíveis sequências de palavras formadas?

```py 
dicionario = {'hoje', 'vou', 'jogar', 'play', 'station', 'playstation', 'de', 
'cadeira', 'sofa'}

string = 'hojevoujogarplaystation'
```

::: Gabarito

As possíveis sequências de palavras seriam:

```py
hoje vou jogar play station
hoje vou jogar playstation
```

:::

???

??? Exercício 2

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

??? Exercício 3

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
True
```

!!! Cuidado
Repare que na útlima chamada, a palavra `md querobo` presente no dicionário faz com que a única sequência de palavras possível seria: `md quero bolo de chá`, pois quando o algoritmo checar o cojunto de caracteres `md querobo`, vai ver que está presente no dicionário e vai recursivamente checar se o sufixo pode formar uma sequência, mas o sufixo `md lodechá` não permite formar um sequência que está presente no dicionário!
!!!

:::

???

??? Desafio

É possível modificar o algoritmo recursivo para nos retornar todas as possíveis separações da string de entrada ao invés de retornar `md True` ou `md False`. Tente implementar essa modificação.

**Dica:** Pense em como armazenar a string de saída e preenchê-la ao longo do loop.

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