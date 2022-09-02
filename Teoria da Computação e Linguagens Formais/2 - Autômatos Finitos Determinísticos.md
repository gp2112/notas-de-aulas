# Autômatos Finitos Determinísticos

Um AF deterministico (AFD) é denotado formalmente por uma **quíntupla**
$(Q, \Sigma, \delta, q_o, F)$ .

- $Q$ -> conjunto finito de estados;
- $q_o$ -> é um elemento de $Q$;
- $F \subseteq Q$ -> é um conjunto de estados finais;
- $\delta$ -> é a função total, chamada de função de transição, de $Q\times \Sigma$ a $Q$

## Esquema da Máquina e Representação usando Grafos

#### Esquema
```nomnoml
[<table>Fita com sequência de símbolos de Sigma |1|1|0|1|1|0|0|0|1|0|]
```

```nomnoml
[<usecase>p;estado anterior]a-> símbolo lido[<usecase>q;novo estado]
```

#### Exemplo

Cadeia de Binários: $\Sigma = \{0, 1\}$ .
Criar uma AF tal que: $\{w_{10} \ | \ w_{10} \ mod \ 4_{10} \equiv 0\}$

```nomnoml
[<usecase> S0] -> 1 [<usecase> S1]
[<usecase> S0] 0 -> [<usecase> S0]

[<usecase> S1] 1 -> [<usecase> S3]
[<usecase> S1] -> 0 [<usecase> S2]

[<usecase> S2] 1 -> [<usecase> S3]
[<usecase> S3] -> 0 [<usecase> S3]

```


