---
title: "aaaCreate Azure внутренним загрузить балансировки - классический PowerShell | Документы Microsoft"
description: "Узнайте, как с помощью PowerShell в hello классической модели развертывания подсистемы балансировки нагрузки, toocreate во внутренний"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="ae5fc-103">Приступая к созданию внутреннего балансировщика нагрузки (классическая модель) с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae5fc-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae5fc-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae5fc-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="ae5fc-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="ae5fc-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="ae5fc-106">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="ae5fc-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="ae5fc-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ae5fc-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ae5fc-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="ae5fc-109">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ae5fc-110">Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ae5fc-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="ae5fc-111">Создание набора внутреннего балансировщика нагрузки для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="ae5fc-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="ae5fc-112">toocreate внутренний балансировщик нагрузки задать и hello серверов, которые будут отправлять их tooit трафик, у вас есть toodo hello следующее:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="ae5fc-113">Создайте экземпляр внутренней балансировки нагрузки, конечную точку hello входящего трафика toobe Балансировка нагрузки для серверов hello набора балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="ae5fc-114">Добавьте конечные точки, соответствующие toohello виртуальных машин, которые будут принимать входящий трафик hello.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="ae5fc-115">Настройка серверов hello, которые будут отправлять что hello трафика toobe с балансировкой нагрузки toosend их трафика toohello виртуальных IP-адресов (VIP) адрес экземпляра hello внутренней балансировки.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="ae5fc-116">Шаг 1. Создание экземпляра внутренней балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="ae5fc-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="ae5fc-117">Для существующей облачной службе или облачной службы, развернутой в региональной виртуальной сети можно создать экземпляр внутренней балансировки нагрузки с помощью следующих команд Windows PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="ae5fc-118">Обратите внимание, что такое использование hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) командлета Windows PowerShell использует набор параметров DefaultProbe hello.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="ae5fc-119">Дополнительную информацию о дополнительных наборах параметров см. в документации [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae5fc-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="ae5fc-120">Шаг 2: Добавление экземпляра внутренняя Балансировка нагрузки toohello конечных точек</span><span class="sxs-lookup"><span data-stu-id="ae5fc-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="ae5fc-121">Пример:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="ae5fc-122">Шаг 3: Настройка вашей toosend серверы их трафика toohello новой внутренняя Балансировка нагрузки конечной точки</span><span class="sxs-lookup"><span data-stu-id="ae5fc-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="ae5fc-123">Иметь слишком настроить серверы hello, трафик которых будет toobe балансировки нагрузки toouse hello новый IP-адрес (hello виртуальных IP-адресов) hello экземпляр внутренней балансировки.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="ae5fc-124">Это адрес hello какие hello внутренняя Балансировка нагрузки прослушивается экземпляром.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="ae5fc-125">В большинстве случаев требуется toojust добавить или изменить запись DNS для hello виртуального IP-адреса экземпляра внутренняя Балансировка нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="ae5fc-126">Если вы указали hello IP-адрес во время создания экземпляра внутренняя Балансировка нагрузки hello hello, уже имеется hello виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="ae5fc-127">В противном случае вы можете увидеть VIP hello из hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="ae5fc-128">toouse эти команды, заполните значения hello и remove hello < и >.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="ae5fc-129">Пример:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="ae5fc-130">Из отображения hello hello команды Get-AzureInternalLoadBalancer Обратите внимание, hello IP-адрес и сделайте hello необходимые изменения tooyour серверы или tooensure записей DNS, трафик отправляется toohello виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="ae5fc-131">Hello платформы Microsoft Azure использует статические публично маршрутизируемый IPv4-адрес для различных сценариев администрирования.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="ae5fc-132">Hello IP-адрес — 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="ae5fc-133">Не блокируйте этот IP-адрес брандмауэрами, поскольку это может привести к непредвиденному поведению.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="ae5fc-134">С учетом tooAzure внутренней балансировки отслеживая проб из состояние работоспособности hello toodetermine подсистемы балансировки нагрузки hello для виртуальных машин в набор балансировки нагрузки используется этот IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="ae5fc-135">Если группа безопасности сети является используется toorestrict трафика tooAzure виртуальные машины в наборе внутренне балансировки нагрузки или примененных tooa подсеть виртуальной сети, убедитесь, что правило сетевой безопасности добавлен tooallow трафика из 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="ae5fc-136">Пример внутренней балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="ae5fc-136">Example of internal load balancing</span></span>

<span data-ttu-id="ae5fc-137">toostep hello окончания tooend процессе создания набор балансировки нагрузки для двух примеров конфигурации появится hello следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="ae5fc-138">Многоуровневое приложение для Интернета</span><span class="sxs-lookup"><span data-stu-id="ae5fc-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="ae5fc-139">Вы хотите tooprovide базы данных службы балансировки нагрузки для набора веб-серверы с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="ae5fc-140">Оба набора серверов размещены в одной облачной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="ae5fc-141">TooTCP трафика порт 1433 для веб-сервера необходимо распределить среди двух виртуальных машин на уровне базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="ae5fc-142">На рисунке 1 показана конфигурация hello.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-142">Figure 1 shows hello configuration.</span></span>

![Внутренний набор с балансировкой нагрузки для уровня базы данных hello](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="ae5fc-144">Конфигурация Hello состоит из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="ae5fc-145">Hello существующей облачной службы размещения виртуальных машин hello называется mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="ae5fc-146">Hello два существующего сервера базы данных именуются DB1 и DB2.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="ae5fc-147">Веб-серверов в веб-уровень hello toohello серверы баз данных на уровне базы данных hello подключаться с помощью hello частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="ae5fc-148">Другой вариант является toouse DNS для виртуальной сети hello и вручную зарегистрировать записи для набора балансировки нагрузки внутренней hello.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="ae5fc-149">Hello следующие команды настраивают новый экземпляр внутренняя Балансировка нагрузки с именем **ILBset** и добавьте виртуальные машины toohello конечные точки, соответствующие toohello двух серверов баз данных:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="ae5fc-150">Удаление конфигурации внутренней балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="ae5fc-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="ae5fc-151">tooremove виртуальную машину как конечную точку из экземпляра балансировщик внутренней нагрузки hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="ae5fc-152">toouse эти команды, заполните значения hello и удалите hello < и >.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="ae5fc-153">Пример:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="ae5fc-154">tooremove экземпляра балансировки внутренней нагрузки из облачной службы, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="ae5fc-155">toouse эти команды, заполните значения hello и удалите hello < и >.</span><span class="sxs-lookup"><span data-stu-id="ae5fc-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="ae5fc-156">Пример:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="ae5fc-157">Дополнительная информация о командлетах для внутреннего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="ae5fc-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="ae5fc-158">tooobtain Дополнительные сведения о командлетах, внутренняя Балансировка нагрузки, запустите следующие команды в командной строке Windows PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="ae5fc-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="ae5fc-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ae5fc-159">Next steps</span></span>

[<span data-ttu-id="ae5fc-160">Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу</span><span class="sxs-lookup"><span data-stu-id="ae5fc-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="ae5fc-161">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="ae5fc-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

