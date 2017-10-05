---
title: "Управление записью пакетов с помощью Наблюдателя за сетями Azure (Azure CLI 1.0) | Документация Майкрософт"
description: "В этой статье объясняется, как с помощью Azure CLI 1.0 управлять функцией записи пакетов в Наблюдателе за сетями."
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
ms.openlocfilehash: 91588910334859c1ea77186674d5bfb31b311b36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="9969e-103">Управление записью пакетов с помощью Наблюдателя за сетями Azure в Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9969e-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9969e-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="9969e-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="9969e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9969e-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="9969e-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="9969e-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="9969e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9969e-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="9969e-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="9969e-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="9969e-109">Возможность записи пакетов Наблюдателя за сетями позволяет создавать сеансы записи для отслеживания входящего и исходящего трафика виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9969e-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="9969e-110">Для сеанса записи предоставляются фильтры, которые позволяют убедиться, что записывается только требуемый трафик.</span><span class="sxs-lookup"><span data-stu-id="9969e-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="9969e-111">Записи пакетов помогают выявить аномалии в работе сети по факту или заранее.</span><span class="sxs-lookup"><span data-stu-id="9969e-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="9969e-112">Они также помогают выполнять сбор сетевой статистики, получать сведения о сетевых вторжениях, выполнять отладку передачи данных между клиентом и сервером и многое другое.</span><span class="sxs-lookup"><span data-stu-id="9969e-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="9969e-113">Так как запись пакетов активируется удаленно, ее не нужно запускать вручную. К тому же она сразу выполняется на требуемой виртуальной машине, что также позволяет сэкономить ценное время.</span><span class="sxs-lookup"><span data-stu-id="9969e-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="9969e-114">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="9969e-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="9969e-115">В этой статье вы ознакомитесь с разными задачами управления, доступными в настоящее время для записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="9969e-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="9969e-116">**Запуск записи пакета**</span><span class="sxs-lookup"><span data-stu-id="9969e-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="9969e-117">**Прекращение записи пакета**</span><span class="sxs-lookup"><span data-stu-id="9969e-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="9969e-118">**Удаление записи пакета**</span><span class="sxs-lookup"><span data-stu-id="9969e-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="9969e-119">**Скачивание записи пакета**</span><span class="sxs-lookup"><span data-stu-id="9969e-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="9969e-120">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9969e-120">Before you begin</span></span>

<span data-ttu-id="9969e-121">В данной статье предполагается, что у вас есть следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="9969e-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="9969e-122">экземпляр Наблюдателя за сетями в регионе, в котором нужно создать запись пакетов;</span><span class="sxs-lookup"><span data-stu-id="9969e-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="9969e-123">виртуальная машина с включенным расширением для записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="9969e-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969e-124">Для записи пакетов требуется, чтобы на виртуальной машине был запущен агент.</span><span class="sxs-lookup"><span data-stu-id="9969e-124">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="9969e-125">Агент устанавливается в качестве расширения.</span><span class="sxs-lookup"><span data-stu-id="9969e-125">The Agent is installed as an extension.</span></span> <span data-ttu-id="9969e-126">Инструкции по расширениям виртуальных машин см. в статье [Обзор расширений и компонентов виртуальной машины под управлением Windows](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="9969e-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="9969e-127">Установка расширения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9969e-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="9969e-128">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="9969e-128">Step 1</span></span>

<span data-ttu-id="9969e-129">Выполните командлет `azure vm extension set`, чтобы установить агент записи пакетов на гостевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9969e-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="9969e-130">Для виртуальных машин Windows:</span><span class="sxs-lookup"><span data-stu-id="9969e-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="9969e-131">Для виртуальных машин Linux:</span><span class="sxs-lookup"><span data-stu-id="9969e-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="9969e-132">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="9969e-132">Step 2</span></span>

<span data-ttu-id="9969e-133">Чтобы убедиться, что агент установлен, выполните командлет `vm extension get` и передайте ему имя группы ресурсов и виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9969e-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="9969e-134">Проверьте итоговый список, чтобы убедиться, что агент установлен.</span><span class="sxs-lookup"><span data-stu-id="9969e-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="9969e-135">Ниже приведен пример ответа после выполнения операции `azure vm extension get`.</span><span class="sxs-lookup"><span data-stu-id="9969e-135">The following sample is an example of the response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up the VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="9969e-136">Запуск записи пакета</span><span class="sxs-lookup"><span data-stu-id="9969e-136">Start a packet capture</span></span>

<span data-ttu-id="9969e-137">После выполнения предыдущих шагов на виртуальной машине будет установлен агент записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="9969e-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="9969e-138">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="9969e-138">Step 1</span></span>

<span data-ttu-id="9969e-139">Далее необходимо извлечь экземпляр Наблюдателя за сетями.</span><span class="sxs-lookup"><span data-stu-id="9969e-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="9969e-140">Эта переменная передается в командлет `network watcher show` на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="9969e-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="9969e-141">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="9969e-141">Step 2</span></span>

<span data-ttu-id="9969e-142">Получите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="9969e-142">Retrieve a storage account.</span></span> <span data-ttu-id="9969e-143">Она используется для хранения файла записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="9969e-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="9969e-144">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="9969e-144">Step 3</span></span>

<span data-ttu-id="9969e-145">С помощью фильтров можно ограничить данные, которые сохраняются при записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="9969e-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="9969e-146">В следующем примере настраивается запись пакетов с несколькими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="9969e-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="9969e-147">Первые три фильтра собирают исходящий TCP-трафик только с локального IP-адреса 10.0.0.3 на порты назначения 20, 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="9969e-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="9969e-148">Последний фильтр собирает только трафик, передаваемый по протоколу UDP.</span><span class="sxs-lookup"><span data-stu-id="9969e-148">The last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="9969e-149">Для записи пакетов можно определить несколько фильтров.</span><span class="sxs-lookup"><span data-stu-id="9969e-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="9969e-150">Если используется сложная структура фильтров, во избежание синтаксических ошибок лучше применять фильтры в виде JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="9969e-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span></span> <span data-ttu-id="9969e-151">Например, используйте флаг -r (вместо -f) и передайте расположение JSON-файла, содержащего следующие фильтры:</span><span class="sxs-lookup"><span data-stu-id="9969e-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span></span>

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


<span data-ttu-id="9969e-152">Ниже приведен пример ожидаемого результата выполнения командлета `network watcher packet-capture create`.</span><span class="sxs-lookup"><span data-stu-id="9969e-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="9969e-153">Получение записи пакета</span><span class="sxs-lookup"><span data-stu-id="9969e-153">Get a packet capture</span></span>

<span data-ttu-id="9969e-154">При выполнении командлета `network watcher packet-capture show` вы получаете сведения о состоянии выполняющейся или завершенной записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="9969e-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="9969e-155">Ниже представлен пример выходных данных командлета `network watcher packet-capture show`,</span><span class="sxs-lookup"><span data-stu-id="9969e-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="9969e-156">полученных после завершения записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="9969e-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="9969e-157">В качестве значения параметра PacketCaptureStatus указано Stopped, а для параметра StopReason задано значение TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="9969e-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="9969e-158">По этому значению можно понять, что запись пакетов выполнена успешно за требуемое время.</span><span class="sxs-lookup"><span data-stu-id="9969e-158">This value shows that the packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="9969e-159">Прекращение записи пакета</span><span class="sxs-lookup"><span data-stu-id="9969e-159">Stop a packet capture</span></span>

<span data-ttu-id="9969e-160">Если выполнить командлет `network watcher packet-capture stop` во время сеанса записи пакета, он будет остановлен.</span><span class="sxs-lookup"><span data-stu-id="9969e-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="9969e-161">При выполнении во время текущего сеанса записи или в имеющемся остановленном сеансе командлет не возвратит ответ.</span><span class="sxs-lookup"><span data-stu-id="9969e-161">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="9969e-162">Удаление записи пакета</span><span class="sxs-lookup"><span data-stu-id="9969e-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="9969e-163">При удалении записи пакета файл в учетной записи хранения не удаляется.</span><span class="sxs-lookup"><span data-stu-id="9969e-163">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="9969e-164">Скачивание записи пакета</span><span class="sxs-lookup"><span data-stu-id="9969e-164">Download a packet capture</span></span>

<span data-ttu-id="9969e-165">После завершения сеанса записи пакета файл записи можно передать в хранилище BLOB-объектов или в локальный файл на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9969e-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="9969e-166">Место хранения записи пакетов определяется при создании сеанса.</span><span class="sxs-lookup"><span data-stu-id="9969e-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="9969e-167">Удобное средство для доступа к этим файлам записи, сохраненным в учетной записи хранения — обозреватель службы хранилища Microsoft Azure, который можно скачать по адресу http://storageexplorer.com/.</span><span class="sxs-lookup"><span data-stu-id="9969e-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="9969e-168">При указании учетной записи хранения файлы записи пакетов сохраняются в ней по следующему адресу:</span><span class="sxs-lookup"><span data-stu-id="9969e-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="9969e-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9969e-169">Next steps</span></span>

<span data-ttu-id="9969e-170">Дополнительные сведения об автоматизации записи пакетов с помощью оповещений на виртуальной машине см. в статье, посвященной [созданию записи пакетов, активируемой с использованием оповещений](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="9969e-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="9969e-171">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9969e-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
