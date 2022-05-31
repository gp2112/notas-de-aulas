# Normalização e Dependências Funcionais

## Qualidade do Projeto Lógico

#### - Como avaliar a qualidade do esquema relacional (projeto lógico)?

- Semântica - completude, consistência, ...
- Implementação - espaço, eficiência de consultas...

#### - Controle de Consistência
1) No esquema da base de dados
	- Estrutura
	- Restrições
2) No SGBD
	- *Constraints* SQL
	- Procedimentos e *Triggers* (gatilhos)
3) Na aplicação

#### - O que é mais eficaz?

--- 

### Análise Informal:
- **Diretriz 1** -> Semântica de atributos nas relações
- **Diretriz 2** -> Redução de valores nulos
	- espaçco, interpretação, consultas
- **Diretriz 3** -> Redução de redundância em tuplas
	- prevenção de anomalias de inserção
	- prevenção de anomalias de remoção
	- prevenção de anomalias de alteração
- **Diretriz 4** -> prevenção de geração de tuplas espúrias (ilegítimas) nas junções

### Análise Formal
- Baseada em **Dependências Funcionais** ==> restrições (dependências) entre atributos.
	- Garantir **consistência** da base de dados: <span style="color:red">Não violar as dependências Funcionais</span>

- Formas Normais e Normalização
	- Baseadas em Dependências Funcionais
	- Avaliação e Garantia da qualidade dos esquemas de relação

## Dependências Funcionais
 **Dependência Funcional (DF)** -> Restrição entre 2 conjuntos de atributos X e Y
					X --> Y
- X determina funcionalmente U, ou Y depende funcionalmente de X
	- se $t_1[x] = t_2[x]$, então $t_1[y] = t_2[y]$

**Exemplos**: 

- **NUSP** -> Nome, Idade, Curso
- **Sigla_Disc** -> Nome_Disc, Créditos
- **Sigla_Disc, NUSP, semestre, ano** -> nota

- Dependência Semântica
- identificada pelo projetista da base de dados
- deve ser validada na instância da base (nos dados)
- **nunca deve ser definida (inferida)**  a partir dos dados

## Garantindo Consistência no Modelo Relacional
- Garantia de consistência na construção da base de dados (i.e. no **ESQUEMA**)
- Qualidade das relações é baseada na análise de **dependências funcionais**
- Uma relação **está em** um determinada **Forma Formal** quando satisfaz um conjunto de condições baseadas nas **dependências funcionais**
- Colocando uma relação em uma forma normal...

![Pasted image 20220511104928](imgs/Pasted%20image%2020220511104928.png)
## Normalização

- Formas Normais baseadas em dependências funcionais
	- baseadas em chave primária
		- 1a FN
		- 2a FN
		- 3a FN
	- Baseadas em chaves candidatas
		- definições genéricas de 2a FN e 3a FN
		- FN de Boyce-Codd (BCNF)
- Forma Normal baseada em dependências multivaloradas
	- 4a FN

### Regras de Inferência de DFs:
- **Reflexiva**: se $Y \subseteq X \longrightarrow X \rightarrow Y$ (**DF Trivial**)
- **Transitiva**: se $X \rightarrow Y, Y \rightarrow Z \longrightarrow X \rightarrow Z$
- **Decomposição**: se x --> YZ => X-->Y, X-->Z
- **Aditiva**: se X->Y, X->Z => X -> YZ
- **Aumentativa**: se X-->Y => XZ --> YZ
- ...

## Definições Iniciais
Dado os conjuntos de atributos **X** e **Y**, e um atributo (qualquer) $a \in X$:

- X --> Y é **dependência funcional total** se (X - {a}) não determina Y.
	- i.e. Y depende, semanticamente, de todo o X
	- ex: Sigla_Disc, NUSP, semestre, ano -> Nota

- X --> Y é **Dependencia Funcional Parcial** se (X-{A}) -> Y
	- i.e. Y depende, semanticamente, só de uma parte de X
	- ex: Sigla_Disc, NUSP, semestre, ano -> Nome_Disc

## 1a Forma Normal
Todos os atributos da relação **Atômicos** e **Monovalorados**
- Parte da definição forma de Modelo Relacional
- Exigida pela maioria dos SGBDRs

#### Colocando uma relação na 1a FN:
![Pasted image 20220511110240](imgs/Pasted%20image%2020220511110240.png)
![Pasted image 20220511110250](imgs/Pasted%20image%2020220511110250.png)
### 2a Forma Normal
- Relação na 1a Forma Normal
- Todos os atributos <u>não primários</u> possuem **dependência total**, <u>transitiva ou não</u>, da **chave primária**

![Pasted image 20220511110431](imgs/Pasted%20image%2020220511110431.png)
### 3a Forma Normal
- Relação entr 1a e 2a Formas Normais
- Todos os atributos <u>não primários</u> possuem <u>dependência total</u>, **não transitiva**, da <u>chave primária</u>.
	- se existir as DFs **X -> Z** e **Z -> Y** e se **Z** não é a chave candidata, então **x -> y** é transitiva.

**Colocando uma relação na 3a FN**:

![Pasted image 20220511111457](imgs/Pasted%20image%2020220511111457.png)
### Forma Normal de Boyce - Codd (BCNF)
- **BCNF** => Extensão da 3a FN genérica
- uma relação R **está** na **bcnf** se:
	- estiver na 3a FN genérica
	- **para toda** DF não-trivial **X->A** válida para a relação R, **X** é uma **chave** em R

#### Na prática:
- Maioria das relação em 3FN genérica também está na BCNF
- Exceção:
	- quando **X->A** e X não é chave / A é atributo primário

![Pasted image 20220516083639](imgs/Pasted%20image%2020220516083639.png)
A relação está **Treinamento** está na BCNF?

Colocando em BCNF:

![Pasted image 20220516083927](imgs/Pasted%20image%2020220516083927.png)
[Dependência Multivalorada](Depend%C3%AAncia%20Multivalorada.md)