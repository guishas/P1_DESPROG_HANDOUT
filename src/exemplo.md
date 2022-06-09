Algoritmo de Programação Dinâmica para o Problema da Quebra em Palavras
=======================================================================

Primeira ideia
--------------

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
-----------------

Bom, agora que você já entendeu como o algoritmo funciona, podemos implementá-lo. Vamos por partes.

Queremos que nosso algoritmo percorra a string inicial até o final. Isso é fácil.

??? Atividade 1

Como ficaria o código que percorre a string inicial do seu segundo caractere ao último.

``` py 
def wordBreak(string, dicionario):

       
```

**Dica:** Você recebe a string inicial, use-a.

::: Gabarito

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    for i in range(1, tamanho):
       
```

Não estranhe começarmos pelo segundo caractere, será explicado abaixo.

:::

???

Agora, precisamos checar se uma parte dessa string está presente no dicionário **E** se o resto da string pode ser quebrada em palavras do dicionário. Qual é essa parte que devemos checar se está presente no dicionário ou não? 

??? Atividade 2

Lembre que o `md for` começa do segundo caractere e vai até ao último e isso vai ser muito útil para nós. Pense no porque ele começa no segundo caractere e não no primeiro.

**Dica:** Lembre de fatiamento de strings em python. Caso não se lembre, pesquise.

::: Gabarito

Essa parte da string que devemos checar se está no dicionário em cada iteração do `md for` é a string inicial fatiada do índice 0 até o índice `md i`. O nosso for começando pelo segundo caractere nos permite escrever o código abaixo.

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    for i in range(1, tamanho):
        if string[0:i] in dicionario and resto da string pode ser quebrada em palavras do dicionário:

```

:::

???

Ótimo, estamos progredindo, o nosso código atual está assim:

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    for i in range(1, tamanho):
        if string[0:i] in dicionario and resto da string pode ser quebrada em palavras do dicionário:

```

Vamos deixar a parte do `md resto da string pode ser quebrada em palavras do dicionário` para depois, mas já vai imaginando o que entra aqui.

??? Atividade 3

Agora pare e pense um pouco sobre essa condição dentro do `md if`, o que acontece se ela for verdadeira? E se ela for falsa?

**Dica:** O que significa a string inicial fatiada do índice 0 até o índice `md i` estar no dicionário e o resto dela poder ser de fato quebrado em palavras que estão presentes no dicionário?
**Dica 2:** O que significa o nosso `md for` acabar e a função ainda não tiver nenhum retorno?

::: Gabarito

A string inicial fatiada estar dentro do dicionário e o resto dela poder ser de fato quebrado em palavras que estão no dicionário é exatamente o que nosso problema tenta resolver, ou seja, a função deve retornar `md True`, pois a string inicial **PODE** ser quebrada em palavras do dicionário.

Mas, o que acontece se o `md for` acabar e a função ainda sim não ter retornado nada? É exatamente o contrário do que foi dito acima, a palavra **NÃO PODE** ser quebrada em palavras do dicionário e por isso retornamos `md False` logo após o `md for`.

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    for i in range(1, tamanho):
        if string[0:i] in dicionario and resto da string pode ser quebrada em palavras do dicionário:
            return True

    return False

```

:::

???

Estamos quase lá! Agora, vamos voltar na comparação `md resto da string pode ser quebrada em palavras do dicionário`. O que nossa função faz no momento é checar se uma fatia da string inicial está no dicionário e se o restante dela pode ser quebrado em palavras do dicionário, certo? Porém, se você pensar bem, a nossa função faz exatamente isso, não? Ela checa se uma string inicial pode ser quebrada em palavras de um determinado dicionário, a única diferença da nossa função para o que queremos fazer em `md resto da string pode ser quebrada em palavras do dicionário` é que o resto da string não vai ser a string inicial e sim uma parte dela.

??? Atividade 4

Pensando nisso, tente deduzir o que precisa ser feito para resolver a comparação `md resto da string pode ser quebrada em palavras do dicionário`. 

**Dica:** Lembre do que foi estudado no início da matéria de Desafios da Programação.

::: Gabarito

Se você pensou em usar recursividade, você acertou! Para resolver isso, basta chamar a nossa função recursivamente passando os parâmetros corretos. Como o nosso objetivo é checar se o **resto** da string pode ser quebrado em palavras do dicionário, precisamos passar como parâmetro esse resto da string e o dicionário inicial. O dicionário é o mesmo, então simplesmente reescrevemos, mas o resto da string pode ser um pouco difícil de enxergar. Usando fatiamento de strings e o índice `md i` que temos no nosso `md for`, podemos representar o **resto** da string como `md string[i:tamanho]`! Dessa forma, nossa função ficaria:

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

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    for i in range(1, tamanho):
        if string[0:i] in dicionario and wordBreak(string[i:tamanho], dicionario):
            return True
        
    return False
```

Faz sentido, não faz? ;)

Pronto, então temos o código do nosso algoritmo que resolve o problema!

Calma..., nosso algoritmo ainda não está 100% pronto, ele possui um problema.

??? Atividade 5

Você consegue identificar esse erro?

**Dica:** Lembre sobre os passos de como fazer uma função recursiva, mais especificamente um dos últimos passos.

::: Caso não se lembre, clique aqui.

1. entenda o que a função recebe e o que deveria fazer.
2. adicione uma chamada recursiva ao código da função.
3. passe para a chamada recursiva um parâmetro menor.
4. não simularás e terás fé.
5. você tem fé na resposta da chamada recursiva, então use-a.
6. isole o caso em que o parâmetro é o menor possível.
7. a solução desse caso é trivial, então calcule ela direto.

:::

::: Gabarito

A nossa função recursiva precisa acabar em algum momento, caso contrário, poderemos ter problemas. Para solucionar isso, basta olharmos para o **Passo 6**. Precisamos isolar o caso em que o parâmetro é o menor possível, o que no nosso caso não é trivial pois nosso parâmetro não é simplesmente um número. Voltando um pouco, vimos que nosso código ia ficar assim: 

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    for i in range(1, tamanho):
        if string[0:i] in dicionario and wordBreak(string[i:tamanho], dicionario):
            return True
        
    return False
```

O parâmetro em questão é a string fatiada, e para isolar o caso em que esse parâmetro é o menor possível basta checar quando essa string for vazia, isso porque quando nossa variável `md i` tiver o mesmo valor que a variável tamanho, a operação `md string[tamanho:tamanho]` resulta em uma string vazia `md ''`. 

O algoritmo com o erro corrigido fica assim:

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

Retornamos `md True` pois uma string vazia `md ''` teoricamente está no dicionário, esse é o motivo.

:::

???

Algoritmo Recursivo
-------------------

Agora sim! Temos nosso algoritmo recursivo para o problema da quebra em palavras.

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    if string == '':
        return True

    for i in range(1, tamanho):
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

??? Ilustrando a recursividade

``` py 
string = 'code'
dicionario = {'c', 'od', 'e', 'x'}

wordBreak(string, dicionario)
```

:tree

???

A string orginal ("code") possui 4 caracteres (c, o, d, e). Logo: $$n = 4$$

Ao analisar a árvore de recursividade, percebemos que ela aumenta exponencialmente conforme n aumenta.

Dessa forma, podemos concluir que nosso algorítmo tem uma complexidade exponencial, uma das piores possíveis, sendo então **O($b^n$)**, onde b > 1.

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

    # Cria lista com tamanho posições e cada posição com o valor False
    wb = [False]*(tamanho)

    for i in range(1, tamanho):
        
        # Se wb[i] for False, checamos se o prefixo está no dicionário
        if wb[i] == False and string[0:i] in dicionario:
            wb[i] = True
        
        # Se wb[i] for True, checamos todas as substrings começando de i+1
        # e guarda os resultados
        if wb[i] == True:

             # Chegou no último índice, retorna True
            if i == tamanho:
                return True
            
            for j in range(i+1, tamanho):

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

Esse algoritmo melhorado pode parecer confuso, mas não é tão difícil quanto parece.

:::

???

Essa estratégia é conhecida como [programação dinâmica](https://en.wikipedia.org/wiki/Dynamic_programming) e  por conta dela a complexidade desse algoritmo é $O(n)$. Esse algoritmo acima é chamado de [Algoritmo de Programação Dinâmica para o Problema da Quebra em Palavras](https://www.geeksforgeeks.org/word-break-problem-dp-32/)! Bonito né?

Agora podemos comparar a eficiência dos dois algoritmos!

| Algoritmo            |  Complexidade              |
|----------------------|----------------------------|
| **Recursivo**        | {red}(**Exponencial**)     | 
| **Dinâmico**         | {green}(**Linear**)        |

Claramente o algoritmo de programação dinâmica é muito melhor, e é dai que vem o seu nome. Agora está na hora de praticar um pouco o que foi apresentado para vocês acima. Faça os exercícios abaixo.

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
dicionario = {'quero', 'não', 'comer', 'lápis', 'bolo', 'cadeira', 'de', 'chá'}

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

??? Exercício 4

Dado o dicionário e a string de entrada abaixo, o que seria printado no terminal?

``` py 
dicionario = {'quero', 'não', 'comer', 'lápis', 'bolo', 'cadeira', 'de', 'chá'}
string = 'nãoqueroocomercadeira'

print(wordBreak(string, dicionario))
```

::: Gabarito

Seria printado `md False`, pois não é possível separar a string de entrada por causa do caractere `md 'o'` presente no meio da string de entrada. Isso porque no dicionário existe a palavra `md 'quero'` e a palavra `md 'comer'` mas não existe a palavra `md 'queroo'`. Por conta disso, o algoritmo ia retornar `md False`.

:::

???

??? Desafio

Refatore o algoritmo recursivo. É possível escrever ele com apenas 4 linhas de código.

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    if string == '':
        return True

    for i in range(1, tamanho):
        if string[0:i] in dicionario and wordBreak(string[i:tamanho], dicionario):
            return True
        
    return False
```

::: Gabarito

``` py 
def wordBreak(string, dicionario):
    tamanho = len(string)

    if string == '':
        return True

    return any([string[0:i] in dicionario and wordBreak(string[i:tamanho], dicionario) for i in range(1, tamanho)])
```

O segredo aqui é a função `md any()` do python, ela retorna `md True` se qualquer item da lista passada como parâmetro é `md True`, caso contrário a função retorna `md False`. Isso é o suficiente para nosso algoritmo continuar funcionando e ter apenas 4 linhas. O código acima é um pouco avançado, se tiver dúvida chame um de nós.

:::

???

<!-- ??? Desafio

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

??? -->