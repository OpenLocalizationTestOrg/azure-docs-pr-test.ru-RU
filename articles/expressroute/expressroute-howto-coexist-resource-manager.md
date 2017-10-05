---
title: "Настройка сосуществующих подключений VPN типа ExpressRoute и \"сеть — сеть\" с помощью модели Azure Resource Manager | Документация Майкрософт"
description: "В этой статье описывается настройка параллельных подключений ExpressRoute и VPN-подключений типа \"сеть — сеть\" для модели развертывания Resource Manager."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: b29147a37f9a90fc80e16b350ac9b91daac1d7f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="91a3c-103">Настройка параллельных подключений ExpressRoute и "сайт-сайт"</span><span class="sxs-lookup"><span data-stu-id="91a3c-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91a3c-104">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="91a3c-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="91a3c-105">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="91a3c-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="91a3c-106">Настройка параллельных подключений VPN типа "сеть — сеть" и ExpressRoute дает целый ряд преимуществ.</span><span class="sxs-lookup"><span data-stu-id="91a3c-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="91a3c-107">Вы можете настроить VPN типа "сеть — сеть" как защищенный путь отработки отказа для ExressRoute или использовать эту VPN для подключения к сайтам, не подключенным через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91a3c-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="91a3c-108">В этой статье мы рассмотрим порядок действия в каждом из этих вариантов.</span><span class="sxs-lookup"><span data-stu-id="91a3c-108">We cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="91a3c-109">Эта статья посвящена модели развертывания Resource Manager. Кроме того, в ней используется PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91a3c-109">This article applies to the Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="91a3c-110">Эта конфигурация недоступна на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="91a3c-110">This configuration is not available in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91a3c-111">Перед выполнением приведенных ниже инструкций необходимо настроить каналы ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91a3c-111">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="91a3c-112">Прежде чем продолжить, убедитесь, что выполнили все инструкции по [созданию канала ExpressRoute](expressroute-howto-circuit-arm.md) и [настройке маршрутизации](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-112">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="91a3c-113">Квоты и ограничения</span><span class="sxs-lookup"><span data-stu-id="91a3c-113">Limits and limitations</span></span>
* <span data-ttu-id="91a3c-114">**Транзитная маршрутизация не поддерживается.**</span><span class="sxs-lookup"><span data-stu-id="91a3c-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="91a3c-115">Нельзя настроить маршрутизацию (через Azure) между локальной сетью, подключенной к VPN типа "сеть — сеть", и локальной сетью, подключенной к ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91a3c-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="91a3c-116">**Номера SKU класса "Базовый" для шлюза не поддерживаются.**</span><span class="sxs-lookup"><span data-stu-id="91a3c-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="91a3c-117">Используйте для [ExpressRoute](expressroute-about-virtual-network-gateways.md) и [VPN-шлюза](../vpn-gateway/vpn-gateway-about-vpngateways.md) номера SKU другого класса.</span><span class="sxs-lookup"><span data-stu-id="91a3c-117">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="91a3c-118">**Поддерживается только VPN-шлюз на основе маршрутов.**</span><span class="sxs-lookup"><span data-stu-id="91a3c-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="91a3c-119">Необходимо использовать [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md) на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="91a3c-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="91a3c-120">**Для VPN-шлюза необходимо настроить статический маршрут.**</span><span class="sxs-lookup"><span data-stu-id="91a3c-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="91a3c-121">Если локальная сеть подключена и к ExpressRoute, и к VPN типа "сеть — сеть", необходимо использовать статический маршрут, настроенный в локальной сети для маршрутизации VPN-подключения типа "сеть — сеть" к Интернету.</span><span class="sxs-lookup"><span data-stu-id="91a3c-121">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="91a3c-122">**Сначала шлюз ExpressRoute нужно настроить, а затем связать с каналом.**</span><span class="sxs-lookup"><span data-stu-id="91a3c-122">**ExpressRoute gateway must be configured first and linked to a circuit.**</span></span> <span data-ttu-id="91a3c-123">Сначала нужно создать шлюз ExpressRoute, связать его с каналом, а затем добавить шлюз VPN типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="91a3c-123">You must create the ExpressRoute gateway first and link it to a circuit before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="91a3c-124">Схемы конфигурации</span><span class="sxs-lookup"><span data-stu-id="91a3c-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="91a3c-125">Настройка VPN типа "сеть-сеть" как пути отработки отказа для ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="91a3c-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="91a3c-126">VPN-подключение типа "сеть-сеть" можно настроить как службу архивации для ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91a3c-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="91a3c-127">Это относится только к виртуальным сетям, привязанным к пути пиринга Azure Private.</span><span class="sxs-lookup"><span data-stu-id="91a3c-127">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="91a3c-128">Для служб, доступ к которым осуществляется через пиринг Azure Public или Microsoft, решения для отработки отказа на основе VPN не существует.</span><span class="sxs-lookup"><span data-stu-id="91a3c-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="91a3c-129">Канал ExpressRoute всегда является основной ссылкой.</span><span class="sxs-lookup"><span data-stu-id="91a3c-129">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="91a3c-130">Данные передаются по пути VPN типа "сеть — сеть", только если канал ExpressRoute не справляется с этой задачей.</span><span class="sxs-lookup"><span data-stu-id="91a3c-130">Data flows through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="91a3c-131">Хотя канал ExpressRoute лучше использовать для VPN типа "сеть — сеть", когда оба маршрута одинаковы, Azure будет выбирать маршрут для назначения пакета по совпадению самого длинного префикса.</span><span class="sxs-lookup"><span data-stu-id="91a3c-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Существуют одновременно](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="91a3c-133">Настройка VPN типа "сеть-сеть" для подключения к сайтам, не подключенным через ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="91a3c-133">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="91a3c-134">Сети можно настроить таким образом, чтобы одни из них подключались непосредственно к Azure по VPN типа "сеть-сеть", а другие — через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91a3c-134">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Существуют одновременно](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="91a3c-136">Виртуальную сеть нельзя настроить как транзитный маршрутизатор.</span><span class="sxs-lookup"><span data-stu-id="91a3c-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="91a3c-137">Выбор действий для использования</span><span class="sxs-lookup"><span data-stu-id="91a3c-137">Selecting the steps to use</span></span>
<span data-ttu-id="91a3c-138">Существует два типа процедур.</span><span class="sxs-lookup"><span data-stu-id="91a3c-138">There are two different sets of procedures to choose from.</span></span> <span data-ttu-id="91a3c-139">Выбор процедуры настройки зависит от того, существует ли уже виртуальная сеть, к которой необходимо подключиться, или требуется создать ее.</span><span class="sxs-lookup"><span data-stu-id="91a3c-139">The configuration procedure that you select depends on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="91a3c-140">У меня нет виртуальной сети, и мне нужно ее создать.</span><span class="sxs-lookup"><span data-stu-id="91a3c-140">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="91a3c-141">Если у вас еще нет виртуальной сети, выполните эти шаги, чтобы создать ее с помощью модели развертывания Resource Manager, а также создать подключение ExpressRoute и VPN типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="91a3c-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="91a3c-142">Чтобы настроить виртуальную сеть, выполните шаги, описанные в разделе [Создание виртуальной сети и параллельных подключений](#new).</span><span class="sxs-lookup"><span data-stu-id="91a3c-142">To configure a virtual network, follow the steps in [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="91a3c-143">У меня уже есть виртуальная сеть с моделью развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="91a3c-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="91a3c-144">Возможно, у вас уже имеется виртуальная сеть, а также подключения к VPN типа "сеть-сеть" или к ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91a3c-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="91a3c-145">В разделе [Настройка параллельных подключений для существующей виртуальной сети](#add) представлены пошаговые инструкции по удалению шлюза и созданию подключений ExpressRoute и VPN типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="91a3c-145">The [To configure coexisting connections for an already existing VNet](#add) section walks you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="91a3c-146">Все шаги по созданию параллельных подключений необходимо выполнять в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="91a3c-146">When creating the new connections, the steps must be completed in a specific order.</span></span> <span data-ttu-id="91a3c-147">При создании шлюзов и подключений не пользуйтесь инструкциями, взятыми из других статей.</span><span class="sxs-lookup"><span data-stu-id="91a3c-147">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="91a3c-148">Чтобы создать параллельные подключения по этой процедуре, необходимо удалить существующий шлюз и настроить новые.</span><span class="sxs-lookup"><span data-stu-id="91a3c-148">In this procedure, creating connections that can coexist requires you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="91a3c-149">Подключение между организациями прервется на время удаления и повторного создания шлюза и подключений, но вам не потребуется выполнять миграцию всех виртуальных машин и служб в новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="91a3c-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="91a3c-150">Виртуальные машины и службы смогут по-прежнему осуществлять связь через балансировщик нагрузки во время настройки шлюза, если они настроены соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="91a3c-150">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="91a3c-151"><a name="new"></a>Создание новой виртуальной сети и параллельных подключений</span><span class="sxs-lookup"><span data-stu-id="91a3c-151"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="91a3c-152">В этой процедуре подробно рассматривается создание виртуальной сети, а также параллельных подключений ExpressRoute и "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="91a3c-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="91a3c-153">Установите последнюю версию командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91a3c-153">Install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="91a3c-154">Дополнительные сведения об установке командлетов см. в статье об [установке и настройке Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91a3c-154">For information about installing the cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="91a3c-155">Командлеты, которые будут использоваться для этой конфигурации, могут немного отличаться от уже знакомых вам.</span><span class="sxs-lookup"><span data-stu-id="91a3c-155">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="91a3c-156">Обязательно используйте командлеты, указанные в инструкциях.</span><span class="sxs-lookup"><span data-stu-id="91a3c-156">Be sure to use the cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="91a3c-157">Войдите в учетную запись и настройте среду.</span><span class="sxs-lookup"><span data-stu-id="91a3c-157">Log in to your account and set up the environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="91a3c-158">Создайте виртуальную сеть и подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="91a3c-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="91a3c-159">Дополнительные сведения о настройке виртуальной сети см. в статье [Создание виртуальной сети с помощью PowerShell](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-159">For more information about the virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="91a3c-160">Подсеть шлюза должна иметь префикс /27 или более короткий префикс (например, /26 или /25).</span><span class="sxs-lookup"><span data-stu-id="91a3c-160">The Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="91a3c-161">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="91a3c-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="91a3c-162">Добавьте подсети.</span><span class="sxs-lookup"><span data-stu-id="91a3c-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="91a3c-163">Сохраните конфигурацию виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="91a3c-163">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="91a3c-164"><a name="gw"></a>Создайте шлюз ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91a3c-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="91a3c-165">Дополнительные сведения о настройке шлюза ExpressRoute см. в статье [Настройка шлюза виртуальной сети для ExpressRoute с помощью диспетчера ресурсов и PowerShell](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-165">For more information about the ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="91a3c-166">Параметр GatewaySKU должен иметь значение *Standard*, *HighPerformance* или *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="91a3c-166">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="91a3c-167">Свяжите шлюз ExpressRoute с каналом ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91a3c-167">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="91a3c-168">После выполнения этого действия подключение локальной сети к Azure через ExpressRoute будет установлено.</span><span class="sxs-lookup"><span data-stu-id="91a3c-168">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="91a3c-169">Дополнительные сведения об операции связывания см. в статье [Связывание виртуальной сети с каналом ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-169">For more information about the link operation, see [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="91a3c-170"><a name="vpngw"></a>Далее создайте VPN-шлюз типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="91a3c-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="91a3c-171">Дополнительные сведения о настройке VPN-шлюза см. в статье [Создание виртуальной сети с подключением типа "сеть — сеть" с помощью PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-171">For more information about the VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="91a3c-172">Параметр GatewaySKU должен иметь значение *Standard*, *HighPerformance* или *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="91a3c-172">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="91a3c-173">Параметр VpnType должен иметь значение *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="91a3c-173">The VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="91a3c-174">Шлюз VPN Azure поддерживает протокол маршрутизации BGP.</span><span class="sxs-lookup"><span data-stu-id="91a3c-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="91a3c-175">Для этой виртуальной сети можно указать ASN (номер AS), добавив параметр -Asn в команду ниже.</span><span class="sxs-lookup"><span data-stu-id="91a3c-175">You can specify ASN (AS Number) for that Virtual Network by adding the -Asn switch in the following command.</span></span> <span data-ttu-id="91a3c-176">Без этого параметра номер AS получит значение по умолчанию — 65515.</span><span class="sxs-lookup"><span data-stu-id="91a3c-176">Not specifying that parameter will default to AS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="91a3c-177">IP-адрес пиринга BGP и номер AS, используемый Azure для VPN-шлюза, можно найти в атрибутах $azureVpn.BgpSettings.BgpPeeringAddress и $azureVpn.BgpSettings.Asn.</span><span class="sxs-lookup"><span data-stu-id="91a3c-177">You can find the BGP peering IP and the AS number that Azure uses for the VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="91a3c-178">Дополнительные сведения см. в статье [Настройка BGP на VPN-шлюзах Azure с помощью Azure Resource Manager и PowerShell](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="91a3c-179">Создайте сущность VPN-шлюза локального сайта.</span><span class="sxs-lookup"><span data-stu-id="91a3c-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="91a3c-180">Эта команда не настраивает локальный VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="91a3c-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="91a3c-181">Она только позволяет указать параметры локального шлюза, такие как общедоступный IP-адрес и локальное адресное пространство, чтобы VPN-шлюз Azure мог подключиться к нему.</span><span class="sxs-lookup"><span data-stu-id="91a3c-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
    <span data-ttu-id="91a3c-182">Если локальное VPN-устройство поддерживает только статическую маршрутизацию, статические маршруты можно настроить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="91a3c-182">If your local VPN device only supports static routing, you can configure the static routes in the following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="91a3c-183">Если локальное VPN-устройство поддерживает протокол BGP, чтобы включить динамическую маршрутизацию, необходимо знать используемый этим устройством IP-адрес пиринга BGP и номер AS.</span><span class="sxs-lookup"><span data-stu-id="91a3c-183">If your local VPN device supports the BGP and you want to enable dynamic routing, you need to know the BGP peering IP and the AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="91a3c-184">Настройте локальное VPN-устройство для подключения к новому VPN-шлюзу Azure.</span><span class="sxs-lookup"><span data-stu-id="91a3c-184">Configure your local VPN device to connect to the new Azure VPN gateway.</span></span> <span data-ttu-id="91a3c-185">Дополнительные сведения о настройке VPN-устройства см. в статье [О VPN-устройствах для подключений VPN-шлюзов типа "сеть — сеть"](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="91a3c-186">Свяжите VPN-шлюз к сети типа "сеть-сеть" в Azure с локальным шлюзом.</span><span class="sxs-lookup"><span data-stu-id="91a3c-186">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="91a3c-187"><a name="add"></a>Настройка параллельных подключений для существующей виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="91a3c-187"><a name="add"></a>To configure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="91a3c-188">При наличии существующей виртуальной сети проверьте размер подсети шлюза.</span><span class="sxs-lookup"><span data-stu-id="91a3c-188">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="91a3c-189">Если размер подсети шлюза — /28 или /29, необходимо сначала удалить шлюз виртуальной сети и увеличить размер подсети шлюза.</span><span class="sxs-lookup"><span data-stu-id="91a3c-189">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="91a3c-190">В этом разделе показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="91a3c-190">The steps in this section show you how to do that.</span></span>

<span data-ttu-id="91a3c-191">Если размер подсети шлюза — /27 или больше, а виртуальная сеть подключается с помощью ExpressRoute, можно пропустить описанные ниже шаги и перейти к шагу 6 ( [Создание VPN-шлюза подключения типа "сеть — сеть"](#vpngw) ) в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="91a3c-191">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="91a3c-192">При удалении существующего шлюза локальные пользователи потеряют подключение к виртуальной сети на время выполнения этой настройки.</span><span class="sxs-lookup"><span data-stu-id="91a3c-192">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="91a3c-193">Вам потребуется установить последнюю версию командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91a3c-193">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="91a3c-194">Дополнительные сведения об установке командлетов см. в статье об [установке и настройке Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91a3c-194">For more information about installing cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="91a3c-195">Командлеты, которые будут использоваться для этой конфигурации, могут немного отличаться от уже знакомых вам.</span><span class="sxs-lookup"><span data-stu-id="91a3c-195">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="91a3c-196">Обязательно используйте командлеты, указанные в инструкциях.</span><span class="sxs-lookup"><span data-stu-id="91a3c-196">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="91a3c-197">Удалите для сети типа "сеть — сеть" существующий VPN-шлюз или шлюз ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="91a3c-197">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="91a3c-198">Удалите подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="91a3c-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="91a3c-199">Добавьте подсеть шлюза с префиксом /27 или больше.</span><span class="sxs-lookup"><span data-stu-id="91a3c-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="91a3c-200">Если в виртуальной сети недостаточно свободных IP-адресов для увеличения размера подсети шлюза, необходимо добавить дополнительные пространства IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="91a3c-200">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="91a3c-201">Сохраните конфигурацию виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="91a3c-201">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="91a3c-202">На этом этапе у вас есть виртуальная сеть без шлюзов.</span><span class="sxs-lookup"><span data-stu-id="91a3c-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="91a3c-203">Чтобы создать новые шлюзы и завершить подключение, перейдите к шагу 4 ( [Создайте шлюз ExpressRoute](#gw)) из предыдущего раздела.</span><span class="sxs-lookup"><span data-stu-id="91a3c-203">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a><span data-ttu-id="91a3c-204">Добавление конфигурации "точка — сеть" к VPN-шлюзу</span><span class="sxs-lookup"><span data-stu-id="91a3c-204">To add point-to-site configuration to the VPN gateway</span></span>
<span data-ttu-id="91a3c-205">Чтобы добавить конфигурацию "точка — сеть" к VPN-шлюзу при настройке параллельных подключений, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="91a3c-205">You can follow the steps below to add Point-to-Site configuration to your VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="91a3c-206">Добавьте пул адресов VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="91a3c-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="91a3c-207">Отправьте корневой сертификат VPN в Azure для VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="91a3c-207">Upload the VPN root certificate to Azure for your VPN gateway.</span></span> <span data-ttu-id="91a3c-208">В этом примере подразумевается, что корневой сертификат хранится на локальном компьютере, где выполняются следующие командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91a3c-208">In this example, it's assumed that the root certificate is stored in the local machine where the following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="91a3c-209">Дополнительные сведения см. в статье [Настройка подключения типа "точка — сеть" к виртуальной сети с помощью PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91a3c-210">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91a3c-210">Next steps</span></span>
<span data-ttu-id="91a3c-211">Дополнительные сведения об ExpressRoute см. в статье [Вопросы и ответы по ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-211">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
