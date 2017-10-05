---
title: "Перемещение данных в Azure Cosmos DB и обратно | Документация Майкрософт"
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
ms.openlocfilehash: 7a11c6ade0325b08ad520448bbf82d64a0a555f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="a9736-103">Перемещение данных в Azure Cosmos DB и из нее с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="a9736-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="a9736-104">В этой статье объясняется, как с помощью действия копирования в фабрике данных Azure перемещать данные в Azure Cosmos DB и обратно (API DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="a9736-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="a9736-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="a9736-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="a9736-106">Данные можно скопировать из любого поддерживаемого в качестве источника хранилища данных в Azure Cosmos DB или из Azure Cosmos DB в любое поддерживаемое в качестве приемника хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-106">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span></span> <span data-ttu-id="a9736-107">Список хранилищ данных, которые поддерживаются в качестве источников и приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="a9736-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a9736-108">Соединитель Azure Cosmos DB поддерживает только API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a9736-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="a9736-109">Сведения о копировании данных "как есть" в JSON-файлы или другую коллекцию Cosmos DB либо из них см. в разделе [Импорт и экспорт документов JSON](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="a9736-109">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="a9736-110">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="a9736-110">Getting started</span></span>
<span data-ttu-id="a9736-111">Вы можете создать конвейер с действием копирования, которое перемещает данные из хранилища Azure Cosmos DB или обратно, с помощью различных инструментов и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="a9736-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="a9736-112">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="a9736-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a9736-113">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="a9736-114">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="a9736-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a9736-115">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="a9736-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a9736-116">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="a9736-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="a9736-117">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-117">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="a9736-118">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="a9736-118">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="a9736-119">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a9736-120">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="a9736-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a9736-121">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="a9736-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a9736-122">Примеры с определениями JSON для сущностей фабрики данных, которые используются для копирования данных в службу Azure Cosmos DB и из нее, приведены в разделе с [примерами JSON](#json-examples) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a9736-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="a9736-123">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для службы Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a9736-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="a9736-124">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="a9736-124">Linked service properties</span></span>
<span data-ttu-id="a9736-125">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a9736-125">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span></span>

| <span data-ttu-id="a9736-126">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="a9736-126">**Property**</span></span> | <span data-ttu-id="a9736-127">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a9736-127">**Description**</span></span> | <span data-ttu-id="a9736-128">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="a9736-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9736-129">type</span><span class="sxs-lookup"><span data-stu-id="a9736-129">type</span></span> |<span data-ttu-id="a9736-130">Для свойства надо указать тип **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="a9736-130">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="a9736-131">Да</span><span class="sxs-lookup"><span data-stu-id="a9736-131">Yes</span></span> |
| <span data-ttu-id="a9736-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="a9736-132">connectionString</span></span> |<span data-ttu-id="a9736-133">Укажите сведения, необходимые для подключения к базе данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a9736-133">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="a9736-134">Да</span><span class="sxs-lookup"><span data-stu-id="a9736-134">Yes</span></span> |

<span data-ttu-id="a9736-135">Пример:</span><span class="sxs-lookup"><span data-stu-id="a9736-135">Example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="a9736-136">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="a9736-136">Dataset properties</span></span>
<span data-ttu-id="a9736-137">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Создание наборов данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="a9736-137">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a9736-138">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="a9736-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a9736-139">Раздел typeProperties во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-139">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a9736-140">Раздел typeProperties для набора данных типа **DocumentDbCollection** содержит приведенные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="a9736-140">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="a9736-141">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="a9736-141">**Property**</span></span> | <span data-ttu-id="a9736-142">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a9736-142">**Description**</span></span> | <span data-ttu-id="a9736-143">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="a9736-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9736-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="a9736-144">collectionName</span></span> |<span data-ttu-id="a9736-145">Имя коллекции документов Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a9736-145">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="a9736-146">Да</span><span class="sxs-lookup"><span data-stu-id="a9736-146">Yes</span></span> |

<span data-ttu-id="a9736-147">Пример:</span><span class="sxs-lookup"><span data-stu-id="a9736-147">Example:</span></span>

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
### <a name="schema-by-data-factory"></a><span data-ttu-id="a9736-148">Схема фабрики данных</span><span class="sxs-lookup"><span data-stu-id="a9736-148">Schema by Data Factory</span></span>
<span data-ttu-id="a9736-149">Для хранилищ данных без схемы, таких как Azure Cosmos DB, служба фабрики данных определяет схему одним из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="a9736-149">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="a9736-150">Если указать структуру данных с помощью свойства **structure** в определении набора данных, служба фабрики данных считает эту структуру схемой.</span><span class="sxs-lookup"><span data-stu-id="a9736-150">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="a9736-151">В этом случае, если строка не содержит значение столбца, ему будет присвоено значение NULL.</span><span class="sxs-lookup"><span data-stu-id="a9736-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="a9736-152">Если структура данных не указана с помощью свойства **structure** в определении набора данных, то служба фабрики данных определяет схему, используя первую строку данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-152">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="a9736-153">В этом случае, если первая строка не содержит полную схему, после операции копирования некоторые столбцы будут отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="a9736-153">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="a9736-154">Таким образом для источников данных без схемы рекомендуется указывать структуру данных с помощью свойства **structure** .</span><span class="sxs-lookup"><span data-stu-id="a9736-154">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="a9736-155">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="a9736-155">Copy activity properties</span></span>
<span data-ttu-id="a9736-156">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="a9736-156">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a9736-157">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="a9736-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="a9736-158">Действие копирования принимает только один набор входных данных и возвращает только один набор выходных.</span><span class="sxs-lookup"><span data-stu-id="a9736-158">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="a9736-159">То, какие свойства будут доступны в разделе typeProperties, зависит от типа действия, а в случае с действием копирования — еще и от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="a9736-159">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="a9736-160">В случае действия копирования, когда источник относится к типу **DocumentDbCollectionSource**, в разделе **typeProperties** доступны приведенные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="a9736-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="a9736-161">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="a9736-161">**Property**</span></span> | <span data-ttu-id="a9736-162">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a9736-162">**Description**</span></span> | <span data-ttu-id="a9736-163">**Допустимые значения**</span><span class="sxs-lookup"><span data-stu-id="a9736-163">**Allowed values**</span></span> | <span data-ttu-id="a9736-164">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="a9736-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a9736-165">запрос</span><span class="sxs-lookup"><span data-stu-id="a9736-165">query</span></span> |<span data-ttu-id="a9736-166">Запрос, нужный для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-166">Specify the query to read data.</span></span> |<span data-ttu-id="a9736-167">Строка запроса, поддерживаемая Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a9736-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="a9736-168">Пример: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="a9736-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="a9736-169">Нет</span><span class="sxs-lookup"><span data-stu-id="a9736-169">No</span></span> <br/><br/><span data-ttu-id="a9736-170">Если не указано, то выполняется инструкция SQL `select <columns defined in structure> from mycollection`.</span><span class="sxs-lookup"><span data-stu-id="a9736-170">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="a9736-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="a9736-171">nestingSeparator</span></span> |<span data-ttu-id="a9736-172">Специальный символ, обозначающий, что документ является вложенным.</span><span class="sxs-lookup"><span data-stu-id="a9736-172">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="a9736-173">Любой символ.</span><span class="sxs-lookup"><span data-stu-id="a9736-173">Any character.</span></span> <br/><br/><span data-ttu-id="a9736-174">Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры.</span><span class="sxs-lookup"><span data-stu-id="a9736-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="a9736-175">Фабрика данных Azure позволяет обозначать иерархию с помощью разделителя nestingSeparator.</span><span class="sxs-lookup"><span data-stu-id="a9736-175">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="a9736-176">В приведенных выше примерах это точка.</span><span class="sxs-lookup"><span data-stu-id="a9736-176">in the above examples.</span></span> <span data-ttu-id="a9736-177">Благодаря этому разделителю действие копирование создаст объект Name с тремя дочерними элементами, First, Middle и Last, в соответствии с элементами Name.First, Name.Middle и Name.Last в определении таблицы.</span><span class="sxs-lookup"><span data-stu-id="a9736-177">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="a9736-178">Нет</span><span class="sxs-lookup"><span data-stu-id="a9736-178">No</span></span> |

<span data-ttu-id="a9736-179">**DocumentDbCollectionSink** поддерживает приведенные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="a9736-179">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="a9736-180">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="a9736-180">**Property**</span></span> | <span data-ttu-id="a9736-181">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a9736-181">**Description**</span></span> | <span data-ttu-id="a9736-182">**Допустимые значения**</span><span class="sxs-lookup"><span data-stu-id="a9736-182">**Allowed values**</span></span> | <span data-ttu-id="a9736-183">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="a9736-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a9736-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="a9736-184">nestingSeparator</span></span> |<span data-ttu-id="a9736-185">Такой специальный символ в имени исходного столбца, который указывает, что нужен вложенный документ.</span><span class="sxs-lookup"><span data-stu-id="a9736-185">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="a9736-186">См. пример выше: элемент `Name.First` в выходной таблице обуславливает в документе Cosmos DB такую структуру JSON:</span><span class="sxs-lookup"><span data-stu-id="a9736-186">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="a9736-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="a9736-187">"Name": {</span></span><br/>    <span data-ttu-id="a9736-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="a9736-188">"First": "John"</span></span><br/><span data-ttu-id="a9736-189">},</span><span class="sxs-lookup"><span data-stu-id="a9736-189">},</span></span> |<span data-ttu-id="a9736-190">Символ, используемый для разделения уровней вложенности.</span><span class="sxs-lookup"><span data-stu-id="a9736-190">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="a9736-191">Значение по умолчанию — `.` (точка).</span><span class="sxs-lookup"><span data-stu-id="a9736-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="a9736-192">Символ, используемый для разделения уровней вложенности.</span><span class="sxs-lookup"><span data-stu-id="a9736-192">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="a9736-193">Значение по умолчанию — `.` (точка).</span><span class="sxs-lookup"><span data-stu-id="a9736-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="a9736-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="a9736-194">writeBatchSize</span></span> |<span data-ttu-id="a9736-195">Число параллельных запросов к службе Azure Cosmos DB для создания документов.</span><span class="sxs-lookup"><span data-stu-id="a9736-195">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="a9736-196">При копировании данных в службу Cosmos DB или из нее с помощью этого свойства можно оптимизировать производительность.</span><span class="sxs-lookup"><span data-stu-id="a9736-196">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="a9736-197">Если увеличить значение свойства writeBatchSize, производительность повышается, потому что в Cosmos DB начинает поступать больше параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="a9736-197">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span></span> <span data-ttu-id="a9736-198">Однако необходимо избежать регулирования, которое может вызвать сообщение об ошибке: "Высокая частота запросов".</span><span class="sxs-lookup"><span data-stu-id="a9736-198">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="a9736-199">Регулирование может произойти по ряду причин, включая размер документов, количество терминов в документах, политику индексации целевой коллекции и т. д. Для операций копирования вы можете использовать коллекцию получше (например, S3), чтобы обеспечить максимальную пропускную способность (2500 единиц запроса в секунду).</span><span class="sxs-lookup"><span data-stu-id="a9736-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="a9736-200">Целое число </span><span class="sxs-lookup"><span data-stu-id="a9736-200">Integer</span></span> |<span data-ttu-id="a9736-201">Нет (значение по умолчанию — 5)</span><span class="sxs-lookup"><span data-stu-id="a9736-201">No (default: 5)</span></span> |
| <span data-ttu-id="a9736-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="a9736-202">writeBatchTimeout</span></span> |<span data-ttu-id="a9736-203">Время ожидания до выполнения операции, пока не завершится срок ее действия.</span><span class="sxs-lookup"><span data-stu-id="a9736-203">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="a9736-204">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="a9736-204">timespan</span></span><br/><br/> <span data-ttu-id="a9736-205">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="a9736-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="a9736-206">Нет</span><span class="sxs-lookup"><span data-stu-id="a9736-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="a9736-207">Документы JSON для импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="a9736-207">Import/Export JSON documents</span></span>
<span data-ttu-id="a9736-208">С помощью этого соединителя Cosmos DB можно выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a9736-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="a9736-209">импортировать документы JSON из различных источников в Cosmos DB, включая хранилище BLOB-объектов Azure, Azure Data Lake, локальную файловую систему или другие файловые хранилища, поддерживаемые фабрикой данных Azure;</span><span class="sxs-lookup"><span data-stu-id="a9736-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="a9736-210">экспортировать документы JSON из коллекции Cosmos DB в различные файловые хранилища;</span><span class="sxs-lookup"><span data-stu-id="a9736-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="a9736-211">переносить данные между коллекциями Cosmos DB "как есть".</span><span class="sxs-lookup"><span data-stu-id="a9736-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="a9736-212">Для обеспечения такого копирования без использования схем:</span><span class="sxs-lookup"><span data-stu-id="a9736-212">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="a9736-213">При использовании мастера копирования установите флажок **Export as-is to JSON files or DocumentDB collection** (Экспортировать как есть в JSON-файлы или коллекцию Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="a9736-213">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="a9736-214">При редактировании JSON не указывайте раздел structure в наборах данных Cosmos DB и свойство nestingSeparator для источника или приемника Cosmos DB в действии копирования.</span><span class="sxs-lookup"><span data-stu-id="a9736-214">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="a9736-215">Чтобы импортировать данные в JSON-файлы или экспортировать их оттуда, в наборе хранилища файлов укажите тип формата "JsonFormat", конфигурацию "filePattern" и пропустите остальные параметры формата. Дополнительные сведения см. в разделе [Формат JSON](data-factory-supported-file-and-compression-formats.md#json-format).</span><span class="sxs-lookup"><span data-stu-id="a9736-215">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="a9736-216">Примеры определений JSON</span><span class="sxs-lookup"><span data-stu-id="a9736-216">JSON examples</span></span>
<span data-ttu-id="a9736-217">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a9736-217">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a9736-218">Они показывают, как копировать данные в Azure Cosmos DB и хранилище BLOB-объектов Azure и обратно.</span><span class="sxs-lookup"><span data-stu-id="a9736-218">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="a9736-219">Тем не менее данные можно копировать **непосредственно** из любых источников в любой указанный [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемник. Для этого используется действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a9736-219">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a><span data-ttu-id="a9736-220">Пример. Копирование данных из Azure Cosmos DB в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="a9736-220">Example: Copy data from Azure Cosmos DB to Azure Blob</span></span>
<span data-ttu-id="a9736-221">В примере ниже показано следующее.</span><span class="sxs-lookup"><span data-stu-id="a9736-221">The sample below shows:</span></span>

1. <span data-ttu-id="a9736-222">Связанная служба типа [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="a9736-223">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a9736-224">Входной [набор данных](data-factory-create-datasets.md) типа [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="a9736-225">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a9736-226">Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [DocumentDbCollectionSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a9736-227">Этот пример копирует данные из Azure Cosmos DB в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="a9736-227">The sample copies data in Azure Cosmos DB to Azure Blob.</span></span> <span data-ttu-id="a9736-228">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="a9736-228">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a9736-229">**Связанная служба Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="a9736-229">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="a9736-230">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="a9736-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="a9736-231">**Входной набор данных Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="a9736-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="a9736-232">В этом примере предполагается, что в базе данных Azure Cosmos DB есть коллекция **Person**.</span><span class="sxs-lookup"><span data-stu-id="a9736-232">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="a9736-233">Если для параметра external задать значение true и указать политику externalData, фабрика данных Azure будет считать эту таблицу внешней по отношению к себе и не созданной в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-233">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="a9736-234">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="a9736-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a9736-235">Данные копируются в новый BLOB-объект каждый час. Путь к BLOB-объекту отражает дату и время по часам.</span><span class="sxs-lookup"><span data-stu-id="a9736-235">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

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
<span data-ttu-id="a9736-236">Образец JSON-документа в коллекции Person в базе данных Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="a9736-236">Sample JSON document in the Person collection in a Cosmos DB database:</span></span>

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
<span data-ttu-id="a9736-237">Служба Cosmos DB поддерживает выполнение запросов к документам, используя для обработки иерархических JSON-документов синтаксис наподобие SQL.</span><span class="sxs-lookup"><span data-stu-id="a9736-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="a9736-238">Пример:</span><span class="sxs-lookup"><span data-stu-id="a9736-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="a9736-239">В конвейере ниже данные копируются из коллекции Person, находящейся в базе данных Azure Cosmos DB, в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="a9736-239">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span></span> <span data-ttu-id="a9736-240">Для действия копирования указаны входные и выходные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-240">As part of the copy activity the input and output datasets have been specified.</span></span>  

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
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a><span data-ttu-id="a9736-241">Пример. Копирование данных из большого двоичного объекта в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a9736-241">Example: Copy data from Azure Blob to Azure Cosmos DB</span></span> 
<span data-ttu-id="a9736-242">В примере ниже показано следующее.</span><span class="sxs-lookup"><span data-stu-id="a9736-242">The sample below shows:</span></span>

1. <span data-ttu-id="a9736-243">Связанная служба типа [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="a9736-244">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a9736-245">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="a9736-246">Выходной [набор данных](data-factory-create-datasets.md) типа [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="a9736-247">Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="a9736-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="a9736-248">В этом примере данные копируются из большого двоичного объекта Azure в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a9736-248">The sample copies data from Azure blob to Azure Cosmos DB.</span></span> <span data-ttu-id="a9736-249">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="a9736-249">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a9736-250">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="a9736-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="a9736-251">**Связанная служба Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="a9736-251">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="a9736-252">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="a9736-252">**Azure Blob input dataset:**</span></span>

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
<span data-ttu-id="a9736-253">**Выходной набор данных Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="a9736-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="a9736-254">В примере данные копируются в коллекцию Person.</span><span class="sxs-lookup"><span data-stu-id="a9736-254">The sample copies data to a collection named “Person”.</span></span>

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
<span data-ttu-id="a9736-255">В приведенном ниже конвейере данные копируются из большого двоичного объекта Azure в коллекцию Person, находящуюся в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a9736-255">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span></span> <span data-ttu-id="a9736-256">Для действия копирования указаны входные и выходные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="a9736-256">As part of the copy activity the input and output datasets have been specified.</span></span>

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
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
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
<span data-ttu-id="a9736-257">Если пример входных данных BLOB-объекта выглядит так:</span><span class="sxs-lookup"><span data-stu-id="a9736-257">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="a9736-258">JSON-файл выходных данных в Cosmos DB будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="a9736-258">Then the output JSON in Cosmos DB will be as:</span></span>

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
<span data-ttu-id="a9736-259">Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры.</span><span class="sxs-lookup"><span data-stu-id="a9736-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="a9736-260">Фабрика данных Azure позволяет обозначать иерархию с помощью разделителя **nestingSeparator**,</span><span class="sxs-lookup"><span data-stu-id="a9736-260">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="a9736-261">которым в этом примере является точка.</span><span class="sxs-lookup"><span data-stu-id="a9736-261">in this example.</span></span> <span data-ttu-id="a9736-262">Благодаря этому разделителю действие копирование создаст объект Name с тремя дочерними элементами, First, Middle и Last, в соответствии с элементами Name.First, Name.Middle и Name.Last в определении таблицы.</span><span class="sxs-lookup"><span data-stu-id="a9736-262">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="a9736-263">Приложение</span><span class="sxs-lookup"><span data-stu-id="a9736-263">Appendix</span></span>
1. <span data-ttu-id="a9736-264">**Вопрос.** Поддерживает ли действие копирования обновление существующих записей?</span><span class="sxs-lookup"><span data-stu-id="a9736-264">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="a9736-265">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="a9736-265">**Answer:** No.</span></span>
2. <span data-ttu-id="a9736-266">**Вопрос:** как работает при повторной попытке Копировать в базе данных Azure Cosmos приходится иметь дело с уже скопированы записей?</span><span class="sxs-lookup"><span data-stu-id="a9736-266">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="a9736-267">**Ответ.** Если у записи есть поле идентификатора, и операция копирования пытается вставить запись с тем же идентификатором, операция копирования завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="a9736-267">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="a9736-268">**Вопрос:** поддерживает фабрики данных [диапазон или секционирование данных на основе хэша](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="a9736-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="a9736-269">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="a9736-269">**Answer:** No.</span></span>
4. <span data-ttu-id="a9736-270">**Вопрос:** можно указать несколько коллекций Azure Cosmos DB для таблицы?</span><span class="sxs-lookup"><span data-stu-id="a9736-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="a9736-271">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="a9736-271">**Answer:** No.</span></span> <span data-ttu-id="a9736-272">Сейчас можно указать только одну коллекцию.</span><span class="sxs-lookup"><span data-stu-id="a9736-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a9736-273">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="a9736-273">Performance and Tuning</span></span>
<span data-ttu-id="a9736-274">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="a9736-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
