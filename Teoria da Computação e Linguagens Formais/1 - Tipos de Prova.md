# Tipos de Prova

## Prova por Dedução

Consiste de uma sequência de afirmações cuja verdade nos leva a alguma afirmação inicial chamada **hipótese** a uma afirmação **conclusão**.

**Forma:** Se $a$ então $b$ ou $a \to b$

**Base:** Provar que $P(1)$ é verdadeiro.

**Passo de Indução:** Para cada $i>0$ , assuma que $P(i)$ é verdadeiro (*hipótese de indução*) e use esta suposição para mostrar que $P(i+1)$ é verdadeiro.

### Exemplo:

**Teorema:** Se $x$ é a soma dos quadrados de quatro inteiros positivos, então $2^x \geq x^2$.

**Dados:**

1. $x = a^2 + b^2 + c^2 + d^2$
2. $a>0, b>0, c>0, a>0$

**Propriedades:**
3. $a^2>0, b^2>0, c^2>0, d^2>0$ - Propriedade da Aritmética

$$x+1 = a^2+b^2+c^2+d^2$$
$$x = a^2 + b^2 + c^2 + d^2 - 1$$

$$2^{x+1} \geq {(x+1)}^2$$
$$2 \cdot 2^x \geq x^2 + 2x + 1$$
Supondo que $2^x \geq x^2$:
$$2\cdot x^2 \geq x^2 + 2x + 1$$
$$x^2 - 2x -1 \geq 0$$
A inequação possui solução real, já que, por Báskhara, $\Delta = 5$.

Logo, provamos o teorema.

## Prova por Indução

Aplicada quando há definições recursivas.

### Exemplo:

**Definição recursiva de árvore**

**Base:** Um único nó é uma árvore, e esse nó é a raíz da árvore.

**Indução:** Se $T_1, T_2, ..., T_k$ são árvores, então podemos formar uma nova árvore da seguinte forma:

1. Comece com um novo nó $N$, a raíz da árvore.
2. Adicione cópias de todas as árvores $T_1, ..., T_k$.
3. Adicione arestas desde o nó N até as raízes de cada uma das árvores de 2.





