---
title: "Параметры VPN-шлюза для распределенных подключений Azure | Документация Майкрософт"
description: "Узнайте о параметрах VPN-шлюза для шлюзов виртуальной сети Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 07aa6946b9c3994c5afc5c88837f23567b95d8a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a>Сведения о параметрах конфигурации VPN-шлюза

VPN-шлюз — это разновидность шлюза виртуальной сети, который передает зашифрованный трафик между виртуальной сетью и локальным расположением через общедоступное подключение. VPN-шлюз можно также использовать для передачи трафика между виртуальными сетями в магистрали Azure.

Подключение VPN-шлюза зависит от конфигурации нескольких ресурсов, каждый из которых содержит настраиваемые параметры. В разделах этой статьи рассматриваются ресурсы и параметры, относящиеся к VPN-шлюзу для виртуальной сети, созданной на основе модели развертывания с помощью Resource Manager. Описания и схемы топологий для каждого варианта подключения можно найти в статье [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md).

## <a name="gwtype"></a>Типы шлюзов

У каждой виртуальной сети может быть только один шлюз виртуальной сети каждого типа. При создании шлюза виртуальной сети необходимо убедиться, что в конфигурации указан правильный тип шлюза.

Для -GatewayType доступны приведенные ниже значения.

* Vpn
* ExpressRoute

Для VPN-шлюза требуется `-GatewayType` *Vpn*.

Пример:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>SKU шлюзов

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-the-gateway-sku"></a>Настройка номера SKU шлюза

#### <a name="azure-portal"></a>Портал Azure

Если для создания шлюза виртуальной сети Resource Manager используется портал Azure, выбрать SKU шлюза можно в раскрывающемся списке. Представленные параметры соответствуют выбранным типу шлюза и типу VPN.

#### <a name="powershell"></a>PowerShell

В следующем примере PowerShell используется `-GatewaySku` со значением VpnGw1.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Изменение номера SKU (размера) шлюза

Для повышения уровня SKU шлюза до более производительного можно воспользоваться командлетом PowerShell `Resize-AzureRmVirtualNetworkGateway`. С помощью этого командлета также можно перейти на более низкий уровень SKU.

В следующем примере PowerShell показано изменение размера шлюза до SKU со значением VpnGw2.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Типы подключения

В модели развертывания с помощью Resource Manager каждой конфигурации необходим определенный тип подключения шлюза виртуальной сети. Для `-ConnectionType` в PowerShell можно указать такие значения (развертывание Resource Manager):

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

В следующем примере PowerShell создается подключение типа "сеть — сеть", для которого требуется тип *IPsec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>Типы VPN

При создании шлюза виртуальной сети для конфигурации VPN-шлюза необходимо указать тип VPN. Выбор типа VPN зависит от топологии подключений, которую вы хотите создать. Например, для подключения типа "точка — сеть" требуется тип VPN на основе маршрутов. Тип VPN может также зависеть от используемого оборудования. Для конфигураций "сеть — сеть" требуется VPN-устройство. Некоторые VPN-устройства поддерживают только определенный тип VPN.

Выбранный тип VPN должен удовлетворять всем требованиям к подключению решения, которое вы хотите создать. Например, если вы хотите создать подключение VPN-шлюза типа "сеть — сеть" и подключение VPN-шлюза типа "точка — сеть" для одной и той же виртуальной сети, то вам следует использовать тип VPN *RouteBased* , так как он необходим для подключения типа "точка — сеть". Необходимо также проверить, поддерживает ли ваше VPN-устройство VPN-подключение на основе маршрутов. 

После создания шлюза виртуальной сети изменить тип VPN невозможно. Для этого потребуется удалить шлюз виртуальной сети и создать новый. Существует два типа VPN:

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

В следующем примере PowerShell используется `-VpnType` со значением *RouteBased*. При создании шлюза необходимо убедиться, что в конфигурации указано правильное значение -VpnType.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Требования к шлюзу

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Подсеть шлюза

Прежде чем создать VPN-шлюз, необходимо создать подсеть для него. Подсеть шлюза содержит IP-адреса, которые используют виртуальные машины и службы шлюза виртуальной сети. При создании шлюза виртуальной сети его виртуальные машины развертываются в подсети шлюза и на них настраиваются необходимые параметры VPN-шлюза. Ни в коем случае не следует развертывать в подсети шлюза что-либо еще (например, дополнительные виртуальные машины). Чтобы подсеть шлюза работала правильно, ее нужно назвать GatewaySubnet. Такое имя позволяет Azure определить, что это подсеть для развертывания виртуальных машин и служб шлюза виртуальной сети.

При создании подсети шлюза указывается количество IP-адресов, которое содержит подсеть. IP-адреса в подсети шлюза выделяются виртуальным машинам и службам шлюза. Некоторым конфигурациям требуется больше IP-адресов, чем прочим. Просмотрите инструкции к конфигурации, которую требуется создать, и убедитесь, что создаваемая подсеть шлюза соответствует указанным требованиям. Кроме того, необходимо убедиться, что подсеть шлюза содержит достаточно IP-адресов для дополнительных конфигураций, которые могут быть добавлены в будущем. Хотя можно создать подсеть шлюза всего лишь с размером /29, мы советуем создавать подсети с размером /28 или больше (/28, /27, /26 и т. д.). Таким образом, если в будущем вы добавите какие-либо функциональные возможности, то вам не придется разделять шлюз и удалять, а затем повторно создавать подсеть шлюза, чтобы получить больше IP-адресов.

В примере PowerShell для Resource Manager ниже показана подсеть шлюза GatewaySubnet. Здесь приведена нотация CIDR, указывающая размер /27, при котором можно использовать достаточно IP-адресов для большинства существующих конфигураций.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Локальные сетевые шлюзы

При создании конфигурации VPN-шлюза нередко шлюз локальной сети представляет ваше локальное расположение. В классической модели развертывания шлюз локальной сети называется "локальным сайтом". 

Для локального сетевого шлюза следует задать имя и общий IP-адрес локального VPN-устройства, а также указать префиксы адресов, принадлежащие к локальному расположению. Azure проверяет наличие сетевого трафика по префиксам адресов назначения, учитывает конфигурацию, указанную для локального сетевого шлюза, и соответствующим образом направляет пакеты. Можно также указать шлюзы локальной сети для конфигураций типа "виртуальная сеть — виртуальная сеть", использующих подключение к VPN-шлюзу.

Следующий пример PowerShell создает шлюз локальной сети.

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Иногда возникает необходимость изменить параметры локального сетевого шлюза. Например, при добавлении или изменении диапазона адресов, либо при изменении IP-адреса VPN-устройства. Для классической виртуальной сети эти параметры можно изменить на классическом портале, на странице "Локальные сети". В случае использования Resource Manager ознакомьтесь с разделом [Изменение параметров шлюза локальной сети с помощью PowerShell](vpn-gateway-modify-local-network-gateway.md).

## <a name="resources"></a>Интерфейсы REST API и командлеты PowerShell

Дополнительные технические материалы и специальные требования к синтаксису, действующие при использовании интерфейсов REST API, командлетов PowerShell или Azure CLI для настройки конфигураций VPN-шлюзов, доступны на приведенных ниже страницах.

| **Классический** | **Диспетчер ресурсов** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [ИНТЕРФЕЙС REST API](https://msdn.microsoft.com/library/jj154113) |[REST API](/rest/api/network/virtualnetworkgateways) |
| Не поддерживается | [Интерфейс командной строки Azure](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о доступных конфигурациях подключений см. в статье [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md).