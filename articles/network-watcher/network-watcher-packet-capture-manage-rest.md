---
title: "Управление записью пакетов с помощью Наблюдателя за сетями Azure (REST API) | Документация Майкрософт"
description: "На этой странице объясняется, как управлять функцией записи пакетов Наблюдателя за сетями с помощью REST API."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 49ec20802a252258d8493eb26510270b925e851a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="3fe42-103">Управление записью пакетов с помощью Наблюдателя за сетями Azure и Azure REST API</span><span class="sxs-lookup"><span data-stu-id="3fe42-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3fe42-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="3fe42-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="3fe42-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fe42-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="3fe42-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="3fe42-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="3fe42-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3fe42-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="3fe42-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="3fe42-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="3fe42-109">Возможность записи пакетов Наблюдателя за сетями позволяет создавать сеансы записи для отслеживания входящего и исходящего трафика виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3fe42-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="3fe42-110">Для сеанса записи предоставляются фильтры, которые позволяют убедиться, что записывается только требуемый трафик.</span><span class="sxs-lookup"><span data-stu-id="3fe42-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="3fe42-111">Записи пакетов помогают выявить аномалии в работе сети по факту или заранее.</span><span class="sxs-lookup"><span data-stu-id="3fe42-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="3fe42-112">Они также помогают выполнять сбор сетевой статистики, получать сведения о сетевых вторжениях, выполнять отладку передачи данных между клиентом и сервером и многое другое.</span><span class="sxs-lookup"><span data-stu-id="3fe42-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="3fe42-113">Так как запись пакетов активируется удаленно, ее не нужно запускать вручную. К тому же она сразу выполняется на требуемой виртуальной машине, что также позволяет сэкономить ценное время.</span><span class="sxs-lookup"><span data-stu-id="3fe42-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="3fe42-114">В этой статье вы ознакомитесь с разными задачами управления, доступными в настоящее время для записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="3fe42-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="3fe42-115">**Получение записи пакета**</span><span class="sxs-lookup"><span data-stu-id="3fe42-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="3fe42-116">**Вывод списка всех записей пакетов**</span><span class="sxs-lookup"><span data-stu-id="3fe42-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="3fe42-117">**Запрос состояния записи пакета**</span><span class="sxs-lookup"><span data-stu-id="3fe42-117">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="3fe42-118">**Запуск записи пакета**</span><span class="sxs-lookup"><span data-stu-id="3fe42-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="3fe42-119">**Прекращение записи пакета**</span><span class="sxs-lookup"><span data-stu-id="3fe42-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="3fe42-120">**Удаление записи пакета**</span><span class="sxs-lookup"><span data-stu-id="3fe42-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="3fe42-121">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="3fe42-121">Before you begin</span></span>

<span data-ttu-id="3fe42-122">В этом сценарии вызывается REST API Наблюдателя за сетями для запуска проверки IP-потока.</span><span class="sxs-lookup"><span data-stu-id="3fe42-122">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="3fe42-123">Чтобы вызвать REST API при помощи PowerShell, потребуется ARMClient.</span><span class="sxs-lookup"><span data-stu-id="3fe42-123">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="3fe42-124">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="3fe42-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="3fe42-125">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create a Network Watcher](network-watcher-create.md) (Создание Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="3fe42-125">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> <span data-ttu-id="3fe42-126">Для записи пакетов необходимо расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="3fe42-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="3fe42-127">Информацию об установке расширения для виртуальной машины Windows см. в статье [Расширение виртуальной машины агента Наблюдателя за сетями для Windows](../virtual-machines/windows/extensions-nwa.md), а для виртуальной машины Linux — в статье [Расширение виртуальной машины агента Наблюдателя за сетями для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="3fe42-127">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="3fe42-128">выполните вход с помощью ARMClient;</span><span class="sxs-lookup"><span data-stu-id="3fe42-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="3fe42-129">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="3fe42-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="3fe42-130">Выполните следующий сценарий, чтобы получить сведения о виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="3fe42-130">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="3fe42-131">Эти сведения необходимы для запуска записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="3fe42-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="3fe42-132">В приведенном ниже коде нужно указать переменные.</span><span class="sxs-lookup"><span data-stu-id="3fe42-132">The following code needs variables:</span></span>

- <span data-ttu-id="3fe42-133">**subscriptionId** — идентификатор подписки. Его можно получить с помощью командлета **Get-AzureRMSubscription**.</span><span class="sxs-lookup"><span data-stu-id="3fe42-133">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="3fe42-134">**resourceGroupName** — имя группы ресурсов, в которой содержатся виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="3fe42-134">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="3fe42-135">Идентификатор виртуальной машины из приведенных выходных данных используется в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="3fe42-135">From the following output, the id of the virtual machine is used in the next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="3fe42-136">Получение записи пакета</span><span class="sxs-lookup"><span data-stu-id="3fe42-136">Get a packet capture</span></span>

<span data-ttu-id="3fe42-137">В следующем примере возвращается состояние отдельной записи пакета.</span><span class="sxs-lookup"><span data-stu-id="3fe42-137">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="3fe42-138">Ниже приведены примеры типичных ответов, которые возвращаются при запросе состояния записи пакета.</span><span class="sxs-lookup"><span data-stu-id="3fe42-138">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="3fe42-139">Вывод списка всех записей пакетов</span><span class="sxs-lookup"><span data-stu-id="3fe42-139">List all packet captures</span></span>

<span data-ttu-id="3fe42-140">Следующий пример возвращает все сеансы записи пакетов в регионе.</span><span class="sxs-lookup"><span data-stu-id="3fe42-140">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="3fe42-141">Ниже приведен пример типичного ответа, возвращаемого при получении всех записей пакетов.</span><span class="sxs-lookup"><span data-stu-id="3fe42-141">The following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="3fe42-142">Запрос состояния записи пакета</span><span class="sxs-lookup"><span data-stu-id="3fe42-142">Query packet capture status</span></span>

<span data-ttu-id="3fe42-143">Следующий пример возвращает все сеансы записи пакетов в регионе.</span><span class="sxs-lookup"><span data-stu-id="3fe42-143">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="3fe42-144">Ниже приведен пример типичного ответа, который возвращается при запросе состояния записи пакета.</span><span class="sxs-lookup"><span data-stu-id="3fe42-144">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="3fe42-145">Запуск записи пакета</span><span class="sxs-lookup"><span data-stu-id="3fe42-145">Start packet capture</span></span>

<span data-ttu-id="3fe42-146">В следующем примере создается запись пакета на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="3fe42-146">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="3fe42-147">Он параметризован таким образом, чтобы обеспечить гибкость при создании примера.</span><span class="sxs-lookup"><span data-stu-id="3fe42-147">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="3fe42-148">Прекращение записи пакета</span><span class="sxs-lookup"><span data-stu-id="3fe42-148">Stop packet capture</span></span>

<span data-ttu-id="3fe42-149">В следующем примере останавливается запись пакета на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="3fe42-149">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="3fe42-150">Он параметризован таким образом, чтобы обеспечить гибкость при создании примера.</span><span class="sxs-lookup"><span data-stu-id="3fe42-150">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="3fe42-151">Удаление записи пакета</span><span class="sxs-lookup"><span data-stu-id="3fe42-151">Delete packet capture</span></span>

<span data-ttu-id="3fe42-152">В следующем примере удаляется запись пакета на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="3fe42-152">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="3fe42-153">Он параметризован таким образом, чтобы обеспечить гибкость при создании примера.</span><span class="sxs-lookup"><span data-stu-id="3fe42-153">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="3fe42-154">При удалении записи пакета файл в учетной записи хранения не удаляется.</span><span class="sxs-lookup"><span data-stu-id="3fe42-154">Deleting a packet capture does not delete the file in the storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fe42-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3fe42-155">Next steps</span></span>

<span data-ttu-id="3fe42-156">Инструкции по скачиванию файлов из учетных записей хранения Azure см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="3fe42-156">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="3fe42-157">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="3fe42-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="3fe42-158">Дополнительные сведения о Storage Explorer можно найти по следующей ссылке: [Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="3fe42-158">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="3fe42-159">Узнайте, как автоматизировать запись пакетов, используя оповещения на виртуальной машине, в статье [Использование записи пакетов для упреждающего мониторинга сети с помощью Функций Azure](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="3fe42-159">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













