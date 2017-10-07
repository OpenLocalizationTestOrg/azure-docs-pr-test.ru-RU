---
title: "Подключение к локальной сети tooan виртуальной сети Azure: через виртуальную Частную сеть для: CLI | Документы Microsoft"
description: "Действия toocreate соединении по протоколу IPsec в локальной сети tooan виртуальной сети Azure через hello общедоступный Интернет. Они помогут вам создать подключение типа \"сеть — сеть\" с использованием VPN-шлюза и интерфейса командной строки."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>Создание виртуальной сети с VPN типа "сеть — сеть" с помощью интерфейса командной строки

В этой статье показано, как toouse hello Azure CLI toocreate через виртуальную Частную сеть для подключения шлюза из вашей локальной сети toohello виртуальной сети. в этой статье инструкциям Hello применяются toohello модели развертывания диспетчера ресурсов. Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.<br>

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Портал Azure (классический)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Схема подключения типа "сеть — сеть" через VPN-шлюз](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

Используется tooconnect — подключение через виртуальную Частную сеть для шлюза в локальной сети tooan виртуальной сети Azure через туннель VPN IPsec/IKE (IKEv1 или IKEv2). Этот тип подключения требуется VPN устройства, расположенного в локальной среде, имеет внешний tooit открытый IP-адрес, назначенный. Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpngateways.md).

## <a name="before-you-begin"></a>Перед началом работы

Убедитесь, что выполнены следующие условия перед началом настройки hello:

* Убедитесь, что у вас есть совместимых устройств VPN и тем, кто имеет доступ tooconfigure его. Дополнительные сведения о совместимых устройствах VPN и их настройке см. в [этой статье](vpn-gateway-about-vpn-devices.md).
* Убедитесь, что у вас есть общедоступный IPv4–адрес для вашего VPN–устройства. Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).
* Если вы не знакомы с hello диапазоны IP-адресов в вашей локальной сети, конфигурации, необходимо toocoordinate с тем, кто сможет предоставить эти сведения для вас. При создании этой конфигурации необходимо указать что Azure будет направлять в локальное расположение tooyour диапазон префиксов hello IP-адресов. Ни один из подсетей hello в локальной сети можно через Знакомство с функциями с hello подсети виртуальной сети, которые будут tooconnect для.
* Убедитесь, что установки последней версии hello команды CLI (2.0 или более поздней версии). Сведения об установке hello командах CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-azure-cli) и [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).

### <a name="example"></a>Примеры значений

Можно использовать следующие значения toocreate тестовой среде hello, или ссылаться toothese значения toobetter понять hello примеры в этой статье:

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1. Подключение tooyour подписки

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. Создание группы ресурсов

Hello пример создает группу ресурсов с именем «TestRG1» в расположении «eastus» hello. При наличии группы ресурсов в регионе hello требуется toocreate виртуальной сети, что один можно использовать вместо этого.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. Создать виртуальную сеть

Если у вас еще нет виртуальной сети, создайте его с помощью hello [создания az сети vnet](/cli/azure/network/vnet#create) команды. При создании виртуальной сети, убедитесь, что hello адресные пространства, указываемые не перекрываются hello адресных пространств, в которых в локальной сети.

Hello следующий пример создает виртуальную сеть с именем «TestVNet1» и подсеть, «Подсети1».

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Создать подсеть шлюза hello

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

Для этой конфигурации необходима также подсеть шлюза. шлюз виртуальной сети Hello использует подсеть шлюза, содержащий hello IP-адреса, используемые службами шлюза VPN hello. При создании подсеть шлюза нужно назвать GatewaySubnet. Если будет присвоено другое имя, вы создадите подсеть, но Azure не будет рассматривать ее как подсеть шлюза.

размер Hello подсеть шлюза hello зависит от настройки шлюза VPN hello, которые должны toocreate. Хотя возможных toocreate как /29 подсеть шлюза, рекомендуется создать подсеть большего размера, включающий несколько адресов, выбрав /27 или /28. Использование большего подсеть шлюза позволяет недостаточно IP-адреса tooaccommodate возможных будущих конфигураций.

Используйте hello [создать подсеть виртуальной сети сети az](/cli/azure/network/vnet/subnet#create) подсеть шлюза hello toocreate команды.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Создание шлюза локальной сети hello

шлюз локальной сети Hello обычно относится tooyour в локальном расположении. Присвоить имя, на который Azure можно ссылаться tooit, а затем укажите hello IP-адрес сайта hello объекта toowhich устройство VPN локальной hello будет создавать подключение. Можно также указать префиксов hello IP-адресов, которые будет проходить через устройство VPN toohello шлюза VPN hello. префиксы адресов Hello, указываемые являются префиксы hello в локальной сети. Если изменяется в локальной сети, можно легко обновлять префиксы hello.

Используйте hello следующие значения:

* Hello *— IP-адрес шлюза* hello IP-адрес локального VPN-устройства. Ваше VPN-устройство не может располагаться вне преобразования сетевых адресов (NAT).
* Hello *--префиксы для адресов локального* являются локальными адресных пространств.

Используйте hello [Создание локальной сети az-шлюз](/cli/azure/network/local-gateway#create) tooadd команда шлюза локальной сети с помощью нескольких префиксов адреса:

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. Запрос общедоступного IP-адреса

VPN-шлюз должен иметь общедоступный IP-адрес. Запросить ресурс IP-адреса hello и затем ссылаться tooit при создании шлюз виртуальной сети. Hello IP-адрес назначается динамически toohello ресурсов при создании шлюза VPN hello. В настоящее время VPN-шлюз поддерживает только *динамическое* выделение общедоступных IP-адресов. Вы не можете запросить назначение статического общедоступного IP-адреса. Однако это не означает, что hello IP-адрес изменяется после назначения tooyour VPN-шлюз. только один раз Hello изменения адреса hello общедоступный IP-адрес когда hello шлюза будет удалена и создана заново. При изменении размера, сбросе или других внутренних операциях обслуживания или обновления IP-адрес VPN-шлюза не изменяется.

Используйте hello [создания сети az public-ip](/cli/azure/network/public-ip#create) toorequest команда динамического общедоступный IP-адрес.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Создание шлюза VPN hello

Создание шлюза VPN hello виртуальной сети. Создание VPN-шлюза может занять too45 минут или более toocomplete.

Используйте hello следующие значения:

* Hello *--тип шлюза* для сайта для сайта конфигурации — *Vpn*. Тип шлюза Hello распространяется всегда конкретных toohello реализации. Дополнительные сведения см. в разделе [Типы шлюзов](vpn-gateway-about-vpn-gateway-settings.md#gwtype).
* Hello *тип vpn —* может быть *routebased* (называется tooas шлюза с динамической некоторые документы), или *PolicyBased* (называется tooas статический шлюз в некоторых документация). приветствия равен конкретных toorequirements hello устройство, которое вы подключаетесь. Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpn-gateway-settings.md#vpntype).
* Выберите номер SKU шлюза, которые должны toouse hello. К определенным номерам SKU применяются ограничения настройки. Дополнительные сведения см. в разделе о [номерах SKU шлюзов](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

Создание шлюза VPN hello, с помощью hello [Создание виртуальной сети — шлюз сети az](/cli/azure/network/vnet-gateway#create) команды. При выполнении этой команды, с помощью hello параметр «--no - wait», вы не видите любой отзыв или выходных данных. Этот параметр позволяет toocreate шлюза hello в фоновом режиме hello. Занимает около 45 минут toocreate шлюз.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. Настройка устройства VPN

Для межсайтовых подключений tooan локальной сети требуется VPN-устройства. На этом этапе мы настроим VPN-устройство. Во время настройки устройства VPN, необходимо hello следующее:

- Общий ключ. Это является hello того же самого общего ключа, указанного при создании через виртуальную Частную сеть для подключения. В наших примерах мы используем простые общие ключи. Рекомендуется создавать более сложные ключа toouse.
- Здравствуйте, общедоступный IP-адрес шлюза виртуальной сети. Hello общедоступный IP-адрес можно просмотреть с помощью hello портал Azure, PowerShell или интерфейс командной строки. toofind hello общедоступный IP-адрес шлюза виртуальной сети, используйте hello [список открытый ip-сетей az](/cli/azure/network/public-ip#list) команды. Для облегчения процесса чтения hello выводится форматированный toodisplay hello список общедоступных IP-адресов в формате таблицы.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Создание VPN-подключения hello

Создайте hello сеть-сеть VPN-подключение между шлюзом виртуальной сети и локальным VPN-устройства. Оплата особое внимание toohello общего ключа значение, которое должно соответствовать hello настроен общий значение ключа для VPN-устройства.

Hello-подключение с помощью hello [создать az сети vpn подключения](/cli/azure/network/vpn-connection#create) команды.

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

Через некоторое время hello будет установлено подключение.

## <a name="toverify"></a>10. Проверьте hello VPN-подключения

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

Если требуется другой метод tooverify toouse подключения, в разделе [Проверка подключения к VPN-шлюз](vpn-gateway-verify-connection-resource-manager.md).

## <a name="connectVM"></a>tooconnect tooa виртуальной машины

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>Стандартные задачи

Этот раздел содержит общие команды, которые могут быть полезны при работе с конфигурациями подключения типа "сайт — сайт". Hello полный список сетевые команды CLI см. в разделе [Azure CLI - сети](/cli/azure/network).

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

* После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. Дополнительные сведения о виртуальных машинах см. [здесь](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Сведения о принудительном туннелировании см. в статье [Настройка принудительного туннелирования с помощью классической модели развертывания](vpn-gateway-forced-tunneling-rm.md).
* Сведения о высокодоступных подключениях в режиме "активный — активный" см. в статье [Настройка высокодоступных подключений: распределенных и между виртуальными сетями](vpn-gateway-highlyavailable.md).
* Список сетевых команд Azure CLI см. в статье об [Azure CLI](https://docs.microsoft.com/cli/azure/network).