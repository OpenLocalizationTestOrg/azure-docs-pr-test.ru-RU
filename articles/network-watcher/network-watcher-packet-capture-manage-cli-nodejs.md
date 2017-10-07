---
title: "снимки aaaManage пакетов с Наблюдатель сети Azure — Azure CLI 1.0 | Документы Microsoft"
description: "На этой странице объясняется, как toomanage hello функция записи пакетов с помощью Azure CLI 1.0 Наблюдатель сети"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a>Управление записью пакетов с помощью Наблюдателя за сетями Azure в Azure CLI 1.0

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API](network-watcher-packet-capture-manage-rest.md)

Захват пакетов Наблюдатель сети позволяет tooand toocreate отслеживания сеансов tootrack трафик от виртуальной машины. Можно записать только трафик hello нужные фильтры предоставляются для tooensure сеанс отслеживания hello. Захват пакетов помогает аномалий toodiagnose сети как реактивный, так и заранее. Другим пользователям включать сбор статистики сети, получение сведений о сети вторжений, toodebug клиент сервер, связи и многое другое. Из-за захват пакетов может tooremotely триггера, эта возможность облегчает нагрузку hello выполнения захват пакетов на нужный машины hello, чтобы экономить время и вручную.

В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.

В этой статье описывается hello задачи управления, которые в настоящее время доступны для получения пакетов.

- [**Запуск записи пакета**](#start-a-packet-capture)
- [**Прекращение записи пакета**](#stop-a-packet-capture)
- [**Удаление записи пакета**](#delete-a-packet-capture)
- [**Скачивание записи пакета**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Перед началом работы

В этой статье предполагается, что hello следующие ресурсы:

- Экземпляр Наблюдатель сети в регионе hello нужно toocreate захват пакетов
- Виртуальная машина с пакет приветствия записать расширение включено.

> [!IMPORTANT]
> Захват пакетов требуется toobe агент, работающий на виртуальной машине hello. Hello агент установлен в качестве расширения. Инструкции по расширениям виртуальных машин см. в статье [Обзор расширений и компонентов виртуальной машины под управлением Windows](../virtual-machines/windows/extensions-features.md).

## <a name="install-vm-extension"></a>Установка расширения виртуальной машины

### <a name="step-1"></a>Шаг 1

Запустите hello `azure vm extension set` агент командлет tooinstall hello пакет отслеживания на hello гостевой виртуальной машине.

Для виртуальных машин Windows:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

Для виртуальных машин Linux:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a>Шаг 2

tooensure, hello агент установлен, запустите hello `vm extension get` командлета и передать его в группу ресурсов hello и имя виртуальной машины. Убедитесь, что установлен hello полученный список tooensure hello агент.

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

Следующий образец Hello приведен пример ответа hello, запуск`azure vm extension get`

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a>Запуск записи пакета

После hello предыдущего выполнения действий, hello пакет отслеживания агент устанавливается на виртуальной машине hello.

### <a name="step-1"></a>Шаг 1

Hello следующим шагом является экземпляр Наблюдатель сети tooretrieve hello. Эта переменная передается toohello `network watcher show` командлет на шаге 4.

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a>Шаг 2

Получите учетную запись хранения. Эта учетная запись хранения — файл записи пакетов используется toostore hello.

```azurecli
azure storage account list
```

### <a name="step-3"></a>Шаг 3.

Фильтры можно использовать toolimit hello данные, которые хранятся с захватом пакетов hello. Hello следующий пример устанавливает захват пакетов с несколькими фильтрами.  Hello первые три фильтры собирать исходящего трафика TCP только с локального IP-адреса 10.0.0.3 toodestination порты 20, 80 и 443.  последний фильтр Hello собирает только трафик UDP.

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Для записи пакетов можно определить несколько фильтров. При использовании структуры сложный фильтр, лучше toouse фильтров является json файл tooavoid синтаксических ошибок. Используйте флаг hello, например, «-r» (вместо «-f») и передать hello расположение файла json, содержащего hello следующие фильтры:

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


Hello следующий пример является hello ожидалось результатов выполнения hello `network watcher packet-capture create` командлета.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a>Получение записи пакета

Под управлением hello `network watcher packet-capture show` , получает hello состояние выполняющегося или завершенного отслеживания пакетов.

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

Hello ниже приведен вывод hello hello `network watcher packet-capture show` командлета. Hello следующий пример — после завершения записи hello. Hello значение PacketCaptureStatus остановлена с StopReason TimeExceeded. Это значение показывает, что захват пакетов hello прошла успешно и время его запуска.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a>Прекращение записи пакета

Запустив hello `network watcher packet-capture stop` командлета, если записи сеанса выполняется она остановлена.

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Hello командлет не возвращает ответа при выполнялись в момент записи сеанса или существующего сеанса, который уже был остановлен.

## <a name="delete-a-packet-capture"></a>Удаление записи пакета

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Удаление захват пакетов не приводит к удалению файла hello в учетной записи хранения hello.

## <a name="download-a-packet-capture"></a>Скачивание записи пакета

После завершения сеанса записи пакета файл записи hello может быть загруженного tooblob хранилища или tooa локальный файл на hello виртуальной Машины. место хранения Hello hello захват пакетов определяется при создании сеанса hello. Tooaccess удобное средство их записывать файлы, сохраненные tooa учетную запись хранения является обозреватель хранилищ Microsoft Azure, которую можно загрузить здесь: http://storageexplorer.com/

При указании учетной записи хранилища пакетов отслеживания файлы сохраняются tooa учетной записи хранилища в hello следующие расположения:

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)

Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).

<!-- Image references -->
