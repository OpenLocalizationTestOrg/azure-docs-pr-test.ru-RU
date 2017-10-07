---
title: "aaaCreate экземпляр Наблюдатель сети Azure | Документы Microsoft"
description: "Эта страница предоставляет toocreate действия hello экземпляр Наблюдатель сети с помощью портала hello и Azure REST API"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Создание экземпляра Наблюдателя за сетями Azure

Наблюдатель сети региональные служба, которая позволяет вам toomonitor и диагностики условий уровнем сети сценарий в, чтобы и из Azure. Мониторинг на уровне сценария позволяет toodiagnose проблемы tooend конец сетевого уровня представления. Диагностика сети и средств визуализации, доступных в Наблюдатель сети помогают понять, диагностики и получить аналитики tooyour сети в Azure.

> [!NOTE]
> Наблюдатель сети в настоящее время поддерживает только CLI 1.0, toocreate инструкции hello экземпляра Наблюдатель сети предоставляется CLI 1.0.

## <a name="create-a-network-watcher-in-hello-portal"></a>Создание Наблюдатель сети на портале hello

Перейдите в слишком**более служб** > **сети** > **Наблюдатель сети**. Можно выбрать все подписки hello требуется tooenable Наблюдатель сети для. Это действие создаст экземпляр Наблюдателя за сетями в каждом регионе, который доступен.

![Создание Наблюдателя за сетями][1]

При включении Наблюдатель сети с помощью портала hello hello имя экземпляра hello Наблюдатель сети будет автоматически задан tooNetworkWatcher_region_name где region_name соответствует toohello регион Azure, где hello экземпляр был включен.  Например, наблюдатель за сетями, включенный в западной части центрального региона США, получит имя NetworkWatcher_westcentralus

Кроме того экземпляр hello Наблюдатель сети, автоматически добавляется в группу ресурсов под названием NetworkWatcherRG.  Если эта группа ресурсов не существует, она будет создана.

При желании toocustomize hello имя экземпляра Наблюдатель сети и hello группы ресурсов, он помещается в, можно использовать Powershell, hello API-интерфейса REST или ARMClient описанных ниже методов.  В каждом случае hello группы ресурсов должна существовать до установки hello Наблюдатель сети в него.  

## <a name="create-a-network-watcher-with-powershell"></a>Создание Наблюдателя за сетями с помощью PowerShell

toocreate экземпляр Наблюдатель сети, запустите следующий пример hello:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>Создайте Наблюдатель сети с hello REST API

ARMclient — используется toocall hello REST API с помощью PowerShell. Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).

### <a name="log-in-with-armclient"></a>Вход с помощью ARMClient

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>Создание hello Наблюдатель сети

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда экземпляр Наблюдатель сети, сведения о доступных возможностях hello:

* [Топология](network-watcher-topology-overview.md)
* [Запись пакетов](network-watcher-packet-capture-overview.md)
* [Проверка IP-потока](network-watcher-ip-flow-verify-overview.md)
* [Определение следующего прыжка](network-watcher-next-hop-overview.md)
* [Представление групп безопасности](network-watcher-security-group-view-overview.md)
* [Ведение журнала потоков NSG](network-watcher-nsg-flow-logging-overview.md)
* [Устранение неполадок шлюза виртуальной сети](network-watcher-troubleshoot-overview.md)

После создания экземпляра Наблюдатель сети записи пакета можно задать в следующей статье hello: [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











