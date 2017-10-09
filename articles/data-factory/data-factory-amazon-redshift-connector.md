---
title: "данные с помощью фабрики данных Amazon Redshift aaaMove | Документы Microsoft"
description: "Дополнительные сведения о том, как данные toomove из Amazon Redshift, с помощью фабрики данных Azure."
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
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="3cc2c-103">Перемещение данных из Amazon Redshift с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="3cc2c-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="3cc2c-104">В этой статье объясняется, как toouse hello действие копирования в данные Amazon Redshift toomove фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="3cc2c-105">Hello статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="3cc2c-106">Можно скопировать данные из хранилища данных Amazon Redshift tooany поддерживается приемника.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="3cc2c-107">Список хранилищ данных, поддерживаемые действием копирования hello как приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="3cc2c-108">Фабрика данных в настоящее время поддерживает перемещение данных из хранилищ данных Amazon Redshift tooother, но не для переноса данных из других tooAmazon хранилищ данных Redshift.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cc2c-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3cc2c-109">Prerequisites</span></span>
* <span data-ttu-id="3cc2c-110">При перемещении данных локального хранилища для данных tooan установить [шлюз управления данными](data-factory-data-management-gateway.md) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="3cc2c-111">Затем шлюз управления данными Grant (использовать IP-адрес компьютера hello) hello tooAmazon Redshift кластера доступа.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="3cc2c-112">В разделе [toohello кластера авторизовать доступ](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) инструкции.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="3cc2c-113">При перемещении хранилища данных Azure tooan данных в разделе [диапазоны IP центр данных Azure](https://www.microsoft.com/download/details.aspx?id=41653) hello вычислений IP-адреса и диапазоны SQL, используемые центрами обработки данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="3cc2c-114">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="3cc2c-114">Getting started</span></span>
<span data-ttu-id="3cc2c-115">Вы можете создать конвейер с действием копирования, который перемещает данные из источника Amazon Redshift, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="3cc2c-116">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="3cc2c-117">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="3cc2c-118">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3cc2c-119">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3cc2c-120">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="3cc2c-121">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="3cc2c-122">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="3cc2c-123">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3cc2c-124">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="3cc2c-125">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="3cc2c-126">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных Amazon Redshift см. в разделе [JSON пример: копирование данных из tooAzure Amazon Redshift больших двоичных объектов](#json-example-copy-data-from-amazon-redshift-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="3cc2c-127">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAmazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="3cc2c-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="3cc2c-128">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="3cc2c-128">Linked service properties</span></span>
<span data-ttu-id="3cc2c-129">Привет, в следующей таблице приводится описание tooAmazon Redshift связанные службы определенные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="3cc2c-130">Свойство</span><span class="sxs-lookup"><span data-stu-id="3cc2c-130">Property</span></span> | <span data-ttu-id="3cc2c-131">Описание</span><span class="sxs-lookup"><span data-stu-id="3cc2c-131">Description</span></span> | <span data-ttu-id="3cc2c-132">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3cc2c-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3cc2c-133">type</span><span class="sxs-lookup"><span data-stu-id="3cc2c-133">type</span></span> |<span data-ttu-id="3cc2c-134">свойство типа Hello должно быть присвоено: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="3cc2c-135">Да</span><span class="sxs-lookup"><span data-stu-id="3cc2c-135">Yes</span></span> |
| <span data-ttu-id="3cc2c-136">server</span><span class="sxs-lookup"><span data-stu-id="3cc2c-136">server</span></span> |<span data-ttu-id="3cc2c-137">IP-адрес или имя сервера Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="3cc2c-138">Да</span><span class="sxs-lookup"><span data-stu-id="3cc2c-138">Yes</span></span> |
| <span data-ttu-id="3cc2c-139">порт</span><span class="sxs-lookup"><span data-stu-id="3cc2c-139">port</span></span> |<span data-ttu-id="3cc2c-140">Hello номер порта TCP hello hello Amazon Redshift сервер использует toolisten для клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="3cc2c-141">Нет, значение по умолчанию — 5439.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-141">No, default value: 5439</span></span> |
| <span data-ttu-id="3cc2c-142">database</span><span class="sxs-lookup"><span data-stu-id="3cc2c-142">database</span></span> |<span data-ttu-id="3cc2c-143">Имя базы данных Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="3cc2c-144">Да</span><span class="sxs-lookup"><span data-stu-id="3cc2c-144">Yes</span></span> |
| <span data-ttu-id="3cc2c-145">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="3cc2c-145">username</span></span> |<span data-ttu-id="3cc2c-146">Имя пользователя, имеющего доступ к базе данных toohello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="3cc2c-147">Да</span><span class="sxs-lookup"><span data-stu-id="3cc2c-147">Yes</span></span> |
| <span data-ttu-id="3cc2c-148">пароль</span><span class="sxs-lookup"><span data-stu-id="3cc2c-148">password</span></span> |<span data-ttu-id="3cc2c-149">Пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-149">Password for hello user account.</span></span> |<span data-ttu-id="3cc2c-150">Да</span><span class="sxs-lookup"><span data-stu-id="3cc2c-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="3cc2c-151">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="3cc2c-151">Dataset properties</span></span>
<span data-ttu-id="3cc2c-152">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3cc2c-153">Разделы structure, availability и policy одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3cc2c-154">Hello **typeProperties** раздела отличается для каждого типа набора данных.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="3cc2c-155">Он содержит сведения о месте hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="3cc2c-156">Hello typeProperties статьи для набора данных типа **RelationalTable** (включает набор данных Amazon Redshift) имеет следующие свойства hello</span><span class="sxs-lookup"><span data-stu-id="3cc2c-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="3cc2c-157">Свойство</span><span class="sxs-lookup"><span data-stu-id="3cc2c-157">Property</span></span> | <span data-ttu-id="3cc2c-158">Описание</span><span class="sxs-lookup"><span data-stu-id="3cc2c-158">Description</span></span> | <span data-ttu-id="3cc2c-159">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3cc2c-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3cc2c-160">tableName</span><span class="sxs-lookup"><span data-stu-id="3cc2c-160">tableName</span></span> |<span data-ttu-id="3cc2c-161">Имя таблицы hello в базе данных Amazon Redshift hello, связанная служба ссылается.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="3cc2c-162">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="3cc2c-163">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="3cc2c-163">Copy activity properties</span></span>
<span data-ttu-id="3cc2c-164">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3cc2c-165">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="3cc2c-166">В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="3cc2c-167">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="3cc2c-168">Если источник действие копирования имеет тип **RelationalSource** (включая Amazon Redshift), hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="3cc2c-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="3cc2c-169">Свойство</span><span class="sxs-lookup"><span data-stu-id="3cc2c-169">Property</span></span> | <span data-ttu-id="3cc2c-170">Описание</span><span class="sxs-lookup"><span data-stu-id="3cc2c-170">Description</span></span> | <span data-ttu-id="3cc2c-171">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3cc2c-171">Allowed values</span></span> | <span data-ttu-id="3cc2c-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3cc2c-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3cc2c-173">query</span><span class="sxs-lookup"><span data-stu-id="3cc2c-173">query</span></span> |<span data-ttu-id="3cc2c-174">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="3cc2c-175">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-175">SQL query string.</span></span> <span data-ttu-id="3cc2c-176">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="3cc2c-177">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="3cc2c-178">Пример JSON: копирование данных из tooAzure Amazon Redshift больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="3cc2c-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="3cc2c-179">В этом примере показано, как данные toocopy из Amazon Redshift базы данных tooan хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="3cc2c-180">Тем не менее, данные можно скопировать **непосредственно** tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="3cc2c-181">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="3cc2c-182">Связанная служба типа [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="3cc2c-183">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="3cc2c-184">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="3cc2c-185">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="3cc2c-186">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="3cc2c-187">Образец Hello копирует данные из результатов запроса в большом двоичном объекте Amazon Redshift tooa каждый час.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="3cc2c-188">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="3cc2c-189">**Связанная служба Amazon Redshift**</span><span class="sxs-lookup"><span data-stu-id="3cc2c-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="3cc2c-190">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="3cc2c-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="3cc2c-191">**Входной набор данных Amazon Redshift**</span><span class="sxs-lookup"><span data-stu-id="3cc2c-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="3cc2c-192">Параметр `"external": true` информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="3cc2c-193">Задайте это свойство tootrue для входного набора данных, который не был создан из действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

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

<span data-ttu-id="3cc2c-194">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="3cc2c-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="3cc2c-195">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3cc2c-196">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="3cc2c-197">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="3cc2c-198">**Действие копирования в конвейере с Azure Redshift (RelationalSource) в качестве источника и большим двоичным объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="3cc2c-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="3cc2c-199">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="3cc2c-200">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="3cc2c-201">запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="3cc2c-202">Сопоставление типов для Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="3cc2c-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="3cc2c-203">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello:</span><span class="sxs-lookup"><span data-stu-id="3cc2c-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="3cc2c-204">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="3cc2c-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="3cc2c-205">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="3cc2c-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="3cc2c-206">При перемещении данных tooAmazon Redshift, Amazon Redshift типы too.NET типы используются следующие сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="3cc2c-207">Тип Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="3cc2c-207">Amazon Redshift Type</span></span> | <span data-ttu-id="3cc2c-208">Тип данных на основе .NET</span><span class="sxs-lookup"><span data-stu-id="3cc2c-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="3cc2c-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="3cc2c-209">SMALLINT</span></span> |<span data-ttu-id="3cc2c-210">Int16</span><span class="sxs-lookup"><span data-stu-id="3cc2c-210">Int16</span></span> |
| <span data-ttu-id="3cc2c-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="3cc2c-211">INTEGER</span></span> |<span data-ttu-id="3cc2c-212">Int32</span><span class="sxs-lookup"><span data-stu-id="3cc2c-212">Int32</span></span> |
| <span data-ttu-id="3cc2c-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="3cc2c-213">BIGINT</span></span> |<span data-ttu-id="3cc2c-214">Int64</span><span class="sxs-lookup"><span data-stu-id="3cc2c-214">Int64</span></span> |
| <span data-ttu-id="3cc2c-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="3cc2c-215">DECIMAL</span></span> |<span data-ttu-id="3cc2c-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="3cc2c-216">Decimal</span></span> |
| <span data-ttu-id="3cc2c-217">REAL</span><span class="sxs-lookup"><span data-stu-id="3cc2c-217">REAL</span></span> |<span data-ttu-id="3cc2c-218">Single</span><span class="sxs-lookup"><span data-stu-id="3cc2c-218">Single</span></span> |
| <span data-ttu-id="3cc2c-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="3cc2c-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="3cc2c-220">Double</span><span class="sxs-lookup"><span data-stu-id="3cc2c-220">Double</span></span> |
| <span data-ttu-id="3cc2c-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="3cc2c-221">BOOLEAN</span></span> |<span data-ttu-id="3cc2c-222">Строка</span><span class="sxs-lookup"><span data-stu-id="3cc2c-222">String</span></span> |
| <span data-ttu-id="3cc2c-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="3cc2c-223">CHAR</span></span> |<span data-ttu-id="3cc2c-224">Строка</span><span class="sxs-lookup"><span data-stu-id="3cc2c-224">String</span></span> |
| <span data-ttu-id="3cc2c-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="3cc2c-225">VARCHAR</span></span> |<span data-ttu-id="3cc2c-226">Строка</span><span class="sxs-lookup"><span data-stu-id="3cc2c-226">String</span></span> |
| <span data-ttu-id="3cc2c-227">DATE</span><span class="sxs-lookup"><span data-stu-id="3cc2c-227">DATE</span></span> |<span data-ttu-id="3cc2c-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="3cc2c-228">DateTime</span></span> |
| <span data-ttu-id="3cc2c-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="3cc2c-229">TIMESTAMP</span></span> |<span data-ttu-id="3cc2c-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="3cc2c-230">DateTime</span></span> |
| <span data-ttu-id="3cc2c-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="3cc2c-231">TEXT</span></span> |<span data-ttu-id="3cc2c-232">Строка</span><span class="sxs-lookup"><span data-stu-id="3cc2c-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="3cc2c-233">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="3cc2c-233">Map source toosink columns</span></span>
<span data-ttu-id="3cc2c-234">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3cc2c-235">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="3cc2c-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="3cc2c-236">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="3cc2c-237">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3cc2c-238">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3cc2c-239">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3cc2c-240">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="3cc2c-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3cc2c-241">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="3cc2c-241">Performance and Tuning</span></span>
<span data-ttu-id="3cc2c-242">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cc2c-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3cc2c-243">Next Steps</span></span>
<span data-ttu-id="3cc2c-244">См. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="3cc2c-244">See hello following articles:</span></span>

* <span data-ttu-id="3cc2c-245">[руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="3cc2c-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
