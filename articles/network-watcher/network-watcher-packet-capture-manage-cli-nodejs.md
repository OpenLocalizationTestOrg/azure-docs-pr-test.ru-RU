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
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="61d3d-103">Управление записью пакетов с помощью Наблюдателя за сетями Azure в Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="61d3d-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="61d3d-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="61d3d-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="61d3d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="61d3d-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="61d3d-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="61d3d-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="61d3d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="61d3d-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="61d3d-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="61d3d-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="61d3d-109">Захват пакетов Наблюдатель сети позволяет tooand toocreate отслеживания сеансов tootrack трафик от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="61d3d-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="61d3d-110">Можно записать только трафик hello нужные фильтры предоставляются для tooensure сеанс отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="61d3d-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="61d3d-111">Захват пакетов помогает аномалий toodiagnose сети как реактивный, так и заранее.</span><span class="sxs-lookup"><span data-stu-id="61d3d-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="61d3d-112">Другим пользователям включать сбор статистики сети, получение сведений о сети вторжений, toodebug клиент сервер, связи и многое другое.</span><span class="sxs-lookup"><span data-stu-id="61d3d-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="61d3d-113">Из-за захват пакетов может tooremotely триггера, эта возможность облегчает нагрузку hello выполнения захват пакетов на нужный машины hello, чтобы экономить время и вручную.</span><span class="sxs-lookup"><span data-stu-id="61d3d-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="61d3d-114">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="61d3d-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="61d3d-115">В этой статье описывается hello задачи управления, которые в настоящее время доступны для получения пакетов.</span><span class="sxs-lookup"><span data-stu-id="61d3d-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="61d3d-116">**Запуск записи пакета**</span><span class="sxs-lookup"><span data-stu-id="61d3d-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="61d3d-117">**Прекращение записи пакета**</span><span class="sxs-lookup"><span data-stu-id="61d3d-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="61d3d-118">**Удаление записи пакета**</span><span class="sxs-lookup"><span data-stu-id="61d3d-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="61d3d-119">**Скачивание записи пакета**</span><span class="sxs-lookup"><span data-stu-id="61d3d-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="61d3d-120">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="61d3d-120">Before you begin</span></span>

<span data-ttu-id="61d3d-121">В этой статье предполагается, что hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="61d3d-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="61d3d-122">Экземпляр Наблюдатель сети в регионе hello нужно toocreate захват пакетов</span><span class="sxs-lookup"><span data-stu-id="61d3d-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="61d3d-123">Виртуальная машина с пакет приветствия записать расширение включено.</span><span class="sxs-lookup"><span data-stu-id="61d3d-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61d3d-124">Захват пакетов требуется toobe агент, работающий на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="61d3d-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="61d3d-125">Hello агент установлен в качестве расширения.</span><span class="sxs-lookup"><span data-stu-id="61d3d-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="61d3d-126">Инструкции по расширениям виртуальных машин см. в статье [Обзор расширений и компонентов виртуальной машины под управлением Windows](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="61d3d-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="61d3d-127">Установка расширения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="61d3d-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="61d3d-128">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="61d3d-128">Step 1</span></span>

<span data-ttu-id="61d3d-129">Запустите hello `azure vm extension set` агент командлет tooinstall hello пакет отслеживания на hello гостевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="61d3d-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="61d3d-130">Для виртуальных машин Windows:</span><span class="sxs-lookup"><span data-stu-id="61d3d-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="61d3d-131">Для виртуальных машин Linux:</span><span class="sxs-lookup"><span data-stu-id="61d3d-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="61d3d-132">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="61d3d-132">Step 2</span></span>

<span data-ttu-id="61d3d-133">tooensure, hello агент установлен, запустите hello `vm extension get` командлета и передать его в группу ресурсов hello и имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="61d3d-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="61d3d-134">Убедитесь, что установлен hello полученный список tooensure hello агент.</span><span class="sxs-lookup"><span data-stu-id="61d3d-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="61d3d-135">Следующий образец Hello приведен пример ответа hello, запуск`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="61d3d-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="61d3d-136">Запуск записи пакета</span><span class="sxs-lookup"><span data-stu-id="61d3d-136">Start a packet capture</span></span>

<span data-ttu-id="61d3d-137">После hello предыдущего выполнения действий, hello пакет отслеживания агент устанавливается на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="61d3d-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="61d3d-138">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="61d3d-138">Step 1</span></span>

<span data-ttu-id="61d3d-139">Hello следующим шагом является экземпляр Наблюдатель сети tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="61d3d-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="61d3d-140">Эта переменная передается toohello `network watcher show` командлет на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="61d3d-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="61d3d-141">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="61d3d-141">Step 2</span></span>

<span data-ttu-id="61d3d-142">Получите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="61d3d-142">Retrieve a storage account.</span></span> <span data-ttu-id="61d3d-143">Эта учетная запись хранения — файл записи пакетов используется toostore hello.</span><span class="sxs-lookup"><span data-stu-id="61d3d-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="61d3d-144">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="61d3d-144">Step 3</span></span>

<span data-ttu-id="61d3d-145">Фильтры можно использовать toolimit hello данные, которые хранятся с захватом пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="61d3d-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="61d3d-146">Hello следующий пример устанавливает захват пакетов с несколькими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="61d3d-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="61d3d-147">Hello первые три фильтры собирать исходящего трафика TCP только с локального IP-адреса 10.0.0.3 toodestination порты 20, 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="61d3d-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="61d3d-148">последний фильтр Hello собирает только трафик UDP.</span><span class="sxs-lookup"><span data-stu-id="61d3d-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="61d3d-149">Для записи пакетов можно определить несколько фильтров.</span><span class="sxs-lookup"><span data-stu-id="61d3d-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="61d3d-150">При использовании структуры сложный фильтр, лучше toouse фильтров является json файл tooavoid синтаксических ошибок.</span><span class="sxs-lookup"><span data-stu-id="61d3d-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="61d3d-151">Используйте флаг hello, например, «-r» (вместо «-f») и передать hello расположение файла json, содержащего hello следующие фильтры:</span><span class="sxs-lookup"><span data-stu-id="61d3d-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

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


<span data-ttu-id="61d3d-152">Hello следующий пример является hello ожидалось результатов выполнения hello `network watcher packet-capture create` командлета.</span><span class="sxs-lookup"><span data-stu-id="61d3d-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="61d3d-153">Получение записи пакета</span><span class="sxs-lookup"><span data-stu-id="61d3d-153">Get a packet capture</span></span>

<span data-ttu-id="61d3d-154">Под управлением hello `network watcher packet-capture show` , получает hello состояние выполняющегося или завершенного отслеживания пакетов.</span><span class="sxs-lookup"><span data-stu-id="61d3d-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="61d3d-155">Hello ниже приведен вывод hello hello `network watcher packet-capture show` командлета.</span><span class="sxs-lookup"><span data-stu-id="61d3d-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="61d3d-156">Hello следующий пример — после завершения записи hello.</span><span class="sxs-lookup"><span data-stu-id="61d3d-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="61d3d-157">Hello значение PacketCaptureStatus остановлена с StopReason TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="61d3d-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="61d3d-158">Это значение показывает, что захват пакетов hello прошла успешно и время его запуска.</span><span class="sxs-lookup"><span data-stu-id="61d3d-158">This value shows that hello packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="61d3d-159">Прекращение записи пакета</span><span class="sxs-lookup"><span data-stu-id="61d3d-159">Stop a packet capture</span></span>

<span data-ttu-id="61d3d-160">Запустив hello `network watcher packet-capture stop` командлета, если записи сеанса выполняется она остановлена.</span><span class="sxs-lookup"><span data-stu-id="61d3d-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="61d3d-161">Hello командлет не возвращает ответа при выполнялись в момент записи сеанса или существующего сеанса, который уже был остановлен.</span><span class="sxs-lookup"><span data-stu-id="61d3d-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="61d3d-162">Удаление записи пакета</span><span class="sxs-lookup"><span data-stu-id="61d3d-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="61d3d-163">Удаление захват пакетов не приводит к удалению файла hello в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="61d3d-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="61d3d-164">Скачивание записи пакета</span><span class="sxs-lookup"><span data-stu-id="61d3d-164">Download a packet capture</span></span>

<span data-ttu-id="61d3d-165">После завершения сеанса записи пакета файл записи hello может быть загруженного tooblob хранилища или tooa локальный файл на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="61d3d-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="61d3d-166">место хранения Hello hello захват пакетов определяется при создании сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="61d3d-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="61d3d-167">Tooaccess удобное средство их записывать файлы, сохраненные tooa учетную запись хранения является обозреватель хранилищ Microsoft Azure, которую можно загрузить здесь: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="61d3d-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="61d3d-168">При указании учетной записи хранилища пакетов отслеживания файлы сохраняются tooa учетной записи хранилища в hello следующие расположения:</span><span class="sxs-lookup"><span data-stu-id="61d3d-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="61d3d-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61d3d-169">Next steps</span></span>

<span data-ttu-id="61d3d-170">Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="61d3d-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="61d3d-171">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61d3d-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
