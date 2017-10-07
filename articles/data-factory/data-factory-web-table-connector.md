---
title: "aaaMove данные из веб-таблицы, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из таблицы на веб-страницу с использованием фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="fadcc-103">Перемещение данных из источника веб-таблицы с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="fadcc-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="fadcc-104">В этой статье рассматриваются как hello toouse действие копирования фабрики данных Azure toomove данных из таблицы в tooa веб-страницы поддерживается приемника хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="fadcc-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="fadcc-105">Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, дан обзор перемещения данных на копии действия и hello список хранилищ данных, поддерживаемые в качестве источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="fadcc-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="fadcc-106">Фабрика данных в настоящее время поддерживает только хранит перемещение данных из веб-tooother данных таблицы, но не перемещения данных из других данных хранит целевую таблицу tooa Web.</span><span class="sxs-lookup"><span data-stu-id="fadcc-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fadcc-107">Сейчас этот веб-соединитель поддерживает только извлечение содержимого таблицы из HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="fadcc-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="fadcc-108">использовать tooretrieve данные из конечной точки HTTP/s [соединителя HTTP](data-factory-http-connector.md) вместо него.</span><span class="sxs-lookup"><span data-stu-id="fadcc-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fadcc-109">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="fadcc-109">Getting started</span></span>
<span data-ttu-id="fadcc-110">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="fadcc-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="fadcc-111">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="fadcc-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="fadcc-112">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="fadcc-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="fadcc-113">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="fadcc-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fadcc-114">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="fadcc-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fadcc-115">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="fadcc-116">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fadcc-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="fadcc-117">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="fadcc-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="fadcc-118">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="fadcc-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="fadcc-119">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="fadcc-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="fadcc-120">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fadcc-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="fadcc-121">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из веб-таблица, в разделе [пример JSON: копирование данных из таблицы Web tooAzure большого двоичного объекта](#json-example-copy-data-from-web-table-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="fadcc-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="fadcc-122">Привет, в следующих разделах содержат сведения о JSON свойства, которые являются таблицы используется toodefine фабрики данных сущностей определенного tooa Web:</span><span class="sxs-lookup"><span data-stu-id="fadcc-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fadcc-123">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="fadcc-123">Linked service properties</span></span>
<span data-ttu-id="fadcc-124">Hello в следующей таблице приводится описание службы конкретных tooWeb связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="fadcc-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="fadcc-125">Свойство</span><span class="sxs-lookup"><span data-stu-id="fadcc-125">Property</span></span> | <span data-ttu-id="fadcc-126">Описание</span><span class="sxs-lookup"><span data-stu-id="fadcc-126">Description</span></span> | <span data-ttu-id="fadcc-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fadcc-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fadcc-128">type</span><span class="sxs-lookup"><span data-stu-id="fadcc-128">type</span></span> |<span data-ttu-id="fadcc-129">свойство типа Hello должно быть присвоено: **Web**</span><span class="sxs-lookup"><span data-stu-id="fadcc-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="fadcc-130">Да</span><span class="sxs-lookup"><span data-stu-id="fadcc-130">Yes</span></span> |
| <span data-ttu-id="fadcc-131">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="fadcc-131">Url</span></span> |<span data-ttu-id="fadcc-132">URL-адрес toohello веб-источнику</span><span class="sxs-lookup"><span data-stu-id="fadcc-132">URL toohello Web source</span></span> |<span data-ttu-id="fadcc-133">Да</span><span class="sxs-lookup"><span data-stu-id="fadcc-133">Yes</span></span> |
| <span data-ttu-id="fadcc-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fadcc-134">authenticationType</span></span> |<span data-ttu-id="fadcc-135">Анонимная.</span><span class="sxs-lookup"><span data-stu-id="fadcc-135">Anonymous.</span></span> |<span data-ttu-id="fadcc-136">Да</span><span class="sxs-lookup"><span data-stu-id="fadcc-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="fadcc-137">Использовать анонимную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="fadcc-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="fadcc-138">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="fadcc-138">Dataset properties</span></span>
<span data-ttu-id="fadcc-139">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="fadcc-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fadcc-140">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="fadcc-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fadcc-141">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="fadcc-142">Hello typeProperties статьи для набора данных типа **таблицы WebTable** имеет следующие свойства hello</span><span class="sxs-lookup"><span data-stu-id="fadcc-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="fadcc-143">Свойство</span><span class="sxs-lookup"><span data-stu-id="fadcc-143">Property</span></span> | <span data-ttu-id="fadcc-144">Описание</span><span class="sxs-lookup"><span data-stu-id="fadcc-144">Description</span></span> | <span data-ttu-id="fadcc-145">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fadcc-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fadcc-146">type</span><span class="sxs-lookup"><span data-stu-id="fadcc-146">type</span></span> |<span data-ttu-id="fadcc-147">Тип набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-147">type of hello dataset.</span></span> <span data-ttu-id="fadcc-148">необходимо задать слишком**таблицы WebTable**</span><span class="sxs-lookup"><span data-stu-id="fadcc-148">must be set too**WebTable**</span></span> |<span data-ttu-id="fadcc-149">Да</span><span class="sxs-lookup"><span data-stu-id="fadcc-149">Yes</span></span> |
| <span data-ttu-id="fadcc-150">path</span><span class="sxs-lookup"><span data-stu-id="fadcc-150">path</span></span> |<span data-ttu-id="fadcc-151">Относительный URL-адрес ресурса toohello, содержащей таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="fadcc-152">Нет.</span><span class="sxs-lookup"><span data-stu-id="fadcc-152">No.</span></span> <span data-ttu-id="fadcc-153">Если путь не указан, используется только hello URL-адрес, указанный в определении службы hello связаны.</span><span class="sxs-lookup"><span data-stu-id="fadcc-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="fadcc-154">index</span><span class="sxs-lookup"><span data-stu-id="fadcc-154">index</span></span> |<span data-ttu-id="fadcc-155">Индекс таблицы hello в ресурсе hello Hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="fadcc-156">В разделе [Get индекс таблицы в HTML-страницу](#get-index-of-a-table-in-an-html-page) раздел для действия toogetting индекса таблицы в HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="fadcc-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="fadcc-157">Да</span><span class="sxs-lookup"><span data-stu-id="fadcc-157">Yes</span></span> |

<span data-ttu-id="fadcc-158">**Пример**</span><span class="sxs-lookup"><span data-stu-id="fadcc-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="fadcc-159">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="fadcc-159">Copy activity properties</span></span>
<span data-ttu-id="fadcc-160">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="fadcc-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fadcc-161">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="fadcc-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="fadcc-162">В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="fadcc-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="fadcc-163">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="fadcc-164">В настоящее время, если источник hello в действии копирования имеет тип **WebSource**, дополнительных свойств не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="fadcc-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="fadcc-165">Пример JSON: копирование данных из таблицы Web tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="fadcc-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="fadcc-166">Hello следующем образце показано:</span><span class="sxs-lookup"><span data-stu-id="fadcc-166">hello following sample shows:</span></span>

1. <span data-ttu-id="fadcc-167">Связанная служба типа [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fadcc-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="fadcc-168">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fadcc-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fadcc-169">Входной [набор данных](data-factory-create-datasets.md) типа [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fadcc-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="fadcc-170">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fadcc-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fadcc-171">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [WebSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fadcc-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fadcc-172">Образец Hello копирует данные из tooan таблицы Web BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="fadcc-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="fadcc-173">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="fadcc-174">Следующий образец Hello показано, как данные toocopy из tooan таблицы Web Azure BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="fadcc-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="fadcc-175">Тем не менее, данные можно скопировать непосредственно tooany из hello приемники уже говорилось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fadcc-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="fadcc-176">**Web связанная служба** в этом примере используется hello Web связанная служба с анонимной проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="fadcc-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="fadcc-177">Сведения об используемых типах аутентификации см. в разделе [Связанная веб-служба](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fadcc-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="fadcc-178">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="fadcc-178">**Azure Storage linked service**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="fadcc-179">**Входной набор данных таблицы WebTable** параметр **внешних** слишком**true** информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fadcc-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="fadcc-180">В разделе [Get индекс таблицы в HTML-страницу](#get-index-of-a-table-in-an-html-page) раздел для действия toogetting индекса таблицы в HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="fadcc-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="fadcc-181">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="fadcc-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="fadcc-182">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="fadcc-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="fadcc-183">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="fadcc-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="fadcc-184">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="fadcc-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="fadcc-185">В определении JSON конвейера hello, hello **источника** тип установлен слишком**WebSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fadcc-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="fadcc-186">В разделе [свойства типа WebSource](#copy-activity-type-properties) список свойств, поддерживаемых hello WebSource hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="fadcc-187">Получение индекса таблицы на HTML-странице</span><span class="sxs-lookup"><span data-stu-id="fadcc-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="fadcc-188">Запустите **Excel 2016** и переключения toohello **данные** вкладки.</span><span class="sxs-lookup"><span data-stu-id="fadcc-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="fadcc-189">Нажмите кнопку **новый запрос** на панели инструментов hello, точка слишком**из других источников** и нажмите кнопку **из Интернета**.</span><span class="sxs-lookup"><span data-stu-id="fadcc-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Меню Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="fadcc-191">В hello **из Интернета** диалогового окна введите **URL-адрес** , вы будете использовать в связанной службы JSON (например: https://en.wikipedia.org/wiki/) наряду с указанием пути, следует указать для hello набора данных (например: корпорация AFI % 27s_100_Years... 100_Movies) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fadcc-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Диалоговое окно "Из Интернета"](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="fadcc-193">В этом примере используется URL-адрес https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="fadcc-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="fadcc-194">Если вы видите **веб-доступа к содержимому** диалоговое окно, выберите hello справа **URL-адрес**, **проверки подлинности**и нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="fadcc-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Диалоговое окно "Доступ к веб-содержимому"](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="fadcc-196">Нажмите кнопку **таблицы** в содержимом toosee представление дерева hello из таблицы hello и выберите команду **изменить** кнопку в нижней части hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![Диалоговое окно навигатора](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="fadcc-198">В hello **редактора запросов** окно, нажмите кнопку **расширенный редактор** на инструментов «hello».</span><span class="sxs-lookup"><span data-stu-id="fadcc-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![Кнопка "Расширенный редактор"](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="fadcc-200">В диалоговом окне Расширенный редактор hello, hello номер рядом слишком «Источник» является индекс hello.</span><span class="sxs-lookup"><span data-stu-id="fadcc-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![Расширенный редактор — индекс](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="fadcc-202">Если вы используете Excel 2013, используйте [Microsoft Power Query для Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello индекса.</span><span class="sxs-lookup"><span data-stu-id="fadcc-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="fadcc-203">В разделе [Connect tooa веб-страницы](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="fadcc-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="fadcc-204">Hello шаги похожи, если вы используете [Microsoft Power BI для рабочего стола](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="fadcc-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="fadcc-205">toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fadcc-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fadcc-206">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="fadcc-206">Performance and Tuning</span></span>
<span data-ttu-id="fadcc-207">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="fadcc-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
