# Ethernet

Definido pelo padrão IEEE 802.3, o Ethernet é a tecnologia predominante em LANs com fio.

Inicialmente usava-se redes Ethernet em barramento (com CSMA/CD com recuo exponencial binário).

Posteriormente usou-se topologia estrela com *hubs* (possíveis colisões no *hub*) e atualmente é usada com *switches* (livres de colisões).

Oferece um serviço sem conexão não confirmado para a camada de rede, o que o torna simples e barato.

## O Quadro Ethernet
O **Preâmbulo** é um padrão de uns e zeros alternados usado para sincronização da temporização em Ethernet assíncrona de 10Mbps e em implementações mais lentas.

As versões mais rápidas da Ethernet são síncronas e essa informação de temporização é mantida para fins de compatibilidade.

![Pasted image 20220519144255](imgs/Pasted%20image%2020220519144255.png)

- O campo **Endereço de Destino** contém um endereço de destino MAC.
- O campo **Endereço de Origem** contém um endereço de origem MAC
- O campo **Comprimento/Tipo** suporta dois usos diferentes
- O valor do **tipo** especifica o protocolo da camada superior que recebe os dados depois que o processamento do Ethernet estiver concluído.
- Indica também o número de *bytes* de dados que vêm depois desse campo:
	- se o valor for inferior a $1536_{10}$, ele indica o comprimento.
- Os campos de **Dados** e **Preenchimento** podem ser de qualquer tamanho que não exceda o tamanho máximo permitido para o quadro.
- Um **preenchimento não especificado** será inserido imediatamente após os dados do usuário quando não houver dados de usuário suficientes para que o quadro satisfaça o comprimento mínimo.
- Esse processo de inserção de dados para complementar um quadro muito pequeno é chamado de ***padding*** (enchimento).
- o campo **Checksum** ou FCS (*Frame Check Sequence*) contém um valor CRC de 4 bytes que é criado pelo dispositivo emissor e recalculado pel dispositivo receptor para verificar se há quadros danificados.

### Envio
No **processo de envio**, a camada de enlace encapsula os dados em um quadro contendo os campos MAC de origem e destino (função de endereçamento), o campo comprimento/tipo (identificação de conteúdos) e o campo *Checksum* (detecção de erros).

Antes de transmitir, ele verifica se tem alguém transmitindo.
Ao transmitir, verifica se houve colisão.

### Recepção
No **processo de recepção**, verifica-se se o endereço de destino do quadro é igual ao endereço da placa de rede que o está recebendo, realiza-se novamente o cálculo do *Checksum* e compara-se com o original (verificação de erros).

Por fim, os dados são passados para a camada superior competente (identificação de conteúdos).