---
title: "Заносит в журнал aaaManage потока группы безопасности сети с Наблюдатель сети Azure — PowerShell | Документы Microsoft"
description: "На этой странице объясняется, каким образом ведет журнал toomanage потока группы безопасности сети в Наблюдатель сети Azure с помощью PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 987e8728fb6459fd6ff8eb5cd3d36ff855f2ccfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a>Настройка журналов потоков для групп безопасности сети с помощью PowerShell

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Сетевая группа безопасности потока журналы являются возможностью Наблюдатель сети, который позволяет вам tooview сведения о входящего и исходящего IP-трафика через группу безопасности сети. Эти потока журналы записываются в формате json и Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5-фрагментному сведения о потоке hello (источник и назначение IP-адрес, порт источника или целевой Protocol) и если hello был разрешен трафик или запрещено.

## <a name="register-insights-provider"></a>Регистрация поставщика Microsoft Insights

В порядке для потока toowork ведения журнала успешно, hello **помощью Microsoft.Insights** должен быть зарегистрирован поставщик. Если вы не уверены в том случае, если hello **помощью Microsoft.Insights** поставщик является зарегистрированным, запустите hello следующий скрипт.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Включение журналов потоков для группы безопасности сети

Следующий пример hello показано Hello команда tooenable потока журналов:

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a>Отключение журналов потоков для группы безопасности сети

Hello используйте следующий пример toodisable потока журналов:

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a>Скачивание журнала потоков

место хранения Hello потока журнала определяется при его создании. Удобное средство tooaccess, эти учетной записи хранения потока сохраняться журналы tooa: Обозреватель хранилищ Microsoft Azure, которую можно загрузить здесь: http://storageexplorer.com/

При указании учетной записи хранилища пакетов отслеживания файлы сохраняются tooa учетной записи хранилища в hello следующие расположения:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Сведения о структуре hello hello журнала [потока группы безопасности сети журнала Обзор](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом слишком[визуализировать журналов потока NSG с PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Узнайте, каким образом слишком[визуализировать NSG потока журналов с помощью средств с открытым исходным кодом](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
