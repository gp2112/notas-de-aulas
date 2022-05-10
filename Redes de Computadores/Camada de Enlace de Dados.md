# Camada de Enlace de Dados
---
Adaptado do material da Professora Kalinka Castelo Branco, das aulas de Redes de Computadores, ICMC-USP

Guilherme Paixão - 05/05/2022

---

![[Pasted image 20220505154850.png]]


## Arquitetura IEEE 802
A Arquitetura IEEE 802 é resultado da tentativa de estabelecer uma arquitetura padrão, nos moldes do *RM-OSI/ISO*, orientada para redes locais.

Define somente padrões para os equivalentes níveis físicos e de enlace do *RM-OSI*.

- **IEEE 802**
	- Conjunto de normas para LANs e MANs
	- Padrão adotado pela ANSI, NIST e ISSO
	- É dividido em partes que são publicados como livros separados

- **IEEE 802.1**
	- Apresenta uma introdução ao conjunto de padrões e primitivas de interface

- **IEEE 802.2 - Logical Link Control**
	- Descreve a parte superior da camada de interface e primitivas de interface

- **Três padrões importantes para redes locais:
	- IEEE 802.3: CSMA/CD
	- IEEE 802.4: Rede em Barramento
	- IEEE 802.5: Rede em Anel (*Token Ring*)

![[Pasted image 20220505143255.png]]

A **Camada Física** executa um papel-chave na comunicação entre computadores, mas os seus esforços, sozinhos, <u>não são suficientes</u>. 
Cada uma das suas funções tem suas limitações, que a **Camada de Enlace** trata.

![[Pasted image 20220505143502.png]]
![[Pasted image 20220505143513.png]]
Os padrões **IEEE** são os padrões LAN predominantes e mais conhecidos. Envolvem apenas as camadas mais inferiores: física e enlace.

**IEEE 802.3 ->** Especifica a camada física e a parte do acesso por canal da camada de enlace (<u>padrão Ethernet oficial</u>)

O **padrão IEEE** parece violar o modelo OSI, à primeira vista:

- **Modelo OSI ->** é uma orientação geral amplamente aceita.
- **Padrão IEEE->** surge posteriormente para resolver problemas surgidos após as redes terem sido criadas. Possui subcamadas LLC e MAC

### IEEE 802 - 802.2 - LLC - Logical Link Control

O padrão **LLC** do IEEE é independente do padrão LAN Ethernet 802.3, e não mudará - não importa o sistema de LAN usado.

Os campos de controle do **LLC** servem para uso em todos os sistemas LAN, não apenas a ethernet, motivo pelo qual a subcamada LLC formalmente não faz parte das especificações do sistema IEEE 802.3

Todas as camadas abaixo da subcamada LLC são específicas da tecnologia de LAN individual em questão.

A subcamada **Media Access Control (MAX)** trata dos protocolos que um host segue para acessar os meios físicos.

**LLC - Logical Link Control**
- Padrões 802.3,4,5,6 não oferecem uma comunicação confiável.
- Para alguns protocolos (e.g. IP) este tipo de serviço é suficiente.

**Padrão IEEE 802.2**
- Provê um serviço de enlace com controle de erro e controle de fluxo.
- Esconde as diferenças entre os diversos protocolos pelos padrões 802.
- Oferece um único formato e interface para a camada de rede.

![[Pasted image 20220505150231.png]]
Provê três tipos de serviços:
- Datagrama não confiável
- Datagrama confirmado
- Orientado a conexão confiável
- Cabeçalho do LLC é baseado no HDLC

**TL,DR**
- Se comunica com as camadas de nível superior através do LLC
- Usa convenção de endereçamento simples
- Usa o Media Access Control (MAC) para escolher que computador transmitirá os dados binários, em um grupo onde todos os computadores estejam tentando transmitir ao mesmo tempo.

#### Endereçamento MAC
- Os endereços MAC (ou físico) têm 48 bits de comprimento e são expressos com doze dígitos hexadecimais
- [0:6] dígitos $b_{16}$ -> identificam o fabricante
- [6:13] dígitos $b_{16}$ -> administrado pelo fornecedor específico
- As vezes são chamados de *burned-in address (BIAs)* porque eles são gravados na ROM e são copiados para a RAM quando a placa de rede é inicializada.
- No linux, execute o comando *ifconfig -a* para ver o endereçco MAC da placa do seu computador. Ex: 88:b1:11:c0:5a:08

![[Pasted image 20220505152748.png]]

Antes de sair da fábrica, o fabricante do hardware atribui um endereçco físico a cada placa de rede. Esse endereçco é programado em um chip na placa de rede. Como o MAC está localizado na placa de rede, se a placa de rede for trocada, o endereçco físico da estação mudará para o novo endereço MAC.

Em uma rede Ethernet, quando um dispositivo quer enviar dados para outro dispositivo, ele pode abrir um caminho de comunicação com o outro dispositivo usando seu endereço mac. 

Quando uma origem envia dados em uma rede, os dados carregam o endereçco MAC do destino pretendido. Como esses dados trafegam pelos meios da rede, a placa de rede em cada dispositivo na rede verifica se o seu endereçco MAC corresponde ao endereçco de destino físico carregado pelo pacote de dados.

Uma parte importante do **encapsulamento** e do **desencapsulamento** é a adição de endereçcos MAC de origem e destino. As informações não podem ser enviadas ou entregues corretamente em uma rede sem esses endereços.

**Desvantagem:** endereçcos MAC não têm estrutura e são considerados espaços de endereços contínuos.

![[Pasted image 20220505153457.png]]

### Enquadramento
Ajuda a obter as informações essenciais que não poderiam, de outra forma, ser obtidas apenas com fluxos de bit codificados.

Exemplos dessas informações são:
- que computadores estão se comunicando entre si.
- quando a comunicação entre computadores começa e termina.
- um registro dos erros que ocorreram durante a comunicação.
- de quem é a vez de "falar" em uma "conversa" entre computadores.

![[Pasted image 20220505153734.png]]

### Media Access Control (MAC)
O Media Access Control (MAC) se refere a protocolos que determinam que computador, em um ambiente de meios compartilhados (domínio de colisão) tem permissão para transmetir dados.

Há duas grandes categorias de MAC: 
- Determinística (revezamento)
	- ex: *token ring*
- Não Determinística (FIFO)
	- ex: Aloha CSMA/CD (Detecção de Portadora Múltiplo Acesso com Detecção de Colisão)

### Ethernet e IEEE 802.3
O nome *Ethernet* descreve um recurso essencial do sistema: o meio físico.

O Palo Alto Research Center (PARC), da Xerox, desenvolveu o primeiro sistema Ethernet experimental nos anos 70. Isso foi usado como base para a especificação 802.3 de 1980.

Logo após, a Digital Equipment Corporation, a Intel e a Xerox desenvolveram e lançaram uma especificação Ethernet, versão 2.0, que foi substancialmente compatível com a IEEE 802.3. Juntas, a Ethernet e a IEEE 802.3 detêm atualmente a maior fatia de mercado de todos os protocolos LAN.

Hoje, o termo Ethernet é frequentemente usado para se referir a todas as LANs baseadas em CSMA/CD (Carrier Sense Multiple Access/Collision Detect) que normalmente estão em conformidade com as especificações Ethernet, incluindo a IEEE 802.3.

**Carcterísticas:**
- são LANs baseadas em CSMA/CD
- são redes de broadcast
- são implementadas através de hardware

A Ethernet fornece serviços correspondentes às camadas 1 e 2, enquanto a IEEE 802.3 especifica a camada física, a camada 1 e a parte de acesso a canais da camada de enlace, a camada 2, mas não define um protocolo de controle de enlace lógico.

![[Pasted image 20220505154805.png]]
![[Pasted image 20220505154814.png]]



