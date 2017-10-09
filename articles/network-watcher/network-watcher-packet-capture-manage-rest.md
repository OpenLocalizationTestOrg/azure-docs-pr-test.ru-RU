---
title: "снимки aaaManage пакетов с Наблюдатель сети Azure — REST API | Документы Microsoft"
description: "На этой странице объясняется, как toomanage hello функция записи пакетов Наблюдатель сети с помощью Azure REST API"
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
ms.openlocfilehash: 7a531fbe796e85e94961bd192d171defb299be05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="6f1d6-103">Управление записью пакетов с помощью Наблюдателя за сетями Azure и Azure REST API</span><span class="sxs-lookup"><span data-stu-id="6f1d6-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6f1d6-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="6f1d6-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="6f1d6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f1d6-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="6f1d6-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="6f1d6-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="6f1d6-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6f1d6-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="6f1d6-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="6f1d6-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="6f1d6-109">Захват пакетов Наблюдатель сети позволяет tooand toocreate отслеживания сеансов tootrack трафик от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="6f1d6-110">Можно записать только трафик hello нужные фильтры предоставляются для tooensure сеанс отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="6f1d6-111">Захват пакетов помогает аномалий toodiagnose сети как реактивный, так и заранее.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="6f1d6-112">Другим пользователям включать сбор статистики сети, получение сведений о сети вторжений, toodebug клиент сервер, связи и многое другое.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="6f1d6-113">Из-за захват пакетов может tooremotely триггера, эта возможность облегчает нагрузку hello выполнения захват пакетов на нужный машины hello, чтобы экономить время и вручную.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="6f1d6-114">В этой статье описывается hello задачи управления, которые в настоящее время доступны для получения пакетов.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="6f1d6-115">**Получение записи пакета**</span><span class="sxs-lookup"><span data-stu-id="6f1d6-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="6f1d6-116">**Вывод списка всех записей пакетов**</span><span class="sxs-lookup"><span data-stu-id="6f1d6-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="6f1d6-117">**Состояние запроса hello захват пакетов**</span><span class="sxs-lookup"><span data-stu-id="6f1d6-117">**Query hello status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="6f1d6-118">**Запуск записи пакета**</span><span class="sxs-lookup"><span data-stu-id="6f1d6-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="6f1d6-119">**Прекращение записи пакета**</span><span class="sxs-lookup"><span data-stu-id="6f1d6-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="6f1d6-120">**Удаление записи пакета**</span><span class="sxs-lookup"><span data-stu-id="6f1d6-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="6f1d6-121">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="6f1d6-121">Before you begin</span></span>

<span data-ttu-id="6f1d6-122">В этом случае вызывать toorun API-интерфейса Rest Наблюдатель сети hello IP потока проверки.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-122">In this scenario, you call hello Network Watcher Rest API toorun IP Flow Verify.</span></span> <span data-ttu-id="6f1d6-123">ARMclient — используется toocall hello REST API с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-123">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="6f1d6-124">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="6f1d6-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="6f1d6-125">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-125">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> <span data-ttu-id="6f1d6-126">Для записи пакетов необходимо расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="6f1d6-127">Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="6f1d6-127">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="6f1d6-128">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="6f1d6-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="6f1d6-129">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="6f1d6-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="6f1d6-130">Запустите следующий сценарий tooreturn hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-130">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="6f1d6-131">Эти сведения необходимы для запуска записи пакетов.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="6f1d6-132">Hello следующий код должен переменных:</span><span class="sxs-lookup"><span data-stu-id="6f1d6-132">hello following code needs variables:</span></span>

- <span data-ttu-id="6f1d6-133">**subscriptionId** -идентификатор подписки hello также можно получить с помощью hello **Get AzureRMSubscription** командлета.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-133">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="6f1d6-134">**resourceGroupName** — hello имя группы ресурсов, содержащем виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-134">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="6f1d6-135">Из hello следующие выходные данные, идентификатор hello hello виртуальной машины используется в следующем примере hello.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-135">From hello following output, hello id of hello virtual machine is used in hello next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="6f1d6-136">Получение записи пакета</span><span class="sxs-lookup"><span data-stu-id="6f1d6-136">Get a packet capture</span></span>

<span data-ttu-id="6f1d6-137">Hello следующий пример возвращает состояние отслеживания однократная hello</span><span class="sxs-lookup"><span data-stu-id="6f1d6-137">hello following example gets hello status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="6f1d6-138">Hello следующие ответы приведены примеры типичных ответа, возвращаемые при запросе hello состояние отслеживания пакетов.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-138">hello following responses are examples of a typical response returned when querying hello status of a packet capture.</span></span>

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

## <a name="list-all-packet-captures"></a><span data-ttu-id="6f1d6-139">Вывод списка всех записей пакетов</span><span class="sxs-lookup"><span data-stu-id="6f1d6-139">List all packet captures</span></span>

<span data-ttu-id="6f1d6-140">Здравствуй, следующий пример возвращает все сеансы регистрации пакетов в области.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-140">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="6f1d6-141">Hello следующий ответ — захватывает пример типичных ответ возвращается, если получение всех пакетов</span><span class="sxs-lookup"><span data-stu-id="6f1d6-141">hello following response is an example of a typical response returned when getting all packet captures</span></span>

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

## <a name="query-packet-capture-status"></a><span data-ttu-id="6f1d6-142">Запрос состояния записи пакета</span><span class="sxs-lookup"><span data-stu-id="6f1d6-142">Query packet capture status</span></span>

<span data-ttu-id="6f1d6-143">Здравствуй, следующий пример возвращает все сеансы регистрации пакетов в области.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-143">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="6f1d6-144">Hello следующий ответ приведен пример ответа обычно, возвращаемый при опросе hello состояние отслеживания пакетов.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-144">hello following response is an example of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="6f1d6-145">Запуск записи пакета</span><span class="sxs-lookup"><span data-stu-id="6f1d6-145">Start packet capture</span></span>

<span data-ttu-id="6f1d6-146">Следующий пример Hello создает захват пакетов на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-146">hello following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="6f1d6-147">пример Hello является параметризованный tooallow для гибкость при создании примера.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-147">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

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

## <a name="stop-packet-capture"></a><span data-ttu-id="6f1d6-148">Прекращение записи пакета</span><span class="sxs-lookup"><span data-stu-id="6f1d6-148">Stop packet capture</span></span>

<span data-ttu-id="6f1d6-149">Следующий пример Hello останавливает захват пакетов на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-149">hello following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="6f1d6-150">пример Hello является параметризованный tooallow для гибкость при создании примера.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-150">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="6f1d6-151">Удаление записи пакета</span><span class="sxs-lookup"><span data-stu-id="6f1d6-151">Delete packet capture</span></span>

<span data-ttu-id="6f1d6-152">Следующий пример Hello удаляет захват пакетов на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-152">hello following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="6f1d6-153">пример Hello является параметризованный tooallow для гибкость при создании примера.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-153">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="6f1d6-154">Удаление захват пакетов не удаляет файл hello в учетной записи хранения hello</span><span class="sxs-lookup"><span data-stu-id="6f1d6-154">Deleting a packet capture does not delete hello file in hello storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f1d6-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f1d6-155">Next steps</span></span>

<span data-ttu-id="6f1d6-156">Инструкции по загрузке файлов из учетных записей хранилища azure, см. в разделе слишком[приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="6f1d6-156">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="6f1d6-157">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="6f1d6-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="6f1d6-158">Дополнительные сведения об обозревателе хранилища можно найти по ссылке hello здесь: [обозреватель хранилищ](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="6f1d6-158">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="6f1d6-159">Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="6f1d6-159">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













