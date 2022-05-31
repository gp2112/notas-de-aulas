# Busca em String

Por Guilherme Paixão

Dado duas *strings*, quão semelhante elas são? 
Como quantificar isso?

Calculamos o "custo" para transformar uma *string* na outra. Ou seja: quanto maior este custo, menos semelhantes elas são. 

Chamamos esse custo de *Edit Distance*.

**Um algorítmo ingênuo:**

Contabilizar quantos caracteres são iguais
```c++
int comp(string str1, string str2) {
	int i, dist=0;
	for (i=0; i<str1.length() && i<str2.length(); i++)
		dist += str1[i] != str2[i];
	return dist;
}
```

**Problema:** 
Imagine que temos ```str1 = "stop"``` e ```str2 = "tops"``` .
Utilizando esse algoritmo, seu custo seria de 4. 

Mas será que essas strings são tão diferentes?

Se deslocarmos a *str2* em uma posição à direita:

```
>>> stop
>>>  tops
```
Podemos ver que seu custo agora iria para 2!

Esse deslocamento chamamos de *gap*.

## Pesos e Gaps
Nosso algorítmo então, precisará considerar esses *gaps*, que são deslocamentos, ou espaços, que podemos fazer para manipular uma string a se igualar a outra.

Ainda, para cada operação dessa, troca e gap, podemos definir um peso.

E para cada troca, também podemos definir regras próprias, como, ter um custo diferente para trocar uma vogal por outro vogal e um vogal por consuante.

Vamos definir o peso de troca como sendo alpha(i, j), em que i é a posição da string1 e j a da string2, e *delta* como o peso de um gap.

Agora modelando nosso algoritmo, uma abordagem mais fácil, nesse caso, é a *top-down*, ou, começar por cima. É fácil de intender se fizermos de forma recursiva.

Podemos dizer que teremos um estado $S(i,j)$, em que i e j são, respectivamente, as posições da string1 e string2.

Quais os casos possíveis para cada $S(i,j)$?

1. Podemos trocar o caracter com um custo alpha(i,j).
2. Podemos realizar um gap com peso *delta* em $i$
3. Podemos realizar um gap com peso *delta* em $j$.

E após cada estado, o que acontece? Afinal analisamos apenas um estado.

1. Quando trocamos o caractere, sabemos que agora str1[i] = str2[j].
Então decrementamos as duas posições, indo para $S(i-1,j-1)$

2. Quando realizamos um gap em $i$ ou $j$, não sabemos, *a priori*, se os caracteres estão iguais. Então precisamos realizar o mesmo processo e ir para o $S(i-1, j)$ ou $S(i, j-1)$ caso o *gap* tenha sido em $i$ ou em $j$ respectivamente.

Agora é fácil de realizar nossa função de recorrência!

$S(i,j) = min\{alpha(i,j) + S(i-1,j-1), delta + S(i-1, j), delta+S(i,j-1)\}$, para $i,j>0$

$S(i,j)=j\times delta$, para $i=0$

$S(i,j) = i \times delta$, para $j=0$

Vamos por isso no código:

```c++
int alpha(int i, int j);
int delta;

int solve(int i, int j) {
	if (i==0)
		return j*delta;
	if (j==0)
		return i*delta;

	return min(
				alpha(i,j)+solve(i-1, j-1),
				delta + solve(i-1, j),
				delta + solve(i, j-1)
			);

}
```

## Complexidade

Apesar de mais fácil de modelar e desse algoritmo ser ótimo, sua implementação acima não é nada eficiente.

Para cada chamada da função *solve*, ela vai se chamar, novamente, 3 vezes. Isso gera uma árvore com, praticamente, 3 nós em cada nível.

![tree](imgs/tree.png)

A altura H da árvore será sempre em função do tamanho das duas strings, n e m, sendo que seu limite superior será a combinação linear de m e n.

$H(m,n) \leq \alpha m + \beta n$

Portanto: $H(m,n) \in O(m+n)$

O número de nós $T_{max}$ máximo dessa árvore, como ela possui até 3 filhos, é dado por:  $T_{max} = 3^H$. 

E sendo o número de Nós da nossa árvore, ou seja, o número de chamadas da função $S(i,j)$, representado por $N$:

$N \leq T_{max} \longrightarrow N \leq 3^{H(m,n)}$ 

Como $H(m,n) \in O(m+n)$

$N \leq 3^{O(m,n)} \therefore N \in O(3^{m+n})$ 

**Conclusão:** A função que implementamos é $O(3^{m+n})$ que é exponencial, sendo computacionalmente inviável para números nem tão grandes assim.

## Utilizando Programação Dinâmica
Mas, felizmente, existe uma forma de melhorar, e muito, essa complexidade utilizando programação dinâmica!

Perceba na árvore de chamadas da função que ocorrem muitas redundâncias. Podemos evitar realizar mais de uma chamada com mesmos parâmetros 
armazenando seus resultados em memória.

Existem dois jeitos de se fazer programação dinâmica: com uma abordagem *top-down*, como fizemos acima, ou *bottom-up*. Na abordagem de PD por *top-down*, utilizamos o método de *Memoization*, e na *bottom-up*, usamos o *tabulation*. 

### *Memoization*

Já que fizemos acima um algoritmo guloso utilizando *top-down*, vamos fazer o mesmo com programação dinâmica, usando o *Memoization*.

Primeiro criarei um *array* de tamanho *MAX* para salvar os resultados da nossa função $solve$.
Esse deverá ser um *array* bidimensional, já que nossa função recebe 2 parâmetros. Então temos:

```c++
const int MAX = 1000;
int MEMO[MAX][MAX];
```
Agora, a fim de podermos saber se o valor e uma posição $i,j$ do array já foi calculado, devemos inicializa-lo com algum valor para representar um espaço "vazio". Sabems que, por $i,j$ serem índices das *strings*, eles não podem ser menores que zero. Então vamos atribuir $-1$ a todo o espaço do *array Memo*. 

Para isso, podemos usar a função *memset* do *cstring*:

```c++
memset(MEMO, -1, sizeof MEMO);
```

E agora basta a gente substituir as chamadas de da função para os valores que já foram calculados:


```c++

int solve(int i, int j) {
    if (i==0)
        return j*delta;
    if (j==0)
        return i*delta;

    // se o valor já existe, não continua mais
    if (MEMO[i][j] != -1)
        return MEMO[i][j];

    MEMO[i][j] = min (
                    alpha(i,j)+solve(i-1,j-1);
                    delta+solve(i-1,j),
                    delta+solve(i,j-1)
                );
    return MEMO[i][j];
    
}

```

Como podemos ver, sempre que o estado $i,j$ já tiver sido computado, reaproveitaremos esse resultado através do valor armazenado no *arrray*.

### Tabulation

A otimização com *Memoization* já foi muito boa: reduziu um algoritmo que errra exponencial em polinomial!

Mas ainda dá para melhorar, dependendo da situação. Como dá para perceber, o *Memoization* ainda realiza chamadas recursivas, que consomem memória. Então, além de gastar com memória extra para armazenar os resultados, ainda gasta mais com cada chamada da função.

Com o método do *Tabulation*, é possível fazer o mesmo algoritmo de forma iterativa, realizando assim appenas uma chamada de função.

Dessa vez, irei chamar no *array* de *TAB*, e irei usar $M$ como sendo o tamanho da primeira string e $N$ como o tamanho da segunda:

```c++
const int MAX 1000; 
int TAB[MAX][MAX];
```

```c++

int solve() {
    int i, j;

    // preenchemos os valores iniciais de TAB com 
    // os valores retornados na condição de parada
    for (j=0; j<N; j++)
        TAB[0][j] = j*delta;

    for (i=0; i<M; i++)
        TAB[i][0] = i*delta;

    for (i=0; i<N; i++)
        for (j=0; j<M; j++) 
            TAB[i+1][j+1] = min(
                                alpha(i+1,j+1)+TAB[i][j],
                                delta+TAB[i][j+1],
                                delta + TAB[i+1][j]
                            );
    return TAB[M][N];

}

Podemos ver que, para cada umma de N operações, o programa fará mais M.

Ou seja, podemos concluir que sua complexidade, no pior cenário, será O(NM), MUITO menor que o exponencial anterior!

```
