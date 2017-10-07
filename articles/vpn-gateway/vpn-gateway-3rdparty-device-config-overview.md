---
title: "aaaAbout сторонних производителей устройства конфигурации tooconnect tooAzure VPN шлюзах VPN | Документы Microsoft"
description: "В этой статье Обзор сторонних стороны конфигураций устройств VPN для подключения VPN-шлюзов tooAzure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="b0903-103">Обзор конфигураций VPN-устройств сторонних производителей</span><span class="sxs-lookup"><span data-stu-id="b0903-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="b0903-104">Приводятся общие сведения о локальной конфигурации устройства VPN для подключения VPN-шлюзов tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b0903-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="b0903-105">Образец Hello виртуальной сети Azure и виртуальной частной сети шлюза программа установки может быть используется tooconnect toodifferent локальными устройствами VPN с hello такими же параметрами.</span><span class="sxs-lookup"><span data-stu-id="b0903-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="b0903-106">Требования к устройствам</span><span class="sxs-lookup"><span data-stu-id="b0903-106">Device requirements</span></span>
<span data-ttu-id="b0903-107">В VPN-шлюзах Azure используются стандартные наборы протоколов IPsec/IKE для VPN-туннелей S2S.</span><span class="sxs-lookup"><span data-stu-id="b0903-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="b0903-108">См. слишком[сведения о VPN-устройства](vpn-gateway-about-vpn-devices.md) hello подробную параметров протокола IPsec/IKE и алгоритмов шифрования по умолчанию для VPN-шлюзы Azure.</span><span class="sxs-lookup"><span data-stu-id="b0903-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="b0903-109">Можно дополнительно указать hello точное сочетание алгоритмов шифрования и значений длины ключа для конкретного подключения, как описано в [о требованиях к шифрования](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="b0903-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="b0903-110"><a name ="singletunnel"></a>Одиночный VPN-туннель</span><span class="sxs-lookup"><span data-stu-id="b0903-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="b0903-111">Первая топология Hello состоит из одного туннеля S2S VPN между шлюзом Azure VPN и локальным VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="b0903-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="b0903-112">При необходимости можно настроить BGP через туннель VPN hello.</span><span class="sxs-lookup"><span data-stu-id="b0903-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![Одиночный туннель](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="b0903-114">См. слишком[настройки подключения сеть сеть](vpn-gateway-howto-site-to-site-resource-manager-portal.md) пошаговые инструкции.</span><span class="sxs-lookup"><span data-stu-id="b0903-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="b0903-115">Hello следующих разделах перечислены параметры hello и предоставить образец toohelp сценария PowerShell, вам начать работу.</span><span class="sxs-lookup"><span data-stu-id="b0903-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="b0903-116">Сведения о сети и VPN-шлюзе</span><span class="sxs-lookup"><span data-stu-id="b0903-116">Network and VPN gateway information</span></span>
<span data-ttu-id="b0903-117">В этом разделе перечислены параметры hello hello примеры выше.</span><span class="sxs-lookup"><span data-stu-id="b0903-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="b0903-118">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="b0903-118">**Parameter**</span></span>                | <span data-ttu-id="b0903-119">**Значение**</span><span class="sxs-lookup"><span data-stu-id="b0903-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="b0903-120">Префиксы адресов виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b0903-120">VNet address prefixes</span></span>        | <span data-ttu-id="b0903-121">10.11.0.0/16;</span><span class="sxs-lookup"><span data-stu-id="b0903-121">10.11.0.0/16</span></span><br><span data-ttu-id="b0903-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b0903-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="b0903-123">IP-адрес VPN-шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="b0903-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="b0903-124">IP-адрес VPN-шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="b0903-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="b0903-125">Префиксы адресов в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b0903-125">On-premises address prefixes</span></span> | <span data-ttu-id="b0903-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b0903-126">10.51.0.0/16</span></span><br><span data-ttu-id="b0903-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b0903-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="b0903-128">IP-адрес VPN-устройства в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b0903-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="b0903-129">IP-адрес VPN-устройства в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b0903-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="b0903-130">*ASN для BGP виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b0903-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="b0903-131">65010</span><span class="sxs-lookup"><span data-stu-id="b0903-131">65010</span></span>                        |
| <span data-ttu-id="b0903-132">*IP-адрес узла BGP Azure</span><span class="sxs-lookup"><span data-stu-id="b0903-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="b0903-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="b0903-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="b0903-134">*ASN BGP в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b0903-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="b0903-135">65050</span><span class="sxs-lookup"><span data-stu-id="b0903-135">65050</span></span>                        |
| <span data-ttu-id="b0903-136">*IP-адрес узла BGP в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b0903-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="b0903-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="b0903-137">10.52.255.254</span></span>                |

* <span data-ttu-id="b0903-138">(*) Необязательные параметры только для BGP</span><span class="sxs-lookup"><span data-stu-id="b0903-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="b0903-139">Пример скрипта PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0903-139">Sample PowerShell script</span></span>
<span data-ttu-id="b0903-140">[Создание подключения S2S VPN с помощью PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) hello содержатся подробные инструкции.</span><span class="sxs-lookup"><span data-stu-id="b0903-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="b0903-141">Этот раздел содержит tooget образец скрипта, которого вы начали.</span><span class="sxs-lookup"><span data-stu-id="b0903-141">This section provides a sample script tooget you started.</span></span>

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
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
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect tooyour subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="b0903-142"><a name ="policybased"></a> [Необязательно] Использование настраиваемой политики IPsec/IKE с параметром UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="b0903-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="b0903-143">Если VPN-устройств не поддерживают селекторы «any к any» трафика (маршрут на основе/VTI-конфигурации на основе), может потребоваться toocreate настраиваемой политики IPsec/IKE и настроить параметр «UsePolicyBasedTrafficSelectors», как описано в [в данной статье ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b0903-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0903-144">Необходимо toocreate политику IPsec/IKE в порядке tooenable параметр «UsePolicyBasedTrafficSelectors» hello соединения.</span><span class="sxs-lookup"><span data-stu-id="b0903-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="b0903-145">Пример сценария Hello ниже создает политику IPsec/IKE с hello следующие алгоритмы и параметры:</span><span class="sxs-lookup"><span data-stu-id="b0903-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="b0903-146">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="b0903-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="b0903-147">IPsec: AES256, SHA1, PFS24, время существования сопоставления безопасности 7200 секунд, размер 20480000 КБ (20 ГБ).</span><span class="sxs-lookup"><span data-stu-id="b0903-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="b0903-148">Он применяет политику hello и включает «UesPolicyBasedTrafficSelectors» на подключение hello.</span><span class="sxs-lookup"><span data-stu-id="b0903-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="b0903-149"><a name ="bgp"></a>[Необязательно] Использование BGP в VPN-подключении типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="b0903-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="b0903-150">При необходимости BGP можно использовать для соединения hello.</span><span class="sxs-lookup"><span data-stu-id="b0903-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="b0903-151">См. статью [Настройка BGP на VPN-шлюзах Azure с помощью PowerShell](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b0903-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="b0903-152">Существует два отличия.</span><span class="sxs-lookup"><span data-stu-id="b0903-152">There are two differences:</span></span>

<span data-ttu-id="b0903-153">префиксы адресов локальной Hello может быть адрес одного узла, IP-адрес узла BGP hello в локальной среде:</span><span class="sxs-lookup"><span data-stu-id="b0903-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="b0903-154">Необходимо задать «-EnableBGP» слишком $True при создании соединения hello:</span><span class="sxs-lookup"><span data-stu-id="b0903-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="b0903-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0903-155">Next steps</span></span>
<span data-ttu-id="b0903-156">В разделе [настройка активных VPN-шлюзов для подключений виртуальной сети для виртуальной сети и между организациями](vpn-gateway-activeactive-rm-powershell.md) действия перекрестные tooconfigure активных и подключения к виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b0903-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

