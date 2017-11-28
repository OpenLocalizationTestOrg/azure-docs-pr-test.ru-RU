---
title: "наборы данных aaaCreate в фабрике данных Azure | Документы Microsoft"
description: "Узнайте, как смещение toocreate наборов данных в фабрике данных Azure, с примеры, использующие такие свойства, как и anchorDateTime."
keywords: "создание набора данных, пример набора данных, пример offset"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="45676-104">Наборы данных в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="45676-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="45676-105">В этой статье описывается, какие бывают наборы данных, каким образом они определяются в формате JSON, а также как они используются в конвейерах фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="45676-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="45676-106">Он предоставляет подробные сведения о каждом разделе (например, структуру, доступности и политики) в определение JSON набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="45676-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="45676-107">Hello статье также приводятся примеры использования hello **смещение**, **anchorDateTime**, и **стиль** свойства в определении JSON набора данных.</span><span class="sxs-lookup"><span data-stu-id="45676-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="45676-108">Новый tooData фабрики, в разделе [tooAzure введение фабрики данных](data-factory-introduction.md) Общие сведения.</span><span class="sxs-lookup"><span data-stu-id="45676-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="45676-109">Если у вас практический опыт работы с Создание фабрик данных, можно получить, лучше понять путем чтения hello [учебника преобразования данных](data-factory-build-your-first-pipeline.md) и hello [учебника перемещения данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="45676-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="45676-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="45676-110">Overview</span></span>
<span data-ttu-id="45676-111">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="45676-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="45676-112">**Конвейер** — это логическая группа **действий**, которые вместе выполняют задачу.</span><span class="sxs-lookup"><span data-stu-id="45676-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="45676-113">Hello действий в конвейере определить tooperform действия на данные.</span><span class="sxs-lookup"><span data-stu-id="45676-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="45676-114">Например можно использовать копирование данных toocopy действия из локального SQL Server tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="45676-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="45676-115">Затем можно использовать действия Hive, которое запускает сценарий Hive на данных tooprocess кластера Azure HDInsight из tooproduce выходные данные больших двоичных объектов хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="45676-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="45676-116">Наконец можно использовать второй копии действия toocopy hello вывода данных tooAzure хранилище данных SQL, поверх какие бизнес-аналитики (BI), отчетов, решения создаются.</span><span class="sxs-lookup"><span data-stu-id="45676-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="45676-117">Дополнительные сведения о конвейерах и действиях см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="45676-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="45676-118">У каждого действия может быть несколько входных **наборов данных** или же ни одного, и каждое действие может производить один или несколько выходных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="45676-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="45676-119">Входной набор данных представляет hello входных данных для действия в конвейере hello, а выходной набор данных представляет hello выходные данные для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="45676-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="45676-120">Наборы данных представляют данные в разных хранилищах, например в таблицах, файлах, папках и документах.</span><span class="sxs-lookup"><span data-stu-id="45676-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="45676-121">Например набор данных больших двоичных объектов Azure задает контейнер больших двоичных объектов hello и папку в хранилище больших двоичных объектов, из которого hello конвейера следует считывать данные hello.</span><span class="sxs-lookup"><span data-stu-id="45676-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="45676-122">Перед созданием набора данных, создать **связанная служба** toolink фабрики данных toohello хранения данных.</span><span class="sxs-lookup"><span data-stu-id="45676-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="45676-123">Связанные службы очень похожи на строки подключения, которые укажите сведения о подключении hello, необходимые для ресурсов tooexternal tooconnect фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="45676-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="45676-124">Наборы данных идентификации данных в пределах hello связаны хранилища данных, например таблиц SQL, файлы, папки и документы.</span><span class="sxs-lookup"><span data-stu-id="45676-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="45676-125">Например хранилище Azure связан ссылки на службу фабрики данных toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="45676-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="45676-126">Набор данных больших двоичных объектов Azure представляет контейнер больших двоичных объектов hello и hello папку, содержащую toobe входного BLOB-объектов hello обработки.</span><span class="sxs-lookup"><span data-stu-id="45676-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="45676-127">Ниже приведен пример сценария.</span><span class="sxs-lookup"><span data-stu-id="45676-127">Here is a sample scenario.</span></span> <span data-ttu-id="45676-128">toocopy данные из базы данных SQL tooa хранилища Blob, создать две связанные службы: служба хранилища Azure и базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="45676-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="45676-129">Затем создайте два набора данных: набор данных больших двоичных объектов Azure (которое означает toohello связанной службой хранилища Azure) и набор данных таблиц SQL Azure (которое означает службы toohello связана база данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="45676-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="45676-130">Здравствуйте, служба хранилища Azure и базы данных SQL Azure связанные службы содержат строки подключения, фабрики данных используется среда выполнения tooconnect tooyour хранилища Azure и базы данных SQL Azure, соответственно.</span><span class="sxs-lookup"><span data-stu-id="45676-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="45676-131">набор данных больших двоичных объектов Azure Hello указывает контейнер больших двоичных объектов hello и больших двоичных объектов папку, содержащую hello входного BLOB-объектов в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="45676-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="45676-132">набор данных таблиц SQL Azure Hello указывает, что таблицы SQL hello в данных hello toowhich базы данных SQL является toobe копируются.</span><span class="sxs-lookup"><span data-stu-id="45676-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="45676-133">Hello следующей схеме показаны связи hello между конвейера, действия, набор данных и связанной службы в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="45676-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Связь между конвейером, действием, набором данных и связанными службами](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="45676-135">JSON набора данных</span><span class="sxs-lookup"><span data-stu-id="45676-135">Dataset JSON</span></span>
<span data-ttu-id="45676-136">Набор данных в фабрике данных определяется в формате JSON, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="45676-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="45676-137">Привет, в следующей таблице описываются свойства в hello выше JSON:</span><span class="sxs-lookup"><span data-stu-id="45676-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="45676-138">Свойство</span><span class="sxs-lookup"><span data-stu-id="45676-138">Property</span></span> | <span data-ttu-id="45676-139">Описание</span><span class="sxs-lookup"><span data-stu-id="45676-139">Description</span></span> | <span data-ttu-id="45676-140">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45676-140">Required</span></span> | <span data-ttu-id="45676-141">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="45676-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="45676-142">name</span><span class="sxs-lookup"><span data-stu-id="45676-142">name</span></span> |<span data-ttu-id="45676-143">Имя набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="45676-143">Name of hello dataset.</span></span> <span data-ttu-id="45676-144">Правила именования для фабрики данных Azure описаны [здесь](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="45676-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="45676-145">Да</span><span class="sxs-lookup"><span data-stu-id="45676-145">Yes</span></span> |<span data-ttu-id="45676-146">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-146">NA</span></span> |
| <span data-ttu-id="45676-147">type</span><span class="sxs-lookup"><span data-stu-id="45676-147">type</span></span> |<span data-ttu-id="45676-148">Тип набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="45676-148">Type of hello dataset.</span></span> <span data-ttu-id="45676-149">Укажите один из типов hello, поддерживаемые фабрикой данных (например: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="45676-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="45676-150">Дополнительные сведения см. в разделе [Тип набора данных](#Type).</span><span class="sxs-lookup"><span data-stu-id="45676-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="45676-151">Да</span><span class="sxs-lookup"><span data-stu-id="45676-151">Yes</span></span> |<span data-ttu-id="45676-152">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-152">NA</span></span> |
| <span data-ttu-id="45676-153">structure</span><span class="sxs-lookup"><span data-stu-id="45676-153">structure</span></span> |<span data-ttu-id="45676-154">Схема набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="45676-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="45676-155">Дополнительные сведения см. в разделе [Структура набора данных](#Structure).</span><span class="sxs-lookup"><span data-stu-id="45676-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="45676-156">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-156">No</span></span> |<span data-ttu-id="45676-157">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-157">NA</span></span> |
| <span data-ttu-id="45676-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="45676-158">typeProperties</span></span> | <span data-ttu-id="45676-159">свойства типа Hello различны для каждого типа (например: BLOB-объектов Azure, таблице Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="45676-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="45676-160">Сведения о hello поддерживается типов и их свойств. в разделе [тип набора данных](#Type).</span><span class="sxs-lookup"><span data-stu-id="45676-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="45676-161">Да</span><span class="sxs-lookup"><span data-stu-id="45676-161">Yes</span></span> |<span data-ttu-id="45676-162">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-162">NA</span></span> |
| <span data-ttu-id="45676-163">external</span><span class="sxs-lookup"><span data-stu-id="45676-163">external</span></span> | <span data-ttu-id="45676-164">Логический флаг toospecify ли набор данных явно созданные конвейере фабрики данных или нет.</span><span class="sxs-lookup"><span data-stu-id="45676-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="45676-165">Если текущий конвейер hello не создается hello входного набора данных для действия, значение этого флага tootrue.</span><span class="sxs-lookup"><span data-stu-id="45676-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="45676-166">Установите этот флаг tootrue для hello входного набора данных hello первое действие в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="45676-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="45676-167">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-167">No</span></span> |<span data-ttu-id="45676-168">нет</span><span class="sxs-lookup"><span data-stu-id="45676-168">false</span></span> |
| <span data-ttu-id="45676-169">availability</span><span class="sxs-lookup"><span data-stu-id="45676-169">availability</span></span> | <span data-ttu-id="45676-170">Определяет hello обработки окна (например, раз в час или каждый день) или hello Фрагментирование модели для производства hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="45676-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="45676-171">Каждая единица данных, потребляемых и создаваемых запуском действия, называется срезом данных.</span><span class="sxs-lookup"><span data-stu-id="45676-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="45676-172">Если доступность hello выходной набор данных является набор toodaily (частота — день, интервал - 1), срез создается ежедневно.</span><span class="sxs-lookup"><span data-stu-id="45676-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="45676-173">Дополнительные сведения см. в разделе [Доступность набора данных](#Availability).</span><span class="sxs-lookup"><span data-stu-id="45676-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="45676-174">Сведения о наборе данных hello Фрагментирование модели, см. hello [планирования и выполнения](data-factory-scheduling-and-execution.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="45676-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="45676-175">Да</span><span class="sxs-lookup"><span data-stu-id="45676-175">Yes</span></span> |<span data-ttu-id="45676-176">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-176">NA</span></span> |
| <span data-ttu-id="45676-177">policy</span><span class="sxs-lookup"><span data-stu-id="45676-177">policy</span></span> |<span data-ttu-id="45676-178">Определяет условия hello или hello условие, которое необходимо выполнить все фрагменты hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="45676-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="45676-179">Дополнительные сведения см. в разделе hello [наборе данных политики](#Policy) раздела.</span><span class="sxs-lookup"><span data-stu-id="45676-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="45676-180">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-180">No</span></span> |<span data-ttu-id="45676-181">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="45676-182">Пример набора данных</span><span class="sxs-lookup"><span data-stu-id="45676-182">Dataset example</span></span>
<span data-ttu-id="45676-183">В следующем примере hello, набор данных hello представляет таблицу с именем **MyTable** в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="45676-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="45676-184">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="45676-184">Note hello following points:</span></span>

* <span data-ttu-id="45676-185">**Тип** имеет значение tooAzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="45676-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="45676-186">**tableName** свойство type (тип определенного tooAzureSqlTable) имеет значение tooMyTable.</span><span class="sxs-lookup"><span data-stu-id="45676-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="45676-187">**linkedServiceName** ссылается tooa связанной службы типа AzureSqlDatabase, которая определена в следующем фрагменте кода JSON hello.</span><span class="sxs-lookup"><span data-stu-id="45676-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="45676-188">**частота доступности** задано tooDay, и **интервал** имеет значение too1.</span><span class="sxs-lookup"><span data-stu-id="45676-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="45676-189">Это означает, что набор данных, hello срез создается ежедневно.</span><span class="sxs-lookup"><span data-stu-id="45676-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="45676-190">**AzureSqlLinkedService** определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="45676-190">**AzureSqlLinkedService** is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="45676-191">В hello предшествующий фрагмент JSON:</span><span class="sxs-lookup"><span data-stu-id="45676-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="45676-192">**Тип** имеет значение tooAzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="45676-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="45676-193">**connectionString** базы данных SQL tooa tooconnect сведения указывает тип свойства.</span><span class="sxs-lookup"><span data-stu-id="45676-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="45676-194">Как видите, hello связанной службы определяет как база данных SQL tooa tooconnect.</span><span class="sxs-lookup"><span data-stu-id="45676-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="45676-195">Hello набор данных определяет, какие таблицы используются как входные и выходные данные для действия "hello" в конвейере.</span><span class="sxs-lookup"><span data-stu-id="45676-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="45676-196">Если набор данных создается конвейером hello, он должен быть помечен как **внешних**.</span><span class="sxs-lookup"><span data-stu-id="45676-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="45676-197">Этот параметр применяется обычно tooinputs первого действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="45676-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="45676-198"><a name="Type"></a>Тип набора данных</span><span class="sxs-lookup"><span data-stu-id="45676-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="45676-199">Тип Hello hello набора данных зависит от hello хранилища данных, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="45676-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="45676-200">См. в следующей таблице список хранилищ данных, поддерживаемые фабрикой данных hello.</span><span class="sxs-lookup"><span data-stu-id="45676-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="45676-201">Нажмите кнопку toolearn хранилище данных как toocreate связанной службы и набор данных для их хранения.</span><span class="sxs-lookup"><span data-stu-id="45676-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="45676-202">Хранилища данных с * могут быть локальными или в IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="45676-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="45676-203">Эти хранилища данных требуется tooinstall [шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="45676-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="45676-204">В примере в предыдущем разделе hello hello hello типа hello набора данных задается слишком**AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="45676-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="45676-205">Аналогичным образом, для набора данных больших двоичных объектов Azure, типа hello hello набора данных задается слишком**AzureBlob**, как показано в следующих JSON hello:</span><span class="sxs-lookup"><span data-stu-id="45676-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <span data-ttu-id="45676-206"><a name="Structure"></a>Структура набора данных</span><span class="sxs-lookup"><span data-stu-id="45676-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="45676-207">Hello **структуры** раздел является необязательным.</span><span class="sxs-lookup"><span data-stu-id="45676-207">hello **structure** section is optional.</span></span> <span data-ttu-id="45676-208">Он определяет схему hello hello набора данных, содержащий коллекцию имена и типы данных столбцов.</span><span class="sxs-lookup"><span data-stu-id="45676-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="45676-209">Используется hello структуры раздел tooprovide сведений о типах, используемых tooconvert типы и сопоставлять столбцы из hello источник toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="45676-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="45676-210">В следующем примере hello, hello набор данных содержит три столбца: `slicetimestamp`, `projectname`, и `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="45676-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="45676-211">Они имеют типы String, String и Decimal соответственно.</span><span class="sxs-lookup"><span data-stu-id="45676-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="45676-212">Каждый столбец в структуре hello содержит hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="45676-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="45676-213">Свойство</span><span class="sxs-lookup"><span data-stu-id="45676-213">Property</span></span> | <span data-ttu-id="45676-214">Описание</span><span class="sxs-lookup"><span data-stu-id="45676-214">Description</span></span> | <span data-ttu-id="45676-215">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45676-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="45676-216">name</span><span class="sxs-lookup"><span data-stu-id="45676-216">name</span></span> |<span data-ttu-id="45676-217">Имя столбца hello.</span><span class="sxs-lookup"><span data-stu-id="45676-217">Name of hello column.</span></span> |<span data-ttu-id="45676-218">Да</span><span class="sxs-lookup"><span data-stu-id="45676-218">Yes</span></span> |
| <span data-ttu-id="45676-219">type</span><span class="sxs-lookup"><span data-stu-id="45676-219">type</span></span> |<span data-ttu-id="45676-220">Тип данных столбца hello.</span><span class="sxs-lookup"><span data-stu-id="45676-220">Data type of hello column.</span></span>  |<span data-ttu-id="45676-221">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-221">No</span></span> |
| <span data-ttu-id="45676-222">culture</span><span class="sxs-lookup"><span data-stu-id="45676-222">culture</span></span> |<span data-ttu-id="45676-223">. Toobe языка и региональных параметров на основе платформы .NET, используемый при hello тип является типом .NET: `Datetime` или `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="45676-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="45676-224">по умолчанию Hello — `en-us`.</span><span class="sxs-lookup"><span data-stu-id="45676-224">hello default is `en-us`.</span></span> |<span data-ttu-id="45676-225">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-225">No</span></span> |
| <span data-ttu-id="45676-226">свойства</span><span class="sxs-lookup"><span data-stu-id="45676-226">format</span></span> |<span data-ttu-id="45676-227">Форматировать toobe строки, использовавшейся hello тип является типом .NET: `Datetime` или `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="45676-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="45676-228">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-228">No</span></span> |

<span data-ttu-id="45676-229">Hello следующие рекомендации помогут определить, когда tooinclude структуры сведения и какие tooinclude в hello **структуры** раздела.</span><span class="sxs-lookup"><span data-stu-id="45676-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="45676-230">**Для источников данных, структурированный**, укажите раздел структуры hello только в том случае, если требуется сопоставить исходные столбцы toosink столбцы, и их имена не являются одинаковыми hello.</span><span class="sxs-lookup"><span data-stu-id="45676-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="45676-231">Данный тип источника структурированных данных хранит данные схемы и сведения о типе и сами данные hello.</span><span class="sxs-lookup"><span data-stu-id="45676-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="45676-232">Примерами структурированных источников данных являются SQL Server, Oracle и таблица Azure.</span><span class="sxs-lookup"><span data-stu-id="45676-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="45676-233">Как сведения о типе для структурированными источниками данных, при включении раздел структуры hello не должно содержать сведения о типе.</span><span class="sxs-lookup"><span data-stu-id="45676-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="45676-234">**Для схемы на источниках чтения данных (в частности, хранилище Blob)**, вы можете toostore данных без сохранения любой схемы или типа данных с использованием данных hello.</span><span class="sxs-lookup"><span data-stu-id="45676-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="45676-235">Для этих типов источников данных включают структуры при необходимости столбцы toosink toomap исходные столбцы.</span><span class="sxs-lookup"><span data-stu-id="45676-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="45676-236">Также включите структуры, когда hello набора данных включает входные данные для операции копирования, типы данных из исходного набора данных должны быть типы преобразованный toonative для приемника hello.</span><span class="sxs-lookup"><span data-stu-id="45676-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="45676-237">Фабрика данных поддерживает следующие значения для предоставления информации о типах в структуре hello: **Int16, Int32, Int64, один, Double, Decimal, Byte [], логическое значение, строка, Guid, Datetime, Datetimeoffset и Timespan**.</span><span class="sxs-lookup"><span data-stu-id="45676-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="45676-238">Это значения типов на основе .NET, совместимые со спецификацией CLS.</span><span class="sxs-lookup"><span data-stu-id="45676-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="45676-239">Фабрика данных автоматически выполняет преобразования типов при перемещении данных из источника данных в хранилище tooa приемник данных.</span><span class="sxs-lookup"><span data-stu-id="45676-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="45676-240">Доступность набора данных</span><span class="sxs-lookup"><span data-stu-id="45676-240">Dataset availability</span></span>
<span data-ttu-id="45676-241">Hello **доступности** в набор данных определяет hello окно обработки (например, каждый час, ежедневно или еженедельно) для набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="45676-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="45676-242">Дополнительные сведения об окнах действий см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="45676-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="45676-243">Hello в следующем разделе доступности указывает, что hello выходного набора данных либо создается каждый час, или входного набора данных hello доступна каждый час:</span><span class="sxs-lookup"><span data-stu-id="45676-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="45676-244">Если конвейер hello имеет hello после времени начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="45676-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="45676-245">Hello выходной набор данных создается каждый час в конвейер hello время начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="45676-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="45676-246">Таким образом, в этом конвейере создаются пять срезов набора данных — по одному для каждого окна действий (с 12:00 до 01:00, с 01:00 до 02:00, с 02:00 до 03:00, с 03:00 до 04:00, с 04:00 до 05:00).</span><span class="sxs-lookup"><span data-stu-id="45676-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="45676-247">Hello следующей таблице описываются свойства, которые можно использовать в разделе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="45676-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="45676-248">Свойство</span><span class="sxs-lookup"><span data-stu-id="45676-248">Property</span></span> | <span data-ttu-id="45676-249">Описание</span><span class="sxs-lookup"><span data-stu-id="45676-249">Description</span></span> | <span data-ttu-id="45676-250">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45676-250">Required</span></span> | <span data-ttu-id="45676-251">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="45676-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="45676-252">frequency</span><span class="sxs-lookup"><span data-stu-id="45676-252">frequency</span></span> |<span data-ttu-id="45676-253">Указывает единицу времени hello для производственного среза набора данных.</span><span class="sxs-lookup"><span data-stu-id="45676-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="45676-254"><b>Поддерживаемые значения</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="45676-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="45676-255">Да</span><span class="sxs-lookup"><span data-stu-id="45676-255">Yes</span></span> |<span data-ttu-id="45676-256">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-256">NA</span></span> |
| <span data-ttu-id="45676-257">interval</span><span class="sxs-lookup"><span data-stu-id="45676-257">interval</span></span> |<span data-ttu-id="45676-258">Задает множитель для частоты.</span><span class="sxs-lookup"><span data-stu-id="45676-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="45676-259">«Интервал частоты x» определяет, как часто hello срезов.</span><span class="sxs-lookup"><span data-stu-id="45676-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="45676-260">К примеру, если требуется hello срез в час toobe набора данных, можно установить <b>частоты</b> слишком<b>час</b>, и <b>интервал</b> слишком<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="45676-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="45676-261">Обратите внимание, что при указании **частоты** как **минуту**, необходимо задать toono hello интервал меньше 15.</span><span class="sxs-lookup"><span data-stu-id="45676-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="45676-262">Да</span><span class="sxs-lookup"><span data-stu-id="45676-262">Yes</span></span> |<span data-ttu-id="45676-263">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-263">NA</span></span> |
| <span data-ttu-id="45676-264">style</span><span class="sxs-lookup"><span data-stu-id="45676-264">style</span></span> |<span data-ttu-id="45676-265">Указывает, является ли hello срезов hello начало или конец интервал приветствия.</span><span class="sxs-lookup"><span data-stu-id="45676-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="45676-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="45676-266">StartOfInterval</span></span></li><li><span data-ttu-id="45676-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="45676-267">EndOfInterval</span></span></li></ul><span data-ttu-id="45676-268">Если **частоты** задано слишком**месяц**, и **стиль** задано слишком**EndOfInterval**, hello срез создается hello последний день месяца.</span><span class="sxs-lookup"><span data-stu-id="45676-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="45676-269">Если **стиль** задано слишком**StartOfInterval**, hello срезов на hello первый день месяца.</span><span class="sxs-lookup"><span data-stu-id="45676-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="45676-270">Если **частоты** задано слишком**день**, и **стиль** задано слишком**EndOfInterval**, hello срезов в hello последний час дня hello.</span><span class="sxs-lookup"><span data-stu-id="45676-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="45676-271">Если **частоты** задано слишком**час**, и **стиль** задано слишком**EndOfInterval**, hello срезов в конце hello hello час.</span><span class="sxs-lookup"><span data-stu-id="45676-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="45676-272">Например для среза для hello период 13: 00 - 14 по hello срез создается в 14: 00.</span><span class="sxs-lookup"><span data-stu-id="45676-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="45676-273">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-273">No</span></span> |<span data-ttu-id="45676-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="45676-274">EndOfInterval</span></span> |
| <span data-ttu-id="45676-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="45676-275">anchorDateTime</span></span> |<span data-ttu-id="45676-276">Определяет hello абсолютное позиционирование в времени, затраченного границ фрагмента dataset toocompute планировщика hello.</span><span class="sxs-lookup"><span data-stu-id="45676-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="45676-277">Обратите внимание, что если этот propoerty частей даты, которые являются более детализированными, чем hello указано частоты, hello более детализированные части игнорируются.</span><span class="sxs-lookup"><span data-stu-id="45676-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="45676-278">Например, если hello **интервал** — **каждый час** (частота: час и интервал: 1) и hello **anchorDateTime** содержит **минуты и секунды**, затем hello минуты и секунды части **anchorDateTime** игнорируются.</span><span class="sxs-lookup"><span data-stu-id="45676-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="45676-279">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-279">No</span></span> |<span data-ttu-id="45676-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="45676-280">01/01/0001</span></span> |
| <span data-ttu-id="45676-281">offset</span><span class="sxs-lookup"><span data-stu-id="45676-281">offset</span></span> |<span data-ttu-id="45676-282">Интервал времени, по которой hello Сдвиг начала и окончания всех фрагментов набора данных.</span><span class="sxs-lookup"><span data-stu-id="45676-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="45676-283">Обратите внимание, что, если оба **anchorDateTime** и **смещение** указан, результат hello shift hello вместе.</span><span class="sxs-lookup"><span data-stu-id="45676-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="45676-284">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-284">No</span></span> |<span data-ttu-id="45676-285">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="45676-286">Пример смещения</span><span class="sxs-lookup"><span data-stu-id="45676-286">offset example</span></span>
<span data-ttu-id="45676-287">По умолчанию ежедневные срезы (`"frequency": "Day", "interval": 1`) создаются в 00.00 (в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="45676-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="45676-288">Время hello начала времени toobe 6: 00 UTC вместо этого, установите hello смещение, как показано в следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="45676-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="45676-289">Пример для anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="45676-289">anchorDateTime example</span></span>
<span data-ttu-id="45676-290">В следующем примере hello hello набора данных создаются каждые 23 часа.</span><span class="sxs-lookup"><span data-stu-id="45676-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="45676-291">Hello первого сегмента начинается hello времени, заданного параметром **anchorDateTime**, который установлен слишком`2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="45676-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="45676-292">Пример для offset и style</span><span class="sxs-lookup"><span data-stu-id="45676-292">offset/style example</span></span>
<span data-ttu-id="45676-293">Hello следующий набор данных — ежемесячно и выводятся на hello 3-й день каждого месяца в 8:00 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="45676-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="45676-294"><a name="Policy"></a>Политика наборов данных</span><span class="sxs-lookup"><span data-stu-id="45676-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="45676-295">Hello **политики** в определения набора данных hello определяет критерии hello или необходимо выполнить условие hello, hello фрагментов набора данных.</span><span class="sxs-lookup"><span data-stu-id="45676-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="45676-296">Политики проверки</span><span class="sxs-lookup"><span data-stu-id="45676-296">Validation policies</span></span>
| <span data-ttu-id="45676-297">Имя политики</span><span class="sxs-lookup"><span data-stu-id="45676-297">Policy name</span></span> | <span data-ttu-id="45676-298">Описание</span><span class="sxs-lookup"><span data-stu-id="45676-298">Description</span></span> | <span data-ttu-id="45676-299">Применить слишком</span><span class="sxs-lookup"><span data-stu-id="45676-299">Applied too</span></span>| <span data-ttu-id="45676-300">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45676-300">Required</span></span> | <span data-ttu-id="45676-301">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="45676-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="45676-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="45676-302">minimumSizeMB</span></span> |<span data-ttu-id="45676-303">Проверяет, данные hello в **хранилища больших двоичных объектов Azure** соответствует hello требования минимальный размер (в мегабайтах).</span><span class="sxs-lookup"><span data-stu-id="45676-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="45676-304">Хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="45676-304">Azure Blob storage</span></span> |<span data-ttu-id="45676-305">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-305">No</span></span> |<span data-ttu-id="45676-306">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-306">NA</span></span> |
| <span data-ttu-id="45676-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="45676-307">minimumRows</span></span> |<span data-ttu-id="45676-308">Проверяет, данные hello в **базы данных Azure SQL** или **таблицы Azure** содержит hello минимальное количество строк.</span><span class="sxs-lookup"><span data-stu-id="45676-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="45676-309">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="45676-309">Azure SQL database</span></span></li><li><span data-ttu-id="45676-310">таблицу Azure;</span><span class="sxs-lookup"><span data-stu-id="45676-310">Azure table</span></span></li></ul> |<span data-ttu-id="45676-311">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-311">No</span></span> |<span data-ttu-id="45676-312">Нет данных</span><span class="sxs-lookup"><span data-stu-id="45676-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="45676-313">Примеры</span><span class="sxs-lookup"><span data-stu-id="45676-313">Examples</span></span>
<span data-ttu-id="45676-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="45676-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="45676-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="45676-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="45676-316">Внешние наборы данных</span><span class="sxs-lookup"><span data-stu-id="45676-316">External datasets</span></span>
<span data-ttu-id="45676-317">Внешних наборов данных являются те, которые не создают выполнение конвейера в фабрике данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="45676-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="45676-318">Если набор данных hello помечен как **внешних**, hello **ExternalData** политики может быть определенный tooinfluence поведение hello доступности срез hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="45676-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="45676-319">Если набор данных не создается фабрикой данных, он должен быть помечен как **external**.</span><span class="sxs-lookup"><span data-stu-id="45676-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="45676-320">Этот параметр обычно применяется toohello вводов первое действие в конвейере, если не используется действие или цепочки конвейера.</span><span class="sxs-lookup"><span data-stu-id="45676-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="45676-321">Имя</span><span class="sxs-lookup"><span data-stu-id="45676-321">Name</span></span> | <span data-ttu-id="45676-322">Описание</span><span class="sxs-lookup"><span data-stu-id="45676-322">Description</span></span> | <span data-ttu-id="45676-323">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45676-323">Required</span></span> | <span data-ttu-id="45676-324">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="45676-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="45676-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="45676-325">dataDelay</span></span> |<span data-ttu-id="45676-326">срез указано время Hello, toodelay hello проверьте на наличие hello hello внешних данных для hello.</span><span class="sxs-lookup"><span data-stu-id="45676-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="45676-327">Например, вы можете отложить ежечасную проверку с помощью этого параметра.</span><span class="sxs-lookup"><span data-stu-id="45676-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="45676-328">Hello параметр применяется только toohello текущего времени.</span><span class="sxs-lookup"><span data-stu-id="45676-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="45676-329">Например если это 1:00 PM в данный момент, и это значение составляет 10 минут, проверки hello начинается в 13:10.</span><span class="sxs-lookup"><span data-stu-id="45676-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="45676-330">Обратите внимание, что этот параметр не влияет на срезы в прошлом hello.</span><span class="sxs-lookup"><span data-stu-id="45676-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="45676-331">Срезы, у которых параметры **Slice End Time**  + и **dataDelay**  < **имеют значение раньше текущего времени**, обрабатываются без задержки.</span><span class="sxs-lookup"><span data-stu-id="45676-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="45676-332">Раз больше 23:59 часов указывается с помощью hello `day.hours:minutes:seconds` формат.</span><span class="sxs-lookup"><span data-stu-id="45676-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="45676-333">Например toospecify 24 часа, не используйте 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="45676-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="45676-334">Вместо этого используйте 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="45676-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="45676-335">Значение 24:00:00 обозначает 24 дня (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="45676-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="45676-336">Чтобы задать 1 день и 4 часа, укажите 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="45676-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="45676-337">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-337">No</span></span> |<span data-ttu-id="45676-338">0</span><span class="sxs-lookup"><span data-stu-id="45676-338">0</span></span> |
| <span data-ttu-id="45676-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="45676-339">retryInterval</span></span> |<span data-ttu-id="45676-340">время ожидания Hello между сбоя и hello следующей попытки.</span><span class="sxs-lookup"><span data-stu-id="45676-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="45676-341">Этот параметр применяется toopresent времени.</span><span class="sxs-lookup"><span data-stu-id="45676-341">This setting applies toopresent time.</span></span> <span data-ttu-id="45676-342">Если предыдущие try hello не пройден, hello следующей попытки после hello **retryInterval** период.</span><span class="sxs-lookup"><span data-stu-id="45676-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="45676-343">Если это 1:00 PM прямо сейчас мы начинаем hello первой попытки.</span><span class="sxs-lookup"><span data-stu-id="45676-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="45676-344">Если hello длительность toocomplete hello первой проверки — 1 минута и не удалось выполнить операцию hello, hello следующий Повтор — 1:00 + 1 минута (длительность) + 1 минута (интервал повтора) = 13:02:00.</span><span class="sxs-lookup"><span data-stu-id="45676-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="45676-345">Срезы в прошлом hello нет без задержки.</span><span class="sxs-lookup"><span data-stu-id="45676-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="45676-346">Повторите попытку Hello происходит немедленно.</span><span class="sxs-lookup"><span data-stu-id="45676-346">hello retry happens immediately.</span></span> |<span data-ttu-id="45676-347">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-347">No</span></span> |<span data-ttu-id="45676-348">00:01:00 (1 минута)</span><span class="sxs-lookup"><span data-stu-id="45676-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="45676-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="45676-349">retryTimeout</span></span> |<span data-ttu-id="45676-350">Здравствуйте, время ожидания для каждой повторной попытке.</span><span class="sxs-lookup"><span data-stu-id="45676-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="45676-351">Если это свойство имеет значение минут too10 hello проверки должна быть завершена в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="45676-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="45676-352">Если он занимает больше 10 минут tooperform hello проверки, hello повторите истечением времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="45676-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="45676-353">Если все попытки для hello истечет время ожидания, hello среза помечается как **TimedOut**.</span><span class="sxs-lookup"><span data-stu-id="45676-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="45676-354">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-354">No</span></span> |<span data-ttu-id="45676-355">00:10:00 (10 минут)</span><span class="sxs-lookup"><span data-stu-id="45676-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="45676-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="45676-356">maximumRetry</span></span> |<span data-ttu-id="45676-357">Hello время toocheck для обеспечения доступности hello hello внешних данных.</span><span class="sxs-lookup"><span data-stu-id="45676-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="45676-358">Hello максимальное допустимое значение — 10.</span><span class="sxs-lookup"><span data-stu-id="45676-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="45676-359">Нет</span><span class="sxs-lookup"><span data-stu-id="45676-359">No</span></span> |<span data-ttu-id="45676-360">3</span><span class="sxs-lookup"><span data-stu-id="45676-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="45676-361">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="45676-361">Create datasets</span></span>
<span data-ttu-id="45676-362">Наборы данных можно создать с помощью одного из указанных ниже инструментов или пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="45676-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="45676-363">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="45676-363">Copy Wizard</span></span> 
- <span data-ttu-id="45676-364">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="45676-364">Azure portal</span></span>
- <span data-ttu-id="45676-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45676-365">Visual Studio</span></span>
- <span data-ttu-id="45676-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45676-366">PowerShell</span></span>
- <span data-ttu-id="45676-367">Шаблон диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="45676-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="45676-368">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="45676-368">REST API</span></span>
- <span data-ttu-id="45676-369">.NET API</span><span class="sxs-lookup"><span data-stu-id="45676-369">.NET API</span></span>

<span data-ttu-id="45676-370">См. следующие учебники пошаговые инструкции по созданию конвейеры и наборов данных с помощью одного из этих средств или пакеты SDK hello.</span><span class="sxs-lookup"><span data-stu-id="45676-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="45676-371">Учебник. Создание первого конвейера для преобразования данных с помощью кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="45676-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="45676-372">Руководство. Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных</span><span class="sxs-lookup"><span data-stu-id="45676-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="45676-373">После создания и развертывания конвейера можно управлять и отслеживать конвейеров с помощью hello Azure портала колонках или приложение hello наблюдения и управления.</span><span class="sxs-lookup"><span data-stu-id="45676-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="45676-374">См. следующие разделы для получения пошаговых инструкций hello.</span><span class="sxs-lookup"><span data-stu-id="45676-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="45676-375">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью портала Azure и PowerShell</span><span class="sxs-lookup"><span data-stu-id="45676-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="45676-376">Мониторинг и управление ими конвейеров с помощью приложения hello мониторинг и управление</span><span class="sxs-lookup"><span data-stu-id="45676-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="45676-377">Контекст наборов данных</span><span class="sxs-lookup"><span data-stu-id="45676-377">Scoped datasets</span></span>
<span data-ttu-id="45676-378">Можно создать наборы данных, которые с помощью hello конвейера с областью tooa **наборы данных** свойство.</span><span class="sxs-lookup"><span data-stu-id="45676-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="45676-379">Такие наборы данных могут использоваться только действиями в пределах указанного конвейера, но не действиями в других конвейерах.</span><span class="sxs-lookup"><span data-stu-id="45676-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="45676-380">Следующий пример Hello определяет конвейера с помощью двух наборов данных (InputDataset rdc и OutputDataset rdc) toobe, используемых в конвейер hello.</span><span class="sxs-lookup"><span data-stu-id="45676-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="45676-381">Наборы с областью данных поддерживаются только при наличии одноразовый конвейеров (где **pipelineMode** задано слишком**OneTime**).</span><span class="sxs-lookup"><span data-stu-id="45676-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="45676-382">Дополнительные сведения см. в разделе [Однократный конвейер](data-factory-create-pipelines.md#onetime-pipeline).</span><span class="sxs-lookup"><span data-stu-id="45676-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="45676-383">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="45676-383">Next steps</span></span>
- <span data-ttu-id="45676-384">Дополнительные сведения о конвейерах см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="45676-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="45676-385">Дополнительные сведения о планировании и выполнении конвейеров см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="45676-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
