# Cadeias de Markov em Tempo Discreto
## Introdução
Seja ${X_t, t=0,1,...}$ um processo estocástico em tempo discreto com espaçco de estados discreto (finito ou infinito enumerável).

#### Propriedade de Markov
A probabilidade de que a cadeia assuma um certo valor futuro, quando seu estado atual é conhecido, não se altera se conhecemos o seu comportamento passado.

$X_t = i$ indica que o processo está no estado $i$ e tempo $t$.

Se o processo está no estado $i$ existe uma probabilidade fica ${P_{ij}}^{t,t+1}$ de que o próximo estado seja $j$.

Em termos probabilísticos, aplicando a propriedade Markoviana, temos que:

$P(X_{t+1}=j|X_0=i_0, X_1=i_1,...,X_{t-1}=i_{t-1}, X_t=i)$
$= P(X_{t+1}=j|X_t=i)$
$= {P_{ij}}^{t,t+1}$

para todos os possíveis valores de $t,i,j,i_0,i_1,...,i_{t-1}$

${P_{ij}}^{t,t+1}$ são chamadas **probabilidades de transição a 1 passo**.

#### Cadeias Estacionárias/Homogênias

Quando as probabilidades de transição não dependem do tempo $t$, ou seja 

${P_{ij}}^{t,t+1} = P_{ij}$

temos uma cadeia de Markov estacionária - com probabilidades de transição estacionárias.


A propriedade de Markov pode valer para uma sequência de tempos, por exemplo se distribuição de $X_{t+1},...,X_{t+k}$ só depende de $X_t$.

Para um número finito $n$ de variáveis aleatórias $X_0,X_1,...,X_n$ deseja-se obter uma probabilidade conjunta de uma particular tragetória da cadeia:

$P(X_0=i_0,X_1=i_1,...,X_n=i_n)$
$= P(X_n=i_n|X_{n-1}=i_{n-1})\times...\times P(X_1=i_1|X_0=i_0)P(X_0=i_0)$
$= P(X_0=i_0)\prod_{t=1}^n{P(X_t=i_t|X_{t-1}=i_{i-1})}$

Precisamos então das distribuições condicionais de $X_t|X_{t-1}, t=1,2,...,n$ e da distribuição de $X_0$.


### Seções

[Cadeias de Markov Reversíveis](Cadeias%20de%20Markov%20Revers%C3%ADveis.md)
[Processos de Decisão Markoviana](Processos%20de%20Decis%C3%A3o%20Markoviana.md)

