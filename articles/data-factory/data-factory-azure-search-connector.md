---
title: "Индекс tooSearch aaaPush данных с помощью фабрики данных | Документы Microsoft"
description: "Дополнительные сведения о данных toopush tooAzure индекс поиска с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="96bc2-103">Извещающие индекс поиска Azure tooan данных с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="96bc2-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="96bc2-104">В этой статье описывается, как tooAzure поиска индекса хранилища данных toopush toouse hello действие копирования из поддерживаемых исходных данных.</span><span class="sxs-lookup"><span data-stu-id="96bc2-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="96bc2-105">Поддерживаемой исходной хранилищ данных, перечислены в исходный столбец hello hello [поддерживаемые источники и приемники](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="96bc2-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="96bc2-106">Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования и сочетания поддерживаемых данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="96bc2-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="96bc2-107">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="96bc2-107">Enabling connectivity</span></span>
<span data-ttu-id="96bc2-108">Служба фабрики данных tooallow подключения tooan к локальному хранилищу данных, установить шлюз управления данными в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="96bc2-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="96bc2-109">Можно установить шлюз на hello того же компьютера, на котором размещен источник данных hello хранения или на отдельном компьютере tooavoid, конкурирующие за ресурсы с данными hello хранилище.</span><span class="sxs-lookup"><span data-stu-id="96bc2-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="96bc2-110">Шлюз управления данными подключается локальными службами toocloud источники данных в виде безопасности и управления.</span><span class="sxs-lookup"><span data-stu-id="96bc2-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="96bc2-111">Сведения о шлюзе управления данными см. в статье [Перемещение данных между локальными источниками и облаком](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="96bc2-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="96bc2-112">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="96bc2-112">Getting started</span></span>
<span data-ttu-id="96bc2-113">Можно создать конвейер действием копирования, которое передает данные из индекса поиска tooAzure источника данных хранилища с помощью различных средств и API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="96bc2-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="96bc2-114">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="96bc2-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="96bc2-115">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="96bc2-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="96bc2-116">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="96bc2-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="96bc2-117">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="96bc2-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="96bc2-118">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="96bc2-119">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="96bc2-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="96bc2-120">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="96bc2-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="96bc2-121">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="96bc2-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="96bc2-122">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="96bc2-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="96bc2-123">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="96bc2-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="96bc2-124">Пример с определениями JSON для сущностей фабрики данных, которые являются индекс поиска tooAzure данных используется toocopy см [пример JSON: скопировать данные из индекса поиска tooAzure SQL Server в локальной](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="96bc2-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="96bc2-125">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAzure индекс поиска:</span><span class="sxs-lookup"><span data-stu-id="96bc2-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="96bc2-126">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="96bc2-126">Linked service properties</span></span>

<span data-ttu-id="96bc2-127">Привет, в следующей таблице приводится описание службы поиска Azure связаны определенные toohello элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="96bc2-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="96bc2-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="96bc2-128">Property</span></span> | <span data-ttu-id="96bc2-129">Описание</span><span class="sxs-lookup"><span data-stu-id="96bc2-129">Description</span></span> | <span data-ttu-id="96bc2-130">Обязательно</span><span class="sxs-lookup"><span data-stu-id="96bc2-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="96bc2-131">type</span><span class="sxs-lookup"><span data-stu-id="96bc2-131">type</span></span> | <span data-ttu-id="96bc2-132">свойство типа Hello должно быть присвоено: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="96bc2-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="96bc2-133">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-133">Yes</span></span> |
| <span data-ttu-id="96bc2-134">url</span><span class="sxs-lookup"><span data-stu-id="96bc2-134">url</span></span> | <span data-ttu-id="96bc2-135">URL-адрес для службы поиска Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="96bc2-136">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-136">Yes</span></span> |
| <span data-ttu-id="96bc2-137">key</span><span class="sxs-lookup"><span data-stu-id="96bc2-137">key</span></span> | <span data-ttu-id="96bc2-138">Ключ администратора для hello службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="96bc2-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="96bc2-139">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="96bc2-140">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="96bc2-140">Dataset properties</span></span>

<span data-ttu-id="96bc2-141">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="96bc2-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="96bc2-142">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.</span><span class="sxs-lookup"><span data-stu-id="96bc2-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="96bc2-143">Hello **typeProperties** раздела отличается для каждого типа набора данных.</span><span class="sxs-lookup"><span data-stu-id="96bc2-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="96bc2-144">Hello typeProperties статьи для набора данных типа hello **AzureSearchIndex** имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="96bc2-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="96bc2-145">Свойство</span><span class="sxs-lookup"><span data-stu-id="96bc2-145">Property</span></span> | <span data-ttu-id="96bc2-146">Описание</span><span class="sxs-lookup"><span data-stu-id="96bc2-146">Description</span></span> | <span data-ttu-id="96bc2-147">Обязательно</span><span class="sxs-lookup"><span data-stu-id="96bc2-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="96bc2-148">type</span><span class="sxs-lookup"><span data-stu-id="96bc2-148">type</span></span> | <span data-ttu-id="96bc2-149">свойство типа Hello должно быть задано слишком**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="96bc2-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="96bc2-150">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-150">Yes</span></span> |
| <span data-ttu-id="96bc2-151">indexName</span><span class="sxs-lookup"><span data-stu-id="96bc2-151">indexName</span></span> | <span data-ttu-id="96bc2-152">Имя индекса поиска Azure hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="96bc2-153">Фабрика данных hello индекс не создается.</span><span class="sxs-lookup"><span data-stu-id="96bc2-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="96bc2-154">Hello индекс должен существовать в поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="96bc2-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="96bc2-155">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="96bc2-156">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="96bc2-156">Copy activity properties</span></span>
<span data-ttu-id="96bc2-157">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="96bc2-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="96bc2-158">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="96bc2-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="96bc2-159">В то время как свойства в разделе "typeProperties" hello, зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="96bc2-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="96bc2-160">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="96bc2-161">Для действия копирования, если приемник hello имеет тип hello **AzureSearchIndexSink**, hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="96bc2-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="96bc2-162">Свойство</span><span class="sxs-lookup"><span data-stu-id="96bc2-162">Property</span></span> | <span data-ttu-id="96bc2-163">Описание</span><span class="sxs-lookup"><span data-stu-id="96bc2-163">Description</span></span> | <span data-ttu-id="96bc2-164">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="96bc2-164">Allowed values</span></span> | <span data-ttu-id="96bc2-165">Обязательно</span><span class="sxs-lookup"><span data-stu-id="96bc2-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="96bc2-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="96bc2-166">WriteBehavior</span></span> | <span data-ttu-id="96bc2-167">Указывает ли toomerge или замены, если документ уже существует в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="96bc2-168">В разделе hello [WriteBehavior свойства](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="96bc2-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="96bc2-169">Merge (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="96bc2-169">Merge (default)</span></span><br/><span data-ttu-id="96bc2-170">Отправить</span><span class="sxs-lookup"><span data-stu-id="96bc2-170">Upload</span></span>| <span data-ttu-id="96bc2-171">Нет</span><span class="sxs-lookup"><span data-stu-id="96bc2-171">No</span></span> |
| <span data-ttu-id="96bc2-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="96bc2-172">WriteBatchSize</span></span> | <span data-ttu-id="96bc2-173">Передает данные в индекс поиска Azure hello достижении writeBatchSize hello размер буфера.</span><span class="sxs-lookup"><span data-stu-id="96bc2-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="96bc2-174">В разделе hello [WriteBatchSize свойство](#writebatchsize-property) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="96bc2-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="96bc2-175">1 too1 000.</span><span class="sxs-lookup"><span data-stu-id="96bc2-175">1 too1,000.</span></span> <span data-ttu-id="96bc2-176">Значение по умолчанию — 1000.</span><span class="sxs-lookup"><span data-stu-id="96bc2-176">Default value is 1000.</span></span> | <span data-ttu-id="96bc2-177">Нет</span><span class="sxs-lookup"><span data-stu-id="96bc2-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="96bc2-178">Свойство WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="96bc2-178">WriteBehavior property</span></span>
<span data-ttu-id="96bc2-179">При записи данных AzureSearchSink выполняет операцию upsert.</span><span class="sxs-lookup"><span data-stu-id="96bc2-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="96bc2-180">Другими словами при создании документа, если ключ документа hello уже существует в индекс поиска Azure hello, поиска Azure обновляет существующий документ hello, а не исключения конфликтов.</span><span class="sxs-lookup"><span data-stu-id="96bc2-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="96bc2-181">Hello AzureSearchSink предоставляет hello, следующие два поведения upsert (с помощью пакета SDK AzureSearch):</span><span class="sxs-lookup"><span data-stu-id="96bc2-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="96bc2-182">**Слияние**: объединение всех столбцов hello в новый документ hello с существующие один hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="96bc2-183">Для столбцов со значением null в новый документ hello hello значение hello существующих один сохраняется.</span><span class="sxs-lookup"><span data-stu-id="96bc2-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="96bc2-184">**Отправка**: hello новый документ заменяет hello существующий.</span><span class="sxs-lookup"><span data-stu-id="96bc2-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="96bc2-185">Для столбцов, не указанных в новый документ hello hello значение toonull есть ли ненулевое значение в существующем документе hello или нет.</span><span class="sxs-lookup"><span data-stu-id="96bc2-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="96bc2-186">по умолчанию Hello **слияния**.</span><span class="sxs-lookup"><span data-stu-id="96bc2-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="96bc2-187">Свойство WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="96bc2-187">WriteBatchSize Property</span></span>
<span data-ttu-id="96bc2-188">Служба Поиска Azure поддерживает запись документов в виде пакета.</span><span class="sxs-lookup"><span data-stu-id="96bc2-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="96bc2-189">Пакет может содержать 1 too1, 000 действия.</span><span class="sxs-lookup"><span data-stu-id="96bc2-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="96bc2-190">Действие, которое обрабатывает одной операции отправки или слияния hello tooperform документа.</span><span class="sxs-lookup"><span data-stu-id="96bc2-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="96bc2-191">Поддержка типов данных</span><span class="sxs-lookup"><span data-stu-id="96bc2-191">Data type support</span></span>
<span data-ttu-id="96bc2-192">Hello следующей таблице указывает, поддерживается ли тип данных поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="96bc2-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="96bc2-193">Тип данных Поиска Azure</span><span class="sxs-lookup"><span data-stu-id="96bc2-193">Azure Search data type</span></span> | <span data-ttu-id="96bc2-194">Поддерживается в приемнике Поиска Azure</span><span class="sxs-lookup"><span data-stu-id="96bc2-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="96bc2-195">Строка</span><span class="sxs-lookup"><span data-stu-id="96bc2-195">String</span></span> | <span data-ttu-id="96bc2-196">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-196">Y</span></span> |
| <span data-ttu-id="96bc2-197">Int32</span><span class="sxs-lookup"><span data-stu-id="96bc2-197">Int32</span></span> | <span data-ttu-id="96bc2-198">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-198">Y</span></span> |
| <span data-ttu-id="96bc2-199">Int64</span><span class="sxs-lookup"><span data-stu-id="96bc2-199">Int64</span></span> | <span data-ttu-id="96bc2-200">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-200">Y</span></span> |
| <span data-ttu-id="96bc2-201">Double</span><span class="sxs-lookup"><span data-stu-id="96bc2-201">Double</span></span> | <span data-ttu-id="96bc2-202">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-202">Y</span></span> |
| <span data-ttu-id="96bc2-203">Логический</span><span class="sxs-lookup"><span data-stu-id="96bc2-203">Boolean</span></span> | <span data-ttu-id="96bc2-204">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-204">Y</span></span> |
| <span data-ttu-id="96bc2-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="96bc2-205">DataTimeOffset</span></span> | <span data-ttu-id="96bc2-206">Да</span><span class="sxs-lookup"><span data-stu-id="96bc2-206">Y</span></span> |
| <span data-ttu-id="96bc2-207">Массив строк</span><span class="sxs-lookup"><span data-stu-id="96bc2-207">String Array</span></span> | <span data-ttu-id="96bc2-208">Нет</span><span class="sxs-lookup"><span data-stu-id="96bc2-208">N</span></span> |
| <span data-ttu-id="96bc2-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="96bc2-209">GeographyPoint</span></span> | <span data-ttu-id="96bc2-210">Нет</span><span class="sxs-lookup"><span data-stu-id="96bc2-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="96bc2-211">Пример JSON: копирование данных из индекса поиска tooAzure в локальной среде SQL Server</span><span class="sxs-lookup"><span data-stu-id="96bc2-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="96bc2-212">Hello следующем образце показано:</span><span class="sxs-lookup"><span data-stu-id="96bc2-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="96bc2-213">Связанная служба типа [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="96bc2-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="96bc2-214">Связанная служба типа [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="96bc2-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="96bc2-215">Входной [набор данных](data-factory-create-datasets.md) типа [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="96bc2-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="96bc2-216">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="96bc2-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="96bc2-217">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) и [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="96bc2-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="96bc2-218">Образец Hello копирует данные временного ряда из индекса поиска Azure tooan базы данных SQL Server в локальной каждый час.</span><span class="sxs-lookup"><span data-stu-id="96bc2-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="96bc2-219">свойства JSON Hello, используемый в этом примере описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="96bc2-220">В качестве первого шага установки hello шлюз управления данными на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="96bc2-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="96bc2-221">Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="96bc2-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="96bc2-222">**Связанная служба Поиска Azure:**</span><span class="sxs-lookup"><span data-stu-id="96bc2-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="96bc2-223">**Связанная служба SQL Server**</span><span class="sxs-lookup"><span data-stu-id="96bc2-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="96bc2-224">**Входной набор данных SQL Server**</span><span class="sxs-lookup"><span data-stu-id="96bc2-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="96bc2-225">Образец Hello предполагается создания таблицы «MyTable» в SQL Server, и она содержит столбец с именем «timestampcolumn» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="96bc2-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="96bc2-226">Вы можете запрашивать через несколько таблиц в одной базе данных с помощью одного набора данных, но одна таблица должна использоваться для набора данных hello tableName typeProperty приветствия.</span><span class="sxs-lookup"><span data-stu-id="96bc2-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="96bc2-227">Параметр «external»: «true» уведомляет службу фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

<span data-ttu-id="96bc2-228">**Выходной набор данных Поиска Azure:**</span><span class="sxs-lookup"><span data-stu-id="96bc2-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="96bc2-229">Hello образец копий данных tooan индекс поиска Azure с именем **продуктов**.</span><span class="sxs-lookup"><span data-stu-id="96bc2-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="96bc2-230">Фабрика данных hello индекс не создается.</span><span class="sxs-lookup"><span data-stu-id="96bc2-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="96bc2-231">tootest hello образца, создайте индекс с таким именем.</span><span class="sxs-lookup"><span data-stu-id="96bc2-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="96bc2-232">Создайте индекс поиска Azure hello с hello столько же столбцов, как и hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="96bc2-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="96bc2-233">Новые записи добавляются в индекс поиска Azure toohello каждый час.</span><span class="sxs-lookup"><span data-stu-id="96bc2-233">New entries are added toohello Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="96bc2-234">**Действие копирования в конвейере со средой SQL в качестве источника и индексом Поиска Azure в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="96bc2-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="96bc2-235">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="96bc2-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="96bc2-236">В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlSource** и **приемник** тип установлен слишком**AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="96bc2-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="96bc2-237">запрос SQL Hello, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="96bc2-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="96bc2-238">При копировании данных из облачного хранилища данных в Поиск Azure свойство `executionLocation` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="96bc2-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="96bc2-239">Hello следующем фрагменте JSON показан hello изменений в соответствии с действием копирования `typeProperties` в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="96bc2-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="96bc2-240">Дополнительные сведения и поддерживаемые значения см. в разделе [Копирование данных из одного облачного хранилища данных в другое](data-factory-data-movement-activities.md#global).</span><span class="sxs-lookup"><span data-stu-id="96bc2-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="96bc2-241">Копирование из облачного источника</span><span class="sxs-lookup"><span data-stu-id="96bc2-241">Copy from a cloud source</span></span>
<span data-ttu-id="96bc2-242">При копировании данных из облачного хранилища данных в Поиск Azure свойство `executionLocation` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="96bc2-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="96bc2-243">Hello следующем фрагменте JSON показан hello изменений в соответствии с действием копирования `typeProperties` в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="96bc2-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="96bc2-244">Дополнительные сведения и поддерживаемые значения см. в разделе [Копирование данных из одного облачного хранилища данных в другое](data-factory-data-movement-activities.md#global).</span><span class="sxs-lookup"><span data-stu-id="96bc2-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="96bc2-245">Также можно сопоставить столбцы из источника toocolumns набора данных из набора данных приемник в определении действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="96bc2-246">Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="96bc2-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="96bc2-247">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="96bc2-247">Performance and tuning</span></span>  
<span data-ttu-id="96bc2-248">. В разделе hello [действие копирования производительности и руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) и различные способы toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="96bc2-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96bc2-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="96bc2-249">Next steps</span></span>
<span data-ttu-id="96bc2-250">См. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="96bc2-250">See hello following articles:</span></span>

* <span data-ttu-id="96bc2-251">[руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="96bc2-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
