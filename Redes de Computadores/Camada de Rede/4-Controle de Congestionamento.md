# Controle de Congestionamento
Excesso de Pacotes em uma sub-rede -> congestionamento que pode levar a um *deadlock* da rede.

**Métodos de Controle de Congestionamento**
- Descarte de Pacotes
- Pré-alocação de *buffers*
- Controle isorrítmico - Limitação do número de pacotes de trânsito
- Controle de tráfego na camada de enlace

**Com base de princípios de controle:**

- Open Loop: Tentam resolver o problema com um bom projeto, não cabendo alterações durante a execução
- Closed Loop: São baseadas no conceito de *feedback*. 
	1. Monitoram o sistema para detectar quando e onde o congestionamento ocorre;
	2. Passam a informação para onde as ações podem ser tomadas;
	3. Ajustam a operação do sistema de modo a corrigir o problema.

- Métricas de monitoramento:
	- % de pacotes descartados
	- Tamanho médio das filas
	- Número de pacotes retransmitidos
	- Atraso no envio
- Aumento desses números indica congestionamento.


