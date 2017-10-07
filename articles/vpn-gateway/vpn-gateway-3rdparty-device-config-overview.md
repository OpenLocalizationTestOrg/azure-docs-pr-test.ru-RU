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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>Обзор конфигураций VPN-устройств сторонних производителей
Приводятся общие сведения о локальной конфигурации устройства VPN для подключения VPN-шлюзов tooAzure. Образец Hello виртуальной сети Azure и виртуальной частной сети шлюза программа установки может быть используется tooconnect toodifferent локальными устройствами VPN с hello такими же параметрами.

## <a name="device-requirements"></a>Требования к устройствам
В VPN-шлюзах Azure используются стандартные наборы протоколов IPsec/IKE для VPN-туннелей S2S. См. слишком[сведения о VPN-устройства](vpn-gateway-about-vpn-devices.md) hello подробную параметров протокола IPsec/IKE и алгоритмов шифрования по умолчанию для VPN-шлюзы Azure. Можно дополнительно указать hello точное сочетание алгоритмов шифрования и значений длины ключа для конкретного подключения, как описано в [о требованиях к шифрования](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Одиночный VPN-туннель
Первая топология Hello состоит из одного туннеля S2S VPN между шлюзом Azure VPN и локальным VPN-устройства. При необходимости можно настроить BGP через туннель VPN hello.

![Одиночный туннель](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

См. слишком[настройки подключения сеть сеть](vpn-gateway-howto-site-to-site-resource-manager-portal.md) пошаговые инструкции. Hello следующих разделах перечислены параметры hello и предоставить образец toohelp сценария PowerShell, вам начать работу.

### <a name="network-and-vpn-gateway-information"></a>Сведения о сети и VPN-шлюзе
В этом разделе перечислены параметры hello hello примеры выше.

| **Параметр**                | **Значение**                    |
| ---                          | ---                          |
| Префиксы адресов виртуальной сети        | 10.11.0.0/16;<br>10.12.0.0/16 |
| IP-адрес VPN-шлюза Azure         | IP-адрес VPN-шлюза Azure         |
| Префиксы адресов в локальной среде | 10.51.0.0/16<br>10.52.0.0/16 |
| IP-адрес VPN-устройства в локальной среде    | IP-адрес VPN-устройства в локальной среде    |
| *ASN для BGP виртуальной сети                | 65010                        |
| *IP-адрес узла BGP Azure           | 10.12.255.30                 |
| *ASN BGP в локальной среде         | 65050                        |
| *IP-адрес узла BGP в локальной среде     | 10.52.255.254                |

* (*) Необязательные параметры только для BGP

### <a name="sample-powershell-script"></a>Пример скрипта PowerShell
[Создание подключения S2S VPN с помощью PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) hello содержатся подробные инструкции. Этот раздел содержит tooget образец скрипта, которого вы начали.

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

### <a name ="policybased"></a> [Необязательно] Использование настраиваемой политики IPsec/IKE с параметром UsePolicyBasedTrafficSelectors
Если VPN-устройств не поддерживают селекторы «any к any» трафика (маршрут на основе/VTI-конфигурации на основе), может потребоваться toocreate настраиваемой политики IPsec/IKE и настроить параметр «UsePolicyBasedTrafficSelectors», как описано в [в данной статье ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> Необходимо toocreate политику IPsec/IKE в порядке tooenable параметр «UsePolicyBasedTrafficSelectors» hello соединения.

Пример сценария Hello ниже создает политику IPsec/IKE с hello следующие алгоритмы и параметры:
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA1, PFS24, время существования сопоставления безопасности 7200 секунд, размер 20480000 КБ (20 ГБ).

Он применяет политику hello и включает «UesPolicyBasedTrafficSelectors» на подключение hello.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[Необязательно] Использование BGP в VPN-подключении типа "сеть — сеть"
При необходимости BGP можно использовать для соединения hello. См. статью [Настройка BGP на VPN-шлюзах Azure с помощью PowerShell](vpn-gateway-bgp-resource-manager-ps.md). Существует два отличия.

префиксы адресов локальной Hello может быть адрес одного узла, IP-адрес узла BGP hello в локальной среде:

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

Необходимо задать «-EnableBGP» слишком $True при создании соединения hello:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Дальнейшие действия
В разделе [настройка активных VPN-шлюзов для подключений виртуальной сети для виртуальной сети и между организациями](vpn-gateway-activeactive-rm-powershell.md) действия перекрестные tooconfigure активных и подключения к виртуальной сети для виртуальной сети.

