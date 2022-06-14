# Protocolos de Roteamento

## Tabela de Roteamento
![](Pasted%20image%2020220609163321.png)

A tabela de roteamento pode dizer muitas coisas sobre um roteador:
- Olhando a tabela, percebemos que esse roteador possui, pelo menos, 3 interfaces (*eth0*, *eth1* e *eth2*)
- Muito provavelmente está conectado a duas redes locais (192.168.1.0/24 e 192.168.2.0/24)
- Conectado a apens uma saída (172.16.32.0/24)

## *Gateway*
Vemos o conceito de "roteador mais inteligente". Esse roteador considera que o 172.16.32.254 é mais inteligente que ele e pode encontrar as redes 10.1.100.0/24 e 10.1.200.0/24. 

Ele não precisa se preocupar como esse outro roteador vai fazer isso: ele simplesmente acredita que ele consegue!

## *Default Gateway*

Assim temos o conceito de *Gateway*: é um portal, nesse caso, o portal de acesso para uma determinada rede. Diferente de *default gateway*.

Dizemos que o *gateway* da rede 10.1.200.0 é o roteador 172.16.32.254.

Essas duas últimas regras podem ser simplificadas utilizando um *default gateway*.

As rotas *default* são usadas para rotear pacotes com destinos que não correspondem as nenhuma das outras rotas da tabela de roteamento.

Geralmente os roteadores são configurados com uma rota *default* para o tráfego dirigido à internet, já que normalmente é impraticável ou desnecessário manter rotas para todas as redes da internet.

Uma rota *default*, na verdade, é uma rota estática especial endereçada a 0.0.0.0 e com máscara 0.0.0.0. Quando um IP de destino é submetido à operação lógica AND com a máscara definida resultará sempre na rede 0.0.0.0.

Podemos reescrever a tabela anterior:
![](Pasted%20image%2020220609164444.png)

**outro exemplo:**

- pacote com destine 192.168.3.12
![](Pasted%20image%2020220609164700.png)

1. Olha a primeira linha: 192.168.3.0/24 é igual a 192.168.1.0? **Não...**
2. Olha na segunda linha: 192.168.3.0/24 é igual a 192.168.2.0/24? **Não...**
3. Olha na terceira linha: 192.168.3.0/24 é igual a 192.168.3.0/24? **Sim!**
4. Como o roteador é diretamente conectado a essa rede, envia o pacote pela *eth2*.

## Sumarização de Rotas
A sumarização de rotas é a "abreviação" de rotas.
Serve para manter uma tabela de roteamento mais limpa

Quanto mais a rede cresce, mais complexa será a tabela de roteamento.

![](Pasted%20image%2020220609165633.png)

### Como fazer essa sumarização?
- Pega-se a tabela de roteamento de um roteador e analisa as rotas;
- Por exemplo: um roteador R1. Sua tabela de roteamento seria:
![](Pasted%20image%2020220609165745.png)

- Vamos "agrupar" as redes 192.168.0.0/30, 192.168.0.3/30 e 192.168.0.64/26.  Esse agrupamento só é possível quando todos possuem o mesmo *gateway*.
![](Pasted%20image%2020220609165913.png)

- Convertemos para binário:
![](Pasted%20image%2020220609165935.png)
- Até onde esse 3 endereços IP são iguais?
- Todos os bites em verde (25 primeiros *bits*) são comuns aos 3 endereços IP, logo podemos sumarizar essas 3 redes em uma única rede: 192.168.0.0/25
- Magicamente 3 rotas viram uma!
- Fazemos o mesmo com os IPs 192.168.0.128, 192.168.0.132 e 192.168.0.192:
![](Pasted%20image%2020220609170108.png)

- Novamente os 25 primeiros bits são iguais, podgo podemos resumir essas três redes em uma: 192.168.0.128/25

**OBS:** 
- Sumarizamos **apenas** rotas que possuem o mesmo *gateway*.
- Muitos roteadores fazem a sumarização de rotas automaticamente, mas isso depende do fabricante e da versão do *firmware*.

## Protocolos Roteáveis
Relembrando: o **IP** é um protocolo da camada de rede e, devido a isso, pode ser roteado por uma *internetwork*, que é uma rede de redes;

Os protocolos que definem a estrutura do pacote e o endereçamento lógico na camada de rede são chamados **protocolos roteados ou roteáveis**;

Exemplo: IPv4 e IPv6

Os protocolos de Roteamento permitem que os roteadores conectados criem um mapa, internamente, de outros roteadores na rede ou na internet.

Roteadores usam protocolos de roteamento para trocar tabelas de roteamento e compartilhar informações de roteamento. Em outras palavras, protocolos de roteamento determinam como os protocolos roteáveis são encaminhados.

Roteadores são capazes de suportar vários protocolos de roteamento independentes e de manter tabelas de roteamento de vários protocolos roteados simultaneamente.

As **tabelas de roteamento** contêm:
- **Tipo de protocolo:** protocolo de roteamento que criou a entrada da tabela de roteamento;
- **Associação destino/próximo salto:** indica se um destino específico está diretamente ligado ao roteador ou se pode ser alcançado com o recurso a outro roteador, chamado *próximo salto*.
- **Métrica:** protocolos de roteamento diferentes utilizam métricas de roteamento diferentes:
	- RIP (*Routing Information Protocol*): utiliza a contagem de saltos como única métrica de roteamento
	- IGRP (*Interior Gateway Routing Protocol*): utiliza uma combinação de métricas (largura de banda, carga, atraso e confiabilidade) para criar um valor de métrica composto.
- **Interface de Saída:** a interface na qual os dados devem ser enviados para que cheguem ao destino final.

As métricas de roteamento são os vlores utilizados para a determinação do melhor caminho até o próximo salto.
![](Pasted%20image%2020220609172555.png)

## Protocolos IGP e EGP
**IGP ->** Um protocolo de roteamento do tipo IGP (*Interior Gateway Protocol*) é utilizado na intercomunicação de redes dentro de um mesmo Sistema Autônomo

**EGP ->** Um protocolo de roteamento EGP (*Exterior Gateway Protocol*) é utilizado, dentro outras coisas, para a intercomunicação de diferentes Sistemas Autônomos

![](Pasted%20image%2020220609172835.png)

- Exemplo único de **EGP**: **BGP** (Border Gateway Protocol), <u>o principal protocolo de roteamento externo da Internet;</u>

- Exemplo de protocolos **IGP**: RIP, IGRP, EIGRP, OSPF e ISIS

### IGP (Internos)

Os IGPs podem ser descritos como protocolos de vetor de distância ou de estado de enlace.

- **RIP** (*Routing Information Protocol*):
	- É o IGP mais tradicionalmente usado
	- Baseado no algorítmo de roteamento por Vetor de Disância
	- Seleciona o caminho com menor número de saltos.
	- Como a contagem de saltos, é a única métrica de roteamento, nem sempre é o caminho mais rápido.
	- Não pode encaminhar um pacote além de 15 saltos.

- **EIGRP** *(Enhanced IGRP)*:
	- Protocolo exclusivo da Cisco
	- Versão avançada do IGRP
	- Algoritmo de Roteamento Vetor de Distância
	- Converge mais rapidamente e gasta menos largura de banda
- **OSPF** *(Open Shortest Peth First)*
	- "*Caminho livre mais curto primeiro*"
	- Determinação de um caminho ótimo
	- Baseado no algoritmo de roteamento por Estado de Enlace
	- Esses critérios incluem as medidas de custo, que são divididas em itens como a velocidade de rota, o tráfego, a confiança e a segurança;
	- Atualmente é o protocolo mais utilizado em sistemas autônomos, juntamente como o ISIS
- **ISIS** *(Intermediate System to Intermediate System)*
	- Bastante similar ao OSPF
	- Baseado no algoritmo de roteamento por estado de Enlace
	- É usado para protocolos roteados que não sejam o IP
- **BGP** *(Border Gateway Protocol)*:
	- O **BGP** é considerado "a cola que mantém a internet ligada"