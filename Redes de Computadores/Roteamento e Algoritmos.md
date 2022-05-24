# Roteamento
Determinar "bons" caminhos (sequência de roteadores) através da rede da fonte até o destino.

- Algoritmos de roteamento são descritos por **grafos**.
- Os **nós** do grafo são **roteadores**.
- As **arestas** do grafo são **enlace**:
	- Custo do enlace: atraso, preço ou nível de congestionamento.
- "Bons" caminhos:
	- Caminhos de menor *custo*
	- Caminhos redundantes

![[Pasted image 20220524170349.png]]

## Classificação de Algoritmos de Roteamento

**Informação Global**
- Todos os roteadores tem informações completas da topologia e do custo dos enlaces
- Algoritmos de estado de enlace (*Link State*)

**Informação Descentralizada**
- Roteadores só conhecem informações sobre seus vizinhos e os enlaces para chegar até eles.
- Processo de computação interativo, troca de informações com os vizinhos.
- Algoritmos de vetor de distância (*distance vector*)

**Estático**:
- As rotas mudam lentamente ao longo do tempo do tempo.
- Muitas vezes dependem de mudanças feitas por um administrador de rede.

**Dinâmico**
- As rotas mudam mais rapidamente
	- Atualizações periódicas
	- Podem responder a mudanças no custo dos enlaces

### Roteamento pelo caminho mais curto
- **Estático** e **Global**: topologia de rede e custo dos enlaces são conhecidos por todos os nós antecipadamente para o cálculo das tabelas de roteamento.
- **Funcionamento**: calcula-se o caminho mais curto pelo Algoritmo de *Dijkstra*.
- Topologia de rede e custo dos enlaces são conhecidos por todos os nós.
	- Implementado via "*link state broadcast"*
	- Todos os Nós tem a mesma informação
- Computa caminhos de menor custo dde um nó (fonte) para todos os outros nós
	- Fornece uma tabela de roteamento para aquele nó
- Convergência: após $k$ iterações, conhece o caminho de menor custo para $k$ destinos.

### Inundação (*Flooding*)
- **Estático** e **Descentralizado**
- **Funcionamento**: Os pacotes que chegam são reencaminhados para todas as linhas, exceto pela que chegou.
- Para reduzir o número de pacotes, é possível acrescentar um contador de saltos no cabeçalho.

### Algoritmos Vetor de Distância
- Conhecido também como Algoritmo de Roteamento de *Bellman-Ford*.
- **Dinâmico** e **Descentralizado**
- **Funcionamento:**
	1. Cada nós mantém um vetor com a distância até seu vizinho, $d_i$
	2. Os nós enviam uns para os outros seus vetores de distância.
	3. Quando recebe um vetor, o nó compara com os custos que conhece
	4. Se o custo até o vizinho mais o custo do vetor recebido for menor que o valor no seu próprio vetor, esse custo é atualizado e a nova rota é atualizada na tabela de roteamento.

 - **Iterativo**:
	 - Continua até que os nós não troquem mais informações.
	 - *Self-terminating*: não há sinal de parada
- **Assíncrono:**
	- Os nós não precisam trocar informações simultaneamente.
- **Distribuído:**
	- Cada nó se comunica apenas com os seus vizinhos, diretamente conectados.
- **Estrutura de dados da Tabela de Distância:**
	- Cada nó tem sua própria tabela
	- Linha para cada possível destino
	- Coluna para cada roteador vizinho

#### Problema da contagem até infinito
![[Pasted image 20220524173619.png]]
- Aumento do custo ou falhas são propagadas muito lentamente
- Os valores para $y$ eram até de 4 até $x$ e de 1 até $z$ eram de 1 até y e de 5 até x/
- O nó $y$ detecta a mudança e atualiza o valor até x no seu vetor comparando 60 com o caminho passando por z

### Algoritmo Estado de Enlace
- *Link State*
- **Dinâmico**
- **Global**
	- Implementado via *link state broadcast*
	- Todos os nós tem a mesma informação
- **Funcioamento**
	1. Descobre seus vizinhos e seus endereço de rede e calcula o custo até cada um deles.
	2. Cria um pacote que informa tudo o que foi descoberto e calculado e envia para todos os outros roteadores
	3. Calcula o caminho mais curto até cada um dos roteadores (*Dijkstra*)

- **Convergência ->** apoós $k$ iterações, conhece o caminho de menor custo para *k* destinos.

### Roteamento Hierárquico
- Problemas do mundo real
	- Roteadores não são todos idênticos
	- As redes não são homogêneas na prática
- Escala:
	- Uma projeção afirma que até 2020 teremos 50 bilhões de dispositivos conectados à internet.
	- Não dá para armazenar todos os destinos em uma única tabela de rotas
	- Mudanças na tabela de rotas congestionariam os enlaces
- Agrega roteadores em regiões chamadas de Sistemas Autônomos (AS)
- Roteadores no mesmo AS rodam o mesmo protocolo de roteamento: protocolo intra-AS
- EM diferentes AS podem rodas diferentes protocolos de roteamento: protocolo Inter-AS

### Roteadores Intra-AS e Inter-AS

#### Roteadores de Borda
- realizam roteamento inter-AS entre si
- realizam roteamento intra-AS com os outros roteadores do mesmo AS

![[Pasted image 20220524174329.png]]