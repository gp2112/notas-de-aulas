# Processo de Poisson

## Distribuição de Poisson

Seja a Variável Aleatória $X$ o número de ocorrências por intervalo fixo (de tempo ou espaçco), dizemos que $X$ tem distribuição de Poisson com parâmetro $\lambda$.

$X \sim Poisson(\lambda), \lambda > 0$

com função de probabilidade:

$P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!}$

$E(X) = \sum_{k=0}^\infty{k \frac{\lambda^k e^{-\lambda}}{k!}}$

$Var(X) = \sum_{k=0}^\infty(k-E(X))\frac{\lambda^k e^{-\lambda}}{k!} = \lambda$

### Teorema 1
Sejam $X$ e $Y$ variáveis aleatórias independentes tais que $X \sim Poisson(\lambda)$ e $Y \sim Poisson(\nu)$

$X + Y \sim Poisson(\lambda + \nu)$

Portanto:

$P(X+Y = n) = \frac{(\lambda+\nu)^n e^{-(\lambda+\nu)}}{n!}, n=0,1,...$

### Teorema 2
Sejam as variáveis aleatórias $N \sim Poisson(\lambda)$ e $M|N \sim Binomial(N,p)$, então

$M \sim Poisson(\lambda p)$

Portanto:

$P(M=k) = \frac{(\lambda p)^k e^{-\lambda p}}{k!}, k=0,1,...$

Dem.: 

$f(k, n, p) = \frac{n!}{k!(n-k)!} p^k(1-p)^{n-k}$
...

## Distribuição Exponencial
Frequentemente usada para modelar o tempo entre eventos que ocorrem a uma taxa média constante.

Se $X$ é uma variável aleatória com distribuição exponencial, sua função densidade de probabilidade tem a forma:

$f(x) = \lambda e^{-\lambda x}, x > 0, \lambda > 0$

Notação: $X \sim Exponencial(\lambda)$ ou $X \sim Exp(\lambda)$

Probabilidades são facilmente calculadas:

$P(a<X<b) = \int_a^b{\lambda e^{-lambda x} dx} = e^{-lambda a} - e^{-\lambda b}$

$E(X) = \int_0^\infty x \lambda e^{-\lambda x} dx = \frac{1}{\lambda}$

$Var(X) = \int_0^\infty (\frac{x-1}{\lambda})^2 \lambda e^{-\lambda x} dx = \frac{1}{\lambda^2} = \frac{E(X)}{\lambda}$

![[Pasted image 20220519114123.png]]

### Falta de Memória

Seja $X \sim Exp(\lambda)$, então:

$P(X>t+s|X>t) = \frac{ P(X>t+s, X>t) }{ P(X>t) } = \frac{P(X>t+1)}{P(X>t)}$
$P(X>t+s|X>t) = \frac{e^{-\lambda (t+s)}}{e^{-\lambda t}} = e^{-\lambda s} = P(X>s)$

Assim

$P(X>t+s|X>t) = P(X>s)$

É a única distribuição contínua com tal propriedade.

### Taxa de Falha/Risco

Seja $X$ uma variável aleatória continua positiva com função de distribuição $F$ e função de densidade $f$. A função <span style="color:red">taxa de falha</span> é definida como:

$P(X \in [t,t+dt]|X>t) = \frac{P(X \in [t,t+dt])}{P(X>t)} \approx \frac{f_x(t)dt}{1-F_x(t)} = h(t)dt$

Em particular, se $X \sim Exp(\lambda)$

$h(t) = \frac{ \lambda e^{-\lambda x} }{ e^{-\lambda x} } = \lambda$  --> Taxa de Falha constante.


Sejam $X_1, X_2$ variáveis aleatórias independentes, então:

- Se $X_i \sim Exp(\lambda)$ e $Y = X_1 + X_2$

$F_y(y) = \int \int_{x_1+x_2\leqy} f_{x_1}(u)f_{x_2}(v) dudv$
