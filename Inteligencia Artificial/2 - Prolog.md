# Prolog

### Átomos
Objetos mais simples. Corresponde uma instância específica do mundo.

ex: joao, maria, vermelho

### Variáveis
Cadeias de letras, dígitos e caracteres, sempre começando com letra maiúscula ou \_.

### Estruturas
Objets de dados que possuem vários componentes.
- todos os objetos estruturados podem ser representados como árvores.
- ex: estrutura *data(7,julho,1953)*
- Tuplas rotuladas
- Componentes podem ter qualquer valor, incluindo subestruturas.
```prolog
pessoa(nome("Joao", "Grandao"), 
	masculino, data(20,jun,1996)).
```

### Listas
- Subconjunto das estruturas:
	- Átomo [] representa a lista vazia
	- *.(x, xs)* representa a lista cuja cabeça é *x* e cuja cauda é *xs*.
- Notações alternativas
	- `[x | xs]` = `.(x, xs)`
	- `[a, ..., z]` = `.(a, ... (z, []))`

### Variável Lógica
Representa objeto simples, porém não especificado
```prolog
?pai(X, maria).
X = joao.
```

### Substituição e Instância
?pai(X, maria).
$\Theta$= *{X=joao}*

- Uma substituição $\Theta$  aplicada a um termo A, denatada por A$\Theta$, é o termo obtido substituindo cada ocorrência de X por $t$ em A, para cada par X=t em $\Theta$ .

- A é uma instância de B se existe uma substituição $\Theta$ tal que A=B$\Theta$

### Conjunção de Interrogações

- ? pai(joao, maria), mulher(maria)
(sem interesse)

### Regras

- Regras são declarações da forma $$A \leftarrow B_1,B_2, ..., B_n$$
A seta para trás $\leftarrow$ é usada para denotar consequência lógica.

filho(X,Y)  $\leftarrow$ pai(\_, Y)