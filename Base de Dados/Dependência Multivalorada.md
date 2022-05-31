# Dependência Multivalorada

- Restrição entre dois conjuntos de atributos 

**A ->> B**
- **A multidetermina B** (ou B é multidependente de A) => o **conjunto de valores** de B é determinado pelo valor de A, e **somente** pelo valor de A.

- DMs são semânticas (assim como as DFs)
- **Simetria** na definição de DM
	- se **X ->> Y**, então **X ->> Z**, Z = R - (X U Y)

Dada uma DM **X ->> Y** em R

Se: 
	a) $Y \subseteq X$ ou
	b) $X \cup Y = R$
Então é **Dependência Multivalorada Trivial**

Senão ==> **Dependência Multivalorada Não-Trivial**

### Exemplos:
![Pasted image 20220516090317](imgs/Pasted%20image%2020220516090317.png)

### Exemplo
![Pasted image 20220516090354](imgs/Pasted%20image%2020220516090354.png)

![Pasted image 20220516090440](imgs/Pasted%20image%2020220516090440.png)

### Problema da DM Não-Trivial
- requer **redundância** nas tuplas
- Exemplo:
	- Empregado = {<u>Nome,Projeto,Dependente</u>}
	- Está na BCNF, mas ainda há redundância de dados
- Solução ==> [4a Forma Normal](4a%20Forma%20Normal.md)!

