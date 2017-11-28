---
title: "Перемещение данных из Amazon Redshift с помощью фабрики данных | Документация Майкрософт"
description: "Узнайте о том, как перемещать данные из Amazon Redshift с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: bccb941363952bb2251629240a88148a6527d62e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="d9856-103">Перемещение данных из Amazon Redshift с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="d9856-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="d9856-104">В этой статье описывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="d9856-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="d9856-105">Эта статья является продолжением статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="d9856-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="d9856-106">Данные из Amazon Redshift можно скопировать в любое хранилище данных, поддерживаемое в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="d9856-106">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="d9856-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d9856-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="d9856-108">Сейчас фабрика данных поддерживает перемещение данных из Amazon Redshift в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="d9856-108">Data factory currently supports moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9856-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d9856-109">Prerequisites</span></span>
* <span data-ttu-id="d9856-110">Для перемещения данных в локальное хранилище установите [шлюз управления данными](data-factory-data-management-gateway.md) на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="d9856-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="d9856-111">Затем предоставьте шлюзу управления данными доступ к кластеру Amazon Redshift (используйте IP-адрес компьютера).</span><span class="sxs-lookup"><span data-stu-id="d9856-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="d9856-112">Инструкции см. в статье об [авторизации доступа к кластеру](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html).</span><span class="sxs-lookup"><span data-stu-id="d9856-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="d9856-113">Если вы перемещаете данные в хранилище данных Azure, вам нужно знать IP-адреса вычислительных ресурсов и диапазоны SQL, используемые центрами обработки данных Azure. Диапазоны IP-адресов центра обработки данных Azure приведены на [этой странице](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d9856-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d9856-114">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="d9856-114">Getting started</span></span>
<span data-ttu-id="d9856-115">Вы можете создать конвейер с действием копирования, который перемещает данные из источника Amazon Redshift, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="d9856-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="d9856-116">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="d9856-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="d9856-117">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="d9856-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="d9856-118">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="d9856-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d9856-119">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d9856-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d9856-120">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="d9856-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="d9856-121">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="d9856-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="d9856-122">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="d9856-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="d9856-123">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="d9856-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d9856-124">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="d9856-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d9856-125">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="d9856-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="d9856-126">Пример определения JSON для сущностей фабрики данных, которые используются для копирования данных из хранилища данных Amazon Redshift, вы найдете в разделе [Пример JSON. Копирование данных из Amazon Redshift в большой двоичный объект Azure](#json-example-copy-data-from-amazon-redshift-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="d9856-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d9856-127">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="d9856-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="d9856-128">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="d9856-128">Linked service properties</span></span>
<span data-ttu-id="d9856-129">В таблице ниже приведено описание элементов JSON, которые относятся к связанной службе Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="d9856-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span></span>

| <span data-ttu-id="d9856-130">Свойство</span><span class="sxs-lookup"><span data-stu-id="d9856-130">Property</span></span> | <span data-ttu-id="d9856-131">Описание</span><span class="sxs-lookup"><span data-stu-id="d9856-131">Description</span></span> | <span data-ttu-id="d9856-132">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9856-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9856-133">type</span><span class="sxs-lookup"><span data-stu-id="d9856-133">type</span></span> |<span data-ttu-id="d9856-134">Для свойства type необходимо задать значение **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="d9856-134">The type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="d9856-135">Да</span><span class="sxs-lookup"><span data-stu-id="d9856-135">Yes</span></span> |
| <span data-ttu-id="d9856-136">server</span><span class="sxs-lookup"><span data-stu-id="d9856-136">server</span></span> |<span data-ttu-id="d9856-137">IP-адрес или имя узла сервера Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="d9856-137">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="d9856-138">Да</span><span class="sxs-lookup"><span data-stu-id="d9856-138">Yes</span></span> |
| <span data-ttu-id="d9856-139">порт</span><span class="sxs-lookup"><span data-stu-id="d9856-139">port</span></span> |<span data-ttu-id="d9856-140">Номер TCP-порта, используемого сервером Amazon Redshift для прослушивания клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="d9856-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="d9856-141">Нет, значение по умолчанию — 5439.</span><span class="sxs-lookup"><span data-stu-id="d9856-141">No, default value: 5439</span></span> |
| <span data-ttu-id="d9856-142">database</span><span class="sxs-lookup"><span data-stu-id="d9856-142">database</span></span> |<span data-ttu-id="d9856-143">Имя базы данных Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="d9856-143">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="d9856-144">Да</span><span class="sxs-lookup"><span data-stu-id="d9856-144">Yes</span></span> |
| <span data-ttu-id="d9856-145">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="d9856-145">username</span></span> |<span data-ttu-id="d9856-146">Имя пользователя, имеющего доступ к базе данных.</span><span class="sxs-lookup"><span data-stu-id="d9856-146">Name of user who has access to the database.</span></span> |<span data-ttu-id="d9856-147">Да</span><span class="sxs-lookup"><span data-stu-id="d9856-147">Yes</span></span> |
| <span data-ttu-id="d9856-148">пароль</span><span class="sxs-lookup"><span data-stu-id="d9856-148">password</span></span> |<span data-ttu-id="d9856-149">Пароль для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="d9856-149">Password for the user account.</span></span> |<span data-ttu-id="d9856-150">Да</span><span class="sxs-lookup"><span data-stu-id="d9856-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="d9856-151">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="d9856-151">Dataset properties</span></span>
<span data-ttu-id="d9856-152">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="d9856-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d9856-153">Разделы structure, availability и policy одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="d9856-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d9856-154">Разделы **typeProperties** для каждого типа набора данных отличаются.</span><span class="sxs-lookup"><span data-stu-id="d9856-154">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="d9856-155">В этом разделе указываются такие сведения, как расположение данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="d9856-155">It provides information about the location of the data in the data store.</span></span> <span data-ttu-id="d9856-156">Раздел typeProperties набора данных типа **RelationalTable** (который включает в себя набор данных Amazon Redshift) содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="d9856-156">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span></span>

| <span data-ttu-id="d9856-157">Свойство</span><span class="sxs-lookup"><span data-stu-id="d9856-157">Property</span></span> | <span data-ttu-id="d9856-158">Описание</span><span class="sxs-lookup"><span data-stu-id="d9856-158">Description</span></span> | <span data-ttu-id="d9856-159">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9856-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9856-160">tableName</span><span class="sxs-lookup"><span data-stu-id="d9856-160">tableName</span></span> |<span data-ttu-id="d9856-161">Имя таблицы в базе данных Amazon Redshift, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="d9856-161">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="d9856-162">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="d9856-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d9856-163">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="d9856-163">Copy activity properties</span></span>
<span data-ttu-id="d9856-164">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d9856-164">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d9856-165">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="d9856-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="d9856-166">В свою очередь свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="d9856-166">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="d9856-167">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="d9856-167">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="d9856-168">Когда источник действия копирования относится к типу **RelationalSource** (который включает Amazon Redshift), в разделе typeProperties доступны следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="d9856-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d9856-169">Свойство</span><span class="sxs-lookup"><span data-stu-id="d9856-169">Property</span></span> | <span data-ttu-id="d9856-170">Описание</span><span class="sxs-lookup"><span data-stu-id="d9856-170">Description</span></span> | <span data-ttu-id="d9856-171">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="d9856-171">Allowed values</span></span> | <span data-ttu-id="d9856-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d9856-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d9856-173">query</span><span class="sxs-lookup"><span data-stu-id="d9856-173">query</span></span> |<span data-ttu-id="d9856-174">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="d9856-174">Use the custom query to read data.</span></span> |<span data-ttu-id="d9856-175">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="d9856-175">SQL query string.</span></span> <span data-ttu-id="d9856-176">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="d9856-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="d9856-177">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="d9856-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob"></a><span data-ttu-id="d9856-178">Пример JSON. Копирование данных из Amazon Redshift в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="d9856-178">JSON example: Copy data from Amazon Redshift to Azure Blob</span></span>
<span data-ttu-id="d9856-179">В этом примере показано, как скопировать данные из базы данных Amazon Redshift в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="d9856-179">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span></span> <span data-ttu-id="d9856-180">Тем не менее данные можно копировать **непосредственно** в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d9856-180">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="d9856-181">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d9856-181">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="d9856-182">Связанная служба типа [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9856-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="d9856-183">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9856-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="d9856-184">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9856-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="d9856-185">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9856-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="d9856-186">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d9856-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="d9856-187">В примере данные из результата запроса к Amazon Redshift каждый час копируются в большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="d9856-187">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span></span> <span data-ttu-id="d9856-188">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="d9856-188">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="d9856-189">**Связанная служба Amazon Redshift**</span><span class="sxs-lookup"><span data-stu-id="d9856-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="d9856-190">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="d9856-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="d9856-191">**Входной набор данных Amazon Redshift**</span><span class="sxs-lookup"><span data-stu-id="d9856-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="d9856-192">Значение `"external": true` означает, что служба фабрики данных считает этот набор данных внешним по отношению к себе и не созданным в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="d9856-192">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="d9856-193">Присвойте значение true этому параметру входного набора данных, который не является результатом какого-либо действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="d9856-193">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="d9856-194">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="d9856-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d9856-195">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="d9856-195">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d9856-196">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="d9856-196">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d9856-197">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="d9856-197">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="d9856-198">**Действие копирования в конвейере с Azure Redshift (RelationalSource) в качестве источника и большим двоичным объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="d9856-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="d9856-199">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="d9856-199">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d9856-200">В определении JSON конвейера для типа **source** установлено значение **RelationalSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d9856-200">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="d9856-201">SQL-запрос, указанный для свойства **query** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="d9856-201">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="d9856-202">Сопоставление типов для Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="d9856-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="d9856-203">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="d9856-203">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="d9856-204">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="d9856-204">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="d9856-205">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="d9856-205">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="d9856-206">Когда данные перемещаются в Amazon Redshift, для преобразования типа Amazon Redshift в тип .NET используются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="d9856-206">When moving data to Amazon Redshift, the following mappings are used from Amazon Redshift types to .NET types.</span></span>

| <span data-ttu-id="d9856-207">Тип Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="d9856-207">Amazon Redshift Type</span></span> | <span data-ttu-id="d9856-208">Тип данных на основе .NET</span><span class="sxs-lookup"><span data-stu-id="d9856-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="d9856-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="d9856-209">SMALLINT</span></span> |<span data-ttu-id="d9856-210">Int16</span><span class="sxs-lookup"><span data-stu-id="d9856-210">Int16</span></span> |
| <span data-ttu-id="d9856-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="d9856-211">INTEGER</span></span> |<span data-ttu-id="d9856-212">Int32</span><span class="sxs-lookup"><span data-stu-id="d9856-212">Int32</span></span> |
| <span data-ttu-id="d9856-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="d9856-213">BIGINT</span></span> |<span data-ttu-id="d9856-214">Int64</span><span class="sxs-lookup"><span data-stu-id="d9856-214">Int64</span></span> |
| <span data-ttu-id="d9856-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="d9856-215">DECIMAL</span></span> |<span data-ttu-id="d9856-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="d9856-216">Decimal</span></span> |
| <span data-ttu-id="d9856-217">REAL</span><span class="sxs-lookup"><span data-stu-id="d9856-217">REAL</span></span> |<span data-ttu-id="d9856-218">Single</span><span class="sxs-lookup"><span data-stu-id="d9856-218">Single</span></span> |
| <span data-ttu-id="d9856-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="d9856-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="d9856-220">Double</span><span class="sxs-lookup"><span data-stu-id="d9856-220">Double</span></span> |
| <span data-ttu-id="d9856-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="d9856-221">BOOLEAN</span></span> |<span data-ttu-id="d9856-222">Строка</span><span class="sxs-lookup"><span data-stu-id="d9856-222">String</span></span> |
| <span data-ttu-id="d9856-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="d9856-223">CHAR</span></span> |<span data-ttu-id="d9856-224">Строка</span><span class="sxs-lookup"><span data-stu-id="d9856-224">String</span></span> |
| <span data-ttu-id="d9856-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="d9856-225">VARCHAR</span></span> |<span data-ttu-id="d9856-226">Строка</span><span class="sxs-lookup"><span data-stu-id="d9856-226">String</span></span> |
| <span data-ttu-id="d9856-227">DATE</span><span class="sxs-lookup"><span data-stu-id="d9856-227">DATE</span></span> |<span data-ttu-id="d9856-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="d9856-228">DateTime</span></span> |
| <span data-ttu-id="d9856-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="d9856-229">TIMESTAMP</span></span> |<span data-ttu-id="d9856-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="d9856-230">DateTime</span></span> |
| <span data-ttu-id="d9856-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="d9856-231">TEXT</span></span> |<span data-ttu-id="d9856-232">Строка</span><span class="sxs-lookup"><span data-stu-id="d9856-232">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="d9856-233">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="d9856-233">Map source to sink columns</span></span>
<span data-ttu-id="d9856-234">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d9856-234">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d9856-235">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="d9856-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="d9856-236">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="d9856-236">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="d9856-237">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="d9856-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d9856-238">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="d9856-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d9856-239">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="d9856-239">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d9856-240">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="d9856-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d9856-241">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="d9856-241">Performance and Tuning</span></span>
<span data-ttu-id="d9856-242">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="d9856-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9856-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9856-243">Next Steps</span></span>
<span data-ttu-id="d9856-244">Ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="d9856-244">See the following articles:</span></span>

* <span data-ttu-id="d9856-245">[руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="d9856-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
