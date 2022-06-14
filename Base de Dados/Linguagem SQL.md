# Linguagem SQL - DDL

## Data Definition Language (DDL)
- Conjunto de comandos para definição do esquema da base de dados
- Compilador/Interpretador DDL

### Dicionário de Dados:
- Banco de dados do sistema
- Armazena descrição do esquema
- Armazena metadados
- Armazena restrições de segurança e integridade

## Data Manipulation Language (DML)
Conjunto de comandos para manipulação dos dados
- recuperação (consulta)
- inserção
- remoção
- modificação

Exemplos em SQL:
- *select*
- *insert*
- *delete*
- *update*

### Dois tipos de DML
**Procedural ->** Exige especificação de quais dados são necessários, e como obtê-los.
- Requer sequência específica de operações a serem executadas
- ex: álgebra relacional

**Não Procedural (declarativa) ->** Exige apenas especificação de quais dados são necessários e não como obtê-los.
- ex: SQL

## Componentes de um SGBD
![Pasted image 20220525102521](imgs/Pasted%20image%2020220525102521.png)

Os componentes funcionais do SGBD:
- componentes de processamento de consultas
- componentes de gerenciamento de armazenamento

## SQL
- Linguagem Declarativa -> Não procedural
- *Structured English Query Language*

## Operadores
- =, <, >, <=, >=, <>
- AND, OR, NOT
- [atributo ou expressao] BETWEEN valor1 AND valor2
- [atributo ou expressao] IS NULL
- LIKE -> Compara partes de um string
	- *atributo LIKE '%string%'* - %-> compara qualquer substring
	- atributo LIKE '_string_ _' - _ -> compara qualquer caractere
	- *case sensitive*!
- [atributo ou expressao] IN/NOT IN

## Tipos de Dados
- INTEGER | SMALLINT | DOUBLE | FLOAT | REAL
- DECIMAL [(precision, scale)]
- CHAR(n) - tamanho fixo - n caracteres
- VARCHAR(n) - tamanho variável
	- máximo de *n* caracteres
- BLOB - *Binary Large Object*
- DATE | TIME | TIMESTAMP

## DDL
### Comandos:

**CREATE TABLE**

Criar uma tabela, definir colunas e restrições

```sql
CREATE TABLE tabela {
	atrib1 tipo [<restricoes da coluna1>],
	atrib2 tipo [<restricoes da coluna2>],
	....
	atribn tipo [<restricoes da coluna n>]

	[<restricoes da tabela>]
};
```

- Restrições de Colunas
	- NOT NULL
	- DEFAULT valor
	- CHECK(condicao)
	
```sql
CREATE TABLE tabela {
	atrib1 tipo [(tamanho) [NOT NULL | DEFAULT valor]],
	atrib2 tipo [CHECK(condicao)],
	....
};
```

- Restições da Tabela
	- CHECK (condicao)
	- PRIMARY KEY [atributos chave primaria]
	- UNIQUE [atributos chave secundaria (terciaria...)]
	- FOREIGN KEY [atributos chave estrangeira]
			REFERENCES tabelaref {chave_primaria} {ações}
				açoes => {ON DELETE|ON UPDATE} {CASCADE | SET NULL | SET DEFAULT}

```sql
CREATE TABLE tabela {
	atrib1 tipo [(tamanho) [NOT NULL | DEFAULT valor]],
	atrib2 tipo [CHECK(condicao)],
	....
	
	[CONSTRAINT nome da restricao]
		PRIMARY KEY atributos_chave_candidata,
	[CONSTRAINT nome da restricao]
		UNIQUE atributos_chave_candidata,
	[CONSTRAINT nome da restricao]
		[ON DELETE CASCADE | SET NULL | SET DEFAULT]
		[ON UPDATE CASCADE | SET NULL | SET DEFAULT],
	[CONSTRAINT nome da restricao]
		CHECK(condicao)
};
```

**OBS:** Oracle não implementa o *Set Default*. Optaram por isso pois alterar a chave seria uma operação muito "perigosa".

**Exemplo:** Criar tabelas para o seguinte esquema:

![Pasted image 20220525114047](imgs/Pasted%20image%2020220525114047.png)

```postgresql
CREATE TABLE aluno (

	NUSP NUMBER NOT NULL,
	CPF CHAR(14),
	RG CHAR(8),
	UF(2),
	NOME VARCHAR(30),
	NASC DATE

	PRIMARY KEY (NUSP),
	UNIQUE(CPF),
	UNIQUE(RG, UF)
);

CREATE TABLE professor (
	NFUNC NUMBER NOT NULL,
	NOME VARCHAR(30),
	TITULACAO VARCHAR(10)

	PRIMARY KEY (NUSP),
	CHECK(UPPER(TITULACAO)) IN ("MESTRE", "DOUTOR", "TITULAR")
);

CREATE TABLE disciplina (
	SIGLA VARCHAR(10) NOT NULL,
	NOME VARCHAR(30),
	NCRED NUMBER,
	PROF NUMBER

	PRIMARY KEY (SIGLA),
	FOREIGN KEY (PROF) REFERENCES professor (NFUNC)
		ON DELETE SET NULL,
	CHECK (NCRED) > 0
);

CREATE TABLE turma (
	SIGLA VARCHAR(10) NOT NULL,
	NUMERO NUMBER NOT NULL,
	NALUNOS NUMBER

	PRIMARY KEY (SIGLA, NUMERO),
	CHECK (NALUNOS) > 0,
	FOREIGN KEY (SIGLA) REFERENCES disciplina (SIGLA)
		ON DELETE CASCADE
);

```

**ALTER TABLE -** Incluir/alterar/remover definições de colunas e restrições
```sql
ALTER TABLE tabela <ação>;
```
**Ação:**
- ADD *novoAtrib* tipo *restrições_de_coluna*
- ADD [CONSTRAINT *nome*] restrição_de_tabela
- DROP *atributo* [CASCADE | RESTRICT]
- DROP CONSTRAINT *nome*
- ALTER atributo DROP DEFAULT
- ALTER atributo SET DEFAULT *valor*

**DROP** *atributo* [CASCADE | RESTRICT]
- CASCADE - todas as visões e restrições (*constraints*) que referenciam o atributo são removidas automaticamente
- RESTRICT - atributo só é removido se não houver nenhuma visão ou restrição que o referencie.

**DROP TABLE -** exclui uma tabela de dados
```sql
DROP TABLE tabela CASCADE|RESTRICT;
```

## Comandos DML

**INSERT -** Insere uma ou mais tuplas em uma tabela.

```sql 
INSERT INTO tabela [(atrib1, atrib2, ...)] VALUES (valor1, valor2, ...);
```

**UPDATE -** modifica o valor de um atributo em uma ou mais tuplas da tabela.

```sql
UPDATE tabela SET
	atributo1 = <valor/expressão>,
	atributo2 = <valor/expressão>,
	...
WHERE <condicao/localizacao>;
```

**DELETE -** remove uma ou mais tuplas da tabela

```sql
DELETE FROM tabela WHERE <condicao/localizacao>;
```

### SELECT 
```sql
SELECT [DISCTINCT|ALL] <lista de atributos> FROM <lista de tabelas>
[WHERE <condicoes>]
[GROUP BY atributo]
	[HAVING <condicoes>]
[ORDER BY atributo [ASC|DESC]]
```

### Junção Interna (*inner join*)
- Combina tuplas relacionadas de diferentes relações em uma única tupla.
- Permite processamento de relacionamentos entre relações
- Muito usada com relações vinculadas por chave estrangeira
![](Pasted%20image%2020220606081955.png)

### Junção Externa (*outer join*)

#### Left Outer Join
- Tuplas atendem à condição de junção
- + Tuplas da tabela à esquerda que não têm correspondentes na tabela à direita
![](Pasted%20image%2020220606082218.png)

#### Right Outer Join
- tuplas que atendem à condição de junção
- + tuplas à tabela à direita que não têm correspondentes na tabela à esquerda

![](Pasted%20image%2020220606082232.png)

#### Full Outer Join
- Tuplas que atemdem à condição de junção
- Tuplas da tabela à esquerda que não têm correspondentes na tabela à direita
- Tuplas da tabela à direita que não têm correspondentes na esquerda
![](Pasted%20image%2020220606082332.png)
---
**Exemplo:**
Suponhamos as tabelas:

**ALUNO**
```
 Column |         Type          | Collation | Nullable | Default 
--------+-----------------------+-----------+----------+---------
 nome   | character varying(50) |           |          | 
 turma  | character(2)          |           |          | 
 id     | integer               |           | not null | 
Indexes:
    "aluno_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "const_turma" FOREIGN KEY (turma) REFERENCES turma(cod)
```
**TURMA**
```
                  Table "public.turma"
 Column  |     Type     | Collation | Nullable | Default 
---------+--------------+-----------+----------+---------
 cod     | character(2) |           | not null | 
 prof_id | integer      |           |          | 
 turno   | character(5) |           |          | 
Indexes:
    "turma_pkey" PRIMARY KEY, btree (cod)
Check constraints:
    "turma_turno_check" CHECK (upper(turno::text) = ANY (ARRAY['MANHA'::text, 'TARDE'::text, 'NOITE'::text]))
Referenced by:
    TABLE "aluno" CONSTRAINT "const_turma" FOREIGN KEY (turma) REFERENCES turma(cod)
```
**PROFESSOR**
```
                   Table "public.professor"  
Column |         Type          | Collation | Nullable | Default    
--------+-----------------------+-----------+----------+---------  
id     | integer               |           | not null |    
nome   | character varying(50) |           |          |
```

**INNER JOIN**
```sql
SELECT * FROM aluno INNER JOIN turma ON turma=turma.cod;
```
```  
nome    | turma | id | cod | prof_id | turno 
-----------+-------+----+-----+---------+-------
 luis      | 43    |  1 | 43  |     662 | NOITE
 guilherme | 42    |  0 | 42  |     732 | MANHA
```
```sql
SELECT * FROM turma INNER JOIN professor ON prof_id=professor.id;
```
```
cod | prof_id | turno | id  |  nome     
-----+---------+-------+-----+--------  
42  |     732 | MANHA | 732 | elaine  
43  |     662 | NOITE | 662 | elisa
```

**LEFT OUTER JOIN**
```sql
SELECT * FROM turma LEFT OUTER JOIN professor ON prof_id=professor.id;
```
```
cod | prof_id | turno | id  |  nome  
-----+---------+-------+-----+--------
 42  |     732 | MANHA | 732 | elaine
 43  |     662 | NOITE | 662 | elisa
 23  |     777 | TARDE |     | 
```

**RIGHT OUTER JOIN**
```sql
SELECT * FROM turma RIGHT OUTER JOIN professor ON prof_id=professor.id;
```
```
cod | prof_id | turno | id  |  nome     
-----+---------+-------+-----+--------  
42  |     732 | MANHA | 732 | elaine  
43  |     662 | NOITE | 662 | elisa  
    |         |       | 123 | farid
```

**FULL OUTER JOIN**
```sql
SELECT * FROM turma FULL OUTER JOIN professor ON prof_id=professor.id;
```
```
cod | prof_id | turno | id  |  nome  
-----+---------+-------+-----+--------
 42  |     732 | MANHA | 732 | elaine
 43  |     662 | NOITE | 662 | elisa
 23  |     777 | TARDE |     | 
     |         |       | 123 | farid
```

---

