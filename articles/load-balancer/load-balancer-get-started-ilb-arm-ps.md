---
title: "aaaCreate Azure внутренним загрузить балансировки - PowerShell | Документы Microsoft"
description: "Узнайте, как с помощью PowerShell в диспетчере ресурсов подсистемы балансировки нагрузки, toocreate во внутренний"
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
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="8c131-103">Создание внутреннего балансировщика нагрузки с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c131-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c131-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="8c131-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="8c131-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c131-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="8c131-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8c131-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="8c131-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="8c131-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8c131-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8c131-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8c131-109">В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8c131-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="8c131-110">Hello следующие шаги поясняют, как с помощью диспетчера ресурсов Azure с помощью PowerShell подсистемы балансировки нагрузки, toocreate во внутренней.</span><span class="sxs-lookup"><span data-stu-id="8c131-110">hello following steps explain how toocreate an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="8c131-111">С помощью диспетчера ресурсов Azure toocreate элементы hello внутренний балансировщик настраиваются отдельно, а затем объединяются toocreate подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c131-111">With Azure Resource Manager, hello items toocreate a Internal load balancer are configured individually and then combined toocreate a load balancer.</span></span>

<span data-ttu-id="8c131-112">Требуется toocreate и настроить hello следующие объекты toodeploy подсистемы балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="8c131-112">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="8c131-113">Внешняя конечного IP-конфигурации — настроит hello частный IP-адрес для входящего сетевого трафика</span><span class="sxs-lookup"><span data-stu-id="8c131-113">Front end IP configuration - will configure hello private IP address for incoming network traffic</span></span>
* <span data-ttu-id="8c131-114">Серверный пул адресов - настроит hello сетевых интерфейсов, которые получат трафик с балансировкой нагрузки hello из пула IP-адресов внешнего интерфейса</span><span class="sxs-lookup"><span data-stu-id="8c131-114">Backend address pool - will configure hello network interfaces which will receive hello load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="8c131-115">Правила балансировки нагрузки - источника и конфигурацию локального порта для hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c131-115">Load balancing rules - source and local port configuration for hello load balancer.</span></span>
* <span data-ttu-id="8c131-116">Проверяет - настраивает модуль проверки состояния работоспособности hello для экземпляров виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="8c131-116">Probes - configures hello health status probe for hello Virtual Machine instances.</span></span>
* <span data-ttu-id="8c131-117">Правила NAT для входящих подключений - настраивает hello правила порта toodirectly доступа одного из экземпляров виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="8c131-117">Inbound NAT rules - configures hello port rules toodirectly access one of hello Virtual Machine instances.</span></span>

<span data-ttu-id="8c131-118">Дополнительные сведения о настройке компонентов балансировщика нагрузки с помощью Azure Resource Manager см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8c131-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="8c131-119">Hello следующие шаги поясняют, как tooconfigure балансировки нагрузки между двумя виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="8c131-119">hello following steps explain how tooconfigure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-toouse-resource-manager"></a><span data-ttu-id="8c131-120">Toouse установки PowerShell диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="8c131-120">Setup PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="8c131-121">Убедитесь, что имеется hello последнюю рабочей версии hello модуль Azure для PowerShell и приняты установки правильно tooaccess подписки Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c131-121">Make sure you have hello latest production version of hello Azure module for PowerShell, and have PowerShell setup correctly tooaccess your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c131-122">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="8c131-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="8c131-123">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="8c131-123">Step 2</span></span>

<span data-ttu-id="8c131-124">Проверьте hello подписки для учетной записи hello</span><span class="sxs-lookup"><span data-stu-id="8c131-124">Check hello subscriptions for hello account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="8c131-125">Запрос tooAuthenticate можно с помощью учетных данных.</span><span class="sxs-lookup"><span data-stu-id="8c131-125">You will be prompted tooAuthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="8c131-126">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="8c131-126">Step 3</span></span>

<span data-ttu-id="8c131-127">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="8c131-127">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="8c131-128">Создание группы ресурсов для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c131-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="8c131-129">Создайте группу ресурсов (пропустите этот шаг, если вы используете существующую группу).</span><span class="sxs-lookup"><span data-stu-id="8c131-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="8c131-130">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="8c131-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="8c131-131">Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8c131-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="8c131-132">Убедитесь, что все команды, которые будет использовать подсистему балансировки нагрузки toocreate hello же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8c131-132">Make sure all commands toocreate a load balancer will use hello same resource group.</span></span>

<span data-ttu-id="8c131-133">В hello в примере выше мы создали группу ресурсов под названием «NRP RG» и расположение «West US».</span><span class="sxs-lookup"><span data-stu-id="8c131-133">In hello example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="8c131-134">Создание виртуальной сети и общедоступного IP-адреса для пула IP-адресов клиентской части</span><span class="sxs-lookup"><span data-stu-id="8c131-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="8c131-135">Создает подсеть для виртуальной сети hello и назначает toovariable $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="8c131-135">Creates a subnet for hello virtual network and assigns toovariable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="8c131-136">Создайте виртуальную сеть:</span><span class="sxs-lookup"><span data-stu-id="8c131-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="8c131-137">Создает виртуальную сеть hello и добавляет hello подсети toohello быть балансировки нагрузки подсети виртуальной сети NRPVNet и назначает toovariable $vnet</span><span class="sxs-lookup"><span data-stu-id="8c131-137">Creates hello virtual network and adds hello subnet lb-subnet-be toohello virtual network NRPVNet and assigns toovariable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="8c131-138">Создание пула IP-адресов клиентской части и пула адресов серверной части</span><span class="sxs-lookup"><span data-stu-id="8c131-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="8c131-139">Настройка пулу IP-интерфейса для входящих hello загрузить балансировки сетевой трафик и трафик с балансировкой нагрузки внутренний адрес пула tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="8c131-139">Setting up a front end IP pool for hello incoming load balancer network traffic and backend address pool tooreceive hello load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c131-140">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="8c131-140">Step 1</span></span>

<span data-ttu-id="8c131-141">Создайте пул IP-интерфейс, с помощью hello частный IP-адрес 10.0.2.5 для hello подсети 10.0.2.0/24 которого будет конечной точкой входящего сетевого трафика hello.</span><span class="sxs-lookup"><span data-stu-id="8c131-141">Create a front end IP pool using hello private IP address 10.0.2.5 for hello subnet 10.0.2.0/24 which will be hello incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="8c131-142">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="8c131-142">Step 2</span></span>

<span data-ttu-id="8c131-143">Настройте пул адресов серверной части использования tooreceive входящего трафика из пула IP-адресов внешнего интерфейса:</span><span class="sxs-lookup"><span data-stu-id="8c131-143">Set up a back end address pool used tooreceive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="8c131-144">Создание правил балансировки нагрузки, правил преобразования сетевых адресов, пробы и подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c131-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="8c131-145">После создания пула IP-адресов внешнего интерфейса hello и hello серверный пул адресов, вам потребуется toocreate hello правил, которые будут принадлежать ресурс балансировки нагрузки toohello:</span><span class="sxs-lookup"><span data-stu-id="8c131-145">After creating hello front end IP pool and hello backend address pool, you will need toocreate hello rules which will belong toohello load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="8c131-146">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="8c131-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="8c131-147">приведенном выше примере Hello создает hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8c131-147">hello example above is creating hello following items:</span></span>

* <span data-ttu-id="8c131-148">Правило NAT, которое все входящие трафика tooport 3441 перейдет tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="8c131-148">NAT rule which all incoming traffic tooport 3441 will go tooport 3389.</span></span>
* <span data-ttu-id="8c131-149">Второе правило NAT, которой все входящие трафика tooport 3442 перейдет tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="8c131-149">a second NAT rule which all incoming traffic tooport 3442 will go tooport 3389.</span></span>
* <span data-ttu-id="8c131-150">правило подсистемы балансировки нагрузки, которая будет загружать сбалансировать весь входящий трафик на открытый порт 80 toolocal порт 80 в пул адресов серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="8c131-150">a load balancer rule which will load balance all incoming traffic on public port 80 toolocal port 80 in hello back end address pool.</span></span>
* <span data-ttu-id="8c131-151">правило проверки, которое будет проверять состояние работоспособности hello для пути «HealthProbe.aspx»</span><span class="sxs-lookup"><span data-stu-id="8c131-151">a probe rule which will check hello health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="8c131-152">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="8c131-152">Step 2</span></span>

<span data-ttu-id="8c131-153">Создайте балансировки нагрузки hello сложения всех объектов (правил NAT, правила подсистемы балансировки нагрузки, проверки конфигурации):</span><span class="sxs-lookup"><span data-stu-id="8c131-153">Create hello load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="8c131-154">Создание сетевых интерфейсов</span><span class="sxs-lookup"><span data-stu-id="8c131-154">Create network interfaces</span></span>

<span data-ttu-id="8c131-155">После создания hello внутренней подсистемы балансировки нагрузки, необходимо определить, какие сетевые интерфейсы будет получать hello входящих сетевой трафик с балансировкой нагрузки, правила преобразования сетевых адресов и проверки.</span><span class="sxs-lookup"><span data-stu-id="8c131-155">After creating hello internal load balancer, you need define which network interfaces will be receiving hello incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="8c131-156">в этом случае Hello сетевой интерфейс настраивается индивидуально и могут назначаться tooa виртуальной машины позднее.</span><span class="sxs-lookup"><span data-stu-id="8c131-156">hello network interface in this case is configured individually and can be assigned tooa virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c131-157">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="8c131-157">Step 1</span></span>

<span data-ttu-id="8c131-158">Получите ресурс hello виртуальной сети и подсети toocreate сетевых интерфейсов:</span><span class="sxs-lookup"><span data-stu-id="8c131-158">Get hello resource virtual network and subnet toocreate network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="8c131-159">На этом шаге создается сетевого интерфейса, которой будет принадлежать пула серверной части подсистемы балансировки нагрузки toohello и свяжите hello первого правила NAT для протокола удаленного рабочего СТОЛА для данного сетевого интерфейса:</span><span class="sxs-lookup"><span data-stu-id="8c131-159">This step creates a network interface which will belong toohello load balancer back end pool and associate hello first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="8c131-160">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="8c131-160">Step 2</span></span>

<span data-ttu-id="8c131-161">Создайте второй сетевой интерфейс с названием «LB-Nic2-BE»:</span><span class="sxs-lookup"><span data-stu-id="8c131-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="8c131-162">На этом шаге создается второго сетевого интерфейса, назначение toohello же балансировки нагрузки обратно завершить пула и связывание hello второе правило NAT для протокола удаленного рабочего СТОЛА:</span><span class="sxs-lookup"><span data-stu-id="8c131-162">This step creates a second network interface, assigning toohello same load balancer back end pool and associating hello second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="8c131-163">конечным результатом Hello отобразится hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8c131-163">hello end result will show hello following:</span></span>

    $backendnic1

<span data-ttu-id="8c131-164">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8c131-164">Expected output:</span></span>

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



### <a name="step-3"></a><span data-ttu-id="8c131-165">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="8c131-165">Step 3</span></span>

<span data-ttu-id="8c131-166">Используйте hello команду Add-AzureRmVMNetworkInterface tooassign hello Сетевых tooa виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="8c131-166">Use hello command Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtual Machine.</span></span>

<span data-ttu-id="8c131-167">Здравствуйте, пошаговые процедуры toocreate виртуальной машины и назначить tooa сетевого Адаптера можно найти следующие документации hello: [создать ВМ Azure с помощью PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c131-167">You can find hello step by step instructions toocreate a virtual machine and assign tooa NIC following hello documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface"></a><span data-ttu-id="8c131-168">Добавьте сетевой интерфейс hello</span><span class="sxs-lookup"><span data-stu-id="8c131-168">Add hello network interface</span></span>

<span data-ttu-id="8c131-169">Если уже имеется созданная виртуальная машина, вы можете добавить hello сетевого интерфейса с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="8c131-169">If you already have a virtual machine created, you can add hello network interface with hello following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="8c131-170">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="8c131-170">Step 1</span></span>

<span data-ttu-id="8c131-171">Загрузка ресурсов подсистемы балансировки нагрузки hello в переменной (Если вы еще не сделали, еще).</span><span class="sxs-lookup"><span data-stu-id="8c131-171">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="8c131-172">Hello переменная, используемая является именем $lb и приветствия используйте одинаковые имена из ресурса подсистемы балансировки нагрузки hello созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="8c131-172">hello variable used is called $lb and use hello same names from hello load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="8c131-173">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="8c131-173">Step 2</span></span>

<span data-ttu-id="8c131-174">Загрузка конфигурации tooa hello серверной переменной.</span><span class="sxs-lookup"><span data-stu-id="8c131-174">Load hello backend configuration tooa variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="8c131-175">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="8c131-175">Step 3</span></span>

<span data-ttu-id="8c131-176">Загрузка сетевого интерфейса hello уже созданы в переменной.</span><span class="sxs-lookup"><span data-stu-id="8c131-176">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="8c131-177">использовать имя переменной Hello — $ сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="8c131-177">hello variable name used is $nic.</span></span> <span data-ttu-id="8c131-178">в приведенном выше примере hello Hello используется имя сетевого интерфейса является hello таким же.</span><span class="sxs-lookup"><span data-stu-id="8c131-178">hello network interface name used is hello same from hello example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="8c131-179">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="8c131-179">Step 4</span></span>

<span data-ttu-id="8c131-180">Измените конфигурацию серверной части hello в сетевом интерфейсе hello.</span><span class="sxs-lookup"><span data-stu-id="8c131-180">Change hello backend configuration on hello network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="8c131-181">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="8c131-181">Step 5</span></span>

<span data-ttu-id="8c131-182">Сохраните объект сетевого интерфейса hello.</span><span class="sxs-lookup"><span data-stu-id="8c131-182">Save hello network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="8c131-183">После добавления сетевого интерфейса внутренний пул подсистемы балансировки нагрузки toohello запуске получения сетевого трафика на основе правила для этого ресурса подсистемы балансировки нагрузки подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="8c131-183">After a network interface is added toohello load balancer backend pool, it starts receiving network traffic based on hello load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="8c131-184">Обновление существующего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c131-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="8c131-185">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="8c131-185">Step 1</span></span>
<span data-ttu-id="8c131-186">С помощью подсистемы балансировки нагрузки hello в приведенном выше примере hello, назначьте toovariable объект подсистемы балансировки нагрузки с помощью Get-AzureRmLoadBalancer $slb</span><span class="sxs-lookup"><span data-stu-id="8c131-186">Using hello load balancer from hello example above, assign load balancer object toovariable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="8c131-187">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="8c131-187">Step 2</span></span>

<span data-ttu-id="8c131-188">В следующем примере hello будет добавить новое правило NAT для входящего трафика через порт 81 в hello переднего плана и порт 8181 резервному hello окончания пула tooan существующей подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c131-188">In hello following example, you will add a new Inbound NAT rule using port 81 in hello front end and port 8181 for hello back end pool tooan existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="8c131-189">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="8c131-189">Step 3</span></span>

<span data-ttu-id="8c131-190">Сохранить hello новую конфигурацию с помощью набора AzureLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="8c131-190">Save hello new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="8c131-191">Удалите балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8c131-191">Remove a load balancer</span></span>

<span data-ttu-id="8c131-192">Используйте hello команду Remove-AzureRmLoadBalancer toodelete подсистемы балансировки нагрузки начатую с именем «NRP-балансировки Нагрузки» в группе ресурсов называется «NRP RG»</span><span class="sxs-lookup"><span data-stu-id="8c131-192">Use hello command Remove-AzureRmLoadBalancer toodelete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="8c131-193">Можно использовать необязательный hello переключения - Force tooavoid hello строки для удаления.</span><span class="sxs-lookup"><span data-stu-id="8c131-193">You can use hello optional switch -Force tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c131-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c131-194">Next steps</span></span>

[<span data-ttu-id="8c131-195">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c131-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8c131-196">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="8c131-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
