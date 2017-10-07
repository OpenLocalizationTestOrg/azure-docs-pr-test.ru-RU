---
title: "Настройка VPN-подключений типа \"сеть — сеть\" в режиме \"активный — активный\" для VPN-шлюзов: Azure Resource Manager и PowerShell | Документы Майкрософт"
description: "В этой статье описана поэтапная настройка подключений в режиме \"активный — активный\" для VPN-шлюзов Azure с помощью Azure Resource Manager и PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Настройка VPN-подключений типа "сеть — сеть" в режиме "активный — активный" для VPN-шлюзов Azure

В этой статье рассматриваются hello действия toocreate активных между организациями и подключений виртуальной сети для виртуальной сети, с помощью модели развертывания диспетчера ресурсов hello и PowerShell.

## <a name="about-highly-available-cross-premises-connections"></a>Высокодоступное подключение между локальными сетями
высокий уровень доступности tooachieve между организациями и подключения к виртуальной сети для виртуальной сети, следует развернуть несколько шлюзов виртуальной частной сети и установить несколько параллельных соединений между сетями и Azure. Сведения о вариантах подключения и топологии подключений см. в статье [Настройка высокодоступных подключений: распределенных и между виртуальными сетями](vpn-gateway-highlyavailable.md).

В этой статье содержатся инструкции hello tooset копирование активный / активный между организациями VPN-подключения, а также активных соединений между двумя виртуальными сетями.

* [Часть 1. Создание и настройка VPN-шлюза Azure в режиме "активный — активный"](#aagateway)
* [Часть 2. Создание подключения между локальными сетями в режиме "активный — активный"](#aacrossprem)
* [Часть 3. Создание подключения между виртуальными сетями в режиме "активный — активный"](#aav2v)
* [Часть 4. Обновление имеющегося шлюза между режимами "активный — активный" и "активный — резервный"](#aaupdate)

Можно объединять эти вместе toobuild топологии сети более сложных, высокой надежности, соответствующий вашим потребностям.

> [!IMPORTANT]
> Обратите внимание, что hello активный / активный режим используется только hello после номера SKU: 
  * VpnGw1, VpnGw2, VpnGw3
  * HighPerformance (для устаревших номеров SKU)
> 
> 

## <a name ="aagateway"></a>Часть 1. Создание и настройка VPN-шлюзов в режиме "активный — активный"
в режимах активных Hello, выполнив действия настроит шлюза Azure VPN. Hello основные различия между шлюзами активный / активный "и" активный резервный hello.

* Требуются две конфигурации IP-адреса шлюза toocreate с общедоступных IP-адресов
* Вы должны установить флаг EnableActiveActiveFeature hello
* номер SKU шлюза Hello необходимо VpnGw1, VpnGw2, VpnGw3 или высокопроизводительные (Конфигурация прежних версий).

Hello другие свойства являются hello такой же, как шлюзы активный активный hello. 

### <a name="before-you-begin"></a>Перед началом работы
* Убедитесь в том, что у вас уже есть подписка Azure. Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).
* Вам потребуется командлеты PowerShell диспетчера ресурсов Azure tooinstall hello. В разделе [Обзор Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.

### <a name="step-1---create-and-configure-vnet1"></a>Шаг 1. Создание и настройка VNet1
#### <a name="1-declare-your-variables"></a>1. Объявление переменных
В этом упражнении мы начнем с объявления переменных. пример Hello hello переменных объявляются с помощью hello значения для этого упражнения. Быть убедиться, что значения hello tooreplace собственными при настройке для рабочей среды. Эти переменные можно использовать при выполнении через toobecome действия hello знакомы с этим типом конфигурации. Изменение переменных hello, а затем скопируйте и вставьте в консоль PowerShell.

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Подключить tooyour подписки и создать новую группу ресурсов
Убедитесь, что переключение tooPowerShell режим toouse hello командлеты диспетчера ресурсов. Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).

Откройте консоль PowerShell и подключить tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Создание TestVNet1
Образец Hello ниже создает виртуальную сеть с именем TestVNet1 и три подсети, один именем GatewaySubnet, одной вызываемой переднего плана и один внутренний вызван. При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet. Если вы используете другое имя, шлюз не будет создан.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>Шаг 2 — Создание hello VPN-шлюза для TestVNet1 активный / активный режим
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Создание общих IP-адресов hello и шлюз IP-конфигурации
Запрос двух открытый IP-адреса toobe выделенный toohello шлюз, создаваемых для виртуальной сети. Также мы определим hello подсети и IP-конфигурации требуется.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. Создание шлюза VPN hello в конфигурации активный активный
Создание шлюза виртуальной сети hello для TestVNet1. Обратите внимание, что имеется две записи GatewayIpConfig hello EnableActiveActiveFeature флаг имеет значение. Создание шлюза может занять некоторое время (45 минут или более toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Получить hello шлюза общих IP-адресов и адрес IP однорангового узла BGP hello
После создания шлюза hello требуется адрес IP однорангового узла BGP hello tooobtain на hello шлюза VPN Azure. Этот адрес будет hello необходимые tooconfigure VPN-шлюз Azure как узла BGP для VPN-устройства в локальной среде.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

Используйте следующие командлеты tooshow hello два общедоступных IP-адресов выделенные для шлюза VPN и их соответствующие адреса IP однорангового узла BGP для каждого экземпляра шлюза hello.

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

порядок Hello hello общих IP-адресов для экземпляров шлюза hello и соответствующего адреса Пиринг BGP приветствия hello таким же. В этом примере hello шлюза виртуальной Машины с помощью открытого IP-адреса 40.112.190.5 будет использовать 10.12.255.4 в качестве его адрес Пиринг BGP и hello шлюз с 138.91.156.129 будет использовать 10.12.255.5. Эти сведения необходимы при настройке локальную подключение toohello активных шлюза VPN-устройства. шлюз Hello показано hello показан на следующем рисунке адреса всех:

![Шлюз в режиме "активный — активный"](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

После создания шлюза hello, можно использовать этот шлюз tooestablish активных между организациями или подключения VNet-VNet. Hello в следующих разделах приведены шаги упражнения hello toocomplete действия hello.

## <a name ="aacrossprem"></a>Часть 2. Создание подключения между локальными сетями в режиме "активный — активный"
tooestablish подключения между организациями необходимо toocreate toorepresent шлюза локальной сети VPN-устройства в локальной среде и шлюза Azure VPN hello tooconnect соединения с hello шлюза локальной сети. В этом примере hello VPN-шлюз Azure находится в режиме активных. В результате несмотря на то, что имеется только один локальный VPN-устройством (шлюз локальной сети) и одно подключение ресурса, оба экземпляра шлюза Azure VPN установит туннелей S2S VPN с локального устройства hello.

Прежде чем продолжить, убедитесь, что вы выполнили инструкции из [первой части](#aagateway) этой статьи.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Шаг 1. Создание и настройка шлюза локальной сети hello
#### <a name="1-declare-your-variables"></a>1. Объявление переменных
В этом упражнении будет toobuild hello конфигурации, представленной схеме hello. Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

Несколько вещей toonote относительно hello параметры шлюза локальной сети:

* Hello шлюза локальной сети может быть в hello таким же или другое расположение и ресурсов группы как hello шлюза VPN. В этом примере показано их в разные группы ресурсов, но в hello Azure местоположения.
* Если имеется только одно устройство VPN в локальной среде, как показано выше, hello активных соединений может работать с или без протокола BGP. Этот пример использует протокол BGP для подключения между организациями hello.
* Если включен протокол BGP, префикс hello toodeclare потребность hello шлюза локальной сети — адрес узла hello ваш адрес BGP одноранговых IP на VPN-устройства. В нашем примере это префикс /32 для адреса 10.52.255.253/32.
* Не забывайте, что для локальных сетей и виртуальной сети Azure должны быть указаны разные номера ASN BGP. Если они являются одинаковыми hello, необходимо toochange вашей виртуальной сети ASN Если VPN-устройства локальной уже использует hello ASN toopeer с соседним узлам BGP.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Создание шлюза локальной сети hello для Site5
Прежде чем продолжить, убедитесь в том, что по-прежнему подключенных tooSubscription 1. Создайте группу ресурсов hello, если он еще не создан.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Шаг 2 - подключения шлюза виртуальной сети hello и шлюз локальной сети
#### <a name="1-get-hello-two-gateways"></a>1. Получить hello двумя шлюзами

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Создание подключения tooSite5 TestVNet1 hello
На этом шаге вы создадите hello подключения из TestVNet1 tooSite5_1 с «EnableBGP» задайте слишком $True.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. Параметры VPN и BGP для локального VPN-устройства
пример Hello ниже перечислены параметры hello, будет вводимых вами в hello BGP раздел конфигурации для локального VPN-устройства для этого упражнения.

    - Site5 ASN            : 65050
    - Site5 BGP IP         : 10.52.255.253
    - Префиксы tooannounce: (например) 10.51.0.0/16 и 10.52.0.0/16
    - Azure VNet ASN       : 65010
    - Azure виртуальная сеть BGP IP-адрес 1: 10.12.255.4 для too40.112.190.5 туннель
    - Azure виртуальная сеть BGP IP-адрес 2: 10.12.255.5 для too138.91.156.129 туннель
    - Статические маршруты: 10.12.255.4/32 назначения, следующего hello VPN туннельный интерфейс too40.112.190.5 назначения 10.12.255.5/32, следующего hello VPN туннельный интерфейс too138.91.156.129
    - eBGP мульти-прыжка: Убедитесь, вариант «мульти-прыжка» hello eBGP включен на вашем устройстве, при необходимости

Hello подключение должно быть установлено, после того как несколько минут и сеанс пиринга BGP hello будет запущена после установки соединения IPsec hello. В этом примере к текущему моменту настроил только одно устройство VPN локальной, приведет к диаграмме hello, показано ниже:

![Подключение между локальными сетями в режиме "активный — активный"](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>Шаг 3 — подключить два шлюза VPN активных toohello локальной VPN устройства
При наличии двух VPN-устройства на hello же локальной сети, можно добиться двумя избыточности, подключающегося hello Azure устройство шлюза VPN toohello второй VPN.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Создание hello второго шлюза локальной сети для Site5
Обратите внимание, что IP-адрес шлюза hello, префикс адреса и адрес пиринг BGP для hello второго шлюза локальной сети не должны перекрываться hello предыдущих шлюза локальной сети для hello же локальной сети.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Подключения шлюза виртуальной сети hello и hello второго шлюза локальной сети
Создание соединения hello с TestVNet1 tooSite5_2 с «EnableBGP» задайте слишком $True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. Параметры VPN и BGP для второго локального VPN-устройства
Аналогичным образом ниже перечислены параметры hello будет ввести в hello второе устройство VPN:

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

После установления соединения hello (туннели) будет иметь два избыточных VPN-устройства и туннели подключения вашей локальной сетью и Azure:

![Подключение между локальными сетями с двойной избыточностью](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>Часть 3. Создание подключения между виртуальными сетями в режиме "активный — активный"
В этом разделе описано, как создать подключение между виртуальными сетями в режиме "активный — активный" с использованием BGP. 

Приведенные ниже инструкции Hello по-прежнему hello предыдущих шагах, перечисленных выше. Необходимо выполнить [часть 1](#aagateway) toocreate hello VPN-шлюз с BGP и настроите TestVNet1. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Шаг 1 — Создание TestVNet2 и hello VPN-шлюза
Это важные toomake в том, что пространство IP-адресов hello hello новой виртуальной сети, TestVNet2, не перекрываются с диапазонов виртуальной сети.

В этом примере hello виртуальные сети относятся toohello одной подписке. Можно настроить виртуальную сеть — сеть соединений между разными подписками; см. слишком[Настройка подключения VNet-VNet](vpn-gateway-vnet-vnet-rm-ps.md) toolearn более подробные сведения. Убедитесь, что добавить hello»-EnableBgp $True» при создании hello tooenable подключений BGP.

#### <a name="1-declare-your-variables"></a>1. Объявление переменных
Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. Создание TestVNet2 в новую группу ресурсов hello

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. Создание VPN-шлюз hello активных для TestVNet2
Запрос двух открытый IP-адреса toobe выделенный toohello шлюз, создаваемых для виртуальной сети. Также мы определим hello подсети и IP-конфигурации требуется.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

Создайте шлюз VPN hello hello как номер и hello флаг «EnableActiveActiveFeature». Обратите внимание, что по умолчанию hello ASN необходимо переопределить на шлюзах Azure VPN. Hello ASN для hello подключенных виртуальных сетей должны быть разные tooenable BGP и транзитной маршрутизацией.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>Шаг 2 — подключить hello TestVNet1 и TestVNet2 шлюзов
В этом примере обоих шлюзов находятся в hello одной подписке. На этом шаге hello можно завершить сеанс PowerShell.

#### <a name="1-get-both-gateways"></a>1. Получение обоих шлюзов
Убедитесь, что вход и подключиться tooSubscription 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Создание двух подключений
На этом шаге вы создадите hello из TestVNet1 tooTestVNet2 и hello соединению из TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Быть убедиться, что tooenable BGP для ОБОИХ подключений.
> 
> 

После выполнения этих действий, подключение hello наладят через несколько минут, и сеанс пиринга BGP hello будет копии после завершения подключения hello виртуальной сети для виртуальной сети с двумя избыточности:

![Подключение между виртуальными сетями в режиме "активный — активный"](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>Часть 4. Обновление имеющегося шлюза между режимами "активный — активный" и "активный — резервный"
Последний раздел Hello описывается способ настройки существующего шлюза Azure VPN из активный резервный tooactive активный режим, или наоборот.

> [!NOTE]
> Этот раздел содержит tooresize hello действия прежних версий SKU (старый SKU) уже созданные VPN-шлюза, из стандартных tooHighPerformance. Эти действия не обновлять старые прежних версий tooone SKU для hello новых SKU.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>Настройте шлюз активный tooactive активный резервный шлюза
#### <a name="1-gateway-parameters"></a>1. Параметры шлюза
Следующий пример Hello преобразует шлюз активный резервный в активных шлюза. Требуется toocreate другой общедоступный IP-адрес, а затем добавить второй конфигурацию IP-адрес шлюза. Ниже показан hello использовать параметры:

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Создать hello общедоступный IP-адрес, а затем добавьте hello второй шлюз IP-конфигурации

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. Включить шлюз hello активный / активный режим и обновление
Необходимо задать hello объекта шлюза в PowerShell tootrigger hello фактического обновления. также необходимо изменить (размер) tooHighPerformance Hello SKU шлюза виртуальной сети hello, так как он был создан ранее, от стандартных.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

Это обновление может занять 30 минут too45.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>Настройте шлюз tooactive standby активных шлюза
#### <a name="1-gateway-parameters"></a>1. Параметры шлюза
Используйте hello же параметры, как описано выше, получить имя hello hello IP-конфигурации требуется tooremove.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Удалите IP-конфигурации шлюза hello и отключить hello активный / активный режим
Аналогичным образом необходимо задать hello объекта шлюза в PowerShell tootrigger hello фактического обновления.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

Это обновление может занять too30 слишком 45 минут.

## <a name="next-steps"></a>Дальнейшие действия
После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
