---
title: "Устранение проблем с маршрутами с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как устранять неполадки маршрутов в модели развертывания Azure Resource Manager с помощью Azure PowerShell."
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
ms.openlocfilehash: 141e3c571d744470fd07e99538b6e38d4144e8d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="2ef22-103">Устранение проблем с маршрутами с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ef22-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ef22-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2ef22-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="2ef22-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ef22-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="2ef22-106">Если возникают проблемы с входящим или исходящим сетевым соединением виртуальной машины Azure, возможно, на потоки трафика ВМ влияют маршруты.</span><span class="sxs-lookup"><span data-stu-id="2ef22-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="2ef22-107">Эта статья содержит обзор возможностей диагностики маршрутов для дальнейшего устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="2ef22-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span></span>

<span data-ttu-id="2ef22-108">Таблицы маршрутов связаны с подсетями и действуют во всех сетевых интерфейсах в подсети.</span><span class="sxs-lookup"><span data-stu-id="2ef22-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="2ef22-109">Для каждого сетевого интерфейса могут применяться указанные далее типы маршрутов.</span><span class="sxs-lookup"><span data-stu-id="2ef22-109">The following types of routes can be applied to each network interface:</span></span>

* <span data-ttu-id="2ef22-110">**Системные маршруты.** По умолчанию каждая подсеть, созданная в виртуальной сети Azure, содержит таблицы системных маршрутов. Они разрешают локальный трафик виртуальной сети, локальный трафик через VPN-шлюзы и интернет-трафик.</span><span class="sxs-lookup"><span data-stu-id="2ef22-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="2ef22-111">Кроме того, существуют системные маршруты для пиринговых виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="2ef22-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="2ef22-112">**Маршруты BGP.** Распространяются на сетевые интерфейсы через ExpressRoute или VPN-подключения типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="2ef22-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="2ef22-113">Дополнительные сведения о маршрутизации BGP см. в статьях [Обзор использования BGP с VPN-шлюзами Azure](../vpn-gateway/vpn-gateway-bgp-overview.md) и [Технический обзор ExpressRoute](../expressroute/expressroute-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2ef22-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="2ef22-114">**Определяемые пользователем маршруты (UDR).** Если вы используете виртуальные сетевые устройства или принудительное туннелирование трафика в локальную сеть через VPN-подключение типа "сеть — сеть", вы можете использовать определяемые пользователем маршруты, связанные с таблицей маршрутов подсети.</span><span class="sxs-lookup"><span data-stu-id="2ef22-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="2ef22-115">Если вы не знакомы с этими маршрутами, прочтите статью [Что такое определяемые пользователем маршруты и IP-пересылка](virtual-networks-udr-overview.md#user-defined-routes) .</span><span class="sxs-lookup"><span data-stu-id="2ef22-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="2ef22-116">Когда в сетевом интерфейсе применяются различные маршруты, может быть сложно определить, какие агрегированные маршруты эффективны.</span><span class="sxs-lookup"><span data-stu-id="2ef22-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span></span> <span data-ttu-id="2ef22-117">Просмотрите все эффективные маршруты сетевого интерфейса в модели развертывания с помощью Azure Resource Manager, чтобы получить информацию, которая поможет устранить неполадки сетевого подключения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2ef22-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="2ef22-118">Использование эффективных маршрутов для устранения неполадок с передачей трафика в виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="2ef22-118">Using Effective Routes to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="2ef22-119">В этой статье для иллюстрации устранения неполадок эффективных маршрутов сетевого интерфейса в качестве примера используется указанный далее сценарий.</span><span class="sxs-lookup"><span data-stu-id="2ef22-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span></span>

<span data-ttu-id="2ef22-120">Виртуальной машине (*VM1*), подключенной к виртуальной сети (*VNet1*, префикс 10.9.0.0/16), не удается подключиться к ВМ (VM3) в виртуальной сети, для которой недавно был осуществлен пиринг (*VNet3*, префикс 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="2ef22-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="2ef22-121">К сетевому интерфейсу VM1-NIC1, подключенному к виртуальной машине, не применяются маршруты UDR или BGP. Применяются только системные маршруты.</span><span class="sxs-lookup"><span data-stu-id="2ef22-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span></span>

<span data-ttu-id="2ef22-122">В этой статье объясняется, как определить причину сбоя подключения с помощью эффективных маршрутов в модели развертывания Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2ef22-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="2ef22-123">Хотя в этом примере используются только системные маршруты, описанные в нем действия помогут определить, почему происходит сбой входящего и исходящего подключения для любого типа маршрута.</span><span class="sxs-lookup"><span data-stu-id="2ef22-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="2ef22-124">Если к виртуальной машине подключены несколько сетевых адаптеров, проверьте эффективные маршруты для каждого из них. Это поможет диагностировать проблемы с входящим и исходящим сетевым соединением виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2ef22-124">If your VM has more than one NIC attached, check effective routes for each of the NICs to diagnose network connectivity issues to and from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="2ef22-125">Просмотр эффективных маршрутов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2ef22-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="2ef22-126">Чтобы просмотреть агрегированные маршруты, которые применяются к виртуальной машине, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2ef22-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="2ef22-127">Просмотр эффективных маршрутов сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="2ef22-127">View effective routes for a network interface</span></span>
<span data-ttu-id="2ef22-128">Для просмотра агрегированных маршрутов, которые применяются к сетевому интерфейсу, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="2ef22-128">To see the aggregate routes that are applied to a network interface, complete the following steps:</span></span>

1. <span data-ttu-id="2ef22-129">Запустите сеанс Azure PowerShell и войдите в Azure.</span><span class="sxs-lookup"><span data-stu-id="2ef22-129">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="2ef22-130">Если вы не знакомы с Azure PowerShell, прочтите статью [Установка и настройка Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="2ef22-130">If you’re not familiar with Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="2ef22-131">Следующая команда возвращает все маршруты, применяемые к сетевому интерфейсу с именем *VM1-NIC1* в группе ресурсов *RG1*.</span><span class="sxs-lookup"><span data-stu-id="2ef22-131">The following command returns all routes applied to a network interface named *VM1-NIC1* in the resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="2ef22-132">Если вы не знаете имя сетевого интерфейса, введите следующую команду, чтобы извлечь имена всех сетевых интерфейсов в группе ресурсов.*</span><span class="sxs-lookup"><span data-stu-id="2ef22-132">If you don’t know the name of a network interface, type the following command to retrieve the names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="2ef22-133">Для каждого маршрута, применяемого в подсети, к которой подключен адаптер, отобразится похожий результат:</span><span class="sxs-lookup"><span data-stu-id="2ef22-133">The following output looks similar to the output for each route applied to the subnet the NIC is connected to:</span></span>
   
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
   
   <span data-ttu-id="2ef22-134">В выходных данных обратите внимание на следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="2ef22-134">Notice the following in the output:</span></span>
   
   * <span data-ttu-id="2ef22-135">**Name**— для определяемых пользователем маршрутов имя эффективного маршрута может быть пустым, если оно не указано явным образом.</span><span class="sxs-lookup"><span data-stu-id="2ef22-135">**Name**: Name of the effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="2ef22-136">**State**— указывает состояние эффективного маршрута.</span><span class="sxs-lookup"><span data-stu-id="2ef22-136">**State**: Indicates state of the effective route.</span></span> <span data-ttu-id="2ef22-137">Возможные значения: Active (Активный) или Invalid (Недействительный)</span><span class="sxs-lookup"><span data-stu-id="2ef22-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="2ef22-138">**AddressPrefixes**— указывает префикс адреса эффективного маршрута в нотации CIDR.</span><span class="sxs-lookup"><span data-stu-id="2ef22-138">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="2ef22-139">**nextHopType**— указывает следующий прыжок для указанного маршрута.</span><span class="sxs-lookup"><span data-stu-id="2ef22-139">**nextHopType**: Indicates the next hop for the given route.</span></span> <span data-ttu-id="2ef22-140">Возможные значения: *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* или *Null*.</span><span class="sxs-lookup"><span data-stu-id="2ef22-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="2ef22-141">Значение *Null* для **nextHopType** в UDR может означать недействительный маршрут.</span><span class="sxs-lookup"><span data-stu-id="2ef22-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="2ef22-142">Например, если для **nextHopType** задано значение *VirtualAppliance* и виртуальная машина с виртуальным сетевым устройством не находится в состоянии подготовки или выполнения.</span><span class="sxs-lookup"><span data-stu-id="2ef22-142">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="2ef22-143">Если для **nextHopType** задано значение *VPNGateway* и в указанной виртуальной сети не подготавливается и не выполняется ни один шлюз, маршрут может стать недопустимым.</span><span class="sxs-lookup"><span data-stu-id="2ef22-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span></span>
   * <span data-ttu-id="2ef22-144">**NextHopIpAddress**— IP-адрес следующего прыжка эффективного маршрута.</span><span class="sxs-lookup"><span data-stu-id="2ef22-144">**NextHopIpAddress**: Specifies the IP address of the next hop of the effective route.</span></span>
   
   <span data-ttu-id="2ef22-145">Следующая команда выводит маршруты в простой для просмотра таблице:</span><span class="sxs-lookup"><span data-stu-id="2ef22-145">The following command returns the routes in an easier to view table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="2ef22-146">Следующий результат получен в рамках сценария, описанного ранее:</span><span class="sxs-lookup"><span data-stu-id="2ef22-146">The following output is some of the output received for the scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="2ef22-147">В результатах, полученных на предыдущем шаге, отсутствует маршрут для виртуальной сети *WestUS-VNet3* (префикс 10.10.0.0/16)** из *WestUS-VNet1* (префикс 10.9.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="2ef22-147">There is no route listed to the *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in the output from the previous step.</span></span> <span data-ttu-id="2ef22-148">Как показано на следующем рисунке, пиринговая связь виртуальной сети *WestUS-VNet3* находится в состоянии *Disconnected* (Отключена).</span><span class="sxs-lookup"><span data-stu-id="2ef22-148">As shown in the following picture, the VNet peering link with the *WestUS-VNet3* VNet is in the *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="2ef22-149">Двунаправленная связь для пиринга разорвана, что объясняет, почему VM1 не удалось подключиться к VM3 в виртуальной сети *WestUS-VNet3* .</span><span class="sxs-lookup"><span data-stu-id="2ef22-149">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="2ef22-150">Заново настройте двунаправленную пиринговую связь для виртуальных сетей *WestUS-VNet1* и *WestUS-VNet3*.</span><span class="sxs-lookup"><span data-stu-id="2ef22-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="2ef22-151">При правильной установке пиринговой связи вы получите такой результат:</span><span class="sxs-lookup"><span data-stu-id="2ef22-151">The output returned after the VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="2ef22-152">После определения проблемы можно добавлять, удалять или изменять маршруты и таблицы маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="2ef22-152">Once you determine the issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="2ef22-153">Введите следующую команду, чтобы просмотреть список используемых для этого команд:</span><span class="sxs-lookup"><span data-stu-id="2ef22-153">Type the following command to see a list of the commands used to do so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="2ef22-154">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="2ef22-154">Considerations</span></span>
<span data-ttu-id="2ef22-155">Ниже приведено несколько аспектов, которые следует учитывать при просмотре списка маршрутов.</span><span class="sxs-lookup"><span data-stu-id="2ef22-155">A few things to keep in mind when reviewing the list of routes returned:</span></span>

* <span data-ttu-id="2ef22-156">Маршрутизация основана на совпадении самого длинного префикса (LPM) среди маршрутов UDR, BGP и системных маршрутов.</span><span class="sxs-lookup"><span data-stu-id="2ef22-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="2ef22-157">При наличии нескольких маршрутов с одинаковыми совпадающими значениями LPM маршрут выбирается по источнику в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="2ef22-157">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span></span>
  
  * <span data-ttu-id="2ef22-158">определяемый пользователем маршрут;</span><span class="sxs-lookup"><span data-stu-id="2ef22-158">User-defined route</span></span>
  * <span data-ttu-id="2ef22-159">маршрут BGP;</span><span class="sxs-lookup"><span data-stu-id="2ef22-159">BGP route</span></span>
  * <span data-ttu-id="2ef22-160">системный (стандартный) маршрут.</span><span class="sxs-lookup"><span data-stu-id="2ef22-160">System (Default) route</span></span>
    
    <span data-ttu-id="2ef22-161">Функция эффективных маршрутов позволяет просмотреть только эффективные маршруты, выделенные из доступных маршрутов при помощи совпадающего значения LPM.</span><span class="sxs-lookup"><span data-stu-id="2ef22-161">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span></span> <span data-ttu-id="2ef22-162">Отображение фактического способа вычисления маршрутов для отдельного сетевого адаптера упрощает устранение неполадок в определенных маршрутах, которые могут повлиять на входящее и исходящее соединение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2ef22-162">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="2ef22-163">Если вы используете маршруты UDR и отправляете трафик на виртуальное сетевое устройство и при этом для параметра *VirtualAppliance* установлено значение **nextHopType**, обязательно включите IP-пересылку на принимающем трафик виртуальном сетевом устройстве, иначе пакеты будут пропускаться.</span><span class="sxs-lookup"><span data-stu-id="2ef22-163">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span></span> 
* <span data-ttu-id="2ef22-164">Если включено принудительное туннелирование, весь исходящий интернет-трафик будет перенаправлен в локальную систему.</span><span class="sxs-lookup"><span data-stu-id="2ef22-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span></span> <span data-ttu-id="2ef22-165">Если этот параметр включен, доступ RDP или SSH из Интернета к виртуальной машине может не работать. Это зависит от способа обработки трафика локальной системой.</span><span class="sxs-lookup"><span data-stu-id="2ef22-165">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span></span> 
  <span data-ttu-id="2ef22-166">Принудительное туннелирование можно включить:</span><span class="sxs-lookup"><span data-stu-id="2ef22-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="2ef22-167">если используется VPN-подключение типа "сеть — сеть" (задайте определяемый пользователем маршрут и укажите для параметра nextHopType значение VPN-шлюза);</span><span class="sxs-lookup"><span data-stu-id="2ef22-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="2ef22-168">если маршрут по умолчанию объявляется через BGP.</span><span class="sxs-lookup"><span data-stu-id="2ef22-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="2ef22-169">Для правильной работы пирингового трафика виртуальной сети системный маршрут, в котором для **nextHopType** *VNetPeering* , должен действовать в диапазоне префиксов пиринговой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2ef22-169">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span></span> <span data-ttu-id="2ef22-170">Если такого маршрута не существует и пиринговая связь сети действует нормально, возможны два сценария действий.</span><span class="sxs-lookup"><span data-stu-id="2ef22-170">If such a route doesn’t exist and the VNet peering link looks OK:</span></span>
  * <span data-ttu-id="2ef22-171">Подождите несколько секунд и повторите попытку, если пиринговая связь установлена недавно.</span><span class="sxs-lookup"><span data-stu-id="2ef22-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="2ef22-172">Иногда требуется больше времени, чтобы распространить маршруты для всех сетевых интерфейсов в подсети.</span><span class="sxs-lookup"><span data-stu-id="2ef22-172">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span></span>
  * <span data-ttu-id="2ef22-173">Правила групп безопасности сети (NSG) могут влиять на потоки трафика.</span><span class="sxs-lookup"><span data-stu-id="2ef22-173">Network Security Group (NSG) rules may be impacting the traffic flows.</span></span> <span data-ttu-id="2ef22-174">Дополнительные сведения см. в статье, посвященной [устранению неполадок с группами безопасности сети](virtual-network-nsg-troubleshoot-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2ef22-174">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

