# Comutadores da Camada de Enlace
A função de um comutador ou *switch* é receber quadros da camada de enlace e repassá-los para enlaces de saída.

O comutador em si é transparente aos hospedeiros e roteadores na sub-rede (eles não possuem endereço MAC).

**Filtragem:** é a capacidade de um comutador que determina se um quadro deve ser repassado ou se deve apenas ser descartado.

**Repasse**: é a capacidade de um comutador que determina as interfaces para as quais um quadro deve ser dirigido e então dirigir o quadro a essas interfaces.

Filtragem e repasse por comutadores são feitos com uma tabela de comutação:

![[Pasted image 20220519155424.png]]

Comutadores são **autodidatas**.

O comutador aprende a localização do adaptador com endereço `01-12-23-34-45-56` ao receber um quadro com esse endereço na origem a partir de uma de suas interfaces.

![[Pasted image 20220519155533.png]]

O horário é marcado pois se passar um período de tempo (tempo de envelhecimento) sem receber novos quadros de um dispositivo, o seu endereço MAC é apagado da tabela.

Podemos identificar diversas vantagens no uso de comutadores:
- Eliminação de colisões;
- Enlaces Heterogêneos;
- Gerenciamento