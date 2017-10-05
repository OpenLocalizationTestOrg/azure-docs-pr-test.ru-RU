---
title: "Создание подсистемы балансировки нагрузки для Интернета с поддержкой IPv6 с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как создать балансировщик нагрузки для Интернета с поддержкой IPv6 с помощью PowerShell для Resource Manager."
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
ms.openlocfilehash: 9d3cd37d3f2912301904b0a35f6fbc978d173079
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="4d2fd-104">Приступая к созданию балансировщика нагрузки для Интернета с поддержкой IPv6 с помощью PowerShell для Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4d2fd-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d2fd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d2fd-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="4d2fd-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="4d2fd-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="4d2fd-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="4d2fd-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="4d2fd-108">Azure Load Balancer является балансировщиком нагрузки 4-го уровня (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="4d2fd-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="4d2fd-109">Балансировщик нагрузки обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными экземплярами службы в облачных службах или виртуальных машинах, определенных в наборе балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="4d2fd-110">Azure Load Balancer может также представить данные службы на нескольких портах, нескольких IP-адресах или обоими этими способами.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="4d2fd-111">Пример сценария развертывания</span><span class="sxs-lookup"><span data-stu-id="4d2fd-111">Example deployment scenario</span></span>

<span data-ttu-id="4d2fd-112">На следующей схеме показано решение балансировки нагрузки, которое развертывается в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-112">The following diagram illustrates the load balancing solution being deployed in this article.</span></span>

![Сценарий использования балансировщика нагрузки](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="4d2fd-114">В этом сценарии вы создадите следующие ресурсы Azure:</span><span class="sxs-lookup"><span data-stu-id="4d2fd-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="4d2fd-115">балансировщик нагрузки для Интернета с общедоступными IPv4- и IPv6-адресами;</span><span class="sxs-lookup"><span data-stu-id="4d2fd-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="4d2fd-116">два правила балансировки нагрузки для сопоставления общедоступных виртуальных IP-адресов с частными конечными точками;</span><span class="sxs-lookup"><span data-stu-id="4d2fd-116">two load balancing rules to map the public VIPs to the private endpoints</span></span>
* <span data-ttu-id="4d2fd-117">группу доступности, которая содержит две виртуальные машины;</span><span class="sxs-lookup"><span data-stu-id="4d2fd-117">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="4d2fd-118">две виртуальные машины;</span><span class="sxs-lookup"><span data-stu-id="4d2fd-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="4d2fd-119">виртуальный сетевой интерфейс для каждой виртуальной машины с назначенными IPv4 и IPv6-адресами.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-the-solution-using-the-azure-powershell"></a><span data-ttu-id="4d2fd-120">Развертывание решения с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d2fd-120">Deploying the solution using the Azure PowerShell</span></span>

<span data-ttu-id="4d2fd-121">Ниже описана процедура создания балансировщика нагрузки для Интернета с помощью Azure Resource Manager и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="4d2fd-122">Azure Resource Manager позволяет по отдельности создавать и настраивать ресурсы, после чего на их основе создается единый ресурс.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-122">With Azure Resource Manager, each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="4d2fd-123">Чтобы развернуть балансировщик нагрузки, необходимо создать и настроить следующие объекты:</span><span class="sxs-lookup"><span data-stu-id="4d2fd-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="4d2fd-124">Конфигурация интерфейсных IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="4d2fd-125">Пул внутренних адресов. Содержит сетевые интерфейсы (сетевые карты) для получения виртуальными машинами трафика от балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="4d2fd-126">Правила балансировки нагрузки. Содержат правила сопоставления общего порта в балансировщике нагрузки с портом в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="4d2fd-127">Правила NAT для входящего трафика. Содержат правила сопоставления общего порта в балансировщике нагрузки с портом на конкретной виртуальной машине в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="4d2fd-128">Пробы. Содержат пробы работоспособности, с помощью которых можно проверить доступность экземпляров виртуальных машин в пуле внутренних адресов.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="4d2fd-129">Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="4d2fd-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="4d2fd-130">Настройка PowerShell для использования Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4d2fd-130">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="4d2fd-131">Убедитесь, что вы используете последнюю рабочую версию модуля Azure Resource Manager для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-131">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="4d2fd-132">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="4d2fd-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="4d2fd-133">При появлении запроса введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="4d2fd-134">Проверка подписок для учетной записи</span><span class="sxs-lookup"><span data-stu-id="4d2fd-134">Check the subscriptions for the account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="4d2fd-135">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-135">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="4d2fd-136">Создайте группу ресурсов (этот шаг можно пропустить, если вы используете существующую группу).</span><span class="sxs-lookup"><span data-stu-id="4d2fd-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="4d2fd-137">Создание виртуальной сети и общедоступного IP-адреса для пула IP-адресов клиентской части</span><span class="sxs-lookup"><span data-stu-id="4d2fd-137">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="4d2fd-138">Создайте виртуальную сеть с подсетью.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="4d2fd-139">Создайте общедоступный IP-адрес (PIP) Azure для интерфейсного пула IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-139">Create Azure Public IP address (PIP) resources for the front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="4d2fd-140">Балансировщик нагрузки использует метку домена общедоступного IP-адреса в качестве префикса к полному доменному имени (FQDN).</span><span class="sxs-lookup"><span data-stu-id="4d2fd-140">The load balancer uses the domain label of the public IP as prefix for its FQDN.</span></span> <span data-ttu-id="4d2fd-141">В этом примере полные доменные имена — *lbnrpipv4.westus.cloudapp.azure.com* и *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-141">In this example, the FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="4d2fd-142">Создание интерфейсных конфигураций IP-адресов и внутреннего пула адресов</span><span class="sxs-lookup"><span data-stu-id="4d2fd-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="4d2fd-143">Создайте интерфейсную конфигурацию адресов, которая использует созданные вами общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-143">Create front-end address configuration that uses the Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="4d2fd-144">Создайте внутренние пулы адресов.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="4d2fd-145">Создание правил балансировки нагрузки, правил преобразования сетевых адресов, пробы и балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="4d2fd-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="4d2fd-146">В этом примере создаются следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="4d2fd-146">This example creates the following items:</span></span>

* <span data-ttu-id="4d2fd-147">правило NAT, которое направляет весь входящий трафик с порта 443 на порт 4443;</span><span class="sxs-lookup"><span data-stu-id="4d2fd-147">a NAT rule to translate all incoming traffic on port 443 to port 4443</span></span>
* <span data-ttu-id="4d2fd-148">правило балансировщика нагрузки, которое балансирует весь входящий трафик на порту 80, перенаправляя трафик на порт 80 других адресов во внутреннем пуле;</span><span class="sxs-lookup"><span data-stu-id="4d2fd-148">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="4d2fd-149">правило балансировщика нагрузки, которое разрешает подключение к виртуальным машинам по протоколу удаленного рабочего стола на порте 3389;</span><span class="sxs-lookup"><span data-stu-id="4d2fd-149">a load balancer rule to allow RDP connection to the VMs on port 3389.</span></span>
* <span data-ttu-id="4d2fd-150">правило пробы, которое проверяет состояние работоспособности на странице *HealthProbe.aspx* или службу на порте 8080;</span><span class="sxs-lookup"><span data-stu-id="4d2fd-150">a probe rule to check the health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="4d2fd-151">балансировщик нагрузки, который использует все эти объекты.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="4d2fd-152">Создайте правила NAT.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-152">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="4d2fd-153">Создайте пробу работоспособности.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-153">Create a health probe.</span></span> <span data-ttu-id="4d2fd-154">Существует два способа настройки пробы:</span><span class="sxs-lookup"><span data-stu-id="4d2fd-154">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="4d2fd-155">проба HTTP</span><span class="sxs-lookup"><span data-stu-id="4d2fd-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="4d2fd-156">или проба TCP:</span><span class="sxs-lookup"><span data-stu-id="4d2fd-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="4d2fd-157">В этом примере мы используем пробу TCP.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-157">For this example, we are going to use the TCP probes.</span></span>

3. <span data-ttu-id="4d2fd-158">Создайте правило балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="4d2fd-159">Создайте балансировщик нагрузки, используя ранее созданные объекты.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-159">Create the load balancer using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-the-back-end-vms"></a><span data-ttu-id="4d2fd-160">Создание сетевых карт для внутренних виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4d2fd-160">Create NICs for the back-end VMs</span></span>

1. <span data-ttu-id="4d2fd-161">Получите виртуальную сеть и подсеть виртуальной сети, в которых должны быть созданы сетевые карты.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-161">Get the Virtual Network and Virtual Network Subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="4d2fd-162">Создайте конфигурации IP-адресов и сетевые карты для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-162">Create IP configurations and NICs for the VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-the-newly-created-nics"></a><span data-ttu-id="4d2fd-163">Создание виртуальных машин и назначение только что созданных сетевых карт</span><span class="sxs-lookup"><span data-stu-id="4d2fd-163">Create virtual machines and assign the newly created NICs</span></span>

<span data-ttu-id="4d2fd-164">Дополнительные сведения о создании виртуальной машины см. в статье [Создание виртуальной машины Windows с помощью Resource Manager и PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d2fd-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="4d2fd-165">Создайте группу доступности и учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="4d2fd-166">Создайте каждую из виртуальных машин и назначьте только что созданные сетевые карты.</span><span class="sxs-lookup"><span data-stu-id="4d2fd-166">Create each VM and assign the previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type the username and password of the local administrator account."

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

## <a name="next-steps"></a><span data-ttu-id="4d2fd-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d2fd-167">Next steps</span></span>

[<span data-ttu-id="4d2fd-168">Приступая к настройке внутренней подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="4d2fd-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="4d2fd-169">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="4d2fd-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="4d2fd-170">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="4d2fd-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
