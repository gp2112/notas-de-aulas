# Introdução à Computação de Alto Desempenho

## Soluções Sequenciais vs Soluções Paralelas
- **Detalhes de *hardware* e *software* são mais visíveis ao programador.**
	- São necessárias diferentes soluções para diferentes:
		- *Hardwares*
		- SOs
		- Modelos de Programação
- **Aspector adicionais a serem considerados**
	- Códigos multidimensionais
	- Identificação do paralelismo na aplicação
	- Maior impacto da arquitetura e software básico
	- Uso de novas ferramentas de software para o desenvolvimento
	- Novas estruturas de programação:
		- Iniciar e finalizar processos;
		- Comunicar dados;
		- Sincronizar Computações;
	- Distribuição de Carga de Trabalho entre processos e processadores

## Conceitos Básicos

- **Computação Paralela**
	- Uso do computador paralelo para aumentar a eficiência ou permitir a eficácia, usando um programa desenvolvido para programação paralela;
- **Computador Paralelo**
	- Computador com multiplos processadores, memórias e outros dispositivos replicados.
- **Programação Concorrente ou paralela ou distribuída**
	- Atividade de programar em uma linguagem de programação para determinar quando e como tarefas podem ser executadas por diferentes processos ao mesmo "tempo", no mesmo processador ou em processadores diferentes.
- ***Threads:***
	- Processos que executam sequencialmente com seu próprio registrador PC, pilha, registradores de dados e mantêm seu estado atual de execução.
	- É uma trilha em execução de um processo
	- Compartilham CPU em um modelo *timeshared*.
	- Compartilham segmento de texto, memória global, descritores de arquivos, processos filhos, sinais de interrupção e outras informações.
- **Processos Concorrentes:**
	- Dois ou mais processos que iniciaram e ainda não finalizaram a sua execução.*
	- São processos que concorrem pelos recursos de um sistema computacional
	- Podem estar executando em um processador ou em diferentes processadores. (*pseudoparalelismo*)
- **Processos Paralelos:**
	- "Paralelismo Real"
	- Sempre executam em processadores distintos.
- **Processos DIstribuídos:**
	- Do ponto de vista teórico, são sinônimos de processos paralelos
	- Tem objetivos e modelos de programação distindos
		- Normalmente visam o compartilhamento de recursos
		- Encapsulam mais os detalhes de níveis inferiores de hardware e software
- **Interação: Comunicação & sincronização**
	- Comunicação: troca de dados
	- Sincronização: garante a ordem de execução dos processos
- **Granulação (granularidade):**
	- Relação entre a computação e a interação
	- Quanto maior a computação frente à interação, maior a granulação.
	- Granulações mais finais (menores) têm o potencial para ofereces melhores desempenhos em sistemas com recursos mais eficientes
		- granulações finas oferecem maior grau de paralelismo
- **Pipeline:**
	- Sobreposição de múltiplas instâncias de um problema
	- Paralelismo temporal extraído de diferentes estágios de uma solução
	- ![Esquema do Pipeline](Pasted%20image%2020220825154321.png)
- **Tempos em Computação**
	- **Execução:** tempo executando instruções do processo na CPU
	- **Resposta:** tempo entre a submissão do processo e seu retorno/finalização.
	- **Ocioso:** tempo que o processo parou aguardando para executar
	- **Sequencial:** tempo de resposta(execução) da versão sequencial de um programa
	- **Paralelo:** tempo de resposta (ou execução) da versão paralela de um programa com vários processos em paralelo (tempo acaba de contar quando o último processo termina).

### Métricas para avaliar ganhos de desempenho
#### **Speedup (sp):** 
Determina o ganho de desempenho. 
- **Absoluto:** considera $T_{seq}$ o melhor algoritmo sequencial conhecido.$$SP = \frac{T_{seq}}{T_{par_p}}$$
- **Relativo:** considera $T_{seq}$ a execução da versão paralela de um processador. $$SP = \frac{T_{p_1}}{T_{par_p}}$$
$p$ -> quantidade de processadores usada

#### Eficiência
Determina a eficiência no uso de $p$ processadores. $$E = \frac{Sp_p}{p}$$

![gráfico da eficiência](Pasted%20image%2020220825155704.png)

- SP linear (Sp = p) -> ideal, é o que buscamos.
- SP sublinear (Sp < p) -> caso comum.
- SP superlinear (Sp > p) -> pode acontecer