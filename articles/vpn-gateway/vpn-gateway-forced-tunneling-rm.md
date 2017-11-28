---
title: "Настройка принудительного туннелирования для подключений типа \"сеть — сеть\" с помощью Resource Manager | Документация Майкрософт"
description: "Как tooredirect или «принудительно» все tooyour назад Интернета трафик локального расположения."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a><span data-ttu-id="772c4-103">Настройка принудительного туннелирования с помощью модели развертывания диспетчера ресурсов Azure hello</span><span class="sxs-lookup"><span data-stu-id="772c4-103">Configure forced tunneling using hello Azure Resource Manager deployment model</span></span>

<span data-ttu-id="772c4-104">Принудительное туннелирование позволяет перенаправлять или «принудительно» все в локальное расположение задней tooyour Интернета трафик через туннель VPN сайт-сайт для проверки и аудита.</span><span class="sxs-lookup"><span data-stu-id="772c4-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="772c4-105">Это критически важное требование безопасности, имеющееся в большинстве корпоративных ИТ-политик.</span><span class="sxs-lookup"><span data-stu-id="772c4-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="772c4-106">Без принудительного туннелирования Интернет-трафик из виртуальных машин в Azure всегда проходит через из сетевой инфраструктуры Azure непосредственно из toohello Интернета, без параметра tooallow hello вы tooinspect или аудита hello трафика.</span><span class="sxs-lookup"><span data-stu-id="772c4-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="772c4-107">Несанкционированный доступ через Интернет потенциально может привести tooinformation раскрытию или другие виды угроз безопасности.</span><span class="sxs-lookup"><span data-stu-id="772c4-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="772c4-108">В этой статье описывается настройка принудительного туннелирования для виртуальных сетей, созданные с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="772c4-108">This article walks you through configuring forced tunneling for virtual networks created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="772c4-109">Принудительное туннелирование можно настроить с помощью PowerShell, не через портал hello.</span><span class="sxs-lookup"><span data-stu-id="772c4-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="772c4-110">Tooconfigure принудительного туннелирования для hello классической модели развертывания из hello, следуя раскрывающегося списка выберите классический статьи:</span><span class="sxs-lookup"><span data-stu-id="772c4-110">If you want tooconfigure forced tunneling for hello classic deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="772c4-111">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="772c4-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="772c4-112">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="772c4-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="772c4-113">Сведения о принудительном туннелировании</span><span class="sxs-lookup"><span data-stu-id="772c4-113">About forced tunneling</span></span>

<span data-ttu-id="772c4-114">Hello, следующая диаграмма иллюстрирует, как работает Принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="772c4-114">hello following diagram illustrates how forced tunneling works.</span></span> 

![Принудительное туннелирование](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="772c4-116">В приведенном выше примере hello hello проводном подсети не является принудительным переднего плана.</span><span class="sxs-lookup"><span data-stu-id="772c4-116">In hello example above, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="772c4-117">Hello рабочих нагрузок в hello внешней подсети можно продолжить tooaccept и из Интернета hello отвечающего toocustomer запросов.</span><span class="sxs-lookup"><span data-stu-id="772c4-117">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="772c4-118">Hello промежуточной и внутренней подсетях выполняется Принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="772c4-118">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="772c4-119">Все исходящие подключения из этих двух подсетей toohello Интернет будет tooan принудительной или перенаправления обратно на локальный сайт через одну приветствия туннели S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="772c4-119">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="772c4-120">Это позволяет вам toorestrict и инспектировать доступ к Интернету из виртуальных машин или облачных служб в Azure, продолжая tooenable необходимые службы многоуровневые архитектуры.</span><span class="sxs-lookup"><span data-stu-id="772c4-120">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="772c4-121">Если в виртуальных сетях не рабочих нагрузок с выходом в Интернет, также можно применить принудительного туннелирования toohello всех виртуальных сетях.</span><span class="sxs-lookup"><span data-stu-id="772c4-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling toohello entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="772c4-122">Требования и рекомендации</span><span class="sxs-lookup"><span data-stu-id="772c4-122">Requirements and considerations</span></span>

<span data-ttu-id="772c4-123">В Azure принудительное туннелирование настраивается с помощью определяемых пользователем маршрутов виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="772c4-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="772c4-124">Перенаправление трафика tooan из локального сайта выражается как шлюз Azure VPN toohello маршрут по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="772c4-124">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="772c4-125">Сведения об определяемых пользователем маршрутах см. в статье [Определяемые пользователем маршруты и IP-пересылка](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="772c4-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="772c4-126">Каждая подсеть виртуальной сети имеет встроенные системные таблицы маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="772c4-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="772c4-127">Таблица маршрутизации Hello система имеет следующие три группы маршрутов hello:</span><span class="sxs-lookup"><span data-stu-id="772c4-127">hello system routing table has hello following three groups of routes:</span></span>
  
  * <span data-ttu-id="772c4-128">**Локальные маршруты виртуальной сети:** непосредственно toohello целевым ВМ в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="772c4-128">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="772c4-129">**Локальные маршруты:** toohello VPN-шлюз Azure.</span><span class="sxs-lookup"><span data-stu-id="772c4-129">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="772c4-130">**Маршрут по умолчанию:** напрямую toohello Интернет.</span><span class="sxs-lookup"><span data-stu-id="772c4-130">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="772c4-131">Пакеты, предназначенные toohello частных IP-адресов не соответствует ни hello предыдущие два маршруты будут удалены.</span><span class="sxs-lookup"><span data-stu-id="772c4-131">Packets destined toohello private IP addresses not covered by hello previous two routes are dropped.</span></span>
* <span data-ttu-id="772c4-132">Эта процедура использует определяемых пользователем маршрутов (UDR) toocreate маршрутизации tooadd таблицы маршрут по умолчанию, а затем задать hello маршрутизации таблицы tooyour виртуальной сети подсетями tooenable принудительного туннелирования в этих подсетях.</span><span class="sxs-lookup"><span data-stu-id="772c4-132">This procedure uses user-defined routes (UDR) toocreate a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="772c4-133">Принудительное туннелирование должно быть связано с виртуальной сетью, в которой есть VPN-шлюз на основе маршрута.</span><span class="sxs-lookup"><span data-stu-id="772c4-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="772c4-134">Необходимо tooset «сайт по умолчанию» среди hello между организациями подключенных toohello локальных сайтов виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="772c4-134">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span> <span data-ttu-id="772c4-135">Кроме того hello из локального VPN-устройство должен быть настроен с помощью 0.0.0.0/0 как трафика селекторов.</span><span class="sxs-lookup"><span data-stu-id="772c4-135">Also, hello on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="772c4-136">Принудительное туннелирование ExpressRoute не настраивается с помощью этого механизма, но вместо этого обеспечивается объявление маршрута по умолчанию через hello ExpressRoute BGP сеансы пиринга.</span><span class="sxs-lookup"><span data-stu-id="772c4-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="772c4-137">Дополнительные сведения см. в разделе hello [документации по ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="772c4-137">For more information, see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="772c4-138">Общие сведения о настройке</span><span class="sxs-lookup"><span data-stu-id="772c4-138">Configuration overview</span></span>

<span data-ttu-id="772c4-139">Hello следующая процедура поможет создать группу ресурсов и виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="772c4-139">hello following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="772c4-140">Затем вы создадите VPN-шлюз и настроите принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="772c4-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="772c4-141">В этой процедуре hello виртуальной сети «MultiTier-VNet» имеет три подсети: 'Переднего плана», «Midtier» и «Серверная часть» с четырьмя соединениях между организациями: «DefaultSiteHQ» и тремя ветвями.</span><span class="sxs-lookup"><span data-stu-id="772c4-141">In this procedure, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="772c4-142">шаги процедуры Hello задать hello «DefaultSiteHQ» hello подключения сайта по умолчанию для принудительного туннелирования, и настройке hello «Midtier» и «Серверная часть» подсетей toouse принудительного туннелирования.</span><span class="sxs-lookup"><span data-stu-id="772c4-142">hello procedure steps set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello 'Midtier' and 'Backend' subnets toouse forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="772c4-143">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="772c4-143">Before you begin</span></span>

<span data-ttu-id="772c4-144">Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="772c4-144">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="772c4-145">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="772c4-145">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="toolog-in"></a><span data-ttu-id="772c4-146">toolog в</span><span class="sxs-lookup"><span data-stu-id="772c4-146">toolog in</span></span>

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="772c4-147">Настройка принудительного туннелирования</span><span class="sxs-lookup"><span data-stu-id="772c4-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="772c4-148">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="772c4-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="772c4-149">Создайте виртуальную сеть и укажите подсети.</span><span class="sxs-lookup"><span data-stu-id="772c4-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="772c4-150">Создайте hello шлюзы локальной сети.</span><span class="sxs-lookup"><span data-stu-id="772c4-150">Create hello local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="772c4-151">Создайте правило, таблицы и маршрут маршрута hello.</span><span class="sxs-lookup"><span data-stu-id="772c4-151">Create hello route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="772c4-152">Свяжите toohello таблицы маршрутов hello Midtier и подсетей серверной части.</span><span class="sxs-lookup"><span data-stu-id="772c4-152">Associate hello route table toohello Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="772c4-153">Создайте hello шлюза с узлом по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="772c4-153">Create hello Gateway with a default site.</span></span> <span data-ttu-id="772c4-154">Это требует toocomplete некоторое время, иногда 45 минут или более, так как в создании и настройке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="772c4-154">This step takes some time toocomplete, sometimes 45 minutes or more, because you are creating and configuring hello gateway.</span></span><br> <span data-ttu-id="772c4-155">Hello **- GatewayDefaultSite** hello параметр командлета, который позволяет hello принудительно маршрутизации toowork конфигурации, поэтому можете следить за tooconfigure этот параметр должным образом.</span><span class="sxs-lookup"><span data-stu-id="772c4-155">hello **-GatewayDefaultSite** is hello cmdlet parameter that allows hello forced routing configuration toowork, so take care tooconfigure this setting properly.</span></span> <span data-ttu-id="772c4-156">Он доступен только в PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="772c4-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="772c4-157">Установите hello сеть-сеть VPN-подключений.</span><span class="sxs-lookup"><span data-stu-id="772c4-157">Establish hello Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```