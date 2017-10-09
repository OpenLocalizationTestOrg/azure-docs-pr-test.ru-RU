---
title: "пространство имен концентраторов событий Azure и включить записи с помощью шаблона aaaCreate | Документы Microsoft"
description: "Создание пространства имен концентраторов событий Azure с одним концентратором событий и включение записи с помощью шаблона Azure Resource Manager."
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="211bf-103">Создание пространства имен концентраторов событий с концентратором событий и включение записи с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="211bf-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="211bf-104">В этой статье показано, как toouse шаблона диспетчера ресурсов Azure, создает пространство имен концентраторов событий с экземпляра концентратора одно событие, а также включает hello [функция записи](event-hubs-capture-overview.md) в концентраторе событий hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="211bf-105">Hello статье описывается, как toodefine какие ресурсы развертываются с указанием как toodefine параметры, которые при выполнении развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="211bf-106">Этот шаблон используется для собственных развертывания или настройте его toomeet вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="211bf-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="211bf-107">Это статье также указывается как toospecify, что события будут записаны в хранилище BLOB-объектов Azure или хранилища Озера данных Azure, на основании hello выборе назначения.</span><span class="sxs-lookup"><span data-stu-id="211bf-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="211bf-108">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="211bf-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="211bf-109">Дополнительные сведения о шаблонах и рекомендациях по соглашениям об именовании ресурсов Azure см. в статье [Naming conventions][Azure Resources naming conventions] (Соглашения об именовании).</span><span class="sxs-lookup"><span data-stu-id="211bf-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="211bf-110">Для завершения шаблонов hello щелкните hello ссылкам GitHub:</span><span class="sxs-lookup"><span data-stu-id="211bf-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="211bf-111">[Концентратор и включение системы отслеживания tooStorage шаблона события][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="211bf-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="211bf-112">[Концентратор и включение системы отслеживания tooAzure хранилища Озера данных шаблона события][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="211bf-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="211bf-113">toocheck для hello последние шаблоны, посетите hello [шаблоны быстрый запуск Azure] [ Azure Quickstart Templates] коллекции и выполните поиск концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="211bf-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="211bf-114">Что вы развернете?</span><span class="sxs-lookup"><span data-stu-id="211bf-114">What will you deploy?</span></span>

<span data-ttu-id="211bf-115">С помощью этого шаблона вы развернете пространство имен концентраторов событий с концентратором событий и включите [запись концентраторов событий](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="211bf-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="211bf-116">[Концентраторы событий](event-hubs-what-is-event-hubs.md) событие обработки службы, используемой tooprovide событий и телеметрии входящих tooAzure в большом масштабе с небольшой задержкой и высокой степенью надежности.</span><span class="sxs-lookup"><span data-stu-id="211bf-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="211bf-117">События отслеживания концентраторов включает вы tooautomatically доставки hello и потоковой передачи данных в хранилище больших двоичных объектов tooAzure концентраторов событий хранилища Озера данных Azure в течение заданного промежутка времени или интервала размер по своему выбору.</span><span class="sxs-lookup"><span data-stu-id="211bf-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="211bf-118">Щелкните hello, следуя tooenable кнопки захвата концентраторов событий в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="211bf-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="211bf-119">[![Развертывание tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="211bf-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="211bf-120">Щелкните hello, следуя tooenable кнопки захвата концентраторов событий в хранилище Озера данных Azure:</span><span class="sxs-lookup"><span data-stu-id="211bf-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="211bf-121">[![Развертывание tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="211bf-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="211bf-122">Параметры</span><span class="sxs-lookup"><span data-stu-id="211bf-122">Parameters</span></span>

<span data-ttu-id="211bf-123">С помощью диспетчера ресурсов Azure можно определить параметры для значения требуется toospecify при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="211bf-124">шаблон Hello имеется раздел с именем `Parameters` , содержащий значения всех параметров hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="211bf-125">Следует определить параметр для тех значений, которые отличаются на основе hello проекта, в которой выполняется развертывание или на основании hello среды, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="211bf-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="211bf-126">Определяет параметры для hello значения, которые всегда остаются одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="211bf-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="211bf-127">Каждое значение параметра используется в hello шаблона toodefine hello ресурсы, которые развертываются.</span><span class="sxs-lookup"><span data-stu-id="211bf-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="211bf-128">шаблон Hello определяет hello следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="211bf-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="211bf-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="211bf-129">eventHubNamespaceName</span></span>

<span data-ttu-id="211bf-130">Имя Hello hello [имен концентраторов событий](event-hubs-create.md) toocreate.</span><span class="sxs-lookup"><span data-stu-id="211bf-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="211bf-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="211bf-131">eventHubName</span></span>

<span data-ttu-id="211bf-132">Имя Hello hello концентратора событий, созданных в hello [имен концентраторов событий](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="211bf-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="211bf-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="211bf-133">messageRetentionInDays</span></span>

<span data-ttu-id="211bf-134">количество дней tooretain hello сообщений в концентратор событий hello Hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="211bf-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="211bf-135">partitionCount</span></span>

<span data-ttu-id="211bf-136">количество секций toocreate в концентратор событий hello Hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-136">hello number of partitions toocreate in hello event hub.</span></span>

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a><span data-ttu-id="211bf-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="211bf-137">captureEnabled</span></span>

<span data-ttu-id="211bf-138">Включение захвата в концентраторе событий hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-138">Enable Capture on hello event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="211bf-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="211bf-139">captureEncodingFormat</span></span>

<span data-ttu-id="211bf-140">формат кодировки Hello, укажите данные о событии tooserialize hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-140">hello encoding format you specify tooserialize hello event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="211bf-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="211bf-141">captureTime</span></span>

<span data-ttu-id="211bf-142">Hello интервал времени, в котором записи концентраторов событий начинается сбор данных hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="211bf-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="211bf-143">captureSize</span></span>
<span data-ttu-id="211bf-144">Интервал размер приветствия, с которой записи начинается сбор данных hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-144">hello size interval at which Capture starts capturing hello data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="211bf-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="211bf-145">captureNameFormat</span></span>

<span data-ttu-id="211bf-146">формат имени Hello захвата концентраторов событий файлов Avro toowrite hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="211bf-147">Обратите внимание, что в формате имени для функции записи должны быть поля `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, и `{Second}`.</span><span class="sxs-lookup"><span data-stu-id="211bf-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="211bf-148">Они могут быть размещены в любом порядке, с разделителями или без них.</span><span class="sxs-lookup"><span data-stu-id="211bf-148">These can be arranged in any order, with or without delimiters.</span></span>
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a><span data-ttu-id="211bf-149">версия_API</span><span class="sxs-lookup"><span data-stu-id="211bf-149">apiVersion</span></span>

<span data-ttu-id="211bf-150">версия Hello API hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="211bf-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="211bf-151">Используйте следующие параметры при выборе хранилища Azure в качестве места расположения hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="211bf-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="211bf-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="211bf-153">Захват требует tooenable идентификатор ресурса учетной записи хранилища Azure, захват tooyour желаемое учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="211bf-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="211bf-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="211bf-154">blobContainerName</span></span>

<span data-ttu-id="211bf-155">Здравствуйте, контейнер больших двоичных объектов, в которой toocapture данные события.</span><span class="sxs-lookup"><span data-stu-id="211bf-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="211bf-156">Используйте следующие параметры при выборе хранилища Озера данных Azure в качестве места расположения hello.</span><span class="sxs-lookup"><span data-stu-id="211bf-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="211bf-157">Необходимо задать разрешения на путь к хранилищу Озера данных, в котором нужно tooCapture hello события.</span><span class="sxs-lookup"><span data-stu-id="211bf-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="211bf-158">. в разделе разрешения tooset [в этой статье](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="211bf-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="211bf-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="211bf-159">subscriptionId</span></span>

<span data-ttu-id="211bf-160">Идентификатор подписки для пространства имен концентраторов событий hello и хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="211bf-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="211bf-161">Оба эти ресурсы должны быть в группе hello таким же идентификатором подписки.</span><span class="sxs-lookup"><span data-stu-id="211bf-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="211bf-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="211bf-162">dataLakeAccountName</span></span>

<span data-ttu-id="211bf-163">Имя хранилища Озера данных Azure Hello hello записанных событий.</span><span class="sxs-lookup"><span data-stu-id="211bf-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="211bf-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="211bf-164">dataLakeFolderPath</span></span>

<span data-ttu-id="211bf-165">путь к папке назначения Hello для hello записанных событий.</span><span class="sxs-lookup"><span data-stu-id="211bf-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="211bf-166">Toodeploy ресурсы для хранилища Azure, как события toocaptured назначения</span><span class="sxs-lookup"><span data-stu-id="211bf-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="211bf-167">Создает пространство имен типа **EventHubs**, одно событие концентратора и позволяет записать tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="211bf-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="211bf-168">Toodeploy ресурсы для хранилища Озера данных Azure назначения</span><span class="sxs-lookup"><span data-stu-id="211bf-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="211bf-169">Создает пространство имен типа **EventHubs**, одно событие концентратора и включает хранилище Озера данных tooAzure отслеживания.</span><span class="sxs-lookup"><span data-stu-id="211bf-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="211bf-170">Команды toorun развертывания</span><span class="sxs-lookup"><span data-stu-id="211bf-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="211bf-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="211bf-171">PowerShell</span></span>

<span data-ttu-id="211bf-172">Развертывание вашей tooenable шаблона отслеживания концентраторов событий в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="211bf-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="211bf-173">Развертывание вашей tooenable шаблона отслеживания концентраторов событий в хранилище Озера данных Azure:</span><span class="sxs-lookup"><span data-stu-id="211bf-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="211bf-174">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="211bf-174">Azure CLI</span></span>

<span data-ttu-id="211bf-175">Выбор хранилища BLOB-объектов Azure в качестве места назначения:</span><span class="sxs-lookup"><span data-stu-id="211bf-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="211bf-176">Выбор Azure Data Lake Store в качестве места назначения:</span><span class="sxs-lookup"><span data-stu-id="211bf-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="211bf-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="211bf-177">Next steps</span></span>

<span data-ttu-id="211bf-178">Можно также настроить записи концентраторов событий через hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="211bf-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="211bf-179">Дополнительные сведения см. в разделе [включения отслеживания концентраторов событий с помощью портала Azure "hello"](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="211bf-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="211bf-180">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="211bf-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="211bf-181">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="211bf-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="211bf-182">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="211bf-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="211bf-183">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="211bf-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
