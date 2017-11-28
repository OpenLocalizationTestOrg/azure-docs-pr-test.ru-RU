---
title: "aaaCreate Azure с выходом в Интернет загрузить балансировки - PowerShell | Документы Microsoft"
description: "Узнайте, как в toocreate из Интернета в диспетчере ресурсов подсистемы балансировки нагрузки с помощью PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="fbc7f-103"><a name="get-started"></a>Создание балансировщика нагрузки для Интернета в Resource Manager с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbc7f-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbc7f-104">Портал</span><span class="sxs-lookup"><span data-stu-id="fbc7f-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="fbc7f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbc7f-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="fbc7f-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="fbc7f-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="fbc7f-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="fbc7f-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="fbc7f-108">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="fbc7f-109">Вы также можете [узнать, как из Интернета toocreate подсистемы балансировки нагрузки с помощью hello классической модели развертывания](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fbc7f-109">You can also [learn how toocreate an Internet-facing load balancer by using hello classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a><span data-ttu-id="fbc7f-110">Развертывание решения hello с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbc7f-110">Deploying hello solution by using Azure PowerShell</span></span>

<span data-ttu-id="fbc7f-111">Hello следующих процедур объясняется, как из Интернета toocreate подсистемы балансировки нагрузки с помощью диспетчера ресурсов Azure с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-111">hello following procedures explain how toocreate an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="fbc7f-112">С помощью диспетчера ресурсов Azure каждый ресурс создается и настроить отдельно и затем поместить toocreate подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a load balancer.</span></span>

<span data-ttu-id="fbc7f-113">Необходимо создать и настроить hello следующие объекты toodeploy подсистемы балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="fbc7f-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="fbc7f-114">Конфигурация внешних IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="fbc7f-115">Пул адресов серверной части: содержит сетевых интерфейсов (NIC) для hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-115">Back-end address pool: contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="fbc7f-116">Правила балансировки нагрузки: содержит правила, которые сопоставляют открытый порт на порт tooa подсистемы балансировки нагрузки hello в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-116">Load-balancing rules: contains rules that map a public port on hello load balancer tooa port in hello back-end address pool.</span></span>
* <span data-ttu-id="fbc7f-117">Правила NAT для входящих подключений: содержит правила, которые сопоставляют открытый порт на порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-117">Inbound NAT rules: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="fbc7f-118">Зонды: содержит доступность toocheck проверки, используемые работоспособности экземпляров виртуальной машины в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-118">Probes: contains health probes used toocheck availability of virtual machine instances in hello back-end address pool.</span></span>

<span data-ttu-id="fbc7f-119">Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="fbc7f-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="fbc7f-120">Настройка toouse PowerShell диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="fbc7f-120">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="fbc7f-121">Убедитесь, что у вас есть hello последнюю версию рабочего модуля hello Azure Resource Manager для PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fbc7f-121">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="fbc7f-122">Войдите в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-122">Sign in tooAzure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="fbc7f-123">При появлении запроса введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="fbc7f-124">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-124">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="fbc7f-125">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-125">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="fbc7f-126">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-126">Create a resource group.</span></span> <span data-ttu-id="fbc7f-127">Если используется существующая группа ресурсов, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="fbc7f-128">Создайте виртуальную сеть и общедоступный IP-адрес пула IP-интерфейса hello</span><span class="sxs-lookup"><span data-stu-id="fbc7f-128">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="fbc7f-129">Создайте подсеть и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="fbc7f-130">Создание Azure открытый ресурс IP-адреса, с именем **общедоступный IP-адрес**, toobe, используемый пулом IP-интерфейса с именем DNS hello **loadbalancernrp.westus.cloudapp.azure.com**. hello, следующая команда использует hello Тип статического выделения.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-130">Create an Azure public IP address resource, named **PublicIP**, toobe used by a front-end IP pool with hello DNS name **loadbalancernrp.westus.cloudapp.azure.com**. hello following command uses hello static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="fbc7f-131">Подсистема балансировки нагрузки Hello использует метку домена hello hello общедоступный IP-адрес как префикс для его полного доменного ИМЕНИ.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-131">hello load balancer uses hello domain label of hello public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="fbc7f-132">Это отличается от hello классической модели развертывания, который использует hello облачной службы как hello балансировки нагрузки полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-132">This is different from hello classic deployment model, which uses hello cloud service as hello load balancer FQDN.</span></span>
   > <span data-ttu-id="fbc7f-133">В этом примере hello полное доменное имя — **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-133">In this example, hello FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="fbc7f-134">Создание пула внешних IP-адресов и пула внутренних адресов</span><span class="sxs-lookup"><span data-stu-id="fbc7f-134">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="fbc7f-135">Создание интерфейса пула IP-с именем **внешнего интерфейса балансировки Нагрузки** , использующий hello **общедоступный IP-адрес** ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-135">Create a front-end IP pool named **LB-Frontend** that uses hello **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="fbc7f-136">Создайте пул адресов серверной части с именем **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-136">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="fbc7f-137">Создание правил NAT, правила балансировщика нагрузки, пробы и балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="fbc7f-137">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="fbc7f-138">В этом примере создается hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="fbc7f-138">This example creates hello following items:</span></span>

* <span data-ttu-id="fbc7f-139">Tootranslate правило NAT, все входящего трафика на tooport 3441 порт 3389</span><span class="sxs-lookup"><span data-stu-id="fbc7f-139">A NAT rule tootranslate all incoming traffic on port 3441 tooport 3389</span></span>
* <span data-ttu-id="fbc7f-140">Tootranslate правило NAT, все входящего трафика на tooport 3442 порт 3389</span><span class="sxs-lookup"><span data-stu-id="fbc7f-140">A NAT rule tootranslate all incoming traffic on port 3442 tooport 3389</span></span>
* <span data-ttu-id="fbc7f-141">Состояние проверки правила toocheck hello работоспособности на страницу с именем **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="fbc7f-141">A probe rule toocheck hello health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="fbc7f-142">Toobalance правило балансировки нагрузки весь входящий трафик на порт 80 tooport 80 на hello адресов в пуле hello серверной части</span><span class="sxs-lookup"><span data-stu-id="fbc7f-142">A load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool</span></span>
* <span data-ttu-id="fbc7f-143">балансировщик нагрузки, который использует все эти объекты.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-143">A load balancer that uses all these objects</span></span>

<span data-ttu-id="fbc7f-144">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-144">Use these steps:</span></span>

1. <span data-ttu-id="fbc7f-145">Создание правил NAT hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-145">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="fbc7f-146">Создайте пробу работоспособности.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-146">Create a health probe.</span></span> <span data-ttu-id="fbc7f-147">Существует два способа tooconfigure зонда.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-147">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="fbc7f-148">проба HTTP</span><span class="sxs-lookup"><span data-stu-id="fbc7f-148">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="fbc7f-149">проба TCP.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-149">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="fbc7f-150">Создайте правило балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-150">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="fbc7f-151">Создайте hello балансировки нагрузки с помощью hello ранее созданных объектов.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-151">Create hello load balancer by using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="fbc7f-152">Создание сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="fbc7f-152">Create NICs</span></span>

<span data-ttu-id="fbc7f-153">Создайте сетевых интерфейсов (или изменить существующие) и связать их tooNAT правила, правила подсистемы балансировки нагрузки и зондов:</span><span class="sxs-lookup"><span data-stu-id="fbc7f-153">Create network interfaces (or modify existing ones) and then associate them tooNAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="fbc7f-154">Получение hello виртуальной сети и подсети виртуальной сети, где hello сетевые адаптеры должны toobe создан.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-154">Get hello virtual network and a virtual network subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="fbc7f-155">Создайте сетевую КАРТУ с именем **быть балансировки нагрузки сетевого адаптера 1**и связать его с первого правила NAT hello и пул адресов серверной части первый (и единственный) hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-155">Create a NIC named **lb-nic1-be**, and associate it with hello first NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="fbc7f-156">Создайте сетевую КАРТУ с именем **балансировки нагрузки nic2 быть**и связать его с hello второе правило NAT и пул адресов серверной части первый (и единственный) hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-156">Create a NIC named **lb-nic2-be**, and associate it with hello second NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="fbc7f-157">Проверьте сетевые адаптеры hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-157">Check hello NICs.</span></span>

        $backendnic1

    <span data-ttu-id="fbc7f-158">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fbc7f-158">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="fbc7f-159">Используйте hello `Add-AzureRmVMNetworkInterface` командлет tooassign hello сетевых адаптеров toodifferent виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-159">Use hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NICs toodifferent VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="fbc7f-160">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="fbc7f-160">Create a virtual machine</span></span>

<span data-ttu-id="fbc7f-161">Рекомендации по созданию виртуальной машины и назначении сетевой карты см. в статье [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) (Создание виртуальной машины в Azure с помощью PowerShell).</span><span class="sxs-lookup"><span data-stu-id="fbc7f-161">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface-toohello-load-balancer"></a><span data-ttu-id="fbc7f-162">Добавление подсистемы балансировки нагрузки toohello hello сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="fbc7f-162">Add hello network interface toohello load balancer</span></span>

1. <span data-ttu-id="fbc7f-163">Получить подсистемы балансировки нагрузки hello из Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-163">Retrieve hello load balancer from Azure.</span></span>

    <span data-ttu-id="fbc7f-164">Загрузка ресурсов подсистемы балансировки нагрузки hello в переменной (Если вы еще не сделали, еще).</span><span class="sxs-lookup"><span data-stu-id="fbc7f-164">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="fbc7f-165">переменная приветствия называется **$lb**. Используйте hello такими же именами из ресурса подсистемы балансировки нагрузки hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-165">hello variable is called **$lb**. Use hello same names from hello load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="fbc7f-166">Загрузка hello внутренней tooa переменной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-166">Load hello back-end configuration tooa variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="fbc7f-167">Загрузка сетевого интерфейса hello уже созданы в переменной.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-167">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="fbc7f-168">Имя переменной Hello **$nic**.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-168">hello variable name is **$nic**.</span></span> <span data-ttu-id="fbc7f-169">Hello имя сетевого интерфейса является hello один из hello предыдущего примера.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-169">hello network interface name is hello same one from hello earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="fbc7f-170">Изменить конфигурацию серверной части hello в сетевом интерфейсе hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-170">Change hello back-end configuration on hello network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="fbc7f-171">Сохраните объект сетевого интерфейса hello.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-171">Save hello network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="fbc7f-172">После добавления пула внутренней подсистемы балансировки нагрузки toohello сетевого интерфейса, она запускает получения сетевого трафика на основе правил балансировки нагрузки hello для этого ресурса подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-172">After a network interface is added toohello load balancer back-end pool, it starts receiving network traffic based on hello load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="fbc7f-173">Обновление существующего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="fbc7f-173">Update an existing load balancer</span></span>

1. <span data-ttu-id="fbc7f-174">С помощью hello загрузить балансировки из Здравствуйте предыдущий пример, присвоить значение переменной toohello объект подсистемы балансировки нагрузки **$slb** с помощью `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-174">By using hello load balancer from hello earlier example, assign a load balancer object toohello variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="fbc7f-175">В следующем примере hello добавьте во входящем правиле NAT — с помощью порт 81 в пуле переднего плана hello и порт 8181 для пула внутренней hello--tooan существующей подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-175">In hello following example, you add an inbound NAT rule--by using port 81 in hello front-end pool and port 8181 for hello back-end pool--tooan existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="fbc7f-176">Сохранение hello новую конфигурацию с помощью `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-176">Save hello new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="fbc7f-177">Удалите балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-177">Remove a load balancer</span></span>

<span data-ttu-id="fbc7f-178">Команда hello `Remove-AzureLoadBalancer` toodelete подсистемы балансировки нагрузки, начатую с именем **балансировки Нагрузки NRP** в группу ресурсов с именем **NRP RG**.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-178">Use hello command `Remove-AzureLoadBalancer` toodelete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="fbc7f-179">Можно использовать необязательный ключ hello **-Force** tooavoid hello строки для удаления.</span><span class="sxs-lookup"><span data-stu-id="fbc7f-179">You can use hello optional switch **-Force** tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbc7f-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbc7f-180">Next steps</span></span>

[<span data-ttu-id="fbc7f-181">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fbc7f-181">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="fbc7f-182">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fbc7f-182">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="fbc7f-183">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="fbc7f-183">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
