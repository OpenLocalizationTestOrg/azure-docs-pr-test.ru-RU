---
title: "Устранение неполадок шлюза виртуальной сети и подключений Azure (PowerShell) | Документация Майкрософт"
description: "На этой странице объясняется, как устранить неполадки с помощью Наблюдателя за сетями Azure и командлетов PowerShell."
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: jdial
ms.openlocfilehash: d7ae5599b3fa1876e2b5af79f56548cd17c1c8ed
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Устранение неполадок шлюза виртуальной сети и подключений с помощью Наблюдателя за сетями Azure и PowerShell

> [!div class="op_single_selector"]
> - [Портал](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

Наблюдатель за сетями предоставляет множество возможностей, так как он позволяет проанализировать сетевые ресурсы в Azure. Одна из этих возможностей — устранение неполадок в ресурсах. Процедуру устранения неполадок с ресурсами можно вызывать с помощью портала, PowerShell, интерфейса командной строки или API-интерфейса REST. При вызове Наблюдатель за сетями проверяет работоспособность шлюза виртуальной сети или подключения и возвращает результаты.

## <a name="before-you-begin"></a>Перед началом работы

В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create a Network Watcher](network-watcher-create.md) (Создание Наблюдателя за сетями).

Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Обзор

В ходе устранения неполадок с ресурсами вы можете устранить проблемы, возникающие со шлюзами виртуальной сети и подключениями. При запросе на устранение неполадок с ресурсами запрашиваются и проверяются журналы. По завершении проверки возвращаются результаты. Запросы на устранение неполадок с ресурсами выполняются долго, поэтому для возвращения результатов может потребоваться несколько минут. Журналы, используемые при устранении неполадок, хранятся в контейнере указанной учетной записи хранения.

## <a name="retrieve-network-watcher"></a>Извлечение Наблюдателя за сетями

Сначала необходимо получить экземпляр Наблюдателя за сетями. Переменная `$networkWatcher` передается в командлет `Start-AzureRmNetworkWatcherResourceTroubleshooting` на шаге 4.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Получение сведений о подключении к шлюзу виртуальной сети

В этом примере выполняется устранение неполадок с таким ресурсом, как подключение. Его также можно передать шлюзу виртуальной сети.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a>Создайте учетную запись хранения.

При устранении неполадок с ресурсами возвращаются данные о работоспособности ресурса, а также сохраняются журналы в учетную запись хранения для анализа. На этом этапе мы создадим учетную запись хранения. При необходимости можно использовать имеющуюся учетную запись хранения.

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a>Выполнение устранения неполадок с ресурсами Наблюдателя за сетями

Для устранения неполадок с ресурсами используется командлет `Start-AzureRmNetworkWatcherResourceTroubleshooting`. В командлет нужно передать объект Наблюдателя за сетями, идентификатор подключения или шлюза виртуальной сети, идентификатор учетной записи хранения и путь, по которому будут храниться результаты.

> [!NOTE]
> Командлет `Start-AzureRmNetworkWatcherResourceTroubleshooting` выполняется длительное время. Это может занять несколько минут.

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

После выполнения командлета Наблюдатель за сетями просматривает ресурсы, чтобы проверить их работоспособность. Он возвращает результаты в оболочку и сохраняет журналы результатов в указанной учетной записи хранения.

## <a name="understanding-the-results"></a>Анализ результатов

Текст действий содержит общие рекомендации по устранению проблемы. Если для устранения проблемы можно что-то сделать, предоставляется ссылка на дополнительные инструкции. Если дополнительных рекомендаций нет, в ответе указывается URL-адрес, открыв который можно отправить запрос в службу поддержки.  Дополнительные сведения о свойствах ответа, а также о данных, которые он содержит, см. в статье [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md) (Обзор устранения неполадок наблюдателя за сетями).

Инструкции по скачиванию файлов из учетных записей хранения Azure см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Кроме того, можно использовать такое средство, как Storage Explorer. Дополнительные сведения об обозревателе хранилищ см. на [этой странице](http://storageexplorer.com/).

## <a name="next-steps"></a>Дальнейшие действия

Если изменены параметры, которые мешают VPN-подключению, см. статью [Управление группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md), чтобы найти сведения о группах безопасности сети и соответствующие правила безопасности.
