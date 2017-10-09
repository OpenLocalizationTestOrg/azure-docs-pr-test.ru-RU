---
title: "aaaMove данные из таблиц Azure | Документы Microsoft"
description: "Узнайте, как toomove данных из табличного хранилища Azure, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="6ab6c-103">Tooand перемещения данных из таблицы Azure, с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="6ab6c-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="6ab6c-104">В этой статье объясняется, как toouse hello действие копирования в фабрике данных Azure toomove данных из табличного хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="6ab6c-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="6ab6c-106">Можно скопировать данные из любого поддерживаемого источника данных хранения tooAzure хранилище таблиц или из табличного хранилища Azure поддерживается tooany приемник данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="6ab6c-107">Список хранилищ данных, поддерживаемые действием копирования hello как источники или приемники см. в разделе hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="6ab6c-108">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="6ab6c-108">Getting started</span></span>
<span data-ttu-id="6ab6c-109">Вы можете создать конвейер с действием копирования, который перемещает данные в хранилище таблиц Azure или из него, с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="6ab6c-110">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6ab6c-111">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="6ab6c-112">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6ab6c-113">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6ab6c-114">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="6ab6c-115">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="6ab6c-116">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="6ab6c-117">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6ab6c-118">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6ab6c-119">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6ab6c-120">Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из таблицы хранилища Azure см. в разделе [JSON примеры](#json-examples) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="6ab6c-121">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAzure хранилище таблиц:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="6ab6c-122">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="6ab6c-122">Linked service properties</span></span>
<span data-ttu-id="6ab6c-123">Существует два типа связанных служб можно использовать toolink фабрикой данных Azure tooan хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="6ab6c-124">**AzureStorage** и **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="6ab6c-125">Hello связанной службой хранилища Azure обеспечивает для фабрики данных hello с toohello глобальный доступ к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="6ab6c-126">В то время как связанные hello SAS хранилища Azure (подпись общего доступа) службы обеспечивает для фабрики данных hello с toohello ограничен или ограниченным временем доступа хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="6ab6c-127">Других различий между этими связанными службами нет.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="6ab6c-128">Выберите службу hello связаны, которая соответствует вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="6ab6c-129">Hello следующие подразделы содержат дополнительные сведения в этих двух связанных служб.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="6ab6c-130">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="6ab6c-130">Dataset properties</span></span>
<span data-ttu-id="6ab6c-131">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6ab6c-132">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6ab6c-133">раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="6ab6c-134">Hello **typeProperties** раздел для набора данных hello типа **AzureTable** имеет следующие свойства hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="6ab6c-135">Свойство</span><span class="sxs-lookup"><span data-stu-id="6ab6c-135">Property</span></span> | <span data-ttu-id="6ab6c-136">Описание</span><span class="sxs-lookup"><span data-stu-id="6ab6c-136">Description</span></span> | <span data-ttu-id="6ab6c-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6ab6c-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ab6c-138">tableName</span><span class="sxs-lookup"><span data-stu-id="6ab6c-138">tableName</span></span> |<span data-ttu-id="6ab6c-139">Имя таблицы hello в экземпляре базы данных таблицы Azure hello, что связанная служба ссылается.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="6ab6c-140">Да.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-140">Yes.</span></span> <span data-ttu-id="6ab6c-141">При tableName указан без azureTableSourceQuery, все записи из таблицы hello не копируются toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="6ab6c-142">Если также указан azureTableSourceQuery записи из таблицы hello, удовлетворяющий hello запроса являются скопированный toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="6ab6c-143">Схема фабрики данных</span><span class="sxs-lookup"><span data-stu-id="6ab6c-143">Schema by Data Factory</span></span>
<span data-ttu-id="6ab6c-144">Для хранилищ данных, без схемы, таких как таблицы Azure служба фабрики данных hello выводит схему hello в одном из следующих способов hello:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="6ab6c-145">При указании hello структуру данных с помощью hello **структуры** свойство в определении набора данных hello, hello служба фабрики данных учитывает эту структуру как hello схемы.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="6ab6c-146">В этом случае, если строка не содержит значение столбца, ему присваивается значение NULL.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="6ab6c-147">Если не указать hello структуру данных с помощью hello **структуры** свойство в определении набора данных hello, фабрики данных выводит схему hello, используя первую строку hello в данных hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="6ab6c-148">В этом случае если первая строка hello не содержит полную схему hello, в результате операции копирования hello пропущены некоторые столбцы.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="6ab6c-149">Таким образом, для источников данных без схемы hello рекомендуется toospecify hello структуру данных с помощью hello **структуры** свойство.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="6ab6c-150">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="6ab6c-150">Copy activity properties</span></span>
<span data-ttu-id="6ab6c-151">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6ab6c-152">Свойства, например имя, описание, входные и выходные таблицы, политики и т. д., доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="6ab6c-153">Свойства доступны в разделе typeProperties hello hello действий на hello другой стороны, могут различаться для каждого типа действия.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="6ab6c-154">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="6ab6c-155">**AzureTableSource** поддерживает следующие свойства в разделе "typeProperties" hello:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="6ab6c-156">Свойство</span><span class="sxs-lookup"><span data-stu-id="6ab6c-156">Property</span></span> | <span data-ttu-id="6ab6c-157">Описание</span><span class="sxs-lookup"><span data-stu-id="6ab6c-157">Description</span></span> | <span data-ttu-id="6ab6c-158">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="6ab6c-158">Allowed values</span></span> | <span data-ttu-id="6ab6c-159">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6ab6c-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ab6c-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="6ab6c-160">azureTableSourceQuery</span></span> |<span data-ttu-id="6ab6c-161">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="6ab6c-162">Строка запроса таблицы Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-162">Azure table query string.</span></span> <span data-ttu-id="6ab6c-163">Примеры в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-163">See examples in hello next section.</span></span> |<span data-ttu-id="6ab6c-164">Нет.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-164">No.</span></span> <span data-ttu-id="6ab6c-165">При tableName указан без azureTableSourceQuery, все записи из таблицы hello не копируются toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="6ab6c-166">Если также указан azureTableSourceQuery записи из таблицы hello, удовлетворяющий hello запроса являются скопированный toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="6ab6c-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="6ab6c-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="6ab6c-168">Указывают ли проглотить исключение hello таблицы не существует.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="6ab6c-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="6ab6c-169">TRUE</span></span><br/><span data-ttu-id="6ab6c-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="6ab6c-170">FALSE</span></span> |<span data-ttu-id="6ab6c-171">Нет</span><span class="sxs-lookup"><span data-stu-id="6ab6c-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="6ab6c-172">Примеры azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="6ab6c-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="6ab6c-173">Если столбец таблицы Azure имеет тип строки:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="6ab6c-174">Если столбец таблицы Azure имеет тип даты и времени:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="6ab6c-175">**AzureTableSink** поддерживает следующие свойства в разделе "typeProperties" hello:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="6ab6c-176">Свойство</span><span class="sxs-lookup"><span data-stu-id="6ab6c-176">Property</span></span> | <span data-ttu-id="6ab6c-177">Описание</span><span class="sxs-lookup"><span data-stu-id="6ab6c-177">Description</span></span> | <span data-ttu-id="6ab6c-178">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="6ab6c-178">Allowed values</span></span> | <span data-ttu-id="6ab6c-179">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6ab6c-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ab6c-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="6ab6c-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="6ab6c-181">Значение по умолчанию раздел ключа, может использоваться приемником hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="6ab6c-182">Строковое значение.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-182">A string value.</span></span> |<span data-ttu-id="6ab6c-183">Нет</span><span class="sxs-lookup"><span data-stu-id="6ab6c-183">No</span></span> |
| <span data-ttu-id="6ab6c-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="6ab6c-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="6ab6c-185">Укажите имя столбца hello, значения которых используются в качестве ключей секционирования.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="6ab6c-186">Если не указано, в качестве ключа секции hello используется AzureTableDefaultPartitionKeyValue.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="6ab6c-187">Имя столбца.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-187">A column name.</span></span> |<span data-ttu-id="6ab6c-188">Нет</span><span class="sxs-lookup"><span data-stu-id="6ab6c-188">No</span></span> |
| <span data-ttu-id="6ab6c-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="6ab6c-189">azureTableRowKeyName</span></span> |<span data-ttu-id="6ab6c-190">Укажите имя столбца hello, значение которого используются в качестве ключа строки.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="6ab6c-191">Если имя не указано, используйте для каждой строки идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="6ab6c-192">Имя столбца.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-192">A column name.</span></span> |<span data-ttu-id="6ab6c-193">Нет</span><span class="sxs-lookup"><span data-stu-id="6ab6c-193">No</span></span> |
| <span data-ttu-id="6ab6c-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="6ab6c-194">azureTableInsertType</span></span> |<span data-ttu-id="6ab6c-195">режим Hello tooinsert данные в таблицу Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="6ab6c-196">Это свойство определяет, имеют ли существующие строки в выходной диапазон hello соответствующие ключи секций и строк значениями заменить или слияние.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="6ab6c-197">toolearn о работе этих параметров (слияния и замены) в разделе [Вставка или слияние сущности](https://msdn.microsoft.com/library/azure/hh452241.aspx) и [Вставка или замена сущности](https://msdn.microsoft.com/library/azure/hh452242.aspx) разделы.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="6ab6c-198">Этот параметр применяется на уровне строк hello, не уровне hello таблицы и ни один из параметров удаляются строки в таблице вывода hello, которые не существуют во входном файле hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="6ab6c-199">merge (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="6ab6c-199">merge (default)</span></span><br/><span data-ttu-id="6ab6c-200">replace</span><span class="sxs-lookup"><span data-stu-id="6ab6c-200">replace</span></span> |<span data-ttu-id="6ab6c-201">Нет</span><span class="sxs-lookup"><span data-stu-id="6ab6c-201">No</span></span> |
| <span data-ttu-id="6ab6c-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6ab6c-202">writeBatchSize</span></span> |<span data-ttu-id="6ab6c-203">Вставляет данные в таблицу Azure hello при hello writeBatchSize или writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="6ab6c-204">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="6ab6c-204">Integer (number of rows)</span></span> |<span data-ttu-id="6ab6c-205">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-205">No (default: 10000)</span></span> |
| <span data-ttu-id="6ab6c-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6ab6c-206">writeBatchTimeout</span></span> |<span data-ttu-id="6ab6c-207">Вставляет данные в таблицу Azure hello при hello writeBatchSize или writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6ab6c-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="6ab6c-208">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="6ab6c-208">timespan</span></span><br/><br/><span data-ttu-id="6ab6c-209">Пример: 00:20:00 (20 минут).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="6ab6c-210">Нет (время ожидания по умолчанию клиент toostorage по умолчанию значение составляет 90 сек)</span><span class="sxs-lookup"><span data-stu-id="6ab6c-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="6ab6c-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="6ab6c-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="6ab6c-212">Сопоставьте исходный столбец tooa целевой столбец с помощью свойства JSON переводчик hello, прежде чем использовать hello целевой столбец как hello azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="6ab6c-213">В следующем примере hello, исходный столбец DivisionID имеет сопоставленных toohello целевого столбца: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="6ab6c-214">Hello DivisionID указывается в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="6ab6c-215">Примеры определений JSON</span><span class="sxs-lookup"><span data-stu-id="6ab6c-215">JSON examples</span></span>
<span data-ttu-id="6ab6c-216">Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6ab6c-217">Они показывают как toocopy tooand данных из табличного хранилища Azure и базы данных больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="6ab6c-218">Тем не менее, данные можно скопировать **непосредственно** из любого tooany источников hello приемников hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="6ab6c-219">Дополнительные сведения см. в разделе hello раздел «поддерживаемые хранилищ данных и форматы» в [перемещения данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="6ab6c-220">Пример: Копирование данных из таблиц Azure tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="6ab6c-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="6ab6c-221">Hello следующем образце показано:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-221">hello following sample shows:</span></span>

1. <span data-ttu-id="6ab6c-222">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (используется для таблиц и больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="6ab6c-223">Входной [набор данных](data-factory-create-datasets.md) типа [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="6ab6c-224">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6ab6c-225">Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [AzureTableSource](#activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6ab6c-226">Образец Hello копирует данные, принадлежащие секции по умолчанию toohello в большом двоичном объекте tooa таблиц Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="6ab6c-227">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6ab6c-228">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="6ab6c-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="6ab6c-229">Фабрика данных Azure поддерживает два типа связанных служб хранилища Azure: **AzureStorage** и **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="6ab6c-230">Для hello первый, укажите строку подключения hello, содержащую ключ учетной записи hello и для hello позже у одного укажите hello Uri подписи общего доступа (SAS).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="6ab6c-231">Дополнительные сведения см. в разделе [Связанные службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="6ab6c-232">**Входной набор данных таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="6ab6c-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="6ab6c-233">Образец Hello предполагается, что вы создали таблицу «MyTable» в таблице Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="6ab6c-234">Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="6ab6c-235">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="6ab6c-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6ab6c-236">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6ab6c-237">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6ab6c-238">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="6ab6c-239">**Действие копирования в конвейере с источником AzureTableSource и приемником BlobSink**</span><span class="sxs-lookup"><span data-stu-id="6ab6c-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="6ab6c-240">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6ab6c-241">В определении JSON конвейера hello, hello **источника** тип установлен слишком**AzureTableSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="6ab6c-242">запрос SQL Hello, указанный с **AzureTableSourceQuery** свойство выбирает hello данные из секции по умолчанию hello toocopy каждый час.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="6ab6c-243">Пример: Копирование данных из больших двоичных объектов Azure tooAzure таблицы</span><span class="sxs-lookup"><span data-stu-id="6ab6c-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="6ab6c-244">Hello следующем образце показано:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-244">hello following sample shows:</span></span>

1. <span data-ttu-id="6ab6c-245">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (используется для таблиц и больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="6ab6c-246">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="6ab6c-247">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="6ab6c-248">Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="6ab6c-249">Образец Hello копирует временных рядов данных из больших двоичных объектов Azure tooan таблицы Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="6ab6c-250">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6ab6c-251">**Связанная служба хранилища Azure (для таблиц и больших двоичных объектов Azure)**:</span><span class="sxs-lookup"><span data-stu-id="6ab6c-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="6ab6c-252">Фабрика данных Azure поддерживает два типа связанных служб хранилища Azure: **AzureStorage** и **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="6ab6c-253">Для hello первый, укажите строку подключения hello, содержащую ключ учетной записи hello и для hello позже у одного укажите hello Uri подписи общего доступа (SAS).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="6ab6c-254">Дополнительные сведения см. в разделе [Связанные службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="6ab6c-255">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="6ab6c-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="6ab6c-256">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6ab6c-257">Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6ab6c-258">путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="6ab6c-259">«external»: параметр «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="6ab6c-260">**Выходной набор данных таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="6ab6c-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="6ab6c-261">Образец Hello копирует tooa таблицу данных, с именем «MyTable» в таблице Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="6ab6c-262">Создание таблицы Azure с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="6ab6c-263">Новые строки добавляются в таблицу toohello каждый час.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-263">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="6ab6c-264">**Действие копирования в конвейере с источником BlobSource и приемником AzureTableSink**</span><span class="sxs-lookup"><span data-stu-id="6ab6c-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="6ab6c-265">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6ab6c-266">В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="6ab6c-267">Сопоставление типов для таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="6ab6c-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="6ab6c-268">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="6ab6c-269">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="6ab6c-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="6ab6c-270">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="6ab6c-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="6ab6c-271">При перемещении данных слишком & из таблицы Azure hello следующие [сопоставления, которые определены службой таблицы Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) используются из типа too.NET типы OData Azure таблицы и наоборот.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="6ab6c-272">Тип данных OData</span><span class="sxs-lookup"><span data-stu-id="6ab6c-272">OData Data Type</span></span> | <span data-ttu-id="6ab6c-273">Тип .NET</span><span class="sxs-lookup"><span data-stu-id="6ab6c-273">.NET Type</span></span> | <span data-ttu-id="6ab6c-274">Сведения</span><span class="sxs-lookup"><span data-stu-id="6ab6c-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ab6c-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="6ab6c-275">Edm.Binary</span></span> |<span data-ttu-id="6ab6c-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="6ab6c-276">byte[]</span></span> |<span data-ttu-id="6ab6c-277">Массив байтов, копирование too64 КБ.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="6ab6c-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="6ab6c-278">Edm.Boolean</span></span> |<span data-ttu-id="6ab6c-279">bool</span><span class="sxs-lookup"><span data-stu-id="6ab6c-279">bool</span></span> |<span data-ttu-id="6ab6c-280">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-280">A Boolean value.</span></span> |
| <span data-ttu-id="6ab6c-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="6ab6c-281">Edm.DateTime</span></span> |<span data-ttu-id="6ab6c-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ab6c-282">DateTime</span></span> |<span data-ttu-id="6ab6c-283">64-битное значение времени, выраженное в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="6ab6c-284">Hello поддерживается DateTime диапазон начинается от 00:00 1 января 1601 г. нашей эры</span><span class="sxs-lookup"><span data-stu-id="6ab6c-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="6ab6c-285">Англиканское летоисчисление, часовой пояс — UTC.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-285">(C.E.), UTC.</span></span> <span data-ttu-id="6ab6c-286">диапазон Hello заканчивается 31 декабря 9999 года.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="6ab6c-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="6ab6c-287">Edm.Double</span></span> |<span data-ttu-id="6ab6c-288">double</span><span class="sxs-lookup"><span data-stu-id="6ab6c-288">double</span></span> |<span data-ttu-id="6ab6c-289">64-битное значение с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="6ab6c-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="6ab6c-290">Edm.Guid</span></span> |<span data-ttu-id="6ab6c-291">Guid</span><span class="sxs-lookup"><span data-stu-id="6ab6c-291">Guid</span></span> |<span data-ttu-id="6ab6c-292">128-битный идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="6ab6c-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="6ab6c-293">Edm.Int32</span></span> |<span data-ttu-id="6ab6c-294">Int32</span><span class="sxs-lookup"><span data-stu-id="6ab6c-294">Int32</span></span> |<span data-ttu-id="6ab6c-295">32-битное целое число.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="6ab6c-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="6ab6c-296">Edm.Int64</span></span> |<span data-ttu-id="6ab6c-297">Int64</span><span class="sxs-lookup"><span data-stu-id="6ab6c-297">Int64</span></span> |<span data-ttu-id="6ab6c-298">64-битное целое число.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="6ab6c-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="6ab6c-299">Edm.String</span></span> |<span data-ttu-id="6ab6c-300">Строка</span><span class="sxs-lookup"><span data-stu-id="6ab6c-300">String</span></span> |<span data-ttu-id="6ab6c-301">Значение в кодировке UTF-16.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="6ab6c-302">Строковые значения могут иметь копии too64 КБ.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="6ab6c-303">Пример преобразования типов</span><span class="sxs-lookup"><span data-stu-id="6ab6c-303">Type Conversion Sample</span></span>
<span data-ttu-id="6ab6c-304">Следующий образец Hello предназначен для копирования данных из больших двоичных объектов Azure tooAzure таблицы, с помощью преобразования типов.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="6ab6c-305">Предположим, что набор данных BLOB-объектов hello в формате CSV и содержит три столбца.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="6ab6c-306">Один из них — это столбец datetime с пользовательского формата datetime использование сокращенного французский имен для дня недели hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="6ab6c-307">Определите набор данных BLOB-объект источника hello следующим, а также определения типов для столбцов hello.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="6ab6c-308">Даны сопоставление типов hello too.NET тип OData таблицы Azure, можно задать hello таблицы в таблице Azure с hello следующие схемы.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="6ab6c-309">**Схема таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="6ab6c-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="6ab6c-310">Имя столбца</span><span class="sxs-lookup"><span data-stu-id="6ab6c-310">Column name</span></span> | <span data-ttu-id="6ab6c-311">Тип</span><span class="sxs-lookup"><span data-stu-id="6ab6c-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="6ab6c-312">userid</span><span class="sxs-lookup"><span data-stu-id="6ab6c-312">userid</span></span> |<span data-ttu-id="6ab6c-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="6ab6c-313">Edm.Int64</span></span> |
| <span data-ttu-id="6ab6c-314">name</span><span class="sxs-lookup"><span data-stu-id="6ab6c-314">name</span></span> |<span data-ttu-id="6ab6c-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="6ab6c-315">Edm.String</span></span> |
| <span data-ttu-id="6ab6c-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="6ab6c-316">lastlogindate</span></span> |<span data-ttu-id="6ab6c-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="6ab6c-317">Edm.DateTime</span></span> |

<span data-ttu-id="6ab6c-318">После этого определите набор данных таблиц Azure hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="6ab6c-319">Раздел «структура» toospecify hello сведения о типе не обязательно, поскольку сведения о типе hello уже задан в hello базового хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="6ab6c-320">В этом случае фабрики данных автоматически тип преобразования, включая hello поля даты и времени с hello пользовательского формата datetime с помощью языка и региональных параметров «fr-fr» hello при перемещении данных из большого двоичного объекта tooAzure таблицы.</span><span class="sxs-lookup"><span data-stu-id="6ab6c-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="6ab6c-321">toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6ab6c-322">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="6ab6c-322">Performance and Tuning</span></span>
<span data-ttu-id="6ab6c-323">toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize, в разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="6ab6c-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
