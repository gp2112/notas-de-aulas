# Endereços de LAN e ARP

## Endereços IP
Endereços da camada de rede.

- Usados para levar o pacote até a rede de destino
- IPv4: 32 bits;
- IPv6: 128 bits

## Endereço MAC (ou de LAN ou Físico)
Usado para levar o pacote de uma interface física a outra fisicamente conectada com a primeira (isto é, na mesma rede).

- Endereços MAC com 48 bits (na maioria das LANs)
- Gravado na memória somente de leitura (ROM) do adaptador de rede

![[Pasted image 20220519145608.png]]
- A alocação dos endereços MAC é administrada pelo IEEE.
- O fabricante compra porções do espaço de endereçco MAC (para assegurar a unicidade);
- Endereçamento MAC tem portabilidade:
	- é possível mover uma placa de uma rede para outra sem reconfiguração de endereço MAC.

## ARP - Protocolo de Resolução de Endereços
**Como determinar o endereço MAC de *B* dado seu indereço IP?**
Usando o protocolo ARP (*Address Resolution Protocol*)!

- Cada nó IP (*Host* ou Roteador) de uma LAN possui um módulo e uma tabela ARP.
- A **Tabela ARP** faz o mapeamento de endereçcos IP/MAC para alguns nós da LAN
	- O mapeamento inclui: *endereço IP*; *endereçco MAC, TTL*
	- TTL (*Time to Live*): tempo depois do qual o mapeamento de endereços será esquecido (tipicamente 20min)

1. *A* conhece o endereço IP de *B* e quer descobrir o endereço físico de *B*
2. *A* envia em *broadcast* um pacote ARP de consulta contendo o endereço IP de *B*
3. Todas as máquinas na LAN recebem a consulta ARP
4. *B* recebe o pacote ARP e responde a *A* com o seu endereço físico
5. *A* armazena os pares de endereço IP+MAC até que a informação se torne obsoleta (esgota a temporização).
	1. Operação em *soft state* --> informação que desaparece com o tempo se não for reatualizada.

### Roteamento para outra LAN

![[Pasted image 20220519152617.png]]
- **Caminho**: roteamento de *A* para *D* via *R*
- Na tabela de roteamento do *host* origem, os pacotes destinados a *D* devem ser enviados ao IP `111.111.111.110`
- Na tabela ARP do *host* origem, com o IP especificado, os quadros devem ser destinados ao endereço MAC `E6-E9-00-17-BB-4B`

1. Cria o pacote IP com origem A, destino D
2. *A* usa ARP para obter o endereço de camada física de *R* corresponde ao endereço IP `111.111.111.110`
3. *A* cria um quadro Ethernet com o endereço físico de *R* como destino, o quadro Ethernet contém o pacote IP de *A* para *D*
4. A camada de enlace de *A* envia o quadro Ethernet
5. A camada de enlace de *R* recebe o quadro Ethernet
6. *R* remove o pacote IP do quadro Ethernet, verifica que ele se destina a D
7. *R* usa ARP para obter o endereço físico de D
8. *R* cria quadro contendo um pacote de *A* para *D* e envia para *D*

