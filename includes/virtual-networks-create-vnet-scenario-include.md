## <a name="scenario"></a><span data-ttu-id="58204-101">Сценарий</span><span class="sxs-lookup"><span data-stu-id="58204-101">Scenario</span></span>
<span data-ttu-id="58204-102">toobetter показывают, как toocreate виртуальной сети и подсети, этот документ будет использовать сценарий hello ниже.</span><span class="sxs-lookup"><span data-stu-id="58204-102">toobetter illustrate how toocreate a VNet and subnets, this document will use hello scenario below.</span></span>

![Сценарий виртуальной сети](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="58204-104">В этом сценарии вы создадите виртуальную сеть с именем **TestVNet** и зарезервированным блоком CIDR **192.168.0.0./16**.</span><span class="sxs-lookup"><span data-stu-id="58204-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="58204-105">Виртуальная сеть будет содержать следующие подсетей hello:</span><span class="sxs-lookup"><span data-stu-id="58204-105">Your VNet will contain hello following subnets:</span></span> 

* <span data-ttu-id="58204-106">**FrontEnd** с блоком **192.168.1.0/24** в качестве блока CIDR.</span><span class="sxs-lookup"><span data-stu-id="58204-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="58204-107">**BackEnd** с блоком **192.168.2.0/24** в качестве блока CIDR.</span><span class="sxs-lookup"><span data-stu-id="58204-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

