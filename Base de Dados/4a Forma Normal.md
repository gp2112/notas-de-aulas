# 4a Forma Normal

A relação R está na 4a Forma Normal se:

- Todas das dependências multivaloradas são **triviais**, ou
- para cada dependência multivalorada não-trivial A->> B, **A é uma chave** (completa) em R

### Exemplos

![[Pasted image 20220516090833.png]]

## Intuição
![[Pasted image 20220516090901.png]]

#### Normalizando a relação para a 4a FN:
- Dada uma DMNT **A ->> B** na relação R, substitui-se **R** por:
	- $A \subseteq B$ e
	- R - B

![[Pasted image 20220516091028.png]]

- Evita redundância de tuplas ==> evita anomalias de inclusão/remoção/alteração
- cenários típicos de normalização para 4a FN (ocorrências de DMNT)
	- atributos **multivalorados independentes** misturados em uma única tabela
		- Ex: Empregado_PD = {<u>Nome, Projeto, Dependente</u>}
	- atributos **multivalorados** ou **CR N:N** armazenados **de maneira incorreta** em múltiplas linhas
		- Ex: Pessoa = {<u>CPF,telefone</u>, nome, data-nasc, ...}

## Observação
- Lembrando o mapeamento ME-R --> Modelo Relacional
	- Atributos multivalorados definem novas relações
		- Sem redundância e sem anomalias

![[Pasted image 20220516091348.png]]

## Considerações Finais
### Normalização
- Uma relação por vez - análise de 1a FN, 2a FN, 3a FN, BCNF e 4a FN
- **forma normal de uma relação** ==> forma normal mais restrita atendida
- **forma normal da base de dados** ==> forma normal mais restrita atendida por <u>todas as relações</u>

### Propriedades Desejáveis:
1) decomposição **sem perda de junção** (sem geração de tuplas ilegítimas)
2) decomposição com **preservação de dependências** (possibilidade de avaliar a DF ==> atributos na mesma tabela)

### Leitura
- **Elmasri, R; Navathe, S.B.** - *Sistemas de Banco de Dados*, Addison Wesley
	- 4a Edição - **Capítulos 10 e 11**
	- 6a Edição - **Capítulo 15**

