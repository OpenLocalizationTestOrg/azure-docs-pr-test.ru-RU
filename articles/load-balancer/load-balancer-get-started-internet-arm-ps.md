---
title: "Создание доступной в Интернете внутренней подсистемы балансировки нагрузки Azure с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как создать балансировщик нагрузки для Интернета в Resource Manager с помощью PowerShell."
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
ms.openlocfilehash: f610afbdfac7b5dd9a1a5eb6812c86d8ce0d63e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="f4cca-103"><a name="get-started"></a>Создание балансировщика нагрузки для Интернета в Resource Manager с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4cca-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4cca-104">Портал</span><span class="sxs-lookup"><span data-stu-id="f4cca-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="f4cca-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4cca-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="f4cca-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="f4cca-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="f4cca-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="f4cca-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f4cca-108">В этой статье описывается модель развертывания с использованием менеджера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f4cca-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="f4cca-109">Вы также можете [узнать, как создать балансировщик нагрузки для Интернета с помощью классической модели развертывания](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f4cca-109">You can also [learn how to create an Internet-facing load balancer by using the classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-by-using-azure-powershell"></a><span data-ttu-id="f4cca-110">Развертывание решения с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4cca-110">Deploying the solution by using Azure PowerShell</span></span>

<span data-ttu-id="f4cca-111">Ниже описана процедура создания балансировщика нагрузки для Интернета с помощью Azure Resource Manager и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4cca-111">The following procedures explain how to create an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="f4cca-112">Azure Resource Manager позволяет по отдельности создавать и настраивать ресурсы, после чего на их основе создается балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f4cca-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a load balancer.</span></span>

<span data-ttu-id="f4cca-113">Чтобы развернуть балансировщик нагрузки, необходимо создать и настроить следующие объекты.</span><span class="sxs-lookup"><span data-stu-id="f4cca-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="f4cca-114">Конфигурация внешних IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="f4cca-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="f4cca-115">Пул внутренних адресов. Содержит сетевые интерфейсы (сетевые карты) для получения виртуальными машинами сетевого трафика от балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f4cca-115">Back-end address pool: contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="f4cca-116">Правила балансировки нагрузки. Содержат правила сопоставления общего порта в балансировщике нагрузки с портом в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="f4cca-116">Load-balancing rules: contains rules that map a public port on the load balancer to a port in the back-end address pool.</span></span>
* <span data-ttu-id="f4cca-117">Правила преобразования сетевых адресов (NAT) для входящего трафика. Содержат правила сопоставления общего порта в балансировщике нагрузки с портом на конкретной виртуальной машине в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="f4cca-117">Inbound NAT rules: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="f4cca-118">Пробы. Содержат пробы работоспособности, с помощью которых можно проверить доступность экземпляров виртуальных машин в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="f4cca-118">Probes: contains health probes used to check availability of virtual machine instances in the back-end address pool.</span></span>

<span data-ttu-id="f4cca-119">Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f4cca-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="f4cca-120">Настройка PowerShell для использования Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f4cca-120">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="f4cca-121">Убедитесь, что вы используете последнюю рабочую версию модуля Azure Resource Manager для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4cca-121">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="f4cca-122">Войдите в Azure.</span><span class="sxs-lookup"><span data-stu-id="f4cca-122">Sign in to Azure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="f4cca-123">При появлении запроса введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="f4cca-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="f4cca-124">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f4cca-124">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="f4cca-125">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="f4cca-125">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="f4cca-126">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f4cca-126">Create a resource group.</span></span> <span data-ttu-id="f4cca-127">Если используется существующая группа ресурсов, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="f4cca-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="f4cca-128">Создание виртуальной сети и общедоступного IP-адреса для пула IP-адресов клиентской части</span><span class="sxs-lookup"><span data-stu-id="f4cca-128">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="f4cca-129">Создайте подсеть и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="f4cca-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="f4cca-130">Создайте ресурс для общедоступного IP-адреса Azure с именем **PublicIP**, который будет использоваться пулом внешних IP-адресов с DNS-именем **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="f4cca-130">Create an Azure public IP address resource, named **PublicIP**, to be used by a front-end IP pool with the DNS name **loadbalancernrp.westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="f4cca-131">В следующей команде используется статическое выделение.</span><span class="sxs-lookup"><span data-stu-id="f4cca-131">The following command uses the static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="f4cca-132">Балансировщик нагрузки использует метку домена общедоступного IP-адреса в качестве префикса к полному доменному имени (FQDN).</span><span class="sxs-lookup"><span data-stu-id="f4cca-132">The load balancer uses the domain label of the public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="f4cca-133">В этом заключается отличие от классической модели развертывания, где в качестве полного доменного имени балансировщика нагрузки используется облачная служба.</span><span class="sxs-lookup"><span data-stu-id="f4cca-133">This is different from the classic deployment model, which uses the cloud service as the load balancer FQDN.</span></span>
   > <span data-ttu-id="f4cca-134">В этом примере используется полное доменное имя **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="f4cca-134">In this example, the FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="f4cca-135">Создание пула внешних IP-адресов и пула внутренних адресов</span><span class="sxs-lookup"><span data-stu-id="f4cca-135">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="f4cca-136">Создайте пул внешних IP-адресов с именем **LB-Frontend**, использующий ресурс **PublicIp**.</span><span class="sxs-lookup"><span data-stu-id="f4cca-136">Create a front-end IP pool named **LB-Frontend** that uses the **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="f4cca-137">Создайте пул адресов серверной части с именем **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="f4cca-137">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="f4cca-138">Создание правил NAT, правила балансировщика нагрузки, пробы и балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="f4cca-138">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="f4cca-139">В этом примере создаются следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="f4cca-139">This example creates the following items:</span></span>

* <span data-ttu-id="f4cca-140">правило NAT, которое направляет весь входящий трафик с порта 3441 на порт 3389;</span><span class="sxs-lookup"><span data-stu-id="f4cca-140">A NAT rule to translate all incoming traffic on port 3441 to port 3389</span></span>
* <span data-ttu-id="f4cca-141">правило NAT, которое направляет весь входящий трафик с порта 3442 на порт 3389;</span><span class="sxs-lookup"><span data-stu-id="f4cca-141">A NAT rule to translate all incoming traffic on port 3442 to port 3389</span></span>
* <span data-ttu-id="f4cca-142">правило пробы, согласно которому будет проверяться состояние работоспособности на странице **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="f4cca-142">A probe rule to check the health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="f4cca-143">правило балансировщика нагрузки, которое балансирует весь входящий трафик на порту 80, перенаправляя трафик на порт 80 других адресов во внутреннем пуле;</span><span class="sxs-lookup"><span data-stu-id="f4cca-143">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool</span></span>
* <span data-ttu-id="f4cca-144">балансировщик нагрузки, который использует все эти объекты.</span><span class="sxs-lookup"><span data-stu-id="f4cca-144">A load balancer that uses all these objects</span></span>

<span data-ttu-id="f4cca-145">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f4cca-145">Use these steps:</span></span>

1. <span data-ttu-id="f4cca-146">Создайте правила NAT.</span><span class="sxs-lookup"><span data-stu-id="f4cca-146">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="f4cca-147">Создайте пробу работоспособности.</span><span class="sxs-lookup"><span data-stu-id="f4cca-147">Create a health probe.</span></span> <span data-ttu-id="f4cca-148">Существует два способа настройки пробы:</span><span class="sxs-lookup"><span data-stu-id="f4cca-148">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="f4cca-149">проба HTTP</span><span class="sxs-lookup"><span data-stu-id="f4cca-149">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="f4cca-150">проба TCP.</span><span class="sxs-lookup"><span data-stu-id="f4cca-150">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="f4cca-151">Создайте правило балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f4cca-151">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="f4cca-152">Создайте балансировщик нагрузки с помощью ранее созданных объектов.</span><span class="sxs-lookup"><span data-stu-id="f4cca-152">Create the load balancer by using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="f4cca-153">Создание сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="f4cca-153">Create NICs</span></span>

<span data-ttu-id="f4cca-154">Создайте сетевые интерфейсы (или измените существующие) и свяжите их с правилами NAT, правилами балансировщика нагрузки и пробами.</span><span class="sxs-lookup"><span data-stu-id="f4cca-154">Create network interfaces (or modify existing ones) and then associate them to NAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="f4cca-155">Получите виртуальную сеть и подсеть виртуальной сети, в которых должны быть созданы сетевые карты.</span><span class="sxs-lookup"><span data-stu-id="f4cca-155">Get the virtual network and a virtual network subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="f4cca-156">Создайте сетевую карту **lb-nic1-be**и сопоставьте ее с первым правилом NAT, а также с первым (и единственным) пулом внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="f4cca-156">Create a NIC named **lb-nic1-be**, and associate it with the first NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="f4cca-157">Создайте сетевую карту **lb-nic2-be**и сопоставьте ее со вторым правилом NAT, а также с первым (и единственным) пулом внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="f4cca-157">Create a NIC named **lb-nic2-be**, and associate it with the second NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="f4cca-158">Проверьте сетевые адаптеры.</span><span class="sxs-lookup"><span data-stu-id="f4cca-158">Check the NICs.</span></span>

        $backendnic1

    <span data-ttu-id="f4cca-159">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="f4cca-159">Expected output:</span></span>

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

5. <span data-ttu-id="f4cca-160">С помощью командлета `Add-AzureRmVMNetworkInterface` назначьте сетевые карты различным виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="f4cca-160">Use the `Add-AzureRmVMNetworkInterface` cmdlet to assign the NICs to different VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="f4cca-161">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f4cca-161">Create a virtual machine</span></span>

<span data-ttu-id="f4cca-162">Рекомендации по созданию виртуальной машины и назначении сетевой карты см. в статье [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) (Создание виртуальной машины в Azure с помощью PowerShell).</span><span class="sxs-lookup"><span data-stu-id="f4cca-162">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface-to-the-load-balancer"></a><span data-ttu-id="f4cca-163">Добавление сетевого интерфейса в балансировщик нагрузки</span><span class="sxs-lookup"><span data-stu-id="f4cca-163">Add the network interface to the load balancer</span></span>

1. <span data-ttu-id="f4cca-164">Извлеките балансировщик нагрузки из Azure.</span><span class="sxs-lookup"><span data-stu-id="f4cca-164">Retrieve the load balancer from Azure.</span></span>

    <span data-ttu-id="f4cca-165">Загрузите ресурс балансировщика нагрузки в переменную (если вы это еще не сделали).</span><span class="sxs-lookup"><span data-stu-id="f4cca-165">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="f4cca-166">Имя переменной — **$lb**. Используйте те же имена из созданного ранее балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f4cca-166">The variable is called **$lb**. Use the same names from the load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="f4cca-167">Загрузите в переменную конфигурацию серверной части.</span><span class="sxs-lookup"><span data-stu-id="f4cca-167">Load the back-end configuration to a variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="f4cca-168">Загрузите в переменную созданный ранее сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="f4cca-168">Load the already created network interface into a variable.</span></span> <span data-ttu-id="f4cca-169">Имя переменной — **$nic**.</span><span class="sxs-lookup"><span data-stu-id="f4cca-169">The variable name is **$nic**.</span></span> <span data-ttu-id="f4cca-170">Имя сетевого интерфейса совпадает с именем в приведенном выше примере.</span><span class="sxs-lookup"><span data-stu-id="f4cca-170">The network interface name is the same one from the earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="f4cca-171">Измените конфигурацию серверной части в сетевом интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="f4cca-171">Change the back-end configuration on the network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="f4cca-172">Сохраните объект сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="f4cca-172">Save the network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="f4cca-173">После того как сетевой интерфейс будет добавлен в пул серверной части балансировщика нагрузки, он начнет получать сетевой трафик согласно правилам балансировки нагрузки для соответствующего ресурса балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f4cca-173">After a network interface is added to the load balancer back-end pool, it starts receiving network traffic based on the load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="f4cca-174">Обновление существующего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="f4cca-174">Update an existing load balancer</span></span>

1. <span data-ttu-id="f4cca-175">Используя балансировщик нагрузки из предыдущего примера, присвойте переменной **$slb** объект балансировщика нагрузки, используя `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f4cca-175">By using the load balancer from the earlier example, assign a load balancer object to the variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="f4cca-176">В следующем примере вы, используя порт 81 во внешнем пуле и порт 8181 во внутреннем пуле, добавите правило NAT для входящего трафика, которое будет применяться к существующему балансировщику нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f4cca-176">In the following example, you add an inbound NAT rule--by using port 81 in the front-end pool and port 8181 for the back-end pool--to an existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="f4cca-177">Сохраните новую конфигурацию с помощью `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="f4cca-177">Save the new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="f4cca-178">Удалите балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f4cca-178">Remove a load balancer</span></span>

<span data-ttu-id="f4cca-179">Воспользуйтесь командой `Remove-AzureLoadBalancer`, чтобы удалить ранее созданный балансировщик нагрузки с именем **NRP-LB** в группе ресурсов **NRP-RG**.</span><span class="sxs-lookup"><span data-stu-id="f4cca-179">Use the command `Remove-AzureLoadBalancer` to delete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="f4cca-180">Чтобы пропустить подтверждение удаления, можно использовать необязательный переключатель **-Force** .</span><span class="sxs-lookup"><span data-stu-id="f4cca-180">You can use the optional switch **-Force** to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4cca-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4cca-181">Next steps</span></span>

[<span data-ttu-id="f4cca-182">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="f4cca-182">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="f4cca-183">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="f4cca-183">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="f4cca-184">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="f4cca-184">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
