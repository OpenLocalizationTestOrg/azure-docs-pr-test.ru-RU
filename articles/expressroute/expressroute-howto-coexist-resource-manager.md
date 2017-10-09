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
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="fbab8-103">Настройка параллельных подключений ExpressRoute и "сайт-сайт"</span><span class="sxs-lookup"><span data-stu-id="fbab8-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbab8-104">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fbab8-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="fbab8-105">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="fbab8-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="fbab8-106">Настройка параллельных подключений VPN типа "сеть — сеть" и ExpressRoute дает целый ряд преимуществ.</span><span class="sxs-lookup"><span data-stu-id="fbab8-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="fbab8-107">Настройка VPN сайтами как путь безопасный переход на другой ресурс для ExressRoute или использовать toosites tooconnect VPN на сайт-сайт, не подключен через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fbab8-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="fbab8-108">Оба сценария в этой статье мы рассмотрим действия tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="fbab8-109">В этой статье относится модели развертывания диспетчера ресурсов toohello и использует PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbab8-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="fbab8-110">Эта конфигурация не доступны в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fbab8-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbab8-111">Каналы ExpressRoute должен быть предварительно настроен, прежде чем выполнять приведенные ниже инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="fbab8-112">Убедитесь в том, чтобы были выполнены направляющие hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и [Настройка маршрутизации](expressroute-howto-routing-arm.md) перед продолжением работы.</span><span class="sxs-lookup"><span data-stu-id="fbab8-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="fbab8-113">Квоты и ограничения</span><span class="sxs-lookup"><span data-stu-id="fbab8-113">Limits and limitations</span></span>
* <span data-ttu-id="fbab8-114">**Транзитная маршрутизация не поддерживается.**</span><span class="sxs-lookup"><span data-stu-id="fbab8-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="fbab8-115">Нельзя настроить маршрутизацию (через Azure) между локальной сетью, подключенной к VPN типа "сеть — сеть", и локальной сетью, подключенной к ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fbab8-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="fbab8-116">**Номера SKU класса "Базовый" для шлюза не поддерживаются.**</span><span class="sxs-lookup"><span data-stu-id="fbab8-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="fbab8-117">Необходимо использовать основные SKU, отличного от шлюза для обоих hello [шлюз ExpressRoute](expressroute-about-virtual-network-gateways.md) и hello [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="fbab8-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="fbab8-118">**Поддерживается только VPN-шлюз на основе маршрутов.**</span><span class="sxs-lookup"><span data-stu-id="fbab8-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="fbab8-119">Необходимо использовать [VPN-шлюз](../vpn-gateway/vpn-gateway-about-vpngateways.md) на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="fbab8-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="fbab8-120">**Для VPN-шлюза необходимо настроить статический маршрут.**</span><span class="sxs-lookup"><span data-stu-id="fbab8-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="fbab8-121">Если локальной сети — подключенных tooboth ExpressRoute и сеть-сеть VPN, должен иметь статический маршрут настроен в вашей локальной сети tooroute hello сеть-сеть VPN подключения toohello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="fbab8-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="fbab8-122">**Шлюз ExpressRoute должен быть настроен и связан tooa канала.**</span><span class="sxs-lookup"><span data-stu-id="fbab8-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="fbab8-123">Необходимо сначала создать шлюз ExpressRoute hello и связать его tooa цепи, прежде чем добавлять hello сеть-сеть VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="fbab8-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="fbab8-124">Схемы конфигурации</span><span class="sxs-lookup"><span data-stu-id="fbab8-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="fbab8-125">Настройка VPN типа "сеть-сеть" как пути отработки отказа для ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fbab8-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="fbab8-126">VPN-подключение типа "сеть-сеть" можно настроить как службу архивации для ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fbab8-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="fbab8-127">Это относится только toovirtual сетей связанного toohello Azure частным путем пиринга.</span><span class="sxs-lookup"><span data-stu-id="fbab8-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="fbab8-128">Для служб, доступ к которым осуществляется через пиринг Azure Public или Microsoft, решения для отработки отказа на основе VPN не существует.</span><span class="sxs-lookup"><span data-stu-id="fbab8-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="fbab8-129">Hello канал ExpressRoute всегда является основной ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="fbab8-130">Поток данных проходит через путь через виртуальную Частную сеть для hello только в том случае, если происходит сбой hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fbab8-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="fbab8-131">Пока канал ExpressRoute предпочтительнее через виртуальную Частную сеть для, когда обоих маршрутах являются одинаковыми hello, Azure будет использовать hello длинного префикса соответствия toochoose hello маршрута к назначения hello пакета.</span><span class="sxs-lookup"><span data-stu-id="fbab8-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Существуют одновременно](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="fbab8-133">Настройка toosites через виртуальную Частную сеть для tooconnect, не подключен через ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fbab8-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="fbab8-134">Можно настроить сети, где некоторые узлы подключаются непосредственно tooAzure через сеть-сеть VPN, и некоторые узлы подключаются через ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fbab8-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Существуют одновременно](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="fbab8-136">Виртуальную сеть нельзя настроить как транзитный маршрутизатор.</span><span class="sxs-lookup"><span data-stu-id="fbab8-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="fbab8-137">При выборе действия toouse hello</span><span class="sxs-lookup"><span data-stu-id="fbab8-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="fbab8-138">Существует два разных набора toochoose процедуры из.</span><span class="sxs-lookup"><span data-stu-id="fbab8-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="fbab8-139">процедуры настройки Hello выбранного зависит от того, имеется ли существующей виртуальной сети, которые должны tooconnect в, или вы хотите toocreate новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="fbab8-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="fbab8-140">Я нет виртуальной сети и требуется toocreate один.</span><span class="sxs-lookup"><span data-stu-id="fbab8-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="fbab8-141">Если у вас еще нет виртуальной сети, выполните эти шаги, чтобы создать ее с помощью модели развертывания Resource Manager, а также создать подключение ExpressRoute и VPN типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="fbab8-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="fbab8-142">tooconfigure виртуальной сети, следуйте указаниям hello [toocreate новую виртуальную сеть и существующих соединений](#new).</span><span class="sxs-lookup"><span data-stu-id="fbab8-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="fbab8-143">У меня уже есть виртуальная сеть с моделью развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fbab8-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="fbab8-144">Возможно, у вас уже имеется виртуальная сеть, а также подключения к VPN типа "сеть-сеть" или к ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fbab8-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="fbab8-145">Hello [tooconfigure существующих соединений для уже существующей виртуальной сети](#add) разделе описан процесс удаления шлюза hello и создания новых ExpressRoute "и" сеть-сеть VPN-подключений.</span><span class="sxs-lookup"><span data-stu-id="fbab8-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="fbab8-146">При создании новых подключений hello, hello действия должны выполняться в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="fbab8-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="fbab8-147">Не используйте инструкции hello в других статьях toocreate, шлюзы и подключения.</span><span class="sxs-lookup"><span data-stu-id="fbab8-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="fbab8-148">В этой процедуре создания соединений, которые могут сосуществовать требует вы toodelete шлюз и настраиваете новых шлюзов.</span><span class="sxs-lookup"><span data-stu-id="fbab8-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="fbab8-149">Вы получите время простоя для подключений между организациями во время удаления и повторного создания шлюза и подключения, но не потребуется toomigrate любой из виртуальных машин и служб tooa новой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fbab8-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="fbab8-150">Виртуальные машины и службы будут иметь доступ toocommunicate out через hello балансировки нагрузки во время настройки шлюза, если они являются toodo настроенный таким образом.</span><span class="sxs-lookup"><span data-stu-id="fbab8-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="fbab8-151"><a name="new"></a>toocreate новую виртуальную сеть и существующих соединений</span><span class="sxs-lookup"><span data-stu-id="fbab8-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="fbab8-152">В этой процедуре подробно рассматривается создание виртуальной сети, а также параллельных подключений ExpressRoute и "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="fbab8-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="fbab8-153">Установите последнюю версию hello hello командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbab8-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="fbab8-154">Сведения об установке hello командлетов см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbab8-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="fbab8-155">Возможно, несколько отличаются от что вы не знакомы с Hello командлеты, которые можно использовать для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fbab8-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="fbab8-156">Указать командлеты hello toouse убедиться, что в этих инструкциях.</span><span class="sxs-lookup"><span data-stu-id="fbab8-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="fbab8-157">Войдите в учетную запись tooyour и настройка среды hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="fbab8-158">Создайте виртуальную сеть и подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="fbab8-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="fbab8-159">Дополнительные сведения о настройке виртуальной сети hello см. в разделе [конфигурации виртуальной сети Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fbab8-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="fbab8-160">Hello подсеть шлюза должна быть /27 или короткое префикс (например, /26 или /25).</span><span class="sxs-lookup"><span data-stu-id="fbab8-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="fbab8-161">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="fbab8-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="fbab8-162">Добавьте подсети.</span><span class="sxs-lookup"><span data-stu-id="fbab8-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="fbab8-163">Сохраните конфигурацию виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="fbab8-164"><a name="gw"></a>Создайте шлюз ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fbab8-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="fbab8-165">Дополнительные сведения о конфигурации шлюза hello ExpressRoute см. в разделе [шлюз ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="fbab8-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="fbab8-166">Hello GatewaySKU должно быть *Стандартная*, *HighPerformance*, или *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="fbab8-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="fbab8-167">Свяжите канал ExpressRoute toohello шлюз ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="fbab8-168">После завершения этого шага hello между локальной сетью и Azure через ExpressRoute, подключение выполняется.</span><span class="sxs-lookup"><span data-stu-id="fbab8-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="fbab8-169">Дополнительные сведения об операции связывания hello см. в разделе [tooExpressRoute связь виртуальных сетей](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="fbab8-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="fbab8-170"><a name="vpngw"></a>Далее создайте VPN-шлюз типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="fbab8-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="fbab8-171">Дополнительные сведения о конфигурации шлюза VPN hello см. в разделе [настроить виртуальную сеть с подключением сайт-сайт](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fbab8-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="fbab8-172">Hello GatewaySKU должно быть *Стандартная*, *HighPerformance*, или *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="fbab8-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="fbab8-173">Hello VpnType должен *routebased*.</span><span class="sxs-lookup"><span data-stu-id="fbab8-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="fbab8-174">Шлюз VPN Azure поддерживает протокол маршрутизации BGP.</span><span class="sxs-lookup"><span data-stu-id="fbab8-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="fbab8-175">Можно указать ASN (номер AS) для этой виртуальной сети путем добавления коммутатора hello - Asn в hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="fbab8-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="fbab8-176">Указание этого параметра не будет по умолчанию tooAS номер 65515.</span><span class="sxs-lookup"><span data-stu-id="fbab8-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="fbab8-177">Здравствуйте, BGP пиринг IP и hello как число, используемое для шлюза VPN hello в $azureVpn.BgpSettings.BgpPeeringAddress и $azureVpn.BgpSettings.Asn Azure можно найти.</span><span class="sxs-lookup"><span data-stu-id="fbab8-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="fbab8-178">Дополнительные сведения см. в статье [Настройка BGP на VPN-шлюзах Azure с помощью Azure Resource Manager и PowerShell](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fbab8-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="fbab8-179">Создайте сущность VPN-шлюза локального сайта.</span><span class="sxs-lookup"><span data-stu-id="fbab8-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="fbab8-180">Эта команда не настраивает локальный VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="fbab8-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="fbab8-181">Вместо этого позволяет tooprovide hello локального шлюза параметры, такие как общедоступный IP-адрес hello и hello локального адресного пространства, hello VPN-шлюз Azure для подключения tooit.</span><span class="sxs-lookup"><span data-stu-id="fbab8-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="fbab8-182">Если локальное устройство VPN поддерживает только статическую маршрутизацию, можно настроить статические маршруты hello в hello следующими способами:</span><span class="sxs-lookup"><span data-stu-id="fbab8-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="fbab8-183">Если локальное устройство VPN поддерживает hello BGP, и вы хотите tooenable динамической маршрутизации, необходимо tooknow hello BGP пиринг IP-адрес и hello как номер вашего локального VPN, который использует устройство.</span><span class="sxs-lookup"><span data-stu-id="fbab8-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="fbab8-184">Настройка локального устройства tooconnect toohello новые Azure VPN шлюза VPN.</span><span class="sxs-lookup"><span data-stu-id="fbab8-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="fbab8-185">Дополнительные сведения о настройке VPN-устройства см. в статье [О VPN-устройствах для подключений VPN-шлюзов типа "сеть — сеть"](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="fbab8-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="fbab8-186">Шлюз через виртуальную Частную сеть для hello ссылку на Azure toohello локального шлюза.</span><span class="sxs-lookup"><span data-stu-id="fbab8-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="fbab8-187"><a name="add"></a>tooconfigure существующих соединений для уже существующей виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="fbab8-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="fbab8-188">При наличии существующей виртуальной сети, проверьте размер подсети шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="fbab8-189">Если подсеть шлюза hello /28 или /29, необходимо сначала удалить шлюз виртуальной сети hello и увеличьте размер подсети шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="fbab8-190">Hello действия, описанные в этом разделе показывается, как toodo.</span><span class="sxs-lookup"><span data-stu-id="fbab8-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="fbab8-191">Если подсеть шлюза hello /27 или больше и виртуальной сети hello подключен через ExpressRoute, можно пропустить шаги hello и продолжить слишком[«Шаг 6 — создать шлюз VPN сеть-сеть»](#vpngw) в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="fbab8-192">При удалении существующего шлюза hello ваших локальных машинах будут потеряны hello подключения tooyour виртуальной сети, при работе в этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fbab8-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="fbab8-193">Вам потребуется tooinstall hello последняя версия командлетов Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="fbab8-194">Дополнительные сведения об установке командлетов см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbab8-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="fbab8-195">Возможно, несколько отличаются от что вы не знакомы с Hello командлеты, которые можно использовать для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fbab8-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="fbab8-196">Указать командлеты hello toouse убедиться, что в этих инструкциях.</span><span class="sxs-lookup"><span data-stu-id="fbab8-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="fbab8-197">Удалите шлюз ExpressRoute или через виртуальную Частную сеть для существующих hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="fbab8-198">Удалите подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="fbab8-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="fbab8-199">Добавьте подсеть шлюза с префиксом /27 или больше.</span><span class="sxs-lookup"><span data-stu-id="fbab8-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fbab8-200">При отсутствии недостаточно IP-адресов в вашей виртуальной сети шлюза hello tooincrease подсети размер tooadd необходимо больше пространства IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="fbab8-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="fbab8-201">Сохраните конфигурацию виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="fbab8-202">На этом этапе у вас есть виртуальная сеть без шлюзов.</span><span class="sxs-lookup"><span data-stu-id="fbab8-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="fbab8-203">toocreate новых шлюзов и завершения подключения, можно продолжить [шаг 4. Создайте шлюз ExpressRoute](#gw)в hello предшествующий набор шагов.</span><span class="sxs-lookup"><span data-stu-id="fbab8-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="fbab8-204">tooadd точка сайт конфигурации toohello VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="fbab8-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="fbab8-205">Выполните действия hello ниже tooadd точки сайтами конфигурации tooyour VPN-шлюза в установке совместной работы.</span><span class="sxs-lookup"><span data-stu-id="fbab8-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="fbab8-206">Добавьте пул адресов VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="fbab8-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="fbab8-207">Отправьте tooAzure hello VPN корневого сертификата для шлюза VPN.</span><span class="sxs-lookup"><span data-stu-id="fbab8-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="fbab8-208">В этом примере предполагается, что корневой сертификат этого hello хранятся в hello локального компьютера, где выполняются следующие командлеты PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="fbab8-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="fbab8-209">Дополнительные сведения см. в статье [Настройка подключения типа "точка — сеть" к виртуальной сети с помощью PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fbab8-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbab8-210">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbab8-210">Next steps</span></span>
<span data-ttu-id="fbab8-211">Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="fbab8-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
