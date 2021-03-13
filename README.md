# Prof Michel - Curso de Redes - Cisco Packet Tracer
# 
## Anotações:
#
### Cabeamento

##### Direto - Usado para conectar equipamentos de funções diferentes
pc -> hub
pc -> switch

##### Crossover - Usado para conectar equipamentos com funções iguais
pc -> pc
hub -> hub
---
### Switch x Hub
-- Switch tem melhor desempenho e segurança que um Hub
-- Switch tem uma porta console usada pra configuração
##### Segurança
	-- No Hub, quando uma máquina envia um pacote pra outra, o pacote vai pro HUB que distribui para todas, e a destinatária é a única que aceitará. Mas se houver um sniffer em alguma máquina, o pacoté poderá ser interceptado por outro que não seja o destinatário
	-- No Switch, quando uma máquina envia um pacote para outra, o pacote vai pro switch mas apenas o destinatário correto receberá esse pacote do switch. Impedindo ação do sniffer.
##### Desempenho
	-- No Hub, se duas máquinas enviam um pacote para outrem ao mesmo tempo, ocorrerá colisão e o processo precisará ser refeito.
	-- No Switch não existe isso, o switch pode receber pacotes ao mesmo tempo que não ocorrerá problemas de colisão.

-- Em uma mesma faixa de IP's, um mesmo range, os equipamentos ligados em HUB's interligados comunicam perfeitamente
-- Se o grupo de equipamentos ligados a um HUB forem de uma rede diferente do grupo de equipamentos ligados a outro HUB, essa comunicação entre HUB's nao ocorre
-- É sabido que redes que utilizam HUB possuem muito mais colisão do que redes que utilizam Switch, com isso impactando o desempenho da rede. Isso se dá devido ao HUB não conseguir trabalhar com duas ou mais requisições ao mesmo tempo. Quando isso ocorre ele descarta as solicitações a as solicita novamente.
-- O Broadcast também causa uma diferença grande de desempenho entre HUB e Switch. Serviço de DHCP utiliza Broadcast, o processo para um equipamento receber um IP do servidor DHCP é muito mais demorado em redes com HUB do que em redes com Switch quando as máquinas pedem DHCP ao mesmo tempo.

### Roteador
- Faz a comunicação entre redes diferentes
- Se eu tenho um HUB com uma rede 192.168.10.x e outro HUB com 192.168.20.x, e eu quero fazer com que os equipamentos ligados a estes dois HUB's se comuniquem, eu utilizo um Roteador Profissional (Nao um Roteador Integrado, caseiro) e faço a configuração pra que em cada uma das portas ligadas a cada HUB ele receba um IP da rede correspondente. Ou seja, o Roteador é uma um equipamento ligado em cada uma das redes, recebendo um IP em cada uma delas.
	- Com isso feito, eu vou configurar as máquinas da rede A e da rede B para que o Roteador seja o Gateway de cada uma delas. Lembrando que pra Rede A ele tem um IP como gatway e pra Rede B ele tem toutro IP como gateway.
---
### Servidor DHCP
- Distribui IP para os clientes de uma rede, dentro de uma faixa pré configurada
- Processo de solicitação de IP pela máquina cliente
	1. O cliente envia, via protocolo DHCP, para o broadcast 255.255.255.255 (todas as máquinas), pedido para localizar o servidor DHCP
	2. O hub dispara para todas as maquinas da rede o pacote DHCP para descobrir quem é o servidor DHCP
	3. O servidor DHCP responde informando o seu IP
	4. O Cliente então solicita um IP ao servidor DHCP
	5. O Servidor DHCP retorna informando ao cliente o seu IP
### Servidor HTTP
- Servidor web é um software responsável por aceitar pedidos em HTTP de clientes, geralmente os navegadores, e servi-los com respostas em HTTP, incluindo opcionalmente dados, que geralmente são páginas.
### Servidor DNS
- Os servidores DNS (Domain Name System, ou sistema de nomes de domínios) são os responsáveis por localizar e traduzir para números IP os endereços dos sites que digitamos nos navegadores.
- Observar o processo de simulação, quando digitamos o IP no navegador, ao inves do endereço, o processo de DNS não ocorre, o que torna mais rápido a abertura da página.
---
### Conceitos de Redes
Classe A - Tem o primeiro octeto entre 1 e 127 - N.H.H.H - 255.0.0.0  ou /8 - até 126 redes e  16.777.214 (2^24 -2) hosts por rede
Classe B - Tem o primeiro octeto entre 128 e 191 - N.N.H.H - 255.255.0.0  ou  /16- até 16.384 (2^14) redes e  65.534 (2^16 -2) hosts por rede 
Classe C - Tem o primeiro octeto entre 192 e 223 - N.N.N.H - 255.255.255.0  ou  /24 - até 2.097.150 (2^21) redes e  254 hosts por rede (rede caseira)
Classe D - Tem o primeiro octeto entre 224 e 239 - Multicast (internet)
Classe E - Tem o primeiro octeto entre 240 e 255 - Experimental
Obs: São sempre retirados 2 hosts por rede que é o IP do Endereço da Rede e o IP do Broadcast (o primeiro e o último IP, respectivamente). O Broadcast é o IP utilizado para mandar pacote para todos os equipamentos da rede.

Pra descobrir o endereço da rede é só pegar um IP da rede é multiplicar pela máscara. Por exemplo:
192.168.20.55
255.255.255.0

Cada octeto é transformado para binário e cada número binário é multiplicado. Como sabemos que 255 é uma sequencia de 8 bits de número 1, basta replicar o octeto:
192.168.20

Como o último octeto da máscara é zero, etão é uma sequencia de 8 bits 0, logo zera o último octeto todo quando multiplicado
192.168.20.0
---
### Broadcast
- broadcasting é um método de transferência de mensagem para todos os receptores simultaneamente.
- O serviço de DHCP, por exemplo, utiliza broadcast
- Em redes muito grandes, o broadcast pode causar problemas de desempenho. Por isso é importante configurar várias redes menores interligadas por um Roteador. O Roteador impede a passagem dos pacotes de broadcast entre redes diferentes.