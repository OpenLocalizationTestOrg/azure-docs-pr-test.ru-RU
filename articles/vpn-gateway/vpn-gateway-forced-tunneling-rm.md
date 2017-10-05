---
title: "Настройка принудительного туннелирования для подключений типа \"сеть — сеть\" с помощью Resource Manager | Документация Майкрософт"
description: "Как перенаправлять или принудительно туннелировать весь интернет-трафик обратно в локальное расположение."
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
ms.openlocfilehash: 207c53924863eb51ee369fe46d5ad12fb1905c53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="configure-forced-tunneling-using-the-azure-resource-manager-deployment-model"></a><span data-ttu-id="c1275-103">Настройка принудительного туннелирования с помощью модели развертывания Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1275-103">Configure forced tunneling using the Azure Resource Manager deployment model</span></span>

<span data-ttu-id="c1275-104">Оно позволяет перенаправлять или "принудительно направлять" весь Интернет-трафик обратно в локальное расположение через VPN типа "сеть — сеть" для проверки и аудита.</span><span class="sxs-lookup"><span data-stu-id="c1275-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="c1275-105">Это критически важное требование безопасности, имеющееся в большинстве корпоративных ИТ-политик.</span><span class="sxs-lookup"><span data-stu-id="c1275-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="c1275-106">Без принудительного туннелирования Интернет-трафик из виртуальных машин в Azure всегда поступает из инфраструктуры сети Azure непосредственно в Интернет, без возможности его проверки или аудита.</span><span class="sxs-lookup"><span data-stu-id="c1275-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="c1275-107">Неавторизованный доступ в Интернет может привести к раскрытию информации или другим нарушениям безопасности.</span><span class="sxs-lookup"><span data-stu-id="c1275-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="c1275-108">В этой статье описано, как выполнить настройку принудительного туннелирования для виртуальных сетей, созданных с помощью модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1275-108">This article walks you through configuring forced tunneling for virtual networks created using the Resource Manager deployment model.</span></span> <span data-ttu-id="c1275-109">Принудительное туннелирование можно настроить с помощью PowerShell, но не на портале.</span><span class="sxs-lookup"><span data-stu-id="c1275-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="c1275-110">Если вы хотите настроить принудительное туннелирование для классической модели развертывания, выберите соответствующую статью из раскрывающегося списка ниже:</span><span class="sxs-lookup"><span data-stu-id="c1275-110">If you want to configure forced tunneling for the classic deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1275-111">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="c1275-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="c1275-112">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1275-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="c1275-113">Сведения о принудительном туннелировании</span><span class="sxs-lookup"><span data-stu-id="c1275-113">About forced tunneling</span></span>

<span data-ttu-id="c1275-114">На схеме ниже показан принцип работы принудительного туннелирования.</span><span class="sxs-lookup"><span data-stu-id="c1275-114">The following diagram illustrates how forced tunneling works.</span></span> 

![Принудительное туннелирование](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="c1275-116">В примере выше для интерфейсной подсети не применяется принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="c1275-116">In the example above, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="c1275-117">Рабочие нагрузки в интерфейсной подсети могут продолжать принимать запросы клиентов непосредственно из Интернета и отвечать на них.</span><span class="sxs-lookup"><span data-stu-id="c1275-117">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="c1275-118">Для подсетей среднего уровня и внутренних подсетей применяется принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="c1275-118">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="c1275-119">Любые исходящие подключения из этих двух подсетей к Интернету будут принудительно перенаправлены обратно на локальный сайт через один из VPN-туннелей, работающих по протоколу S2S.</span><span class="sxs-lookup"><span data-stu-id="c1275-119">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="c1275-120">Это позволяет ограничивать и проверять доступ в Интернет с виртуальных машин или облачных служб в Azure, при этом поддерживая необходимую многоуровневую архитектуру служб.</span><span class="sxs-lookup"><span data-stu-id="c1275-120">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="c1275-121">Кроме того, вы можете применять принудительное туннелирование для всех виртуальных сетей, если в них нет рабочих нагрузок, требующих взаимодействия с Интернетом.</span><span class="sxs-lookup"><span data-stu-id="c1275-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling to the entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="c1275-122">Требования и рекомендации</span><span class="sxs-lookup"><span data-stu-id="c1275-122">Requirements and considerations</span></span>

<span data-ttu-id="c1275-123">В Azure принудительное туннелирование настраивается с помощью определяемых пользователем маршрутов виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c1275-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="c1275-124">Перенаправление трафика на локальный сайт выполняется с помощью маршрута по умолчанию к VPN-шлюзу Azure.</span><span class="sxs-lookup"><span data-stu-id="c1275-124">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="c1275-125">Сведения об определяемых пользователем маршрутах см. в статье [Определяемые пользователем маршруты и IP-пересылка](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1275-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="c1275-126">Каждая подсеть виртуальной сети имеет встроенные системные таблицы маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="c1275-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="c1275-127">Системная таблица маршрутизации содержит три указанные ниже группы маршрутов.</span><span class="sxs-lookup"><span data-stu-id="c1275-127">The system routing table has the following three groups of routes:</span></span>
  
  * <span data-ttu-id="c1275-128">**Маршруты локальной виртуальной сети.** Они ведут непосредственно к виртуальным машинам назначения в той же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c1275-128">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="c1275-129">**Локальные маршруты.** Ведут к VPN-шлюзу Azure.</span><span class="sxs-lookup"><span data-stu-id="c1275-129">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="c1275-130">**Маршрут по умолчанию.** Ведет напрямую в Интернет.</span><span class="sxs-lookup"><span data-stu-id="c1275-130">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="c1275-131">Пакеты, предназначенные для частных IP-адресов, не входящих в предыдущие два маршрута, будут удалены.</span><span class="sxs-lookup"><span data-stu-id="c1275-131">Packets destined to the private IP addresses not covered by the previous two routes are dropped.</span></span>
* <span data-ttu-id="c1275-132">В этой процедуре используются определяемые пользователем маршруты для создания таблицы маршрутизации с целью добавления маршрута по умолчанию и последующего сопоставления таблицы маршрутизации с подсетями вашей виртуальной сети для включения принудительного туннелирования в этих подсетях.</span><span class="sxs-lookup"><span data-stu-id="c1275-132">This procedure uses user-defined routes (UDR) to create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="c1275-133">Принудительное туннелирование должно быть связано с виртуальной сетью, в которой есть VPN-шлюз на основе маршрута.</span><span class="sxs-lookup"><span data-stu-id="c1275-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="c1275-134">Из числа локальных межорганизационных сайтов, подключенных к виртуальной сети, необходимо выбрать "сайт по умолчанию".</span><span class="sxs-lookup"><span data-stu-id="c1275-134">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span> <span data-ttu-id="c1275-135">Кроме того, локальное VPN-устройство необходимо настроить для использования диапазона адресов 0.0.0.0/0 в качестве селекторов трафика.</span><span class="sxs-lookup"><span data-stu-id="c1275-135">Also, the on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="c1275-136">С помощью этого механизма невозможно настроить принудительное туннелирование ExpressRoute. Такое туннелирование включается, когда предлагается маршрут по умолчанию с помощью сеансов пиринга BGP ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c1275-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="c1275-137">Дополнительные сведения см. в [документации по ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="c1275-137">For more information, see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="c1275-138">Общие сведения о настройке</span><span class="sxs-lookup"><span data-stu-id="c1275-138">Configuration overview</span></span>

<span data-ttu-id="c1275-139">Следующая процедура поможет создать группу ресурсов и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="c1275-139">The following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="c1275-140">Затем вы создадите VPN-шлюз и настроите принудительное туннелирование.</span><span class="sxs-lookup"><span data-stu-id="c1275-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="c1275-141">В этой процедуре в виртуальную сеть MultiTier-VNet входят три подсети (Frontend, Midtier и Backend) с четырьмя распределенными подключениями DefaultSiteHQ и тремя ветвями Branch.</span><span class="sxs-lookup"><span data-stu-id="c1275-141">In this procedure, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="c1275-142">Выполнив указанные ниже действия, можно настроить подключение DefaultSiteHQ в качестве подключения к сайту по умолчанию для принудительного туннелирования, а также настроить принудительное туннелирование для подсетей Midtier и Backend.</span><span class="sxs-lookup"><span data-stu-id="c1275-142">The procedure steps set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the 'Midtier' and 'Backend' subnets to use forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c1275-143">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="c1275-143">Before you begin</span></span>

<span data-ttu-id="c1275-144">Установите последнюю версию командлетов PowerShell для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1275-144">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c1275-145">Дополнительные сведения об установке командлетов PowerShell см. в статье [Как установить и настроить Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c1275-145">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="to-log-in"></a><span data-ttu-id="c1275-146">Вход</span><span class="sxs-lookup"><span data-stu-id="c1275-146">To log in</span></span>

[!INCLUDE [To log in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="c1275-147">Настройка принудительного туннелирования</span><span class="sxs-lookup"><span data-stu-id="c1275-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="c1275-148">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c1275-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="c1275-149">Создайте виртуальную сеть и укажите подсети.</span><span class="sxs-lookup"><span data-stu-id="c1275-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="c1275-150">Создайте шлюзы локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c1275-150">Create the local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="c1275-151">Создайте таблицу маршрутизации и правило маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="c1275-151">Create the route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="c1275-152">Сопоставьте таблицу маршрутизации с подсетями "Midtier" и "Backend".</span><span class="sxs-lookup"><span data-stu-id="c1275-152">Associate the route table to the Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="c1275-153">Создайте шлюза с узлом по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c1275-153">Create the Gateway with a default site.</span></span> <span data-ttu-id="c1275-154">Выполнение этого шага занимает некоторое время (иногда 45 минут или более), так как выполняется создание и настройка шлюза.</span><span class="sxs-lookup"><span data-stu-id="c1275-154">This step takes some time to complete, sometimes 45 minutes or more, because you are creating and configuring the gateway.</span></span><br> <span data-ttu-id="c1275-155">**-GatewayDefaultSite** — это параметр командлета, благодаря которому работает конфигурация принудительной маршрутизации. Поэтому настройте этот параметр должным образом.</span><span class="sxs-lookup"><span data-stu-id="c1275-155">The **-GatewayDefaultSite** is the cmdlet parameter that allows the forced routing configuration to work, so take care to configure this setting properly.</span></span> <span data-ttu-id="c1275-156">Он доступен только в PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c1275-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="c1275-157">Установите VPN-подключения "сайт — сайт".</span><span class="sxs-lookup"><span data-stu-id="c1275-157">Establish the Site-to-Site VPN connections.</span></span>

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