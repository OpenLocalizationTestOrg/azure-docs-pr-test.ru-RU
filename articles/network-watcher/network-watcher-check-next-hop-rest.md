---
title: "aaaFind следующего прыжка с Azure сети наблюдателя следующего прыжка - REST | Документы Microsoft"
description: "В этой статье описывается, как можно найти какие hello тип следующего прыжка — и IP-адрес, с помощью следующего прыжка hello Azure REST API"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>Узнать, какой тип следующего прыжка hello является использование возможностей следующего прыжка hello в Aure Наблюдатель сети, с помощью Azure REST API

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

Следующий прыжок является компонентом Наблюдатель сети, который предоставляет возможность hello получить тип следующего прыжка hello и IP-адрес, на основе указанной виртуальной машины. Эта возможность полезна в определении передачи трафика, оставляя виртуальной машины шлюза, Интернет или назначения tooits tooget виртуальных сетей.

## <a name="before-you-begin"></a>Перед началом работы

ARMclient — используется toocall hello REST API с помощью PowerShell. Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.

## <a name="scenario"></a>Сценарий

Hello сценарии, описанные в данной статье используется следующего прыжка, функция Наблюдатель сети, извлекают тип следующего прыжка hello и IP-адрес для ресурса. Посетите toolearn Дополнительные сведения о следующего прыжка [следующего прыжка Обзор](network-watcher-next-hop-overview.md).

Вам предстоит:

* Получить hello следующего прыжка для виртуальной машины.

## <a name="log-in-with-armclient"></a>Вход с помощью ARMClient

Войдите в tooarmclient с учетными данными Azure.

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Получение виртуальной машины

Запустите следующий сценарий tooreturn hello виртуальной машины. Эти данные потребуются при выполнении следующего прыжка.

После кода Hello необходимые значения для hello следующие переменные:

- **subscriptionId** -hello toouse идентификатор подписки.
- **resourceGroupName** — hello имя группы ресурсов, содержащем виртуальные машины.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Из hello следующие выходные данные, идентификатор hello hello виртуальной машины используется в hello в следующем примере:

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>Получение следующего прыжка

После создания заголовка авторизации hello hello следующего прыжка из виртуальной машины могут быть получены. Hello следующие значения должно быть заменено toowork примере кода hello.

> [!Important]
> Для API-интерфейса REST Наблюдатель сети вызовы hello имя группы ресурсов в запросе hello, что URI является hello группы ресурсов, содержащий hello Наблюдатель сети не hello ресурсы при выполнении hello диагностических действий на.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> Следующий прыжок требуется что toorun распределения ресурсов виртуальной Машины hello.

## <a name="results"></a>Результаты

Hello ниже приведен пример выходных данных hello получено. Hello результаты содержат hello следующие значения:

* **nextHopType** -это значение является одним из hello следующие значения: Интернет, VirtualAppliance, задана как VirtualNetworkGateway, VnetLocal, HyperNetGateway или нет.
* **nextHopIpAddress** -hello IP-адрес следующего прыжка hello.
* **routeTableId** - hello значение — uri для таблицы маршрутов hello, связанные с маршрутом hello, или если нет пользовательских маршрута определенных hello значение *маршрут системы* возвращается.

Здесь представлены Hello hello результаты в формате json.

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>Дальнейшие действия

После может toofind out hello следующего прыжка для виртуальной машины, можно просмотреть hello безопасность сетевых ресурсов, посетив [Обзор представления безопасности](network-watcher-security-group-view-overview.md)














