# Acesso ao Enlace
- Camada de Enlace na Internet
	- Modelo Básico da Internet
		- Dentro de um único prédio, as LANs são bastante utilizadas para interconexões.
		- Infraestrutura geograficamente distribuída é construída a partir de linhas privadas ponto-a-ponto
- Protocolo de enlace de dados utilizados em linhas ponto-a-ponto
	- **PPP (Point-to-Point Protocol**

## PPP Point-to-Point Protocol
Descrito na RFC 1661 e mais elaborado na RFC 1662

#### Características
- Realiza o tratamento de erros
- Reconhece e trata diferentes protocolos
- Permite que endereçcos IP sejam negociados em tempo de conexão
- Permite autenticação
- Orientado a caractere (quadros representam um número inteiro de *bytes*)

- Enquadramento utilizando marcadores não ambíguos e detecção de erros
- Um protocolo de controle de enlace para ativar, testar, negociar opções e desativar linhas: **LCP (Link Control Protocol)**
- Um protocolo para negociar opções da camada de rede, permitindo o uso de vários protocolos de redes: **NCP (Network Control Protocol)**

#### Quadro PPP
![[Pasted image 20220517172912.png]]
**Delimitação:** *flag* **01111110**
**Endereçco**: Contém valor fixo **1111111**
**Controle:** Contém o valor padrão **00000011**
- O LCP fornece um mecanismo para omitir o Endereço e o Controle

### Usos:

#### SONET
#### ADSL
#### DSLAM

## Alocação

**Como** alocar um único canal de *broadcast* entre usuários concorrentes?

- Alocação Estática
- Alocação Dinâmica

### Alocação Estática
- Geralmente usa multiplexação
- Eficiente quando:
	- Número de usuários é pequeno e fixo
	- Cada usuário demanda tráfego pesado
- Problemas
	- Número de usuários grande e variável
	- Tráfego em rajadas

### Alocação Dinâmica
Baseado em 5 premissas:

#### Tráfego independente
- Existem *n* estações independentes que geram quadros a serem transmitidos
- A estação fica bloqueada até o quadro ser totalmente transmitido

#### Premissa de Canal Único
- Todas as estações compartilham um único canal de comunicação, tanto para transmissão quanto para recepção

#### Colisões observáveis
- A transmissão "simultânea" de dois ou mais quadros por estações causa uma colisão
- Estações são capazes de detectar colisões
- Quadros envolvidos em colisões devem ser retransmitidos posteriormente.

#### Tempo contínuo ou segmentado
- Em tempo *contínuo* os quadros podem ser transmitidos a qualquer instânte.
- Em tempo *segmentado* (**Slotted**) o tempo é dividido em intervalos discretos (slots) e as transmissões de quadros sempre começam no início de um *slot*

#### Detecção de Portadora
- **Com** a detecção de portadora (*Carrier Sense*) as estações conseguem detectar se o canal está em uso antes de tentarem utilizá-lo e podem aguardar até um momento em que ele esteja livre;
- **Sem** detecção de portadora (No Carrier Sense) as estações não conseguem detectar se o canal está em uso. Assim, transmitem quando necessário.


## Tipos de Enlace
- Ponto-a-Ponto (dio único, ex: PPP, SLIP)
- *Broadcast* (fio ou meio compartilhado, ex: Ethernet)
- *Switched* (Ex: switched Ethernet, ATM, etc)

[[Ethernet]]
