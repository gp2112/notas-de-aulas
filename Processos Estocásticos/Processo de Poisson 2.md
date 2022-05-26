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

$P(N(s+t)-N(s)=K|N(u), u\leq s) = P(N(s+t)-N(s)=k)$

$P(N(s+t)-N(s)=k|N(u), u\leq s) = \frac{ e^{-\lambda t} (\lambda t)^k}{k!}$

$N(s+t) - N(s) \sim Poisson(\lambda t), s \geq 0, t > 0$

Assim, número de eventos em qualquer intervalo de comprimento $t$ tem distribuição de Poisson com taxa $\lambda t$ . 

<span style="color:red">Ou seja, o Processo de Poisson não depende do ponto, apenas do intervalo.</span>

**Propriedades**

- $N(t) \sim Poisson(\lambda t)$
- Portanto $E[N(t)] = Var[N(t)] = \lambda t$
- Os incrementos são estacionários, ou seja, a distribuição de $N(s+t)-N(s)$ só depende da amplitude $t$.

Processos de Poisson são, em geral, bons modelos para ocorrências aleatórias de um evento contínuo.

Alguns exemplos: chegadas de clientes em uma fila, emissão de particulas radioativas, ocorrência de uma doença rara, fótons que chegam a um telescópio espacial.

**Exemplo**

Seja $N(t) \sim Poisson(\lambda t)$, com $\lambda = 8$. Queremos calcular $P(N_{2.5}=17,N_{3.7}=22,N_{4.3}=36)$

Os eventos são equivalentes:

$\{N_{2.5}=17,N_{3.7}=22,N_{4.3}=36\}$
$\{N_{2.5}=17,N_{3.7}-N{2.5}=5,N_{4.3}-N{3.7}=14\}$

Sendo $f(t, k)$ a função distribuição de probabilidade de Poisson com parâmetro $\lambda t$

$f(2.5, 17)\times f(1.2, 5) \times f(0.6)$

**Exemplo**
Clientes chegam a uma loja segundo um processo de Poisson com taxa $\lambda = 4$ clientes por hora. Sabendo que a loja abre 9h:

- Qual a probabilidade de exatamente 1 cliente ter chegado até às 09:30?

$P(N_{0.5}=1) = \frac{e^{-2}\cdot 2^1}{1!}$

- Qual a probabilidade de chegarem 5 clientes até 11:30?

$P(N_2=5) = \frac{e^{-8}\cdot 8^5}{5!}$

- Qual a probabilidade de às 11:30 terem chegado 5 clientes, dado que às 9h chegou 1 cliente?

$P(N_2=5|N_{0.5}=1) = P(N_{1.5}=5) = \frac{e^{-6}\cdot 6^5}{5!}$


**Teorema**
Seja $\{N(t), t\geq 0\}$ um processo de Poisson com taxa $\lambda$. Então, para qualquer intervalo $B \subset [0, \infty)]$, em que $B$ é a união de um número finito de intervalos disjuntos, $B=U_{j=1}^m B_j$ com comprimento $d(B_J)=b_J$ e seja $b=\sum_{j=1}^m b_j$. Então:

$P(N(b)=k) = \frac{e^{-\lambda b}(\lambda b)^k}{k!}$

**Exemplo**

Uma empresa utiliza 10km de cabo fibra óptica, sendo 60% deste cabo de qualidade inferior(Classe B) e apresenta um número de falhas como um processo de Poisson com taxa $\lambda_B=0.2$ (falhas/km). Os outros 40% do cabo são de qualidade superior (Classe A) e o número de falhas é um processo de Poisson com taxa $\lambda_A=0.1$ (falhas/km). 

- Qual a probabilidade de pelo menos uma falha ser observada nos 10km de cabo da empresa?

$P(N(b)>0) = 1-P(N(b)=0) = 1 - (0.6\frac{e^{-1.2}\cdot (1.2)^0}{0!} +0.4 \frac{e^{-0.4}\cdot (0.4)^0}{0!})$
$P(N(b)>0) = 1- 0.6e^{-1.2} - 0.4e^{-0.4}$

- Se uma falha é observada nos 10km, qual a classificação mais provável para o cabo que apresenta a falha?

$P(A|N(b)=1) = \frac{P(N(b)=1|A)P(A)}{P(N(b)=1)}$ 

**Teorema**

Seja $\{N(t),t\geq 0\}$ um processo de Poisson com taxa $\lambda b_1$ e $N_2(t)$ um processo de Poisson com taxa $\lambda b_2$. Então, $N(t)=N_1(t)+N_2(t)$ é um processo de Poisson com taxa $\lambda b_1 + \lambda b_2$.

$N(t) \sim Poisson(\lambda(b_1+B_2))$

