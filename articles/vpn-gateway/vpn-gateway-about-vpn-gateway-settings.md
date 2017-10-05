---
title: "Параметры VPN-шлюза для распределенных подключений Azure | Документация Майкрософт"
description: "Узнайте о параметрах VPN-шлюза для шлюзов виртуальной сети Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 07aa6946b9c3994c5afc5c88837f23567b95d8a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="68d45-103">Сведения о параметрах конфигурации VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="68d45-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="68d45-104">VPN-шлюз — это разновидность шлюза виртуальной сети, который передает зашифрованный трафик между виртуальной сетью и локальным расположением через общедоступное подключение.</span><span class="sxs-lookup"><span data-stu-id="68d45-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="68d45-105">VPN-шлюз можно также использовать для передачи трафика между виртуальными сетями в магистрали Azure.</span><span class="sxs-lookup"><span data-stu-id="68d45-105">You can also use a VPN gateway to send traffic between virtual networks across the Azure backbone.</span></span>

<span data-ttu-id="68d45-106">Подключение VPN-шлюза зависит от конфигурации нескольких ресурсов, каждый из которых содержит настраиваемые параметры.</span><span class="sxs-lookup"><span data-stu-id="68d45-106">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="68d45-107">В разделах этой статьи рассматриваются ресурсы и параметры, относящиеся к VPN-шлюзу для виртуальной сети, созданной на основе модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="68d45-107">The sections in this article discuss the resources and settings that relate to a VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="68d45-108">Описания и схемы топологий для каждого варианта подключения можно найти в статье [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="68d45-108">You can find descriptions and topology diagrams for each connection solution in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="68d45-109"><a name="gwtype"></a>Типы шлюзов</span><span class="sxs-lookup"><span data-stu-id="68d45-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="68d45-110">У каждой виртуальной сети может быть только один шлюз виртуальной сети каждого типа.</span><span class="sxs-lookup"><span data-stu-id="68d45-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="68d45-111">При создании шлюза виртуальной сети необходимо убедиться, что в конфигурации указан правильный тип шлюза.</span><span class="sxs-lookup"><span data-stu-id="68d45-111">When you are creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span></span>

<span data-ttu-id="68d45-112">Для -GatewayType доступны приведенные ниже значения.</span><span class="sxs-lookup"><span data-stu-id="68d45-112">The available values for -GatewayType are:</span></span>

* <span data-ttu-id="68d45-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="68d45-113">Vpn</span></span>
* <span data-ttu-id="68d45-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="68d45-114">ExpressRoute</span></span>

<span data-ttu-id="68d45-115">Для VPN-шлюза требуется `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="68d45-115">A VPN gateway requires the `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="68d45-116">Пример:</span><span class="sxs-lookup"><span data-stu-id="68d45-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="68d45-117"><a name="gwsku"></a>SKU шлюзов</span><span class="sxs-lookup"><span data-stu-id="68d45-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-the-gateway-sku"></a><span data-ttu-id="68d45-118">Настройка номера SKU шлюза</span><span class="sxs-lookup"><span data-stu-id="68d45-118">Configure the gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="68d45-119">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="68d45-119">Azure portal</span></span>

<span data-ttu-id="68d45-120">Если для создания шлюза виртуальной сети Resource Manager используется портал Azure, выбрать SKU шлюза можно в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="68d45-120">If you use the Azure portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown.</span></span> <span data-ttu-id="68d45-121">Представленные параметры соответствуют выбранным типу шлюза и типу VPN.</span><span class="sxs-lookup"><span data-stu-id="68d45-121">The options you are presented with correspond to the Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="68d45-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68d45-122">PowerShell</span></span>

<span data-ttu-id="68d45-123">В следующем примере PowerShell используется `-GatewaySku` со значением VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="68d45-123">The following PowerShell example specifies the `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="68d45-124"><a name="resize"></a>Изменение номера SKU (размера) шлюза</span><span class="sxs-lookup"><span data-stu-id="68d45-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="68d45-125">Для повышения уровня SKU шлюза до более производительного можно воспользоваться командлетом PowerShell `Resize-AzureRmVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="68d45-125">If you want to upgrade your gateway SKU to a more powerful SKU, you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="68d45-126">С помощью этого командлета также можно перейти на более низкий уровень SKU.</span><span class="sxs-lookup"><span data-stu-id="68d45-126">You can also downgrade the gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="68d45-127">В следующем примере PowerShell показано изменение размера шлюза до SKU со значением VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="68d45-127">The following PowerShell example shows a gateway SKU being resized to VpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="68d45-128"><a name="connectiontype"></a>Типы подключения</span><span class="sxs-lookup"><span data-stu-id="68d45-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="68d45-129">В модели развертывания с помощью Resource Manager каждой конфигурации необходим определенный тип подключения шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="68d45-129">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="68d45-130">Для `-ConnectionType` в PowerShell можно указать такие значения (развертывание Resource Manager):</span><span class="sxs-lookup"><span data-stu-id="68d45-130">The available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="68d45-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="68d45-131">IPsec</span></span>
* <span data-ttu-id="68d45-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="68d45-132">Vnet2Vnet</span></span>
* <span data-ttu-id="68d45-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="68d45-133">ExpressRoute</span></span>
* <span data-ttu-id="68d45-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="68d45-134">VPNClient</span></span>

<span data-ttu-id="68d45-135">В следующем примере PowerShell создается подключение типа "сеть — сеть", для которого требуется тип *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="68d45-135">In the following PowerShell example, we create a S2S connection that requires the connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="68d45-136"><a name="vpntype"></a>Типы VPN</span><span class="sxs-lookup"><span data-stu-id="68d45-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="68d45-137">При создании шлюза виртуальной сети для конфигурации VPN-шлюза необходимо указать тип VPN.</span><span class="sxs-lookup"><span data-stu-id="68d45-137">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="68d45-138">Выбор типа VPN зависит от топологии подключений, которую вы хотите создать.</span><span class="sxs-lookup"><span data-stu-id="68d45-138">The VPN type that you choose depends on the connection topology that you want to create.</span></span> <span data-ttu-id="68d45-139">Например, для подключения типа "точка — сеть" требуется тип VPN на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="68d45-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="68d45-140">Тип VPN может также зависеть от используемого оборудования.</span><span class="sxs-lookup"><span data-stu-id="68d45-140">A VPN type can also depend on the hardware that you are using.</span></span> <span data-ttu-id="68d45-141">Для конфигураций "сеть — сеть" требуется VPN-устройство.</span><span class="sxs-lookup"><span data-stu-id="68d45-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="68d45-142">Некоторые VPN-устройства поддерживают только определенный тип VPN.</span><span class="sxs-lookup"><span data-stu-id="68d45-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="68d45-143">Выбранный тип VPN должен удовлетворять всем требованиям к подключению решения, которое вы хотите создать.</span><span class="sxs-lookup"><span data-stu-id="68d45-143">The VPN type you select must satisfy all the connection requirements for the solution you want to create.</span></span> <span data-ttu-id="68d45-144">Например, если вы хотите создать подключение VPN-шлюза типа "сеть — сеть" и подключение VPN-шлюза типа "точка — сеть" для одной и той же виртуальной сети, то вам следует использовать тип VPN *RouteBased* , так как он необходим для подключения типа "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="68d45-144">For example, if you want to create a S2S VPN gateway connection and a P2S VPN gateway connection for the same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="68d45-145">Необходимо также проверить, поддерживает ли ваше VPN-устройство VPN-подключение на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="68d45-145">You would also need to verify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="68d45-146">После создания шлюза виртуальной сети изменить тип VPN невозможно.</span><span class="sxs-lookup"><span data-stu-id="68d45-146">Once a virtual network gateway has been created, you can't change the VPN type.</span></span> <span data-ttu-id="68d45-147">Для этого потребуется удалить шлюз виртуальной сети и создать новый.</span><span class="sxs-lookup"><span data-stu-id="68d45-147">You have to delete the virtual network gateway and create a new one.</span></span> <span data-ttu-id="68d45-148">Существует два типа VPN:</span><span class="sxs-lookup"><span data-stu-id="68d45-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="68d45-149">В следующем примере PowerShell используется `-VpnType` со значением *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="68d45-149">The following PowerShell example specifies the `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="68d45-150">При создании шлюза необходимо убедиться, что в конфигурации указано правильное значение -VpnType.</span><span class="sxs-lookup"><span data-stu-id="68d45-150">When you are creating a gateway, you must make sure that the -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="68d45-151"><a name="requirements"></a>Требования к шлюзу</span><span class="sxs-lookup"><span data-stu-id="68d45-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="68d45-152"><a name="gwsub"></a>Подсеть шлюза</span><span class="sxs-lookup"><span data-stu-id="68d45-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="68d45-153">Прежде чем создать VPN-шлюз, необходимо создать подсеть для него.</span><span class="sxs-lookup"><span data-stu-id="68d45-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="68d45-154">Подсеть шлюза содержит IP-адреса, которые используют виртуальные машины и службы шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="68d45-154">The gateway subnet contains the IP addresses that the virtual network gateway VMs and services use.</span></span> <span data-ttu-id="68d45-155">При создании шлюза виртуальной сети его виртуальные машины развертываются в подсети шлюза и на них настраиваются необходимые параметры VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="68d45-155">When you create your virtual network gateway, gateway VMs are deployed to the gateway subnet and configured with the required VPN gateway settings.</span></span> <span data-ttu-id="68d45-156">Ни в коем случае не следует развертывать в подсети шлюза что-либо еще (например, дополнительные виртуальные машины).</span><span class="sxs-lookup"><span data-stu-id="68d45-156">You must never deploy anything else (for example, additional VMs) to the gateway subnet.</span></span> <span data-ttu-id="68d45-157">Чтобы подсеть шлюза работала правильно, ее нужно назвать GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="68d45-157">The gateway subnet must be named 'GatewaySubnet' to work properly.</span></span> <span data-ttu-id="68d45-158">Такое имя позволяет Azure определить, что это подсеть для развертывания виртуальных машин и служб шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="68d45-158">Naming the gateway subnet 'GatewaySubnet' lets Azure know that this is the subnet to deploy the virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="68d45-159">При создании подсети шлюза указывается количество IP-адресов, которое содержит подсеть.</span><span class="sxs-lookup"><span data-stu-id="68d45-159">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="68d45-160">IP-адреса в подсети шлюза выделяются виртуальным машинам и службам шлюза.</span><span class="sxs-lookup"><span data-stu-id="68d45-160">The IP addresses in the gateway subnet are allocated to the gateway VMs and gateway services.</span></span> <span data-ttu-id="68d45-161">Некоторым конфигурациям требуется больше IP-адресов, чем прочим.</span><span class="sxs-lookup"><span data-stu-id="68d45-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="68d45-162">Просмотрите инструкции к конфигурации, которую требуется создать, и убедитесь, что создаваемая подсеть шлюза соответствует указанным требованиям.</span><span class="sxs-lookup"><span data-stu-id="68d45-162">Look at the instructions for the configuration that you want to create and verify that the gateway subnet you want to create meets those requirements.</span></span> <span data-ttu-id="68d45-163">Кроме того, необходимо убедиться, что подсеть шлюза содержит достаточно IP-адресов для дополнительных конфигураций, которые могут быть добавлены в будущем.</span><span class="sxs-lookup"><span data-stu-id="68d45-163">Additionally, you may want to make sure your gateway subnet contains enough IP addresses to accommodate possible future additional configurations.</span></span> <span data-ttu-id="68d45-164">Хотя можно создать подсеть шлюза всего лишь с размером /29, мы советуем создавать подсети с размером /28 или больше (/28, /27, /26 и т. д.).</span><span class="sxs-lookup"><span data-stu-id="68d45-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="68d45-165">Таким образом, если в будущем вы добавите какие-либо функциональные возможности, то вам не придется разделять шлюз и удалять, а затем повторно создавать подсеть шлюза, чтобы получить больше IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="68d45-165">That way, if you add functionality in the future, you won't have to tear your gateway, then delete and recreate the gateway subnet to allow for more IP addresses.</span></span>

<span data-ttu-id="68d45-166">В примере PowerShell для Resource Manager ниже показана подсеть шлюза GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="68d45-166">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="68d45-167">Здесь приведена нотация CIDR, указывающая размер /27, при котором можно использовать достаточно IP-адресов для большинства существующих конфигураций.</span><span class="sxs-lookup"><span data-stu-id="68d45-167">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="68d45-168"><a name="lng"></a>Локальные сетевые шлюзы</span><span class="sxs-lookup"><span data-stu-id="68d45-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="68d45-169">При создании конфигурации VPN-шлюза нередко шлюз локальной сети представляет ваше локальное расположение.</span><span class="sxs-lookup"><span data-stu-id="68d45-169">When creating a VPN gateway configuration, the local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="68d45-170">В классической модели развертывания шлюз локальной сети называется "локальным сайтом".</span><span class="sxs-lookup"><span data-stu-id="68d45-170">In the classic deployment model, the local network gateway was referred to as a Local Site.</span></span> 

<span data-ttu-id="68d45-171">Для локального сетевого шлюза следует задать имя и общий IP-адрес локального VPN-устройства, а также указать префиксы адресов, принадлежащие к локальному расположению.</span><span class="sxs-lookup"><span data-stu-id="68d45-171">You give the local network gateway a name, the public IP address of the on-premises VPN device, and specify the address prefixes that are located on the on-premises location.</span></span> <span data-ttu-id="68d45-172">Azure проверяет наличие сетевого трафика по префиксам адресов назначения, учитывает конфигурацию, указанную для локального сетевого шлюза, и соответствующим образом направляет пакеты.</span><span class="sxs-lookup"><span data-stu-id="68d45-172">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="68d45-173">Можно также указать шлюзы локальной сети для конфигураций типа "виртуальная сеть — виртуальная сеть", использующих подключение к VPN-шлюзу.</span><span class="sxs-lookup"><span data-stu-id="68d45-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="68d45-174">Следующий пример PowerShell создает шлюз локальной сети.</span><span class="sxs-lookup"><span data-stu-id="68d45-174">The following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="68d45-175">Иногда возникает необходимость изменить параметры локального сетевого шлюза.</span><span class="sxs-lookup"><span data-stu-id="68d45-175">Sometimes you need to modify the local network gateway settings.</span></span> <span data-ttu-id="68d45-176">Например, при добавлении или изменении диапазона адресов, либо при изменении IP-адреса VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="68d45-176">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span></span> <span data-ttu-id="68d45-177">Для классической виртуальной сети эти параметры можно изменить на классическом портале, на странице "Локальные сети".</span><span class="sxs-lookup"><span data-stu-id="68d45-177">For a classic VNet, you can change these settings in the classic portal on the Local Networks page.</span></span> <span data-ttu-id="68d45-178">В случае использования Resource Manager ознакомьтесь с разделом [Изменение параметров шлюза локальной сети с помощью PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="68d45-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="68d45-179"><a name="resources"></a>Интерфейсы REST API и командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="68d45-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="68d45-180">Дополнительные технические материалы и специальные требования к синтаксису, действующие при использовании интерфейсов REST API, командлетов PowerShell или Azure CLI для настройки конфигураций VPN-шлюзов, доступны на приведенных ниже страницах.</span><span class="sxs-lookup"><span data-stu-id="68d45-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="68d45-181">**Классический**</span><span class="sxs-lookup"><span data-stu-id="68d45-181">**Classic**</span></span> | <span data-ttu-id="68d45-182">**Диспетчер ресурсов**</span><span class="sxs-lookup"><span data-stu-id="68d45-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="68d45-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68d45-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="68d45-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68d45-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="68d45-185">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="68d45-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="68d45-186">REST API</span><span class="sxs-lookup"><span data-stu-id="68d45-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="68d45-187">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="68d45-187">Not supported</span></span> | [<span data-ttu-id="68d45-188">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="68d45-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="68d45-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68d45-189">Next steps</span></span>

<span data-ttu-id="68d45-190">Дополнительные сведения о доступных конфигурациях подключений см. в статье [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="68d45-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>