---
title: "Топология Наблюдатель сети Azure aaaView - PowerShell | Документы Microsoft"
description: "В этой статье описывается как toouse PowerShell tooquery топологии сети."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a>Просмотр топологии Наблюдателя за сетями с помощью PowerShell

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

В этом сценарии используется hello `Get-AzureRmNetworkWatcherTopology` сведения о топологии hello tooretrieve командлета. Имеется также статью о том, как слишком[получить топология сети с помощью REST API](network-watcher-topology-rest.md).

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.

## <a name="scenario"></a>Сценарий

Hello сценарий, описанный в этой статье получает ответ hello топологии для данной группы ресурсов.

## <a name="retrieve-network-watcher"></a>Извлечение Наблюдателя за сетями

Первым шагом Hello — экземпляр Наблюдатель сети tooretrieve hello. Hello `$networkWatcher` переменной передается toohello `Get-AzureRmNetworkWatcherTopology` командлета.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a>Получение топологии

Hello `Get-AzureRmNetworkWatcherTopology` командлет извлекает hello топологии для данной группы ресурсов.

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a>Результаты

Hello возвращаемые результаты имеют свойство имени «ресурсы», содержащих hello текста ответа json для hello `Get-AzureRmNetworkWatcherTopology` командлета.  Hello ответ содержит ресурсы hello hello сетевой группы безопасности и их связи (то есть Contains, связано).

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом toovisualize вашего потока NSG ведет журнал с помощью Power BI, посетив [визуализировать NSG потоки журналов с помощью Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


