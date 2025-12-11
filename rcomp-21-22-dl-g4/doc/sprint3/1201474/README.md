RCOMP 2021-2022 Project - Sprint 2 - Member 1201474 folder
===========================================
# Edifício 1

**Planeamento**
-------------------
# RCOMP SPRINT3 - 1201474
=======================================
# Building 1

## Planeamento
Neste Sprint, foram mantidas todas as definições do projeto do ***Packet Tracer*** elaborado no Sprint anterior, de forma a ser utilizado como base do novo projeto.

### Definição de designações e IDs
Após a definição e distribuição de todas as designações e ids, iniciou-se a simulação no *Packet Tracer*.

* **Building 1 OSPF area id** - 1
* **Backbone OSPF area id** - 0
* **VOIP prefix F0** - 
* **VOIP prefix F1** - 01
* **DNS domain name** - building-1.rcomp-21-22-dl-g4
* **DNS server name** - ns.rcomp-20-21-dl-g4
* **Dns server ip de rede**- 172.18.84.66/26

> Conforme o pedido no enunciado, um dos servers já existentes no projeto do Sprint2 passou a ter o serviço DNS, com o endereço 172.18.84.66 .

## Projeto no *Packet Tracer*
Após a definição e distribuição de todas as designações e ids, iniciou-se a simulação no *Packet Tracer*.

![projeto](Building1.png)
Simulação completa elaborada para o edifício 1.

## 1. Rotas dinâmicas OSPF
* Começámos por eliminar as tabelas de rotas em todos os routers, exceto a rota default que liga ao ISP.
* Depois definimos a área do backbone que tem como id 0.
* De seguida fizemos o mesmo passo mudando os ips para os ips das vlans do edifício 3 e a respetiva wildcard com área 3.

Comandos usados:

router ospf 1 network router-backboneAddress wildcard area 0

network router-address network-wildcard area id

...


### 2. HTTP
Com base na interpretação do eunciado adicionámos um server que assegura os serviços HTTP e que está ligado à network
DMZ. Assim:

* Adicionámos um servidor conectado à VLAN DMZ para assegurar o serviço HTTP.
* Criámos uma página HTML identificando o edifício.


### 3. Serviço DHCPv4
Como está especificado no enunciado, o *router* de cada edifício deve estar configurado de modo a fornecer um serviço **DHCPv4** a todas as *networks* locais excluindo as *networks* DMZ e o *backbone*.
Assim:
* A configuração do VOIP foi feita com a opção 150, de acordo com o pedido no enunciado.

* Os nomes da *pools* utilizados foram:
    * B1-VOIP
    * B1-F1
    * B1-F0
    * B1-WIFI

* Após a configuração de DHCP em cada VLAN foi feita a exclusão do ip dessa VLAN no router através do seguinte comando:
  **ip dhcp excluded-address ip_router**
* De seguida todos os pcs e laptops passam a receber configuração DHCP.


### 4. Serviço VOIP
* Nas portas do switch ligadas aos telefones foi ativado o voice vlan(switchport voice vlan VLANID) e desativado o voice
  vlan(no switchport access vlan).
* De seguida configurámos o serviço de telefonia onde definimos o número máximo de e-phones e o número de cada um.

  ephone-dn 1
  number 1000  
   
  ephone-dn 2
  number 1001

  ...

* Por último, tivemos de preparar as chamadas entre os edifícios, onde foi utilizado o comando ***dia-peer voice***. O padrão escolhido para reconhecer os números do edifício 1 foi **"1..."**, para o 2 foi **"2..."** e para o 4 **"3..."**. Cada padrão é reencaminhado para o *router* do respetivo edifício.

### 5. DNS
* O DNS server(ns.rcomp-21-22-dl-g4) e o DNS domain name(building-1.rcomp-21-22-dl-g4) já tinham sido definidos na configuração do DHCP.
* Assim criámos records como pedido no enunciado.
* Aos restantes servidores adicionámos o DNS server manualmente.

### 6. NAT
* Foram efetuados os comandos guardados no ficheiro de configuração do *router* 1 para cada porta especificada no enunciado, **80(HTTP)**, **443(HTTPS)** e **53(DNS)** para TCP e UDP.

* Por fim, colocou-se cada VLAN dentro da NAT criada à exceção da do backbone, através dos comandos:
  ip nat inside
  ip nat outside

### 7. ACLs

* Para a configuração das ACLs começámos por bloquear as falsificações internas excluíndo a DMZ.
* A seguir permitimos todos os pedidos de ICMP e respostas echo.
* Todo o tráfico para a DMZ foi bloqueado exceto o DNS e HTTP/HTTPS. E o tráfico da DMZ foi permitido.
* Qualquer tráfico direcionado para o router com um IPv4 que pertence a ele foi bloqueado.
* Por fim o tráfico que passa pelo router foi permitido.

Todas as configurações encontram-se no ficheiro de configurações do router.

