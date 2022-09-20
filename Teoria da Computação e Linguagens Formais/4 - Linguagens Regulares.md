# Linguagens Regulares

Linguagem regular é uma linguagem que pode ser expressa por uma expressão regular.

Seja um alfabeto $\Sigma$:
- A linguagem vazia ($L = \oslash$) é regular
- Se $x$ é um elemento qualquer do alfabeto $\Sigma$, a linguagem formada pelo conjunto desse elemento ($L = \{x\}$) é uma linguagem regular.
- Se $A$ e $B$ são linguagens regulares, então as linguagens formadas por $A \bigcup B$ , pela concatenação ($L = A \bullet B$) e fecho de Kleene ($L=A^*$ ou $L=B^*$) desses conjuntos também são LRs.
- Nenhuma outra linguagem sobre o alfabeto $\Sigma$ é regular.
## Lema do Bombeamento

O Lema do Bombeamento define as condições necessárias para que uma linguagem seja regular.

Se L é uma linguagem regular, então:
- $\forall L \ \exists p>0$, $p$ -> Comprimento de Bombeamento da linguagem L
- $\forall w \in T(L),$  $|w| \geq p \rightarrow \exists x,y,z$ tal que
	- $w = xyz$
	- $y \neq \epsilon$ 
	- $|xy| \leq p$
	- $\forall i \geq 0, xy^iz \in T(L)$
O valor mínimo do comprimento de bombeamento $p$ é chamado de *mínimo comprimento de bombeamento* da linguagem $L$. 
