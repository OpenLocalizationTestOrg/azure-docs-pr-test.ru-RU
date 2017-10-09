---
title: "aaaCopy данных из базы данных SQL Azure | Документы Microsoft"
description: "Узнайте, как toocopy данных из базы данных SQL Azure, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="901a2-103">Tooand копирования данных из базы данных SQL Azure, с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="901a2-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="901a2-104">В этой статье объясняется, как toouse hello действие копирования в tooand данных toomove фабрики данных Azure, из базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="901a2-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="901a2-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="901a2-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="901a2-106">Supported scenarios</span></span>
<span data-ttu-id="901a2-107">Можно скопировать данные **из базы данных SQL Azure** toohello следующие хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="901a2-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="901a2-108">Можно скопировать данные из hello, следуя хранилищ данных **tooAzure базы данных SQL**:</span><span class="sxs-lookup"><span data-stu-id="901a2-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="901a2-109">Поддерживаемый тип проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="901a2-109">Supported authentication type</span></span>
<span data-ttu-id="901a2-110">Соединитель базы данных SQL Azure поддерживает обычную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="901a2-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="901a2-111">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="901a2-111">Getting started</span></span>
<span data-ttu-id="901a2-112">Можно создать конвейер с действием копирования, которое перемещает данные из базы данных SQL Azure или в нее с помощью различных инструментов и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="901a2-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="901a2-113">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="901a2-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="901a2-114">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="901a2-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="901a2-115">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="901a2-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="901a2-116">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="901a2-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="901a2-117">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="901a2-118">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="901a2-118">Create a **data factory**.</span></span> <span data-ttu-id="901a2-119">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="901a2-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="901a2-120">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="901a2-121">Например при копировании данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure, создается два связанных служб toolink вашей учетной записи хранилища Azure и фабрики данных tooyour базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="901a2-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="901a2-122">Свойства связанной службы, определенные tooAzure базы данных SQL, в разделе [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="901a2-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="901a2-123">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="901a2-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="901a2-124">В примере hello, упомянутые в последнем шаге hello создать контейнер больших двоичных объектов dataset toospecify hello и папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="901a2-125">И создайте другую таблицу SQL hello toospecify набора данных в базе данных Azure SQL hello, содержащий hello данные, скопированные из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="901a2-126">Свойства набора данных, определенных tooAzure хранилища Озера данных, в разделе [свойства набора данных](#dataset-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="901a2-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="901a2-127">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="901a2-128">В примере hello приведенные выше используются BlobSource в исходной и SqlSink в приемник для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="901a2-129">Аналогично Если копируются из базы данных SQL Azure tooAzure хранилища больших двоичных объектов, использовать SqlSource и BlobSink в действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="901a2-130">Свойства действия копирования, определенные tooAzure базы данных SQL, в разделе [скопировать свойства действия](#copy-activity-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="901a2-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="901a2-131">Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="901a2-132">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="901a2-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="901a2-133">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="901a2-134">Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из базы данных SQL Azure см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-sql-database) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="901a2-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="901a2-135">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAzure базы данных SQL:</span><span class="sxs-lookup"><span data-stu-id="901a2-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="901a2-136">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="901a2-136">Linked service properties</span></span>
<span data-ttu-id="901a2-137">Azure SQL связанные ссылки на службу фабрики данных tooyour базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="901a2-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="901a2-138">в следующей таблице Hello предоставляет описание tooAzure SQL определенные элементы JSON связанной службы.</span><span class="sxs-lookup"><span data-stu-id="901a2-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="901a2-139">Свойство</span><span class="sxs-lookup"><span data-stu-id="901a2-139">Property</span></span> | <span data-ttu-id="901a2-140">Описание</span><span class="sxs-lookup"><span data-stu-id="901a2-140">Description</span></span> | <span data-ttu-id="901a2-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="901a2-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="901a2-142">type</span><span class="sxs-lookup"><span data-stu-id="901a2-142">type</span></span> |<span data-ttu-id="901a2-143">свойство типа Hello должно быть присвоено: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="901a2-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="901a2-144">Да</span><span class="sxs-lookup"><span data-stu-id="901a2-144">Yes</span></span> |
| <span data-ttu-id="901a2-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="901a2-145">connectionString</span></span> |<span data-ttu-id="901a2-146">Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных SQL Azure toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="901a2-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="901a2-147">Поддерживается только обычная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="901a2-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="901a2-148">Да</span><span class="sxs-lookup"><span data-stu-id="901a2-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="901a2-149">Настройка [брандмауэр базы данных SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello сервера базы данных слишком[сервер служб Azure tooaccess hello](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="901a2-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="901a2-150">Кроме того при копировании данных tooAzure базы данных SQL из внешней в Azure, включая из локальных источников данных со шлюзом фабрики данных, настройте соответствующий диапазон IP-адресов для компьютера hello, передающий данные tooAzure базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="901a2-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="901a2-151">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="901a2-151">Dataset properties</span></span>
<span data-ttu-id="901a2-152">toospecify dataset toorepresent входных или выходных данных в базе данных Azure SQL, задайте свойство типа hello hello набора данных для: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="901a2-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="901a2-153">Набор hello **linkedServiceName** свойство toohello имя набора данных hello hello Azure SQL связанной службы.</span><span class="sxs-lookup"><span data-stu-id="901a2-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="901a2-154">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="901a2-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="901a2-155">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="901a2-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="901a2-156">раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="901a2-157">Hello **typeProperties** раздел для набора данных hello типа **AzureSqlTable** имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="901a2-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="901a2-158">Свойство</span><span class="sxs-lookup"><span data-stu-id="901a2-158">Property</span></span> | <span data-ttu-id="901a2-159">Описание</span><span class="sxs-lookup"><span data-stu-id="901a2-159">Description</span></span> | <span data-ttu-id="901a2-160">Обязательно</span><span class="sxs-lookup"><span data-stu-id="901a2-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="901a2-161">tableName</span><span class="sxs-lookup"><span data-stu-id="901a2-161">tableName</span></span> |<span data-ttu-id="901a2-162">Имя hello таблицы или представления в экземпляр базы данных SQL Azure hello, связанная служба ссылается.</span><span class="sxs-lookup"><span data-stu-id="901a2-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="901a2-163">Да</span><span class="sxs-lookup"><span data-stu-id="901a2-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="901a2-164">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="901a2-164">Copy activity properties</span></span>
<span data-ttu-id="901a2-165">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="901a2-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="901a2-166">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="901a2-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="901a2-167">Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.</span><span class="sxs-lookup"><span data-stu-id="901a2-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="901a2-168">В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="901a2-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="901a2-169">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="901a2-170">При перемещении данных из базы данных Azure SQL, следует установить hello исходного типа в действие копирования hello слишком**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="901a2-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="901a2-171">Аналогичным образом, при перемещении базы данных Azure SQL tooan данных задаются тип приемника hello в действии копирования hello слишком**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="901a2-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="901a2-172">Этот раздел содержит список свойств, поддерживаемых типами SqlSource и SqlSink.</span><span class="sxs-lookup"><span data-stu-id="901a2-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="901a2-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="901a2-173">SqlSource</span></span>
<span data-ttu-id="901a2-174">В действии копирования, когда источник hello типа **SqlSource**, hello следующие свойства доступны в **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="901a2-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="901a2-175">Свойство</span><span class="sxs-lookup"><span data-stu-id="901a2-175">Property</span></span> | <span data-ttu-id="901a2-176">Описание</span><span class="sxs-lookup"><span data-stu-id="901a2-176">Description</span></span> | <span data-ttu-id="901a2-177">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="901a2-177">Allowed values</span></span> | <span data-ttu-id="901a2-178">Обязательно</span><span class="sxs-lookup"><span data-stu-id="901a2-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="901a2-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="901a2-179">sqlReaderQuery</span></span> |<span data-ttu-id="901a2-180">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="901a2-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="901a2-181">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="901a2-181">SQL query string.</span></span> <span data-ttu-id="901a2-182">Пример: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="901a2-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="901a2-183">Нет</span><span class="sxs-lookup"><span data-stu-id="901a2-183">No</span></span> |
| <span data-ttu-id="901a2-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="901a2-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="901a2-185">Имя hello хранимой процедуры, который считывает данные из таблицы источника hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="901a2-186">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="901a2-186">Name of hello stored procedure.</span></span> <span data-ttu-id="901a2-187">Hello последней инструкцией SQL должна быть инструкция SELECT в hello хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="901a2-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="901a2-188">Нет</span><span class="sxs-lookup"><span data-stu-id="901a2-188">No</span></span> |
| <span data-ttu-id="901a2-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="901a2-189">storedProcedureParameters</span></span> |<span data-ttu-id="901a2-190">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="901a2-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="901a2-191">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="901a2-191">Name/value pairs.</span></span> <span data-ttu-id="901a2-192">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="901a2-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="901a2-193">Нет</span><span class="sxs-lookup"><span data-stu-id="901a2-193">No</span></span> |

<span data-ttu-id="901a2-194">Если hello **sqlReaderQuery** указан для hello SqlSource, hello действие копирования выполняет этот запрос данных hello базы данных SQL Azure источника tooget hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="901a2-195">Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="901a2-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="901a2-196">Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello hello набора данных JSON, используемые toobuild запроса (`select column1, column2 from mytable`) toorun от hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="901a2-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="901a2-197">Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="901a2-198">При использовании **sqlReaderStoredProcedureName**, по-прежнему требуется toospecify значение для hello **tableName** свойство в наборе данных hello JSON.</span><span class="sxs-lookup"><span data-stu-id="901a2-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="901a2-199">Хотя какие-либо проверки этой таблицы отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="901a2-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="901a2-200">Пример SqlSource</span><span class="sxs-lookup"><span data-stu-id="901a2-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="901a2-201">**Определение Hello хранимые процедуры:**</span><span class="sxs-lookup"><span data-stu-id="901a2-201">**hello stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a><span data-ttu-id="901a2-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="901a2-202">SqlSink</span></span>
<span data-ttu-id="901a2-203">**SqlSink** поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="901a2-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="901a2-204">Свойство</span><span class="sxs-lookup"><span data-stu-id="901a2-204">Property</span></span> | <span data-ttu-id="901a2-205">Описание</span><span class="sxs-lookup"><span data-stu-id="901a2-205">Description</span></span> | <span data-ttu-id="901a2-206">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="901a2-206">Allowed values</span></span> | <span data-ttu-id="901a2-207">Обязательно</span><span class="sxs-lookup"><span data-stu-id="901a2-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="901a2-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="901a2-208">writeBatchTimeout</span></span> |<span data-ttu-id="901a2-209">Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="901a2-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="901a2-210">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="901a2-210">timespan</span></span><br/><br/> <span data-ttu-id="901a2-211">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="901a2-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="901a2-212">Нет</span><span class="sxs-lookup"><span data-stu-id="901a2-212">No</span></span> |
| <span data-ttu-id="901a2-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="901a2-213">writeBatchSize</span></span> |<span data-ttu-id="901a2-214">Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="901a2-215">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="901a2-215">Integer (number of rows)</span></span> |<span data-ttu-id="901a2-216">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="901a2-216">No (default: 10000)</span></span> |
| <span data-ttu-id="901a2-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="901a2-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="901a2-218">Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез.</span><span class="sxs-lookup"><span data-stu-id="901a2-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="901a2-219">Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="901a2-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="901a2-220">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="901a2-220">A query statement.</span></span> |<span data-ttu-id="901a2-221">Нет</span><span class="sxs-lookup"><span data-stu-id="901a2-221">No</span></span> |
| <span data-ttu-id="901a2-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="901a2-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="901a2-223">Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения.</span><span class="sxs-lookup"><span data-stu-id="901a2-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="901a2-224">Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="901a2-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="901a2-225">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="901a2-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="901a2-226">Нет</span><span class="sxs-lookup"><span data-stu-id="901a2-226">No</span></span> |
| <span data-ttu-id="901a2-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="901a2-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="901a2-228">Имя hello хранимой процедуры upserts (обновления или вставки) данные в целевой таблице hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="901a2-229">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="901a2-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="901a2-230">Нет</span><span class="sxs-lookup"><span data-stu-id="901a2-230">No</span></span> |
| <span data-ttu-id="901a2-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="901a2-231">storedProcedureParameters</span></span> |<span data-ttu-id="901a2-232">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="901a2-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="901a2-233">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="901a2-233">Name/value pairs.</span></span> <span data-ttu-id="901a2-234">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="901a2-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="901a2-235">Нет</span><span class="sxs-lookup"><span data-stu-id="901a2-235">No</span></span> |
| <span data-ttu-id="901a2-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="901a2-236">sqlWriterTableType</span></span> |<span data-ttu-id="901a2-237">Укажите имя toobe тип таблицы, используемых в hello хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="901a2-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="901a2-238">Действие копирования предоставляет hello данных, перемещаемых во временной таблице с этой таблицей.</span><span class="sxs-lookup"><span data-stu-id="901a2-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="901a2-239">Кода хранимой процедуры можно объединять hello данные копируются с существующими данными.</span><span class="sxs-lookup"><span data-stu-id="901a2-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="901a2-240">Имя типа таблицы.</span><span class="sxs-lookup"><span data-stu-id="901a2-240">A table type name.</span></span> |<span data-ttu-id="901a2-241">Нет</span><span class="sxs-lookup"><span data-stu-id="901a2-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="901a2-242">Пример SqlSink</span><span class="sxs-lookup"><span data-stu-id="901a2-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="901a2-243">Примеры JSON для копирования данных tooand из базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="901a2-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="901a2-244">Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="901a2-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="901a2-245">Они показывают как toocopy tooand данных из базы данных SQL Azure и хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="901a2-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="901a2-246">Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="901a2-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="901a2-247">Пример: Копирование данных из базы данных SQL Azure tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="901a2-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="901a2-248">Hello же определяет hello, следуя фабрики данных сущности:</span><span class="sxs-lookup"><span data-stu-id="901a2-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="901a2-249">Связанная служба типа [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="901a2-250">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="901a2-251">Входной [набор данных](data-factory-create-datasets.md) типа [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="901a2-252">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="901a2-253">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="901a2-254">Образец Hello копирует данные временных рядов (каждый час, день, т. д.) из таблицы в большом двоичном объекте tooa базы данных Azure SQL каждый час.</span><span class="sxs-lookup"><span data-stu-id="901a2-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="901a2-255">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="901a2-256">**Связанная служба базы данных SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="901a2-256">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="901a2-257">В разделе hello [связанной службы SQL Azure](#linked-service) раздел hello список свойств, поддерживаемых этой связанной службой.</span><span class="sxs-lookup"><span data-stu-id="901a2-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="901a2-258">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="901a2-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="901a2-259">В разделе hello [больших двоичных объектов Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) статье hello список свойств, поддерживаемых этой связанной службой.</span><span class="sxs-lookup"><span data-stu-id="901a2-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="901a2-260">**Входной набор данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="901a2-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="901a2-261">Образец Hello предполагается создания таблицы «MyTable» в Azure SQL и содержит столбец с именем «timestampcolumn» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="901a2-262">Параметр «external»: «true» уведомляет службу hello фабрики данных Azure, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="901a2-263">. В разделе hello [свойства тип набора данных Azure SQL](#dataset) раздел hello список свойств, поддерживаемых этим типом набора данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="901a2-264">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="901a2-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="901a2-265">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="901a2-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="901a2-266">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="901a2-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="901a2-267">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
<span data-ttu-id="901a2-268">. В разделе hello [свойства тип набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) раздел hello список свойств, поддерживаемых этим типом набора данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="901a2-269">**Действие копирования в конвейере с базой данных SQL в качестве источника и BLOB-объектом в качестве приемника:**</span><span class="sxs-lookup"><span data-stu-id="901a2-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="901a2-270">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="901a2-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="901a2-271">В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="901a2-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="901a2-272">запрос SQL Hello, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="901a2-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="901a2-273">В примере hello **sqlReaderQuery** указан для hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="901a2-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="901a2-274">Действие копирования Hello этот запрос запускает hello tooget hello базы данных SQL Azure исходных данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="901a2-275">Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="901a2-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="901a2-276">Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello hello набора данных JSON, используемые toobuild toorun запроса от hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="901a2-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="901a2-277">Например, `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="901a2-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="901a2-278">Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="901a2-279">В разделе hello [источника Sql](#sqlsource) раздел и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) список свойств, поддерживаемых SqlSource и BlobSink hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="901a2-280">Пример: Копирование данных из больших двоичных объектов Azure tooAzure базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="901a2-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="901a2-281">Образец Hello определяет hello, следуя фабрики данных сущности:</span><span class="sxs-lookup"><span data-stu-id="901a2-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="901a2-282">Связанная служба типа [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="901a2-283">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="901a2-284">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="901a2-285">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="901a2-286">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="901a2-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="901a2-287">Образец Hello копирует данные временных рядов (каждый час, день, т. д.) из таблицы tooa BLOB-объектов Azure в базе данных Azure SQL каждый час.</span><span class="sxs-lookup"><span data-stu-id="901a2-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="901a2-288">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="901a2-289">**Связанная служба SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="901a2-289">**Azure SQL linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="901a2-290">В разделе hello [связанной службы SQL Azure](#linked-service) раздел hello список свойств, поддерживаемых этой связанной службой.</span><span class="sxs-lookup"><span data-stu-id="901a2-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="901a2-291">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="901a2-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="901a2-292">В разделе hello [больших двоичных объектов Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) статье hello список свойств, поддерживаемых этой связанной службой.</span><span class="sxs-lookup"><span data-stu-id="901a2-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="901a2-293">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="901a2-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="901a2-294">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="901a2-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="901a2-295">Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="901a2-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="901a2-296">путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="901a2-297">«external»: параметр «true» уведомляет службу hello фабрики данных, что эта таблица является внешней toohello фабрики данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
<span data-ttu-id="901a2-298">. В разделе hello [свойства тип набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) раздел hello список свойств, поддерживаемых этим типом набора данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="901a2-299">**Выходной набор данных базы данных SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="901a2-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="901a2-300">Образец Hello копирует tooa таблицу данных, с именем «MyTable» в Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="901a2-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="901a2-301">Создать таблицу hello в SQL Azure с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="901a2-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="901a2-302">Новые строки добавляются в таблицу toohello каждый час.</span><span class="sxs-lookup"><span data-stu-id="901a2-302">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
<span data-ttu-id="901a2-303">. В разделе hello [свойства тип набора данных Azure SQL](#dataset) раздел hello список свойств, поддерживаемых этим типом набора данных.</span><span class="sxs-lookup"><span data-stu-id="901a2-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="901a2-304">**Действие копирования в конвейере с BLOB-объектом в качестве источника и базой данных SQL в качестве приемника:**</span><span class="sxs-lookup"><span data-stu-id="901a2-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="901a2-305">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="901a2-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="901a2-306">В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="901a2-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
<span data-ttu-id="901a2-307">В разделе hello [приемника Sql](#sqlsink) раздел и [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) hello список свойств, поддерживаемых SqlSink и BlobSource.</span><span class="sxs-lookup"><span data-stu-id="901a2-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="901a2-308">Столбцы идентификаторов в целевой базе данных hello</span><span class="sxs-lookup"><span data-stu-id="901a2-308">Identity columns in hello target database</span></span>
<span data-ttu-id="901a2-309">В этом разделе приведен пример копирования данных из исходной таблицы без tooa назначения идентификаторов столбца таблицы со столбцом идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="901a2-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="901a2-310">**Исходная таблица:**</span><span class="sxs-lookup"><span data-stu-id="901a2-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="901a2-311">**Целевая таблица:**</span><span class="sxs-lookup"><span data-stu-id="901a2-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="901a2-312">Обратите внимание, что этот hello целевая таблица имеет столбец идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="901a2-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="901a2-313">**Определение JSON исходного набора данных**</span><span class="sxs-lookup"><span data-stu-id="901a2-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="901a2-314">**Определение JSON целевого набора данных**</span><span class="sxs-lookup"><span data-stu-id="901a2-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="901a2-315">Обратите внимание, что у исходной и целевой таблиц разные схемы (в целевой есть дополнительный столбец с идентификаторами).</span><span class="sxs-lookup"><span data-stu-id="901a2-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="901a2-316">В этом случае необходимо toospecify **структуры** свойство в определении набора данных целевого hello, который не содержит столбца идентификаторов hello.</span><span class="sxs-lookup"><span data-stu-id="901a2-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="901a2-317">Вызов хранимой процедуры из приемника SQL</span><span class="sxs-lookup"><span data-stu-id="901a2-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="901a2-318">Пример вызова хранимой процедуры из приемника SQL в действии копирования в конвейере приведен в статье [Invoke stored procedure from copy activity in Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md) (Вызов хранимой процедуры из действия копирования в фабрике данных Azure).</span><span class="sxs-lookup"><span data-stu-id="901a2-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="901a2-319">Сопоставление типов для базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="901a2-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="901a2-320">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статье действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:</span><span class="sxs-lookup"><span data-stu-id="901a2-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="901a2-321">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="901a2-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="901a2-322">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="901a2-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="901a2-323">При перемещении данных tooand из базы данных SQL Azure, hello следующие сопоставления используются из типа too.NET типа SQL и наоборот.</span><span class="sxs-lookup"><span data-stu-id="901a2-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="901a2-324">сопоставление Hello выполняется аналогично hello сопоставление типов данных SQL Server для ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="901a2-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="901a2-325">Тип ядра СУБД SQL Server</span><span class="sxs-lookup"><span data-stu-id="901a2-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="901a2-326">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="901a2-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="901a2-327">bigint</span><span class="sxs-lookup"><span data-stu-id="901a2-327">bigint</span></span> |<span data-ttu-id="901a2-328">Int64</span><span class="sxs-lookup"><span data-stu-id="901a2-328">Int64</span></span> |
| <span data-ttu-id="901a2-329">binary;</span><span class="sxs-lookup"><span data-stu-id="901a2-329">binary</span></span> |<span data-ttu-id="901a2-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="901a2-330">Byte[]</span></span> |
| <span data-ttu-id="901a2-331">bit</span><span class="sxs-lookup"><span data-stu-id="901a2-331">bit</span></span> |<span data-ttu-id="901a2-332">Логический</span><span class="sxs-lookup"><span data-stu-id="901a2-332">Boolean</span></span> |
| <span data-ttu-id="901a2-333">char;</span><span class="sxs-lookup"><span data-stu-id="901a2-333">char</span></span> |<span data-ttu-id="901a2-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="901a2-334">String, Char[]</span></span> |
| <span data-ttu-id="901a2-335">дата</span><span class="sxs-lookup"><span data-stu-id="901a2-335">date</span></span> |<span data-ttu-id="901a2-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="901a2-336">DateTime</span></span> |
| <span data-ttu-id="901a2-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="901a2-337">Datetime</span></span> |<span data-ttu-id="901a2-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="901a2-338">DateTime</span></span> |
| <span data-ttu-id="901a2-339">datetime2;</span><span class="sxs-lookup"><span data-stu-id="901a2-339">datetime2</span></span> |<span data-ttu-id="901a2-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="901a2-340">DateTime</span></span> |
| <span data-ttu-id="901a2-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="901a2-341">Datetimeoffset</span></span> |<span data-ttu-id="901a2-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="901a2-342">DateTimeOffset</span></span> |
| <span data-ttu-id="901a2-343">Decimal</span><span class="sxs-lookup"><span data-stu-id="901a2-343">Decimal</span></span> |<span data-ttu-id="901a2-344">Decimal</span><span class="sxs-lookup"><span data-stu-id="901a2-344">Decimal</span></span> |
| <span data-ttu-id="901a2-345">Атрибут FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="901a2-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="901a2-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="901a2-346">Byte[]</span></span> |
| <span data-ttu-id="901a2-347">Float</span><span class="sxs-lookup"><span data-stu-id="901a2-347">Float</span></span> |<span data-ttu-id="901a2-348">Double</span><span class="sxs-lookup"><span data-stu-id="901a2-348">Double</span></span> |
| <span data-ttu-id="901a2-349">изображение</span><span class="sxs-lookup"><span data-stu-id="901a2-349">image</span></span> |<span data-ttu-id="901a2-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="901a2-350">Byte[]</span></span> |
| <span data-ttu-id="901a2-351">int</span><span class="sxs-lookup"><span data-stu-id="901a2-351">int</span></span> |<span data-ttu-id="901a2-352">Int32</span><span class="sxs-lookup"><span data-stu-id="901a2-352">Int32</span></span> |
| <span data-ttu-id="901a2-353">money;</span><span class="sxs-lookup"><span data-stu-id="901a2-353">money</span></span> |<span data-ttu-id="901a2-354">Decimal</span><span class="sxs-lookup"><span data-stu-id="901a2-354">Decimal</span></span> |
| <span data-ttu-id="901a2-355">nchar;</span><span class="sxs-lookup"><span data-stu-id="901a2-355">nchar</span></span> |<span data-ttu-id="901a2-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="901a2-356">String, Char[]</span></span> |
| <span data-ttu-id="901a2-357">ntext</span><span class="sxs-lookup"><span data-stu-id="901a2-357">ntext</span></span> |<span data-ttu-id="901a2-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="901a2-358">String, Char[]</span></span> |
| <span data-ttu-id="901a2-359">numeric</span><span class="sxs-lookup"><span data-stu-id="901a2-359">numeric</span></span> |<span data-ttu-id="901a2-360">Decimal</span><span class="sxs-lookup"><span data-stu-id="901a2-360">Decimal</span></span> |
| <span data-ttu-id="901a2-361">nvarchar;</span><span class="sxs-lookup"><span data-stu-id="901a2-361">nvarchar</span></span> |<span data-ttu-id="901a2-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="901a2-362">String, Char[]</span></span> |
| <span data-ttu-id="901a2-363">real;</span><span class="sxs-lookup"><span data-stu-id="901a2-363">real</span></span> |<span data-ttu-id="901a2-364">Single</span><span class="sxs-lookup"><span data-stu-id="901a2-364">Single</span></span> |
| <span data-ttu-id="901a2-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="901a2-365">rowversion</span></span> |<span data-ttu-id="901a2-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="901a2-366">Byte[]</span></span> |
| <span data-ttu-id="901a2-367">smalldatetime;</span><span class="sxs-lookup"><span data-stu-id="901a2-367">smalldatetime</span></span> |<span data-ttu-id="901a2-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="901a2-368">DateTime</span></span> |
| <span data-ttu-id="901a2-369">smallint;</span><span class="sxs-lookup"><span data-stu-id="901a2-369">smallint</span></span> |<span data-ttu-id="901a2-370">Int16</span><span class="sxs-lookup"><span data-stu-id="901a2-370">Int16</span></span> |
| <span data-ttu-id="901a2-371">smallmoney;</span><span class="sxs-lookup"><span data-stu-id="901a2-371">smallmoney</span></span> |<span data-ttu-id="901a2-372">Decimal</span><span class="sxs-lookup"><span data-stu-id="901a2-372">Decimal</span></span> |
| <span data-ttu-id="901a2-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="901a2-373">sql_variant</span></span> |<span data-ttu-id="901a2-374">Object *</span><span class="sxs-lookup"><span data-stu-id="901a2-374">Object *</span></span> |
| <span data-ttu-id="901a2-375">text</span><span class="sxs-lookup"><span data-stu-id="901a2-375">text</span></span> |<span data-ttu-id="901a2-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="901a2-376">String, Char[]</span></span> |
| <span data-ttu-id="901a2-377">time</span><span class="sxs-lookup"><span data-stu-id="901a2-377">time</span></span> |<span data-ttu-id="901a2-378">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="901a2-378">TimeSpan</span></span> |
| <span data-ttu-id="901a2-379">Timestamp</span><span class="sxs-lookup"><span data-stu-id="901a2-379">timestamp</span></span> |<span data-ttu-id="901a2-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="901a2-380">Byte[]</span></span> |
| <span data-ttu-id="901a2-381">tinyint;</span><span class="sxs-lookup"><span data-stu-id="901a2-381">tinyint</span></span> |<span data-ttu-id="901a2-382">Byte</span><span class="sxs-lookup"><span data-stu-id="901a2-382">Byte</span></span> |
| <span data-ttu-id="901a2-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="901a2-383">uniqueidentifier</span></span> |<span data-ttu-id="901a2-384">Guid</span><span class="sxs-lookup"><span data-stu-id="901a2-384">Guid</span></span> |
| <span data-ttu-id="901a2-385">varbinary;</span><span class="sxs-lookup"><span data-stu-id="901a2-385">varbinary</span></span> |<span data-ttu-id="901a2-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="901a2-386">Byte[]</span></span> |
| <span data-ttu-id="901a2-387">varchar.</span><span class="sxs-lookup"><span data-stu-id="901a2-387">varchar</span></span> |<span data-ttu-id="901a2-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="901a2-388">String, Char[]</span></span> |
| <span data-ttu-id="901a2-389">xml</span><span class="sxs-lookup"><span data-stu-id="901a2-389">xml</span></span> |<span data-ttu-id="901a2-390">xml</span><span class="sxs-lookup"><span data-stu-id="901a2-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="901a2-391">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="901a2-391">Map source toosink columns</span></span>
<span data-ttu-id="901a2-392">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="901a2-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="901a2-393">Повторяющаяся операция копирования</span><span class="sxs-lookup"><span data-stu-id="901a2-393">Repeatable copy</span></span>
<span data-ttu-id="901a2-394">При копировании данных tooSQL базы данных сервера, действие копирования hello добавляет таблицу приемник toohello данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="901a2-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="901a2-395">tooperform UPSERT. Вместо этого в разделе [tooSqlSink Repeatable записи](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) статьи.</span><span class="sxs-lookup"><span data-stu-id="901a2-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="901a2-396">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="901a2-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="901a2-397">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="901a2-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="901a2-398">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="901a2-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="901a2-399">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="901a2-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="901a2-400">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="901a2-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="901a2-401">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="901a2-401">Performance and Tuning</span></span>
<span data-ttu-id="901a2-402">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="901a2-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
