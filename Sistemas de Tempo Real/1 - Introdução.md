# Introdução

### Noção Intuitiva

Um sistema é dito de tempo real se a sincronização de eventos internos com a dinâmica do ambiente é de responssabilidade do sistema.

Um sistema de tempo real:

- Possui um limite de tempo de resposta;
- é correto se o valor de resposta e o tempo estão corretos;
-  Preditibilidade temporal -- se é determinístico ou estocástico;

> "Queremos evitar indeterminismo temporal, ou seja, maximizar o determinismo temporal do sistema."


### RT com respeito à dependência do modelo

**Erro** -> **Falta** -> **Falha**

- **Sistema**
	- **Erro:** causa do problema
	- **Falta:** consequência do erro no sistema
- **Ambiente do Usuário**
	- **Falha:** comportamento errado do sistema para o usuário

**Tolerância a faltas:**

- Conceito base para sistemas de Tempo Real!

$c$  -> *tempo de resposta (custo)*
$d$ -> *deadline*
$\delta$ -> *delay*

normalmente: $$\delta = c - d, se \ c > d$$$$\delta = 0, se \ c \leq d$$
### Tempo Real Rígido (*Hard Real-Time*)

Qualquer falta no atendimento do *deadline* implica em falha no sistema.

ex: Alarme de reator nuclear, despertador.

Rigidez $\neq$ Criticalidade: 

- **Rigidez:** o quão estrito é o requisito.
- **Criticalidade:** O quão danoso é a falha.

### Tempo Real Não-Rígido *(non-Hard Real-Time)*

Possui um limite de faltas de deadlines.

- Excessos de faltas implica em falha.

#### Tempo Real *Firm*:

- Respostas atrazadas são inválidas

#### Tempo Real *Soft*

- Respostas atrazadas são degradadas
- Requisições continuam no sistema - qualidade cai.