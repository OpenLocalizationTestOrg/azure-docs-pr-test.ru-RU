---
title: "Связывание виртуальной сети tooan канал ExpressRoute: PowerShell: Azure | Документы Microsoft"
description: "Этот документ содержит общие сведения о том, как toolink виртуальных сетей (Vnet) tooExpressRoute каналов с помощью модели развертывания диспетчера ресурсов hello и PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Подключение виртуальной сети tooan канал ExpressRoute
> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Интерфейс командной строки Azure](howto-linkvnet-cli.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-linkvnet-classic.md)
>

Эта статья поможет вам связать каналы ExpressRoute tooAzure виртуальных сетей (Vnet) с помощью модели развертывания диспетчера ресурсов hello и PowerShell. Виртуальные сети может быть либо в hello же часть другую подписку или подписку. В этой статье также показано, как связать tooupdate виртуальной сети. 

## <a name="before-you-begin"></a>Перед началом работы
* Установите последнюю версию hello hello модули Azure PowerShell. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
* Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.
* Вам потребуется активный канал ExpressRoute. 
  * Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и иметь цепи hello, предоставляемой поставщиком соединения. 
  * Убедитесь, что для вашего канала настроен частный пиринг Azure. В разделе hello [Настройка маршрутизации](expressroute-howto-routing-arm.md) маршрутизации инструкции. 
  * Убедитесь, что настроен открытого пиринга Azure и hello пиринга BGP между вашей сетью и Майкрософт работает так, чтобы можно было включить подключение начала до конца.
  * Вам необходимо создать и полностью подготовить виртуальную сеть и шлюз виртуальной сети. Следуйте инструкциям hello слишком[создать шлюз виртуальной сети для ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Шлюз виртуальной сети для ExpressRoute использует hello «ExpressRoute», тип шлюза не VPN.

* Объедините too10 виртуальных сетей tooa стандартные каналом expressroute. Все виртуальные сети должны быть в hello геополитические совпадают при использовании стандартных канал ExpressRoute. 

* Можно связать виртуальных сетей за пределами области геополитические hello объекта hello канал ExpressRoute или подключения большее количество виртуальных сетей tooyour канал ExpressRoute, если вы включили hello ExpressRoute премиальное дополнение. Проверьте hello [часто задаваемые вопросы о](expressroute-faqs.md) Дополнительные сведения о премиальное дополнение hello.


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Подключить виртуальную сеть в Привет одному каналу tooa подписки
Tooan шлюза виртуальной сети канал ExpressRoute можно подключиться с помощью hello, выполнив командлет. Убедитесь, что шлюз виртуальной сети, hello создается и готов для связывания перед запуском командлета hello:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Подключить виртуальную сеть в цепи tooa другой подписке
Канал ExpressRoute может совместно использоваться несколькими подписками. Следующий рисунок Hello показана простая схема способ управления доступом подходит для каналов ExpressRoute в нескольких подписках.

Каждый из hello маленькие облака в облако hello является используется toorepresent подписках, которые принадлежат toodifferent отделам в организации. Каждый из отделов hello hello организации можно использовать собственную подписку для развертывания своих служб--, но они могут совместно использовать одной ExpressRoute цепи tooconnect tooyour назад в локальной сети. Одному отделу (в этом примере: ИТ) может быть владельцем hello канал ExpressRoute. Другие подписки в hello организации можно использовать канал ExpressRoute hello.

> [!NOTE]
> Плата за подключение и пропускную способность для hello канал ExpressRoute будет применен toohello владельца подписки. Все виртуальные сети совместно использовать hello же пропускной способности.
> 
> 

![Подключение между подписками](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>Администрирование: владельцы канала и его пользователи

Hello «владелец схемы» зарегистрирован как авторизованный пользователь питания, для hello ресурсов цепь ExpressRoute. Владелец канала Hello можно создать авторизацию, может быть активирован с «канала пользователи». Пользователи канала являются владельцами виртуальной сети hello шлюзов, которые не находятся в одной подписке, как hello канал ExpressRoute. Пользователи канала могут активировать разрешения (по одному разрешению для каждой виртуальной сети).

Владелец канала Hello имеет авторизаций toomodify и revoke power hello в любое время. Отмена авторизации приведет все подключения ссылку, удаляемый из подписки hello, доступ к которым был отозван.

### <a name="circuit-owner-operations"></a>Действия владельца канала

**toocreate авторизации**

Владелец канала Hello создает авторизации. Это приведет к создание hello ключ авторизации, которое может быть используемые схемы пользователя tooconnect их toohello шлюзы виртуальной сети канал ExpressRoute. Разрешение действительно только для одного подключения.

Hello в следующем фрагменте кода показан командлет как toocreate авторизации:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


Hello toothis ответ будет содержать ключ авторизации hello и состояние:

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**tooreview авторизации**

Владелец канала Hello, можно просмотреть все разрешения, выданные для конкретного канала, выполнив следующий командлет hello.

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**tooadd авторизации**

Владелец канала Hello можно добавить параметры авторизации с помощью hello, выполнив командлет:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**toodelete авторизации**

Владелец канала Hello можно revoke и удаление авторизации пользователя toohello, выполнив следующий командлет hello:

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>Действия пользователя канала

пользователь канала Hello должен идентификатор однорангового hello и ключ авторизации от владельца канала hello. ключ авторизации Hello представляет собой идентификатор GUID.

Идентификатор однорангового узла можно проверить из hello следующую команду:

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem авторизации подключения**

пользователя канала Hello можно выполнить следующий командлет tooredeem hello авторизации:

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease авторизации подключения**

Авторизации можно освободить путем удаления соединений hello, связывающий hello цепь ExpressRoute toohello виртуальной сети.

## <a name="modify-a-virtual-network-connection"></a>Изменение подключения к виртуальной сети
Вы можете изменить определенные свойства подключения к виртуальной сети. 

**Вес подключения tooupdate hello**

Виртуальная сеть может быть подключенных toomultiple каналы ExpressRoute. Может появиться hello одинаковые префиксы из более чем один канал ExpressRoute. toochoose, какой трафик toosend подключения, предназначенные для этого префикса, вы можете изменить *недопустимо* соединения. Трафик будет отправляться по соединению, hello с наивысшим hello *недопустимо*.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

Здравствуйте, диапазон *недопустимо* — 0 too32000. значение по умолчанию Hello — 0.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).
