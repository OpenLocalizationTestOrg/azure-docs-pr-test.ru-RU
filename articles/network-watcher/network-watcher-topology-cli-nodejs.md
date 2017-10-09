---
title: "Топология Наблюдатель сети Azure aaaView - Azure CLI 1.0 | Документы Microsoft"
description: "В этой статье описывается как tooquery toouse Azure CLI 1.0 топологии сети."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 30679d6dc74e85bacfc86c63bd1afa873893c772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a>Просмотр топологии Наблюдателя за сетями с помощью Azure CLI 1.0

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

компонент топологии Hello Наблюдатель сети предоставляет визуальное представление hello сетевым ресурсам в подписке. На портале hello этой визуализации представлены tooyou автоматически. Hello информации за представление топологии hello hello портала можно извлечь с помощью PowerShell.
Эта возможность обеспечивает сведения о топологии hello более универсально, как hello данных могут использоваться другие средства toobuild out hello визуализации.

В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux. 

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

В этом сценарии используется hello `network watcher topology` сведения о топологии hello tooretrieve командлета. Имеется также статью о том, как слишком[получить топология сети с помощью REST API](network-watcher-topology-rest.md).

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.

## <a name="scenario"></a>Сценарий

Hello сценарий, описанный в этой статье получает ответ hello топологии для данной группы ресурсов.

## <a name="retrieve-topology"></a>Получение топологии

Hello `network watcher topology` командлет извлекает hello топологии для данной группы ресурсов. Добавьте аргумент hello «--json» tooview oput hello в формате json

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a>Результаты

Hello возвращаемые результаты имеют свойство имени «ресурсы», содержащих hello текста ответа json для hello `network watcher topology` командлета.  Hello ответ содержит ресурсы hello hello сетевой группы безопасности и их связи (то есть Contains, связано).

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о правилах безопасности hello, которые будут применяться tooyour сетевым ресурсам, посетив [Общие сведения о представлении группы безопасности](network-watcher-security-group-view-overview.md)
