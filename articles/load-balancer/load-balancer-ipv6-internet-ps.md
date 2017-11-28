---
title: "Подсистема балансировки нагрузки aaaCreate Azure с выходом в Интернет с IPv6 - PowerShell | Документы Microsoft"
description: "Узнайте, как Подсистема балансировки с протоколом IPv6, с помощью PowerShell для диспетчера ресурсов нагрузки toocreate из Интернета"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, Azure Load Balancer, двойной стек, общедоступный IP-адрес, встроенная поддержка Ipv6, мобильное устройство, Интернет вещей"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="325b5-104">Приступая к созданию балансировщика нагрузки для Интернета с поддержкой IPv6 с помощью PowerShell для Resource Manager</span><span class="sxs-lookup"><span data-stu-id="325b5-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="325b5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="325b5-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="325b5-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="325b5-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="325b5-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="325b5-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="325b5-108">Azure Load Balancer является балансировщиком нагрузки 4-го уровня (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="325b5-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="325b5-109">Подсистема балансировки нагрузки Hello обеспечивает высокую доступность путем распределения входящего трафика между экземплярами службы работоспособности в облачных службах или виртуальных машин в набор балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="325b5-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="325b5-110">Azure Load Balancer может также представить данные службы на нескольких портах, нескольких IP-адресах или обоими этими способами.</span><span class="sxs-lookup"><span data-stu-id="325b5-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="325b5-111">Пример сценария развертывания</span><span class="sxs-lookup"><span data-stu-id="325b5-111">Example deployment scenario</span></span>

<span data-ttu-id="325b5-112">Hello следующей схеме показано решение, которое развертывается в этой статье по балансировке нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="325b5-112">hello following diagram illustrates hello load balancing solution being deployed in this article.</span></span>

![Сценарий использования балансировщика нагрузки](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="325b5-114">В этом случае будут созданы следующие ресурсы Azure hello:</span><span class="sxs-lookup"><span data-stu-id="325b5-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="325b5-115">балансировщик нагрузки для Интернета с общедоступными IPv4- и IPv6-адресами;</span><span class="sxs-lookup"><span data-stu-id="325b5-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="325b5-116">два загрузить балансировки правила toomap hello открытые виртуальные IP-адреса toohello закрытый конечные точки</span><span class="sxs-lookup"><span data-stu-id="325b5-116">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>
* <span data-ttu-id="325b5-117">Группа доступности toothat содержит hello две виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="325b5-117">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="325b5-118">две виртуальные машины;</span><span class="sxs-lookup"><span data-stu-id="325b5-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="325b5-119">виртуальный сетевой интерфейс для каждой виртуальной машины с назначенными IPv4 и IPv6-адресами;</span><span class="sxs-lookup"><span data-stu-id="325b5-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a><span data-ttu-id="325b5-120">Развертывание решения hello, с помощью hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="325b5-120">Deploying hello solution using hello Azure PowerShell</span></span>

<span data-ttu-id="325b5-121">Привет, следующие шаги показывают, как с помощью диспетчера ресурсов Azure с помощью PowerShell подсистемы балансировки нагрузки, toocreate из Интернета.</span><span class="sxs-lookup"><span data-stu-id="325b5-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="325b5-122">С помощью диспетчера ресурсов Azure каждый ресурс создается и настроить отдельно, затем объединить toocreate ресурса.</span><span class="sxs-lookup"><span data-stu-id="325b5-122">With Azure Resource Manager, each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="325b5-123">toodeploy подсистемы балансировки нагрузки, создания и настройки hello следующие объекты:</span><span class="sxs-lookup"><span data-stu-id="325b5-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="325b5-124">Конфигурация интерфейсных IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="325b5-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="325b5-125">Пул адресов серверной части - содержит сетевых интерфейсов (NIC) для hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="325b5-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="325b5-126">Правила балансировки нагрузки — содержит правила сопоставления открытый порт hello tooport подсистемы балансировки нагрузки в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="325b5-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="325b5-127">Правила NAT для входящих подключений — содержит правила, сопоставление порта открытый порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="325b5-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="325b5-128">Проверяет — содержит доступность toocheck проверки, используемые работоспособности экземпляров виртуальных машин в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="325b5-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="325b5-129">Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="325b5-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="325b5-130">Настройка toouse PowerShell диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="325b5-130">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="325b5-131">Убедитесь, что у вас есть hello последнюю версию рабочего модуля hello Azure Resource Manager для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="325b5-131">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="325b5-132">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="325b5-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="325b5-133">При появлении запроса введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="325b5-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="325b5-134">Проверьте hello подписки для учетной записи hello</span><span class="sxs-lookup"><span data-stu-id="325b5-134">Check hello subscriptions for hello account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="325b5-135">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="325b5-135">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="325b5-136">Создайте группу ресурсов (этот шаг можно пропустить, если вы используете существующую группу).</span><span class="sxs-lookup"><span data-stu-id="325b5-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="325b5-137">Создайте виртуальную сеть и общедоступный IP-адрес пула IP-интерфейса hello</span><span class="sxs-lookup"><span data-stu-id="325b5-137">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="325b5-138">Создайте виртуальную сеть с подсетью.</span><span class="sxs-lookup"><span data-stu-id="325b5-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="325b5-139">Создайте Azure общедоступный IP-адрес (PIP) ресурсы для hello переднего плана пул IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="325b5-139">Create Azure Public IP address (PIP) resources for hello front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="325b5-140">Подсистема балансировки нагрузки Hello использует метку домена hello hello общедоступный IP-адрес как префикс для его полного доменного ИМЕНИ.</span><span class="sxs-lookup"><span data-stu-id="325b5-140">hello load balancer uses hello domain label of hello public IP as prefix for its FQDN.</span></span> <span data-ttu-id="325b5-141">В этом примере, полных доменных имен hello *lbnrpipv4.westus.cloudapp.azure.com* и *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="325b5-141">In this example, hello FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="325b5-142">Создание интерфейсных конфигураций IP-адресов и внутреннего пула адресов</span><span class="sxs-lookup"><span data-stu-id="325b5-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="325b5-143">Создайте конфигурацию адрес интерфейса, использующий hello общедоступных IP-адресов, созданный.</span><span class="sxs-lookup"><span data-stu-id="325b5-143">Create front-end address configuration that uses hello Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="325b5-144">Создайте внутренние пулы адресов.</span><span class="sxs-lookup"><span data-stu-id="325b5-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="325b5-145">Создание правил балансировки нагрузки, правил преобразования сетевых адресов, пробы и балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="325b5-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="325b5-146">В этом примере создается hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="325b5-146">This example creates hello following items:</span></span>

* <span data-ttu-id="325b5-147">правило NAT для tootranslate весь входящий трафик на порте 443 tooport 4443</span><span class="sxs-lookup"><span data-stu-id="325b5-147">a NAT rule tootranslate all incoming traffic on port 443 tooport 4443</span></span>
* <span data-ttu-id="325b5-148">toobalance правило балансировки нагрузки весь входящий трафик на порт 80 tooport 80 на hello адресов серверной части пула hello.</span><span class="sxs-lookup"><span data-stu-id="325b5-148">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="325b5-149">нагрузки балансировки правило tooallow RDP соединение toohello виртуальных машин на порт 3389.</span><span class="sxs-lookup"><span data-stu-id="325b5-149">a load balancer rule tooallow RDP connection toohello VMs on port 3389.</span></span>
* <span data-ttu-id="325b5-150">состояние проверки правила toocheck hello работоспособности на страницу с именем *HealthProbe.aspx* или службе через порт 8080</span><span class="sxs-lookup"><span data-stu-id="325b5-150">a probe rule toocheck hello health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="325b5-151">балансировщик нагрузки, который использует все эти объекты.</span><span class="sxs-lookup"><span data-stu-id="325b5-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="325b5-152">Создание правил NAT hello.</span><span class="sxs-lookup"><span data-stu-id="325b5-152">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="325b5-153">Создайте пробу работоспособности.</span><span class="sxs-lookup"><span data-stu-id="325b5-153">Create a health probe.</span></span> <span data-ttu-id="325b5-154">Существует два способа tooconfigure зонда.</span><span class="sxs-lookup"><span data-stu-id="325b5-154">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="325b5-155">проба HTTP</span><span class="sxs-lookup"><span data-stu-id="325b5-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="325b5-156">или проба TCP:</span><span class="sxs-lookup"><span data-stu-id="325b5-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="325b5-157">В этом примере мы будем приветствия toouse TCP-зонды.</span><span class="sxs-lookup"><span data-stu-id="325b5-157">For this example, we are going toouse hello TCP probes.</span></span>

3. <span data-ttu-id="325b5-158">Создайте правило балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="325b5-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="325b5-159">Создайте hello подсистемы балансировки нагрузки с помощью hello ранее созданных объектов.</span><span class="sxs-lookup"><span data-stu-id="325b5-159">Create hello load balancer using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a><span data-ttu-id="325b5-160">Создать сетевые адаптеры для hello внутренней виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="325b5-160">Create NICs for hello back-end VMs</span></span>

1. <span data-ttu-id="325b5-161">Получить hello виртуальную сеть и подсеть виртуальной сети, где hello сетевые адаптеры должны toobe создан.</span><span class="sxs-lookup"><span data-stu-id="325b5-161">Get hello Virtual Network and Virtual Network Subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="325b5-162">Создайте IP-конфигурации и сетевых адаптеров для hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="325b5-162">Create IP configurations and NICs for hello VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a><span data-ttu-id="325b5-163">Создание виртуальных машин и назначить новые сетевые адаптеры hello</span><span class="sxs-lookup"><span data-stu-id="325b5-163">Create virtual machines and assign hello newly created NICs</span></span>

<span data-ttu-id="325b5-164">Дополнительные сведения о создании виртуальной машины см. в статье [Создание виртуальной машины Windows с помощью Resource Manager и PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="325b5-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="325b5-165">Создайте группу доступности и учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="325b5-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="325b5-166">Создайте каждой виртуальной Машины и назначьте hello предыдущих создан сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="325b5-166">Create each VM and assign hello previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="325b5-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="325b5-167">Next steps</span></span>

[<span data-ttu-id="325b5-168">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="325b5-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="325b5-169">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="325b5-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="325b5-170">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="325b5-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
