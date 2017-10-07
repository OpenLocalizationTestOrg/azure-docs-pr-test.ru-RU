---
title: "Топология Наблюдатель сети Azure aaaView - интерфейса API REST | Документы Microsoft"
description: "В этой статье описывается, как toouse REST API tooquery топологии сети."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a>Просмотр топологии Наблюдателя за сетями с помощью REST API

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

компонент топологии Hello Наблюдатель сети предоставляет визуальное представление hello сетевым ресурсам в подписке. На портале hello этой визуализации представлены tooyou автоматически. Hello информации за представление топологии hello hello портала можно извлечь с помощью PowerShell.
Эта возможность обеспечивает сведения о топологии hello более универсально, как hello данных могут использоваться другие средства toobuild out hello визуализации.

взаимодействие Hello моделируется в две связи.

- **Вложение.** Например, виртуальная сеть содержит подсеть, которая, в свою очередь, содержит сетевую карту.
- **Связь.** Например, сетевая карта связана с виртуальной машиной.

Hello ниже представлена свойства, которые возвращаются при запросе hello топологии REST API.

* **имя** - hello имя ресурса hello
* **Идентификатор** -hello uri ресурса hello.
* **расположение** -hello расположение, где существует ресурс hello.
* **ассоциации** -список сопоставлений toohello ссылка на объект.
    * **имя** -hello объекта hello ссылка на имя ресурса.
    * **resourceId** -hello resourceId является uri hello hello ресурса, на который ссылается связь hello.
    * **Тип associationType** -это значение ссылается на связь hello hello объекта дочернего и родительского hello. Допустимые значения: **Contains** или **Associated**.

## <a name="before-you-begin"></a>Перед началом работы

В этом случае можно получить сведения о топологии hello. ARMclient — используется toocall hello REST API с помощью PowerShell. Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.

## <a name="scenario"></a>Сценарий

Hello сценарий, описанный в этой статье получает ответ hello топологии для данной группы ресурсов.

## <a name="log-in-with-armclient"></a>Вход с помощью ARMClient

Войдите в tooarmclient с учетными данными Azure.

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a>Получение топологии

Следующий пример Hello запрашивает топологии hello hello REST API.  пример Hello является параметризованный tooallow для гибкость при создании примера.  Замените значения в угловых скобках (\< \>).

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

Hello после ответа является примером сокращенный ответ, который возвращается, если получить топологию группа ресурсов:

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

