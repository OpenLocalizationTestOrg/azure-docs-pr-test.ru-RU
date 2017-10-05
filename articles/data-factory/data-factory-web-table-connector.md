---
title: "Перемещение данных из веб-таблицы с помощью фабрики данных Azure | Документация Майкрософт"
description: "Узнайте, как перемещать данные из таблицы на веб-странице с помощью фабрики данных Azure."
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
ms.openlocfilehash: 9e006bc7289fa0239f1650ac6ad43dd159e3c7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="6c8ff-103">Перемещение данных из источника веб-таблицы с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="6c8ff-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="6c8ff-104">В этой статье описано, как с помощью действия копирования в фабрике данных Azure переместить данные из таблицы на веб-странице в хранилище данных, поддерживаемое в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span></span> <span data-ttu-id="6c8ff-105">В этой статье в продолжение темы о [действиях перемещения данных](data-factory-data-movement-activities.md) приведены общие сведения о перемещении данных с помощью действия копирования, а также список поддерживаемых хранилищ данных, используемых в качестве источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="6c8ff-106">Сейчас фабрика данных поддерживает только перемещение данных из веб-таблицы в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-106">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c8ff-107">Сейчас этот веб-соединитель поддерживает только извлечение содержимого таблицы из HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="6c8ff-108">Чтобы извлечь данные из конечной точки HTTP (HTTPS), используйте [соединитель HTTP](data-factory-http-connector.md).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-108">To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6c8ff-109">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="6c8ff-109">Getting started</span></span>
<span data-ttu-id="6c8ff-110">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="6c8ff-111">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-111">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="6c8ff-112">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="6c8ff-113">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-113">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6c8ff-114">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6c8ff-115">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6c8ff-115">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="6c8ff-116">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-116">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="6c8ff-117">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-117">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="6c8ff-118">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6c8ff-119">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-119">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6c8ff-120">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="6c8ff-121">Пример определений JSON для сущностей фабрики данных, которые используются для копирования данных из веб-таблицы, доступен в разделе [Пример JSON. Копирование данных из веб-таблицы в большой двоичный объект Azure](#json-example-copy-data-from-web-table-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-121">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="6c8ff-122">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к веб-таблице.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-122">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6c8ff-123">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="6c8ff-123">Linked service properties</span></span>
<span data-ttu-id="6c8ff-124">В приведенной далее таблице содержится описание элементов JSON, которые относятся к связанной веб-службе.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-124">The following table provides description for JSON elements specific to Web linked service.</span></span>

| <span data-ttu-id="6c8ff-125">Свойство</span><span class="sxs-lookup"><span data-stu-id="6c8ff-125">Property</span></span> | <span data-ttu-id="6c8ff-126">Описание</span><span class="sxs-lookup"><span data-stu-id="6c8ff-126">Description</span></span> | <span data-ttu-id="6c8ff-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6c8ff-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c8ff-128">type</span><span class="sxs-lookup"><span data-stu-id="6c8ff-128">type</span></span> |<span data-ttu-id="6c8ff-129">Для свойства type необходимо задать значение **Web**</span><span class="sxs-lookup"><span data-stu-id="6c8ff-129">The type property must be set to: **Web**</span></span> |<span data-ttu-id="6c8ff-130">Да</span><span class="sxs-lookup"><span data-stu-id="6c8ff-130">Yes</span></span> |
| <span data-ttu-id="6c8ff-131">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="6c8ff-131">Url</span></span> |<span data-ttu-id="6c8ff-132">URL-адрес источника Web</span><span class="sxs-lookup"><span data-stu-id="6c8ff-132">URL to the Web source</span></span> |<span data-ttu-id="6c8ff-133">Да</span><span class="sxs-lookup"><span data-stu-id="6c8ff-133">Yes</span></span> |
| <span data-ttu-id="6c8ff-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6c8ff-134">authenticationType</span></span> |<span data-ttu-id="6c8ff-135">Анонимная.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-135">Anonymous.</span></span> |<span data-ttu-id="6c8ff-136">Да</span><span class="sxs-lookup"><span data-stu-id="6c8ff-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="6c8ff-137">Использовать анонимную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="6c8ff-137">Using Anonymous authentication</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="6c8ff-138">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="6c8ff-138">Dataset properties</span></span>
<span data-ttu-id="6c8ff-139">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-139">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6c8ff-140">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6c8ff-141">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-141">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="6c8ff-142">Раздел typeProperties набора данных типа **WebTable** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-142">The typeProperties section for dataset of type **WebTable** has the following properties</span></span>

| <span data-ttu-id="6c8ff-143">Свойство</span><span class="sxs-lookup"><span data-stu-id="6c8ff-143">Property</span></span> | <span data-ttu-id="6c8ff-144">Описание</span><span class="sxs-lookup"><span data-stu-id="6c8ff-144">Description</span></span> | <span data-ttu-id="6c8ff-145">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6c8ff-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6c8ff-146">type</span><span class="sxs-lookup"><span data-stu-id="6c8ff-146">type</span></span> |<span data-ttu-id="6c8ff-147">Тип набора данных.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-147">type of the dataset.</span></span> <span data-ttu-id="6c8ff-148">Необходимо задать значение **WebTable**</span><span class="sxs-lookup"><span data-stu-id="6c8ff-148">must be set to **WebTable**</span></span> |<span data-ttu-id="6c8ff-149">Да</span><span class="sxs-lookup"><span data-stu-id="6c8ff-149">Yes</span></span> |
| <span data-ttu-id="6c8ff-150">path</span><span class="sxs-lookup"><span data-stu-id="6c8ff-150">path</span></span> |<span data-ttu-id="6c8ff-151">Относительный URL-адрес ресурса, который содержит таблицу.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-151">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="6c8ff-152">Нет.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-152">No.</span></span> <span data-ttu-id="6c8ff-153">Если путь не задан, используется только URL-адрес, указанный в определении связанной службы.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-153">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="6c8ff-154">index</span><span class="sxs-lookup"><span data-stu-id="6c8ff-154">index</span></span> |<span data-ttu-id="6c8ff-155">Индекс таблицы в ресурсе.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-155">The index of the table in the resource.</span></span> <span data-ttu-id="6c8ff-156">Дополнительные сведения см. в разделе [Получение индекса таблицы на HTML-странице](#get-index-of-a-table-in-an-html-page).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="6c8ff-157">Да</span><span class="sxs-lookup"><span data-stu-id="6c8ff-157">Yes</span></span> |

<span data-ttu-id="6c8ff-158">**Пример**</span><span class="sxs-lookup"><span data-stu-id="6c8ff-158">**Example:**</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="6c8ff-159">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="6c8ff-159">Copy activity properties</span></span>
<span data-ttu-id="6c8ff-160">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-160">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6c8ff-161">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="6c8ff-162">В свою очередь свойства, доступные в разделе typeProperties действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-162">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="6c8ff-163">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-163">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="6c8ff-164">В настоящее время, если источник в действии копирования относится к типу **WebSource**, дополнительные свойства не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-164">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-to-azure-blob"></a><span data-ttu-id="6c8ff-165">Пример JSON. Копирование данных из веб-таблицы в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="6c8ff-165">JSON example: Copy data from Web table to Azure Blob</span></span>
<span data-ttu-id="6c8ff-166">В примере ниже используется следующее:</span><span class="sxs-lookup"><span data-stu-id="6c8ff-166">The following sample shows:</span></span>

1. <span data-ttu-id="6c8ff-167">Связанная служба типа [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="6c8ff-168">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6c8ff-169">Входной [набор данных](data-factory-create-datasets.md) типа [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="6c8ff-170">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6c8ff-171">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [WebSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6c8ff-172">В этом примере данные из веб-таблицы каждый час копируются в BLOB-объект Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-172">The sample copies data from a Web table to an Azure blob every hour.</span></span> <span data-ttu-id="6c8ff-173">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-173">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="6c8ff-174">В следующем примере показано, как скопировать данные из веб-таблицы в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-174">The following sample shows how to copy data from a Web table to an Azure blob.</span></span> <span data-ttu-id="6c8ff-175">Тем не менее данные можно напрямую копировать в любые приемники, указанные в статье [Действия перемещения данных](data-factory-data-movement-activities.md). Для этого применяется действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-175">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="6c8ff-176">**Связанная веб-служба**. В этом примере используется связанная веб-служба с анонимным доступом.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-176">**Web linked service** This example uses the Web linked service with anonymous authentication.</span></span> <span data-ttu-id="6c8ff-177">Сведения об используемых типах аутентификации см. в разделе [Связанная веб-служба](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="6c8ff-178">**Связанная служба хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="6c8ff-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="6c8ff-179">**Входной набор данных WebTable**. Если для параметра **external** задать значение **true**, то фабрика данных воспримет этот набор данных как внешний, не созданный в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-179">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="6c8ff-180">Дополнительные сведения см. в разделе [Получение индекса таблицы на HTML-странице](#get-index-of-a-table-in-an-html-page).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span>  
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


<span data-ttu-id="6c8ff-181">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="6c8ff-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="6c8ff-182">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-182">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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



<span data-ttu-id="6c8ff-183">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="6c8ff-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="6c8ff-184">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-184">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="6c8ff-185">В определении конвейера JSON для типа **source** установлено значение **WebSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-185">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="6c8ff-186">Список свойств, поддерживаемых WebSource, см. в разделе [Свойства типа WebSource](#copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-186">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span></span>

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
        "description": "Copy from a Web table to an Azure blob",
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="6c8ff-187">Получение индекса таблицы на HTML-странице</span><span class="sxs-lookup"><span data-stu-id="6c8ff-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="6c8ff-188">Запустите **Excel 2016** и перейдите на вкладку **Данные**.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-188">Launch **Excel 2016** and switch to the **Data** tab.</span></span>  
2. <span data-ttu-id="6c8ff-189">На панели инструментов щелкните **Создать запрос**, выберите **Из других источников** и щелкните **Из Интернета**.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-189">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Меню Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="6c8ff-191">В диалоговом окне **Из Интернета** введите **URL-адрес**, который будет использоваться в JSON связанной службы (например, https://en.wikipedia.org/wiki/), вместе с указанным для набора данных путем (например, AFI%27s_100_Years…100_Movies), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-191">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Диалоговое окно "Из Интернета"](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="6c8ff-193">В этом примере используется URL-адрес https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="6c8ff-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="6c8ff-194">Если отображается диалоговое окно **Доступ к веб-содержимому**, выберите соответствующий **URL-адрес** и **тип аутентификации**, а затем нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-194">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Диалоговое окно "Доступ к веб-содержимому"](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="6c8ff-196">В представлении дерева щелкните элемент **table**, чтобы просмотреть содержимое таблицы, а затем в нижней части экрана нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-196">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Диалоговое окно навигатора](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="6c8ff-198">В окне **Редактор запросов** на панели инструментов нажмите кнопку **Расширенный редактор**.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-198">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![Кнопка "Расширенный редактор"](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="6c8ff-200">В диалоговом окне "Расширенный редактор" число, отображаемое рядом с полем "Источник", является индексом.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-200">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Расширенный редактор — индекс](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="6c8ff-202">Если вы работаете с Excel 2013, используйте [Microsoft Power Query для Excel](https://www.microsoft.com/download/details.aspx?id=39379), чтобы получить индекс.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="6c8ff-203">Дополнительные сведения см. в статье [Подключение к веб-странице](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-203">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="6c8ff-204">Точно так же можно использовать [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-204">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="6c8ff-205">Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в разделе [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6c8ff-205">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6c8ff-206">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="6c8ff-206">Performance and Tuning</span></span>
<span data-ttu-id="6c8ff-207">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="6c8ff-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
