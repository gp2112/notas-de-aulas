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


**Funcão da Camada de Enlace de Dados** -> Transferir dados da camada de rede da máquina de **origem** para a camada de rede da máquina **destino**.

![[Pasted image 20220510143017.png]]
- Lida com quadros -> grupos de bits transmitidos pela rede
- Depede da camada Física para enviar/receber bits

- **Controle de Enlace Lógico (LLC)** -> Fornece mecanismos de multiplexação e controle de fluxo.
- **Controle de Acesso ao Meio (MAC)** -> Provê acesso a um canal de comunicação e o endereçamento neste canal.

![[Pasted image 20220510143240.png]]
- Dois elementos físicos **fisicamente conectados**:
	- Host-Roteador, roteador-roteador, host-host
- Unidade de dados: quadro(*frame*)

![[Pasted image 20220510143333.png]]

### Serviços

- Delimitação de quadros (enquadramento ou framing)
	- Divide e encapsula pacotes em quadros
	- Acrescenta "endereços físicos" usados nos cabeçalhos dos quadros para identificar a fonte e o destino dos quadros.
- Acesso ao enlace:
	- Implementa acesso ao canal se o meio é compartilhado
- Entrega confiável entre os dois equipamentos fisicamente conectados:
	- Raramente usado em enlaces com baixa taca de erro (fibra, alguns tipos de par traçado)
	- Enlaces sem fio (wireless) -> altas taxas de erro.
- **Controle de Fluxo**
	- Limitação da transmissão entre transmissor e receptor
- **Detecção de erros**
	- Erros causados pela atenuação do sinal e ruídos
	- Receptor detecta erro e pede para reenviar o quadro perdido.
- **Correção de Erros**
	- Receptor identifica e corrige o bit com erro(s) sem recorrer à retransmissão.

### Protocolos
A maioria dos protocolos de enlace possuem os seguintes elementos:

- **Cabeçalho** -> possui informações de controle para que haja a comunicação horizontal entre as camadas de enlace da origem e destino. É formado por diversos campos, cada um com uma função específica no protocolo.
- **Dados** -> Encapsula o PDU de rede passando pela camada de rede.
- **Código de Detecção de Erro (CDE)** -> tem a função de controlar erros na camada de enlace.
![[Pasted image 20220510144052.png]]

### Tipos de Serviços

Os serviços são fornecidos nas seguintes combinações:

- Serviço sem conexão não confirmado
- Serviço sem conexão confirmado
- Serviço orientado a conexão confirmado

#### Serviço sem Conexão não Confirmado
- Conexão não é previamente estabelecida
- A máquina emissora envia *frames* sem receber confirmação de recebimento da máquina receptora
- Quadros perdidos são ignorados e tratados pelas camadas superiores
- Apropriado para:
	- Aplicações onde a taxa de erro é muito baixa
	- Aplicações de tempo real onde dados atrasados são piores que dados ruins, como streaming de áudio
- Serviço normalmente usado em LANs

#### Serviço sem Conexão Confirmado
- Conexão náo e estabelecida previamente
- Cada *frame* enviado é individualmente confirmado. Dessa forma o emissor sabe se o *frame* foi recebido ou não e poderá enviá-lo novamente
- Origem usa um mecanismo de temporização para reenviar quadros não confirmados
- Útil para canais não confiáveis, como Wireless

#### Serviço Orientado à Conexão Confirmado
- Mais sofisticado
- Emissor e receptor estabelecem conexão antes do envio de dados;
- Cada *frame* enviado é numerado
- Cada *frame* é recebido exatamente uma vez e todos os *frames* chegam em ordem
- O serviço oferecido para a camada de rede é uma sequência de bits corretos

**Considerações:**
- Confirmação na camada de enlace é uma otimização, não um requisito -> pode ser deixada para a camada de transporte (fim-a-fim)
- O serviço a ser oferecido para a camada de rede depende, dentre outros fatores, da aplicação que utilizará esse serviço.

### Delimitação de Quadros
- A camada física transmite uma sequência de bits (bit stream), que pode ser grande e conter erros;
- A camada de enlace deve detectar e, se necessário, corrigir os erros de transmissão
- A sequência de bits é quebrada em *frames*.

#### Métodos para Delimitação de Quadros
- Contagem de Caracteres
- Caracteres de início e de fim, com caractere de preenchimento
- Flags de início e de fim, com caractere de preenchimento
- Flasg de início e de fim, com caractere de preenchimento;
- Violação de código da camada física

#### Contagem de Caracteres
Usa um campo no cabeçalho para indicar o número de caracteres no quadro.

**Problema**: o caractere de contagem pode sofrer erro de transmissão, impossibilitando o reconhecimento do início do próximo quadro;

Assim, **não é** usado na prática para protocolos da camada de enlace.

![[Pasted image 20220510152747.png]]

#### Caracteres de Início e de Fim
Reconhecimento do início e do fim de um quadro através dos caracteres ASCII:

- **Início:** DLE STX (Data Link Scape, Start TeXt)
- **De Fim**: DLE ETC (Data Link Scape, End of TeXt)

**->** Método usado em protocolos orientados a caracteres.

- Se os caracteres oara DLE STX e DLE ETX ocorrem nos dados -> Inserir um caracter DLE adicional antes de cada DLE nos dados (*byte stuffing*)

Técnica presa ao código ASCII e a caracteres de 8bits.

![[Pasted image 20220510153208.png]]

#### Flags de início e de fim
Permite codificar caracteres com um número arbitrário de bits por caractere, usando um padrão especial de bits (*flag*) para sinalizar início e fim do quadro

- Sempre que 5 "ums" (1s) consecutivos são encontrados nos dados, o emissor insere um zero (*bit stuffing*), para que não haja a interpretação de um flag de entrada/saída no meio do dado.

- Quando o receptor encontra cinco "ums" seguidos por um zero, o *stuff* é retirado

![[Pasted image 20220510153430.png]]

#### Violação de Código
- Baseado em características da camada física (por isso violação)
- O início e fim do quadro é definido pela utilização de um código de transmissão inválido.
- Por serem sinais reservados, não é necessário inserir bytes ou bits de dados
- São fáceis de serem identificados

![[Pasted image 20220510154859.png]]

Bits a serem transmitidos -> 01000111111000110001000001111110

a) Contagem de Caracteres: 01000111111000110001000001111110

b) Caracteres de Início e Fim: 000100000000001001000111111000110001000000010000011111100001000000000011

c) Flags de Início e Fim:

01111110010001111101000110001000001111101001111110