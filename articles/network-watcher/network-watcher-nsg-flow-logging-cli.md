---
title: "Управление журналами потоков для групп безопасности сети с помощью Наблюдателя за сетями (Azure CLI) | Документация Майкрософт"
description: "На этой странице объясняется, как управлять журналами потоков для групп безопасности сети с помощью Наблюдателя за сетями в Azure CLI"
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 51683e937b7985bb61671645f3e2e1be6d786201
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a>Настройка журналов потоков для групп безопасности сети с помощью Azure CLI

> [!div class="op_single_selector"]
> - [портал Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Журналы потоков для групп безопасности сети — это компонент Наблюдателя за сетями, который позволяет просматривать сведения о входящем и исходящем IP-трафике через группу безопасности сети. Эти журналы потоков записываются в формате JSON. В них отображаются входящие и исходящие потоки по каждому правилу, сетевая карта, с которой связан поток, сведения о 5 кортежах потока (IP-адрес источника и места назначения, порт источника и места назначения, протокол), а также сведения о состоянии трафика (разрешен или запрещен).

В этой статье мы используем наш новейший интерфейс командной строки для модели развертывания ресурсов и управления ими, а именно Azure CLI 2.0. Этот интерфейс доступен для Windows, Mac и Linux.

Для выполнения действий, описанных в этой статье, требуется [установить интерфейс командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="register-insights-provider"></a>Регистрация поставщика Microsoft Insights

Для успешного ведения журналов потоков должен быть зарегистрирован поставщик **Microsoft.Insights**. Если вы не знаете, зарегистрирован ли поставщик **Microsoft.Insights**, выполните следующий сценарий.

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Включение журналов потоков для группы безопасности сети

Команда для включения журналов потоков показана в следующем примере.

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a>Отключение журналов потоков для группы безопасности сети

Чтобы отключить журналы потоков, используйте следующий пример:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a>Скачивание журнала потоков

Место хранения журнала потоков определяется при его создании. Удобное средство для доступа к этим журналам потоков, сохраненным в учетной записи хранения — обозреватель службы хранилища Microsoft Azure, который можно скачать по адресу http://storageexplorer.com/.

При указании учетной записи хранения файлы записи пакетов сохраняются в ней по следующему адресу:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId=/SUBSCRIPTIONS/{subscriptionID}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/{nsgName}/y={year}/m={month}/d={day}/h={hour}/m=00/macAddress={macAddress}/PT1H.json
```

Сведения о структуре журнала см. в статье [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md) (Обзор журнала потоков для группы безопасности сети).

## <a name="next-steps"></a>Следующие шаги

Узнайте, как [визуализировать сведения журналов потоков группы безопасности сети с помощью PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).

Узнайте, как [визуализировать сведения журналов потоков группы безопасности сети с помощью средств с открытым кодом](network-watcher-visualize-nsg-flow-logs-open-source-tools.md).
