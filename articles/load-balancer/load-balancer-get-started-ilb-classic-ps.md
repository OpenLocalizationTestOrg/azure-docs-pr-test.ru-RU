---
title: "Создание внутренней подсистемы балансировки нагрузки Azure с помощью классической версии PowerShell | Документация Майкрософт"
description: "Узнайте, как создать внутренний балансировщик нагрузки в классической модели развертывания с помощью PowerShell."
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
ms.openlocfilehash: f701fb3564c62cf8088cc4362a10c5e2c2301ae6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="64630-103">Приступая к созданию внутреннего балансировщика нагрузки (классическая модель) с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="64630-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="64630-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64630-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="64630-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="64630-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="64630-106">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="64630-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="64630-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="64630-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="64630-108">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="64630-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="64630-109">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="64630-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="64630-110">Узнайте, как [выполнить эти действия с помощью модели Resource Manager](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="64630-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="64630-111">Создание набора внутреннего балансировщика нагрузки для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="64630-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="64630-112">Чтобы создать набор внутреннего балансировщика нагрузки и серверы, которые будут направлять на него свой трафик, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="64630-112">To create an internal load balancer set and the servers that will send their traffic to it, you have to do the following:</span></span>

1. <span data-ttu-id="64630-113">Создайте экземпляр внутренней балансировки нагрузки. Он будет служить конечной точкой для входящего трафика, который необходимо распределять по серверам в наборе балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="64630-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="64630-114">Добавьте конечные точки, соответствующие виртуальным машинам, которые будут принимать входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="64630-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="64630-115">Настройте серверы, которые будут отправлять трафик для балансировки нагрузки, таким образом, чтобы они передавали трафик на виртуальный IP-адрес экземпляра внутренней балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="64630-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="64630-116">Шаг 1. Создание экземпляра внутренней балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="64630-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="64630-117">Для существующей облачной службы или облачной службы, развернутой в региональной виртуальной сети, можно создать экземпляр внутренней балансировки нагрузки с помощью следующих команд Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="64630-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with the following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of the subnet within your virtual network>"
$IP="<The IPv4 address to use on the subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="64630-118">Обратите внимание, что здесь командлет [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell использует набор параметров DefaultProbe.</span><span class="sxs-lookup"><span data-stu-id="64630-118">Note that this use of the [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses the DefaultProbe parameter set.</span></span> <span data-ttu-id="64630-119">Дополнительную информацию о дополнительных наборах параметров см. в документации [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="64630-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-to-the-internal-load-balancing-instance"></a><span data-ttu-id="64630-120">Шаг 2: Добавление конечных точек в экземпляр внутренней балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="64630-120">Step 2: Add endpoints to the Internal Load Balancing instance</span></span>

<span data-ttu-id="64630-121">Пример:</span><span class="sxs-lookup"><span data-stu-id="64630-121">Here is an example:</span></span>

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

### <a name="step-3-configure-your-servers-to-send-their-traffic-to-the-new-internal-load-balancing-endpoint"></a><span data-ttu-id="64630-122">Шаг 3. Настройка серверов для отправки трафика на новую конечную точку внутренней балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="64630-122">Step 3: Configure your servers to send their traffic to the new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="64630-123">На серверах, трафик которых будет перераспределяться, необходимо настроить использование нового виртуального IP-адреса экземпляра внутренней балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="64630-123">You have to  configure the servers whose traffic is going to be load balanced to use the new IP address (the VIP) of the Internal Load Balancing instance.</span></span> <span data-ttu-id="64630-124">Этот адрес прослушивается экземпляром внутренней балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="64630-124">This is the address on which the Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="64630-125">В большинстве случаев достаточно просто добавить или изменить запись DNS для виртуального IP-адреса экземпляра внутренней балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="64630-125">In most cases, you need to just add or modify a DNS record for the VIP of the Internal Load Balancing instance.</span></span>

<span data-ttu-id="64630-126">Если во время создания экземпляра внутренней балансировки нагрузки вы указали IP-адрес, то виртуальный IP-адрес у вас уже есть.</span><span class="sxs-lookup"><span data-stu-id="64630-126">If you specified the IP address during the creation of the Internal Load Balancing instance, you already have the VIP.</span></span> <span data-ttu-id="64630-127">В противном случае его можно получить с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="64630-127">Otherwise, you can see the VIP from the following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="64630-128">Чтобы использовать эти команды, заполните значения и удалите символы < и >.</span><span class="sxs-lookup"><span data-stu-id="64630-128">To use these commands, fill in the values and remove the < and >.</span></span> <span data-ttu-id="64630-129">Пример:</span><span class="sxs-lookup"><span data-stu-id="64630-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="64630-130">Обратите внимание на IP-адрес в результатах выполнения команды Get-AzureInternalLoadBalancer и внесите необходимые изменения в настройки серверов или записи DNS, чтобы обеспечить отправку трафика на виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="64630-130">From the display of the Get-AzureInternalLoadBalancer command, note the IP address and make the necessary changes to your servers or DNS records to ensure that traffic gets sent to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="64630-131">Для различных сценариев администрирования платформа Microsoft Azure использует статические общедоступные маршрутизируемые IPv4-адреса.</span><span class="sxs-lookup"><span data-stu-id="64630-131">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="64630-132">IP-адрес — 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="64630-132">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="64630-133">Не блокируйте этот IP-адрес брандмауэрами, поскольку это может привести к непредвиденному поведению.</span><span class="sxs-lookup"><span data-stu-id="64630-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="64630-134">Во внутренней подсистеме балансировки нагрузки Azure этот IP-адрес используется зондами мониторинга для определения состояния виртуальных машин в наборе балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="64630-134">With respect to Azure Internal Load Balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="64630-135">Если группа безопасности сети используется для ограничения трафика, поступающего на виртуальные машины Azure во внутреннем наборе балансировки нагрузки, или если она применяется к подсети виртуальной сети, убедитесь, что правила сетевой безопасности разрешают поступление сетевого трафика с адреса 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="64630-135">If a Network Security Group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a Virtual Network Subnet, ensure that a Network Security Rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="64630-136">Пример внутренней балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="64630-136">Example of internal load balancing</span></span>

<span data-ttu-id="64630-137">Подробное описание создания набора балансировки нагрузки для двух примеров конфигурации см. в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="64630-137">To step you through the end-to end process of creating a load-balanced set for two example configurations, see the following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="64630-138">Многоуровневое приложение для Интернета</span><span class="sxs-lookup"><span data-stu-id="64630-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="64630-139">Вы хотите предоставить службу базы данных с балансировкой нагрузки для набора веб-серверов с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="64630-139">You want to provide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="64630-140">Оба набора серверов размещены в одной облачной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="64630-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="64630-141">Трафик веб-серверов для TCP-порта 1433 необходимо распределить среди двух виртуальных машин на уровне базы данных.</span><span class="sxs-lookup"><span data-stu-id="64630-141">Web server traffic to TCP port 1433 must be distributed among two virtual machines in the database tier.</span></span> <span data-ttu-id="64630-142">На рис. 1 показана эта конфигурация.</span><span class="sxs-lookup"><span data-stu-id="64630-142">Figure 1 shows the configuration.</span></span>

![Внутренний набор балансировки нагрузки для уровня базы данных](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="64630-144">Конфигурация состоит из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="64630-144">The configuration consists of the following:</span></span>

* <span data-ttu-id="64630-145">Существующая облачная служба, в которой размещены виртуальные машины, называется mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="64630-145">The existing cloud service hosting the virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="64630-146">Два существующих сервера базы данных называются DB1 и DB2.</span><span class="sxs-lookup"><span data-stu-id="64630-146">The two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="64630-147">Веб-серверы на уровне Интернета подключаются к серверам базы данных на уровне базы данных, используя частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="64630-147">Web servers in the web tier connect to the database servers in the database tier by using the private IP address.</span></span> <span data-ttu-id="64630-148">Другой вариант — использовать собственный DNS-сервер для виртуальной сети и вручную зарегистрировать запись A для набора внутреннего балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="64630-148">Another option is to use your own DNS for the virtual network and manually register an A record for the internal load balancer set.</span></span>

<span data-ttu-id="64630-149">Следующие команды позволяют настроить новый экземпляр внутренней балансировки нагрузки с именем **ILBset** и добавить конечные точки для виртуальных машин, соответствующие двум серверам базы данных:</span><span class="sxs-lookup"><span data-stu-id="64630-149">The following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints to the virtual machines corresponding to the two database servers:</span></span>

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

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="64630-150">Удаление конфигурации внутренней балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="64630-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="64630-151">Чтобы удалить виртуальную машину как конечную точку из экземпляра внутреннего балансировщика нагрузки, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="64630-151">To remove a virtual machine as an endpoint from an internal load balancer instance, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of the VM>"
$epname="<Name of the endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="64630-152">Чтобы использовать эти команды, заполните значения и удалите символы < и >.</span><span class="sxs-lookup"><span data-stu-id="64630-152">To use these commands, fill in the values, removing the < and >.</span></span>

<span data-ttu-id="64630-153">Пример:</span><span class="sxs-lookup"><span data-stu-id="64630-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="64630-154">Чтобы удалить экземпляр внутреннего балансировщика нагрузки из облачной службы, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="64630-154">To remove an internal load balancer instance from a cloud service, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="64630-155">Чтобы использовать эти команды, заполните значения и удалите символы < и >.</span><span class="sxs-lookup"><span data-stu-id="64630-155">To use these commands, fill in the value and remove the < and >.</span></span>

<span data-ttu-id="64630-156">Пример:</span><span class="sxs-lookup"><span data-stu-id="64630-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="64630-157">Дополнительная информация о командлетах для внутреннего балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="64630-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="64630-158">Чтобы получить дополнительную информацию о командлетах внутренней балансировки нагрузки, выполните следующие команды в командной строке Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="64630-158">To obtain additional information about Internal Load Balancing cmdlets, run the following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="64630-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64630-159">Next steps</span></span>

[<span data-ttu-id="64630-160">Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу</span><span class="sxs-lookup"><span data-stu-id="64630-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="64630-161">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="64630-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

