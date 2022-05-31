# Mapeamento entre Esquemas
---

## Alterando os 7 passos
1. Mapear todos os CEs Fortes que **não fazem parte de ocorrências de generalização**
2. Mapear todos os CEs Fracas **que não fazem parte de ocorrências de generalização** <- <span style="color: red">Passo 2A</span>
3. Mapear todos os CR de cardinalidade 1:1 do DER
4. Mapear todos os CR de cardinalidade 1:N do DER
5. Mapear todos os CR de cardinalidade M:N do DER
6. Mapear todos os CR de grau > 2 do DER
7. Mapear todos os tributos MUltivalordos de CEs e CRs do DER

## Mapeamento da Generalização (Passo 2A)
* Analisar uma a uma todas as ocorrências da abstração de generalização e escolher a melhor opção de mapeamento
* Cada ocorrência da abstração é mapeada de maneira independente (mesmo dentro de uma mesma hierarquia).

### Três alternativas principais:
1. Mapear o CEG e os CEEs em **relações diferentes**
2. Mapear o CEG e todos os CEEs em uma **única relação**
3. Mapear cada CEE (e apenas eles) em sua própria relação, junto com seus respectivos atributos genéricos

* Cada alternativa pode ser mapeada de mais de uma maneira
	* **Procedimento padrão** de mapeamento

#### Os 9 Procedimentos Padrão
![Pasted image 20220502091044](imgs/Pasted%20image%2020220502091044.png)

#### Alternativa 1 
* **Mapear o CEG e os CEEs em Relações Diferentes**

* Interessante quando:
	* há poucos CE específicos (todos conhecidos)
	* Consultas tipicamente se concentram em um ou poucos CEEs de cada vez
	* CEEs participam de relacionamentos com outros CEs
* Aplicável a Especialização Total ou PArcial
	* <span style="color: red">Mas não garante Especialização total</span>

 **Procedimento Padrão 1**

![Pasted image 20220502085044](imgs/Pasted%20image%2020220502085044.png)
**Exemplo:** como mapear?

![Pasted image 20220502085152](imgs/Pasted%20image%2020220502085152.png)
* A ocorrência da generalização deve ser **mutualmente exclusiva** (disjunção). 

* **Procedimento padrão 2**
![Pasted image 20220502085305](imgs/Pasted%20image%2020220502085305.png)
**Exemplo:** Como mapear?

![Pasted image 20220502085338](imgs/Pasted%20image%2020220502085338.png)
* Semelhante ao procedimento 1: Usado quando a Generalização é definida com **sobreposição**

**Procedimento Padrão 3**
![Pasted image 20220502085700](imgs/Pasted%20image%2020220502085700.png)

#### Alternativa 2
* **Mapear o CEG e todos os CEEs em uma Única Relação**
* É interessante quando:
	* existem **poucos atributos específicos** nos CEEs
	* há possibilidade de "surgirem" especializações [sem atributos específicos] não previstas no projeto
	* Só o CEG participa de relacionamentos
* Aplicável a Especialização Total ou Parcial
	* <span style="color:red">não garante Especialização Total</span>


**Procedimento Padrão 4**
![Pasted image 20220502085915](imgs/Pasted%20image%2020220502085915.png)
**Exemplo:** Como mapear?

![Pasted image 20220502085938](imgs/Pasted%20image%2020220502085938.png)
* Generalização deve ser **mutuamente exclusiva**
	* em cada tupla apenas os atributos correspondentes ao subtipo da entidadepodem possuir valor
	* os atributos correspondentes aos demais subtipos devems er sempre mantidos nulos

**Procedimento padrão 5**
![Pasted image 20220502090106](imgs/Pasted%20image%2020220502090106.png)
![Pasted image 20220502090122](imgs/Pasted%20image%2020220502090122.png)
* Generalização definida com **sobreposição**
* Se uma entidade pertence a um CEE, então na tupla **pelo menos 1 atributo** correspondente ao CEE deve possuir **valor não nulo**

**Exemplo:** Como mapear?

![Pasted image 20220502090244](imgs/Pasted%20image%2020220502090244.png)
**Procedimento Padrão 6**
![Pasted image 20220502090307](imgs/Pasted%20image%2020220502090307.png)
![Pasted image 20220502090315](imgs/Pasted%20image%2020220502090315.png)
* Indica quais CEEs uma entidade pertence usando valores booleanos

#### Alternativa 3
* **Mapear cada CEE (apenas) em sua própria relação, junto com seus respectivos genéricos
* É interessante quando:
	* é frequente o acesso a cada entidade em sua totalidade, incluindo seus dados genéricos e específicos
	* Aplicável **apenas** a especialização total
* Só os CEEs participam de relacionamentos

**Procedimento Padrão 7**

![Pasted image 20220502090729](imgs/Pasted%20image%2020220502090729.png)
**Exemplo:** Como Mapear?

![Pasted image 20220502090752](imgs/Pasted%20image%2020220502090752.png)
![Pasted image 20220502090803](imgs/Pasted%20image%2020220502090803.png)

**Procedimento Padrão 8**

**Exemplo:**: Como Mapear?
![Pasted image 20220502090856](imgs/Pasted%20image%2020220502090856.png)

**Procedimento Padrão 9**

![Pasted image 20220502090914](imgs/Pasted%20image%2020220502090914.png)
**Exemplo:** Como mapear?

![Pasted image 20220502090944](imgs/Pasted%20image%2020220502090944.png)


#### Casos Especiais
* Atributos específicos que podem identificar univocamente o CEE podem ser colocados como chaves secundárias

![Pasted image 20220502091144](imgs/Pasted%20image%2020220502091144.png)

### Exercício
![Pasted image 20220502091205](imgs/Pasted%20image%2020220502091205.png)

---
## Bibliografia
[Mapeamento de Agregação](Mapeamento%20de%20Agrega%C3%A7%C3%A3o.md)

---
Material coletado e adaptado por Guilherme Paixão dos slides feitos pela professora Elaine Parros Machado de Sousa para a disciplina de Bases de Dados, ICMC-USP. 

Todos os direitos reservados.