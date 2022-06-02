# Protocolos de Acesso Múltiplo
Algorítmo distribuído que determina como as estações compartilham o canal, isto é, determinam quando cada estação pode transmitir.

- Principal função da subcamada MAC (Medium Acess COntrol)
- Comunicação sobre o compartilhamento do canal deve utilizar o próprio canal.

#### O que esperar destes protocolos:
- Síncrono/Assíncrono
- Informação necessária sobre outras estações
- Robustez
- Desempenho


# Classes
## Particionamento de Canal

### TDMA - Acesso Múltiplo por Divisão de Tempo
- Acesso ao canal é feito por "turnos"

## Acesso Aleatório
- Quando um nó tem um pacote a enviar
	- Transmite com toda a taxa do canal
	- Não há regra de coordenação pré-determinada entre os nós
- **Colisão:** dois nós ou mais transmitindo

### ALOHA puro
- Estação realiza o envio sempre que tiver dados para enviar
- Se houver colisão, aguarda um tempo aleatório para realizar a transmissão
- Taxa máxima de sucesso é de 18%.

### Slotted ALOHA
- Tempo é dividido em compartimentos de tamanho igual (tempo de transmissão de um quadro)
- Estação transmite no início do próximo compartimento
- Se houver colisão, retransmite o quadro nos futuros compartimentos após um tempo aleatório
- Taxa máxima de sucesso é de 37%

### CSMA (Acesso Múltiplo com Detecção de Portadora)

- Escuta antes de transmitir
	- Se o canal parece vazio: transmite o pacote
	- Se o canal está ocupado, adia a transmissão
- Diferentes protocolos:
	- **CSMA 1-Persistente**: Assim que canal tiver livre, realiza transmissão.
	- **CSMA Não-persistente:** se o canal está ocupado, escuta o canal novamente após um intervalo aleatório de tempo. Assim que concluir que o canal está livre, realiza a transmissão,
	- **CSMA P-Persistente**: assim que o canal se tornar livre, realiza a transmissão com probabilidade *p* ou aguarda até o próximo compartimento (de acordo com a probabilidade *(1-p)*) e repete essa operação até acontecer um envio.

- Em todos, havendo colisão, aguarda tempo aleatório.

#### Comparação de acordo com o *throughtput*
![Pasted image 20220517175223](imgs/Pasted%20image%2020220517175223.png)

### CSMA/CD - CSMA / Detecção de Colisão
- Escuta o canal enquanto transmite
- Transmissões com colisões são interrompidas, reduzindo o desperdício do canal
- Retransmissões persistentes ou não-persistentes
- **Recuo exponencial binário**: ao transmitir um quadro que já tenha experimentado $n$ colisões, um nó escolhe o valor de $K$  aleatoriamente a partir de $\{0,1,2,...,2^n-1\}$
- Usado no Ethernet, IEEE 802.3

## Passagem de Permissão

### *Pooling*
- Nó *master* "convida" os nós *slaves* a transmitirem um de cada vez de maneira circular
- Quando cada nó termina sua transmissão, o nó mestre repassa a permissão para o próximo
- Usado no IEEE 802.15 (base para o ZIgBee) e no *Bluetooth*
- Problemas:
	- *Polling Overhead* 
	- Latência (atraso de seleção)
	- Ponto único de falha (mestre)

[Piggybacking](Piggybacking.md)
[Resumo MAC](Resumo%20MAC.md)