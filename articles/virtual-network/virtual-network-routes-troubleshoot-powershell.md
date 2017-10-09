---
title: "маршруты aaaTroubleshoot - PowerShell | Документы Microsoft"
description: "Узнайте, как tootroubleshoot маршрутизирует в модели развертывания диспетчера ресурсов Azure hello, с помощью Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="d2bba-103">Устранение проблем с маршрутами с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2bba-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2bba-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d2bba-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="d2bba-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2bba-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="d2bba-106">При возникновении tooor проблем подключения к сети из вашей виртуальной машины (ВМ) Azure, маршруты может влиять на трафик, поступающий на виртуальную Машину.</span><span class="sxs-lookup"><span data-stu-id="d2bba-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="d2bba-107">Это статье представлен обзор возможностей диагностики для маршрутов, toohelp дополнительную диагностику.</span><span class="sxs-lookup"><span data-stu-id="d2bba-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="d2bba-108">Таблицы маршрутов связаны с подсетями и действуют во всех сетевых интерфейсах в подсети.</span><span class="sxs-lookup"><span data-stu-id="d2bba-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="d2bba-109">следующие типы маршрутов Hello может быть применен tooeach сетевой интерфейс:</span><span class="sxs-lookup"><span data-stu-id="d2bba-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="d2bba-110">**Системные маршруты.** По умолчанию каждая подсеть, созданная в виртуальной сети Azure, содержит таблицы системных маршрутов. Они разрешают локальный трафик виртуальной сети, локальный трафик через VPN-шлюзы и интернет-трафик.</span><span class="sxs-lookup"><span data-stu-id="d2bba-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="d2bba-111">Кроме того, существуют системные маршруты для пиринговых виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="d2bba-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="d2bba-112">**Маршруты BGP:** распространяются toonetwork интерфейсов с помощью ExpressRoute или VPN-подключения сеть сеть.</span><span class="sxs-lookup"><span data-stu-id="d2bba-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="d2bba-113">Дополнительные сведения о маршрутизации BGP, считывая hello [BGP шлюзах VPN со](../vpn-gateway/vpn-gateway-bgp-overview.md) и [Обзор ExpressRoute](../expressroute/expressroute-introduction.md) статей.</span><span class="sxs-lookup"><span data-stu-id="d2bba-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="d2bba-114">**Определяемые пользователем маршруты (UDR):** Если вы используете виртуальных сетевых устройств или являются принудительного туннелирования трафика tooan локальной сети через VPN сайтами, возможно, определяемых пользователем маршрутов (UDRs), связанных с вашей подсети таблицы маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d2bba-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="d2bba-115">Если вы не знакомы с UDRs, прочтите hello [определяемых пользователем маршрутов](virtual-networks-udr-overview.md#user-defined-routes) статьи.</span><span class="sxs-lookup"><span data-stu-id="d2bba-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="d2bba-116">С hello различные маршруты, в которых может быть применен tooa сетевого интерфейса, который может быть трудно toodetermine статистические маршруты, вступают в силу.</span><span class="sxs-lookup"><span data-stu-id="d2bba-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="d2bba-117">toohelp устранения неполадок подключения к сети виртуальной Машины, можно просмотреть все hello действующих маршрутов для сетевого интерфейса в модели развертывания диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d2bba-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="d2bba-118">С помощью поток трафика действующих маршрутах tootroubleshoot виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="d2bba-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="d2bba-119">В этой статье используется hello, выполнив сценарий как пример tooillustrate как tootroubleshoot hello эффективную маршрутов для сетевого интерфейса:</span><span class="sxs-lookup"><span data-stu-id="d2bba-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="d2bba-120">Виртуальная машина (*VM1*) подключен toohello виртуальной сети (*VNet1*, префикс: 10.9.0.0/16) происходит сбой tooconnect tooa VM(VM3) в только что peered виртуальной сети (*VNet3*, префикса 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="d2bba-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="d2bba-121">Существуют не UDRs или BGP направляет примененных tooVM1-NIC1 сетевой интерфейс подключен toohello виртуальной Машины, применяются только маршруты системы.</span><span class="sxs-lookup"><span data-stu-id="d2bba-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="d2bba-122">В этой статье объясняется, как вызвать toodetermine hello сбоя подключения hello, с помощью возможностей действующих маршрутах в модели развертывания, управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="d2bba-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="d2bba-123">Хотя пример hello использует только маршруты системы, hello же действия можно использовать toodetermine сбоев входящие и исходящие подключения через любой тип маршрута.</span><span class="sxs-lookup"><span data-stu-id="d2bba-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="d2bba-124">Если ВМ имеет более одного сетевого Адаптера, подключенного, проверьте действующих маршрутах для каждого hello tooand проблем подключения к сети toodiagnose сетевых адаптеров из виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d2bba-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="d2bba-125">Просмотр эффективных маршрутов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d2bba-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="d2bba-126">toosee hello статистические маршрутов, примененные tooa ВМ, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="d2bba-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="d2bba-127">Просмотр эффективных маршрутов сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="d2bba-127">View effective routes for a network interface</span></span>
<span data-ttu-id="d2bba-128">toosee hello статистические маршрутах, которые применяются tooa сетевого интерфейса, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="d2bba-128">toosee hello aggregate routes that are applied tooa network interface, complete hello following steps:</span></span>

1. <span data-ttu-id="d2bba-129">Запуск сеанса и имени входа tooAzure Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2bba-129">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="d2bba-130">Если вы не знакомы с помощью Azure PowerShell, прочтите hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.</span><span class="sxs-lookup"><span data-stu-id="d2bba-130">If you’re not familiar with Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="d2bba-131">Hello следующая команда возвращает все маршруты применения tooa сетевой интерфейс с именем *VM1 NIC1* в группе ресурсов hello *RG1*.</span><span class="sxs-lookup"><span data-stu-id="d2bba-131">hello following command returns all routes applied tooa network interface named *VM1-NIC1* in hello resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="d2bba-132">Если вы не знаете имя hello сетевого интерфейса, введите hello, следующая команда tooretrieve hello имена всех сетевых интерфейсов в group.* ресурсов</span><span class="sxs-lookup"><span data-stu-id="d2bba-132">If you don’t know hello name of a network interface, type hello following command tooretrieve hello names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="d2bba-133">Hello следующие выходные данные выглядят аналогично toohello выходные данные для каждой подсети hello маршрута применения toohello, сетевой Адаптер подключен к:</span><span class="sxs-lookup"><span data-stu-id="d2bba-133">hello following output looks similar toohello output for each route applied toohello subnet hello NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="d2bba-134">Обратите внимание, следующие hello в выходных данных hello:</span><span class="sxs-lookup"><span data-stu-id="d2bba-134">Notice hello following in hello output:</span></span>
   
   * <span data-ttu-id="d2bba-135">**Имя**: имя действующего маршрута hello может быть пустым, если не указано явным образом, для определяемых пользователем маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d2bba-135">**Name**: Name of hello effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="d2bba-136">**Состояние**: Указывает состояние действующего маршрута hello.</span><span class="sxs-lookup"><span data-stu-id="d2bba-136">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="d2bba-137">Возможные значения: Active (Активный) или Invalid (Недействительный)</span><span class="sxs-lookup"><span data-stu-id="d2bba-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="d2bba-138">**AddressPrefixes**: Указывает префикс адреса hello hello действующего маршрута в нотации CIDR.</span><span class="sxs-lookup"><span data-stu-id="d2bba-138">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="d2bba-139">**nextHopType**: указывает hello следующего прыжка для заданного маршрута hello.</span><span class="sxs-lookup"><span data-stu-id="d2bba-139">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="d2bba-140">Возможные значения: *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* или *Null*.</span><span class="sxs-lookup"><span data-stu-id="d2bba-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="d2bba-141">Значение *Null* для **nextHopType** в UDR может означать недействительный маршрут.</span><span class="sxs-lookup"><span data-stu-id="d2bba-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="d2bba-142">Например если **nextHopType** — *VirtualAppliance* и виртуальное устройство hello сети виртуальной Машины не находится в состоянии подготовки и выполнения.</span><span class="sxs-lookup"><span data-stu-id="d2bba-142">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="d2bba-143">Если **nextHopType** — *VPNGateway* и нет шлюза Подготовка и выполнение в hello данной виртуальной сети, маршрут hello могут стать недопустимыми.</span><span class="sxs-lookup"><span data-stu-id="d2bba-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
   * <span data-ttu-id="d2bba-144">**NextHopIpAddress**: Указывает IP-адрес следующего прыжка действующего маршрута hello hello hello.</span><span class="sxs-lookup"><span data-stu-id="d2bba-144">**NextHopIpAddress**: Specifies hello IP address of hello next hop of hello effective route.</span></span>
   
   <span data-ttu-id="d2bba-145">Hello следующая команда возвращает hello маршруты в таблицу tooview проще:</span><span class="sxs-lookup"><span data-stu-id="d2bba-145">hello following command returns hello routes in an easier tooview table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="d2bba-146">Hello следующие выходные данные выглядят некоторые hello выходных данных, полученных для описанному выше сценарию hello:</span><span class="sxs-lookup"><span data-stu-id="d2bba-146">hello following output is some of hello output received for hello scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="d2bba-147">Нет нет в списке маршрута toohello *WestUS VNet3* виртуальной сети (префикс 10.10.0.0/16)** из *WestUS VNet1* (префикса 10.9.0.0/16) в выходных данных hello из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="d2bba-147">There is no route listed toohello *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello output from hello previous step.</span></span> <span data-ttu-id="d2bba-148">Как показано в следующий рисунок hello hello виртуальную сеть пиринга связь с hello *WestUS VNet3* виртуальной сети находится в hello *Disconnected* состояния.</span><span class="sxs-lookup"><span data-stu-id="d2bba-148">As shown in hello following picture, hello VNet peering link with hello *WestUS-VNet3* VNet is in hello *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="d2bba-149">Hello двусторонней связи для hello пиринг нарушена, который объясняет, почему VM1 не удалось подключиться tooVM3 в hello *WestUS VNet3* виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d2bba-149">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="d2bba-150">Заново настройте двунаправленную пиринговую связь для виртуальных сетей *WestUS-VNet1* и *WestUS-VNet3*.</span><span class="sxs-lookup"><span data-stu-id="d2bba-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="d2bba-151">Hello выходные данные, возвращаемые после hello виртуальную сеть пиринга правильно связи выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d2bba-151">hello output returned after hello VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="d2bba-152">После определения проблемы hello, можно добавлять, удалять, или изменить маршруты и таблиц маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d2bba-152">Once you determine hello issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="d2bba-153">Введите hello, следующая команда toosee список команд, используемых toodo hello так:</span><span class="sxs-lookup"><span data-stu-id="d2bba-153">Type hello following command toosee a list of hello commands used toodo so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="d2bba-154">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="d2bba-154">Considerations</span></span>
<span data-ttu-id="d2bba-155">Возвращено несколько вещей tookeep помнить при просмотре списка hello маршрутов:</span><span class="sxs-lookup"><span data-stu-id="d2bba-155">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="d2bba-156">Маршрутизация основана на совпадении самого длинного префикса (LPM) среди маршрутов UDR, BGP и системных маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d2bba-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="d2bba-157">Если имеется несколько маршрутов с hello же LPM совпадение, то маршрут выбирается в зависимости от ее исходной конфигурации в hello следующий порядок:</span><span class="sxs-lookup"><span data-stu-id="d2bba-157">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>
  
  * <span data-ttu-id="d2bba-158">определяемый пользователем маршрут;</span><span class="sxs-lookup"><span data-stu-id="d2bba-158">User-defined route</span></span>
  * <span data-ttu-id="d2bba-159">маршрут BGP;</span><span class="sxs-lookup"><span data-stu-id="d2bba-159">BGP route</span></span>
  * <span data-ttu-id="d2bba-160">системный (стандартный) маршрут.</span><span class="sxs-lookup"><span data-stu-id="d2bba-160">System (Default) route</span></span>
    
    <span data-ttu-id="d2bba-161">С действующих маршрутах вы увидите только действующих маршрутах, которые LPM соответствие всех доступных маршрутов hello.</span><span class="sxs-lookup"><span data-stu-id="d2bba-161">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="d2bba-162">Отображая фактически оценку hello маршруты для данного сетевого Адаптера, это позволяет намного проще tootroubleshoot определенные маршруты, в которых может влиять на подключение из виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d2bba-162">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="d2bba-163">Если вы используете UDRs и отправки трафика tooa сети виртуальной машины (оценки уязвимости сети), с *VirtualAppliance* как **nextHopType**, включить IP-пересылки на принимающей трафик hello hello уязвимости сети или пакеты будут удалены.</span><span class="sxs-lookup"><span data-stu-id="d2bba-163">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span> 
* <span data-ttu-id="d2bba-164">Если включено Принудительное туннелирование, весь исходящий трафик Интернета будет перенаправленное tooon организациями.</span><span class="sxs-lookup"><span data-stu-id="d2bba-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="d2bba-165">RDP/SSH из Интернета tooyour виртуальной Машины не может работать с этим параметром, в зависимости от того, каким образом hello в локальной обработки этого трафика.</span><span class="sxs-lookup"><span data-stu-id="d2bba-165">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span> 
  <span data-ttu-id="d2bba-166">Принудительное туннелирование можно включить:</span><span class="sxs-lookup"><span data-stu-id="d2bba-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="d2bba-167">если используется VPN-подключение типа "сеть — сеть" (задайте определяемый пользователем маршрут и укажите для параметра nextHopType значение VPN-шлюза);</span><span class="sxs-lookup"><span data-stu-id="d2bba-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="d2bba-168">если маршрут по умолчанию объявляется через BGP.</span><span class="sxs-lookup"><span data-stu-id="d2bba-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="d2bba-169">Для трафик пиринговой виртуальной сети toowork трафика правильной системе маршрут с **nextHopType** *VNetPeering* должен существовать для hello одноранговыми префикс диапазона виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d2bba-169">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="d2bba-170">Если такой маршрут не существует и hello виртуальную сеть пиринга ссылку выглядит правильно:</span><span class="sxs-lookup"><span data-stu-id="d2bba-170">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="d2bba-171">Подождите несколько секунд и повторите попытку, если пиринговая связь установлена недавно.</span><span class="sxs-lookup"><span data-stu-id="d2bba-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="d2bba-172">Время от времени занимает больше времени, маршруты toopropagate tooall hello сетевых интерфейсов в подсети.</span><span class="sxs-lookup"><span data-stu-id="d2bba-172">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="d2bba-173">Правила группы безопасности сети (NSG) может влиять на трафик, поступающий hello.</span><span class="sxs-lookup"><span data-stu-id="d2bba-173">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="d2bba-174">Дополнительные сведения см. в разделе hello [Устранение сетевых групп безопасности](virtual-network-nsg-troubleshoot-powershell.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="d2bba-174">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

