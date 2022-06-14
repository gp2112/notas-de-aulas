# Sistema de Filas

Uma classe de modelos em que os clientes chegam de uma maneira aleatória a um serviço.

- Na chegada eles são **obrigados** a esperar na fila até que seja sua vez de serem atendidos.
- Uma vez atendidos, geralmente presume-se que eles saiam do sistema.

Para esses modelos, estaremos interessados em determinar:

1. O número médio de clientes no serviço (ou fila)
2. O tempo médio que um cliente passa no serviço (ou espera na fila).

### Definições:

- $L$ -> Número médio de clientes no serviço.
- $L_Q$ -> Número médio de clientes esperando na fila.
- $W$ -> A quantidade média de tempo que um cliente passa no serviço.
- $W_Q$ -> O tempo médio que um cliente passa esperando na fila.

**Proposição:** Sejam $\lambda$ a taxa média de chegada de clientes que entram no serviço, ou seja, se $N(t)$ denota o número de chegadas de clientes no tempo $t$, então: $$\lambda = \lim_{t\to \infty} \frac{N(t)}{t}$$\

Portanto, o número médio de clientes em serviço $L$ é proporcional a quantidade média de tempo que um cliente passa no serviço $W$, ou seja:
$$L = \lambda W$$\

## Probabilidade de Estado Estacionário

Se $X(t)$ denota o número de clientes no sistema no tempo $t$, define-se por $P_n, n \geq 0$, por: $$P_n=\lim_{t \to \infty} P(X(t)=n)$$\
$P_n$ é a probabilidade limite ou de longo prazo de que haverá exatamente $n$ clientes no sistema.

Por exemplo: se $P_0=0.3$, então, a longo prazo, o sistema ficará sem clientes por 30% do tempo.

Da mesma forma, $P_1=0.2$ implicaria que em 20% do tempo o sistema teria exatamente um cliente.


