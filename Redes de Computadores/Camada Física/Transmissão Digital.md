# Transmissão Digital

---
## Dados Digitais
![Pasted image 20220428142925](imgs/Pasted%20image%2020220428142925.png)

#### **Fatores Relevantes na transmissão de sinais digitais:**
- Componente contínua
- Largura de banda
- Informação de Clock
- Deteção de Erros

---
### Codificação em Linha
Consiste em apresentar o sinal digital de forma mais adequada à transmissão.

- Canais com ou sem fio transportam sinais analógico
- Como utilizar esses meios para enviar sinais digitais?
- **Codificar!** --> Converção de dados em sinais digitais que os representam.

#### Esquemas de Transmissão em Banda Base
**Non Return to Zero (NRZ)**
	- Depende apenas do estado do *bit*
	- Tensão positiva representa "1", negativa "0" (ou vice-versa)
	- Presença de luz -> 1, ausência -> 0 (ou vice versa)
	
**Non Return to Zero Inverted (NRZI)**
	- Depende do estado anterior
	- Quando ocorrer um *bit* "1", o sinal é invertido e quando ocorrer um *bit* "0", nada acontece (ou vice versa) 
	
Ambos possuem problema de sincronização:
--> No **NRZ** apenas longas sequências de 0 e 1
--> No **NRZI** apenas sequências de 0

**Vantagem** --> Conceito simples e fácil de implementar

**Desvantagem** --> Possui uma componente DC ( gera distorções do sinal ao passar por transformadores) e para longas sequências de um tipo de bit, o código não possui capacidade de sincronização

---
#### Codificação Multinível Binária
Mais do que dois níveis para a codificação dos dados.
**Tipos:**
	• Bipolar Alternate Mark Inversion (Bipolar-AMI); e  
	• Pseudoternário.

- **Bipolar Alternate Mark Inversion (Bipolar-AMI):**
	- O binário 0 é representado pela ausência de sinal
	- O bit 1 é representado por pulso negativo/positivo
	- Os pulsos para o bit 1 têm polaridade alternada

- **Pseudoternário:**
	- Bit 0 representado pela ausência de sinal
	- Bit 1 representado pela alternância entre polaridade
	- Nenhuma vantagem ou desvantagem sobre o **AMI**

**Vantagens:**
	- Sem perda de sincronismo se a sequência de bits 1 ocorrer (o 0 ainda é um problema)
	- Sem componente DC --> pode-se usar transformador para isolar a linha
	- Fácil de detectar erros, já que não se pode violar a alternância dos sinais

**Desvantagens**
	- Receptor deve distinguir entre 3 níveis (+A, -A, 0)
	- Requer aproximadamente 3dB mais de potência de sinal para a mesma probabilidade de erro de bit.

---
#### Codificação Bifásica

- **Codificação Manchester**
	- Transição no meio de cada período de bit
	- Transição serve como clock e dado
	- Pode-se adotar:
		- Transição alto para baixo representa 0
		- Transição baixo para alto representa 1
	- Usada pelo IEEE 302.3 (Internet)

![Pasted image 20220428150537](imgs/Pasted%20image%2020220428150537.png)

**Problema** -> exige largura de banda duas vezes maior que o NRZ

- **Codificação Manchester Diferencial**
	- Transição do Clock ocorre no meio periodo de *bit*
	- Inversão da transição no meio período de *bit* representa 0;
	- Nenhuma transição representa 1
	- Usado pelo IEEE 802.5 (*Token Ring*)

**Em Resumo** -> Se não houver inversão de transição do *bit* é 1, caso contrário, é 0.

**Manchester Diferencial  X  Manchester:

- **Vantagem** -> por ser diferencial, é mais resistente a ruídos e distorções.
- **Desvantagem** -> para descobrirmos no Manchester  Diferencial qual  é o sinal transmitido, precisamos saber qual era o estado anterior do sinal.

**Manchester e Manchester Diferencial

- **Vantagens**
	- Sincronismo no meio da transição do *bit*
	- Nenhum componente DC
	- Detecção de erro -> ausência de uma transição
	
- **Desvantagens
	- Taxa de modulação máxima é duas vezes a do **NRZ**.
	- Requer maior largura de banda.

![Pasted image 20220428151240](imgs/Pasted%20image%2020220428151240.png)

#### Exercícios:

![Pasted image 20220428151311](imgs/Pasted%20image%2020220428151311.png)

![Pasted image 20220428151341](imgs/Pasted%20image%2020220428151341.png)

#### Multiline Transmission Three Level (MLT-3)

- Parece com **NRZI** mas utiliza 3 níveis
- Quando o bit 0 aparece, nada acontece
- Quando o bit 1 aparece:
	- Se o bit 1 não-zero anterior é positivo, subtraia V;
	- Se o bit 1 não-zero anterior é negativo, adicione V;

**Vantagens** -> Requer banda menor que a codificação bifásica e resukta em emnos interferência

**Desvantagens** -> Receptor deve distinguir entre 3 níveis

---
### Codificação por Bloco
Foi concebida para melhorar o desempenho da codificação em  
linha incluindo redundância e possibilidade de verificação de erros.

Basta substituir blocos de n bits por blocos de x bits.  
• Para isso:  
	• A sequência de bits é dividida em blocos de n bits;  
	• Os blocos de n bits são substituídos;  
	• É feita uma codificação de linha.

#### Codificação 4B/5B
- Minimiza o problema de sincronização do NRZI
- **Reduz sequências de 0** --> cada 4 *bits* são mapeados para uma sequência de 5 bits
- Utiliza NRZI como codificação de linha
- É utilizado no padrão ethernet 100Mbps
- Com a substituição de blocos de bits, ficarão blocos não alocados que podem ser alocados para controle de transmissão


![Pasted image 20220428153017](imgs/Pasted%20image%2020220428153017.png)
![Pasted image 20220428153032](imgs/Pasted%20image%2020220428153032.png)
- Na prática as duas estratégias são utilizadas conjuntamente

![Pasted image 20220428153059](imgs/Pasted%20image%2020220428153059.png)

#### Exercício
![Pasted image 20220428153128](imgs/Pasted%20image%2020220428153128.png)

---
## Dados Analógicos
![Pasted image 20220428154614](imgs/Pasted%20image%2020220428154614.png)

### PCM - Pulse-Code Modulation

É um método usado para converter sinais analógicos em digitais por meio de três etapas -> amostragem, quantização e codificação.

#### DIagrama de Blocos do PCM
![Pasted image 20220428154037](imgs/Pasted%20image%2020220428154037.png)
#### Teorema da Amostragem (Teorema de Nyquist)
Toda informação de um sinal analógico pode ser recuperada se uma amostragem for reaizada a uma taxa de duas vezes a maior frequência do sinal. O sinal analógico pode ser reconstruído a partir dessas amosras utilizando-se um filtro passa-baixa.

#### PAM - Pulse-Amplitude Modulation
Permite a modulação do sinal através da **discretização das amplitudes do sinal modulante**. Essa modulação é feita multiplicando-se o sinal modulante por um trem de pulsos da portadora, que consiste em uma onda quadrada.

#### Transmissão Paralela
* Requer mais de um canal de comunicação

#### Transmissão Serial
* Transmissão mais simples
* Utiliza apenas um canal de comunicação
* **Transmissão Serial Síncrona
	* Requer um relógio de sincronismo confiável
	* A cincronização é efetivada na camada de enlace
* **Transmissão Serial Assíncrona**
	* Inserção de bits extras deixa mais lenta
	* Mais barata -> recomendada para baixas velocidades

### Multiplexação
* Transmissão simultânea de dois ou mais elementos (sinais) de informação utilizando o mesmo meio de transmissão
* **Objetivo** -> maximizar o número de conexões

### Métodos de Multiplexação:
* Divisão de Frquência (FDM)
	* Por divisão de comprimento de onda (WDM)
* Divisão de Tempo (TDM)
* DIvisão de Código

#### Divisão de Frequência
* Designa-se uma faixa de frequência para cada sinal
* O sinal deve ser deslocado em frequência para a sua posição antes de ser realizada a multiplexação dos canais com a modulação
* O novo sinal modulado não pode ter intersecção na frequência com outros canais

#### Divisão de Comprimento
* Forma do FDM aplicado a **fibras ópticas**
* Utiliza-se diferentes comprimentos de ondas

#### Divisão de Tempo
* Usuários se alternam em rodízios -> cada um usa  toda a largura de banda por determinado período de tempo

#### Divisão de Código
* N ̃ao ́e baseado em propriedades f ́ısicas, e sim em  
propriedades matem ́aticas:  
• Valores de um espa ̧co de vetores ortogonais podem ser  
combinados e separados sem interferˆencia.  
• Cada emissor recebe um c ́odigo bin ́ario que representa  
vetores ortogonais e utiliza esse c ́odigo para construir seu  
sinal digital.  
• Os sinais de diferentes emissores s ̃ao combinados  
(somados).  
• Os receptores que tamb ́em conhecem os respectivos  
c ́odigos bin ́arios podem recuperar o sinal digital a partir do  
sinal combinado.

[Camada de Enlace de Dados](Camada%20de%20Enlace%20de%20Dados.md)