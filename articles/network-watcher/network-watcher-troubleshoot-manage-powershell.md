---
title: "aaaTroubleshoot шлюз виртуальной сети Azure и соединения — PowerShell | Документы Microsoft"
description: "На этой странице объясняется, как toouse hello Наблюдатель сети Azure устранения командлет PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Устранение неполадок шлюза виртуальной сети и подключений с помощью Наблюдателя за сетями Azure и PowerShell

> [!div class="op_single_selector"]
> - [Портал](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

Наблюдатель сети предоставляет множество возможностей, по отношению к сетевым ресурсам в Azure toounderstanding. Одна из этих возможностей — устранение неполадок в ресурсах. Устранение неполадок ресурсов можно вызвать через портал hello, PowerShell, CLI или REST API. При вызове Наблюдатель сети проверяет работоспособность hello шлюза виртуальной сети или подключения и возвращает результаты.

## <a name="before-you-begin"></a>Перед началом работы

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.

Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Обзор

Устранение неполадок ресурсов предоставляет возможность hello Устранение неполадок, возникающих с подключениями и шлюзах виртуальной сети. При запросе tooresource Устранение неполадок, журналы, запросы и проверен. После завершения проверки hello результатов. Запрашивает ресурс, который долго выполняющиеся запросы по устранению неполадок, которой может занять несколько минут tooreturn результат. Устранение неполадок журналы Hello хранятся в контейнер в учетной записи хранилища, который указан.

## <a name="retrieve-network-watcher"></a>Извлечение Наблюдателя за сетями

Первым шагом Hello — экземпляр Наблюдатель сети tooretrieve hello. Hello `$networkWatcher` переменной передается toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` командлет на шаге 4.

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

Устранение неполадок ресурсов возвращает данные о работоспособности hello hello ресурса, также сохраняет журналы tooa хранилища учетной записи toobe проверены. На этом этапе мы создадим учетную запись хранения. При необходимости можно использовать имеющуюся учетную запись хранения.

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a>Выполнение устранения неполадок с ресурсами Наблюдателя за сетями

Устранение ресурсы с hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` командлета. Мы передаем объект Наблюдатель сети hello командлета hello, hello идентификатор hello подключения или шлюза виртуальной сети, ИД учетной записи хранилища hello и hello путь toostore hello результаты.

> [!NOTE]
> Hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` командлета является долго выполняющихся и может занять несколько минут toocomplete.

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

После выполнения командлета hello Наблюдатель сети проверки работоспособности hello tooverify ресурсов hello. Он возвращает результаты hello toohello оболочки и сохраняет журналы hello результатов в указанную учетную запись хранения hello.

## <a name="understanding-hello-results"></a>Основные сведения о результатах hello

текст Hello действия даются общие рекомендации по как tooresolve hello проблему. Если действие может устранить проблему hello, ссылка предоставляется с Дополнительные рекомендации. В случае hello которых нет Дополнительные рекомендации, ответ hello предоставляет tooopen URL-адрес hello обращение в службу поддержки.  Дополнительные сведения о свойствах hello ответа hello и которые не включены [Общие сведения об устранении Наблюдатель сети](network-watcher-troubleshoot-overview.md)

Инструкции по загрузке файлов из учетных записей хранилища azure, см. в разделе слишком[приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Кроме того, можно использовать такое средство, как Storage Explorer. Дополнительные сведения об обозревателе хранилища можно найти по ссылке hello здесь: [обозреватель хранилищ](http://storageexplorer.com/)

## <a name="next-steps"></a>Дальнейшие действия

Если параметры были изменены, остановите подключения VPN, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, возможно, в вопросе.
