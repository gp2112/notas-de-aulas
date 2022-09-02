# Autômatos Finitos Não Determinístico

Um autômato não determinístico é como um autômato determinístico, com a única diferença que a função de transição $\delta$ é uma função total de $Q \times \Sigma$ para $2^Q$, ou seja, de $Q\times \Sigma$ para o conjunto dos subconjuntos finitos de $Q$.

A função de transição $\delta$ retorna um subconjunto de estados, ao invés de um estado único.

Para cada estado $q_1$ e $q_2$ e todo símbolo $v$ em $\Sigma$, se $q_2\in \delta(q_1,v)$, existe um vértice do nó $q_1$ para o nó $q_2$. 
O fato do autômato ser não-determinístico implica que **pode haver mais de um vértice com o mesmo rótulo $v$.**

Seja um autômato finito não-determinístico, dizemos que existe um caminho $w$ do estado $q_1$ ao estado $q_2$ para alguma palavra $w\in \Sigma$ se $q_2\in \delta^*({q_1,w})$ .

### Equivalência entre AFD e AFND

**Teorema:** se L é reconhecida por um AFND, então ela é reconhecida por uma AFD.

#### Exemplo:

Determinar se a palavra $w \subset \Sigma, \Sigma = \{x \in \{0,1\}\}$ possui $01$ no fim.

##### Não Determinístico

|       | 0             | 1     |
| ----- | ------------- | ----- |
| $q_0$ | $\{q_0,q_1\}$ | $q_0$ |
| $q_1$ |    -     | $q_2$ |
| $q_2$ |   -       | -  |

#### Determinístico

|       | 0     | 1     |
| ----- | ----- | ----- |
| $q_0$ | $q_1$ | $q_0$ |
| $q_1$ | $q_1$ | $q_2$ |
| $q_2$ | -     | -     |

$q_0$ $\{q_0,q_1\}$ 


## Autômatos FInitos com $\epsilon$ transições

