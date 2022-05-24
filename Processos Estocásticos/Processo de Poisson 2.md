# Processo de Poisson #2

### Processo de Contagem

Um processo estocástico $\{N(t), t\geq 0\}$  é um processo de contagem se $N(t)$ representa o total de ocorrências de um evento até o tempo $t$.

Consequentemente,
- $N(t) \geq 0$
- $N(t)$ assume valores inteiros positivos.
- Se $s < t$, então $N(s) \leq N(t)$
- Para $s < t, N(t)-N(s)$ é o número de ocorrências do evento no intervalo $(s,t]$


**Incrementos Independentes**
Um processo de contagem tem <span style="color:red"><i>incrementos independentes</i></span> se os números de ocorrências em intervalos disjuntos são independentes.

Ou seja,

$N(t_1) - N(t_0), N(t_2)-N(t_1),...,N(t_n)-N(t_{n-1})$

são variáveis aleatórias independentes para quaisquer $t_0 = 0 < t_1 < ... < t_n$

**Indrementos Estacionários**
Um processo de contagem tem <span style="color:red"><i>incrementos estacionários</i></span> se o número de ocorrências do evento em qualquer intervalo de tempo depende somente do seu comprimento.

Ou seja, $N(s+t)-N(s)$ tem a mesma distribuição $\forall s$.

## Processo de Poisson
Um processo de Poisson com taxa $\lambda > 0$ é um processo de contagem $\{N(t), t \geq 0\}$ tal que:

- Os incrementos $N(t_1) - N(t_0), N(t_2)-N(t_1),...,N(t_n)-N(t_{n-1})$ são variáveis aleatórias independentes para quaisquer $t_0 = 0 < t_1<t_2<...<t_n$,
- $N(0)=0$
- $P(N(t+h)-N(t)=1) = \lambda h + o(h)$
- $P(N(t+h)-N(t) \geq 2) = o(h)$

**Função o(h)**
Uma função $f(.)$ é $o(h)$ se:

$lim_{h\to 0}\frac{f(h)}{h}=0$

- Se $f(.)$ é $o(h)$ e $g(.)$ é $o(h)$, então $f(.) + g(.)$ é $o(h)$
- Se $f(.)$ é $o(h)$, então $g(.) = cf(.)$ é $o(h)$

Qualquer combinação linear finita de funções $o(h)$ é $o(h)$

**Teorema**
Se $\{N(t), t \geq 0\}$ é um processo de Poisson com taxa $\lambda$. Então:

$P(N(t)=k) = \frac{ e^{-\lambda t} (\lambda t)^k}{k!} \longrightarrow N(t) \sim Poisson(\lambda), s \geq 0, t > 0$

Ou seja, o número de eventos em qualquer intervalo de comprimento $t$ tem distribuição de Poisson com taxa $lambda t$
