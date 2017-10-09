---
title: "aaaConfigure всегда на прослушиватели группы доступности — Microsoft Azure | Документы Microsoft"
description: "Настройте прослушиватели группы доступности на модели hello диспетчера ресурсов Azure, используя внутренний балансировщик нагрузки с помощью одного или нескольких IP-адресов."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="f6fea-103">Настройка одного или нескольких прослушивателей групп доступности AlwaysOn в модели Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f6fea-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="f6fea-104">В этой статье вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="f6fea-104">This topic shows how to:</span></span>

* <span data-ttu-id="f6fea-105">создать внутренний балансировщик нагрузки для групп доступности SQL Server с помощью командлетов PowerShell;</span><span class="sxs-lookup"><span data-stu-id="f6fea-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="f6fea-106">Добавление дополнительных IP адресов tooa подсистемы балансировки нагрузки по более чем одной группы доступности.</span><span class="sxs-lookup"><span data-stu-id="f6fea-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="f6fea-107">Прослушиватель группы доступности является имя виртуальной сети, чтобы клиенты могли подключаться toofor доступ к базе данных.</span><span class="sxs-lookup"><span data-stu-id="f6fea-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="f6fea-108">На виртуальных машинах Azure подсистемы балансировки нагрузки содержит hello IP-адрес для прослушивателя hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="f6fea-109">маршруты подсистемы балансировки нагрузки Hello трафик toohello экземпляра SQL Server, который прослушивает порт пробы hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="f6fea-110">Обычно группа доступности использует внутреннюю подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="f6fea-111">В такой системе можно разместить один или несколько IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f6fea-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="f6fea-112">Каждый IP-адрес использует определенный порт пробы.</span><span class="sxs-lookup"><span data-stu-id="f6fea-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="f6fea-113">В этом документе показано, как toocreate toouse PowerShell подсистему балансировки нагрузки или добавьте IP-адреса tooan существующей подсистемы балансировки нагрузки для группы доступности SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f6fea-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="f6fea-114">Здравствуйте, возможность tooassign нескольких IP адресов tooan внутренняя Подсистема балансировки нагрузки — новый tooAzure и доступна только в модели диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f6fea-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="f6fea-115">toocomplete этой задачи необходимо toohave развернуты группы доступности SQL Server на виртуальных машинах Azure в модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f6fea-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="f6fea-116">Обе виртуальные машины SQL Server должны принадлежать toohello одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="f6fea-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="f6fea-117">Можно использовать hello [шаблона Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Создание группы доступности hello в диспетчере ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f6fea-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="f6fea-118">Этот шаблон автоматически создает группу доступности hello, включая hello внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="f6fea-119">При необходимости можно [вручную настроить группу доступности AlwaysOn](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="f6fea-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="f6fea-120">Здесь предполагается, что группы доступности уже настроены.</span><span class="sxs-lookup"><span data-stu-id="f6fea-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="f6fea-121">Связанные разделы включают:</span><span class="sxs-lookup"><span data-stu-id="f6fea-121">Related topics include:</span></span>

* [<span data-ttu-id="f6fea-122">Настройка групп доступности AlwaysOn в виртуальной машине Azure (графический пользовательский интерфейс)</span><span class="sxs-lookup"><span data-stu-id="f6fea-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="f6fea-123">Настройка подключения между виртуальными сетями с помощью Azure Resource Manager и PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6fea-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="f6fea-124">Настройка брандмауэра Windows hello</span><span class="sxs-lookup"><span data-stu-id="f6fea-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="f6fea-125">Настройка доступа к SQL Server tooallow брандмауэра Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="f6fea-126">правила брандмауэра Hello разрешить потребление toohello подключений TCP-порты, экземпляр SQL Server hello и пробы прослушивателя hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="f6fea-127">Дополнительные сведения см. в разделе [Настройка брандмауэра Windows для доступа к ядру СУБД](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="f6fea-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="f6fea-128">Создайте правило входящего подключения для hello порт SQL Server и для порта пробы hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="f6fea-129">Пример сценария. Создание внутреннего балансировщика нагрузки с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6fea-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="f6fea-130">Если вы создали свою группу доступности с hello [шаблона Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello внутренней подсистемы балансировки нагрузки уже был создан.</span><span class="sxs-lookup"><span data-stu-id="f6fea-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="f6fea-131">Hello следующий сценарий PowerShell создает внутренний балансировщик нагрузки, настраивает правила подсистемы балансировки нагрузки hello и задает IP-адрес для hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="f6fea-132">сценарий toorun hello, откройте Windows PowerShell ISE и вставьте скрипт hello в области сценариев hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="f6fea-133">Используйте `Login-AzureRMAccount` toolog в tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6fea-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="f6fea-134">Если у вас несколько подписок Azure, используйте `Select-AzureRmSubscription ` tooset hello подписки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <span data-ttu-id="f6fea-135"><a name="Add-IP"></a>Пример сценария: Добавление IP адрес tooan существующей подсистемы балансировки нагрузки с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6fea-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="f6fea-136">toouse больше, чем к одной группе доступности, добавить дополнительные IP адрес toohello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="f6fea-137">Каждому IP-адресу требуется собственное правило балансировки нагрузки, порт пробы и внешний порт.</span><span class="sxs-lookup"><span data-stu-id="f6fea-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="f6fea-138">Hello переднего плана используется порт hello использование экземпляра SQL Server toohello tooconnect приложениями.</span><span class="sxs-lookup"><span data-stu-id="f6fea-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="f6fea-139">IP-адресов для различных групп доступности можно используйте hello же интерфейсный порт.</span><span class="sxs-lookup"><span data-stu-id="f6fea-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="f6fea-140">Для групп доступности SQL Server для каждого IP-адреса требуется определенный порт пробы.</span><span class="sxs-lookup"><span data-stu-id="f6fea-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="f6fea-141">Например, если один IP-адрес в балансировщике нагрузки использует порт пробы 59999, другие IP-адреса не могут использовать этот порт пробы.</span><span class="sxs-lookup"><span data-stu-id="f6fea-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="f6fea-142">Дополнительные сведения об ограничениях см. в пункте **Частный внешний IP-адрес на балансировщик нагрузки** раздела [Ограничения сети — Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="f6fea-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="f6fea-143">Дополнительные сведения об ограничениях групп доступности см. в разделе [Ограничения (группы доступности)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="f6fea-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="f6fea-144">Hello следующий сценарий добавляет новый IP адрес tooan существующей подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="f6fea-145">Hello ILB использует порт прослушивателя hello hello балансировки интерфейсный порт.</span><span class="sxs-lookup"><span data-stu-id="f6fea-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="f6fea-146">Этот порт может быть hello порт, прослушиваемый SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f6fea-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="f6fea-147">Для экземпляров SQL Server по умолчанию порт hello — 1433.</span><span class="sxs-lookup"><span data-stu-id="f6fea-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="f6fea-148">правила для группы доступности балансировки нагрузки Hello требует плавающий IP-адрес (прямой возврат сервера), порт внутренней hello hello же, как интерфейсный порт hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="f6fea-149">Обновите hello переменные среды.</span><span class="sxs-lookup"><span data-stu-id="f6fea-149">Update hello variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a><span data-ttu-id="f6fea-150">Настройте прослушиватель hello</span><span class="sxs-lookup"><span data-stu-id="f6fea-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="f6fea-151">Задайте порт прослушивателя hello в SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="f6fea-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="f6fea-152">Запустите SQL Server Management Studio и подключитесь toohello первичной реплики.</span><span class="sxs-lookup"><span data-stu-id="f6fea-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="f6fea-153">Перейдите в слишком**высокий уровень доступности AlwaysOn** | **группы доступности** | **прослушиватели группы доступности**.</span><span class="sxs-lookup"><span data-stu-id="f6fea-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="f6fea-154">Теперь вы увидите имя прослушивателя hello, созданный в диспетчере отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="f6fea-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="f6fea-155">Щелкните правой кнопкой мыши имя прослушивателя hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="f6fea-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="f6fea-156">В hello **порт** укажите hello номер порта для прослушивателя группы доступности hello $EndpointPort ранее с помощью hello (по умолчанию hello — 1433), затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f6fea-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="f6fea-157">Подключение toohello теста hello прослушивателя</span><span class="sxs-lookup"><span data-stu-id="f6fea-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="f6fea-158">подключение к tootest hello:</span><span class="sxs-lookup"><span data-stu-id="f6fea-158">tootest hello connection:</span></span>

1. <span data-ttu-id="f6fea-159">Tooa RDP сервера SQL в hello виртуальных сетевых, но не собственные hello реплики.</span><span class="sxs-lookup"><span data-stu-id="f6fea-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="f6fea-160">Это может быть hello другие серверы SQL Server в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="f6fea-161">Используйте **sqlcmd** программа tootest hello соединения.</span><span class="sxs-lookup"><span data-stu-id="f6fea-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="f6fea-162">Например, следующий скрипт hello устанавливает **sqlcmd** toohello первичной подключения через прослушиватель hello с проверкой подлинности Windows:</span><span class="sxs-lookup"><span data-stu-id="f6fea-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="f6fea-163">Если прослушиватель hello не использует порт hello по умолчанию порт (1433), укажите порт hello в строке подключения hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="f6fea-164">Например hello следующие команды sqlcmd подключается tooa прослушивания по порту 1435:</span><span class="sxs-lookup"><span data-stu-id="f6fea-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="f6fea-165">Hello SQLCMD подключения автоматически подключается toowhichever экземпляра SQL Server узлов hello первичной реплики.</span><span class="sxs-lookup"><span data-stu-id="f6fea-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="f6fea-166">Убедитесь, что открыт порт hello, указываемые на брандмауэре hello и серверов SQL.</span><span class="sxs-lookup"><span data-stu-id="f6fea-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="f6fea-167">Оба сервера требуют входящее правило для hello TCP-порт, который можно использовать.</span><span class="sxs-lookup"><span data-stu-id="f6fea-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="f6fea-168">Дополнительные сведения см. в статье [Добавление и изменение правила брандмауэра](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6fea-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="f6fea-169">Рекомендации и ограничения</span><span class="sxs-lookup"><span data-stu-id="f6fea-169">Guidelines and limitations</span></span>
<span data-ttu-id="f6fea-170">Обратите внимание hello следовать рекомендациям прослушивателя группы доступности в Azure с помощью внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="f6fea-171">С внутренней подсистемы балансировки нагрузки, только доступ прослушиватель hello в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f6fea-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="f6fea-172">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="f6fea-172">For more information</span></span>
<span data-ttu-id="f6fea-173">Дополнительные сведения см. в статье [Введение в группы доступности AlwaysOn SQL Server на виртуальных машинах Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="f6fea-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="f6fea-174">Командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6fea-174">PowerShell cmdlets</span></span>
<span data-ttu-id="f6fea-175">Используйте следующие командлеты PowerShell toocreate внутренний балансировщик нагрузки для виртуальных машин Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f6fea-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="f6fea-176">Командлет [New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) создает подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="f6fea-177">Командлет [New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) создает конфигурацию внешних IP-адресов для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="f6fea-178">Командлет [New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) создает конфигурацию правила для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="f6fea-179">Командлет [New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) создает конфигурацию внутреннего пула IP-адресов для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="f6fea-180">Командлет [New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) создает конфигурацию пробы для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f6fea-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="f6fea-181">Командлет [Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) удаляет подсистему балансировки нагрузки из группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f6fea-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
