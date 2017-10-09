---
title: "Параметры шлюза aaaVPN для соединения с Azure между организациями | Документы Microsoft"
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
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="24eb8-103">Сведения о параметрах конфигурации VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="24eb8-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="24eb8-104">VPN-шлюз — это разновидность шлюза виртуальной сети, который передает зашифрованный трафик между виртуальной сетью и локальным расположением через общедоступное подключение.</span><span class="sxs-lookup"><span data-stu-id="24eb8-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="24eb8-105">Также можно использовать VPN-шлюз toosend трафика между виртуальными сетями через hello Azure магистрали.</span><span class="sxs-lookup"><span data-stu-id="24eb8-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="24eb8-106">Шлюз VPN-подключения зависит от конфигурации hello несколько ресурсов, каждый из которых содержит настраиваемые параметры.</span><span class="sxs-lookup"><span data-stu-id="24eb8-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="24eb8-107">Hello в этой статье описываются hello ресурсы и параметры, связанные tooa VPN-шлюз для виртуальной сети, созданной в модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="24eb8-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="24eb8-108">Можно найти описания и схемы топологии для каждого подключения решения в hello [о VPN-шлюз](vpn-gateway-about-vpngateways.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="24eb8-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="24eb8-109"><a name="gwtype"></a>Типы шлюзов</span><span class="sxs-lookup"><span data-stu-id="24eb8-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="24eb8-110">У каждой виртуальной сети может быть только один шлюз виртуальной сети каждого типа.</span><span class="sxs-lookup"><span data-stu-id="24eb8-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="24eb8-111">При создании шлюза виртуальной сети, необходимо проверить правильность hello типа шлюза для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="24eb8-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="24eb8-112">могут Hello доступные значения — тип шлюза.</span><span class="sxs-lookup"><span data-stu-id="24eb8-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="24eb8-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="24eb8-113">Vpn</span></span>
* <span data-ttu-id="24eb8-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="24eb8-114">ExpressRoute</span></span>

<span data-ttu-id="24eb8-115">VPN-шлюза требует hello `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="24eb8-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="24eb8-116">Пример:</span><span class="sxs-lookup"><span data-stu-id="24eb8-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="24eb8-117"><a name="gwsku"></a>SKU шлюзов</span><span class="sxs-lookup"><span data-stu-id="24eb8-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="24eb8-118">Настройка шлюза hello SKU</span><span class="sxs-lookup"><span data-stu-id="24eb8-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="24eb8-119">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="24eb8-119">Azure portal</span></span>

<span data-ttu-id="24eb8-120">Если вы используете hello Azure портала toocreate шлюз виртуальной сети диспетчер ресурсов, можно выбрать номер SKU шлюза hello с помощью раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="24eb8-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="24eb8-121">Параметры Hello решаемой соответствуют toohello тип шлюза и выбранного типа VPN.</span><span class="sxs-lookup"><span data-stu-id="24eb8-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="24eb8-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24eb8-122">PowerShell</span></span>

<span data-ttu-id="24eb8-123">Hello PowerShell пример указывает hello `-GatewaySku` как VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="24eb8-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="24eb8-124"><a name="resize"></a>Изменение номера SKU (размера) шлюза</span><span class="sxs-lookup"><span data-stu-id="24eb8-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="24eb8-125">Если требуется tooupgrade вашей tooa SKU шлюза SKU более широкими возможностями, можно использовать hello `Resize-AzureRmVirtualNetworkGateway` командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24eb8-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="24eb8-126">Также можно понизить размер SKU шлюза hello, с помощью этого командлета.</span><span class="sxs-lookup"><span data-stu-id="24eb8-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="24eb8-127">Следующий пример PowerShell Hello показывает, что шлюз SKU изменяющего tooVpnGw2.</span><span class="sxs-lookup"><span data-stu-id="24eb8-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="24eb8-128"><a name="connectiontype"></a>Типы подключения</span><span class="sxs-lookup"><span data-stu-id="24eb8-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="24eb8-129">В модели развертывания диспетчера ресурсов hello каждой конфигурации требуется тип подключения шлюза конкретной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="24eb8-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="24eb8-130">Hello доступные PowerShell диспетчера ресурсов значения `-ConnectionType` являются:</span><span class="sxs-lookup"><span data-stu-id="24eb8-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="24eb8-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="24eb8-131">IPsec</span></span>
* <span data-ttu-id="24eb8-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="24eb8-132">Vnet2Vnet</span></span>
* <span data-ttu-id="24eb8-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="24eb8-133">ExpressRoute</span></span>
* <span data-ttu-id="24eb8-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="24eb8-134">VPNClient</span></span>

<span data-ttu-id="24eb8-135">В следующем примере PowerShell hello, мы создадим S2S подключение, требующее тип подключения hello *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="24eb8-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="24eb8-136"><a name="vpntype"></a>Типы VPN</span><span class="sxs-lookup"><span data-stu-id="24eb8-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="24eb8-137">При создании hello шлюз виртуальной сети для настройки шлюза VPN, необходимо указать тип VPN.</span><span class="sxs-lookup"><span data-stu-id="24eb8-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="24eb8-138">Hello Выбор типа VPN зависит от топологии hello подключения, которые должны toocreate.</span><span class="sxs-lookup"><span data-stu-id="24eb8-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="24eb8-139">Например, для подключения типа "точка — сеть" требуется тип VPN на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="24eb8-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="24eb8-140">Тип VPN также может зависеть от оборудования hello, в которых используется.</span><span class="sxs-lookup"><span data-stu-id="24eb8-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="24eb8-141">Для конфигураций "сеть — сеть" требуется VPN-устройство.</span><span class="sxs-lookup"><span data-stu-id="24eb8-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="24eb8-142">Некоторые VPN-устройства поддерживают только определенный тип VPN.</span><span class="sxs-lookup"><span data-stu-id="24eb8-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="24eb8-143">Hello выбранного типа VPN должен удовлетворять всем требованиям hello соединения для решения hello необходимом toocreate.</span><span class="sxs-lookup"><span data-stu-id="24eb8-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="24eb8-144">Например, если требуется toocreate S2S VPN-подключения шлюза и подключение шлюза P2S VPN hello одной виртуальной сети, используется тип VPN *routebased* так, как P2S требуется тип routebased VPN.</span><span class="sxs-lookup"><span data-stu-id="24eb8-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="24eb8-145">Необходимо также tooverify, что VPN-устройства поддерживается routebased VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="24eb8-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="24eb8-146">После создания шлюза виртуальной сети невозможно изменить тип VPN hello.</span><span class="sxs-lookup"><span data-stu-id="24eb8-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="24eb8-147">У вас есть toodelete hello шлюз виртуальной сети и создать новую.</span><span class="sxs-lookup"><span data-stu-id="24eb8-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="24eb8-148">Существует два типа VPN:</span><span class="sxs-lookup"><span data-stu-id="24eb8-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="24eb8-149">Hello PowerShell пример указывает hello `-VpnType` как *routebased*.</span><span class="sxs-lookup"><span data-stu-id="24eb8-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="24eb8-150">При создании шлюз, убедитесь, что hello - VpnType подходит для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="24eb8-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="24eb8-151"><a name="requirements"></a>Требования к шлюзу</span><span class="sxs-lookup"><span data-stu-id="24eb8-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="24eb8-152"><a name="gwsub"></a>Подсеть шлюза</span><span class="sxs-lookup"><span data-stu-id="24eb8-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="24eb8-153">Прежде чем создать VPN-шлюз, необходимо создать подсеть для него.</span><span class="sxs-lookup"><span data-stu-id="24eb8-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="24eb8-154">подсеть шлюза Hello содержит hello IP-адреса шлюза виртуальной сети, hello виртуальные машины и службы используют.</span><span class="sxs-lookup"><span data-stu-id="24eb8-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="24eb8-155">При создании шлюз виртуальной сети шлюза виртуальных машин, развернутых toohello подсеть шлюза и настроены параметры шлюза VPN требуется hello.</span><span class="sxs-lookup"><span data-stu-id="24eb8-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="24eb8-156">Что-либо еще, (например, дополнительные виртуальные машины) подсеть шлюза toohello никогда не следует развернуть.</span><span class="sxs-lookup"><span data-stu-id="24eb8-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="24eb8-157">подсеть шлюза Hello должен называться «GatewaySubnet» toowork должным образом.</span><span class="sxs-lookup"><span data-stu-id="24eb8-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="24eb8-158">Именования подсеть шлюза hello «GatewaySubnet» позволяет Azure знать, что это hello подсети toodeploy hello шлюз виртуальной сети виртуальных машин и служб.</span><span class="sxs-lookup"><span data-stu-id="24eb8-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="24eb8-159">При создании hello подсеть шлюза, можно указать содержит hello число IP-адресов, которые hello подсети.</span><span class="sxs-lookup"><span data-stu-id="24eb8-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="24eb8-160">Hello IP-адресов в подсети шлюза hello: выделенный toohello шлюза виртуальные машины и службы шлюза.</span><span class="sxs-lookup"><span data-stu-id="24eb8-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="24eb8-161">Некоторым конфигурациям требуется больше IP-адресов, чем прочим.</span><span class="sxs-lookup"><span data-stu-id="24eb8-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="24eb8-162">Просмотрите инструкции hello hello конфигурации требуется toocreate и убедитесь, что вы хотите toocreate подсети шлюза hello соответствует этим требованиям.</span><span class="sxs-lookup"><span data-stu-id="24eb8-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="24eb8-163">Кроме того вы можете toomake подсети шлюза должен содержать достаточно IP-адреса tooaccommodate возможных будущих дополнительных конфигураций.</span><span class="sxs-lookup"><span data-stu-id="24eb8-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="24eb8-164">Хотя можно создать подсеть шлюза всего лишь с размером /29, мы советуем создавать подсети с размером /28 или больше (/28, /27, /26 и т. д.).</span><span class="sxs-lookup"><span data-stu-id="24eb8-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="24eb8-165">Таким образом, если добавить функциональность в будущем, hello вы не будет иметь tootear шлюз, а затем удалите и создайте hello tooallow подсеть шлюза для дополнительных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="24eb8-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="24eb8-166">Hello PowerShell диспетчера ресурсов пример с именем GatewaySubnet подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="24eb8-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="24eb8-167">Вы увидите в нотации CIDR hello указывает /27, позволяющий недостаточно IP-адресов для большинства конфигураций, которые в настоящее время существует.</span><span class="sxs-lookup"><span data-stu-id="24eb8-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="24eb8-168"><a name="lng"></a>Локальные сетевые шлюзы</span><span class="sxs-lookup"><span data-stu-id="24eb8-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="24eb8-169">При создании конфигурации шлюза VPN, шлюз локальной сети hello часто представляет ваше расположение в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="24eb8-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="24eb8-170">В hello классической модели развертывания шлюз локальной сети hello была ссылка tooas локального узла.</span><span class="sxs-lookup"><span data-stu-id="24eb8-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="24eb8-171">Присвойте имя шлюза локальной сети hello, hello общедоступный IP-адрес VPN-устройство локальной hello и указывать префиксы адресов hello, расположенных на hello в локальное расположение.</span><span class="sxs-lookup"><span data-stu-id="24eb8-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="24eb8-172">Azure просматривает hello префиксов адресов конечного сетевого трафика, обращается к hello конфигурации, который указан для шлюза локальной сети и соответствующим образом направляет пакеты.</span><span class="sxs-lookup"><span data-stu-id="24eb8-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="24eb8-173">Можно также указать шлюзы локальной сети для конфигураций типа "виртуальная сеть — виртуальная сеть", использующих подключение к VPN-шлюзу.</span><span class="sxs-lookup"><span data-stu-id="24eb8-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="24eb8-174">Следующий пример PowerShell Hello создает новый шлюз локальной сети:</span><span class="sxs-lookup"><span data-stu-id="24eb8-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="24eb8-175">Иногда требуется параметры шлюза локальной сети toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="24eb8-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="24eb8-176">Например, при добавлении или изменении hello диапазон адресов, а для hello IP-адрес устройства VPN hello изменений.</span><span class="sxs-lookup"><span data-stu-id="24eb8-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="24eb8-177">Для классической виртуальной сети можно изменить эти параметры в классический портал hello на странице приветствия локальных сетей.</span><span class="sxs-lookup"><span data-stu-id="24eb8-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="24eb8-178">В случае использования Resource Manager ознакомьтесь с разделом [Изменение параметров шлюза локальной сети с помощью PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="24eb8-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="24eb8-179"><a name="resources"></a>Интерфейсы REST API и командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="24eb8-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="24eb8-180">Дополнительные технические ресурсы и конкретные требования к синтаксису, при использовании REST API, командлеты PowerShell или Azure CLI для конфигурации VPN-шлюза, см. следующие страницы приветствия:</span><span class="sxs-lookup"><span data-stu-id="24eb8-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="24eb8-181">**Классический**</span><span class="sxs-lookup"><span data-stu-id="24eb8-181">**Classic**</span></span> | <span data-ttu-id="24eb8-182">**Диспетчер ресурсов**</span><span class="sxs-lookup"><span data-stu-id="24eb8-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="24eb8-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24eb8-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="24eb8-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24eb8-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="24eb8-185">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="24eb8-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="24eb8-186">REST API</span><span class="sxs-lookup"><span data-stu-id="24eb8-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="24eb8-187">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="24eb8-187">Not supported</span></span> | [<span data-ttu-id="24eb8-188">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="24eb8-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="24eb8-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="24eb8-189">Next steps</span></span>

<span data-ttu-id="24eb8-190">Дополнительные сведения о доступных конфигурациях подключений см. в статье [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="24eb8-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>