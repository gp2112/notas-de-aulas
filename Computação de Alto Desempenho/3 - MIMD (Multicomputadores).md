# MIMD Multicomputadores

## Máquinas MIMD com meórias distribuídas

- DIferentes Computadores (nós)
- Interconectados por uma rede de conexão
- Nós são unidades independentes e **assíncronas**
- Espaços de endereçamento são locais aos processos
- Exemplos de arquiteturas: *clusters*, *MPP (massive, parallel processos)* e *Grids*

### Clusters

- Nós formados usualmente por CPUs multicore
- Características da rede de interconexão afetam diretamente o desempenho
- Projeto do algoritmo paralelo deve ter como foco um *trade-off*
	- Maximizar o grau de concorrência
	- Minimizar sobrecarga de comunicação
**Benefícios:**
- Escalabilidade Absoluta: há possibilidade de máquinas com vários nós
- Escalabilidade Incremental: novos nós podem ser adicionados
- Usam sistemas operacionais e outras ferramentas de software disponíveis para máquinas SISD

#### Questões de proejto dos SOs de Clusters
- gerenciamento de falhas
	- Clusters para alta disponibilidade
		- Oferecem alta probabilidade que os recursos estejam disponíveis
		- Caso haja falha, novas requisições são tratadas por outro nó
	- Clusters com tolerância a falhas
		- Garante funcionamento mesmo na presença de falhas
- Redundância garante retorno de requisições não retornadas
	- *Failover*: recuperação de falhas para outro dispositivo
	- *Failback*: retorno ao dispositivo original quando este voltar a funcionar
- Escalonamento: essencial à escalabilidade
- Usos de computação paralela sobre máquinas MIMD com memória distribuída

#### Sistemas Básicos para Clusters
- Oferecem suporte ao desenvolvimento e execução de aplicações concorrentes com passagem de mensagens
- SOs gerenciam cada nó
	- *Linux* é um exemplo
- Compiladores tradicionais são usuais: C, Fortran, Java
- **Middlewares oferecem recursos extras** de software/hardware para:
	- Ponto de entrada único de processos
		- Grenciamento de sbmissões, espaço único de processos e migração de processos
	- Interface de Usuário padronizada, controle único e pontos de verificação
	- Espaço único para E/S, hierarquia de sistemas de arquivos e rede virtual única

### Massively Parallel Processors (MPP)

- **São supercomputadores MIMD com memória distribuída** como clusters
	- Mas orçados na feixa de milhões de dólares
	- Usados para problemas que requerem maior desempenho
- Normalmente usam tecnologias escalares/vetoriais já conhecidas e redes proprietárias de alto desempenho (mais eficiência)
![](Pasted%20image%2020220912091516.png)


## Grades (Grids)

- Representam sistemas e tecnologia usadas para conectar computadores isolados geograficamente
	- Geralmente é um cluster heterogêneo, fracamente acoplado e internacional
- Fornece uma infraestrutura técnica para que organizações compartilhem um objetivo comum, formando organização virtual
	- Felxível, com muitos membros que mudam
- Grinds têm características multilaterais que consideram seus pares
	- Diferente de modelos já consolidados como cliente-servidor ou peer-to-peer
	- Envolve novos serviços, ferramentas e protocolos para habilitar o funcionamento dessas organizações