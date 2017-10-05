---
title: "Перемещение данных в таблицу Azure и из нее | Документация Майкрософт"
description: "Узнайте, как переместить данные в таблицу SQL Azure и из нее с помощью фабрики данных Azure."
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
ms.openlocfilehash: 792a551ae3dae46c503e5f0dda74cd0ac3a69c3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="22549-103">Перемещение данных в таблицу SQL Azure и из нее с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="22549-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="22549-104">В этой статье описывается, как с помощью действия копирования в фабрике данных Azure перемещать данные в хранилище таблиц Azure и из него.</span><span class="sxs-lookup"><span data-stu-id="22549-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="22549-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="22549-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="22549-106">Данные можно скопировать из любого поддерживаемого в качестве источника хранилища данных в хранилище таблиц Azure или из хранилища таблиц Azure в любое поддерживаемое в качестве приемника хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="22549-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="22549-107">Список хранилищ данных, которые поддерживаются в качестве источников и приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="22549-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="22549-108">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="22549-108">Getting started</span></span>
<span data-ttu-id="22549-109">Вы можете создать конвейер с действием копирования, который перемещает данные в хранилище таблиц Azure или из него, с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="22549-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="22549-110">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="22549-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="22549-111">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="22549-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="22549-112">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="22549-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="22549-113">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="22549-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="22549-114">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="22549-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="22549-115">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="22549-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="22549-116">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="22549-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="22549-117">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="22549-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="22549-118">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="22549-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="22549-119">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="22549-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="22549-120">Примеры с определениями JSON для сущностей фабрики данных, которые используются для копирования данных в хранилище таблиц Azure и из него, приведены в разделе [Примеры JSON](#json-examples) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="22549-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="22549-121">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к хранилищу таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="22549-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="22549-122">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="22549-122">Linked service properties</span></span>
<span data-ttu-id="22549-123">Для связи хранилища BLOB-объектов Azure с фабрикой данных Azure можно использовать два типа связанных служб:</span><span class="sxs-lookup"><span data-stu-id="22549-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="22549-124">**AzureStorage** и **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="22549-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="22549-125">Связанная служба хранилища Azure предоставляет фабрике данных глобальный доступ к хранилищу Azure,</span><span class="sxs-lookup"><span data-stu-id="22549-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="22549-126">а связанная служба SAS хранилища Azure — ограниченный или привязанный ко времени доступ к хранилищу Azure.</span><span class="sxs-lookup"><span data-stu-id="22549-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="22549-127">Других различий между этими связанными службами нет.</span><span class="sxs-lookup"><span data-stu-id="22549-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="22549-128">Выберите связанную службу, соответствующую вашим задачам.</span><span class="sxs-lookup"><span data-stu-id="22549-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="22549-129">Более подробно эти службы описаны в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="22549-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="22549-130">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="22549-130">Dataset properties</span></span>
<span data-ttu-id="22549-131">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="22549-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="22549-132">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="22549-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="22549-133">Раздел typeProperties во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="22549-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="22549-134">Раздел **typeProperties** набора данных типа **AzureTable** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="22549-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="22549-135">Свойство</span><span class="sxs-lookup"><span data-stu-id="22549-135">Property</span></span> | <span data-ttu-id="22549-136">Описание</span><span class="sxs-lookup"><span data-stu-id="22549-136">Description</span></span> | <span data-ttu-id="22549-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="22549-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22549-138">tableName</span><span class="sxs-lookup"><span data-stu-id="22549-138">tableName</span></span> |<span data-ttu-id="22549-139">Имя таблицы в экземпляре базы данных таблиц Azure, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="22549-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="22549-140">Да.</span><span class="sxs-lookup"><span data-stu-id="22549-140">Yes.</span></span> <span data-ttu-id="22549-141">Если tableName указывается без azureTableSourceQuery, все записи из таблицы копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="22549-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="22549-142">Если azureTableSourceQuery указывается, записи из таблицы, удовлетворяющие запросу, копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="22549-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="22549-143">Схема фабрики данных</span><span class="sxs-lookup"><span data-stu-id="22549-143">Schema by Data Factory</span></span>
<span data-ttu-id="22549-144">Для хранилищ данных без схемы, таких как таблица Azure, служба фабрики данных определяет схему одним из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="22549-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="22549-145">Если указать структуру данных с помощью свойства **structure** в определении набора данных, то служба фабрики данных считает эту структуру схемой.</span><span class="sxs-lookup"><span data-stu-id="22549-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="22549-146">В этом случае, если строка не содержит значение столбца, ему присваивается значение NULL.</span><span class="sxs-lookup"><span data-stu-id="22549-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="22549-147">Если структура данных не указана с помощью свойства **structure** в определении набора данных, то фабрика данных определяет схему, используя первую строку данных.</span><span class="sxs-lookup"><span data-stu-id="22549-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="22549-148">В этом случае, если первая строка не содержит полную схему, после операции копирования некоторые столбцы будут отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="22549-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="22549-149">Таким образом для источников данных без схемы рекомендуется указывать структуру данных с помощью свойства **structure** .</span><span class="sxs-lookup"><span data-stu-id="22549-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="22549-150">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="22549-150">Copy activity properties</span></span>
<span data-ttu-id="22549-151">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="22549-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="22549-152">Свойства, например имя, описание, входные и выходные таблицы, политики и т. д., доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="22549-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="22549-153">С другой стороны, свойства, доступные в разделе typeProperties действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="22549-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="22549-154">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="22549-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="22549-155">**AzureTableSource** в разделе typeProperties поддерживает следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="22549-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="22549-156">Свойство</span><span class="sxs-lookup"><span data-stu-id="22549-156">Property</span></span> | <span data-ttu-id="22549-157">Описание</span><span class="sxs-lookup"><span data-stu-id="22549-157">Description</span></span> | <span data-ttu-id="22549-158">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="22549-158">Allowed values</span></span> | <span data-ttu-id="22549-159">Обязательно</span><span class="sxs-lookup"><span data-stu-id="22549-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="22549-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="22549-160">azureTableSourceQuery</span></span> |<span data-ttu-id="22549-161">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="22549-161">Use the custom query to read data.</span></span> |<span data-ttu-id="22549-162">Строка запроса таблицы Azure.</span><span class="sxs-lookup"><span data-stu-id="22549-162">Azure table query string.</span></span> <span data-ttu-id="22549-163">Примеры приведены в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="22549-163">See examples in the next section.</span></span> |<span data-ttu-id="22549-164">Нет.</span><span class="sxs-lookup"><span data-stu-id="22549-164">No.</span></span> <span data-ttu-id="22549-165">Если tableName указывается без azureTableSourceQuery, все записи из таблицы копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="22549-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="22549-166">Если azureTableSourceQuery указывается, записи из таблицы, удовлетворяющие запросу, копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="22549-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="22549-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="22549-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="22549-168">Указывает, игнорируются ли исключения таблицы.</span><span class="sxs-lookup"><span data-stu-id="22549-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="22549-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="22549-169">TRUE</span></span><br/><span data-ttu-id="22549-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="22549-170">FALSE</span></span> |<span data-ttu-id="22549-171">Нет</span><span class="sxs-lookup"><span data-stu-id="22549-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="22549-172">Примеры azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="22549-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="22549-173">Если столбец таблицы Azure имеет тип строки:</span><span class="sxs-lookup"><span data-stu-id="22549-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="22549-174">Если столбец таблицы Azure имеет тип даты и времени:</span><span class="sxs-lookup"><span data-stu-id="22549-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="22549-175">**AzureTableSink** поддерживает указанные ниже свойства в разделе typeProperties.</span><span class="sxs-lookup"><span data-stu-id="22549-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="22549-176">Свойство</span><span class="sxs-lookup"><span data-stu-id="22549-176">Property</span></span> | <span data-ttu-id="22549-177">Описание</span><span class="sxs-lookup"><span data-stu-id="22549-177">Description</span></span> | <span data-ttu-id="22549-178">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="22549-178">Allowed values</span></span> | <span data-ttu-id="22549-179">Обязательно</span><span class="sxs-lookup"><span data-stu-id="22549-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="22549-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="22549-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="22549-181">Значение ключа раздела по умолчанию, которое может использоваться приемником.</span><span class="sxs-lookup"><span data-stu-id="22549-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="22549-182">Строковое значение.</span><span class="sxs-lookup"><span data-stu-id="22549-182">A string value.</span></span> |<span data-ttu-id="22549-183">Нет</span><span class="sxs-lookup"><span data-stu-id="22549-183">No</span></span> |
| <span data-ttu-id="22549-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="22549-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="22549-185">Укажите имя столбца, значения которого используются в качестве ключей секций.</span><span class="sxs-lookup"><span data-stu-id="22549-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="22549-186">Если не указано, в качестве ключа раздела используется AzureTableDefaultPartitionKeyValue.</span><span class="sxs-lookup"><span data-stu-id="22549-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="22549-187">Имя столбца.</span><span class="sxs-lookup"><span data-stu-id="22549-187">A column name.</span></span> |<span data-ttu-id="22549-188">Нет</span><span class="sxs-lookup"><span data-stu-id="22549-188">No</span></span> |
| <span data-ttu-id="22549-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="22549-189">azureTableRowKeyName</span></span> |<span data-ttu-id="22549-190">Укажите имя столбца, значения которого используются в качестве ключа строки.</span><span class="sxs-lookup"><span data-stu-id="22549-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="22549-191">Если имя не указано, используйте для каждой строки идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="22549-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="22549-192">Имя столбца.</span><span class="sxs-lookup"><span data-stu-id="22549-192">A column name.</span></span> |<span data-ttu-id="22549-193">Нет</span><span class="sxs-lookup"><span data-stu-id="22549-193">No</span></span> |
| <span data-ttu-id="22549-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="22549-194">azureTableInsertType</span></span> |<span data-ttu-id="22549-195">Режим для вставки данных в таблицу Azure.</span><span class="sxs-lookup"><span data-stu-id="22549-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="22549-196">Это свойство контролирует, будут ли заменены или объединены значения в существующих строках в выходной таблице с совпадающими ключами секций и строк.</span><span class="sxs-lookup"><span data-stu-id="22549-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="22549-197">Чтобы узнать о действии этих параметров (merge и replace), ознакомьтесь со статьями [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) (Вставка или слияние сущностей) и [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) (Вставка или замена сущности).</span><span class="sxs-lookup"><span data-stu-id="22549-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="22549-198">Этот параметр применяется на уровне строки, а не таблицы, и ни один из параметров не приводит к удалению строк в выходной таблице, которые отсутствуют во входных данных.</span><span class="sxs-lookup"><span data-stu-id="22549-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="22549-199">merge (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="22549-199">merge (default)</span></span><br/><span data-ttu-id="22549-200">replace</span><span class="sxs-lookup"><span data-stu-id="22549-200">replace</span></span> |<span data-ttu-id="22549-201">Нет</span><span class="sxs-lookup"><span data-stu-id="22549-201">No</span></span> |
| <span data-ttu-id="22549-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="22549-202">writeBatchSize</span></span> |<span data-ttu-id="22549-203">Вставка данных в таблицу Azure при достижении writeBatchSize или writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="22549-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="22549-204">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="22549-204">Integer (number of rows)</span></span> |<span data-ttu-id="22549-205">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="22549-205">No (default: 10000)</span></span> |
| <span data-ttu-id="22549-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="22549-206">writeBatchTimeout</span></span> |<span data-ttu-id="22549-207">Вставка данных в таблицу Azure при достижении writeBatchSize или writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="22549-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="22549-208">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="22549-208">timespan</span></span><br/><br/><span data-ttu-id="22549-209">Пример: 00:20:00 (20 минут).</span><span class="sxs-lookup"><span data-stu-id="22549-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="22549-210">Нет (по умолчанию используется время ожидания, стандартное для клиента хранения — 90 секунд)</span><span class="sxs-lookup"><span data-stu-id="22549-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="22549-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="22549-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="22549-212">Чтобы вы могли использовать целевой столбец как azureTablePartitionKeyName, необходимо сопоставить исходный столбец с целевым столбцом с помощью свойства JSON translator.</span><span class="sxs-lookup"><span data-stu-id="22549-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="22549-213">В следующем примере исходный столбец DivisionID сопоставляется с целевым столбцом: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="22549-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="22549-214">DivisionID указывается в качестве ключа секции.</span><span class="sxs-lookup"><span data-stu-id="22549-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="22549-215">Примеры JSON</span><span class="sxs-lookup"><span data-stu-id="22549-215">JSON examples</span></span>
<span data-ttu-id="22549-216">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="22549-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="22549-217">В них показано, как копировать данные в хранилище таблиц Azure и хранилище BLOB-объектов Azure и обратно.</span><span class="sxs-lookup"><span data-stu-id="22549-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="22549-218">Однако данные можно скопировать данные **непосредственно** из любых источников на любой из поддерживаемых приемников.</span><span class="sxs-lookup"><span data-stu-id="22549-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="22549-219">Дополнительные сведения см. в разделе "Поддерживаемые хранилища данных и форматы" статьи [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="22549-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="22549-220">Пример. Копирование данных из таблицы Azure в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="22549-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="22549-221">В примере ниже используется следующее:</span><span class="sxs-lookup"><span data-stu-id="22549-221">The following sample shows:</span></span>

1. <span data-ttu-id="22549-222">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (используется для таблиц и больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="22549-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="22549-223">Входной [набор данных](data-factory-create-datasets.md) типа [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="22549-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="22549-224">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="22549-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="22549-225">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [AzureTableSource](#activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="22549-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="22549-226">В примере ниже данные из стандартной секции таблицы Azure копируются в большой двоичный объект каждый час.</span><span class="sxs-lookup"><span data-stu-id="22549-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="22549-227">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="22549-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="22549-228">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="22549-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="22549-229">Фабрика данных Azure поддерживает два типа связанных служб хранилища Azure: **AzureStorage** и **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="22549-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="22549-230">Для первой необходимо указать строку подключения, содержащую ключ учетной записи, а для второй — URI подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="22549-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="22549-231">Дополнительные сведения см. в разделе [Связанные службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="22549-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="22549-232">**Входной набор данных таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="22549-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="22549-233">В примере предполагается, что вы создали в таблице Azure таблицу MyTable.</span><span class="sxs-lookup"><span data-stu-id="22549-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="22549-234">Если параметру external присвоить значение true, фабрика данных воспримет этот набор данных как внешний и созданный не в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="22549-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="22549-235">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="22549-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="22549-236">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="22549-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="22549-237">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="22549-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="22549-238">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="22549-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="22549-239">**Действие копирования в конвейере с источником AzureTableSource и приемником BlobSink**</span><span class="sxs-lookup"><span data-stu-id="22549-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="22549-240">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="22549-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="22549-241">В определении JSON конвейера для типа **source** установлено значение **AzureTableSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="22549-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="22549-242">SQL-запрос, указанный в свойстве **AzureTableSourceQuery** , каждый час выбирает данные для копирования из стандартного раздела.</span><span class="sxs-lookup"><span data-stu-id="22549-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="22549-243">Пример. Копирование данных из большого двоичного объекта Azure в таблицу Azure</span><span class="sxs-lookup"><span data-stu-id="22549-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="22549-244">В примере ниже используется следующее:</span><span class="sxs-lookup"><span data-stu-id="22549-244">The following sample shows:</span></span>

1. <span data-ttu-id="22549-245">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (используется для таблиц и больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="22549-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="22549-246">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="22549-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="22549-247">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="22549-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="22549-248">[Конвейер](data-factory-create-pipelines.md) с действием копирования, которое использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="22549-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="22549-249">В этом примере данные временного ряда каждый час копируются из большого двоичного объекта Azure в таблицу Azure.</span><span class="sxs-lookup"><span data-stu-id="22549-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="22549-250">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="22549-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="22549-251">**Связанная служба хранилища Azure (для таблиц и больших двоичных объектов Azure)**:</span><span class="sxs-lookup"><span data-stu-id="22549-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="22549-252">Фабрика данных Azure поддерживает два типа связанных служб хранилища Azure: **AzureStorage** и **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="22549-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="22549-253">Для первой необходимо указать строку подключения, содержащую ключ учетной записи, а для второй — URI подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="22549-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="22549-254">Дополнительные сведения см. в разделе [Связанные службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="22549-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="22549-255">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="22549-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="22549-256">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="22549-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="22549-257">Путь к папке с BLOB-объектом и имя файла вычисляются динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="22549-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="22549-258">В пути к папке используется год, месяц и день начала, а в имени файла — час начала.</span><span class="sxs-lookup"><span data-stu-id="22549-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="22549-259">Когда для параметра external задано значение true, служба фабрики данных считает этот набор данных внешним по отношению к себе и не созданным в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="22549-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="22549-260">**Выходной набор данных таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="22549-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="22549-261">В этом примере данные копируются в таблицу MyTable, которая создана в таблице Azure.</span><span class="sxs-lookup"><span data-stu-id="22549-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="22549-262">Создайте таблицу Azure с количеством столбцов, которое должно быть в CSV-файле большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="22549-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="22549-263">Новые строки добавляются в таблицу каждый час.</span><span class="sxs-lookup"><span data-stu-id="22549-263">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="22549-264">**Действие копирования в конвейере с источником BlobSource и приемником AzureTableSink**</span><span class="sxs-lookup"><span data-stu-id="22549-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="22549-265">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="22549-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="22549-266">В определении JSON конвейера для типа **source** установлено значение **BlobSource**, а для типа **sink** — значение **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="22549-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="22549-267">Сопоставление типов для таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="22549-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="22549-268">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="22549-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="22549-269">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="22549-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="22549-270">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="22549-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="22549-271">При перемещении данных в таблицу Azure или из нее выполняется преобразование типов OData таблиц Azure в тип .NET (и наоборот) на основе указанных ниже [сопоставлений, определенных службой таблиц Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="22549-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="22549-272">Тип данных OData</span><span class="sxs-lookup"><span data-stu-id="22549-272">OData Data Type</span></span> | <span data-ttu-id="22549-273">Тип .NET</span><span class="sxs-lookup"><span data-stu-id="22549-273">.NET Type</span></span> | <span data-ttu-id="22549-274">Сведения</span><span class="sxs-lookup"><span data-stu-id="22549-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22549-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="22549-275">Edm.Binary</span></span> |<span data-ttu-id="22549-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="22549-276">byte[]</span></span> |<span data-ttu-id="22549-277">Массив байтов размером до 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="22549-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="22549-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="22549-278">Edm.Boolean</span></span> |<span data-ttu-id="22549-279">bool</span><span class="sxs-lookup"><span data-stu-id="22549-279">bool</span></span> |<span data-ttu-id="22549-280">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="22549-280">A Boolean value.</span></span> |
| <span data-ttu-id="22549-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="22549-281">Edm.DateTime</span></span> |<span data-ttu-id="22549-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="22549-282">DateTime</span></span> |<span data-ttu-id="22549-283">64-битное значение времени, выраженное в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="22549-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="22549-284">Допустимый диапазон времени начинается в 00:00 1 января 1601 года н. э.</span><span class="sxs-lookup"><span data-stu-id="22549-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="22549-285">Англиканское летоисчисление, часовой пояс — UTC.</span><span class="sxs-lookup"><span data-stu-id="22549-285">(C.E.), UTC.</span></span> <span data-ttu-id="22549-286">Заканчивается диапазон 31 декабря 9999 года.</span><span class="sxs-lookup"><span data-stu-id="22549-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="22549-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="22549-287">Edm.Double</span></span> |<span data-ttu-id="22549-288">double</span><span class="sxs-lookup"><span data-stu-id="22549-288">double</span></span> |<span data-ttu-id="22549-289">64-битное значение с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="22549-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="22549-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="22549-290">Edm.Guid</span></span> |<span data-ttu-id="22549-291">Guid</span><span class="sxs-lookup"><span data-stu-id="22549-291">Guid</span></span> |<span data-ttu-id="22549-292">128-битный идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="22549-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="22549-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="22549-293">Edm.Int32</span></span> |<span data-ttu-id="22549-294">Int32</span><span class="sxs-lookup"><span data-stu-id="22549-294">Int32</span></span> |<span data-ttu-id="22549-295">32-битное целое число.</span><span class="sxs-lookup"><span data-stu-id="22549-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="22549-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="22549-296">Edm.Int64</span></span> |<span data-ttu-id="22549-297">Int64</span><span class="sxs-lookup"><span data-stu-id="22549-297">Int64</span></span> |<span data-ttu-id="22549-298">64-битное целое число.</span><span class="sxs-lookup"><span data-stu-id="22549-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="22549-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="22549-299">Edm.String</span></span> |<span data-ttu-id="22549-300">Строка</span><span class="sxs-lookup"><span data-stu-id="22549-300">String</span></span> |<span data-ttu-id="22549-301">Значение в кодировке UTF-16.</span><span class="sxs-lookup"><span data-stu-id="22549-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="22549-302">Размер строкового значения не должен превышать 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="22549-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="22549-303">Пример преобразования типов</span><span class="sxs-lookup"><span data-stu-id="22549-303">Type Conversion Sample</span></span>
<span data-ttu-id="22549-304">В следующем примере данные копируются из BLOB-объекта Azure в таблицу Azure с преобразованием типов.</span><span class="sxs-lookup"><span data-stu-id="22549-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="22549-305">Предположим, набор данных большого двоичного объекта имеет формат CSV и содержит три столбца.</span><span class="sxs-lookup"><span data-stu-id="22549-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="22549-306">Один из них — это столбец даты и времени, в котором данные указаны в пользовательском формате (используются французские сокращения дней недели).</span><span class="sxs-lookup"><span data-stu-id="22549-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="22549-307">Определите исходный набор данных большого двоичного объекта и укажите определения типов столбцов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="22549-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

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
<span data-ttu-id="22549-308">Учитывая сопоставление типа OData таблицы Azure с типом .NET, таблицу в таблице Azure нужно определить посредством приведенной ниже схемы.</span><span class="sxs-lookup"><span data-stu-id="22549-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="22549-309">**Схема таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="22549-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="22549-310">Имя столбца</span><span class="sxs-lookup"><span data-stu-id="22549-310">Column name</span></span> | <span data-ttu-id="22549-311">Тип</span><span class="sxs-lookup"><span data-stu-id="22549-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="22549-312">userid</span><span class="sxs-lookup"><span data-stu-id="22549-312">userid</span></span> |<span data-ttu-id="22549-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="22549-313">Edm.Int64</span></span> |
| <span data-ttu-id="22549-314">name</span><span class="sxs-lookup"><span data-stu-id="22549-314">name</span></span> |<span data-ttu-id="22549-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="22549-315">Edm.String</span></span> |
| <span data-ttu-id="22549-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="22549-316">lastlogindate</span></span> |<span data-ttu-id="22549-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="22549-317">Edm.DateTime</span></span> |

<span data-ttu-id="22549-318">Далее нужно определить набор данных таблицы Azure, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="22549-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="22549-319">Указывать раздел structure с информацией о типах не нужно, так как типы уже указаны в базовом хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="22549-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

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

<span data-ttu-id="22549-320">В этом случае при перемещении данных из большого двоичного объекта в таблицу Azure фабрика данных автоматически преобразует типы (включая тип поля с датой и временем в пользовательском формате), используя язык и региональные параметры fr-fr.</span><span class="sxs-lookup"><span data-stu-id="22549-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="22549-321">Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в разделе [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="22549-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="22549-322">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="22549-322">Performance and Tuning</span></span>
<span data-ttu-id="22549-323">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md). В ней описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="22549-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
