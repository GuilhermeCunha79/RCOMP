RCOMP 2021-2022 Project - Sprint 2 - Member 1201474 folder
===========================================
# Edifício 1

**Planeamento**
-------------------
> No inicio do projeto dividimos os endereços de rede pelos vários espaços e serviços. Esta divisão encontra-se devidamnete justificada no planning.md.
No cálculo da subnetting atribuimos as mascáras para cada end device dependendo do seu número de nodes, após isso ordenámos por ordem descrescente e somámos o respetivo tamanho de blocos a cada endereço, após isso calculámos o broadcast, o primeiro e último valores de endereço válidos.
Para além dos endereços, atribuímos também as VLANs a cada end device tendo em consideração o intervalo atribuído ao nosso grupo.
Para o edifício 1 os endereços de rede atribuidos e VLANs encontram-se na seguinte tabela:
>
![Subrede](NetworkAdress.png)
![Subrede](NetworkAdress2.png)
>
> Apesar de apenas serem estas VLANs do edifício, estão representadas na simulação todas as VLANs do campus, nos switches.
>
**Projeto no Packet Tracer**
--------------------------
>Depois de todos os cálculos feitos em relação aos endereços e às VLANs, iniciámos a simulação no packet tracer. Para o edifício 3 a rede definida foi a seguinte:
>
![Simulação](Building1_simulation.png)
>
**Explicação do projeto implementado**

>**Backbone**
>
> O backbone do campus está representado através do Switch B1_MC que corresponde ao main cross connect, dos Switches B2_ICC, B3_ICC, B4_ICC e os seus routers que correspondem aos restantes edifícios do campus, e também  pelo router do edifício 1.
> Tal como no Sprint 1, as ligações de dados pelos edifícios foi realizada através dos ICs e HCs e destes para os end devices. Apesar de não ser visível na simulação, ligámos o MC aos vários ICs utilizando cabos redundantes para o caso de eventualidades. As ligações MC - IC são feitas usando cabos de fibra e nas entre IC - HC e todas as outras ligações usámos cabos de cobre em coerência com o sprint 1.
>
>
> **Ligação à Internet**
>
> Para representar a ligção à internet usámos uma Clound, um router ISP de endereço (15.203.48.117/30) e um Modem. O routerB1 está a completar a ligação.
>
>
> **Especificações do Edifício 1**
>
> A implementação do edifício 1 começa a partir do Switch B1_ICC que representa o IC, este está ligado a dois Switches B1_HCC_F0 e B1_HCC_F1 que representam os HCs de ce cada piso, por sua vez ao B1_HCC_F0 estão ligados 3 Switches e ao B1_HCC_F1 estão ligados 4 que representam os CPs de cada piso, a estes estão ligados 1 Server, 1 PC, 1 Phone-PT, 1 Access Point e por wireless 1 Laptop. No piso 0 não foi adicionado nenhum access point visto desde o sprint 1, este piso n tinha. 
> Apenas existia um access point no piso 1 visto a internet deste abrangia o piso 0 também.
Todos os switches foram configurados de modo a terem as portas necessárias para as ligações de cobre e fibra (portas FGE para os cabos de fibra e portas FCE para cabos de cobre), e todos se encontram em trunk mode de modo a partilharem a database de VLANs.
Uma vez que o objetivo do sprint era apresenar um plano de rede, optámos por simplificar e não apreentar a quantidade total de nodes que se encontra no enunciado, assim cada end device representa esses nodes.
>
> 