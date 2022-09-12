# Memória Compartilhada e Distribuída em Máquinas MIMD

## Semântica de Memórias Compartilhadas

- Diferentes Módulos de memória são usuais com um mesmo endereçamento
- Redes de conexão mais complexas permitem concorrência de R/W
- Entrega de requisições podem ocorrer em ordens diferentes da esperada
- Cópias de blocos de memória podem estar em diferentes caches
- Ditam **regras entre hardwar e software** para ordem de R/W nos módulos
- Determinam **quando writers "alcançam" R/W** de outras variáveis

**Alguns modelos de consistência de memória:**  
- Estrita  
	- escritas são visíveis instantaneamente a todos os processos  
- Sequencial  
	- processos veem a mesma ordem de requisições de acesso à memória  
- (de) Processador  
	- escritas de um processo são observadas por ele na mesma ordem 
- Fraca  
	- sincronizações explícitas são consistentes sequencialmente  
- (de) Liberação  
	- sincronizações explícitas são consistentes ao processador em relação aos demais

### Consistência Estrita
- Garante que a leitura sempre obtém última escrita instantaneamente
	- Assume *clock* global e que não há atraso em mensagens no *hardware*.
		- **Impossível!**
	- Futuros R/W só ocorrerão depois de um *write* prévio finalizar.
- Possível quando:
	- Só um módulo de memória
	- Critérios FIO
	- Sem caches
	- Sem duplicações
- Gera um grande gargalo para o desempeho em sistemas reais
	- Impede otimizações no *hardware* e no compilador.

### Consistência Sequencial
- *Hardware* intercala requisições re R/W em uma ordem não determinística
- Todas as CPUs veem a mesma ordem para manter consistência
	- Ainda há visão de um *clock* global, mas a ordem pode variar
	- Assume que memória é atômica
![](Pasted%20image%2020220901152706.png)

### Consistência de Processador
- Menos rigoroza e mais fácil de implementar em mais CPUs
- Não garante que todas as CPUs veem a mesma ordem
	- Diferentemente da sequencial
- Propriedades:
	- Escritas de uma CPU são vistas nas outras na ordem da emissão

### Consistência Fraca
- Não garante nem a ordem de escrita de uma CPU
	- Uma CPU vê 1A antes de 1B e outra CPU pode ver 1B antes de 1A
- Variáveis de sincronização + operação de sincronização explícita (barreiras)
	- Permitem que escritas pendentes finalizem e nenhuma inicie até todas as escritas antigas terminem, incluindo operação de sincronização
- Sincronização descarrega pipeline
	- Coloca memória em um estado estável, sem operações pendentes
	- Operações de sincronização são consistentes entre si
		- CPUs enxergam sincronizações na mesma ordem
	- Insere uma sincronização explícita entre acessos
	- No exemplo abaixo, a ordem das escritas 1A e 1B não é garantida; mas 1C ocorre depois

- Software impõe uma ordem na sequência de eventos
	- Há um atraso no processamento pelo esvaziamento do *pipeline*
		- **São lentas** por precisar esperar todas as transações atuais terminarem
		- Sincronizações não são frequentes por questões de desempenho

![](Pasted%20image%2020220901153710.png)

### Consistência de Liberação
- Tenta melhorar ineficiência da Consistência Fraca
	- Operações de sincronização são divididas em *acquire* e *release*
	- Semelhantes a um *lock/unlock*. Garante [Consistência de Processador](###Consistência de Processador).
- Foco da proposta:
	- Quando um processo deixa a **região crítica**, não é necessário forçar que todas as escritas finalizem, basta garantir que elas terminem antes de outros processos entrarem naquela RC
- *Aquire*
	- Usado pela CPU quando há um *read* ou *write* na var compartilhada
	- Obtém acesso exclusivo aos dados compartilhados para poder escrever
	- Só obtém acesso garantindo exclusão mútua
- *Release*
	- Marca a saída da **região crítica**
		- Não força o fim das escritas, mas só finaliza de fato quando elas terminarem
	- Novas (outras) operações na memória podem iniciar imediatamente
		- Novo *acquire* só prossegue se *release* prévio terminou

## Coerência de Cache com Memória Compartilhada

- *Caches* são muito usadas
	- reduzem demanda sobre rede de interconexão e às memórias mais lentas
- Replicam dados da memória em diferentes níveis de *cache*
- Diferentes CPUs/Núcleos replicam os níveis de *cache*
- Dados replicados nas caches podem ficar desatualizados em *writes*
- **Determina:**
	- regras para a propagação da atualização dos dados
	- requisitos esperados de R/W para uma posição de memória
- Determinam a propagação de *writes*; mas não quando os *Writes* ocorrerão
	- O "quando" é determinado pelos modelos de consistência de memória.

- Soluções por *software* e *hardware*
	- *software*: deixam *hardware* mais simples e sõa mais conservadoras (lentas), ex: evitando uso de cache
	- *Hardware*: protocolos *update*, *invalidate* ou *adaptive*

### Protocolo MESI

**M -** Modified
**E -**  Exclusive
**S -**  Shared
**I  -**    Invalid

considerando um barramento simples:
![](Pasted%20image%2020220901160104.png)
Máquina de Estados FInitos
![](Pasted%20image%2020220901160337.png)

#### Soluções por Hardware

##### Protocolo Snoopy (monitoração):
- Voltados às redes de conexão em barramento, máquinas simétricas
- Controladores monitoram o barramento
	- Permitem na gestão dos estados dos protocolos de coerência

![](Pasted%20image%2020220901160555.png)

##### Protocolo de Diretório (máquinas assimétricas):
- Voltados

#### Falso Compartilhamento
- Ocorre quando dados diferentes de um bloco compartilhado são atualizados pelos processadores em suas *caches*