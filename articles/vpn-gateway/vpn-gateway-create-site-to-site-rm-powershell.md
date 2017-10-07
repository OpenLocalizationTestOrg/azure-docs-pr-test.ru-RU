---
title: "Подключение к локальной сети tooan виртуальной сети Azure: через виртуальную Частную сеть для: PowerShell | Документы Microsoft"
description: "Действия toocreate соединении по протоколу IPsec в локальной сети tooan виртуальной сети Azure через hello общедоступный Интернет. Они помогут вам создать подключение типа \"сеть — сеть\" с использованием VPN-шлюза и PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью PowerShell

В этой статье показано, как toouse toocreate сайта для сайта PowerShell VPN-подключения шлюза в локальной сети toohello виртуальной сети. в этой статье инструкциям Hello применяются toohello модели развертывания диспетчера ресурсов. Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Портал Azure (классический)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Классический портал (классическая модель)](vpn-gateway-site-to-site-create.md)
> 
>


Используется tooconnect — подключение через виртуальную Частную сеть для шлюза в локальной сети tooan виртуальной сети Azure через туннель VPN IPsec/IKE (IKEv1 или IKEv2). Этот тип подключения требуется VPN устройства, расположенного в локальной среде, имеет внешний tooit открытый IP-адрес, назначенный. Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpngateways.md).

![Схема подключения типа "сеть — сеть" через VPN-шлюз](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>Перед началом работы

Убедитесь, что выполнены следующие условия перед началом настройки hello:

* Убедитесь, что у вас есть совместимых устройств VPN и тем, кто имеет доступ tooconfigure его. Дополнительные сведения о совместимых устройствах VPN и их настройке см. в [этой статье](vpn-gateway-about-vpn-devices.md).
* Убедитесь, что у вас есть общедоступный IPv4–адрес для вашего VPN–устройства. Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).
* Если вы не знакомы с hello диапазоны IP-адресов в вашей локальной сети, конфигурации, необходимо toocoordinate с тем, кто сможет предоставить эти сведения для вас. При создании этой конфигурации необходимо указать что Azure будет направлять в локальное расположение tooyour диапазон префиксов hello IP-адресов. Ни один из подсетей hello в локальной сети можно через Знакомство с функциями с hello подсети виртуальной сети, которые будут tooconnect для.
* Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure. Командлеты PowerShell часто обновляются, и обычно требуется tooupdate PowerShell командлеты tooget hello последние функции функциональные возможности по работе. Если не обновлять ваш командлеты PowerShell, hello значений, заданных может завершиться ошибкой. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения о загрузке и установке командлетов PowerShell.

### <a name="example"></a>Примеры значений

Hello примерах в этой статье используется hello следующие значения. Можно использовать эти значения toocreate тестовой среде, или ссылаться toothem toobetter понять hello примеры в этой статье.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Подключение tooyour подписки

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. Создание виртуальной сети и подсети шлюза

Если у вас нет виртуальной сети, создайте ее. При создании виртуальной сети, убедитесь, что hello адресные пространства, указываемые не перекрываются hello адресных пространств, в которых в локальной сети.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate виртуальную сеть и подсеть шлюза

В этом примере создается виртуальная сеть и подсеть шлюза. При наличии виртуальной сети, которая требуется подсеть шлюза, чтобы увидеть tooadd [tooadd шлюз подсети tooa виртуальная сеть уже создан](#gatewaysubnet).

Создайте группу ресурсов:

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

Создайте свою виртуальную сеть.

1. Установка переменных hello.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Создайте hello виртуальной сети.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>tooadd tooa шлюз подсети виртуальной сети уже создан

1. Установка переменных hello.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Создайте подсеть шлюза hello.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Задание конфигурации hello.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Создание шлюза локальной сети hello

шлюз локальной сети Hello обычно относится tooyour в локальном расположении. Присвоить имя, на который Azure можно ссылаться tooit, а затем укажите hello IP-адрес сайта hello объекта toowhich устройство VPN локальной hello будет создавать подключение. Можно также указать префиксов hello IP-адресов, которые будет проходить через устройство VPN toohello шлюза VPN hello. префиксы адресов Hello, указываемые являются префиксы hello в локальной сети. Если изменяется в локальной сети, можно легко обновлять префиксы hello.

Используйте hello следующие значения:

* Hello *GatewayIPAddress* — hello IP-адрес локального VPN-устройства. Ваше VPN-устройство не может располагаться вне преобразования сетевых адресов (NAT).
* Hello *AddressPrefix* это в локальной памяти.

tooadd шлюз локальной сети с префиксом один адрес:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

tooadd шлюза локальной сети с помощью нескольких префиксов адреса:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

toomodify префиксов IP-адресов для шлюза локальной сети:<br>
Иногда префиксы адресов шлюза локальной сети могут изменяться. Hello действия можно предпринять toomodify IP-адреса, от которых зависят префиксы создали шлюза VPN-подключения. В разделе hello [префиксов изменение IP-адресов для шлюза локальной сети](#modify) этой статьи.

## <a name="PublicIP"></a>4. Запрос общедоступного IP-адреса

VPN-шлюз должен иметь общедоступный IP-адрес. Запросить ресурс IP-адреса hello и затем ссылаться tooit при создании шлюз виртуальной сети. Hello IP-адрес назначается динамически toohello ресурсов при создании шлюза VPN hello. В настоящее время VPN-шлюз поддерживает только *динамическое* выделение общедоступных IP-адресов. Вы не можете запросить назначение статического общедоступного IP-адреса. Однако это не означает, что hello IP-адрес изменяется после назначения tooyour VPN-шлюз. только один раз Hello изменения адреса hello общедоступный IP-адрес когда hello шлюза будет удалена и создана заново. При изменении размера, сбросе или других внутренних операциях обслуживания или обновления IP-адрес VPN-шлюза не изменяется.

Запрос общедоступный IP-адрес, который будет назначен tooyour виртуальной сети шлюза VPN.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Создайте адресации конфигурации IP-адрес шлюза hello

Конфигурация шлюза Hello определяет подсеть hello и hello открытый IP адрес toouse. Используйте следующий пример toocreate hello конфигурацию шлюза.

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Создание шлюза VPN hello

Создание шлюза VPN hello виртуальной сети. Создание VPN-шлюза может занять too45 минут или более toocomplete.

Используйте hello следующие значения:

* Hello *- тип шлюза* для сайта для сайта конфигурации — *Vpn*. Тип шлюза Hello распространяется всегда конкретных toohello реализации. Например, для других конфигураций шлюза может потребоваться тип шлюза ExpressRoute.
* Hello *- VpnType* может быть *routebased* (называется tooas шлюза с динамической некоторые документы), или *PolicyBased* (называется tooas статический шлюз некоторые документы ). Дополнительные сведения о типах VPN-шлюзов см. в статье [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md).
* Выберите номер SKU шлюза, которые должны toouse hello. К определенным номерам SKU применяются ограничения настройки. Дополнительные сведения см. в разделе о [номерах SKU шлюзов](vpn-gateway-about-vpn-gateway-settings.md#gwsku). Если возникает ошибка при создании шлюза VPN hello относительно hello - GatewaySku, проверьте, установить последнюю версию hello hello командлеты PowerShell.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. Настройка устройства VPN

Для межсайтовых подключений tooan локальной сети требуется VPN-устройства. На этом этапе мы настроим VPN-устройство. Во время настройки устройства VPN, необходимо hello следующее:

- Общий ключ. Это является hello того же самого общего ключа, указанного при создании через виртуальную Частную сеть для подключения. В наших примерах мы используем простые общие ключи. Рекомендуется создавать более сложные ключа toouse.
- Здравствуйте, общедоступный IP-адрес шлюза виртуальной сети. Hello общедоступный IP-адрес можно просмотреть с помощью hello портал Azure, PowerShell или интерфейс командной строки. hello toofind общедоступный IP-адрес шлюза виртуальной сети с помощью PowerShell, hello используйте следующий пример:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Создание VPN-подключения hello

Создайте подключение через виртуальную Частную сеть для hello между шлюз виртуальной сети и VPN-устройства. Быть убедиться, что значениями hello tooreplace собственными. Hello общий ключ должен соответствовать hello значение, которое используется для конфигурации устройства VPN. Обратите внимание, что hello "-тип подключения" сеть-сеть является *IPsec*.

1. Установка переменных hello.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Создание подключения hello.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

Через некоторое время hello будет установлено подключение.

## <a name="toverify"></a>9. Проверьте hello VPN-подключения

Существует несколько способов tooverify VPN-подключение.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa виртуальной машины

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>Изменение префиксов IP-адресов для шлюза локальной сети

Если изменить префиксов hello IP-адресов, которые должны направляться в локальное расположение tooyour, можно изменить hello шлюза локальной сети. Мы приводим два набора инструкций. инструкции Hello выбранного зависят от того, уже создали подключения шлюза.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>Изменить IP-адрес шлюза hello шлюза локальной сети

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

*  После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. Дополнительные сведения о виртуальных машинах см. [здесь](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
