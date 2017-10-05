---
title: "Отправка данных в индекс поиска с использованием фабрики данных | Документация Майкрософт"
description: "Узнайте о том, как передавать данные в индекс Поиска Azure с использованием фабрики данных Azure."
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
ms.openlocfilehash: 5c617c7a2f2eb4da2164ce5f802354a64dfd1fa1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="7cc3e-103">Передача данных в индекс Поиска Azure с использованием фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="7cc3e-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="7cc3e-104">В этой статье описывается, как использовать действие копирования для передачи данных из поддерживаемого исходного хранилища данных в индекс Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-104">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="7cc3e-105">Поддерживаемые исходные хранилища данных перечислены в столбце "Источник" таблицы [поддерживаемых источников и приемников](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-105">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="7cc3e-106">Эта статья основана на статье о [действиях перемещения данных](data-factory-data-movement-activities.md) , в которой приведены общие сведения о перемещении данных с помощью действия копирования и поддерживаемых сочетаниях хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-106">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="7cc3e-107">Включение соединения</span><span class="sxs-lookup"><span data-stu-id="7cc3e-107">Enabling connectivity</span></span>
<span data-ttu-id="7cc3e-108">Чтобы разрешить подключение службы фабрики данных к локальному хранилищу данных, установите в локальной среде шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-108">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="7cc3e-109">Его можно установить на том же компьютере, на котором размещено исходное хранилище данных, или на отдельном компьютере во избежание конкуренции за ресурсы с хранилищем данных.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-109">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="7cc3e-110">Шлюз управления данными обеспечивает безопасное и управляемое подключение локальных источников данных к облачным службам.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-110">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="7cc3e-111">Сведения о шлюзе управления данными см. в статье [Перемещение данных между локальными источниками и облаком](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7cc3e-112">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="7cc3e-112">Getting started</span></span>
<span data-ttu-id="7cc3e-113">Вы можете создать конвейер с действием копирования, который перемещает данные из исходного хранилища данных в индекс Поиска Azure, с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-113">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="7cc3e-114">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="7cc3e-115">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="7cc3e-116">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7cc3e-117">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="7cc3e-118">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7cc3e-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="7cc3e-119">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="7cc3e-120">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="7cc3e-121">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="7cc3e-122">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="7cc3e-123">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="7cc3e-124">Пример определений JSON для сущностей фабрики данных, которые используются для копирования данных в индекс Поиска Azure, вы найдете в разделе [Пример JSON. Копирование данных с локального сервера SQL Server в индекс поиска Azure](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-124">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="7cc3e-125">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к индексу Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7cc3e-126">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="7cc3e-126">Linked service properties</span></span>

<span data-ttu-id="7cc3e-127">В таблице ниже приведены описания элементов JSON, которые относятся к связанной службе Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-127">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="7cc3e-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="7cc3e-128">Property</span></span> | <span data-ttu-id="7cc3e-129">Описание</span><span class="sxs-lookup"><span data-stu-id="7cc3e-129">Description</span></span> | <span data-ttu-id="7cc3e-130">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7cc3e-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="7cc3e-131">type</span><span class="sxs-lookup"><span data-stu-id="7cc3e-131">type</span></span> | <span data-ttu-id="7cc3e-132">Для свойства type необходимо задать значение **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-132">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="7cc3e-133">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-133">Yes</span></span> |
| <span data-ttu-id="7cc3e-134">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="7cc3e-134">url</span></span> | <span data-ttu-id="7cc3e-135">URL-адрес службы Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-135">URL for the Azure Search service.</span></span> | <span data-ttu-id="7cc3e-136">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-136">Yes</span></span> |
| <span data-ttu-id="7cc3e-137">key</span><span class="sxs-lookup"><span data-stu-id="7cc3e-137">key</span></span> | <span data-ttu-id="7cc3e-138">Ключ администратора службы Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-138">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="7cc3e-139">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="7cc3e-140">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="7cc3e-140">Dataset properties</span></span>

<span data-ttu-id="7cc3e-141">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-141">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7cc3e-142">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="7cc3e-143">Разделы **typeProperties** для каждого типа набора данных отличаются.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-143">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="7cc3e-144">Раздел typeProperties для набора данных типа **AzureSearchIndex** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-144">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="7cc3e-145">Свойство</span><span class="sxs-lookup"><span data-stu-id="7cc3e-145">Property</span></span> | <span data-ttu-id="7cc3e-146">Описание</span><span class="sxs-lookup"><span data-stu-id="7cc3e-146">Description</span></span> | <span data-ttu-id="7cc3e-147">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7cc3e-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="7cc3e-148">type</span><span class="sxs-lookup"><span data-stu-id="7cc3e-148">type</span></span> | <span data-ttu-id="7cc3e-149">Для свойства type необходимо задать значение **AzureSearchIndex**</span><span class="sxs-lookup"><span data-stu-id="7cc3e-149">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="7cc3e-150">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-150">Yes</span></span> |
| <span data-ttu-id="7cc3e-151">indexName</span><span class="sxs-lookup"><span data-stu-id="7cc3e-151">indexName</span></span> | <span data-ttu-id="7cc3e-152">Имя индекса Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-152">Name of the Azure Search index.</span></span> <span data-ttu-id="7cc3e-153">Фабрика данных не создает индекс.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-153">Data Factory does not create the index.</span></span> <span data-ttu-id="7cc3e-154">Индекс должен существовать в Поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-154">The index must exist in Azure Search.</span></span> | <span data-ttu-id="7cc3e-155">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="7cc3e-156">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="7cc3e-156">Copy activity properties</span></span>
<span data-ttu-id="7cc3e-157">Полный список разделов и свойств, используемых для определения действий, см. в статье [Конвейеры и действия в фабрике данных Azure: создание конвейеров, цепочки действий и расписаний для них](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-157">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7cc3e-158">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="7cc3e-159">В свою очередь свойства, доступные в разделе typeProperties, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-159">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="7cc3e-160">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-160">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="7cc3e-161">Для действия копирования, когда приемник относится к типу **AzureSearchIndexSink**, в разделе typeProperties доступны указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-161">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="7cc3e-162">Свойство</span><span class="sxs-lookup"><span data-stu-id="7cc3e-162">Property</span></span> | <span data-ttu-id="7cc3e-163">Описание</span><span class="sxs-lookup"><span data-stu-id="7cc3e-163">Description</span></span> | <span data-ttu-id="7cc3e-164">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="7cc3e-164">Allowed values</span></span> | <span data-ttu-id="7cc3e-165">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7cc3e-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="7cc3e-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="7cc3e-166">WriteBehavior</span></span> | <span data-ttu-id="7cc3e-167">Указывает действие (объединение или замена), выполняемое, если документ уже существует в индексе.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="7cc3e-168">Ознакомьтесь с разделом [Свойство WriteBehavior](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-168">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="7cc3e-169">Merge (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="7cc3e-169">Merge (default)</span></span><br/><span data-ttu-id="7cc3e-170">Отправить</span><span class="sxs-lookup"><span data-stu-id="7cc3e-170">Upload</span></span>| <span data-ttu-id="7cc3e-171">Нет</span><span class="sxs-lookup"><span data-stu-id="7cc3e-171">No</span></span> |
| <span data-ttu-id="7cc3e-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="7cc3e-172">WriteBatchSize</span></span> | <span data-ttu-id="7cc3e-173">Передает данные в индекс Поиска Azure, когда размер буфера достигает значения writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-173">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="7cc3e-174">Ознакомьтесь с разделом [Свойство WriteBatchSize](#writebatchsize-property).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-174">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="7cc3e-175">1–1000.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-175">1 to 1,000.</span></span> <span data-ttu-id="7cc3e-176">Значение по умолчанию — 1000.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-176">Default value is 1000.</span></span> | <span data-ttu-id="7cc3e-177">Нет</span><span class="sxs-lookup"><span data-stu-id="7cc3e-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="7cc3e-178">Свойство WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="7cc3e-178">WriteBehavior property</span></span>
<span data-ttu-id="7cc3e-179">При записи данных AzureSearchSink выполняет операцию upsert.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="7cc3e-180">Другими словами, если при создании документа ключ документа уже существует в индексе Поиска Azure, Поиск Azure обновляет существующий документ, а не создает исключения из-за конфликта.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-180">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="7cc3e-181">AzureSearchSink проявляет два типа поведения upsert (с использованием пакета SDK AzureSearch):</span><span class="sxs-lookup"><span data-stu-id="7cc3e-181">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="7cc3e-182">**Объединение**. Все столбцы в новом документе объединяются со столбцами в существующем.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-182">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="7cc3e-183">Для столбцов с значением null в новом документе значение столбцов в существующем документе сохраняется.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-183">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="7cc3e-184">**Отправка**. Новый документ заменяет существующий.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-184">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="7cc3e-185">Для столбцов, не указанных в новом документе, задается значение null независимо от того, есть ли в существующем документе столбцы с значением, отличным от null.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-185">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="7cc3e-186">Поведение по умолчанию — **объединение**.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-186">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="7cc3e-187">Свойство WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="7cc3e-187">WriteBatchSize Property</span></span>
<span data-ttu-id="7cc3e-188">Служба Поиска Azure поддерживает запись документов в виде пакета.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="7cc3e-189">Пакет может содержать от 1 до 1000 действий.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-189">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="7cc3e-190">Действие обрабатывает один документ для выполнения операции передачи или объединения.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-190">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="7cc3e-191">Поддержка типов данных</span><span class="sxs-lookup"><span data-stu-id="7cc3e-191">Data type support</span></span>
<span data-ttu-id="7cc3e-192">В следующей таблице представлены сведения о поддержке типов данных Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-192">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="7cc3e-193">Тип данных Поиска Azure</span><span class="sxs-lookup"><span data-stu-id="7cc3e-193">Azure Search data type</span></span> | <span data-ttu-id="7cc3e-194">Поддерживается в приемнике Поиска Azure</span><span class="sxs-lookup"><span data-stu-id="7cc3e-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="7cc3e-195">Строка</span><span class="sxs-lookup"><span data-stu-id="7cc3e-195">String</span></span> | <span data-ttu-id="7cc3e-196">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-196">Y</span></span> |
| <span data-ttu-id="7cc3e-197">Int32</span><span class="sxs-lookup"><span data-stu-id="7cc3e-197">Int32</span></span> | <span data-ttu-id="7cc3e-198">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-198">Y</span></span> |
| <span data-ttu-id="7cc3e-199">Int64</span><span class="sxs-lookup"><span data-stu-id="7cc3e-199">Int64</span></span> | <span data-ttu-id="7cc3e-200">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-200">Y</span></span> |
| <span data-ttu-id="7cc3e-201">Double</span><span class="sxs-lookup"><span data-stu-id="7cc3e-201">Double</span></span> | <span data-ttu-id="7cc3e-202">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-202">Y</span></span> |
| <span data-ttu-id="7cc3e-203">Логический</span><span class="sxs-lookup"><span data-stu-id="7cc3e-203">Boolean</span></span> | <span data-ttu-id="7cc3e-204">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-204">Y</span></span> |
| <span data-ttu-id="7cc3e-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="7cc3e-205">DataTimeOffset</span></span> | <span data-ttu-id="7cc3e-206">Да</span><span class="sxs-lookup"><span data-stu-id="7cc3e-206">Y</span></span> |
| <span data-ttu-id="7cc3e-207">Массив строк</span><span class="sxs-lookup"><span data-stu-id="7cc3e-207">String Array</span></span> | <span data-ttu-id="7cc3e-208">Нет</span><span class="sxs-lookup"><span data-stu-id="7cc3e-208">N</span></span> |
| <span data-ttu-id="7cc3e-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="7cc3e-209">GeographyPoint</span></span> | <span data-ttu-id="7cc3e-210">Нет</span><span class="sxs-lookup"><span data-stu-id="7cc3e-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="7cc3e-211">Пример JSON. Копирование данных с локального сервера SQL Server в индекс поиска Azure</span><span class="sxs-lookup"><span data-stu-id="7cc3e-211">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="7cc3e-212">В примере ниже используется следующее:</span><span class="sxs-lookup"><span data-stu-id="7cc3e-212">The following sample shows:</span></span>

1.  <span data-ttu-id="7cc3e-213">Связанная служба типа [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="7cc3e-214">Связанная служба типа [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="7cc3e-215">Входной [набор данных](data-factory-create-datasets.md) типа [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="7cc3e-216">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="7cc3e-217">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) и [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="7cc3e-218">В этом примере каждый час копируются данные временных рядов из локальной базы данных SQL Server в индекс Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-218">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="7cc3e-219">Используемые в этом примере свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-219">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="7cc3e-220">Сначала настройте шлюз управления данными на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-220">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="7cc3e-221">Инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="7cc3e-221">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="7cc3e-222">**Связанная служба Поиска Azure:**</span><span class="sxs-lookup"><span data-stu-id="7cc3e-222">**Azure Search linked service:**</span></span>

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

<span data-ttu-id="7cc3e-223">**Связанная служба SQL Server**</span><span class="sxs-lookup"><span data-stu-id="7cc3e-223">**SQL Server linked service**</span></span>

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

<span data-ttu-id="7cc3e-224">**Входной набор данных SQL Server**</span><span class="sxs-lookup"><span data-stu-id="7cc3e-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="7cc3e-225">В примере предполагается, что вы уже создали таблицу MyTable в SQL Server и она содержит столбец с именем timestampcolumn для данных временного ряда.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-225">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="7cc3e-226">Можно выполнить запрос к нескольким таблицам в одной базе данных, используя один набор данных, но для typeProperty tableName набора данных нужно указать одну таблицу.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-226">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="7cc3e-227">Если для параметра external задать значение true, то фабрика данных воспримет этот набор данных как внешний, который создан не в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-227">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="7cc3e-228">**Выходной набор данных Поиска Azure:**</span><span class="sxs-lookup"><span data-stu-id="7cc3e-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="7cc3e-229">В примере данные копируются в индекс Поиска Azure с именем **products**.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-229">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="7cc3e-230">Фабрика данных не создает индекс.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-230">Data Factory does not create the index.</span></span> <span data-ttu-id="7cc3e-231">Чтобы проверить пример, создайте индекс с таким именем.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-231">To test the sample, create an index with this name.</span></span> <span data-ttu-id="7cc3e-232">Создайте индекс Поиска Azure с таким же количеством столбцов, что и во входном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-232">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="7cc3e-233">Новые записи добавляются в индекс Поиска Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-233">New entries are added to the Azure Search index every hour.</span></span>

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

<span data-ttu-id="7cc3e-234">**Действие копирования в конвейере со средой SQL в качестве источника и индексом Поиска Azure в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="7cc3e-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="7cc3e-235">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-235">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="7cc3e-236">В определении JSON конвейера для свойства type параметра **source** установлено значение **SqlSource**, а для свойства type параметра **sink** — значение **AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-236">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="7cc3e-237">SQL-запрос, указанный для свойства **SqlReaderQuery** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-237">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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

<span data-ttu-id="7cc3e-238">При копировании данных из облачного хранилища данных в Поиск Azure свойство `executionLocation` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="7cc3e-239">Для примера в приведенном ниже фрагменте JSON показано изменение, необходимое в действии копирования `typeProperties`.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-239">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="7cc3e-240">Дополнительные сведения и поддерживаемые значения см. в разделе [Копирование данных из одного облачного хранилища данных в другое](data-factory-data-movement-activities.md#global).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="7cc3e-241">Копирование из облачного источника</span><span class="sxs-lookup"><span data-stu-id="7cc3e-241">Copy from a cloud source</span></span>
<span data-ttu-id="7cc3e-242">При копировании данных из облачного хранилища данных в Поиск Azure свойство `executionLocation` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="7cc3e-243">Для примера в приведенном ниже фрагменте JSON показано изменение, необходимое в действии копирования `typeProperties`.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="7cc3e-244">Дополнительные сведения и поддерживаемые значения см. в разделе [Копирование данных из одного облачного хранилища данных в другое](data-factory-data-movement-activities.md#global).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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

<span data-ttu-id="7cc3e-245">Также можно сопоставить столбцы из набора данных, используемого в качестве источника, со столбцами из приемника в определении действия копирования.</span><span class="sxs-lookup"><span data-stu-id="7cc3e-245">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="7cc3e-246">Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7cc3e-247">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="7cc3e-247">Performance and tuning</span></span>  
<span data-ttu-id="7cc3e-248">Сведения о ключевых факторах, влияющих на производительность перемещения данных (действие копирования), и различных способах оптимизации этого процесса см. в статье [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="7cc3e-248">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cc3e-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7cc3e-249">Next steps</span></span>
<span data-ttu-id="7cc3e-250">Ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="7cc3e-250">See the following articles:</span></span>

* <span data-ttu-id="7cc3e-251">[руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="7cc3e-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
