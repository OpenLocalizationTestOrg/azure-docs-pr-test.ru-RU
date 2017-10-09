---
title: "aaaAutomatically масштабирования единицы производительности концентраторов событий Azure | Документы Microsoft"
description: "Включить автоматическое увеличению на tooautomatically пространства имен, масштабирования единицы пропускной способности"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Автоматическое масштабирование единиц пропускной способности концентратора событий Azure

## <a name="overview"></a>Обзор

Концентраторы событий Azure представляют собой платформу потоковой передачи платформы с высокой степенью масштабируемости. Таким образом клиенты концентраторов событий часто повысить их использования после адаптации toohello службы. Такого увеличения требуется возрастающее hello, предопределенные видеодрайвером пропускной способности единицы (TUs) tooscale концентраторов событий и обработки больших скоростью передачи. Hello *увеличению автоматически* функции концентраторов событий автоматически масштабируется hello число TUs toomeet потребностями. Увеличение единиц пропускной способности предотвращает сценарии регулирования, в которых:

* скорости входящего трафика данных превышают установленные единицы пропускной способности;
* скорости запросов исходящего трафика данных превышают установленные единицы пропускной способности.

## <a name="how-auto-inflate-works"></a>Как работает автоматическое расширение

Трафик концентраторов событий контролируется с помощью единиц пропускной способности. Одна единица пропускной способности разрешает входящий трафик со скоростью до 1 МБ/с и исходящий трафик со скоростью вдвое выше. В концентраторах событий ценовой категории "Стандартный" можно настроить от 1 до 20 единиц пропускной способности. Увеличению автоматически включает toostart небольших единиц минимальная пропускная способность требуется hello. функция Hello затем автоматически масштабируется toohello максимальное количество единиц производительности, что нужно, в зависимости от hello увеличение трафика. Увеличению автоматически предоставляет hello следующие преимущества:

- Небольшое эффективного toostart масштабирования механизм и вертикального масштабирования, как вы увеличиваться.
- Автоматически масштабируйте указанного верхний предел toohello без проблем регулирования.
- Более широкие возможности управления масштабированием, как вы управляете и о том, сколько tooscale.

## <a name="enable-auto-inflate-on-a-namespace"></a>Включение автоматического расширения в пространстве имен

Можно включить или отключить автоматическое увеличению на пространство имен, используя один из следующих методов hello:

1. Hello [портал Azure](https://portal.azure.com).
2. Шаблон Azure Resource Manager.

### <a name="enable-auto-inflate-through-hello-portal"></a>Включение автоматического увеличению через портал hello

Функцию автоматического увеличению hello в пространстве имен можно включить при создании имен концентраторов событий:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

Если этот параметр включен, можно начать с малого числа единиц пропускной способности и повышать его по мере роста потребностей использования. Hello верхний предел для расширению не влияет на цены, зависящее от hello число TUs, используемый в час.

Можно также включить увеличению автоматически с помощью hello **шкалы** параметр в колонке параметров hello hello портала:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Включение автоматического расширения с помощью шаблона Azure Resource Manager

Вы можете включить автоматическое расширение во время развертывания шаблона Azure Resource Manager. Например, набор hello `isAutoInflateEnabled` свойство слишком**true** и задайте `maximumThroughputUnits` too10.

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

Полный шаблон hello, в разделе hello [пространства имен для создания концентраторов событий и включение увеличению](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) шаблона на GitHub.

## <a name="next-steps"></a>Дальнейшие действия

На сайте ссылкам hello, изучите более подробную концентраторов событий:

* [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md)
* [Создание концентратора событий](event-hubs-create.md)
