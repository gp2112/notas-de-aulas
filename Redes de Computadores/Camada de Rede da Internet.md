# Camada de Rede da Internet
![[Pasted image 20220526143341.png]]
## Endereços IP
Endereço IP -> identificador de 32 *bits* (IPv4) para interfaces de roteadores e *hosts*.

![[Pasted image 20220526143450.png]]

**Interface:** conexão entre roteador ou *host* e enlace físico.
- Roteador tem tipicamente múltiplas interfaces
- *Hosts* podem ter múltiplas interfaces
- Endereços IP são associados com interfaces, não com o *host* ou com o roteador

![[Pasted image 20220526143604.png]]
**Endereço IP**
- Parte de rede -> bit mais significativo
- Parte de *host* -> bits menos significativos

**O que é uma rede? (na perspectiva do endereço)**

As interfaces de dispositivos com a mesma parte de rede no endereço IP podem fisicamente se comunicar sem o auxílio de um roteador.

**Exemplo:** uma rede consistindo de 3 redes IP (para endereços IP começando com 223, os primeiros 24 bits são o endereço de rede)

![[Pasted image 20220526143936.png]]
**Como encontrar as redes:**
- Separe cada interface de roteadores e *hosts*
- Crie ilhas de redes isoladas
- Use a técnica de nuvens

**Endereços Especiais**
![[Pasted image 20220526151932.png]]

## Endereçamento *Classful*
![[Pasted image 20220526152009.png]]
- Classe A endereça $2^7=128$  redes e $2^{24} - 2 = 16777214$ hosts por rede
- Classe B endereça $2^{14}=16384$ redes e $2^{16}-2=65534$ hosts por redes
- Classe C endereça $2^{21}=2097152$ redes e $2^8-2=254$ hosts por rede

- Uso ineficiente do espaço do endereçamento, exaustão do espaço de endereços.
- Ex: rede de Classe B aloca endereços para 65000 hosts, mesmo se só existem 2000 hosts naquela rede.

**CIDR (*Classledd INterdomain Routing***
- A porção de endereço de rede tem tamanho arbitrário
- Formato do endereço: A.B.C.D/x, onde x é o número de bits na parte de rede do endereço
![[Pasted image 20220526152516.png]]

### Como obter um endereço IP?
**Endereço Fixo ->** definido pelo administrador

**Endereço dinâmico por DHCP ->** permite a atribuição dinâmica de endereços IP.

1. O *host* envia (por *broadcast*) uma mensagem "DHCP discover".
2. O servidor DHCP responde com mensagem "DHCP offer"
3. O *host* solicita um endereço IP com mensagem "DHCP request"
4. O servidor DHCP envia um endereço com a mensagem "DHCP ack"

![[Pasted image 20220526153456.png]]

**Como o ISP obtém seu bloco de endereço?**
Por meio do **ICANN** (*Internet Corporation for Assigned Names and Numbers*)
- Aloca endereços
- Gerencia DNS
- Atribui nomes de domínios
- Alocação de intereços é realizada pela **IANA**
- Por meio dos **RIRs**: *Regional Internet Registry* 

### Formato do datagrama IPv4
![[Pasted image 20220526153859.png]]
**Envio do Datagrama:**
- A verifica o endereço de rede de E e descobre que está em uma sub-rede diferente
- A consulta suatabela de roteamento e descobre que o pacote deve ser enviado para o roteador no endereço 223.1.1.4
- A repassa o pacote para a camada de enlace, que envia o datagrama em um quadro para o roteador

**Recebimento do Datagrama**
- Roteador recebe o datagrama da sua camada de enlace
- Roteador consulta sua tabela de roteamento e descobre que o pacote deve ser enviado para o E
- Roteador verifica o endereço de rede de E e descobre que está na mesma sub-rede de sua interfaze com endereço 223.1.2.9
- Roteador repassa o pacote para a camada de enlace, que envia o pacote em um quadro para E