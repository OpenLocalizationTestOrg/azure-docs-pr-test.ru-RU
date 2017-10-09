---
title: "Связывание виртуальной сети tooan канал ExpressRoute: CLI: Azure | Документы Microsoft"
description: "Этот документ содержит общие сведения о том, как toolink виртуальных сетей (Vnet) tooExpressRoute каналов с помощью модели развертывания диспетчера ресурсов hello и интерфейс командной строки."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>Подключение с использованием интерфейса CLI канал ExpressRoute tooan виртуальной сети

Эта статья поможет вам ссылку с помощью CLI каналы ExpressRoute tooAzure виртуальных сетей (Vnet). с помощью Azure CLI toolink hello виртуальные сети должны создаваться с помощью модели развертывания диспетчера ресурсов hello. Они могут быть либо в hello одной подписке или входить в другую подписку. Если вы хотите toouse tooconnect другой метод вашей виртуальной сети tooan канал ExpressRoute, можно выбрать статьи из hello после списка:

> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Интерфейс командной строки Azure](howto-linkvnet-cli.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>Предварительные требования для настройки

* Требуется последняя версия hello hello командной строки (CLI). Дополнительные сведения см. в статье [Установка Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
* Требуется tooreview hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.
* Вам потребуется активный канал ExpressRoute. 
  * Следуйте инструкциям hello слишком[создать канал ExpressRoute](howto-circuit-cli.md) и иметь цепи hello, предоставляемой поставщиком соединения. 
  * Убедитесь, что для вашего канала настроен частный пиринг Azure. В разделе hello [Настройка маршрутизации](howto-routing-cli.md) маршрутизации инструкции. 
  * Убедитесь, что настроен частный пиринг Azure. Hello пиринга BGP между вашей сетью и Майкрософт должны работать так, чтобы можно было включить подключение начала до конца.
  * Вам необходимо создать и полностью подготовить виртуальную сеть и шлюз виртуальной сети. Следуйте инструкциям hello слишком[настроить шлюз виртуальной сети для ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli). Быть убедиться, что toouse `--gateway-type ExpressRoute`.

* Объедините too10 виртуальных сетей tooa стандартные каналом expressroute. Все виртуальные сети должны быть в hello геополитические совпадают при использовании стандартных канал ExpressRoute. 

* При включении hello ExpressRoute премиальное дополнение можно связать виртуальную сеть за пределами области геополитические hello объекта hello канал ExpressRoute или подключения большее количество виртуальных сетей tooyour канал ExpressRoute. Дополнительные сведения о премиальное дополнение hello. в разделе hello [часто задаваемые вопросы о](expressroute-faqs.md).

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Подключить виртуальную сеть в Привет одному каналу tooa подписки

Канал ExpressRoute tooan шлюза виртуальной сети можно подключиться, используя пример hello. Убедитесь, что шлюз виртуальной сети, hello создается и готов для связывания перед выполнением команды hello.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Подключить виртуальную сеть в цепи tooa другой подписке

Канал ExpressRoute может совместно использоваться несколькими подписками. на следующем рисунке Hello показана простая схема способ управления доступом подходит для каналов ExpressRoute в нескольких подписках.

Каждый из hello маленькие облака в облако hello является используется toorepresent подписках, которые принадлежат toodifferent отделам в организации. Каждый из отделов hello hello организации можно использовать собственную подписку для развертывания своих служб--, но они могут совместно использовать одной ExpressRoute цепи tooconnect tooyour назад в локальной сети. Одному отделу (в этом примере: ИТ) может быть владельцем hello канал ExpressRoute. Другие подписки в hello организации можно использовать канал ExpressRoute hello.

> [!NOTE]
> Плата за подключение и пропускную способность для hello выделенного канала будет применен toohello владельца канала ExpressRoute. Все виртуальные сети совместно использовать hello же пропускной способности.
> 
> 

![Подключение между подписками](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>Администрирование: владельцы и пользователи канала

Hello «Владелец схемы» зарегистрирован как авторизованный пользователь питания, для hello ресурсов цепь ExpressRoute. Hello владельца канала можно создать авторизацию, может быть активирован с «Канала пользователи». Пользователи канала являются владельцами виртуальной сети hello шлюзов, которые не находятся в одной подписке, как hello канал ExpressRoute. Пользователи канала могут использовать разрешения (по одному разрешению на виртуальную сеть).

Hello владельца канала имеет авторизаций toomodify и revoke power hello в любое время. При отзыве авторизации все связи соединения удаляются из подписки hello, доступ к которым был отозван.

### <a name="circuit-owner-operations"></a>Действия владельца канала

**toocreate авторизации**

Hello владельца канала создает авторизации, который создает ключ авторизации, который может быть используемые tooconnect пользователя канала их toohello шлюзы виртуальной сети канал ExpressRoute. Разрешение действительно только для одного подключения.

Следующий пример показывает как Hello toocreate авторизации:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

Hello ответ содержит ключ авторизации hello и состояние:

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**tooreview авторизации**

Hello владельцем канала, можно просмотреть все разрешения, выданные для конкретного канала, выполнив следующий пример hello.

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**tooadd авторизации**

Hello владельца канала можно добавить параметры авторизации, используя следующий пример hello:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**toodelete авторизации**

Hello владелец канала может revoke и удаление авторизации пользователя toohello, выполнив следующий пример hello:

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>Действия пользователя канала

Hello пользователя канала требуется идентификатор однорангового hello и ключ авторизации из hello владельца канала. ключ авторизации Hello представляет собой идентификатор GUID.

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem авторизации подключения**

Hello пользователя канала можно выполнять следующие tooredeem пример hello авторизации:

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease авторизации подключения**

Авторизации можно освободить путем удаления соединений hello, связывающий hello цепь ExpressRoute toohello виртуальной сети.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).
