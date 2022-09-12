# Máquinas SIMD - Single Instruction & Multiple Data

- Consideram processadores com
	- uma Unidade de Controle (UC) controlando múltiplas Unidades Funcionais
		- ULA e FPU principalmente
	- Uma mesma instrução executando nas Unidades Funcionais com dados diferentes
- Considera **execuções síncronas** sobre diferentes dados
- Alto grau de paralelismo de dados (*supercomputadores*)
	- Operações sobre **vetores e matrizes de dados** (*float* e *double*)
		- **Maior precisão** e **vazão** de operações em **ponto-flutuante**.
	- Voltadas para aplicações que têm essa demanda sobre dados em vetores
![](Pasted%20image%2020220912092901.png)

- Alternativa aos *mainframes*
	- Voltados a multiprogramação e operações intensas de E/S

- **Dificuldade para algumas execuções**
```c
if (b == 0)
	c = a;
else
	c = a/b;
```
- Uma única instrução opera sincronamente dados distindos
- if() acima e executado em **2 passos**

- um exemplo básico de arquitetura: processadores SIMD do ILLIAC IV

![](Pasted%20image%2020220912093231.png)

## Computação Vetorial

- Supercomputadores vs Processadores Matriciais
	- Ambos executam operações sobre matrizes ou
	- Vetores de números de ponto flutuante
	- padrão IEEE 754
	- Ex: $c_{i,j} = \sum_{k=1}^N a_{i,k} \times b_{j,j}$
	 ![](Pasted%20image%2020220912093452.png)

- Operarões de ponto-flutuante são mais complexas
	- Exemplo (base 10): $1\times 10^0 + 1\times 10^3 \rightarrow 1001\times 10^0$ ou $1.001\times 10^3$ ou ...
		- 4 passos básicos (simplificado)
			- 1 - Compara expoentes $\rightarrow$ $0 \neq 3$ ?
			- 2 - Desloca expoentes $\rightarrow 0.001\times 10^3 + 1\times 10^3$ 
			- 3 - Executa a operação $\rightarrow 1.001\times 10^3$
			- 4 - Arredonda/normaliza $\rightarrow 1.001\times 10^3$ (ja estava)

- Processadores vetoriais
	- Normalmente são ULAs com pipeline cujos estágios operam nrs de ponto-flutuante

- Processadores Matriciais
	- Normalmente são paralelas
![](Pasted%20image%2020220912094146.png)
- Processadores para processamento vetorial

![](Pasted%20image%2020220912094249.png)

## GPUs

- *Graphics Processing Unit*
