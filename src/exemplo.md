Sprint 2
======

Algoritmo de Programação Dinâmica para o Problema da Quebra em Palavras
---------

O [Algoritmo de Programação Dinâmica para o Problema da Quebra em Palavras](https://www.geeksforgeeks.org/word-break-problem-dp-32/) busca resolver um problema interessante. Vamos primeiro imaginar que temos um 
conjunto de palavras separadas, como o dicionário abaixo. Agora, imagine que queremos saber se um conjunto de 
caracteres, como a string abaixo, consegue ser segmentado em uma sequência de palavras desse nosso dicionário separadas por espaço. 

``` py
dicionario = {"i", "like", "ice", "cream", "icecream", "sam", "sung", "samsung"}
string = "ilikeicecream"
```

??? Exercício

Pense um pouco e responda, no exemplo acima, você acha que é possível segmentar a string em uma sequência 
de palavras do nosso dicionário?

::: Gabarito
Sim! É possível segmentar a nossa string em um conjunto de palavras presentes no dicionário. As sequências de palavras seria:
``` py 
i like ice cream
i like icecream
```

Perceba que podemos formar duas sequências de palavras! Não apenas uma.

:::

???

Normalmente, a saída do algoritmo vai nos retornar verdadeiro (**True**), se for possível formar pelo menos uma sequência de palavras, ou falso (**False**) se não for possível formar uma sequência.

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
