# Processos de Decisão Markoviana

Seja uma cadeia de Markov $\{X_t, t=0,1,...\}$ com espaçco de estados $\{1,2,...,M\}$

- Após observar o estado do processo, uma **ação** deve ser tomada.
- Seja $A$ (finito) o espaço de possíveis ações.

Deseja-se obter as seguintes probabilidades:

$P(X_{t+1}=j|X_0,a_0,X_1,a_1,...,X_t=i,a_t=a), j=1,2,...,M$

que, pela propriedade Markoviana ficam:

$P(X_{t+1}=j|X_t=i,a_t=a) = P_{ij}(a), j=1,2,...,M$

### Como decidir qual a "melhor" ação a ser tomada?

Precisamos de uma **regra** ou **política de decisão** bem definida.

#### Definição
Uma política de decisão aleatória é um conjunto de probabilidades,
$\beta = \{\beta_i(a), a \in A, i \in \{1,...,M\}\}$

sendo 

$\beta_i(a) = P($escolher a ação $a \in A|X_t=i)$

Consequentemente,

$0 \leq \beta_i(a) \leq 1, \forall i, a$
$\sum_a{\beta_i(a)=1,\forall i}$

Sob uma politica $\beta, \{X_t, t=0,1,...\}$ é uma cadeia de Marov com probabilidades de transição,

$P_{ij}(\beta) = P_\beta(X_{t+1} = j|X_t=i)$
$P_{ij}(\beta) = \sum_aP(X_{t+1}=j, a_t=a|X_t=i)$
$P_{ij}(\beta) = \sum_aP(X_{t+1}=j|X_t=i, a_t=a)P($escolher a ação $a|X_t=i)$
$P_{ij}(\beta) = \sum_a{P_{ij}(a)\beta_i(a)}$

Vamos assumir que $\{X_t, t=0,1,...\}$ é uma cadeia de Marvok ergótica qualquer que seja a regra de decisão $\beta$.

As probabilidades limite são:

$\pi_{ia} = \lim_{t \to \infty}{P_\beta(X_t=i,a_t=a)}$

e as seguintes condições são satisfeitas,

$\pi_{ia} \geq 0, \sum_i{\sum_a{\pi_{ia}}} = 1$

$\sum_a{\pi_{ja}} = \sum_i\sum_a{\pi_{ia}P_{ij}(a)}, \forall j$

$\pi_{ia}$ são as probabilidades limite da cadeia estar no estado $i$ e a ação a ser selecionada.

Se as condições anteriores são satisfeitas, pode-se mostrar que:

$\beta_i(a) = P($escolher ação $a \in A|X_t=i)$
$= \frac{P(X_t=i, a_t=a)}{P(X_t=i)}$
$= \frac{\pi_{ia}}{\sum_a{\pi_{ia}}}$

### Qual a regra de decisão "ótima"?

Defina uma função de ganho $R(i,a)$ quando a ação $a$ é escolhida e o processo está no estado $i$.

Seja $R(X_i, a_i)$ o ganho obtido no tempo $i$.

Defina a política que maximiza uma função dos ganhos sujeito às condições anteriores.

No limite, temos que o ganho esperado é dado por:

$lim_{t \to \infty}{E[R(X_t,a_t)]} = \sum_i\sum_a{R(i, a)\pi_{ia}}$









