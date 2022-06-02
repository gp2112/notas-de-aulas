# Endereços IP
Formados por 32 *bits*, representados por notação decimal com pontos.
- Exemplo: 192.168.0.1

Possuem uma parte que representa a rede e outra que representa o *host*:
![](Pasted%20image%2020220602163731.png)

## Máscara de Rede


## NAT (Network Address Translation)
O NAT é a tradução de Endereço de Rede, definida na RFC-1631.
Foi criada para reduzir o número de IPs(IPv4) públicos na internet.

Ao realizar uma NAT, alguns endereços são matidos e outros são alterados dependendo da direção do pacote em uma conexão. Um dispositivo habilitado para NAT geralmente opera na borda de uma rede *stub*. 

**Rede *stub*** -Rede que possui uma única conexão para a rede externa.

Ao realizar uma NAT para os endereços de uma rede local é necessário possuir ao menos um endereço público que estará localizado no roteador que provê acesso à internet.

![](Pasted%20image%2020220602164141.png)

Ao receber um pacote pela rede local, o roteador altera o conteúdo do cabeçalho do pacote, trocando o endereço privado de origem pelo seu endereço público. Este mapeamento é armazenado na tabela NAT e o pacote é encaminhado.

Ao responder, o *host* da internet irá endereçar o pacote ao endereço interno global, pois foi este quem o enviou.

Ao receber a resposta, o roteador saberá que esta é uma resposta para o *host* interno por meio do mapeamento existente na tabela NAT criada por ele.

Para prover esse serviço sem que haja mapeamentos duplicados, a NAT utiliza uma multiplexação no nível das portas, por meio da PAT - *Port Address Translation*.

A PAT faz um mapeamento mais detalhado na tabela NAT utilizando IP de origem, IP de destino e porta de origem e destino.

![](Pasted%20image%2020220602164758.png)

## Desvantagens
Apesar de todas as vantagens apresentadas pela NAT, ela também possui desvantagens:
- Aumenta o atraso devido à tradução de cada endereço IP dentro dos cabeçalhos dos pacotes;
- Leva à perda da rastreabilidade de IP ponta-a-ponta, pois é muito mais difícil rastrear pacotes que passam por diversas alterações de endereço;
- Força alguns aplicativos que usam endereçamento IP a pararem de funcionar, pois oculta os endereços IP ponta-a-ponta.

## Links
[jodies.de/ipcalc](https://jodies.de/ipcalc)
www.subnettingquestions.com