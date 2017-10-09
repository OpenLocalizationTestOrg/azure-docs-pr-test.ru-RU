---
title: "aaaConfigure ILB прослушивателя для групп доступности AlwaysOn в Azure | Документы Microsoft"
description: "В этом учебнике используются ресурсы, созданные с помощью hello классической модели развертывания, и создает всегда на прослушиватель группы доступности в Azure, которая использует внутренний балансировщик нагрузки."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="9c1dd-103">Настройка прослушивателя внутреннего балансировщика нагрузки для групп доступности AlwaysOn в Azure</span><span class="sxs-lookup"><span data-stu-id="9c1dd-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c1dd-104">Внутренний прослушиватель</span><span class="sxs-lookup"><span data-stu-id="9c1dd-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="9c1dd-105">Внешний прослушиватель</span><span class="sxs-lookup"><span data-stu-id="9c1dd-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="9c1dd-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="9c1dd-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c1dd-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9c1dd-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9c1dd-108">В этой статье описывается использование hello hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="9c1dd-109">Корпорация Майкрософт рекомендует наиболее новые развертывания для использования модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="9c1dd-110">tooconfigure прослушивателя для группы доступности Always On, в модели hello диспетчера ресурсов, в разделе [настройки балансировки нагрузки для группы доступности AlwaysOn в Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="9c1dd-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="9c1dd-111">В группе доступности могут быть реплики, доступные только локально или только в Azure. В гибридных конфигурациях возможны оба способа доступа одновременно.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="9c1dd-112">Реплики в Azure может находиться в пределах hello же регионе или в нескольких регионах, использующие несколько виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="9c1dd-113">Hello процедуры, описанные в этой статье предполагается, что вы уже [группа доступности настроена](../classic/portal-sql-alwayson-availability-groups.md) , но еще не настроен прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="9c1dd-114">Рекомендации и ограничения для внутренних прослушивателей</span><span class="sxs-lookup"><span data-stu-id="9c1dd-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="9c1dd-115">Hello внутренней подсистемы балансировки нагрузки (ILB) с прослушивателем группы доступности в Azure используется тема toohello рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="9c1dd-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="9c1dd-116">прослушиватель группы доступности Hello поддерживается на Windows Server 2008 R2, Windows Server 2012 и Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="9c1dd-117">Только один прослушиватель группы доступности внутренней поддерживается для каждой облачной службы, так как прослушиватель hello настроен toohello ILB, а имеется только один ILB для каждой облачной службы.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="9c1dd-118">Однако это возможно toocreate несколько внешних прослушивателей.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="9c1dd-119">Дополнительные сведения см. в статье [Настройка внешнего прослушивателя для групп доступности AlwaysOn в Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="9c1dd-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="9c1dd-120">Определить доступность hello hello прослушивателя</span><span class="sxs-lookup"><span data-stu-id="9c1dd-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="9c1dd-121">В этой статье рассматривается создание прослушивателя, использующего внутренний балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="9c1dd-122">Если вам требуется прослушивателя открытого или внешними, см. hello в этой статье, посвященной параметр вверх [внешний прослушиватель](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9c1dd-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="9c1dd-123">Создание конечных точек балансировки нагрузки в ВМ со службой Direct Server Return</span><span class="sxs-lookup"><span data-stu-id="9c1dd-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="9c1dd-124">Сначала создать ILB, запустив сценарий hello позже в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="9c1dd-125">Создайте конечную точку с балансировкой нагрузки для каждой виртуальной машины с репликой Azure.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="9c1dd-126">Если у вас есть реплики в нескольких регионах, каждая реплика для этого региона должна быть в hello же облачную службу в hello же виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="9c1dd-127">Чтобы создать реплики группы доступности, охватывающие несколько регионов Azure, необходимо настроить несколько виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="9c1dd-128">Дополнительные сведения о настройке кросс-подключения к виртуальной сети см. в разделе [настройки сетевых подключений виртуальной сети toovirtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="9c1dd-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="9c1dd-129">В hello портал Azure перейдите tooeach виртуальной Машины, на котором размещена подробные сведения о реплике tooview hello.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="9c1dd-130">Нажмите кнопку hello **конечные точки** вкладки для каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="9c1dd-131">Убедитесь, что hello **имя** и **общий порт** hello прослушиватель конечной точки требуется toouse уже не используются.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="9c1dd-132">В примере hello в этом разделе, имеет имя hello *MyEndpoint*, а порт hello *1433*.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="9c1dd-133">На локальном клиенте Загрузите и установите hello последней [модуль PowerShell](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9c1dd-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="9c1dd-134">Запустите Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="9c1dd-135">Открывает новый сеанс PowerShell с hello Azure загруженными административными модулями.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="9c1dd-136">Запустите `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="9c1dd-137">Этот командлет перенаправит браузер tooa toodownload публикации параметров файла tooa локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="9c1dd-138">Может потребоваться ввод учетных данных для входа в подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="9c1dd-139">Запустите следующие hello `Import-AzurePublishSettingsFile` загруженный файл настроек публикации командой hello путь hello:</span><span class="sxs-lookup"><span data-stu-id="9c1dd-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="9c1dd-140">После публикации hello импорта файла параметров, можно управлять подпиской Azure в сеансе PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="9c1dd-141">Для *балансировщика нагрузки* вам потребуется назначить статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="9c1dd-142">Проверьте текущую конфигурацию виртуальной сети hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="9c1dd-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="9c1dd-143">Примечание hello *подсети* имя для подсети hello, содержащей hello ВМ, на которых размещены реплики hello.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="9c1dd-144">Это имя используется в параметре hello $SubnetName в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="9c1dd-145">Примечание hello *VirtualNetworkSite* имя и hello начиная *AddressPrefix* для hello подсети, содержащей hello ВМ, на которых размещены реплики hello.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="9c1dd-146">Найдите доступные IP-адреса, передав оба значения toohello `Test-AzureStaticVNetIP` команду и просмотрев hello *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="9c1dd-147">Например, если hello виртуальной сети называется *MyVNet* и имеет диапазон адресов подсети, который начинается с позиции *172.16.0.128*, hello следующая команда, будет выведен список доступных адресов:</span><span class="sxs-lookup"><span data-stu-id="9c1dd-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="9c1dd-148">Выберите один из доступных адресов hello и использовать его в параметре hello $ILBStaticIP hello скрипт на следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="9c1dd-149">Скопируйте hello, следуя PowerShell скрипт tooa текстовый редактор и задайте toosuit hello значения переменных среды.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="9c1dd-150">Для некоторых параметров указаны значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="9c1dd-151">Вы не сможете добавить внутренний балансировщик нагрузки к имеющимся развернутым службам, использующим территориальные группы.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="9c1dd-152">Дополнительные сведения о требованиях внутреннего балансировщика нагрузки см. в статье [Обзор внутренней подсистемы балансировки нагрузки](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c1dd-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="9c1dd-153">Кроме того Если группа доступности охватывает регионы Azure, необходимо запустить скрипт hello один раз в каждом центре обработки данных для hello облачной службы и узлы, находящиеся в этом центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="9c1dd-154">После установки переменных hello hello Копировать сценарий из сеанса hello текстового редактора tooyour PowerShell toorun его.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="9c1dd-155">Если появится запрос hello  **>>** , нажмите клавишу ВВОД еще раз убедиться, что скрипт hello toomake запуска.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="9c1dd-156">Проверка наличия пакета KB2854082</span><span class="sxs-lookup"><span data-stu-id="9c1dd-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="9c1dd-157">Открыть порты брандмауэра hello в узлах группы доступности</span><span class="sxs-lookup"><span data-stu-id="9c1dd-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="9c1dd-158">Создание прослушивателя группы доступности hello</span><span class="sxs-lookup"><span data-stu-id="9c1dd-158">Create hello availability group listener</span></span>

<span data-ttu-id="9c1dd-159">Создание прослушивателя группы доступности hello в два этапа.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="9c1dd-160">Во-первых создайте ресурс кластера точки доступа клиента hello и настроить зависимости.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="9c1dd-161">Во-вторых настройте ресурсы кластера hello в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="9c1dd-162">Создать точку доступа клиента hello и настроить зависимости кластера hello</span><span class="sxs-lookup"><span data-stu-id="9c1dd-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="9c1dd-163">Настройка ресурсов кластера hello в PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c1dd-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="9c1dd-164">Для ILB необходимо использовать IP-адрес hello hello ILB, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="9c1dd-165">tooobtain этот IP-адрес в PowerShell hello используйте следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="9c1dd-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="9c1dd-166">На одном из hello виртуальные машины скопируйте сценарий PowerShell hello для текстового редактора tooa операционной системы и установка переменных hello toohello записанные ранее значения.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="9c1dd-167">Для Windows Server 2012 или более поздней версии используйте следующий сценарий hello:</span><span class="sxs-lookup"><span data-stu-id="9c1dd-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="9c1dd-168">Для Windows Server 2008 R2 используйте следующий сценарий hello:</span><span class="sxs-lookup"><span data-stu-id="9c1dd-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="9c1dd-169">После того как вы hello заданные переменные, откройте окно Windows PowerShell с повышенными привилегиями, вставить hello сценарий из hello текстового редактора в вашей toorun сеанса PowerShell его.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="9c1dd-170">Если появится запрос hello  **>>** , нажмите клавишу ВВОД еще раз убедиться, что начать выполнение скрипта hello toomake.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="9c1dd-171">Повторите hello в предыдущих шагах, для каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="9c1dd-172">Этот скрипт настраивает ресурс IP-адреса hello с IP-адресом hello hello облачной службы и устанавливает прочие параметры, такие как порт пробы hello.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="9c1dd-173">При подключении hello ресурс IP-адреса, он может отвечать toohello опрос на порту пробы hello из hello балансировкой нагрузки конечной точки, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="9c1dd-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="9c1dd-174">Перевод прослушивателя hello в интерактивном режиме</span><span class="sxs-lookup"><span data-stu-id="9c1dd-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="9c1dd-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c1dd-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="9c1dd-176">Прослушиватель группы доступности hello теста (в пределах hello же виртуальной сети)</span><span class="sxs-lookup"><span data-stu-id="9c1dd-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="9c1dd-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c1dd-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
