---
title: "Создание внутренней подсистемы балансировки нагрузки Azure с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как создать внутренний балансировщик нагрузки в диспетчере ресурсов с помощью PowerShell."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7bd31ab8f52ec5e81f6966000554be46eaa59396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="1c9c2-103">Создание внутреннего балансировщика нагрузки с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c9c2-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c9c2-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="1c9c2-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="1c9c2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c9c2-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="1c9c2-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="1c9c2-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="1c9c2-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="1c9c2-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="1c9c2-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1c9c2-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="1c9c2-109">В этой статье описывается использование модели развертывания c помощью Resource Manager. Для большинства новых развертываний мы рекомендуем использовать эту модель вместо [классической](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1c9c2-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="1c9c2-110">Ниже описана процедура создания внутреннего балансировщика нагрузки при помощи Azure Resource Manager с PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-110">The following steps explain how to create an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="1c9c2-111">Диспетчер ресурсов Azure позволяет по отдельности настраивать элементы для создания внутренней подсистемы балансировки нагрузки, после чего на их основе создается балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-111">With Azure Resource Manager, the items to create a Internal load balancer are configured individually and then combined to create a load balancer.</span></span>

<span data-ttu-id="1c9c2-112">Чтобы развернуть балансировщик нагрузки, необходимо создать и настроить следующие объекты:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-112">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="1c9c2-113">Настройка внешнего IP-адреса — настройка частного IP-адреса для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-113">Front end IP configuration - will configure the private IP address for incoming network traffic</span></span>
* <span data-ttu-id="1c9c2-114">Внутренний пул адресов — настройка сетевых интерфейсов, которые будут получать трафик с распределенной нагрузкой из внешнего пула IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-114">Backend address pool - will configure the network interfaces which will receive the load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="1c9c2-115">Правила балансировки нагрузки — конфигурация исходного и локального портов для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-115">Load balancing rules - source and local port configuration for the load balancer.</span></span>
* <span data-ttu-id="1c9c2-116">Пробы — настройка проб для проверки состояния работоспособности экземпляров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-116">Probes - configures the health status probe for the Virtual Machine instances.</span></span>
* <span data-ttu-id="1c9c2-117">Входящие правила преобразования сетевых адресов (NAT) — настройка правил порта для прямого доступа к одному из экземпляров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-117">Inbound NAT rules - configures the port rules to directly access one of the Virtual Machine instances.</span></span>

<span data-ttu-id="1c9c2-118">Дополнительные сведения о настройке компонентов балансировщика нагрузки с помощью Azure Resource Manager см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1c9c2-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="1c9c2-119">Далее описана настройка балансировщика нагрузки для двух виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-119">The following steps explain how to configure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-to-use-resource-manager"></a><span data-ttu-id="1c9c2-120">Настройка PowerShell для использования диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="1c9c2-120">Setup PowerShell to use Resource Manager</span></span>

<span data-ttu-id="1c9c2-121">Обязательно установите последнюю рабочую версию модуля Azure для PowerShell и правильно настройте PowerShell для доступа к подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-121">Make sure you have the latest production version of the Azure module for PowerShell, and have PowerShell setup correctly to access your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="1c9c2-122">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="1c9c2-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="1c9c2-123">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="1c9c2-123">Step 2</span></span>

<span data-ttu-id="1c9c2-124">Проверка подписок для учетной записи</span><span class="sxs-lookup"><span data-stu-id="1c9c2-124">Check the subscriptions for the account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="1c9c2-125">Вам будет предложено пройти проверку подлинности с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-125">You will be prompted to Authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="1c9c2-126">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-126">Step 3</span></span>

<span data-ttu-id="1c9c2-127">Выберите, какие подписки Azure будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-127">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="1c9c2-128">Создание группы ресурсов для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="1c9c2-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="1c9c2-129">Создайте группу ресурсов (пропустите этот шаг, если вы используете существующую группу).</span><span class="sxs-lookup"><span data-stu-id="1c9c2-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="1c9c2-130">Диспетчер ресурсов Azure требует, чтобы все группы ресурсов указывали расположение.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="1c9c2-131">Оно используется по умолчанию для ресурсов в этой группе.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="1c9c2-132">Убедитесь, что во всех командах создания подсистемы балансировки нагрузки используется одна группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-132">Make sure all commands to create a load balancer will use the same resource group.</span></span>

<span data-ttu-id="1c9c2-133">В приведенном выше примере мы создали группу ресурсов под названием «NRP RG» с расположением «Запад США».</span><span class="sxs-lookup"><span data-stu-id="1c9c2-133">In the example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="1c9c2-134">Создание виртуальной сети и общедоступного IP-адреса для пула IP-адресов клиентской части</span><span class="sxs-lookup"><span data-stu-id="1c9c2-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="1c9c2-135">Создание подсети для виртуальной сети и присвоение ее переменной $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="1c9c2-135">Creates a subnet for the virtual network and assigns to variable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="1c9c2-136">Создайте виртуальную сеть:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="1c9c2-137">Создание виртуальной сети, добавление подсети lb-subnet-be к виртуальной сети NRPVNet и присвоение ее переменной $vnet</span><span class="sxs-lookup"><span data-stu-id="1c9c2-137">Creates the virtual network and adds the subnet lb-subnet-be to the virtual network NRPVNet and assigns to variable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="1c9c2-138">Создание пула IP-адресов клиентской части и пула адресов серверной части</span><span class="sxs-lookup"><span data-stu-id="1c9c2-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="1c9c2-139">Настройка пула IP-адресов клиентской части для входящего сетевого трафика подсистемы балансировки нагрузки и пула адресов серверной части для получения распределенного сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-139">Setting up a front end IP pool for the incoming load balancer network traffic and backend address pool to receive the load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="1c9c2-140">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="1c9c2-140">Step 1</span></span>

<span data-ttu-id="1c9c2-141">Создание внешнего пула IP-адресов с помощью частного IP-адреса 10.0.2.5 для подсети 10.0.2.0/24, которая будет служить конечной точкой для входящего сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-141">Create a front end IP pool using the private IP address 10.0.2.5 for the subnet 10.0.2.0/24 which will be the incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="1c9c2-142">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="1c9c2-142">Step 2</span></span>

<span data-ttu-id="1c9c2-143">Настройте пул адресов серверной части для приема входящего трафика из пула IP-адресов клиентской части:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-143">Set up a back end address pool used to receive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="1c9c2-144">Создание правил балансировки нагрузки, правил преобразования сетевых адресов, пробы и подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="1c9c2-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="1c9c2-145">После создания пула IP-адресов клиентской части и пула адресов серверной части необходимо создать правила, которые будут принадлежать ресурсу подсистемы балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-145">After creating the front end IP pool and the backend address pool, you will need to create the rules which will belong to the load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="1c9c2-146">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="1c9c2-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="1c9c2-147">В вышеприведенном примере создаются следующие элементы.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-147">The example above is creating the following items:</span></span>

* <span data-ttu-id="1c9c2-148">Входящее правило NAT для направления трафика с порта 3441 на порт 3389.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-148">NAT rule which all incoming traffic to port 3441 will go to port 3389.</span></span>
* <span data-ttu-id="1c9c2-149">Второе входящее правило NAT для направления трафика с порта 3442 на порт 3389.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-149">a second NAT rule which all incoming traffic to port 3442 will go to port 3389.</span></span>
* <span data-ttu-id="1c9c2-150">Правило балансировки нагрузки, согласно которому весь трафик, поступающий на общедоступный порт 80, будет распределяться на локальный порт 80 в пуле адресов серверной части.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-150">a load balancer rule which will load balance all incoming traffic on public port 80 to local port 80 in the back end address pool.</span></span>
* <span data-ttu-id="1c9c2-151">Правило пробы, согласно которому будет проверяться доступность пути «HealthProbe.aspx».</span><span class="sxs-lookup"><span data-stu-id="1c9c2-151">a probe rule which will check the health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="1c9c2-152">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="1c9c2-152">Step 2</span></span>

<span data-ttu-id="1c9c2-153">Создайте подсистему балансировки нагрузки, объединив все объекты (правила преобразования сетевых адресов, правила балансировки нагрузки, настройки проб):</span><span class="sxs-lookup"><span data-stu-id="1c9c2-153">Create the load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="1c9c2-154">Создание сетевых интерфейсов</span><span class="sxs-lookup"><span data-stu-id="1c9c2-154">Create network interfaces</span></span>

<span data-ttu-id="1c9c2-155">После создания внутренней подсистемы балансировки нагрузки необходимо определить сетевые интерфейсы, к которым будут применяться правила NAT и пробы и которые будут получать сетевой трафик с распределенной нагрузкой.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-155">After creating the internal load balancer, you need define which network interfaces will be receiving the incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="1c9c2-156">В этом случае сетевой интерфейс настраивается отдельно и может быть назначен виртуальной машине не сразу.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-156">The network interface in this case is configured individually and can be assigned to a virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="1c9c2-157">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="1c9c2-157">Step 1</span></span>

<span data-ttu-id="1c9c2-158">Определите ресурс виртуальной сети и подсети для создания сетевых интерфейсов:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-158">Get the resource virtual network and subnet to create network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="1c9c2-159">На этом шаге мы создаем сетевой интерфейс, которой будет принадлежать пулу серверной части подсистемы балансировки нагрузки, а затем назначаем первое правило NAT протоколу удаленного рабочего стола для данного сетевого интерфейса:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-159">This step creates a network interface which will belong to the load balancer back end pool and associate the first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="1c9c2-160">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="1c9c2-160">Step 2</span></span>

<span data-ttu-id="1c9c2-161">Создайте второй сетевой интерфейс с названием «LB-Nic2-BE»:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="1c9c2-162">На этом шаге мы создаем второй сетевой интерфейс, присваиваем его тому же пулу серверной части подсистемы балансировки нагрузки и связываем второе правило NAT с протоколом удаленного рабочего стола:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-162">This step creates a second network interface, assigning to the same load balancer back end pool and associating the second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="1c9c2-163">Результат будет аналогичным следующему:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-163">The end result will show the following:</span></span>

    $backendnic1

<span data-ttu-id="1c9c2-164">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-164">Expected output:</span></span>

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a><span data-ttu-id="1c9c2-165">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-165">Step 3</span></span>

<span data-ttu-id="1c9c2-166">Используйте команду Add-AzureRmVMNetworkInterface, чтобы присвоить сетевую карту виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-166">Use the command Add-AzureRmVMNetworkInterface to assign the NIC to a virtual Machine.</span></span>

<span data-ttu-id="1c9c2-167">Пошаговые инструкции по созданию виртуальной машины и назначению сетевой карты описаны в статье [Создание виртуальной машины Windows с помощью Resource Manager и PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c9c2-167">You can find the step by step instructions to create a virtual machine and assign to a NIC following the documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface"></a><span data-ttu-id="1c9c2-168">Добавление сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="1c9c2-168">Add the network interface</span></span>

<span data-ttu-id="1c9c2-169">Если виртуальная машина у вас уже есть, добавьте сетевой интерфейс, выполнив описанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="1c9c2-169">If you already have a virtual machine created, you can add the network interface with the following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="1c9c2-170">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="1c9c2-170">Step 1</span></span>

<span data-ttu-id="1c9c2-171">Загрузите ресурс балансировщика нагрузки в переменную (если вы это еще не сделали).</span><span class="sxs-lookup"><span data-stu-id="1c9c2-171">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="1c9c2-172">Имя переменной — $lb. Используйте имена из ресурса балансировщика нагрузки, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-172">The variable used is called $lb and use the same names from the load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="1c9c2-173">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="1c9c2-173">Step 2</span></span>

<span data-ttu-id="1c9c2-174">Загрузите в переменную конфигурацию серверной части.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-174">Load the backend configuration to a variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="1c9c2-175">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-175">Step 3</span></span>

<span data-ttu-id="1c9c2-176">Загрузите в переменную созданный ранее сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-176">Load the already created network interface into a variable.</span></span> <span data-ttu-id="1c9c2-177">Имя переменной — $nic.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-177">the variable name used is $nic.</span></span> <span data-ttu-id="1c9c2-178">Имя сетевого интерфейса совпадает с именем в приведенном выше примере.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-178">The network interface name used is the same from the example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="1c9c2-179">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-179">Step 4</span></span>

<span data-ttu-id="1c9c2-180">Измените конфигурацию серверной части в сетевом интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-180">Change the backend configuration on the network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="1c9c2-181">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="1c9c2-181">Step 5</span></span>

<span data-ttu-id="1c9c2-182">Сохраните объект сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-182">Save the network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="1c9c2-183">После того как сетевой интерфейс будет добавлен в пул серверной части балансировщика нагрузки, он начнет получать сетевой трафик согласно правилам балансировки нагрузки для соответствующего ресурса балансировщика.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-183">After a network interface is added to the load balancer backend pool, it starts receiving network traffic based on the load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="1c9c2-184">Обновление существующего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="1c9c2-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="1c9c2-185">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="1c9c2-185">Step 1</span></span>
<span data-ttu-id="1c9c2-186">Используя балансировщик нагрузки из предыдущего примера, присвойте переменной $slb ссылку на объект балансировщика нагрузки, используя метод Get-AzureRmLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-186">Using the load balancer from the example above, assign load balancer object to variable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="1c9c2-187">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="1c9c2-187">Step 2</span></span>

<span data-ttu-id="1c9c2-188">В следующем примере вы добавите новое входящее правило NAT для порта 81 на клиентской части и порта 8181 на серверной части, которое будет применяться к пулу существующего балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-188">In the following example, you will add a new Inbound NAT rule using port 81 in the front end and port 8181 for the back end pool to an existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="1c9c2-189">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-189">Step 3</span></span>

<span data-ttu-id="1c9c2-190">Сохраните новую конфигурацию, используя командлет Set-AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-190">Save the new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="1c9c2-191">Удалите балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-191">Remove a load balancer</span></span>

<span data-ttu-id="1c9c2-192">Воспользуйтесь командой Remove-AzureRmLoadBalancer, чтобы удалить ранее созданного балансировщика нагрузки с именем NRP-LB в группе ресурсов NRP RG.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-192">Use the command Remove-AzureRmLoadBalancer to delete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="1c9c2-193">Чтобы пропустить подтверждение удаления, можно использовать необязательный ключ -Force.</span><span class="sxs-lookup"><span data-stu-id="1c9c2-193">You can use the optional switch -Force to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c9c2-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c9c2-194">Next steps</span></span>

[<span data-ttu-id="1c9c2-195">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="1c9c2-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="1c9c2-196">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="1c9c2-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
