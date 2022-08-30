# Introdução

## Problema dos Generais Bizantinos


![](Pasted%20image%2020220829101711.png)

### Problema com 2 Generais

- Enviar mensageiros para o capitão vermelho, acampado do outro lado do campo de batalha, avisando o momento exato do ataque.
- O problema do general azul era impedir que as duas diviões do Exército Vermelho combinassem o momento do ataque.
- Condições para o combate e vitória
	- A comunicação entre os militares dos exércitos ocorre somente via mensageiros
	- O exército vermelho ganha se suas tropas atacarem exatamente ao mesmo tempo
	- O exército azul ganha caso contrário
- Mensageiros de uma divisão vermelha devem atravessar as cercanias de Bizâncio

## Sistemas DIstribuídos
- **Segundo Tanenbaum:** Um sistema distribuído é uma coleção de computadores independentes que aparenta aos usuários como se fosse um único computador.
- Dois aspectos da definição:
	- **Hardware:** as máquinas são autônomas
	- **Software:** os usuários vêem o sistema como uma única máquina.
- Deve-se considerar também tolerância a falhas.

![](Pasted%20image%2020220829102534.png)

- **Definição de Coulouris:** 
	- Um sistema no qual os componentes de *hardware* ou *software*, localizados em computadores interligados em rede, se comunicam e coordenam suas ações apenas enviando mensagens entre si
	- Concorrência
	- Inexistência de relógio global
	- Falhas independentes

### Erros que se assume quando desenvolve um SD
- Rede é confiável
- Rede é segura
- Rede é homogênea
- Topologia não muda
- Latência é zero
- *Bandwidth* é infinita
- Custo de transporte é zero
- Existe um administrador

### Vantagens x Desvantagens
- **Vantagens:**
	- **Extensibilidade**
		- O Sistema pode crescer gradativamente
		- Novos softwares podem ser instalados gradativamente
		- Manutenção facilitada
	- **Compartilhamento de Recursos**
		- Recursos de alto custo podem ser melhor utilizados
		- Servidores de arquivo
		- Servidores de e-mail
		- Servidores de correio
		- etc.
	- **Replicação**
		- Diversas cópias de um mesmo arquivo podem ser armazenadas em locais distintos aumentando a confiabilidade
	- **Disponibilidade**
		- Falha de um elemento não interrompe a operação do sistema global

- **Desvantagens**
	- **Gerenciamento:**
		- Dependendo do modelo, cada usuário pode necessitar ser um gerente
		- Execução de backup é complexa
		- Alocação de tempo de processameto
		- Manutenção/evolução do *software*
	- **Desempenho/Confiabilidade**
		Dependência da rede utilizada
	- **Segurança**
		- Para aumentar a flexibilidade do sistema existem clientes com acesso à comunicação básica e isto enfraquece a segurança
		- via de regra, qualquer informação colocada na rede deixa de ser "segredo"
		- Existem mecanismos para melhorar a segurança