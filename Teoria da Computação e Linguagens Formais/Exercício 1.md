
**1. Prove usando a indução, que a soma dos $n$ primeiros números ímpares é igual a $n^2$**.

Sendo $x_k$ o k-ésimo número ímpar: 

$$P(n) = \sum_{k=1}^n x_k = n^2$$
Provando $P(n-1)$: $$P(n-1) = P(n)-x_n$$$$(n-1)^2 = n^2 - x_n$$$$n^2 -2n +1 = n^2 - x_n$$$$x_n = 2n-1$$
Provamos que $x_n$, $n\geq 1$ , é ímpar. Assim, provamos também que o teorema é verdadeiro.

**2. Prove, usando indução estrutural, que uma árvore binária de altura $h$ possui, no máximo, $2^{h+1}-1$ vértices.**

Suponto uma árvore binária totalmente balanceada, em que $T_k$ representa o número de vértices acumulados até o $k$-ésimo nível e $N_k$ representa o número de vértices no nivel $k$:

$$T_h = 2^{h+1}-1$$
$$T_h = T_{h-1} + N_h \therefore T_{h}-T_{h-1} = N_h$$
$$2^{h+1}-1 - 2^{h} + 1 = N_h$$
$$N_h = 2\cdot 2^h - 2^h$$
$$N_h = 2^h$$
Como a árvore é binária e perfeitamente balanceada, sabemos então que o número de vértices em um nível $k$ é $2^k$, o que corresponde ao resultado.
**3. Provar: se $p^2$ é par, então $p$ é par.**

Considere P o conjunto dos números pares.

Vamos supor que $p$ é ímpar:

$$p = 2k+1, k \in \mathbb{N}$$
$$p^2 = (2k+1)^2 = 4k^2 + 4k + 1$$
$$p^2 = 4k(k+1) + 1$$
$$p^2 \notin P$$ Logo, provamos por contradição que, se $p^2$ é par, $p$ deve ser par.