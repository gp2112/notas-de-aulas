# Camada de Rede

A Camada de Rede tem a função de transportar pacotes entre os sistemas finais da rede.
Ela deve ter uma entidade em cada sistema final ou roteador da rede.

![Pasted image 20220524163056](imgs/Pasted%20image%2020220524163056.png)
### **Três Funções Importantes**:
- **Determinação de Caminhos:** rota escolhida pelos pacotes entre a origem e o destino (algoritmo de roteamento)
- **Comutação:** mover pacotes entre as portas de entrada e de saída dos roteadores
- **Estabelecimento de Conexão:** algumas arquiteturas de rede exigem o estabelecimento de circuitos virtuais antes da transmissão de dados.

Existem dois serviços para entregar pacotes em seus respectivos destinos:
- Redes de Circuitos Virtuais
- Redes de Datagramas

**Protocolo de Roteamento** -> Especifica como roteadores se comunicam uns com os outros.

**Protocolo roteável** -> Pode ser encaminhado para uma outra rede. (ex: ip)

---
# Serviços
Existem dois tipos de serviços para entregar pacotes aos seus destinos.

## Redes de Circuitos Virtuais (VC)
- Estabelece-se uma conexão antes do envio de dados
- Libera-se a conexão após troca de dados
- Cada pacote transporta um identificador do VC, não transporta o endereço completo do destino.
- Cada roteador na rota mantém informações de estado para a conexão que passa por ele.
- **Vantagens:**
	- Orientado ao desempenho
	- A banda passante e os recursos do roteador podem ser alocados por VC
	- Controle de Qualidade de Serviço (QoS) por VC

### Sinalização
- É usado para estabelecer, manter e encerrar Circuitos Virtuais.
- Usados em ATM, *Frame Relay*, X-25, mas não na Internet.

![Pasted image 20220524164612](imgs/Pasted%20image%2020220524164612.png)
- Ótimo para conversação humana
	- tempos restritos, exigências de confiabilidade
	- Necessário para serviço garantino
- Sistemas finais mais simples:
	- Telefones
	- Complexidade dentro da rede

## Redes de Datagramas
- Não estabelece conexões!
- Não há informação de estado de conexão nos roteadores.
- Pacotes tipicamente trasnsportam o endereço de destino
	- Pacotes para o mesmo destino podem seguir diferentes rotas.
- Usado na internet!
![Pasted image 20220524165355](imgs/Pasted%20image%2020220524165355.png)
- Dados trocados entre computadores.
- Sistemas finais inteligentes
	- podem se adaptar, realizar controle e recuperação de erros.
	- rede é simples.
	- Complexidade nos sistemas finais.
- Muitos tipos de enlaces
