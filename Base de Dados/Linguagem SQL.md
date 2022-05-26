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
![[Pasted image 20220525102521.png]]

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

![[Pasted image 20220525114047.png]]

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