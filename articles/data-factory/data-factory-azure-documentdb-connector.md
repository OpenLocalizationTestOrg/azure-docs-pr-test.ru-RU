---
title: "aaaMove данных из базы данных Azure Cosmos | Документы Microsoft"
description: "Узнайте, как переместить данные в коллекцию Azure Cosmos DB и из нее с помощью фабрики данных Azure"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="94edd-103">Tooand перемещения данных из базы данных Azure Cosmos, с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="94edd-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="94edd-104">В этой статье объясняется, как toouse hello действие копирования в данных toomove фабрики данных Azure из DB Cosmos Azure (DocumentDB API).</span><span class="sxs-lookup"><span data-stu-id="94edd-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="94edd-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="94edd-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="94edd-106">Можно скопировать данные из любого поддерживаемого источника данных хранения Cosmos DB tooAzure или из Azure Cosmos DB tooany поддерживается приемник данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="94edd-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="94edd-107">Список хранилищ данных, поддерживаемые действием копирования hello как источники или приемники см. в разделе hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="94edd-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="94edd-108">Соединитель Azure Cosmos DB поддерживает только API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="94edd-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="94edd-109">toocopy данные в виде-— см. в/из JSON-файлов или другой коллекции Cosmos DB [документов JSON импорта и экспорта](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="94edd-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="94edd-110">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="94edd-110">Getting started</span></span>
<span data-ttu-id="94edd-111">Вы можете создать конвейер с действием копирования, которое перемещает данные из хранилища Azure Cosmos DB или обратно, с помощью различных инструментов и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="94edd-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="94edd-112">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="94edd-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="94edd-113">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="94edd-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="94edd-114">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="94edd-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="94edd-115">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="94edd-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="94edd-116">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="94edd-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="94edd-117">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="94edd-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="94edd-118">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="94edd-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="94edd-119">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="94edd-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="94edd-120">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="94edd-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="94edd-121">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="94edd-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="94edd-122">Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из БД Cosmos. в разделе [JSON примеры](#json-examples) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="94edd-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="94edd-123">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooCosmos DB:</span><span class="sxs-lookup"><span data-stu-id="94edd-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="94edd-124">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="94edd-124">Linked service properties</span></span>
<span data-ttu-id="94edd-125">Привет, в следующей таблице приводится описание tooAzure определенные элементы JSON DB Cosmos связанной службы.</span><span class="sxs-lookup"><span data-stu-id="94edd-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="94edd-126">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="94edd-126">**Property**</span></span> | <span data-ttu-id="94edd-127">**Описание**</span><span class="sxs-lookup"><span data-stu-id="94edd-127">**Description**</span></span> | <span data-ttu-id="94edd-128">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="94edd-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94edd-129">type</span><span class="sxs-lookup"><span data-stu-id="94edd-129">type</span></span> |<span data-ttu-id="94edd-130">свойство типа Hello должно быть присвоено: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="94edd-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="94edd-131">Да</span><span class="sxs-lookup"><span data-stu-id="94edd-131">Yes</span></span> |
| <span data-ttu-id="94edd-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="94edd-132">connectionString</span></span> |<span data-ttu-id="94edd-133">Укажите сведения, необходимые tooconnect tooAzure Cosmos DB, базы данных.</span><span class="sxs-lookup"><span data-stu-id="94edd-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="94edd-134">Да</span><span class="sxs-lookup"><span data-stu-id="94edd-134">Yes</span></span> |

<span data-ttu-id="94edd-135">Пример:</span><span class="sxs-lookup"><span data-stu-id="94edd-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="94edd-136">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="94edd-136">Dataset properties</span></span>
<span data-ttu-id="94edd-137">Полный список разделов и свойства, доступные для определения наборов данных можно найти toohello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="94edd-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="94edd-138">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="94edd-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="94edd-139">раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="94edd-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="94edd-140">Hello typeProperties статьи для набора данных hello типа **DocumentDbCollection** имеет следующие свойства hello.</span><span class="sxs-lookup"><span data-stu-id="94edd-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="94edd-141">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="94edd-141">**Property**</span></span> | <span data-ttu-id="94edd-142">**Описание**</span><span class="sxs-lookup"><span data-stu-id="94edd-142">**Description**</span></span> | <span data-ttu-id="94edd-143">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="94edd-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94edd-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="94edd-144">collectionName</span></span> |<span data-ttu-id="94edd-145">Имя коллекции документов Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="94edd-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="94edd-146">Да</span><span class="sxs-lookup"><span data-stu-id="94edd-146">Yes</span></span> |

<span data-ttu-id="94edd-147">Пример:</span><span class="sxs-lookup"><span data-stu-id="94edd-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="94edd-148">Схема фабрики данных</span><span class="sxs-lookup"><span data-stu-id="94edd-148">Schema by Data Factory</span></span>
<span data-ttu-id="94edd-149">Для хранилищ данных, без схемы, таких как Azure Cosmos DB служба фабрики данных hello выводит схему hello в одном из следующих способов hello:</span><span class="sxs-lookup"><span data-stu-id="94edd-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="94edd-150">При указании hello структуру данных с помощью hello **структуры** свойство в определении набора данных hello, hello служба фабрики данных учитывает эту структуру как hello схемы.</span><span class="sxs-lookup"><span data-stu-id="94edd-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="94edd-151">В этом случае, если строка не содержит значение столбца, ему будет присвоено значение NULL.</span><span class="sxs-lookup"><span data-stu-id="94edd-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="94edd-152">Если не указать hello структуру данных с помощью hello **структуры** свойство в определении набора данных hello, hello служба фабрики данных выводит схему hello, используя первую строку hello в данных hello.</span><span class="sxs-lookup"><span data-stu-id="94edd-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="94edd-153">В этом случае если первая строка hello не содержит полную схему hello, некоторые столбцы будет отсутствовать в результате hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="94edd-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="94edd-154">Таким образом, для источников данных без схемы hello рекомендуется toospecify hello структуру данных с помощью hello **структуры** свойство.</span><span class="sxs-lookup"><span data-stu-id="94edd-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="94edd-155">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="94edd-155">Copy activity properties</span></span>
<span data-ttu-id="94edd-156">Полный список разделов и свойства, доступные для определения действий можно найти toohello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="94edd-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="94edd-157">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="94edd-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="94edd-158">Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.</span><span class="sxs-lookup"><span data-stu-id="94edd-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="94edd-159">Свойства доступны в разделе typeProperties hello hello действий на hello различные другой стороны, для каждого типа действия и в случае действия копирования, они различаются в зависимости от типа hello источники и приемники.</span><span class="sxs-lookup"><span data-stu-id="94edd-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="94edd-160">В случае действия копирования, когда источник типа **DocumentDbCollectionSource** hello следующие свойства доступны в **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="94edd-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="94edd-161">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="94edd-161">**Property**</span></span> | <span data-ttu-id="94edd-162">**Описание**</span><span class="sxs-lookup"><span data-stu-id="94edd-162">**Description**</span></span> | <span data-ttu-id="94edd-163">**Допустимые значения**</span><span class="sxs-lookup"><span data-stu-id="94edd-163">**Allowed values**</span></span> | <span data-ttu-id="94edd-164">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="94edd-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="94edd-165">query</span><span class="sxs-lookup"><span data-stu-id="94edd-165">query</span></span> |<span data-ttu-id="94edd-166">Укажите данные tooread hello запроса.</span><span class="sxs-lookup"><span data-stu-id="94edd-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="94edd-167">Строка запроса, поддерживаемая Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="94edd-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="94edd-168">Пример: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="94edd-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="94edd-169">Нет</span><span class="sxs-lookup"><span data-stu-id="94edd-169">No</span></span> <br/><br/><span data-ttu-id="94edd-170">Если не указан, hello выполняемой инструкции SQL:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="94edd-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="94edd-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="94edd-171">nestingSeparator</span></span> |<span data-ttu-id="94edd-172">Вложенные tooindicate специальный символ, который hello документа</span><span class="sxs-lookup"><span data-stu-id="94edd-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="94edd-173">Любой символ.</span><span class="sxs-lookup"><span data-stu-id="94edd-173">Any character.</span></span> <br/><br/><span data-ttu-id="94edd-174">Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры.</span><span class="sxs-lookup"><span data-stu-id="94edd-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="94edd-175">Фабрика данных Azure позволяет пользовательская иерархия toodenote через nestingSeparator, который является «.»</span><span class="sxs-lookup"><span data-stu-id="94edd-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="94edd-176">в hello выше примерах.</span><span class="sxs-lookup"><span data-stu-id="94edd-176">in hello above examples.</span></span> <span data-ttu-id="94edd-177">Разделитель hello hello действие копирования будет создавать объект «Name» hello с тремя дочерние элементы первой, средней и Last, соответствующим too"Name.First», «Name.Middle» и «Name.Last» в hello определение таблицы.</span><span class="sxs-lookup"><span data-stu-id="94edd-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="94edd-178">Нет</span><span class="sxs-lookup"><span data-stu-id="94edd-178">No</span></span> |

<span data-ttu-id="94edd-179">**DocumentDbCollectionSink** поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="94edd-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="94edd-180">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="94edd-180">**Property**</span></span> | <span data-ttu-id="94edd-181">**Описание**</span><span class="sxs-lookup"><span data-stu-id="94edd-181">**Description**</span></span> | <span data-ttu-id="94edd-182">**Допустимые значения**</span><span class="sxs-lookup"><span data-stu-id="94edd-182">**Allowed values**</span></span> | <span data-ttu-id="94edd-183">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="94edd-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="94edd-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="94edd-184">nestingSeparator</span></span> |<span data-ttu-id="94edd-185">Требуется специальный символ в tooindicate имя столбца источника hello вложенном документе.</span><span class="sxs-lookup"><span data-stu-id="94edd-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="94edd-186">Пример выше: `Name.First` в выходных данных hello таблицы выводятся hello следующая структура JSON в документе Cosmos DB hello:</span><span class="sxs-lookup"><span data-stu-id="94edd-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="94edd-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="94edd-187">"Name": {</span></span><br/>    <span data-ttu-id="94edd-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="94edd-188">"First": "John"</span></span><br/><span data-ttu-id="94edd-189">},</span><span class="sxs-lookup"><span data-stu-id="94edd-189">},</span></span> |<span data-ttu-id="94edd-190">Символ, используемые tooseparate уровней вложения.</span><span class="sxs-lookup"><span data-stu-id="94edd-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="94edd-191">Значение по умолчанию — `.` (точка).</span><span class="sxs-lookup"><span data-stu-id="94edd-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="94edd-192">Символ, используемые tooseparate уровней вложения.</span><span class="sxs-lookup"><span data-stu-id="94edd-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="94edd-193">Значение по умолчанию — `.` (точка).</span><span class="sxs-lookup"><span data-stu-id="94edd-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="94edd-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="94edd-194">writeBatchSize</span></span> |<span data-ttu-id="94edd-195">Число используемых параллельных запросов документов toocreate tooAzure Cosmos DB службы.</span><span class="sxs-lookup"><span data-stu-id="94edd-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="94edd-196">Можно оптимизировать производительность hello, при копировании данных из базы данных Cosmos при помощи этого свойства.</span><span class="sxs-lookup"><span data-stu-id="94edd-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="94edd-197">При увеличении writeBatchSize, так как несколько параллельных запросов tooCosmos DB отправляются можно ожидать более высокую производительность.</span><span class="sxs-lookup"><span data-stu-id="94edd-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="94edd-198">Тем не менее необходимо tooavoid регулирования, может вызывать ошибки приветственное сообщение: «частота велик» запроса.</span><span class="sxs-lookup"><span data-stu-id="94edd-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="94edd-199">Регулирование может произойти по ряду причин, включая размер документов, количество терминов в документах, политику индексации целевой коллекции и т. д. Для операций копирования, можно использовать доступной пропускной способностью большинство лучше hello toohave коллекции (например S3) (2 500 запрос единицы в секунду).</span><span class="sxs-lookup"><span data-stu-id="94edd-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="94edd-200">Целое число </span><span class="sxs-lookup"><span data-stu-id="94edd-200">Integer</span></span> |<span data-ttu-id="94edd-201">Нет (значение по умолчанию — 5)</span><span class="sxs-lookup"><span data-stu-id="94edd-201">No (default: 5)</span></span> |
| <span data-ttu-id="94edd-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="94edd-202">writeBatchTimeout</span></span> |<span data-ttu-id="94edd-203">Время ожидания для операции toocomplete hello до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="94edd-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="94edd-204">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="94edd-204">timespan</span></span><br/><br/> <span data-ttu-id="94edd-205">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="94edd-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="94edd-206">Нет</span><span class="sxs-lookup"><span data-stu-id="94edd-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="94edd-207">Документы JSON для импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="94edd-207">Import/Export JSON documents</span></span>
<span data-ttu-id="94edd-208">С помощью этого соединителя Cosmos DB можно выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="94edd-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="94edd-209">импортировать документы JSON из различных источников в Cosmos DB, включая хранилище BLOB-объектов Azure, Azure Data Lake, локальную файловую систему или другие файловые хранилища, поддерживаемые фабрикой данных Azure;</span><span class="sxs-lookup"><span data-stu-id="94edd-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="94edd-210">экспортировать документы JSON из коллекции Cosmos DB в различные файловые хранилища;</span><span class="sxs-lookup"><span data-stu-id="94edd-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="94edd-211">переносить данные между коллекциями Cosmos DB "как есть".</span><span class="sxs-lookup"><span data-stu-id="94edd-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="94edd-212">tooachieve скопировать такие независимо от схемы,</span><span class="sxs-lookup"><span data-stu-id="94edd-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="94edd-213">При использовании мастера копирования, проверьте hello **«экспортировать как-файлы tooJSON или Cosmos DB коллекции «** параметр.</span><span class="sxs-lookup"><span data-stu-id="94edd-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="94edd-214">Когда редактирования JSON, не указывают раздел «структура» hello в наборах данных Cosmos DB ни свойство «nestingSeparator» на Cosmos DB источника и приемника в действии копирования.</span><span class="sxs-lookup"><span data-stu-id="94edd-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="94edd-215">tooimport из / tooJSON файлы экспорта в наборе hello файла хранилища данных укажите тип формата как «JsonFormat», конфигурации «filePattern» и пропустить hello настроек формата rest, см. [формат JSON](data-factory-supported-file-and-compression-formats.md#json-format) раздела подробно.</span><span class="sxs-lookup"><span data-stu-id="94edd-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="94edd-216">Примеры определений JSON</span><span class="sxs-lookup"><span data-stu-id="94edd-216">JSON examples</span></span>
<span data-ttu-id="94edd-217">Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="94edd-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="94edd-218">Они показывают как toocopy tooand данных из базы данных Cosmos Azure и хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="94edd-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="94edd-219">Тем не менее, данные можно скопировать **непосредственно** из любого tooany источников hello приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="94edd-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="94edd-220">Пример: Копирование данных из tooAzure Azure Cosmos DB BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="94edd-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="94edd-221">Hello ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="94edd-221">hello sample below shows:</span></span>

1. <span data-ttu-id="94edd-222">Связанная служба типа [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="94edd-223">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="94edd-224">Входной [набор данных](data-factory-create-datasets.md) типа [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="94edd-225">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="94edd-226">Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [DocumentDbCollectionSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="94edd-227">Образец Hello копирования данных в Azure Cosmos DB tooAzure больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="94edd-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="94edd-228">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="94edd-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="94edd-229">**Связанная служба Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="94edd-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="94edd-230">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="94edd-230">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="94edd-231">**Входной набор данных Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="94edd-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="94edd-232">Образец Hello предполагается, что имеется коллекция с именем **лицо** в базе данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="94edd-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="94edd-233">Параметр «external»: «true», и указание externalData сведения о политике hello фабрики данных Azure службы этой таблицы hello является внешней toohello фабрики данных и не полученные в результате действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="94edd-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="94edd-234">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="94edd-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="94edd-235">Данные — новый большой двоичный объект скопированный tooa каждый час с hello путь для большого двоичного объекта hello отражения hello определенной даты и времени с гранулярностью час.</span><span class="sxs-lookup"><span data-stu-id="94edd-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="94edd-236">Пример документа JSON в коллекции пользователя в базе данных Cosmos DB hello:</span><span class="sxs-lookup"><span data-stu-id="94edd-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="94edd-237">Служба Cosmos DB поддерживает выполнение запросов к документам, используя для обработки иерархических JSON-документов синтаксис наподобие SQL.</span><span class="sxs-lookup"><span data-stu-id="94edd-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="94edd-238">Пример:</span><span class="sxs-lookup"><span data-stu-id="94edd-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="94edd-239">следующие Hello конвейера копирует данные из hello коллекции человека в hello tooan базы данных Azure Cosmos DB BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="94edd-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="94edd-240">Как часть hello действия копирования hello указаны входные и выходные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="94edd-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="94edd-241">Пример: Копирование данных из больших двоичных объектов Azure tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="94edd-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="94edd-242">Hello ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="94edd-242">hello sample below shows:</span></span>

1. <span data-ttu-id="94edd-243">Связанная служба типа [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="94edd-244">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="94edd-245">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="94edd-246">Выходной [набор данных](data-factory-create-datasets.md) типа [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="94edd-247">Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="94edd-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="94edd-248">Образец Hello копирует данные из BLOB-объектов Azure tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="94edd-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="94edd-249">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="94edd-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="94edd-250">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="94edd-250">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="94edd-251">**Связанная служба Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="94edd-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="94edd-252">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="94edd-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="94edd-253">**Выходной набор данных Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="94edd-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="94edd-254">Образец Hello копирует tooa сбора данных, с именем «Person».</span><span class="sxs-lookup"><span data-stu-id="94edd-254">hello sample copies data tooa collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="94edd-255">следующие Hello конвейера копирует данные из BLOB-объектов Azure toohello коллекции человека в hello Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="94edd-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="94edd-256">Как часть hello действия копирования hello указаны входные и выходные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="94edd-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="94edd-257">Если входные данные большого двоичного объекта образец hello как</span><span class="sxs-lookup"><span data-stu-id="94edd-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="94edd-258">Затем hello выходных данных JSON в Cosmos DB будет как:</span><span class="sxs-lookup"><span data-stu-id="94edd-258">Then hello output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="94edd-259">Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры.</span><span class="sxs-lookup"><span data-stu-id="94edd-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="94edd-260">Фабрика данных Azure позволяет пользовательская иерархия toodenote через **nestingSeparator**, который является «.»</span><span class="sxs-lookup"><span data-stu-id="94edd-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="94edd-261">которым в этом примере является точка.</span><span class="sxs-lookup"><span data-stu-id="94edd-261">in this example.</span></span> <span data-ttu-id="94edd-262">Разделитель hello hello действие копирования будет создавать объект «Name» hello с тремя дочерние элементы первой, средней и Last, соответствующим too"Name.First», «Name.Middle» и «Name.Last» в hello определение таблицы.</span><span class="sxs-lookup"><span data-stu-id="94edd-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="94edd-263">Приложение</span><span class="sxs-lookup"><span data-stu-id="94edd-263">Appendix</span></span>
1. <span data-ttu-id="94edd-264">**Вопрос:** hello действие копирования поддержки обновления существующих записей?</span><span class="sxs-lookup"><span data-stu-id="94edd-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="94edd-265">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="94edd-265">**Answer:** No.</span></span>
2. <span data-ttu-id="94edd-266">**Вопрос:** как работает при повторной попытке копирования tooAzure Cosmos DB приходится иметь дело с уже скопированы записей?</span><span class="sxs-lookup"><span data-stu-id="94edd-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="94edd-267">**Ответ:** Если записей имеет поля «Идентификатор», и операция копирования hello пытается tooinsert запись с hello таким же Идентификатором операции копирования hello выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="94edd-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="94edd-268">**Вопрос.** Поддерживает ли фабрика данных [секционирование данных по диапазонам или хэш-секционирование](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="94edd-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="94edd-269">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="94edd-269">**Answer:** No.</span></span>
4. <span data-ttu-id="94edd-270">**Вопрос.** Можно ли указать больше одной коллекции Azure Cosmos DB для таблицы?</span><span class="sxs-lookup"><span data-stu-id="94edd-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="94edd-271">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="94edd-271">**Answer:** No.</span></span> <span data-ttu-id="94edd-272">Сейчас можно указать только одну коллекцию.</span><span class="sxs-lookup"><span data-stu-id="94edd-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="94edd-273">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="94edd-273">Performance and Tuning</span></span>
<span data-ttu-id="94edd-274">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="94edd-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
