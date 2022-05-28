# Busca em String

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
			)

}
```

## Complexidade

Apesar de mais fácil de modelar e desse algoritmo ser ótimo, sua implementação acima não é nada eficiente.

Para cada chamada da função *solve*, ela vai se chamar, novamente, 3 vezes. Isso gera uma árvore com, praticamente, 3 nós em cada nível.


![[Pasted image 20220527154913.png]]
A altura H da árvore será sempre em função do tamanho das duas strings, n e m, sendo que seu limite superior será a combinação linear de m e n.

$H(m,n) \leq \alpha m + \beta n$

Portanto: $H(m,n) \in O(m+n)$

O número de nós $T_{max}$ máximo dessa árvore, como ela possui até 3 filhos, é dado por:  $T_{max} = 3^H$. 

E sendo o número de Nós da nossa árvore, ou seja, o número de chamadas da função $S(i,j)$, representado por $N$:

$N \leq T_{max} \longrightarrow N \leq 3^{H(m,n)}$ 

Como $H(m,n) \in O(m+n)$

$N \leq 3^{O(m,n)} \therefore N \in O(3^{m+n})$ 

**Conclusão:** A função que implementamos é $O(3^{m+n})$ que é exponencial, dendo computacionalmente inviável de se computar para números nem tão grandes assim.

## Utilizando Programação Dinâmica
Mas, felizmente, existe uma forma de melhorar, e muito, essa complexidade utilizando programação dinâmica!

Perceba na árvore de chamadas da função que ocorrem muitas redundâncias. Podemos evitar essas chamadas
