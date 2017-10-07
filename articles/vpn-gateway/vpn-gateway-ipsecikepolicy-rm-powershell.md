---
title: "Настройка политики IPsec/IKE для VPN-подключений типа \"сеть — сеть\" или \"виртуальная сеть — виртуальная сеть\". Azure Resource Manager: PowerShell | Документация Майкрософт"
description: "В этой статье описана настройка политики IPsec/IKE для подключений типа \"сеть — сеть\" или \"виртуальная сеть — виртуальная сеть\" с VPN-шлюзами Azure с помощью Azure Resource Manager и PowerShell."
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a>Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"

В этой статье рассматриваются tooconfigure hello действия политики IPsec/IKE для соединений через виртуальную Частную сеть для или виртуальной сети для виртуальной сети, с помощью модели развертывания диспетчера ресурсов hello и PowerShell.

## <a name="about"></a>Параметры политики IPsec и IKE для VPN-шлюзов Azure
Стандарт протоколов IPsec и IKE поддерживает широкий набор алгоритмов шифрования в различных сочетаниях. См. слишком[о требованиях шифрования и VPN-шлюзы Azure](vpn-gateway-about-compliance-crypto.md) toosee, как это может помочь, обеспечивая между организациями и подключения к виртуальной сети для виртуальной сети удовлетворяют требованиям соответствия и безопасности.

В этой статье предоставляет toocreate инструкции и настроить политику IPsec/IKE и применить tooa существующего или нового соединения.

* [Часть 1 - toocreate рабочего процесса и задать политику IPsec/IKE](#workflow)
* [Часть 2. Поддерживаемые алгоритмы шифрования и уровни стойкости ключей](#params)
* [Часть 3. Создание нового подключения VPN типа "сеть — сеть" с помощью политики IPsec/IKE](#crossprem)
* [Часть 4. Создание нового подключения VPN типа "виртуальная сеть — виртуальная сеть" с помощью политики IPsec/IKE](#vnet2vnet)
* [Часть 5. Управление политикой IPsec/IKE (а также ее создание, добавление и удаление) для подключения](#managepolicy)

> [!IMPORTANT]
> 1. Обратите внимание, что политики IPsec/IKE работает только на hello, следуя SKU шлюза.
>    * ***VpnGw1, VpnGw2, VpnGw3*** (на основе маршрутов);
>    * ***Standard*** и ***HighPerformance*** (на основе маршрутов).
> 2. Можно указать только ***одну*** комбинацию политик для каждого подключения.
> 3. Вам следует указать все алгоритмы и параметры для IKE (основной режим) и IPsec (быстрый режим). Указать частичную политику нельзя.
> 4. Обратитесь к спецификации поставщиков устройств VPN политики tooensure hello поддерживается на устройствах VPN локальной. S2S или подключения к виртуальной сети для виртуальной сети не удается установить, если политики hello несовместимы.

## <a name ="workflow"></a>Часть 1 - toocreate рабочего процесса и задать политику IPsec/IKE
В этом разделе представлен краткий обзор hello политики рабочих процессов toocreate и обновление IPsec/IKE для подключения S2S VPN или виртуальной сети для виртуальной сети.
1. Создание виртуальной сети и VPN-шлюза.
2. Создание шлюза локальной сети для локального подключения или другой виртуальной сети и шлюза для подключения типа "виртуальная сеть — виртуальная сеть".
3. Создание политики IPsec/IKE с выбранными алгоритмами и параметрами.
4. Создайте соединение (IPsec или VNet2VNet) с помощью политики IPsec/IKE hello
5. Добавление, обновление и удаление политики IPsec/IKE для существующего подключения.

инструкции Hello в этой статье поможет вам установить и настроить политики IPsec/IKE, как показано на диаграмме hello:

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <a name ="params"></a>Часть 2. Поддерживаемые алгоритмы шифрования и уровни стойкости ключей

Hello следующей таблице перечислены hello поддерживается алгоритмов шифрования и значений длины ключа можно настроить hello клиентами.

| **IPsec/IKEv2**  | **Варианты**    |
| ---  | --- 
| Шифрование IKEv2 | AES256, AES192, AES128, DES3, DES  
| Проверка целостности IKEv2  | SHA384, SHA256, SHA1, MD5  |
| Группа DH         | DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, нет |
| Шифрование IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, нет    |
| Целостность IPsec  | GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5 |
| Группа PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, нет 
| Время существования QM SA   | (**Необязательно** — используются значения по умолчанию, если не заданы другие значения.)<br>Секунды (целое число, **минимум 300**, по умолчанию — 27 000 с)<br>Килобайты (целое число, **минимум 1024**, по умолчанию — 102 400 000 КБ)   |
| Селектор трафика | UsePolicyBasedTrafficSelectors** ($True/$False; **необязательно** — по умолчанию используется значение $False, если не задано другое значение.)    |
|  |  |

> [!IMPORTANT]
> 1. **Если GCMAES используется как для алгоритма шифрования IPsec, необходимо выбрать hello того же алгоритма GCMAES и длину ключа для проверки целостности IPsec; Например с помощью GCMAES128 для обоих**
> 2. Время существования сопоставления безопасности основного режима IKEv2 имеет фиксированный размер 28800 секунд на шлюзах Azure VPN hello
> 3. Параметр «UsePolicyBasedTrafficSelectors» слишком $ значение True, если соединение будет настраивать hello Azure VPN шлюза tooconnect toopolicy VPN брандмауэр на локальном компьютере. При включении PolicyBasedTrafficSelectors необходимо tooensure устройство VPN имеет соответствующий трафик селекторы hello определенных все сочетания свои префиксы (шлюз локальной сети) в локальной сети из префиксов hello виртуальной сети Azure, Вместо any к any. Например при свои префиксы в локальной сети, 10.1.0.0/16 и 10.2.0.0/16 и префиксы вашей виртуальной сети: 192.168.0.0/16 и 172.16.0.0/16, необходимо toospecify hello, следуя селекторы трафика:
>    * 10.1.0.0/16 <====> 192.168.0.0/16;
>    * 10.1.0.0/16 <====> 172.16.0.0/16;
>    * 10.2.0.0/16 <====> 192.168.0.0/16;
>    * 10.2.0.0/16 <====> 172.16.0.0/16.

Дополнительные сведения о селекторах трафика на основе политик см. в статье [Подключение VPN-шлюзов Azure к нескольким локальным VPN-устройствам на основе политики с помощью PowerShell](vpn-gateway-connect-multiple-policybased-rm-ps.md).

Привет, в следующей таблице перечислены hello соответствующие группы Диффи-Хелмана, поддерживаемых hello пользовательской политики:

| **Группа Диффи-Хелмана**  | **DHGroup**              | **PFSGroup** | **Длина ключа** |
| --- | --- | --- | --- |
| 1                         | DHGroup1                 | PFS1         | MODP (768 бит)   |
| 2                         | DHGroup2                 | PFS2         | MODP (1024 бит)  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP (2048 бит)  |
| 19                        | ECP256                   | ECP256       | ECP (256 бит)    |
| 20                        | ECP384                   | ECP284       | ECP (384 бит)    |
| 24                        | DHGroup24                | PFS24        | MODP (2048 бит)  |

См. слишком[RFC3526](https://tools.ietf.org/html/rfc3526) и [RFC5114](https://tools.ietf.org/html/rfc5114) для получения дополнительных сведений.

## <a name ="crossprem"></a>Часть 3. Создание нового подключения VPN типа "сеть — сеть" с помощью политики IPsec/IKE

В этом разделе содержится описание этапов hello создания с помощью политик IPsec/IKE S2S VPN-подключения. Hello описанной ниже процедуре создается подключение hello согласно схеме hello:

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

Пошаговые инструкции по созданию VPN-подключения типа "сеть — сеть" см. в статье [Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md).

### <a name="before"></a>Перед началом работы

* Убедитесь в том, что у вас уже есть подписка Azure. Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).
* Установите командлеты PowerShell диспетчера ресурсов Azure hello. В разделе [Обзор Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.

### <a name="createvnet1"></a>Шаг 1 — Создание hello виртуальной сети, шлюз виртуальной частной сети и шлюза локальной сети

#### <a name="1-declare-your-variables"></a>1. Объявление переменных

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Подключить tooyour подписки и создать новую группу ресурсов

Убедитесь, что переключение tooPowerShell режим toouse hello командлеты диспетчера ресурсов. Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).

Откройте консоль PowerShell и подключить tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>3. Создание виртуальной сети hello, шлюза VPN и шлюза локальной сети

Следующий образец Hello создает виртуальную сеть hello, TestVNet1, три подсети и шлюз VPN hello. При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet. Если вы используете другое имя, создание шлюза завершится сбоем.

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

### <a name="s2sconnection"></a>Шаг 2. Создание VPN-подключения типа "сеть — сеть" с помощью политики IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Создайте политику IPsec/IKE

Следующий пример скрипта Hello создает политику IPsec/IKE с hello следующие алгоритмы и параметры:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

Если вы используете GCMAES для IPsec, необходимо использовать hello того же алгоритма GCMAES и длину ключа для шифрования IPsec и целостности данных, например:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: **GCMAES256, GCMAES256**, PFS24, время существования SA (7200 секунд), 2048 КБ

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a>2. Создание hello S2S VPN-подключения с hello политики IPsec/IKE

Подключение к S2S VPN создавать и применять политики IPsec/IKE hello, созданного ранее.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

При необходимости можно добавить «-UsePolicyBasedTrafficSelectors $True» toohello создать подключение командлет tooenable Azure VPN шлюза tooconnect основе toopolicy VPN-устройства на локальном компьютере, как описано выше.

> [!IMPORTANT]
> После политику IPsec/IKE для подключения, hello VPN-шлюз Azure только отправить или принять предложение hello IPsec/IKE с указанным алгоритмов шифрования и значений длины ключа для этого конкретного соединения. Убедитесь, что устройство VPN локальной для соединения hello использует или принимает сочетание hello точное политики, в противном случае не устанавливает туннель S2S VPN hello.


## <a name ="vnet2vnet"></a>Часть 4. Создание нового подключения VPN типа "виртуальная сеть — виртуальная сеть" с помощью политики IPsec/IKE

Hello шаги создания подключения виртуальной сети для виртуальной сети с помощью политик IPsec/IKE, аналогичные toothat S2S VPN-подключения. Hello следующие примеры сценариев создайте hello подключение как показано на диаграмме hello:

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

Подробные инструкции по созданию подключения типа "виртуальная сеть — виртуальная сеть" см. в статье [Настройка подключения VPN-шлюза между виртуальными сетями с помощью PowerShell](vpn-gateway-vnet-vnet-rm-ps.md). Необходимо выполнить [часть 3](#crossprem) toocreate hello шлюза VPN и настроите TestVNet1.

### <a name="createvnet2"></a>Шаг 1 — Создание hello второй виртуальной сети и шлюза VPN

#### <a name="1-declare-your-variables"></a>1. Объявление переменных

Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a>2. Создание hello второй виртуальной сети и шлюза VPN в новую группу ресурсов hello

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a>Шаг 2 — Создание виртуальной сети toVNet соединение со hello политики IPsec/IKE

Аналогичные toohello S2S VPN-подключения, создайте политику IPsec/IKE, а затем применить toopolicy toohello новое соединение.

#### <a name="1-create-an-ipsecike-policy"></a>1. Создайте политику IPsec/IKE

Следующий пример скрипта Hello создает различные политики IPsec/IKE с hello следующие алгоритмы и параметры:
* IKEv2: AES128, SHA1, DHGroup14
* IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a>2. Создание подключения к виртуальной сети для виртуальной сети с hello политики IPsec/IKE

Создание подключения VNet-VNet и применение hello созданной вами политикой IPsec/IKE. В этом примере обоих шлюзов находятся в hello одной подписке. Поэтому его невозможно toocreate и настроить оба соединения с hello же политики IPsec/IKE в hello одного сеанса PowerShell.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> После политику IPsec/IKE для подключения, hello VPN-шлюз Azure только отправить или принять предложение hello IPsec/IKE с указанным алгоритмов шифрования и значений длины ключа для этого конкретного соединения. Убедитесь, что hello политики IPsec для оба соединения являются hello совпадают, в противном случае не будет установить подключение виртуальной сети для виртуальной сети.

После выполнения этих действий, hello подключения через несколько минут, и вы получите следующие топологии сети, как показано в начале hello hello:

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <a name ="managepolicy"></a>Часть 5. Обновление политики IPsec/IKE для подключения

Hello последнего раздела показано, как toomanage политики IPsec/IKE для существующего подключения S2S или виртуальной сети для виртуальной сети. Упражнение Hello ниже руководстве hello после операции подключения.

1. Показать политики IPsec/IKE hello соединения
2. Добавление или обновление подключения tooa политики IPsec/IKE hello
3. Удалить политику IPsec/IKE hello подключения

Hello же действия относятся tooboth S2S и подключения к виртуальной сети для виртуальной сети.

> [!IMPORTANT]
> Политика IPsec/IKE поддерживается только для *стандартных* и *высокопроизводительных* VPN-шлюзов на основе маршрутов. Он не поддерживает hello базовый номер SKU шлюза или шлюза VPN на основе политики hello.

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a>1. Показать политики IPsec/IKE hello соединения

Hello в следующем примере показано, как tooget hello политика IPsec/IKE на соединение. сценарии Hello также продолжить из упражнения hello выше.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

Последняя команда Hello список hello настроен для подключения hello текущую политику IPsec/IKE, если оно назначено. Следующий пример выходных данных Hello предназначен для hello подключения:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

В случае без настроенной политики IPsec/IKE hello команды (PS > $connection6.policy) возвращает пустой возврата. Это не означает IPsec/IKE не настроена на подключение hello, но это не настраиваемой политики IPsec/IKE. Hello фактическое соединение использует политику по умолчанию hello согласовывается между локальным устройством VPN и VPN-шлюз Azure hello.

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a>2. Добавление или обновление политики IPsec/IKE для подключения

Hello шаги tooadd новой политики или обновление существующей политики на подключение, hello же: создать новую политику, а затем применить hello новое подключение toohello политики.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

добавить tooenable «UsePolicyBasedTrafficSelectors» при подключении tooan локальных VPN-устройства на основе политик hello «-UsePolicyBaseTrafficSelectors» параметра toohello командлета, или задайте для него слишком параметр hello $False toodisable:

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

Можно получить подключение hello снова toocheck при обновлении политики hello.

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

Вы увидите hello вывод последнюю строку hello, как показано в следующий пример hello:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a>3. Удаление политики IPsec/IKE из подключения

После удаления hello настраиваемой политики из соединения, hello VPN-шлюз Azure переходит назад toohello [по умолчанию список предложений IPsec/IKE](vpn-gateway-about-vpn-devices.md) и снова согласовывает с локальными VPN-устройства.

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

Можно использовать hello toocheck же скрипт, если политика hello удалена из соединения hello.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о селекторах трафика на основе политик см. в статье [Подключение VPN-шлюзов Azure к нескольким локальным VPN-устройствам на основе политики с помощью PowerShell](vpn-gateway-connect-multiple-policybased-rm-ps.md).

После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
