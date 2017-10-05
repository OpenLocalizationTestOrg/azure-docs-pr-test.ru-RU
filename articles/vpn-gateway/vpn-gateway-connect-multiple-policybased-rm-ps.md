---
title: "Подключение VPN-шлюзов Azure к нескольким локальным VPN-устройствам на основе политики. Azure Resource Manager: PowerShell | Документация Майкрософт"
description: "В этой статье описывается настройка VPN-шлюза Azure на основе маршрутов для нескольких VPN-устройств на основе политики с помощью Azure Resource Manager и PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 17211379ec61891982a02efca6730ca0da87c1ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-azure-vpn-gateways-to-multiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="98ab1-103">Подключение VPN-шлюзов Azure к нескольким локальным VPN-устройствам на основе политики с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="98ab1-103">Connect Azure VPN gateways to multiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="98ab1-104">Эта статья поможет вам настроить VPN-шлюз Azure на основе маршрутов для подключения к нескольким локальным VPN-устройствам на основе политики, которые используют настраиваемые политики IPsec/IKE для VPN-подключений типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="98ab1-104">This article helps you configure an Azure route-based VPN gateway to connect to multiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="98ab1-105">VPN-шлюзы на основе политики и маршрутов</span><span class="sxs-lookup"><span data-stu-id="98ab1-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="98ab1-106">VPN-устройства на основе политики *и* маршрутов отличаются способом установки селекторов трафика IPsec для подключения:</span><span class="sxs-lookup"><span data-stu-id="98ab1-106">Policy- *vs.* route-based VPN devices differ in how the IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="98ab1-107">VPN-устройства **на основе политики** используют комбинации префиксов из двух сетей, чтобы определить способ шифрования и расшифровки трафика через IPsec- туннели.</span><span class="sxs-lookup"><span data-stu-id="98ab1-107">**Policy-based** VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="98ab1-108">Обычно это включено для устройств брандмауэра, выполняющих фильтрацию пакетов.</span><span class="sxs-lookup"><span data-stu-id="98ab1-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="98ab1-109">Шифрование и расшифровка туннеля IPsec добавляются в фильтрацию пакетов и подсистему обработки.</span><span class="sxs-lookup"><span data-stu-id="98ab1-109">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>
* <span data-ttu-id="98ab1-110">VPN-устройства **на основе маршрута** используют селекторы трафика типа "любой к любому" (подстановочные) и позволяют таблицам пересылки и маршрута направлять трафик в различные IPsec-туннели.</span><span class="sxs-lookup"><span data-stu-id="98ab1-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="98ab1-111">Обычно это включено для платформ маршрутизатора, где каждый IPsec-туннель смоделирован как сетевой интерфейс или VTI (виртуальный интерфейс туннеля).</span><span class="sxs-lookup"><span data-stu-id="98ab1-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="98ab1-112">Следующие схемы выделяют две модели:</span><span class="sxs-lookup"><span data-stu-id="98ab1-112">The following diagrams highlight the two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="98ab1-113">Пример VPN-устройства на основе политики</span><span class="sxs-lookup"><span data-stu-id="98ab1-113">Policy-based VPN example</span></span>
![на основе политик](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="98ab1-115">Пример VPN-устройства на основе маршрута</span><span class="sxs-lookup"><span data-stu-id="98ab1-115">Route-based VPN example</span></span>
![на основе маршрута](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="98ab1-117">Поддержка Azure VPN-устройств на основе политики</span><span class="sxs-lookup"><span data-stu-id="98ab1-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="98ab1-118">В настоящее время Azure поддерживает оба режима VPN-шлюзов: VPN-шлюзы на основе маршрута и VPN-шлюзы на основе политики.</span><span class="sxs-lookup"><span data-stu-id="98ab1-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="98ab1-119">Они разработаны для различных внутренних платформ. Дополнительные сведения см. в следующих спецификациях:</span><span class="sxs-lookup"><span data-stu-id="98ab1-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="98ab1-120">**VPN-шлюзы на основе политики**</span><span class="sxs-lookup"><span data-stu-id="98ab1-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="98ab1-121">**VPN-шлюзы на основе маршрута**</span><span class="sxs-lookup"><span data-stu-id="98ab1-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="98ab1-122">**SKU шлюза Azure**</span><span class="sxs-lookup"><span data-stu-id="98ab1-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="98ab1-123">базовая;</span><span class="sxs-lookup"><span data-stu-id="98ab1-123">Basic</span></span>                       | <span data-ttu-id="98ab1-124">Категория "Базовая", "Стандартная", HighPerformance</span><span class="sxs-lookup"><span data-stu-id="98ab1-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="98ab1-125">**Версия IKE**</span><span class="sxs-lookup"><span data-stu-id="98ab1-125">**IKE version**</span></span>          | <span data-ttu-id="98ab1-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="98ab1-126">IKEv1</span></span>                       | <span data-ttu-id="98ab1-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="98ab1-127">IKEv2</span></span>                                    |
| <span data-ttu-id="98ab1-128">**Макс. Подключения типа "сеть — сеть"**</span><span class="sxs-lookup"><span data-stu-id="98ab1-128">**Max. S2S connections**</span></span> | <span data-ttu-id="98ab1-129">**1**</span><span class="sxs-lookup"><span data-stu-id="98ab1-129">**1**</span></span>                       | <span data-ttu-id="98ab1-130">Категория "Базовый", "Стандартный": 10</span><span class="sxs-lookup"><span data-stu-id="98ab1-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="98ab1-131">Категория HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="98ab1-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="98ab1-132">С настраиваемой политикой IPsec/IKE теперь можно настроить VPN-шлюзы Azure на основе маршрута, чтобы использовать селекторы трафика на основе префикса с параметром "**PolicyBasedTrafficSelectors**" для подключения к локальным VPN-устройствам на основе политики.</span><span class="sxs-lookup"><span data-stu-id="98ab1-132">With the custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways to use prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", to connect to on-premises policy-based VPN devices.</span></span> <span data-ttu-id="98ab1-133">Эта возможность позволит подключиться из виртуальной сети Azure и VPN-шлюза к нескольким локальным устройствам VPN и брандмауэра на основе политики, не ограничиваясь единым подключением из текущих VPN-шлюзов Azure на основе политики.</span><span class="sxs-lookup"><span data-stu-id="98ab1-133">This capability allows you to connect from an Azure virtual network and VPN gateway to multiple on-premises policy-based VPN/firewall devices, removing the single connection limit from the current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="98ab1-134">Чтобы включить возможность такого подключения, ваши локальные устройства VPN на основе политики должны поддерживать **IKEv2** для подключения к VPN-шлюзам Azure на основе маршрута.</span><span class="sxs-lookup"><span data-stu-id="98ab1-134">To enable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** to connect to the Azure route-based VPN gateways.</span></span> <span data-ttu-id="98ab1-135">Проверьте характеристики VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="98ab1-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="98ab1-136">Локальные сети, выполняющие подключение через VPN-устройства на основе политики с помощью этого механизма, могут подключаться только к виртуальной сети Azure. **Подключение к другим локальным или виртуальным сетям с помощью одного VPN-шлюза Azure невозможно**.</span><span class="sxs-lookup"><span data-stu-id="98ab1-136">The on-premises networks connecting through policy-based VPN devices with this mechanism can only connect to the Azure virtual network; **they cannot transit to other on-premises networks or virtual networks via the same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="98ab1-137">Параметр конфигурации является частью настраиваемой политики подключения IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="98ab1-137">The configuration option is part of the custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="98ab1-138">При включении параметра селектора трафика на основе политики вы должны указать полную политику (алгоритмы шифрования и целостности IPsec/IKE, уровни стойкости ключей и время существования SA).</span><span class="sxs-lookup"><span data-stu-id="98ab1-138">If you enable the policy-based traffic selector option, you must specify the complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="98ab1-139">На следующей схеме показано, почему транзитная маршрутизация через VPN-шлюз Azure не работает с включенным параметром на основе политики.</span><span class="sxs-lookup"><span data-stu-id="98ab1-139">The following diagram shows why transit routing via Azure VPN gateway doesn't work with the policy-based option:</span></span>

![передача на основе политики](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="98ab1-141">Как показано на схеме, у VPN-шлюза Azure есть селекторы трафика из виртуальной сети для каждого локального префикса в сети, а не префиксов кросс-подключения.</span><span class="sxs-lookup"><span data-stu-id="98ab1-141">As shown in the diagram, the Azure VPN gateway has traffic selectors from the virtual network to each of the on-premises network prefixes, but not the cross-connection prefixes.</span></span> <span data-ttu-id="98ab1-142">Например, локальные сайты 2, 3 и 4 могут все взаимодействовать с сетью VNet1, но не могут подключиться через VPN-шлюз Azure друг к другу.</span><span class="sxs-lookup"><span data-stu-id="98ab1-142">For example, on-premises site 2, site 3, and site 4 can each communicate to VNet1 respectively, but cannot connect via the Azure VPN gateway to each other.</span></span> <span data-ttu-id="98ab1-143">На схеме показаны селекторы трафика с кросс-подключением, недоступные для VPN-шлюза Azure в этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="98ab1-143">The diagram shows the cross-connect traffic selectors that are not available in the Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="98ab1-144">Настройка селекторов трафика на основе политики для подключения</span><span class="sxs-lookup"><span data-stu-id="98ab1-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="98ab1-145">Инструкции в этой статье основаны на том же примере, который описан в статье о [настройке политики IPsec/IKE для подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"](vpn-gateway-ipsecikepolicy-rm-powershell.md) для установки подключения VPN типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="98ab1-145">The instructions in this article follow the same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) to establish a S2S VPN connection.</span></span> <span data-ttu-id="98ab1-146">Это показано на схеме ниже:</span><span class="sxs-lookup"><span data-stu-id="98ab1-146">This is shown in the following diagram:</span></span>

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="98ab1-148">Этапы подключения:</span><span class="sxs-lookup"><span data-stu-id="98ab1-148">The workflow to enable this connectivity:</span></span>
1. <span data-ttu-id="98ab1-149">Создание виртуальной сети, VPN-шлюза и шлюза локальной сети для распределенного подключения.</span><span class="sxs-lookup"><span data-stu-id="98ab1-149">Create the virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="98ab1-150">Создание политики IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="98ab1-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="98ab1-151">Применение политики при создании подключения типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть" и **включение селекторов трафика на основе политики** для подключения.</span><span class="sxs-lookup"><span data-stu-id="98ab1-151">Apply the policy when you create a S2S or VNet-to-VNet connection, and **enable the policy-based traffic selectors** on the connection</span></span>
4. <span data-ttu-id="98ab1-152">Если подключение уже создано, можно применить или обновить политику для существующего подключения.</span><span class="sxs-lookup"><span data-stu-id="98ab1-152">If the connection is already created, you can apply or update the policy to an existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="98ab1-153">Включение селекторов трафика на основе политики для подключения</span><span class="sxs-lookup"><span data-stu-id="98ab1-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="98ab1-154">Чтобы перейти к этому разделу, убедитесь, что выполнены требования [по настройке политики IPsec/IKE (часть 3)](vpn-gateway-ipsecikepolicy-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="98ab1-154">Make sure you have completed [Part 3 of the Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="98ab1-155">В следующем примере используются те же параметры и действия:</span><span class="sxs-lookup"><span data-stu-id="98ab1-155">The following example uses the same parameters and steps:</span></span>

### <a name="step-1---create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="98ab1-156">Шаг 1. Создание виртуальной сети, VPN-шлюза и шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="98ab1-156">Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-to-your-subscription"></a><span data-ttu-id="98ab1-157">1. Объявите переменные и подключитесь к подписке</span><span class="sxs-lookup"><span data-stu-id="98ab1-157">1. Declare your variables & connect to your subscription</span></span>
<span data-ttu-id="98ab1-158">В этом упражнении мы начнем с объявления переменных.</span><span class="sxs-lookup"><span data-stu-id="98ab1-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="98ab1-159">Обязательно замените значения своими при настройке для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="98ab1-159">Be sure to replace the values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
<span data-ttu-id="98ab1-160">Для работы с командлетами диспетчера ресурсов необходимо перейти в режим PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98ab1-160">To use the Resource Manager cmdlets, make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="98ab1-161">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="98ab1-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="98ab1-162">Откройте консоль PowerShell и подключитесь к своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="98ab1-162">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="98ab1-163">Для подключения используйте следующий пример.</span><span class="sxs-lookup"><span data-stu-id="98ab1-163">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="98ab1-164">2) Создание виртуальной сети, VPN-шлюза и шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="98ab1-164">2. Create the virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="98ab1-165">В следующем примере создается виртуальная сеть TestVNet1 с тремя подсетями и VPN-шлюзом.</span><span class="sxs-lookup"><span data-stu-id="98ab1-165">The following example creates the virtual network, TestVNet1 with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="98ab1-166">При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="98ab1-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="98ab1-167">Если вы используете другое имя, создание шлюза завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="98ab1-167">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="98ab1-168">Шаг 2. Создание подключения VPN типа "сеть — сеть" с помощью политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="98ab1-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="98ab1-169">1. Создание политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="98ab1-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98ab1-170">Вам необходимо создать политику IPsec/IKE для включения параметра "UsePolicyBasedTrafficSelectors" для подключения.</span><span class="sxs-lookup"><span data-stu-id="98ab1-170">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="98ab1-171">В следующем примере создается политика IPsec/IKE с этими алгоритмами и параметрами:</span><span class="sxs-lookup"><span data-stu-id="98ab1-171">The following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="98ab1-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="98ab1-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="98ab1-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span><span class="sxs-lookup"><span data-stu-id="98ab1-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="98ab1-174">2) Создание подключения VPN типа "сеть — сеть" с помощью селекторов трафика на основе политики и политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="98ab1-174">2. Create the S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="98ab1-175">Создайте подключение VPN типа "сеть — сеть" и примените политику IPsec/IKE, созданную на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="98ab1-175">Create an S2S VPN connection and apply the IPsec/IKE policy created in the previous step.</span></span> <span data-ttu-id="98ab1-176">Чтобы включить селекторы трафика на основе политики для подключения, дополнительному параметру -UsePolicyBasedTrafficSelectors должно быть задано значение $True.</span><span class="sxs-lookup"><span data-stu-id="98ab1-176">Be aware of the additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on the connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="98ab1-177">После выполнения этих действий подключение VPN типа "сеть — сеть" будет использовать для подключения определенную выше политику IPsec/IKE и включит селекторы трафика на основе политики.</span><span class="sxs-lookup"><span data-stu-id="98ab1-177">After completing the steps, the S2S VPN connection will use the IPsec/IKE policy defined, and enable policy-based traffic selectors on the connection.</span></span> <span data-ttu-id="98ab1-178">Вы можете повторить те же действия, чтобы добавить подключения для дополнительных локальных VPN-устройств на основе политики из одного VPN-шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="98ab1-178">You can repeat the same steps to add more connections to additional on-premises policy-based VPN devices from the same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="98ab1-179">Обновление селекторов трафика на основе политики для подключения</span><span class="sxs-lookup"><span data-stu-id="98ab1-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="98ab1-180">Из последнего раздела вы узнаете, как обновить параметр селекторов трафика на основе политики для существующего подключения VPN типа "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="98ab1-180">The last section shows you how to update the policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-the-connection"></a><span data-ttu-id="98ab1-181">1. Получение подключения</span><span class="sxs-lookup"><span data-stu-id="98ab1-181">1. Get the connection</span></span>
<span data-ttu-id="98ab1-182">Получение ресурса подключения</span><span class="sxs-lookup"><span data-stu-id="98ab1-182">Get the connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-the-policy-based-traffic-selectors-option"></a><span data-ttu-id="98ab1-183">2) Использование параметра селекторов трафика на основе политики</span><span class="sxs-lookup"><span data-stu-id="98ab1-183">2. Check the policy-based traffic selectors option</span></span>
<span data-ttu-id="98ab1-184">В следующей строке показано, используются ли для подключения селекторы трафика на основе политики:</span><span class="sxs-lookup"><span data-stu-id="98ab1-184">The following line shows whether the policy-based traffic selectors are used for the connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="98ab1-185">Если строка возвращает значение **True**, селекторы трафика на основе политики настроены для подключения. В противном случае возвращается значение **False**.</span><span class="sxs-lookup"><span data-stu-id="98ab1-185">If the line returns "**True**", then policy-based traffic selectors are configured on the connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-the-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="98ab1-186">3. Обновление селекторов трафика на основе политики для подключения</span><span class="sxs-lookup"><span data-stu-id="98ab1-186">3. Update the policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="98ab1-187">После получения ресурса подключения можно включить или отключить этот параметр.</span><span class="sxs-lookup"><span data-stu-id="98ab1-187">Once you obtain the connection resource, you can enable or disable the option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="98ab1-188">Отключение параметра UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="98ab1-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="98ab1-189">В следующем примере отключается параметр селекторов трафика на основе политики и не изменяется политика IPsec/IKE:</span><span class="sxs-lookup"><span data-stu-id="98ab1-189">The following example disables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="98ab1-190">Включение параметра UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="98ab1-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="98ab1-191">В следующем примере включается параметр селекторов трафика на основе политики и не изменяется политика IPsec/IKE:</span><span class="sxs-lookup"><span data-stu-id="98ab1-191">The following example enables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="98ab1-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98ab1-192">Next steps</span></span>
<span data-ttu-id="98ab1-193">Установив подключение, можно добавить виртуальные машины в виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="98ab1-193">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="98ab1-194">Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98ab1-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="98ab1-195">Дополнительные сведения о настраиваемых политиках IPsec/IKE см. в статье [Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"](vpn-gateway-ipsecikepolicy-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="98ab1-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
