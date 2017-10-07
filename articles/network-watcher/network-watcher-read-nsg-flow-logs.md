---
title: "журналы потока aaaRead NSG | Документы Microsoft"
description: "В этой статье показано, каким образом ведет журнал tooparse NSG потока"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: b4f0f64639c7b2a6b4db50e54d15056bfd809e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-nsg-flow-logs"></a><span data-ttu-id="1a098-103">Чтение журналов последовательностей NSG</span><span class="sxs-lookup"><span data-stu-id="1a098-103">Read NSG flow logs</span></span>

<span data-ttu-id="1a098-104">Узнайте, каким образом tooread NSG потока ведет журнал записей с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a098-104">Learn how tooread NSG flow logs entries with PowerShell.</span></span>

<span data-ttu-id="1a098-105">Журналы последовательностей NSG хранятся в учетной записи хранения в [блочных BLOB-объектах](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span><span class="sxs-lookup"><span data-stu-id="1a098-105">NSG flow logs are stored in a storage account in [block blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span></span> <span data-ttu-id="1a098-106">Блочные BLOB-объекты состоят из небольших блоков.</span><span class="sxs-lookup"><span data-stu-id="1a098-106">Block blobs are made up of smaller blocks.</span></span> <span data-ttu-id="1a098-107">Каждый журнал — это отдельный блочный BLOB-объект, который создается один раз в час.</span><span class="sxs-lookup"><span data-stu-id="1a098-107">Each log is a separate block blob that is generated every hour.</span></span> <span data-ttu-id="1a098-108">Новые журналы создаются каждый час, журналы hello обновляются новые записи каждые несколько минут hello последние данные.</span><span class="sxs-lookup"><span data-stu-id="1a098-108">New logs are generated every hour, hello logs are updated with new entries every few minutes with hello latest data.</span></span> <span data-ttu-id="1a098-109">В этой статье вы узнаете, как части tooread hello потока журналы.</span><span class="sxs-lookup"><span data-stu-id="1a098-109">In this article you learn how tooread portions of hello flow logs.</span></span>

## <a name="scenario"></a><span data-ttu-id="1a098-110">Сценарий</span><span class="sxs-lookup"><span data-stu-id="1a098-110">Scenario</span></span>

<span data-ttu-id="1a098-111">Следующие сценарии hello имеется примере потока журнала, хранящиеся в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="1a098-111">In hello following scenario, you have an example flow log that is stored in a storage account.</span></span> <span data-ttu-id="1a098-112">мы пошагово как выборочно считывать hello последние события в журналах NSG потока.</span><span class="sxs-lookup"><span data-stu-id="1a098-112">we step through how you can selectively read hello latest events in NSG flow logs.</span></span> <span data-ttu-id="1a098-113">В этой статье мы будем использовать PowerShell, однако hello концепции, описанные в статье hello не ограниченной toohello язык программирования и, применимые tooall языков, поддерживаемых hello API-интерфейсов хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="1a098-113">In this article we will use PowerShell, however, hello concepts discussed in hello article are not limited toohello programming language and are applicable tooall languages supported by hello Azure Storage APIs</span></span>

## <a name="setup"></a><span data-ttu-id="1a098-114">Настройка</span><span class="sxs-lookup"><span data-stu-id="1a098-114">Setup</span></span>

<span data-ttu-id="1a098-115">Прежде чем мы начнем работу, вам необходимо включить журналы потоков для одной или нескольких групп безопасности сети в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1a098-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="1a098-116">Инструкции по включению сетевой безопасности потока журналов см. в следующей статьей toohello: [ведения журнала tooflow введение для групп безопасности сети](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a098-116">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="retrieve-hello-block-list"></a><span data-ttu-id="1a098-117">Получить список блокировок hello</span><span class="sxs-lookup"><span data-stu-id="1a098-117">Retrieve hello block list</span></span>

<span data-ttu-id="1a098-118">Здравствуйте, следуя PowerShell настраивает переменные hello необходимые hello tooquery NSG потока журнала больших двоичных объектов и список hello блоках hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) блочного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="1a098-118">hello following PowerShell sets up hello variables needed tooquery hello NSG flow log blob and list hello blocks within hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span></span> <span data-ttu-id="1a098-119">Обновите hello сценария toocontain допустимые значения для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="1a098-119">Update hello script toocontain valid values for your environment.</span></span>

```powershell
# hello SubscriptionID toouse
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains hello Network Security Group
$resourceGroupName = "<resourceGroupName>"

# hello name of hello Network Security Group
$nsgName = "NSGName"

# hello storage account name that contains hello NSG logs
$storageAccountName = "<storageAccountName>" 

# hello date and time for hello log toobe queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve hello primary storage account key tooaccess hello NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context toobe used tooquery hello logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of hello blob that contains hello NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets hello storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets hello block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from hello storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores hello block list in a variable from hello block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

<span data-ttu-id="1a098-120">Hello `$blockList` переменная возвращает список блоков hello в большом двоичном объекте hello.</span><span class="sxs-lookup"><span data-stu-id="1a098-120">hello `$blockList` variable returns a list of hello blocks in hello blob.</span></span> <span data-ttu-id="1a098-121">Каждый блочный BLOB-объект содержит не менее двух блоков.</span><span class="sxs-lookup"><span data-stu-id="1a098-121">Each block blob contains at least two blocks.</span></span>  <span data-ttu-id="1a098-122">Hello первый блок имеет длину `21` байт, этот блок содержит hello открывающей скобкой журнала hello json.</span><span class="sxs-lookup"><span data-stu-id="1a098-122">hello first block has a length of `21` bytes, this block contains hello opening brackets of hello json log.</span></span> <span data-ttu-id="1a098-123">Hello других блок hello закрывающие скобки и имеет длину `9` байт.</span><span class="sxs-lookup"><span data-stu-id="1a098-123">hello other block is hello closing brackets and has a length of `9` bytes.</span></span>  <span data-ttu-id="1a098-124">Как можно видеть hello следующий пример журнала содержит семь записей, каждая отдельная запись выполняется.</span><span class="sxs-lookup"><span data-stu-id="1a098-124">As you can see hello following example log has seven entries in it, each being an individual entry.</span></span> <span data-ttu-id="1a098-125">Все новые записи в журнале hello добавляются окончания toohello прямо перед hello конечный блок.</span><span class="sxs-lookup"><span data-stu-id="1a098-125">All new entries in hello log are added toohello end right before hello final block.</span></span>

```
Name                                         Length Committed
----                                         ------ ---------
ZDk5MTk5N2FkNGE0MmY5MTk5ZWViYjA0YmZhODRhYzY=     21      True
NzQxNDA5MTRhNDUzMGI2M2Y1MDMyOWZlN2QwNDZiYzQ=   2685      True
ODdjM2UyMWY3NzFhZTU3MmVlMmU5MDNlOWEwNWE3YWY=   2586      True
ZDU2MjA3OGQ2ZDU3MjczMWQ4MTRmYWNhYjAzOGJkMTg=   2688      True
ZmM3ZWJjMGQ0ZDA1ODJlOWMyODhlOWE3MDI1MGJhMTc=   2775      True
ZGVkYTc4MzQzNjEyMzlmZWE5MmRiNjc1OWE5OTc0OTQ=   2676      True
ZmY2MjUzYTIwYWIyOGU1OTA2ZDY1OWYzNmY2NmU4ZTY=   2777      True
Mzk1YzQwM2U0ZWY1ZDRhOWFlMTNhYjQ3OGVhYmUzNjk=   2675      True
ZjAyZTliYWE3OTI1YWZmYjFmMWI0MjJhNzMxZTI4MDM=      9      True
```

## <a name="read-hello-block-blob"></a><span data-ttu-id="1a098-126">Чтение hello блочный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="1a098-126">Read hello block blob</span></span>

<span data-ttu-id="1a098-127">Теперь нам нужны tooread hello `$blocklist` переменных tooretrieve hello данных.</span><span class="sxs-lookup"><span data-stu-id="1a098-127">Next we need tooread hello `$blocklist` variable tooretrieve hello data.</span></span> <span data-ttu-id="1a098-128">В этом примере мы итерации hello блокировки считать hello байт из каждого блока и баллов истории их в массиве.</span><span class="sxs-lookup"><span data-stu-id="1a098-128">In this example we iterate through hello blocklist, read hello bytes from each block and story them in an array.</span></span> <span data-ttu-id="1a098-129">Мы используем hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) данные hello tooretrieve метода.</span><span class="sxs-lookup"><span data-stu-id="1a098-129">We use hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method tooretrieve hello data.</span></span>

```powershell
# Set hello size of hello byte array toohello largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array toostore values in
$valuearray = @()

# Define hello starting index tootrack hello current block being read
$index = 0

# Loop through each block in hello block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object toostory hello bytes from hello block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download hello data into hello ByteArray, starting with hello current index, for hello number of bytes in hello current block. Index is increased by 3 when reading tooremove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment hello index by adding hello current block length toohello previous index
$index = $index + $blockList[$i].Length

# Retrieve hello string from hello byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add hello log entry toohello value array
$valuearray += $value
}
```

<span data-ttu-id="1a098-130">Теперь hello `$valuearray` массив содержит строковое значение hello каждого блока.</span><span class="sxs-lookup"><span data-stu-id="1a098-130">Now hello `$valuearray` array contains hello string value of each block.</span></span> <span data-ttu-id="1a098-131">запись tooverify hello, get hello второй toohello последнее значение из массива hello, запустив `$valuearray[$valuearray.Length-2]`.</span><span class="sxs-lookup"><span data-stu-id="1a098-131">tooverify hello entry, get hello second toohello last value from hello array by running `$valuearray[$valuearray.Length-2]`.</span></span> <span data-ttu-id="1a098-132">Нам не нужно, последнее значение hello является просто hello закрывающую скобку.</span><span class="sxs-lookup"><span data-stu-id="1a098-132">We do not want hello last value is just hello closing bracket.</span></span>

<span data-ttu-id="1a098-133">результаты Hello этого значения отображаются в hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1a098-133">hello results of this value are shown in hello following example:</span></span>

```json
        {
             "time": "2017-06-16T20:59:43.7340000Z",
             "systemId": "5f4d02d3-a7d0-4ed4-9ce8-c0ae9377951c",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/CONTOSONSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_AllowInternetOutBound","flows":[{"mac":"000D3A18077E","flowTuples":["1497646722,10.0.0.4,168.62.32.14,44904,443,T,O,A","1497646722,10.0.0.4,52.240.48.24,45218,443,T,O,A","1497646725,10.
0.0.4,168.62.32.14,44910,443,T,O,A","1497646725,10.0.0.4,52.240.48.24,45224,443,T,O,A","1497646728,10.0.0.4,168.62.32.14,44916,443,T,O,A","1497646728,10.0.0.4,52.240.48.24,45230,443,T,O,A","1497646732,10.0.0.4,168.62.32.14,44922,443,T,O,A","14976
46732,10.0.0.4,52.240.48.24,45236,443,T,O,A","1497646735,10.0.0.4,168.62.32.14,44928,443,T,O,A","1497646735,10.0.0.4,52.240.48.24,45242,443,T,O,A","1497646738,10.0.0.4,168.62.32.14,44934,443,T,O,A","1497646738,10.0.0.4,52.240.48.24,45248,443,T,O,
A","1497646742,10.0.0.4,168.62.32.14,44942,443,T,O,A","1497646742,10.0.0.4,52.240.48.24,45256,443,T,O,A","1497646745,10.0.0.4,168.62.32.14,44948,443,T,O,A","1497646745,10.0.0.4,52.240.48.24,45262,443,T,O,A","1497646749,10.0.0.4,168.62.32.14,44954
,443,T,O,A","1497646749,10.0.0.4,52.240.48.24,45268,443,T,O,A","1497646753,10.0.0.4,168.62.32.14,44960,443,T,O,A","1497646753,10.0.0.4,52.240.48.24,45274,443,T,O,A","1497646756,10.0.0.4,168.62.32.14,44966,443,T,O,A","1497646756,10.0.0.4,52.240.48
.24,45280,443,T,O,A","1497646759,10.0.0.4,168.62.32.14,44972,443,T,O,A","1497646759,10.0.0.4,52.240.48.24,45286,443,T,O,A","1497646763,10.0.0.4,168.62.32.14,44978,443,T,O,A","1497646763,10.0.0.4,52.240.48.24,45292,443,T,O,A","1497646766,10.0.0.4,
168.62.32.14,44984,443,T,O,A","1497646766,10.0.0.4,52.240.48.24,45298,443,T,O,A","1497646769,10.0.0.4,168.62.32.14,44990,443,T,O,A","1497646769,10.0.0.4,52.240.48.24,45304,443,T,O,A","1497646773,10.0.0.4,168.62.32.14,44996,443,T,O,A","1497646773,
10.0.0.4,52.240.48.24,45310,443,T,O,A","1497646776,10.0.0.4,168.62.32.14,45002,443,T,O,A","1497646776,10.0.0.4,52.240.48.24,45316,443,T,O,A","1497646779,10.0.0.4,168.62.32.14,45008,443,T,O,A","1497646779,10.0.0.4,52.240.48.24,45322,443,T,O,A"]}]}
,{"rule":"DefaultRule_DenyAllInBound","flows":[]},{"rule":"UserRule_ssh-rule","flows":[]},{"rule":"UserRule_web-rule","flows":[{"mac":"000D3A18077E","flowTuples":["1497646738,13.82.225.93,10.0.0.4,1180,80,T,I,A","1497646750,13.82.225.93,10.0.0.4,
1184,80,T,I,A","1497646768,13.82.225.93,10.0.0.4,1181,80,T,I,A","1497646780,13.82.225.93,10.0.0.4,1336,80,T,I,A"]}]}]}
        }
```

<span data-ttu-id="1a098-134">Этот сценарий является примером направление журналы без необходимости весь журнал целиком hello tooparse tooread записей в NSG.</span><span class="sxs-lookup"><span data-stu-id="1a098-134">This scenario is an example of how tooread entries in NSG flow logs without having tooparse hello entire log.</span></span> <span data-ttu-id="1a098-135">Можно считывать новых записей в журнале hello записываемые с помощью идентификатор блокировки hello или отслеживания длина hello блоков, хранящихся в hello блочного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="1a098-135">You can read new entries in hello log as they are written by using hello block ID or by tracking hello length of blocks stored in hello block blob.</span></span> <span data-ttu-id="1a098-136">Это позволяет tooread только hello новых записей.</span><span class="sxs-lookup"><span data-stu-id="1a098-136">This allows you tooread only hello new entries.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1a098-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a098-137">Next steps</span></span>

<span data-ttu-id="1a098-138">Посетите [визуализировать журналы потока NSG Наблюдатель сети Azure, с помощью средств с открытым исходным кодом](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn Дополнительные сведения о других способах tooview NSG потока журналы.</span><span class="sxs-lookup"><span data-stu-id="1a098-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn more about other ways tooview NSG flow logs.</span></span>

<span data-ttu-id="1a098-139">Дополнительные сведения о больших двоичных объектах хранилища посетите toolearn: [привязки хранилища больших двоичных объектов Azure функции](../azure-functions/functions-bindings-storage-blob.md)</span><span class="sxs-lookup"><span data-stu-id="1a098-139">toolearn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span></span>
