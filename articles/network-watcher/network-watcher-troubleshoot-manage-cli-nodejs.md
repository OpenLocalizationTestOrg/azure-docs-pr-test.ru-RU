---
title: "aaaTroubleshoot шлюз виртуальной сети Azure и соединений - Azure CLI 1.0 | Документы Microsoft"
description: "На этой странице объясняется, как toouse hello Наблюдатель сети Azure Устранение неполадок Azure CLI 1.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a>Устранение неполадок шлюза виртуальной сети и подключений с помощью наблюдателя за сетями Azure и Azure CLI 1.0

> [!div class="op_single_selector"]
> - [Портал](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

Наблюдатель сети предоставляет множество возможностей, по отношению к сетевым ресурсам в Azure toounderstanding. Одна из этих возможностей — устранение неполадок в ресурсах. Устранение неполадок ресурсов можно вызвать через портал hello, PowerShell, CLI или REST API. При вызове Наблюдатель сети проверяет работоспособность hello шлюза виртуальной сети или подключения и возвращает результаты.

В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux. 

## <a name="before-you-begin"></a>Перед началом работы

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.

Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](/network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Обзор

Устранение неполадок ресурсов предоставляет возможность hello Устранение неполадок, возникающих с подключениями и шлюзах виртуальной сети. При запросе tooresource Устранение неполадок, журналы, запросы и проверен. После завершения проверки hello результатов. Запрашивает ресурс, который долго выполняющиеся запросы по устранению неполадок, которой может занять несколько минут tooreturn результат. Устранение неполадок журналы Hello хранятся в контейнер в учетной записи хранилища, который указан.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Получение сведений о подключении к шлюзу виртуальной сети

В этом примере выполняется устранение неполадок с таким ресурсом, как подключение. Его также можно передать шлюзу виртуальной сети. Hello следующий командлет отображает hello vpn подключений в группе ресурсов.

```azurecli
azure network vpn-connection list -g resourceGroupName
```

Также можно запустить команду toosee hello hello подключений в подписке.

```azurecli
azure network vpn-connection list -s subscription
```

Получив имя hello подключения hello, tooget этой команды можно выполнить его идентификатором ресурса:

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a>Создайте учетную запись хранения.

Устранение неполадок ресурсов возвращает данные о работоспособности hello hello ресурса, также сохраняет журналы tooa хранилища учетной записи toobe проверены. На этом этапе мы создадим учетную запись хранения. При необходимости можно использовать имеющуюся учетную запись хранения.

1. Создать учетную запись хранения hello

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. Получить ключи учетной записи хранения hello

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. Создание контейнера hello

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Выполнение устранения неполадок с ресурсами Наблюдателя за сетями

Устранение ресурсы с hello `network watcher troubleshoot` командлета. Мы передаем группы ресурсов hello командлет hello, hello имя hello Наблюдатель сети, hello идентификатор соединения hello hello идентификатор учетной записи хранения hello и hello путь toohello большого двоичного объекта toostore hello диагностики результаты в.

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

После выполнения командлета hello Наблюдатель сети проверки работоспособности hello tooverify ресурсов hello. Он возвращает результаты hello toohello оболочки и сохраняет журналы hello результатов в указанную учетную запись хранения hello.

## <a name="understanding-hello-results"></a>Основные сведения о результатах hello

текст Hello действия даются общие рекомендации по как tooresolve hello проблему. Если действие может устранить проблему hello, ссылка предоставляется с Дополнительные рекомендации. В случае hello которых нет Дополнительные рекомендации, ответ hello предоставляет tooopen URL-адрес hello обращение в службу поддержки.  Дополнительные сведения о свойствах hello ответа hello и которые не включены [Общие сведения об устранении Наблюдатель сети](network-watcher-troubleshoot-overview.md)

Инструкции по загрузке файлов из учетных записей хранилища azure, см. в разделе слишком[приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Кроме того, можно использовать такое средство, как Storage Explorer. Дополнительные сведения об обозревателе хранилища можно найти по ссылке hello здесь: [обозреватель хранилищ](http://storageexplorer.com/)

## <a name="next-steps"></a>Дальнейшие действия

Если параметры были изменены, остановите подключения VPN, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, возможно, в вопросе.
