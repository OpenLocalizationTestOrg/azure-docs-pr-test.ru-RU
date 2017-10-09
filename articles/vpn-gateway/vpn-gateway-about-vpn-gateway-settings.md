---
title: "Параметры шлюза aaaVPN для соединения с Azure между организациями | Документы Microsoft"
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
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a>Сведения о параметрах конфигурации VPN-шлюза

VPN-шлюз — это разновидность шлюза виртуальной сети, который передает зашифрованный трафик между виртуальной сетью и локальным расположением через общедоступное подключение. Также можно использовать VPN-шлюз toosend трафика между виртуальными сетями через hello Azure магистрали.

Шлюз VPN-подключения зависит от конфигурации hello несколько ресурсов, каждый из которых содержит настраиваемые параметры. Hello в этой статье описываются hello ресурсы и параметры, связанные tooa VPN-шлюз для виртуальной сети, созданной в модели развертывания диспетчера ресурсов. Можно найти описания и схемы топологии для каждого подключения решения в hello [о VPN-шлюз](vpn-gateway-about-vpngateways.md) статьи.

## <a name="gwtype"></a>Типы шлюзов

У каждой виртуальной сети может быть только один шлюз виртуальной сети каждого типа. При создании шлюза виртуальной сети, необходимо проверить правильность hello типа шлюза для конфигурации.

могут Hello доступные значения — тип шлюза.

* Vpn
* ExpressRoute

VPN-шлюза требует hello `-GatewayType` *Vpn*.

Пример:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>SKU шлюзов

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>Настройка шлюза hello SKU

#### <a name="azure-portal"></a>Портал Azure

Если вы используете hello Azure портала toocreate шлюз виртуальной сети диспетчер ресурсов, можно выбрать номер SKU шлюза hello с помощью раскрывающегося списка hello. Параметры Hello решаемой соответствуют toohello тип шлюза и выбранного типа VPN.

#### <a name="powershell"></a>PowerShell

Hello PowerShell пример указывает hello `-GatewaySku` как VpnGw1.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Изменение номера SKU (размера) шлюза

Если требуется tooupgrade вашей tooa SKU шлюза SKU более широкими возможностями, можно использовать hello `Resize-AzureRmVirtualNetworkGateway` командлета PowerShell. Также можно понизить размер SKU шлюза hello, с помощью этого командлета.

Следующий пример PowerShell Hello показывает, что шлюз SKU изменяющего tooVpnGw2.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Типы подключения

В модели развертывания диспетчера ресурсов hello каждой конфигурации требуется тип подключения шлюза конкретной виртуальной сети. Hello доступные PowerShell диспетчера ресурсов значения `-ConnectionType` являются:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

В следующем примере PowerShell hello, мы создадим S2S подключение, требующее тип подключения hello *IPsec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>Типы VPN

При создании hello шлюз виртуальной сети для настройки шлюза VPN, необходимо указать тип VPN. Hello Выбор типа VPN зависит от топологии hello подключения, которые должны toocreate. Например, для подключения типа "точка — сеть" требуется тип VPN на основе маршрутов. Тип VPN также может зависеть от оборудования hello, в которых используется. Для конфигураций "сеть — сеть" требуется VPN-устройство. Некоторые VPN-устройства поддерживают только определенный тип VPN.

Hello выбранного типа VPN должен удовлетворять всем требованиям hello соединения для решения hello необходимом toocreate. Например, если требуется toocreate S2S VPN-подключения шлюза и подключение шлюза P2S VPN hello одной виртуальной сети, используется тип VPN *routebased* так, как P2S требуется тип routebased VPN. Необходимо также tooverify, что VPN-устройства поддерживается routebased VPN-подключения. 

После создания шлюза виртуальной сети невозможно изменить тип VPN hello. У вас есть toodelete hello шлюз виртуальной сети и создать новую. Существует два типа VPN:

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Hello PowerShell пример указывает hello `-VpnType` как *routebased*. При создании шлюз, убедитесь, что hello - VpnType подходит для вашей конфигурации.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Требования к шлюзу

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Подсеть шлюза

Прежде чем создать VPN-шлюз, необходимо создать подсеть для него. подсеть шлюза Hello содержит hello IP-адреса шлюза виртуальной сети, hello виртуальные машины и службы используют. При создании шлюз виртуальной сети шлюза виртуальных машин, развернутых toohello подсеть шлюза и настроены параметры шлюза VPN требуется hello. Что-либо еще, (например, дополнительные виртуальные машины) подсеть шлюза toohello никогда не следует развернуть. подсеть шлюза Hello должен называться «GatewaySubnet» toowork должным образом. Именования подсеть шлюза hello «GatewaySubnet» позволяет Azure знать, что это hello подсети toodeploy hello шлюз виртуальной сети виртуальных машин и служб.

При создании hello подсеть шлюза, можно указать содержит hello число IP-адресов, которые hello подсети. Hello IP-адресов в подсети шлюза hello: выделенный toohello шлюза виртуальные машины и службы шлюза. Некоторым конфигурациям требуется больше IP-адресов, чем прочим. Просмотрите инструкции hello hello конфигурации требуется toocreate и убедитесь, что вы хотите toocreate подсети шлюза hello соответствует этим требованиям. Кроме того вы можете toomake подсети шлюза должен содержать достаточно IP-адреса tooaccommodate возможных будущих дополнительных конфигураций. Хотя можно создать подсеть шлюза всего лишь с размером /29, мы советуем создавать подсети с размером /28 или больше (/28, /27, /26 и т. д.). Таким образом, если добавить функциональность в будущем, hello вы не будет иметь tootear шлюз, а затем удалите и создайте hello tooallow подсеть шлюза для дополнительных IP-адресов.

Hello PowerShell диспетчера ресурсов пример с именем GatewaySubnet подсеть шлюза. Вы увидите в нотации CIDR hello указывает /27, позволяющий недостаточно IP-адресов для большинства конфигураций, которые в настоящее время существует.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Локальные сетевые шлюзы

При создании конфигурации шлюза VPN, шлюз локальной сети hello часто представляет ваше расположение в локальной среде. В hello классической модели развертывания шлюз локальной сети hello была ссылка tooas локального узла. 

Присвойте имя шлюза локальной сети hello, hello общедоступный IP-адрес VPN-устройство локальной hello и указывать префиксы адресов hello, расположенных на hello в локальное расположение. Azure просматривает hello префиксов адресов конечного сетевого трафика, обращается к hello конфигурации, который указан для шлюза локальной сети и соответствующим образом направляет пакеты. Можно также указать шлюзы локальной сети для конфигураций типа "виртуальная сеть — виртуальная сеть", использующих подключение к VPN-шлюзу.

Следующий пример PowerShell Hello создает новый шлюз локальной сети:

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Иногда требуется параметры шлюза локальной сети toomodify hello. Например, при добавлении или изменении hello диапазон адресов, а для hello IP-адрес устройства VPN hello изменений. Для классической виртуальной сети можно изменить эти параметры в классический портал hello на странице приветствия локальных сетей. В случае использования Resource Manager ознакомьтесь с разделом [Изменение параметров шлюза локальной сети с помощью PowerShell](vpn-gateway-modify-local-network-gateway.md).

## <a name="resources"></a>Интерфейсы REST API и командлеты PowerShell

Дополнительные технические ресурсы и конкретные требования к синтаксису, при использовании REST API, командлеты PowerShell или Azure CLI для конфигурации VPN-шлюза, см. следующие страницы приветствия:

| **Классический** | **Диспетчер ресурсов** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [ИНТЕРФЕЙС REST API](https://msdn.microsoft.com/library/jj154113) |[REST API](/rest/api/network/virtualnetworkgateways) |
| Не поддерживается | [Интерфейс командной строки Azure](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о доступных конфигурациях подключений см. в статье [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md).