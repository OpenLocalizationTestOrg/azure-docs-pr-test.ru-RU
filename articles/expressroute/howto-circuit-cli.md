---
title: "Создание и изменение канала ExpressRoute Azure с помощью CLI | Документация Майкрософт"
description: "В этой статье описывается toocreate, подготовки, проверьте, обновить, удалить и отзыв канал ExpressRoute с использованием интерфейса CLI."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>Создание и изменение канала ExpressRoute с помощью CLI


В этой статье описывается, как toocreate канал Azure ExpressRoute с помощью hello интерфейс командной строки (CLI). В этой статье также рассказывается, как состояние toocheck hello, обновить, или удалить и Отмена подготовки схемы. Если требуется toouse toowork другой метод с каналами ExpressRoute hello статьи можно выбрать из hello после списка:

> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Интерфейс командной строки Azure](howto-circuit-cli.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>Перед началом работы

* Прежде чем начать, установите последнюю версию hello hello команды CLI (2.0 или более поздней версии). Сведения об установке hello командах CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-azure-cli) и [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).
* Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.

## <a name="create-and-provision-an-expressroute-circuit"></a>Создание и предоставление канала ExpressRoute

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Войдите в tooyour учетная запись Azure и выберите подписку

toobegin конфигурацию входа tooyour учетная запись Azure. Используйте следующие примеры toohelp подключении hello.

```azurecli
az login
```

Проверьте hello подписки для учетной записи hello.

```azurecli
az account list
```

Выберите подписку hello, для которого требуется toocreate канал ExpressRoute.

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Получить список поддерживаемых поставщиков, расположений и полос пропускания hello

Прежде чем создавать канал ExpressRoute, необходимо hello список поставщиков поддерживаемых соединений, расположений и полосы пропускания. Hello CLI команды «az express route списка поставщиков сетевых услуг —» возвращает эту информацию, которая будет использоваться на последующих этапах:

```azurecli
az network express-route list-service-providers
```

Hello ответ — аналогично toohello в следующем примере:

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

Проверьте toosee hello ответа, если указана поставщиком соединения. Запишите hello следующую информацию, который потребуется при создании канала:

* Имя
* PeeringLocations
* BandwidthsOffered

Теперь вы готовы toocreate канал ExpressRoute.

### <a name="3-create-an-expressroute-circuit"></a>3. Создание канала ExpressRoute

> [!IMPORTANT]
> Ваш канал ExpressRoute оплачивается с момента hello выдачи ключа службы. Выполните эту операцию при готовности tooprovision hello цепи hello поставщика услуг подключения.
> 
> 

Перед созданием канала ExpressRoute необходимо создать группу ресурсов (если вы этого еще не сделали) Можно создать группу ресурсов, выполнив следующую команду hello:

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

Привет, в следующем примере показано, как circuit toocreate ExpressRoute 200 Мбит/с до Equinix в Силиконовой долине. Если вы используете другой поставщик и другие параметры, подставьте в запрос соответствующие данные. 

Убедитесь, что указан правильный уровень номера SKU hello и семейство номеров SKU:

* Уровень SKU определяет, какая надстройка включена — ExpressRoute Standard или ExpressRoute Premium. Можно указать «Стандартный» hello tooget стандартном номере SKU или «Premium» hello premium надстройки.
* Семейство номеров SKU определяет hello выставления счетов с типом. Выберите Metereddata для тарифного плана с оплатой за трафик или Unlimiteddata для безлимитного тарифного плана. Можно изменить hello выставления счетов с типом от «Metereddata «too'Unlimiteddata», но не может изменить тип hello из «Unlimiteddata» too'Metereddata».


Ваш канал ExpressRoute оплачивается с момента hello выдачи ключа службы. Следующий пример Hello представляет собой запрос на новый ключ службы:

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

Hello ответ содержит ключ службы hello.

### <a name="4-list-all-expressroute-circuits"></a>4. Получение списка всех каналов ExpressRoute

tooget список все каналы ExpressRoute hello, которые были созданы, выполните команду «Список express route сети az» hello. Вы можете получить эти сведения в любое время с помощью этой команды. toolist все каналы сделать hello вызова без параметров.

```azurecli
az network express-route list
```

Ключ службы, перечисленные в hello *ServiceKey* поле ответа hello.

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

Вы можете получить подробное описание всех параметров hello, с помощью hello команды hello "-h" параметра.

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Отправка ключа tooyour подключения hello службы поставщика для подготовки

«ServiceProviderProvisioningState» предоставляет сведения о текущем состоянии hello подготовки на стороне поставщика услуг hello. Hello состояния содержит состояние hello hello стороны Майкрософт. Дополнительные сведения см. в разделе hello [рабочих процессов в статье](expressroute-workflows.md#expressroute-circuit-provisioning-states).

При создании нового канала ExpressRoute hello схемы имеет hello следующие состояния:

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

изменения схемы Hello toohello при поставщика услуг подключения hello находится в процессе hello включить его для вас следующие состояния:

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

Для вас toobe может toouse канал ExpressRoute он должен быть в hello следующие состояния:

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Периодически Проверьте состояние hello и состояние hello ключа канала hello

Проверка состояния hello и состояние hello hello ключа канала позволяет узнать, когда поставщик подключит ваш канал. После настройки канала hello «ServiceProviderProvisioningState» отображается как «Подготовлена», как показано в следующий пример hello:

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

Hello ответ — аналогично toohello в следующем примере:

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7. Создание конфигурации маршрутизации

Пошаговые инструкции см. в разделе hello [expressroute в конфигурацию маршрутизации](howto-routing-cli.md) статью toocreate и изменения пиринги в цепи.

> [!IMPORTANT]
> Эти инструкции применяются только toocircuits, созданных с помощью службы поставщиков, предлагающих услуги подключений второго уровня. Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), то он возьмет на себя настройку маршрутизации и управление ею.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Связывание виртуальной сети tooan канал ExpressRoute

Затем свяжите виртуальной сети tooyour канал ExpressRoute. Используйте hello [связывание виртуальной сети цепи tooExpressRoute](howto-linkvnet-cli.md) статьи.

## <a name="modify"></a>Изменение канала ExpressRoute

Некоторые свойства канала ExpressRoute можно изменить, не повлияв на подключение. Можно внести следующие изменения без простоев hello.

* Включать и отключать надстройку ExpressRoute "Премиум" для канала ExpressRoute.
* Можно увеличить hello пропускной способностью вашего канала ExpressRoute условии, что емкость доступны через порт hello. Тем не менее понижение уровня полосы пропускания канала hello не поддерживается. 
* Можно изменить план контроля использования программных продуктов hello с измеряемые данных tooUnlimited данных. Однако изменение hello измерения план из данных tooMetered данных не поддерживается.
* Параметр *Allow Classic Operations*(Разрешить классические операции) можно включать и отключать.

Дополнительные сведения об ограничениях и ограничениях см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute премиальное дополнение

Премиальное дополнение hello ExpressRoute можно включить для вашей существующей цепи с помощью hello следующую команду:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

цепь Hello теперь имеет hello ExpressRoute premium дополнительные возможности. Мы начинаем выставления счетов для hello premium дополнительные возможности, как только команда hello успешно запущена.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute премиальное дополнение

> [!IMPORTANT]
> Эта операция может завершиться ошибкой, если вы используете ресурсы, которые больше, чем то, что разрешено для стандартной схемы hello.
> 
> 

Перед отключением hello ExpressRoute премиальное дополнение, понять hello следующие условия:

* Перед понизить из premium toostandard, убедитесь, что имеется менее 10 цепи связанных toohello виртуальных сетей. Если у вас их больше 10, запрос на обновление завершится ошибкой и мы будем выставлять вам счета по тарифам ценовой категории "Премиум".
* Все связи с виртуальными сетями в других геополитических регионах необходимо разорвать. Если вы не отсоедините все ваши виртуальные сети, запрос обновления завершится ошибкой и мы будем выставлять вам счета по тарифам ценовой категории "Премиум".
* Для частного пиринга таблица маршрутов должна содержать менее 4000 маршрутов. Если размер таблицы маршрутов больше 4000 маршрутов, удаляет сеанс BGP hello. Hello сеанс не будет повторно включать до hello число префиксов, объявленных меньше 4 000.

Надстройка premium hello ExpressRoute для существующей цепи hello можно отключить с помощью hello в следующем примере:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>пропускная способность контура tooupdate hello ExpressRoute

Параметры пропускной способности hello поддерживается для поставщика, проверьте hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md). Можно выбрать любой большего размера, чем размер hello вашей существующей цепи.

> [!IMPORTANT]
> Если имеется существующий порт hello недостаточной емкости, имеется канал ExpressRoute toorecreate hello. Обновление схемы hello невозможно, если доступна без дополнительной емкости в этом расположении.
>
> Нельзя уменьшить hello пропускной способности канала ExpressRoute без прерывания. Понижение уровня полосы пропускания требует вы toodeprovision hello канал ExpressRoute и повторной инициализации новый канал ExpressRoute.
>

После принятия решения необходимо использовать ваш канал hello, следующая команда tooresize размер hello:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

Ваш канал подбирается на стороне Майкрософт hello. После этого необходимо обратиться к настройки подключения поставщика tooupdate на своей стороне toomatch это изменение. После внесения этого уведомления, мы начинаем выставления счетов за hello обновить параметр пропускной способности.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>hello toomove SKU из отслеживаемых toounlimited

Hello SKU канал ExpressRoute можно изменить с помощью hello в следующем примере:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>Классический toohello toocontrol доступа и диспетчер ресурсов среды

Ознакомьтесь с инструкциями hello в [каналы ExpressRoute переместить из модели развертывания диспетчера ресурсов hello классический toohello](expressroute-howto-move-arm.md).

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Отзыв и удаление канала ExpressRoute

toodeprovision и удалить канал ExpressRoute убедитесь, что вы понимаете hello следующие условия:

* Необходимо удалить связь всех виртуальных сетей с каналом expressroute hello. Если операция завершается неудачно, убедитесь, что цепь toohello связанные toosee, если все виртуальные сети.
* Если состояние подготовки службы поставщика hello ExpressRoute канала **Provisioning** или **инициализировано**, необходимо работать с ваш канал hello toodeprovision поставщика службы с их стороны. Мы продолжить tooreserve ресурсы и выставлять вам счет на поставщика услуг hello завершения списания цепи hello и уведомляет нас.
* Hello канала можно удалить, если поставщик услуг hello отозваны hello канала. Если канала отозваны, состояние подготовки поставщика услуг hello устанавливается слишком**не инициализировано**. Это приостанавливает выставление счетов для hello схемы.

Ваш канал ExpressRoute можно удалить, выполнив следующую команду hello:

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

После создания ваш канал, убедитесь, что hello следующие задания:

* [Создание и изменение маршрутизации для канала ExpressRoute](howto-routing-cli.md)
* [Связать вашей виртуальной сети tooyour канал ExpressRoute](howto-linkvnet-cli.md)
