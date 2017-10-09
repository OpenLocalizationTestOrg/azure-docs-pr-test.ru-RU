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
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a>Подключения Azure VPN шлюзы toomultiple в локальной среде на основе политики VPN-устройства с помощью PowerShell

Эта статья поможет вам настройки Azure на основе маршрутов VPN шлюза tooconnect toomultiple в локальной среде на основе политики VPN-устройств использование настраиваемых политик IPsec/IKE S2S VPN-подключений.

## <a name="about-policy-based-and-route-based-vpn-gateways"></a>VPN-шлюзы на основе политики и маршрутов

Политики — *и* VPN-устройства на основе маршрутов отличаются по установке hello IPsec трафик селекторы для подключения:

* **На основе политики** VPN-устройства использовать сочетания hello префиксы из обоих toodefine сетей, как трафика шифруются и расшифровываются туннелей IPsec. Обычно это включено для устройств брандмауэра, выполняющих фильтрацию пакетов. IPsec туннель шифрования и расшифровки добавляются toohello фильтрации пакетов и подсистемы выполнения.
* **На основе маршрутов** селекторы трафика any к any (подстановочный знак) использовать VPN-устройства, а также позволяют маршрутизации пересылки таблицы туннелей IPsec toodifferent прямой трафик. Обычно это включено для платформ маршрутизатора, где каждый IPsec-туннель смоделирован как сетевой интерфейс или VTI (виртуальный интерфейс туннеля).

Hello следующие схемы выделите hello две модели:

### <a name="policy-based-vpn-example"></a>Пример VPN-устройства на основе политики
![на основе политик](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a>Пример VPN-устройства на основе маршрута
![на основе маршрута](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a>Поддержка Azure VPN-устройств на основе политики
В настоящее время Azure поддерживает оба режима VPN-шлюзов: VPN-шлюзы на основе маршрута и VPN-шлюзы на основе политики. Они разработаны для различных внутренних платформ. Дополнительные сведения см. в следующих спецификациях:

|                          | **VPN-шлюзы на основе политики** | **VPN-шлюзы на основе маршрута**               |
| ---                      | ---                         | ---                                      |
| **SKU шлюза Azure**    | базовая;                       | Категория "Базовая", "Стандартная", HighPerformance         |
| **Версия IKE**          | IKEv1                       | IKEv2                                    |
| **Макс. Подключения типа "сеть — сеть"** | **1**                       | Категория "Базовый", "Стандартный": 10<br> Категория HighPerformance: 30 |
|                          |                             |                                          |

С помощью настраиваемой политики IPsec/IKE hello, теперь можно настроить Azure на основе маршрутов VPN шлюзы toouse трафика на основе префикса селекторы с параметром «**PolicyBasedTrafficSelectors**», tooconnect организациями tooon на основе политики VPN-устройства. Эта возможность позволяет tooconnect из виртуальной сети Azure и toomultiple шлюза VPN локальной политики VPN или брандмауэр устройств на основе снятие hello текущего Azure на основе политики VPN-шлюзов hello ограничение одного соединения.

> [!IMPORTANT]
> 1. tooenable такого подключения VPN-устройств в локальной среде на основе политики должны поддерживать **IKEv2** tooconnect toohello Azure шлюзах VPN на основе маршрутов. Проверьте характеристики VPN-устройства.
> 2. Hello локальные сети при подключении через VPN-устройства на основе политик с помощью этого механизма можно подключиться только toohello виртуальной сети Azure; **они не транзитной tooother локальным сетям или виртуальные сети через hello один шлюз Azure VPN**.
> 3. параметр конфигурации Hello является частью hello настраиваемой политики IPsec/IKE соединения. При включении вариант селектора hello трафика на основе политик, необходимо указать полный политики hello (алгоритмы шифрования и целостности IPsec/IKE ключевые преимущества и время существования сопоставления безопасности).

Hello, следующая схема показывает, почему транзитной маршрутизацией через шлюз Azure VPN не работает с параметром на основе политики hello:

![передача на основе политики](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

Как показано на схеме hello hello VPN-шлюз Azure имеет селекторы трафика из tooeach виртуальной сети hello hello в локальной сети префиксы, но не префиксы hello нескольких соединений. Например, на локальном сайте 2, сайтами 3 и 4 можно каждого взаимодействуют tooVNet1 соответственно, но не может подключаться с помощью hello Azure VPN шлюза tooeach других. Hello показан hello подключения между селекторы трафика, которые недоступны в шлюз Azure VPN hello в этой конфигурации.

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a>Настройка селекторов трафика на основе политики для подключения

Hello инструкции выполните hello же пример, как описано в [политике настроить IPsec/IKE S2S или виртуальная сеть — сеть](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish S2S VPN-подключения. Это показано в hello, следующая схема:

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

Здравствуйте, рабочий процесс tooenable этого подключения:
1. Создание виртуальной сети hello, шлюза VPN и шлюза локальной сети для подключения между организациями
2. Создайте политику IPsec/IKE
3. Применить политику hello при создании подключения S2S или виртуальной сети для виртуальной сети, и **включить селекторы трафика на основе политики hello** в соединении hello
4. Если соединение hello уже создано, можно применить или обновить существующее соединение hello политики tooan

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a>Включение селекторов трафика на основе политики для подключения

Убедитесь, что выполнены [часть 3 статьи политики IPsec/IKE Настройка hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) для этого раздела. в этом примере используется следующая Hello hello же параметры и шаги:

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>Шаг 1 — Создание hello виртуальной сети, шлюз виртуальной частной сети и шлюза локальной сети

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a>1. Объявите переменные & подключения tooyour подписки
В этом упражнении мы начнем с объявления переменных. Быть убедиться, что значения hello tooreplace собственными при настройке для рабочей среды.

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
hello toouse командлеты диспетчера ресурсов убедитесь в том, что режима tooPowerShell. Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).

Откройте консоль PowerShell и подключить tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>2. Создание виртуальной сети hello, шлюза VPN и шлюза локальной сети
Следующий пример Hello создает виртуальную сеть hello, TestVNet1 с три подсети и шлюз VPN hello. При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet. Если вы используете другое имя, создание шлюза завершится сбоем.

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a>Шаг 2. Создание подключения VPN типа "сеть — сеть" с помощью политики IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Создайте политику IPsec/IKE

> [!IMPORTANT]
> Необходимо toocreate политику IPsec/IKE в порядке tooenable параметр «UsePolicyBasedTrafficSelectors» hello соединения.

Hello следующий пример создает политику IPsec/IKE с эти алгоритмы и параметры:
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a>2. Создание hello S2S VPN-подключения с селекторы трафика на основе политики и политики IPsec/IKE
Создание подключения к S2S VPN и применение политики IPsec/IKE hello, созданной на предыдущем шаге hello. Следует учитывать hello дополнительный параметр «-UsePolicyBasedTrafficSelectors $True» позволяющий селекторы трафика на основе политик в соединении hello.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

После выполнения действий hello hello S2S VPN-подключение будет использовать hello определена политика IPsec/IKE и включить селекторы трафика на основе политик в соединении hello. Это действие можно повторять hello же шаги tooadd дополнительные подключения tooadditional в локальной среде на основе политики VPN-устройства из hello один шлюз Azure VPN.

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a>Обновление селекторов трафика на основе политики для подключения
Hello последнего раздела показано, как параметр tooupdate hello трафика на основе политики селекторы для существующего подключения S2S VPN.

### <a name="1-get-hello-connection"></a>1. Получить подключение hello
Получите ресурс подключения hello.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a>2. Установите флажок hello трафика на основе политики селекторы
Hello следующая строка показывает, используются ли для соединения hello селекторы hello трафика на основе политик:

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

Возвращает строку hello»**True**», затем селекторы трафика на основе политики настроены на соединение hello; в противном случае возвращается «**False**.»

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a>3. Обновить hello селекторы трафика на основе политик для подключения
После получения hello ресурс подключения, можно включить или отключить параметр hello.

#### <a name="disable-usepolicybasedtrafficselectors"></a>Отключение параметра UsePolicyBasedTrafficSelectors
Hello следующий пример отключает параметр селекторы hello трафика на основе политик, но оставляет hello без изменений политики IPsec/IKE.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a>Включение параметра UsePolicyBasedTrafficSelectors
Hello следующий пример включает параметр селекторы hello трафика на основе политик, но оставляет hello без изменений политики IPsec/IKE.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a>Дальнейшие действия
После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Дополнительные сведения о настраиваемых политиках IPsec/IKE см. в статье [Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"](vpn-gateway-ipsecikepolicy-rm-powershell.md).
