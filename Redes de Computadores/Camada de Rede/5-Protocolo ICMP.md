# O Protocolo ICMP (*Internet Control Message Protocol*)
A operação de uma rede IP é monitorada rigorosamente pelos roteadores.

Quando algo inesperado ocorre, o evento é reportado pelo protocolo **ICMP** definido na RFC-729;

O protocolo ICMP também é utilizado para testes de rede através do comando *ping*.

O ICMP utiliza mensagens para realizar suas tarefas. Na sua RFC são definidas 16 mensagens, sendo as mais importantes:
- *Destination Unreachable*: Utilizado quando a sub-rede/roteador não podem localizar o destino.
- *Time Exceeded*: Notifica o descarte do pacote, pois seu TTL atingiu valor zero.
- *Source Quench*: Essa mensagem solicita ao emissor uma redução dos dados enviados.
- *Redirect*: Um roteador envia esta mensagem quando, ao receber um pacote, detecta-se a existência de uma rota melhor através de outro roteador.
- *Echo*: Usado pelo comando *ping* para verifica conectividade.
- *Echo Reply*: Resposta à requisição Echo.


