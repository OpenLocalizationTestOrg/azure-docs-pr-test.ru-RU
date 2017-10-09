---
title: "Подключения Azure VPN шлюзы toomultiple в локальной среде на основе политики VPN-устройства: диспетчера ресурсов Azure: PowerShell | Документы Microsoft"
description: "В этой статье описывается настройка Azure на основе маршрутов VPN шлюза toomultiple на основе политики VPN-устройства с помощью диспетчера ресурсов Azure и PowerShell."
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
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="4e1a2-103">Подключения Azure VPN шлюзы toomultiple в локальной среде на основе политики VPN-устройства с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e1a2-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="4e1a2-104">Эта статья поможет вам настройки Azure на основе маршрутов VPN шлюза tooconnect toomultiple в локальной среде на основе политики VPN-устройств использование настраиваемых политик IPsec/IKE S2S VPN-подключений.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="4e1a2-105">VPN-шлюзы на основе политики и маршрутов</span><span class="sxs-lookup"><span data-stu-id="4e1a2-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="4e1a2-106">Политики — *и* VPN-устройства на основе маршрутов отличаются по установке hello IPsec трафик селекторы для подключения:</span><span class="sxs-lookup"><span data-stu-id="4e1a2-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="4e1a2-107">**На основе политики** VPN-устройства использовать сочетания hello префиксы из обоих toodefine сетей, как трафика шифруются и расшифровываются туннелей IPsec.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="4e1a2-108">Обычно это включено для устройств брандмауэра, выполняющих фильтрацию пакетов.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="4e1a2-109">IPsec туннель шифрования и расшифровки добавляются toohello фильтрации пакетов и подсистемы выполнения.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="4e1a2-110">**На основе маршрутов** селекторы трафика any к any (подстановочный знак) использовать VPN-устройства, а также позволяют маршрутизации пересылки таблицы туннелей IPsec toodifferent прямой трафик.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="4e1a2-111">Обычно это включено для платформ маршрутизатора, где каждый IPsec-туннель смоделирован как сетевой интерфейс или VTI (виртуальный интерфейс туннеля).</span><span class="sxs-lookup"><span data-stu-id="4e1a2-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="4e1a2-112">Hello следующие схемы выделите hello две модели:</span><span class="sxs-lookup"><span data-stu-id="4e1a2-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="4e1a2-113">Пример VPN-устройства на основе политики</span><span class="sxs-lookup"><span data-stu-id="4e1a2-113">Policy-based VPN example</span></span>
![на основе политик](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="4e1a2-115">Пример VPN-устройства на основе маршрута</span><span class="sxs-lookup"><span data-stu-id="4e1a2-115">Route-based VPN example</span></span>
![на основе маршрута](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="4e1a2-117">Поддержка Azure VPN-устройств на основе политики</span><span class="sxs-lookup"><span data-stu-id="4e1a2-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="4e1a2-118">В настоящее время Azure поддерживает оба режима VPN-шлюзов: VPN-шлюзы на основе маршрута и VPN-шлюзы на основе политики.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="4e1a2-119">Они разработаны для различных внутренних платформ. Дополнительные сведения см. в следующих спецификациях:</span><span class="sxs-lookup"><span data-stu-id="4e1a2-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="4e1a2-120">**VPN-шлюзы на основе политики**</span><span class="sxs-lookup"><span data-stu-id="4e1a2-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="4e1a2-121">**VPN-шлюзы на основе маршрута**</span><span class="sxs-lookup"><span data-stu-id="4e1a2-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="4e1a2-122">**SKU шлюза Azure**</span><span class="sxs-lookup"><span data-stu-id="4e1a2-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="4e1a2-123">базовая;</span><span class="sxs-lookup"><span data-stu-id="4e1a2-123">Basic</span></span>                       | <span data-ttu-id="4e1a2-124">Категория "Базовая", "Стандартная", HighPerformance</span><span class="sxs-lookup"><span data-stu-id="4e1a2-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="4e1a2-125">**Версия IKE**</span><span class="sxs-lookup"><span data-stu-id="4e1a2-125">**IKE version**</span></span>          | <span data-ttu-id="4e1a2-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="4e1a2-126">IKEv1</span></span>                       | <span data-ttu-id="4e1a2-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="4e1a2-127">IKEv2</span></span>                                    |
| <span data-ttu-id="4e1a2-128">**Макс. Подключения типа "сеть — сеть"**</span><span class="sxs-lookup"><span data-stu-id="4e1a2-128">**Max. S2S connections**</span></span> | <span data-ttu-id="4e1a2-129">**1**</span><span class="sxs-lookup"><span data-stu-id="4e1a2-129">**1**</span></span>                       | <span data-ttu-id="4e1a2-130">Категория "Базовый", "Стандартный": 10</span><span class="sxs-lookup"><span data-stu-id="4e1a2-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="4e1a2-131">Категория HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="4e1a2-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="4e1a2-132">С помощью настраиваемой политики IPsec/IKE hello, теперь можно настроить Azure на основе маршрутов VPN шлюзы toouse трафика на основе префикса селекторы с параметром «**PolicyBasedTrafficSelectors**», tooconnect организациями tooon на основе политики VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="4e1a2-133">Эта возможность позволяет tooconnect из виртуальной сети Azure и toomultiple шлюза VPN локальной политики VPN или брандмауэр устройств на основе снятие hello текущего Azure на основе политики VPN-шлюзов hello ограничение одного соединения.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="4e1a2-134">tooenable такого подключения VPN-устройств в локальной среде на основе политики должны поддерживать **IKEv2** tooconnect toohello Azure шлюзах VPN на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="4e1a2-135">Проверьте характеристики VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="4e1a2-136">Hello локальные сети при подключении через VPN-устройства на основе политик с помощью этого механизма можно подключиться только toohello виртуальной сети Azure; **они не транзитной tooother локальным сетям или виртуальные сети через hello один шлюз Azure VPN**.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="4e1a2-137">параметр конфигурации Hello является частью hello настраиваемой политики IPsec/IKE соединения.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="4e1a2-138">При включении вариант селектора hello трафика на основе политик, необходимо указать полный политики hello (алгоритмы шифрования и целостности IPsec/IKE ключевые преимущества и время существования сопоставления безопасности).</span><span class="sxs-lookup"><span data-stu-id="4e1a2-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="4e1a2-139">Hello, следующая схема показывает, почему транзитной маршрутизацией через шлюз Azure VPN не работает с параметром на основе политики hello:</span><span class="sxs-lookup"><span data-stu-id="4e1a2-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![передача на основе политики](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="4e1a2-141">Как показано на схеме hello hello VPN-шлюз Azure имеет селекторы трафика из tooeach виртуальной сети hello hello в локальной сети префиксы, но не префиксы hello нескольких соединений.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="4e1a2-142">Например, на локальном сайте 2, сайтами 3 и 4 можно каждого взаимодействуют tooVNet1 соответственно, но не может подключаться с помощью hello Azure VPN шлюза tooeach других.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="4e1a2-143">Hello показан hello подключения между селекторы трафика, которые недоступны в шлюз Azure VPN hello в этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="4e1a2-144">Настройка селекторов трафика на основе политики для подключения</span><span class="sxs-lookup"><span data-stu-id="4e1a2-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="4e1a2-145">Hello инструкции выполните hello же пример, как описано в [политике настроить IPsec/IKE S2S или виртуальная сеть — сеть](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish S2S VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="4e1a2-146">Это показано в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="4e1a2-146">This is shown in hello following diagram:</span></span>

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="4e1a2-148">Здравствуйте, рабочий процесс tooenable этого подключения:</span><span class="sxs-lookup"><span data-stu-id="4e1a2-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="4e1a2-149">Создание виртуальной сети hello, шлюза VPN и шлюза локальной сети для подключения между организациями</span><span class="sxs-lookup"><span data-stu-id="4e1a2-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="4e1a2-150">Создайте политику IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="4e1a2-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="4e1a2-151">Применить политику hello при создании подключения S2S или виртуальной сети для виртуальной сети, и **включить селекторы трафика на основе политики hello** в соединении hello</span><span class="sxs-lookup"><span data-stu-id="4e1a2-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="4e1a2-152">Если соединение hello уже создано, можно применить или обновить существующее соединение hello политики tooan</span><span class="sxs-lookup"><span data-stu-id="4e1a2-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="4e1a2-153">Включение селекторов трафика на основе политики для подключения</span><span class="sxs-lookup"><span data-stu-id="4e1a2-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="4e1a2-154">Убедитесь, что выполнены [часть 3 статьи политики IPsec/IKE Настройка hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) для этого раздела.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="4e1a2-155">в этом примере используется следующая Hello hello же параметры и шаги:</span><span class="sxs-lookup"><span data-stu-id="4e1a2-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="4e1a2-156">Шаг 1 — Создание hello виртуальной сети, шлюз виртуальной частной сети и шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="4e1a2-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="4e1a2-157">1. Объявите переменные & подключения tooyour подписки</span><span class="sxs-lookup"><span data-stu-id="4e1a2-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="4e1a2-158">В этом упражнении мы начнем с объявления переменных.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="4e1a2-159">Быть убедиться, что значения hello tooreplace собственными при настройке для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

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
<span data-ttu-id="4e1a2-160">hello toouse командлеты диспетчера ресурсов убедитесь в том, что режима tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="4e1a2-161">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4e1a2-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="4e1a2-162">Откройте консоль PowerShell и подключить tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="4e1a2-163">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="4e1a2-164">2. Создание виртуальной сети hello, шлюза VPN и шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="4e1a2-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="4e1a2-165">Следующий пример Hello создает виртуальную сеть hello, TestVNet1 с три подсети и шлюз VPN hello.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="4e1a2-166">При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="4e1a2-167">Если вы используете другое имя, создание шлюза завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-167">If you name it something else, your gateway creation fails.</span></span>

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="4e1a2-168">Шаг 2. Создание подключения VPN типа "сеть — сеть" с помощью политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="4e1a2-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="4e1a2-169">1. Создайте политику IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="4e1a2-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e1a2-170">Необходимо toocreate политику IPsec/IKE в порядке tooenable параметр «UsePolicyBasedTrafficSelectors» hello соединения.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="4e1a2-171">Hello следующий пример создает политику IPsec/IKE с эти алгоритмы и параметры:</span><span class="sxs-lookup"><span data-stu-id="4e1a2-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="4e1a2-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="4e1a2-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="4e1a2-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span><span class="sxs-lookup"><span data-stu-id="4e1a2-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="4e1a2-174">2. Создание hello S2S VPN-подключения с селекторы трафика на основе политики и политики IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="4e1a2-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="4e1a2-175">Создание подключения к S2S VPN и применение политики IPsec/IKE hello, созданной на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="4e1a2-176">Следует учитывать hello дополнительный параметр «-UsePolicyBasedTrafficSelectors $True» позволяющий селекторы трафика на основе политик в соединении hello.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="4e1a2-177">После выполнения действий hello hello S2S VPN-подключение будет использовать hello определена политика IPsec/IKE и включить селекторы трафика на основе политик в соединении hello.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="4e1a2-178">Это действие можно повторять hello же шаги tooadd дополнительные подключения tooadditional в локальной среде на основе политики VPN-устройства из hello один шлюз Azure VPN.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="4e1a2-179">Обновление селекторов трафика на основе политики для подключения</span><span class="sxs-lookup"><span data-stu-id="4e1a2-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="4e1a2-180">Hello последнего раздела показано, как параметр tooupdate hello трафика на основе политики селекторы для существующего подключения S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="4e1a2-181">1. Получить подключение hello</span><span class="sxs-lookup"><span data-stu-id="4e1a2-181">1. Get hello connection</span></span>
<span data-ttu-id="4e1a2-182">Получите ресурс подключения hello.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="4e1a2-183">2. Установите флажок hello трафика на основе политики селекторы</span><span class="sxs-lookup"><span data-stu-id="4e1a2-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="4e1a2-184">Hello следующая строка показывает, используются ли для соединения hello селекторы hello трафика на основе политик:</span><span class="sxs-lookup"><span data-stu-id="4e1a2-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="4e1a2-185">Возвращает строку hello»**True**», затем селекторы трафика на основе политики настроены на соединение hello; в противном случае возвращается «**False**.»</span><span class="sxs-lookup"><span data-stu-id="4e1a2-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="4e1a2-186">3. Обновить hello селекторы трафика на основе политик для подключения</span><span class="sxs-lookup"><span data-stu-id="4e1a2-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="4e1a2-187">После получения hello ресурс подключения, можно включить или отключить параметр hello.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="4e1a2-188">Отключение параметра UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="4e1a2-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="4e1a2-189">Hello следующий пример отключает параметр селекторы hello трафика на основе политик, но оставляет hello без изменений политики IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="4e1a2-190">Включение параметра UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="4e1a2-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="4e1a2-191">Hello следующий пример включает параметр селекторы hello трафика на основе политик, но оставляет hello без изменений политики IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="4e1a2-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e1a2-192">Next steps</span></span>
<span data-ttu-id="4e1a2-193">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="4e1a2-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="4e1a2-194">Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4e1a2-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="4e1a2-195">Дополнительные сведения о настраиваемых политиках IPsec/IKE см. в статье [Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"](vpn-gateway-ipsecikepolicy-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4e1a2-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
