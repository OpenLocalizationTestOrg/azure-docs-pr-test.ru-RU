---
title: "Настройка BGP на VPN-шлюзах Azure с помощью Resource Manager и PowerShell | Документы Майкрософт"
description: "В этой статье описана поэтапная настройка протокола BGP для VPN-шлюзов Azure с помощью Azure Resource Manager и PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>Как tooconfigure BGP на шлюзах VPN Azure с помощью PowerShell
В этой статье описывается tooenable действия hello BGP на-сайтами (S2S) VPN-подключения между организациями и подключение к виртуальной сети для виртуальной сети, с помощью модели развертывания диспетчера ресурсов hello и PowerShell.

## <a name="about-bgp"></a>О протоколе BGP
BGP — hello протокол маршрутизации обычно используется в hello информации через Интернет tooexchange маршрутизации и возможности доступа между двумя или более сетями. BGP обеспечивает VPN-шлюзы Azure hello и VPN-устройства локальной называется узлов BGP или соседей, tooexchange «маршруты» сообщит обоих шлюзов на доступность hello и возможности доступа для тех префиксов toogo через hello шлюзы или маршрутизаторы участвующих. BGP можно также включить транзитной маршрутизацией среди нескольких сетей, распространение маршрутов BGP шлюз узнает из одного tooall однорангового узла BGP других узлов BGP.

В разделе [Обзор BGP со шлюзами VPN Azure](vpn-gateway-bgp-overview.md) дополнительную информацию о преимуществах BGP и toounderstand hello технических требований и рекомендаций, связанных с помощью BGP.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Приступая к работе с BGP на VPN-шлюзах Azure

В этой статье рассматриваются hello действия toodo hello следующие задачи:

* [Часть 1 — активация BGP на VPN-шлюзе Azure](#enablebgp)
* [Часть 2 — создание подключения между локальными сетями с использованием BGP](#crossprembgp)
* [Часть 3 — создание подключения между виртуальными сетями с использованием BGP](#v2vbgp)

Каждая часть инструкции hello forms это основной стандартный блок для включения BGP в сетевое подключение. Если вы прошли все три части, как показано в hello, следующая схема сборки hello топологии:

![Топология BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

Можно объединять части вместе toobuild более сложных, мульти-прыжка транзитной сети, соответствующий вашим потребностям.

## <a name ="enablebgp"></a>Часть 1 — Настройка BGP на hello Azure VPN-шлюза
действия по настройке Hello настроить hello параметров BGP hello шлюза Azure VPN как показано в hello, следующая схема:

![Шлюз BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Перед началом работы
* Убедитесь в том, что у вас уже есть подписка Azure. Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).
* Установите командлеты PowerShell диспетчера ресурсов Azure hello. Дополнительные сведения об установке hello командлеты PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). 

### <a name="step-1---create-and-configure-vnet1"></a>Шаг 1. Создание и настройка VNet1
#### <a name="1-declare-your-variables"></a>1. Объявление переменных
В этом упражнении мы начнем с объявления переменных. Hello следующий пример hello переменных объявляются с помощью hello значения для этого упражнения. Быть убедиться, что значения hello tooreplace собственными при настройке для рабочей среды. Эти переменные можно использовать при выполнении через toobecome действия hello знакомы с этим типом конфигурации. Изменение переменных hello, а затем скопируйте и вставьте в консоль PowerShell.

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Подключить tooyour подписки и создать новую группу ресурсов
hello toouse командлеты диспетчера ресурсов убедитесь в том, что режима tooPowerShell. Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).

Откройте консоль PowerShell и подключить tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Создание TestVNet1
Hello следующий пример создает виртуальную сеть с именем TestVNet1 и три подсети, один именем GatewaySubnet, одной вызываемой переднего плана и один внутренний вызван. При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet. Если вы используете другое имя, создание шлюза завершится сбоем.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>Шаг 2 — Создание hello VPN-шлюза для TestVNet1 с параметрами BGP
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1. Создайте hello конфигурации IP-адресов и подсети
Запрос открытый IP-адрес toobe toohello выделенный шлюз, создаваемых для виртуальной сети. Также мы определим hello требуется подсеть и IP-конфигурации.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2. Создайте шлюз VPN hello hello как число
Создание шлюза виртуальной сети hello для TestVNet1. BGP требуется TestVNet1 типа на основе маршрутов VPN-шлюза, а также hello сложения параметр - Asn, tooset hello ASN (номер AS). Если не задан параметр ASN hello, назначается ASN 65515. Создание шлюза может занять некоторое время (30 минут или более toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3. Получить hello Azure BGP однорангового узла, IP-адрес
После создания шлюза hello требуется tooobtain hello IP-однорангового узла BGP адрес на hello шлюза VPN Azure. Этот адрес будет hello необходимые tooconfigure VPN-шлюз Azure как узла BGP для VPN-устройства в локальной среде.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

Последняя команда Hello показывает hello соответствующей конфигурации BGP hello VPN-шлюз Azure; Например:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

После создания шлюза hello с протоколом BGP можно использовать этот шлюз tooestablish между организациями подключение или подключение виртуальной сети для виртуальной сети. Hello следующие разделы содержат пошаговые инструкции hello действия toocomplete hello упражнении.

## <a name ="crossprembbgp"></a>Часть 2 — создание подключения между локальными сетями с использованием BGP

tooestablish подключения между организациями необходимо toocreate toorepresent шлюза локальной сети VPN-устройства в локальной среде и hello VPN-подключения tooconnect шлюза с hello шлюза локальной сети. Хотя статей, которые помогают выполнить эти действия, в этой статье содержатся параметры конфигурации BGP hello необходимые toospecify hello дополнительные свойства.

![BGP между локальными сетями](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Прежде чем продолжить, убедитесь, что вы выполнили инструкции из [первой части](#enablebgp) этой статьи.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Шаг 1. Создание и настройка шлюза локальной сети hello

#### <a name="1-declare-your-variables"></a>1. Объявление переменных

В этом упражнении продолжается конфигурации hello toobuild иллюстрации hello. Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Несколько вещей toonote относительно hello параметры шлюза локальной сети:

* Hello шлюза локальной сети может быть в hello таким же или другое расположение и ресурсов группы как hello шлюза VPN. В нашем примере они располагаются в разных группах ресурсов и расположениях.
* адрес узла hello ваш адрес BGP одноранговых IP на VPN-устройства используется префикс минимальное Hello, требуется toodeclare hello шлюза локальной сети. В нашем примере это префикс /32 для адреса 10.52.255.254/32.
* Не забывайте, что для локальных сетей и виртуальной сети Azure должны быть указаны разные номера ASN BGP. Если они являются одинаковыми hello, необходимо toochange вашей виртуальной сети ASN Если VPN-устройства локальной уже использует hello ASN toopeer с соседним узлам BGP.

Прежде чем продолжить, убедитесь, что будут по-прежнему подключенных tooSubscription 1.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Создание шлюза локальной сети hello для Site5

Убедиться, что группа ресурсов hello toocreate быть в том случае, если она не была создана, прежде чем создать шлюз локальной сети hello. Обратите внимание, hello два дополнительных параметров для шлюза локальной сети hello: BgpPeerAddress и Asn.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Шаг 2 - подключения шлюза виртуальной сети hello и шлюз локальной сети

#### <a name="1-get-hello-two-gateways"></a>1. Получить hello двумя шлюзами

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Создание подключения tooSite5 TestVNet1 hello

На этом этапе можно создать подключение hello TestVNet1 tooSite5. Необходимо указать «-EnableBGP $True» tooenable BGP для этого подключения. Как было сказано ранее, это возможных toohave BGP и не BGP подключения hello же шлюза VPN Azure. Если включен протокол BGP в свойстве соединения hello, Azure не включит BGP для этого подключения несмотря на то, что параметры BGP уже настроены для обоих шлюзов.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

Hello следующий пример формирует список параметров Привет вводимых вами в hello BGP раздел конфигурации для локального VPN-устройства для этого упражнения.

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Hello подключение выполняется через несколько минут и запускает сеанс пиринга BGP hello после установления соединения IPsec hello.

## <a name ="v2vbgp"></a>Часть 3 — создание подключения между виртуальными сетями с использованием BGP

В этом разделе добавит подключение виртуальной сети для виртуальной сети с протоколом BGP, как показано на hello, следующая схема:

![BGP между виртуальными сетями](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

Привет, следуя инструкциям по-прежнему hello предыдущих шагах. Необходимо выполнить [части I](#enablebgp) toocreate hello VPN-шлюз с BGP и настроите TestVNet1. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Шаг 1 — Создание TestVNet2 и hello VPN-шлюза

Это важные toomake в том, что пространство IP-адресов hello hello новой виртуальной сети, TestVNet2, не перекрываются с диапазонов виртуальной сети.

В этом примере hello виртуальные сети относятся toohello одной подписке. Вы можете создавать подключения между виртуальным сетями из разных подписок. Дополнительные сведения см. в статье [Настройка подключения VPN-шлюза между виртуальными сетями с помощью PowerShell](vpn-gateway-vnet-vnet-rm-ps.md). Убедитесь, что добавить hello»-EnableBgp $True» при создании hello tooenable подключений BGP.

#### <a name="1-declare-your-variables"></a>1. Объявление переменных

Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
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

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Создание VPN-шлюз hello для TestVNet2 с параметрами BGP

Запрос открытый IP-адрес toobe выделенный toohello шлюза вы создадите для виртуальной сети и определите необходимые hello подсети и IP-конфигурации.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Создайте шлюз VPN hello hello как число. По умолчанию hello ASN необходимо переопределить на шлюзах Azure VPN. Hello ASN для hello подключенных виртуальных сетей должны быть разные tooenable BGP и транзитной маршрутизацией.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
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

На этом этапе можно создать hello из TestVNet1 tooTestVNet2 и hello соединению с TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Быть убедиться, что tooenable BGP для ОБОИХ подключений.
> 
> 

После выполнения этих действий, hello подключение выполняется через несколько минут. сеанс пиринга BGP Hello работает после завершения hello подключения VNet-VNet.

Если вы выполнили все три части этого упражнения, вы установили hello следующие топологии сети:

![BGP между виртуальными сетями](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Дальнейшие действия

После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
