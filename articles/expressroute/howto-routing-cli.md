---
title: "Как tooconfigure маршрутизации для канала Azure ExpressRoute: CLI | Документы Microsoft"
description: "Эта статья поможет вам создавать и подготавливать hello private, public и Microsoft пиринг канал ExpressRoute. В этой статье также рассказывается, как состояние toocheck hello, обновления или удаления пиринги для своего канала."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>Создание и изменение маршрутизации для канала ExpressRoute с помощью CLI

Эта статья поможет вам создавать и управлять ими конфигурации маршрутизации для канала ExpressRoute в модели развертывания диспетчера ресурсов hello, используя интерфейс командной строки. Можно также проверить состояние hello, update или delete и отзыв пиринги за канал ExpressRoute. Если вы хотите toouse toowork другой метод с ваш канал, выберите статью из hello после списка:

> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Интерфейс командной строки Azure](howto-routing-cli.md)
> * [Видео — частный пиринг](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Видео — общедоступный пиринг](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Видео — пиринг Майкрософт](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Предварительные требования для настройки

* Прежде чем начать, установите последнюю версию hello hello команды CLI (2.0 или более поздней версии). Сведения об установке hello командах CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-azure-cli).
* Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочего процесса](expressroute-workflows.md) страниц перед началом настройки.
* Вам потребуется активный канал ExpressRoute. Следуйте инструкциям hello слишком[создать канал ExpressRoute](howto-circuit-cli.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить. Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен для вас команды hello может toorun toobe в этой статье.

Эти инструкции применяются только toocircuits, созданных с помощью предложения службы связи уровня 2 поставщиков услуг. Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), то он возьмет на себя настройку маршрутизации и управление ею.

Для каждого канала ExpressRoute можно настроить один, два или все три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft). Пиринги можно настраивать в любом порядке, Тем не менее необходимо выполнить настройку hello из каждого из них пиринга одновременно.

## <a name="azure-private-peering"></a>Частный пиринг Azure

Этот раздел поможет вам создать, получить, обновление и удаление hello Azure закрытая конфигурация пиринга канал ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate открытого пиринга Azure

1. Установите последнюю версию hello Azure CLI. Необходимо использовать последнюю версию hello hello Azure интерфейс командной строки (CLI). * hello проверки [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.

  ```azurecli
  az login
  ```

  Выберите подписку hello требуется канал ExpressRoute toocreate

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Создайте канал ExpressRoute. Следуйте инструкциям toocreate hello [канал ExpressRoute](howto-circuit-cli.md) и их подготовки с помощью поставщика услуг подключения hello.

  Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас. В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello. Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.
3. Убедитесь, что подготовлены, а также включить toomake цепь ExpressRoute hello. Используйте следующий пример hello.

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Настройка открытого пиринга Azure для hello схемы. Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:

  * / 30 подсеть для основной ссылки hello. подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.
  * / 30 подсеть для дополнительной ссылки hello. подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.
  * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
  * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS. Для этого пиринга можно использовать частный номер AS. Не используйте номер 65515.
  * **Необязательно —** хэш MD5 при выборе toouse один.

  Используйте следующий пример tooconfigure Azure закрытого пиринга для своего канала hello.

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  При выборе toouse хэш MD5, используйте следующий пример hello:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure закрытого пиринга подробные сведения

Сведения о конфигурации можно получить с помощью hello в следующем примере:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

Hello вывода будет примерно toohello следующий пример:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate конфигурации закрытого пиринга Azure

Вы можете обновить любая часть конфигурации hello, используя следующий пример hello. В этом примере выполняется обновление hello VLAN ID канала hello из 100 too500.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>toodelete открытого пиринга Azure

Пиринг конфигурации можно удалить, выполнив следующий пример hello.

> [!WARNING]
> Необходимо убедиться, что все виртуальные сети будут отключены от hello канал ExpressRoute перед запуском этого примера. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Общедоступный пиринг Azure

Этот раздел поможет вам создать, получить, обновление и удаление hello Azure открытая конфигурация пиринга канал ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate частного пиринга Azure

1. Установите последнюю версию hello Azure CLI. Необходимо использовать последнюю версию hello hello Azure интерфейс командной строки (CLI). * hello проверки [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.

  ```azurecli
  az login
  ```

  Выберите подписку hello, для которого требуется toocreate канал ExpressRoute.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Создайте канал ExpressRoute.  Следуйте инструкциям toocreate hello [канал ExpressRoute](howto-circuit-cli.md) и их подготовки с помощью поставщика услуг подключения hello.

  Если ваш поставщик услуг подключения оказывает услуги третьего уровня, попросите его включить для вас частный пиринг Azure. В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello. Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.
3. Проверьте hello tooensure цепь ExpressRoute подготовленный и также включена. Используйте следующий пример hello.

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Настройка открытого пиринга Azure для hello схемы. Убедитесь, что следующие сведения, прежде чем продолжить дальнейшей hello.

  * / 30 подсеть для основной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4.
  * / 30 подсеть для дополнительной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4.
  * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
  * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS.
  * **Необязательно —** хэш MD5 при выборе toouse один.

  Выполните следующий пример tooconfigure Azure открытый пиринг для своего канала hello.

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  При выборе toouse хэш MD5, используйте следующий пример hello:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Номер AS должен быть указан в качестве ASN пиринга, а не ASN клиента.

### <a name="tooview-azure-public-peering-details"></a>tooview открытый пиринг сведения о Azure

Можно получить сведения о конфигурации, используя следующий пример hello:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

Hello вывода будет примерно toohello следующий пример:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate конфигурации открытого пиринга Azure

Вы можете обновить любая часть конфигурации hello, используя следующий пример hello. В этом примере выполняется обновление hello VLAN ID канала hello из 200 too600.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>toodelete частного пиринга Azure

Пиринг конфигурации можно удалить, выполнив следующий пример hello.

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Пиринг Майкрософт

Этот раздел поможет вам создать, получить, обновление и удаление пиринга конфигурации Microsoft hello за канал ExpressRoute.

> [!IMPORTANT]
> Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт hello, даже если не определены фильтры маршрутов. Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала. Дополнительные сведения см. в руководстве по [настройке фильтра маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate пиринг Майкрософт

1. Установите последнюю версию hello Azure CLI. Используйте hello последнюю версию hello Azure интерфейс командной строки (CLI). * hello проверки [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.

  ```azurecli
  az login
  ```

  Выберите подписку hello, для которого требуется toocreate канал ExpressRoute.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Создайте канал ExpressRoute. Следуйте инструкциям toocreate hello [канал ExpressRoute](howto-circuit-cli.md) и их подготовки с помощью поставщика услуг подключения hello.

  Если поставщиком соединения предлагает управляемых служб уровня 3, вы можете запросить tooenable поставщика вашего подключения к Azure закрытого пиринга для вас. В этом случае нет необходимости toofollow указаниям, приведенным в следующих разделах hello. Однако если поставщиком соединения не поддерживает управление маршрутизации, после создания ваш канал, по-прежнему конфигурацию с помощью hello дальнейшие действия.

3. Убедитесь, что подготовлены, а также включить toomake цепь ExpressRoute hello. Используйте следующий пример hello.

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Настройка Microsoft пиринг для цепи hello. Убедитесь, что hello следующую информацию, прежде чем продолжить.

  * / 30 подсеть для основной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.
  * / 30 подсеть для дополнительной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.
  * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
  * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS.
  * Объявленные префиксы: необходимо предоставить список всех префиксов планирование tooadvertise сеансом BGP hello. Допускаются только общедоступные префиксы IP-адресов. Если планируется toosend набор префиксов, вы можете отправить список с разделителями запятыми. Эти префиксы должны быть tooyou, зарегистрированные в RIR / IRR.
  * **Необязательно —** клиента ASN: если префиксы рекламы, не зарегистрированный toohello пиринг как число, можно указать hello в качестве номера toowhich они зарегистрированы.
  * Имя реестра маршрутизации: Можно указать hello RIR / IRR, для какой hello, а число и префиксы зарегистрирована.
  * **Необязательно —** хэш MD5 при выборе toouse один.

   Выполните следующие пиринг Майкрософт пример tooconfigure для своего канала hello.

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>данные пиринга tooget Microsoft

Сведения о конфигурации можно получить с помощью hello в следующем примере:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

Hello вывода будет примерно toohello следующий пример:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>Конфигурация пиринга Майкрософт tooupdate

Вы можете обновить любая часть конфигурации hello. Hello объявленные префиксы канала hello обновляются с too124.1.0.0/24 123.1.0.0/24 в hello в следующем примере:

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>toodelete пиринг Майкрософт

Пиринг конфигурации можно удалить, выполнив следующий пример hello.

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>Дальнейшие действия

Следующий шаг [связывание виртуальной сети tooan канал ExpressRoute](howto-linkvnet-cli.md).

* Дополнительную информацию о рабочих процессах ExpressRoute см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).
* Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).
* Подробнее о работе с виртуальными сетями см. в статье [Обзор виртуальных сетей](../virtual-network/virtual-networks-overview.md).