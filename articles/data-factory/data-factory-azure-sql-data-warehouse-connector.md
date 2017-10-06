---
title: "aaaCopy данных в хранилище данных SQL Azure | Документы Microsoft"
description: "Узнайте, как toocopy данные из хранилища данных SQL Azure, с помощью фабрики данных Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="360fa-103">Tooand копирования данных из хранилища данных SQL Azure, с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="360fa-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="360fa-104">В этой статье объясняется, как toouse hello действие копирования в фабрике данных Azure toomove данные из хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="360fa-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="360fa-106">tooachieve Наилучшая производительность, используйте PolyBase tooload данных в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="360fa-107">Hello [PolyBase используйте tooload данных в хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) раздел содержит подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="360fa-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="360fa-108">Пошаговое руководство и пример использования см. в статье [Загрузка 1 ТБ в хранилище данных SQL Azure с помощью фабрики данных Azure [мастер копирования] менее чем за 15 минут](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="360fa-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="360fa-109">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="360fa-109">Supported scenarios</span></span>
<span data-ttu-id="360fa-110">Можно скопировать данные **из хранилища данных SQL Azure** toohello следующие хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="360fa-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="360fa-111">Можно скопировать данные из hello, следуя хранилищ данных **tooAzure хранилище данных SQL**:</span><span class="sxs-lookup"><span data-stu-id="360fa-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="360fa-112">При копировании данных из SQL Server или база данных SQL Azure tooAzure хранилище данных SQL, если таблица hello не существует в конечное хранилище hello, фабрики данных можно автоматически создать hello таблицу в хранилище данных SQL с использованием схемы hello hello таблицы в источнике hello хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="360fa-113">Дополнительные сведения см. в разделе [Автоматическое создание таблицы](#auto-table-creation).</span><span class="sxs-lookup"><span data-stu-id="360fa-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="360fa-114">Поддерживаемый тип проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="360fa-114">Supported authentication type</span></span>
<span data-ttu-id="360fa-115">Соединитель хранилища данных SQL Azure поддерживает обычную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="360fa-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="360fa-116">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="360fa-116">Getting started</span></span>
<span data-ttu-id="360fa-117">Вы можете создать конвейер с действием копирования, который перемещает данные в хранилище данных SQL Azure или из него, с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="360fa-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="360fa-118">Hello простым способом toocreate конвейера, который копирует данные из хранилища данных SQL Azure — toouse hello копирования данных мастер.</span><span class="sxs-lookup"><span data-stu-id="360fa-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="360fa-119">В разделе [учебника: загрузка данных в хранилище данных SQL с фабрикой данных](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="360fa-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="360fa-120">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="360fa-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="360fa-121">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="360fa-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="360fa-122">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="360fa-123">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="360fa-123">Create a **data factory**.</span></span> <span data-ttu-id="360fa-124">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="360fa-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="360fa-125">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="360fa-126">Например при копировании данных из хранилища данных Azure SQL tooan хранилища BLOB-объектов Azure, создается два связанных служб toolink вашей учетной записи хранилища Azure и фабрики данных tooyour хранилища данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="360fa-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="360fa-127">Свойства связанной службы, определенные tooAzure хранилище данных SQL, в разделе [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="360fa-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="360fa-128">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="360fa-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="360fa-129">В примере hello, упомянутые в последнем шаге hello создать контейнер больших двоичных объектов dataset toospecify hello и папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="360fa-130">И создайте другую таблицу hello toospecify набора данных в хранилище данных Azure SQL hello, содержащий hello данные, скопированные из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="360fa-131">Свойства набора данных, определенных tooAzure хранилище данных SQL, в разделе [свойства набора данных](#dataset-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="360fa-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="360fa-132">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="360fa-133">В примере hello приведенные выше используются BlobSource в исходной и SqlDWSink в приемник для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="360fa-134">Аналогично при копировании из хранилища данных SQL Azure tooAzure хранилища BLOB-объектов используется SqlDWSource и BlobSink в действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="360fa-135">Свойства действия копирования, определенные tooAzure хранилище данных SQL, в разделе [скопировать свойства действия](#copy-activity-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="360fa-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="360fa-136">Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="360fa-137">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="360fa-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="360fa-138">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="360fa-139">Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных SQL Azure см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="360fa-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="360fa-140">Hello в следующих разделах содержатся сведения о JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAzure хранилище данных SQL:</span><span class="sxs-lookup"><span data-stu-id="360fa-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="360fa-141">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="360fa-141">Linked service properties</span></span>
<span data-ttu-id="360fa-142">Привет, в следующей таблице приводится описание tooAzure службы хранилища данных SQL, которые связаны определенные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="360fa-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="360fa-143">Свойство</span><span class="sxs-lookup"><span data-stu-id="360fa-143">Property</span></span> | <span data-ttu-id="360fa-144">Описание</span><span class="sxs-lookup"><span data-stu-id="360fa-144">Description</span></span> | <span data-ttu-id="360fa-145">Обязательно</span><span class="sxs-lookup"><span data-stu-id="360fa-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="360fa-146">type</span><span class="sxs-lookup"><span data-stu-id="360fa-146">type</span></span> |<span data-ttu-id="360fa-147">свойство типа Hello должно быть присвоено: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="360fa-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="360fa-148">Да</span><span class="sxs-lookup"><span data-stu-id="360fa-148">Yes</span></span> |
| <span data-ttu-id="360fa-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="360fa-149">connectionString</span></span> |<span data-ttu-id="360fa-150">Укажите сведения, необходимые для свойства connectionString hello tooconnect toohello хранилище данных SQL Azure экземпляра.</span><span class="sxs-lookup"><span data-stu-id="360fa-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="360fa-151">Поддерживается только обычная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="360fa-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="360fa-152">Да</span><span class="sxs-lookup"><span data-stu-id="360fa-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="360fa-153">Настройка [брандмауэр базы данных SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) и hello сервера базы данных слишком[сервер служб Azure tooaccess hello](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="360fa-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="360fa-154">Кроме того при копировании данных tooAzure хранилище данных SQL из внешней в Azure, включая из локальных источников данных со шлюзом фабрики данных, настройте соответствующий диапазон IP-адресов для компьютера hello, передающий данные tooAzure хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="360fa-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="360fa-155">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="360fa-155">Dataset properties</span></span>
<span data-ttu-id="360fa-156">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="360fa-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="360fa-157">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="360fa-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="360fa-158">раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="360fa-159">Hello **typeProperties** раздел для набора данных hello типа **AzureSqlDWTable** имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="360fa-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="360fa-160">Свойство</span><span class="sxs-lookup"><span data-stu-id="360fa-160">Property</span></span> | <span data-ttu-id="360fa-161">Описание</span><span class="sxs-lookup"><span data-stu-id="360fa-161">Description</span></span> | <span data-ttu-id="360fa-162">Обязательно</span><span class="sxs-lookup"><span data-stu-id="360fa-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="360fa-163">tableName</span><span class="sxs-lookup"><span data-stu-id="360fa-163">tableName</span></span> |<span data-ttu-id="360fa-164">Имя hello таблицы или представления в базе данных хранилища данных SQL Azure hello, hello связанной службы относится.</span><span class="sxs-lookup"><span data-stu-id="360fa-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="360fa-165">Да</span><span class="sxs-lookup"><span data-stu-id="360fa-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="360fa-166">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="360fa-166">Copy activity properties</span></span>
<span data-ttu-id="360fa-167">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="360fa-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="360fa-168">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="360fa-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="360fa-169">Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.</span><span class="sxs-lookup"><span data-stu-id="360fa-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="360fa-170">В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="360fa-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="360fa-171">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="360fa-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="360fa-172">SqlDWSource</span></span>
<span data-ttu-id="360fa-173">Если источник имеет тип **SqlDWSource**, hello следующие свойства доступны в **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="360fa-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="360fa-174">Свойство</span><span class="sxs-lookup"><span data-stu-id="360fa-174">Property</span></span> | <span data-ttu-id="360fa-175">Описание</span><span class="sxs-lookup"><span data-stu-id="360fa-175">Description</span></span> | <span data-ttu-id="360fa-176">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="360fa-176">Allowed values</span></span> | <span data-ttu-id="360fa-177">Обязательно</span><span class="sxs-lookup"><span data-stu-id="360fa-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="360fa-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="360fa-178">sqlReaderQuery</span></span> |<span data-ttu-id="360fa-179">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="360fa-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="360fa-180">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="360fa-180">SQL query string.</span></span> <span data-ttu-id="360fa-181">Например, select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="360fa-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="360fa-182">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-182">No</span></span> |
| <span data-ttu-id="360fa-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="360fa-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="360fa-184">Имя hello хранимой процедуры, который считывает данные из таблицы источника hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="360fa-185">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="360fa-185">Name of hello stored procedure.</span></span> <span data-ttu-id="360fa-186">Hello последней инструкцией SQL должна быть инструкция SELECT в hello хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="360fa-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="360fa-187">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-187">No</span></span> |
| <span data-ttu-id="360fa-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="360fa-188">storedProcedureParameters</span></span> |<span data-ttu-id="360fa-189">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="360fa-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="360fa-190">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="360fa-190">Name/value pairs.</span></span> <span data-ttu-id="360fa-191">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="360fa-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="360fa-192">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-192">No</span></span> |

<span data-ttu-id="360fa-193">Если hello **sqlReaderQuery** указан для hello SqlDWSource, hello действие копирования запускает этот запрос для hello tooget hello хранилище данных SQL Azure исходных данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="360fa-194">Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="360fa-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="360fa-195">Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello hello набора данных JSON, используемые toobuild toorun запроса от hello хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="360fa-196">Пример: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="360fa-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="360fa-197">Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="360fa-198">Пример SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="360fa-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="360fa-199">**Определение Hello хранимые процедуры:**</span><span class="sxs-lookup"><span data-stu-id="360fa-199">**hello stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="360fa-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="360fa-200">SqlDWSink</span></span>
<span data-ttu-id="360fa-201">**SqlDWSink** поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="360fa-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="360fa-202">Свойство</span><span class="sxs-lookup"><span data-stu-id="360fa-202">Property</span></span> | <span data-ttu-id="360fa-203">Описание</span><span class="sxs-lookup"><span data-stu-id="360fa-203">Description</span></span> | <span data-ttu-id="360fa-204">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="360fa-204">Allowed values</span></span> | <span data-ttu-id="360fa-205">Обязательно</span><span class="sxs-lookup"><span data-stu-id="360fa-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="360fa-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="360fa-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="360fa-207">Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез.</span><span class="sxs-lookup"><span data-stu-id="360fa-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="360fa-208">Дополнительные сведения см. в [разделе о повторяемости](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="360fa-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="360fa-209">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="360fa-209">A query statement.</span></span> |<span data-ttu-id="360fa-210">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-210">No</span></span> |
| <span data-ttu-id="360fa-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="360fa-211">allowPolyBase</span></span> |<span data-ttu-id="360fa-212">Указывает, является ли toouse PolyBase (если применимо), а не BULKINSERT механизм.</span><span class="sxs-lookup"><span data-stu-id="360fa-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="360fa-213">**С помощью PolyBase — hello рекомендуется как tooload данные в хранилище данных SQL.**</span><span class="sxs-lookup"><span data-stu-id="360fa-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="360fa-214">В разделе [PolyBase используйте tooload данных в хранилище данных SQL Azure](#use-polybase-to-load-data-into-azure-sql-data-warehouse) раздела для отображения сведений и ограничения.</span><span class="sxs-lookup"><span data-stu-id="360fa-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="360fa-215">Да</span><span class="sxs-lookup"><span data-stu-id="360fa-215">True</span></span> <br/><span data-ttu-id="360fa-216">False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="360fa-216">False (default)</span></span> |<span data-ttu-id="360fa-217">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-217">No</span></span> |
| <span data-ttu-id="360fa-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="360fa-218">polyBaseSettings</span></span> |<span data-ttu-id="360fa-219">Группа свойств, которые могут быть указаны при hello **allowPolybase** задано слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="360fa-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="360fa-220">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-220">No</span></span> |
| <span data-ttu-id="360fa-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="360fa-221">rejectValue</span></span> |<span data-ttu-id="360fa-222">Указывает hello число или процент строк, может быть отклонено перед hello запрос завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="360fa-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="360fa-223">Узнайте больше о hello PolyBase отклонить параметры в hello **аргументы** раздел [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="360fa-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="360fa-224">0 (по умолчанию), 1, 2, ...</span><span class="sxs-lookup"><span data-stu-id="360fa-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="360fa-225">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-225">No</span></span> |
| <span data-ttu-id="360fa-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="360fa-226">rejectType</span></span> |<span data-ttu-id="360fa-227">Указывает, задан ли параметр rejectValue hello в значение литерала или в процентах.</span><span class="sxs-lookup"><span data-stu-id="360fa-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="360fa-228">Value (по умолчанию), Percentage</span><span class="sxs-lookup"><span data-stu-id="360fa-228">Value (default), Percentage</span></span> |<span data-ttu-id="360fa-229">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-229">No</span></span> |
| <span data-ttu-id="360fa-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="360fa-230">rejectSampleValue</span></span> |<span data-ttu-id="360fa-231">Определяет количество hello tooretrieve строк перед hello PolyBase повторно вычисляет процент отклоненных строк hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="360fa-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="360fa-232">1, 2, …</span></span> |<span data-ttu-id="360fa-233">Да, если **rejectType** имеет значение **percentage**.</span><span class="sxs-lookup"><span data-stu-id="360fa-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="360fa-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="360fa-234">useTypeDefault</span></span> |<span data-ttu-id="360fa-235">Указывает, как toohandle отсутствующих значений в разделенных текстовых файлов, если PolyBase получает данные из текстового файла hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="360fa-236">Дополнительные сведения об этом свойстве из подраздела аргументы hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="360fa-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="360fa-237">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="360fa-237">True, False (default)</span></span> |<span data-ttu-id="360fa-238">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-238">No</span></span> |
| <span data-ttu-id="360fa-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="360fa-239">writeBatchSize</span></span> |<span data-ttu-id="360fa-240">Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello</span><span class="sxs-lookup"><span data-stu-id="360fa-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="360fa-241">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="360fa-241">Integer (number of rows)</span></span> |<span data-ttu-id="360fa-242">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="360fa-242">No (default: 10000)</span></span> |
| <span data-ttu-id="360fa-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="360fa-243">writeBatchTimeout</span></span> |<span data-ttu-id="360fa-244">Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="360fa-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="360fa-245">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="360fa-245">timespan</span></span><br/><br/> <span data-ttu-id="360fa-246">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="360fa-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="360fa-247">Нет</span><span class="sxs-lookup"><span data-stu-id="360fa-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="360fa-248">Пример SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="360fa-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="360fa-249">Использовать PolyBase tooload данные в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="360fa-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="360fa-250">Применение **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** — это эффективный способ загрузки большого объема данных в хранилище данных SQL Azure с высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="360fa-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="360fa-251">Большой рост пропускной способности hello можно просмотреть с помощью PolyBase вместо механизм BULKINSERT по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="360fa-252">Подробное сравнение см. в разделе [Базовые показатели производительности](data-factory-copy-activity-performance.md#performance-reference).</span><span class="sxs-lookup"><span data-stu-id="360fa-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="360fa-253">Пошаговое руководство и пример использования см. в статье [Загрузка 1 ТБ в хранилище данных SQL Azure с помощью фабрики данных Azure [мастер копирования] менее чем за 15 минут](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="360fa-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="360fa-254">Если источник данных находится в **больших двоичных объектов Azure или хранилища Озера данных Azure**и формат hello совместим с PolyBase, можно скопировать непосредственно tooAzure хранилище данных SQL с помощью PolyBase.</span><span class="sxs-lookup"><span data-stu-id="360fa-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="360fa-255">Дополнительные сведения см. в разделе **[Прямое копирование с помощью PolyBase](#direct-copy-using-polybase)**.</span><span class="sxs-lookup"><span data-stu-id="360fa-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="360fa-256">Если хранилище данных источника и формат не поддерживается изначально PolyBase, можно использовать hello  **[копии промежуточного хранения, с помощью PolyBase](#staged-copy-using-polybase)**  вместо этого компонента.</span><span class="sxs-lookup"><span data-stu-id="360fa-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="360fa-257">Он также позволяет повысить пропускную способность автоматически преобразования данных hello в формате, совместимом с PolyBase и хранение данных hello в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="360fa-258">После этого данные загружаются в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="360fa-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="360fa-259">Набор hello `allowPolyBase` свойство слишком**true** как показано в hello в следующем примере для фабрики данных Azure toouse PolyBase toocopy данных в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="360fa-260">При установке allowPolyBase tootrue, можно указать конкретные свойства PolyBase с использованием hello `polyBaseSettings` группы свойств.</span><span class="sxs-lookup"><span data-stu-id="360fa-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="360fa-261">в разделе hello [SqlDWSink](#SqlDWSink) подробные сведения о свойствах, которые можно использовать с polyBaseSettings см.</span><span class="sxs-lookup"><span data-stu-id="360fa-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="360fa-262">Прямое копирование с помощью PolyBase</span><span class="sxs-lookup"><span data-stu-id="360fa-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="360fa-263">PolyBase для хранилища данных SQL напрямую поддерживает хранилище BLOB-объектов Azure и Azure Data Lake Store (с использованием субъекта-службы) в качестве источника и с определенными требованиями к формату файлов.</span><span class="sxs-lookup"><span data-stu-id="360fa-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="360fa-264">Если источник данных не отвечает требованиям hello, описанные в этом разделе, напрямую можно скопировать из источника данных хранилища tooAzure, хранилище данных SQL с помощью PolyBase.</span><span class="sxs-lookup"><span data-stu-id="360fa-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="360fa-265">В противном случае можно использовать [промежуточное копирование с помощью PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="360fa-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="360fa-266">toocopy данные из хранилища Озера данных tooSQL хранилища данных эффективно, ознакомьтесь с дополнительными [фабрики данных Azure позволяет проще и удобный toouncover полезные сведения из данных, даже при использовании хранилища Озера данных с хранилищем данных SQL](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="360fa-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="360fa-267">Если не выполняются требования к hello, фабрики данных Azure проверяет параметры hello и автоматическое переключение toohello BULKINSERT механизм для перемещения данных hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="360fa-268">Тип **связанной службы источника** — **AzureStorage** или **AzureDataLakeStore с проверкой подлинности на основе субъекта-службы**.</span><span class="sxs-lookup"><span data-stu-id="360fa-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="360fa-269">Hello **входного набора данных** относится к типу: **AzureBlob** или **AzureDataLakeStore**, и hello тип формата под `type` свойств является **OrcFormat** , или **TextFormat** с hello конфигурации:</span><span class="sxs-lookup"><span data-stu-id="360fa-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="360fa-270">Параметр `rowDelimiter` должен содержать значение **\n**.</span><span class="sxs-lookup"><span data-stu-id="360fa-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="360fa-271">`nullValue`задано слишком**пустая строка** ("»), или `treatEmptyAsNull` задано слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="360fa-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="360fa-272">`encodingName`задано слишком**utf-8**, который является **по умолчанию** значение.</span><span class="sxs-lookup"><span data-stu-id="360fa-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="360fa-273">Параметры `escapeChar`, `quoteChar`, `firstRowAsHeader` и `skipLineCount` не указываются.</span><span class="sxs-lookup"><span data-stu-id="360fa-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="360fa-274">Параметр `compression` может иметь значение **no compression**, **GZip** или **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="360fa-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="360fa-275">Имеется не `skipHeaderLineCount` в разделе **BlobSource** или **AzureDataLakeStore** для hello действие копирования в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="360fa-276">Имеется не `sliceIdentifierColumnName` в разделе **SqlDWSink** для hello действие копирования в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="360fa-277">PolyBase гарантирует, что за один цикл выполнения либо все данные будут обновлены, либо ничего не будет обновлено.</span><span class="sxs-lookup"><span data-stu-id="360fa-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="360fa-278">tooachieve **повторимость**, можно использовать `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="360fa-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="360fa-279">Имеется не `columnMapping` , используемых в hello, связанные в действии копирования.</span><span class="sxs-lookup"><span data-stu-id="360fa-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="360fa-280">промежуточное копирование с помощью PolyBase</span><span class="sxs-lookup"><span data-stu-id="360fa-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="360fa-281">Если исходные данные не соответствуют критериям hello, представленных в предыдущем разделе hello, можно включить копирование данных через промежуточный промежуточного хранилища больших двоичных объектов (не может быть хранилище Premium).</span><span class="sxs-lookup"><span data-stu-id="360fa-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="360fa-282">В этом случае фабрики данных Azure автоматически выполняет преобразование в hello данных toomeet данных требования к формату PolyBase, а затем используйте PolyBase tooload данных в хранилище данных SQL и в последней очистки временных данных из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="360fa-283">Подробные сведения о том, как работает копирование данных через промежуточное хранилище BLOB-объектов Azure, см. в разделе [Промежуточное копирование](data-factory-copy-activity-performance.md#staged-copy).</span><span class="sxs-lookup"><span data-stu-id="360fa-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="360fa-284">После копирования данных из объекта данных локального хранения в хранилище данных SQL Azure, используя PolyBase и промежуточного хранения, если ваша версия шлюза управления данными не ниже 2.4, требует JRE (среда выполнения Java) на шлюзе компьютеру, на котором находится источник данных используется tootransform в правильном формате.</span><span class="sxs-lookup"><span data-stu-id="360fa-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="360fa-285">Рекомендуем обновить ваш последний tooavoid toohello шлюза такая зависимость.</span><span class="sxs-lookup"><span data-stu-id="360fa-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="360fa-286">toouse эту функцию, создайте [связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) , обозначающий toohello учетной записи хранилища Azure с hello промежуточные BLOB-объекта хранилища, затем укажите hello `enableStaging` и `stagingSettings` свойств для действия копирования hello как показано в hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="360fa-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="360fa-287">Рекомендации по использованию PolyBase</span><span class="sxs-lookup"><span data-stu-id="360fa-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="360fa-288">Hello следующие разделы содержат дополнительные советы и рекомендации toohello те, которые упоминаются в [советы и рекомендации для хранилища данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="360fa-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="360fa-289">Необходимые разрешения базы данных</span><span class="sxs-lookup"><span data-stu-id="360fa-289">Required database permission</span></span>
<span data-ttu-id="360fa-290">toouse PolyBase, его необходимо быть пользователем hello используется tooload данных в хранилище данных SQL имеет hello [разрешение «УПРАВЛЕНИЕ»](https://msdn.microsoft.com/library/ms191291.aspx) hello целевой базе данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="360fa-291">Одним из способов tooachieve, tooadd этот пользователь является членом роли «db_owner».</span><span class="sxs-lookup"><span data-stu-id="360fa-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="360fa-292">Узнайте, как toodo, выполнив следующие [в этом разделе](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="360fa-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="360fa-293">Ограничение размера строки и типа данных</span><span class="sxs-lookup"><span data-stu-id="360fa-293">Row size and data type limitation</span></span>
<span data-ttu-id="360fa-294">Загружает Polybase ограничены tooloading строк и меньше, чем **1 МБ** и не удается загрузить tooVARCHR(MAX), NVARCHAR(MAX) или VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="360fa-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="360fa-295">См. слишком[здесь](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="360fa-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="360fa-296">Если у вас есть источник данных со строками размером более 1 МБ, вы можете toosplit hello исходных таблиц по вертикали в несколько небольших описаний, где hello наибольший размер строки в каждой из них не превышает hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="360fa-297">Затем можно загрузить Hello несколько таблиц меньшего размера, с помощью PolyBase и объединяются друг с другом в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="360fa-298">Класс ресурсов хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="360fa-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="360fa-299">tooachieve лучшие возможности пропускной способности рассмотрим tooassign больше ресурсов класса toohello пользователя, используемые tooload данные в хранилище данных SQL через PolyBase.</span><span class="sxs-lookup"><span data-stu-id="360fa-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="360fa-300">Узнайте, как toodo, выполнив следующие [измените пример класса ресурса для пользователя](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="360fa-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="360fa-301">Использование tableName в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="360fa-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="360fa-302">Hello следующей таблице приведены примеры о том, как toospecify hello **tableName** свойство в наборе данных JSON для различных сочетаний схему и имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="360fa-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="360fa-303">Схема базы данных</span><span class="sxs-lookup"><span data-stu-id="360fa-303">DB Schema</span></span> | <span data-ttu-id="360fa-304">Имя таблицы</span><span class="sxs-lookup"><span data-stu-id="360fa-304">Table name</span></span> | <span data-ttu-id="360fa-305">Свойство tableName в JSON</span><span class="sxs-lookup"><span data-stu-id="360fa-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="360fa-306">dbo</span><span class="sxs-lookup"><span data-stu-id="360fa-306">dbo</span></span> |<span data-ttu-id="360fa-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="360fa-307">MyTable</span></span> |<span data-ttu-id="360fa-308">MyTable или dbo.MyTable либо [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="360fa-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="360fa-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="360fa-309">dbo1</span></span> |<span data-ttu-id="360fa-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="360fa-310">MyTable</span></span> |<span data-ttu-id="360fa-311">dbo1.MyTable или [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="360fa-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="360fa-312">dbo</span><span class="sxs-lookup"><span data-stu-id="360fa-312">dbo</span></span> |<span data-ttu-id="360fa-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="360fa-313">My.Table</span></span> |<span data-ttu-id="360fa-314">[My.Table] или [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="360fa-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="360fa-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="360fa-315">dbo1</span></span> |<span data-ttu-id="360fa-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="360fa-316">My.Table</span></span> |<span data-ttu-id="360fa-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="360fa-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="360fa-318">Если появится следующая ошибка hello, это может быть проблема с hello значение, указанное для hello свойство tableName.</span><span class="sxs-lookup"><span data-stu-id="360fa-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="360fa-319">См. таблице hello hello правильно toospecify значений свойства JSON tableName hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="360fa-320">Столбцы со значениями по умолчанию</span><span class="sxs-lookup"><span data-stu-id="360fa-320">Columns with default values</span></span>
<span data-ttu-id="360fa-321">В настоящее время функция в фабрике данных принимает только PolyBase hello одинаковое количество столбцов в целевой таблице hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="360fa-322">Предположим, у вас есть таблица с четырьмя столбцами и один из них определен со значением по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="360fa-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="360fa-323">Hello входные данные должны по-прежнему содержит четыре столбца.</span><span class="sxs-lookup"><span data-stu-id="360fa-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="360fa-324">Предоставление 3 столбец входного набора данных были бы получены аналогичные toohello ошибки, сообщением:</span><span class="sxs-lookup"><span data-stu-id="360fa-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="360fa-325">Значение NULL рассматривается как вариант значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="360fa-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="360fa-326">Если hello столбец допускает значения NULL, hello входных данных (в BLOB-объектов) для этого столбца может быть пустым (не может отсутствовать из входного набора данных hello).</span><span class="sxs-lookup"><span data-stu-id="360fa-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="360fa-327">PolyBase вставит значение NULL для них в hello хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="360fa-328">Автоматическое создание таблицы</span><span class="sxs-lookup"><span data-stu-id="360fa-328">Auto table creation</span></span>
<span data-ttu-id="360fa-329">Если вы используете мастер копирования toocopy данные из SQL Server или база данных SQL Azure tooAzure хранилище данных SQL и hello таблицы, которая соответствует toohello исходной таблицы не существует в конечное хранилище hello, фабрики данных можно автоматически создать таблицу hello в hello хранилище данных с помощью схемы исходной таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="360fa-330">Фабрика данных создает таблицу hello в конечное хранилище hello с hello, имя в хранилище данных источника hello же таблицы.</span><span class="sxs-lookup"><span data-stu-id="360fa-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="360fa-331">Hello типы данных для столбцов выбираются основании после сопоставления типа hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="360fa-332">При необходимости выполняет toofix преобразования типа любые проблемы совместимости между хранилищами источника и назначения.</span><span class="sxs-lookup"><span data-stu-id="360fa-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="360fa-333">Также используется распределение таблиц методом циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="360fa-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="360fa-334">Тип столбца исходной базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="360fa-334">Source SQL Database column type</span></span> | <span data-ttu-id="360fa-335">Тип столбца целевого хранилища данных SQL (ограничение размера)</span><span class="sxs-lookup"><span data-stu-id="360fa-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="360fa-336">int</span><span class="sxs-lookup"><span data-stu-id="360fa-336">Int</span></span> | <span data-ttu-id="360fa-337">int</span><span class="sxs-lookup"><span data-stu-id="360fa-337">Int</span></span> |
| <span data-ttu-id="360fa-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="360fa-338">BigInt</span></span> | <span data-ttu-id="360fa-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="360fa-339">BigInt</span></span> |
| <span data-ttu-id="360fa-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="360fa-340">SmallInt</span></span> | <span data-ttu-id="360fa-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="360fa-341">SmallInt</span></span> |
| <span data-ttu-id="360fa-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="360fa-342">TinyInt</span></span> | <span data-ttu-id="360fa-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="360fa-343">TinyInt</span></span> |
| <span data-ttu-id="360fa-344">Bit</span><span class="sxs-lookup"><span data-stu-id="360fa-344">Bit</span></span> | <span data-ttu-id="360fa-345">Bit</span><span class="sxs-lookup"><span data-stu-id="360fa-345">Bit</span></span> |
| <span data-ttu-id="360fa-346">Decimal</span><span class="sxs-lookup"><span data-stu-id="360fa-346">Decimal</span></span> | <span data-ttu-id="360fa-347">Decimal</span><span class="sxs-lookup"><span data-stu-id="360fa-347">Decimal</span></span> |
| <span data-ttu-id="360fa-348">Числовой</span><span class="sxs-lookup"><span data-stu-id="360fa-348">Numeric</span></span> | <span data-ttu-id="360fa-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="360fa-349">Decimal</span></span> |
| <span data-ttu-id="360fa-350">Float</span><span class="sxs-lookup"><span data-stu-id="360fa-350">Float</span></span> | <span data-ttu-id="360fa-351">Float</span><span class="sxs-lookup"><span data-stu-id="360fa-351">Float</span></span> |
| <span data-ttu-id="360fa-352">Money</span><span class="sxs-lookup"><span data-stu-id="360fa-352">Money</span></span> | <span data-ttu-id="360fa-353">Money</span><span class="sxs-lookup"><span data-stu-id="360fa-353">Money</span></span> |
| <span data-ttu-id="360fa-354">Real</span><span class="sxs-lookup"><span data-stu-id="360fa-354">Real</span></span> | <span data-ttu-id="360fa-355">Real</span><span class="sxs-lookup"><span data-stu-id="360fa-355">Real</span></span> |
| <span data-ttu-id="360fa-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="360fa-356">SmallMoney</span></span> | <span data-ttu-id="360fa-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="360fa-357">SmallMoney</span></span> |
| <span data-ttu-id="360fa-358">Binary</span><span class="sxs-lookup"><span data-stu-id="360fa-358">Binary</span></span> | <span data-ttu-id="360fa-359">Binary</span><span class="sxs-lookup"><span data-stu-id="360fa-359">Binary</span></span> |
| <span data-ttu-id="360fa-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="360fa-360">Varbinary</span></span> | <span data-ttu-id="360fa-361">Varbinary (вверх too8000)</span><span class="sxs-lookup"><span data-stu-id="360fa-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="360fa-362">Дата</span><span class="sxs-lookup"><span data-stu-id="360fa-362">Date</span></span> | <span data-ttu-id="360fa-363">Дата</span><span class="sxs-lookup"><span data-stu-id="360fa-363">Date</span></span> |
| <span data-ttu-id="360fa-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="360fa-364">DateTime</span></span> | <span data-ttu-id="360fa-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="360fa-365">DateTime</span></span> |
| <span data-ttu-id="360fa-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="360fa-366">DateTime2</span></span> | <span data-ttu-id="360fa-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="360fa-367">DateTime2</span></span> |
| <span data-ttu-id="360fa-368">Время</span><span class="sxs-lookup"><span data-stu-id="360fa-368">Time</span></span> | <span data-ttu-id="360fa-369">Время</span><span class="sxs-lookup"><span data-stu-id="360fa-369">Time</span></span> |
| <span data-ttu-id="360fa-370">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="360fa-370">DateTimeOffset</span></span> | <span data-ttu-id="360fa-371">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="360fa-371">DateTimeOffset</span></span> |
| <span data-ttu-id="360fa-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="360fa-372">SmallDateTime</span></span> | <span data-ttu-id="360fa-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="360fa-373">SmallDateTime</span></span> |
| <span data-ttu-id="360fa-374">текст</span><span class="sxs-lookup"><span data-stu-id="360fa-374">Text</span></span> | <span data-ttu-id="360fa-375">Varchar (вверх too8000)</span><span class="sxs-lookup"><span data-stu-id="360fa-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="360fa-376">NText</span><span class="sxs-lookup"><span data-stu-id="360fa-376">NText</span></span> | <span data-ttu-id="360fa-377">NVarChar (вверх too4000)</span><span class="sxs-lookup"><span data-stu-id="360fa-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="360fa-378">Образ —</span><span class="sxs-lookup"><span data-stu-id="360fa-378">Image</span></span> | <span data-ttu-id="360fa-379">VarBinary (вверх too8000)</span><span class="sxs-lookup"><span data-stu-id="360fa-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="360fa-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="360fa-380">UniqueIdentifier</span></span> | <span data-ttu-id="360fa-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="360fa-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="360fa-382">Char</span><span class="sxs-lookup"><span data-stu-id="360fa-382">Char</span></span> | <span data-ttu-id="360fa-383">Char</span><span class="sxs-lookup"><span data-stu-id="360fa-383">Char</span></span> |
| <span data-ttu-id="360fa-384">NCHAR</span><span class="sxs-lookup"><span data-stu-id="360fa-384">NChar</span></span> | <span data-ttu-id="360fa-385">NCHAR</span><span class="sxs-lookup"><span data-stu-id="360fa-385">NChar</span></span> |
| <span data-ttu-id="360fa-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="360fa-386">VarChar</span></span> | <span data-ttu-id="360fa-387">VarChar (вверх too8000)</span><span class="sxs-lookup"><span data-stu-id="360fa-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="360fa-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="360fa-388">NVarChar</span></span> | <span data-ttu-id="360fa-389">NVarChar (вверх too4000)</span><span class="sxs-lookup"><span data-stu-id="360fa-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="360fa-390">xml</span><span class="sxs-lookup"><span data-stu-id="360fa-390">Xml</span></span> | <span data-ttu-id="360fa-391">Varchar (вверх too8000)</span><span class="sxs-lookup"><span data-stu-id="360fa-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="360fa-392">Сопоставление типов для хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="360fa-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="360fa-393">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:</span><span class="sxs-lookup"><span data-stu-id="360fa-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="360fa-394">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="360fa-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="360fa-395">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="360fa-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="360fa-396">При перемещении данных слишком & из хранилища данных SQL Azure, hello следующие сопоставления используются из типа too.NET типа SQL и наоборот.</span><span class="sxs-lookup"><span data-stu-id="360fa-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="360fa-397">сопоставление Hello — то же, что hello [сопоставление типов данных SQL Server для ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="360fa-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="360fa-398">Тип ядра СУБД SQL Server</span><span class="sxs-lookup"><span data-stu-id="360fa-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="360fa-399">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="360fa-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="360fa-400">bigint</span><span class="sxs-lookup"><span data-stu-id="360fa-400">bigint</span></span> |<span data-ttu-id="360fa-401">Int64</span><span class="sxs-lookup"><span data-stu-id="360fa-401">Int64</span></span> |
| <span data-ttu-id="360fa-402">binary;</span><span class="sxs-lookup"><span data-stu-id="360fa-402">binary</span></span> |<span data-ttu-id="360fa-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="360fa-403">Byte[]</span></span> |
| <span data-ttu-id="360fa-404">bit</span><span class="sxs-lookup"><span data-stu-id="360fa-404">bit</span></span> |<span data-ttu-id="360fa-405">Логический</span><span class="sxs-lookup"><span data-stu-id="360fa-405">Boolean</span></span> |
| <span data-ttu-id="360fa-406">char;</span><span class="sxs-lookup"><span data-stu-id="360fa-406">char</span></span> |<span data-ttu-id="360fa-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="360fa-407">String, Char[]</span></span> |
| <span data-ttu-id="360fa-408">дата</span><span class="sxs-lookup"><span data-stu-id="360fa-408">date</span></span> |<span data-ttu-id="360fa-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="360fa-409">DateTime</span></span> |
| <span data-ttu-id="360fa-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="360fa-410">Datetime</span></span> |<span data-ttu-id="360fa-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="360fa-411">DateTime</span></span> |
| <span data-ttu-id="360fa-412">datetime2;</span><span class="sxs-lookup"><span data-stu-id="360fa-412">datetime2</span></span> |<span data-ttu-id="360fa-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="360fa-413">DateTime</span></span> |
| <span data-ttu-id="360fa-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="360fa-414">Datetimeoffset</span></span> |<span data-ttu-id="360fa-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="360fa-415">DateTimeOffset</span></span> |
| <span data-ttu-id="360fa-416">Decimal</span><span class="sxs-lookup"><span data-stu-id="360fa-416">Decimal</span></span> |<span data-ttu-id="360fa-417">Decimal</span><span class="sxs-lookup"><span data-stu-id="360fa-417">Decimal</span></span> |
| <span data-ttu-id="360fa-418">Атрибут FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="360fa-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="360fa-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="360fa-419">Byte[]</span></span> |
| <span data-ttu-id="360fa-420">Float</span><span class="sxs-lookup"><span data-stu-id="360fa-420">Float</span></span> |<span data-ttu-id="360fa-421">Double</span><span class="sxs-lookup"><span data-stu-id="360fa-421">Double</span></span> |
| <span data-ttu-id="360fa-422">изображение</span><span class="sxs-lookup"><span data-stu-id="360fa-422">image</span></span> |<span data-ttu-id="360fa-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="360fa-423">Byte[]</span></span> |
| <span data-ttu-id="360fa-424">int</span><span class="sxs-lookup"><span data-stu-id="360fa-424">int</span></span> |<span data-ttu-id="360fa-425">Int32</span><span class="sxs-lookup"><span data-stu-id="360fa-425">Int32</span></span> |
| <span data-ttu-id="360fa-426">money;</span><span class="sxs-lookup"><span data-stu-id="360fa-426">money</span></span> |<span data-ttu-id="360fa-427">Decimal</span><span class="sxs-lookup"><span data-stu-id="360fa-427">Decimal</span></span> |
| <span data-ttu-id="360fa-428">nchar;</span><span class="sxs-lookup"><span data-stu-id="360fa-428">nchar</span></span> |<span data-ttu-id="360fa-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="360fa-429">String, Char[]</span></span> |
| <span data-ttu-id="360fa-430">ntext</span><span class="sxs-lookup"><span data-stu-id="360fa-430">ntext</span></span> |<span data-ttu-id="360fa-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="360fa-431">String, Char[]</span></span> |
| <span data-ttu-id="360fa-432">numeric</span><span class="sxs-lookup"><span data-stu-id="360fa-432">numeric</span></span> |<span data-ttu-id="360fa-433">Decimal</span><span class="sxs-lookup"><span data-stu-id="360fa-433">Decimal</span></span> |
| <span data-ttu-id="360fa-434">nvarchar;</span><span class="sxs-lookup"><span data-stu-id="360fa-434">nvarchar</span></span> |<span data-ttu-id="360fa-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="360fa-435">String, Char[]</span></span> |
| <span data-ttu-id="360fa-436">real;</span><span class="sxs-lookup"><span data-stu-id="360fa-436">real</span></span> |<span data-ttu-id="360fa-437">Single</span><span class="sxs-lookup"><span data-stu-id="360fa-437">Single</span></span> |
| <span data-ttu-id="360fa-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="360fa-438">rowversion</span></span> |<span data-ttu-id="360fa-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="360fa-439">Byte[]</span></span> |
| <span data-ttu-id="360fa-440">smalldatetime;</span><span class="sxs-lookup"><span data-stu-id="360fa-440">smalldatetime</span></span> |<span data-ttu-id="360fa-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="360fa-441">DateTime</span></span> |
| <span data-ttu-id="360fa-442">smallint;</span><span class="sxs-lookup"><span data-stu-id="360fa-442">smallint</span></span> |<span data-ttu-id="360fa-443">Int16</span><span class="sxs-lookup"><span data-stu-id="360fa-443">Int16</span></span> |
| <span data-ttu-id="360fa-444">smallmoney;</span><span class="sxs-lookup"><span data-stu-id="360fa-444">smallmoney</span></span> |<span data-ttu-id="360fa-445">Decimal</span><span class="sxs-lookup"><span data-stu-id="360fa-445">Decimal</span></span> |
| <span data-ttu-id="360fa-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="360fa-446">sql_variant</span></span> |<span data-ttu-id="360fa-447">Object *</span><span class="sxs-lookup"><span data-stu-id="360fa-447">Object *</span></span> |
| <span data-ttu-id="360fa-448">text</span><span class="sxs-lookup"><span data-stu-id="360fa-448">text</span></span> |<span data-ttu-id="360fa-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="360fa-449">String, Char[]</span></span> |
| <span data-ttu-id="360fa-450">time</span><span class="sxs-lookup"><span data-stu-id="360fa-450">time</span></span> |<span data-ttu-id="360fa-451">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="360fa-451">TimeSpan</span></span> |
| <span data-ttu-id="360fa-452">Timestamp</span><span class="sxs-lookup"><span data-stu-id="360fa-452">timestamp</span></span> |<span data-ttu-id="360fa-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="360fa-453">Byte[]</span></span> |
| <span data-ttu-id="360fa-454">tinyint;</span><span class="sxs-lookup"><span data-stu-id="360fa-454">tinyint</span></span> |<span data-ttu-id="360fa-455">Byte</span><span class="sxs-lookup"><span data-stu-id="360fa-455">Byte</span></span> |
| <span data-ttu-id="360fa-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="360fa-456">uniqueidentifier</span></span> |<span data-ttu-id="360fa-457">Guid</span><span class="sxs-lookup"><span data-stu-id="360fa-457">Guid</span></span> |
| <span data-ttu-id="360fa-458">varbinary;</span><span class="sxs-lookup"><span data-stu-id="360fa-458">varbinary</span></span> |<span data-ttu-id="360fa-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="360fa-459">Byte[]</span></span> |
| <span data-ttu-id="360fa-460">varchar.</span><span class="sxs-lookup"><span data-stu-id="360fa-460">varchar</span></span> |<span data-ttu-id="360fa-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="360fa-461">String, Char[]</span></span> |
| <span data-ttu-id="360fa-462">xml</span><span class="sxs-lookup"><span data-stu-id="360fa-462">xml</span></span> |<span data-ttu-id="360fa-463">xml</span><span class="sxs-lookup"><span data-stu-id="360fa-463">Xml</span></span> |

<span data-ttu-id="360fa-464">Также можно сопоставить столбцы из источника toocolumns набора данных из набора данных приемник в определении действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="360fa-465">Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="360fa-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="360fa-466">Примеры JSON для копирования данных tooand из хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="360fa-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="360fa-467">Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="360fa-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="360fa-468">Они показывают как toocopy tooand данные из хранилища данных SQL Azure и хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="360fa-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="360fa-469">Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="360fa-470">Пример: Копирование данных из хранилища данных SQL Azure tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="360fa-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="360fa-471">Образец Hello определяет hello, следуя фабрики данных сущности:</span><span class="sxs-lookup"><span data-stu-id="360fa-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="360fa-472">Связанная служба типа [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="360fa-473">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="360fa-474">Входной [набор данных](data-factory-create-datasets.md) типа [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="360fa-475">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="360fa-476">Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlDWSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="360fa-477">Образец Hello копирует данные временных рядов (каждый час, день, т. д.) из таблицы в большом двоичном объекте tooa базы данных хранилища данных SQL Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="360fa-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="360fa-478">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="360fa-479">**Связанная служба хранилища данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="360fa-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="360fa-480">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="360fa-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="360fa-481">**Входной набор данных хранилища данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="360fa-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="360fa-482">Образец Hello предполагается создания таблицы «MyTable» в хранилище данных SQL Azure и содержит столбец с именем «timestampcolumn» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="360fa-483">Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="360fa-484">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="360fa-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="360fa-485">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="360fa-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="360fa-486">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="360fa-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="360fa-487">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="360fa-488">**Действие копирования в конвейере с источником SqlDWSource и приемником BlobSink**</span><span class="sxs-lookup"><span data-stu-id="360fa-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="360fa-489">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="360fa-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="360fa-490">В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlDWSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="360fa-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="360fa-491">запрос SQL Hello, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="360fa-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> <span data-ttu-id="360fa-492">В примере hello **sqlReaderQuery** указан для hello SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="360fa-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="360fa-493">Действие копирования Hello этот запрос запускает hello tooget hello хранилище данных SQL Azure исходных данных.</span><span class="sxs-lookup"><span data-stu-id="360fa-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="360fa-494">Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="360fa-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="360fa-495">Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello hello набора данных JSON, используемые toobuild запроса (выберите column1, column2 из mytable) toorun от hello хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="360fa-496">Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="360fa-497">Пример: Копирование данных из больших двоичных объектов Azure tooAzure хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="360fa-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="360fa-498">Образец Hello определяет hello, следуя фабрики данных сущности:</span><span class="sxs-lookup"><span data-stu-id="360fa-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="360fa-499">Связанная служба типа [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="360fa-500">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="360fa-501">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="360fa-502">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="360fa-503">Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, которое использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="360fa-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="360fa-504">Образец Hello копирует данные временных рядов (каждый час, день, т. д.) из таблицы tooa BLOB-объектов Azure в базе данных хранилища данных SQL Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="360fa-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="360fa-505">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="360fa-506">**Связанная служба хранилища данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="360fa-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="360fa-507">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="360fa-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="360fa-508">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="360fa-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="360fa-509">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="360fa-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="360fa-510">Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="360fa-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="360fa-511">путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="360fa-512">«external»: параметр «true» уведомляет службу hello фабрики данных, что эта таблица является внешней toohello фабрики данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="360fa-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="360fa-513">**Выходной набор данных хранилища данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="360fa-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="360fa-514">Образец Hello копирует tooa таблицу данных, с именем «MyTable» в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="360fa-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="360fa-515">Создать таблицу hello в хранилище данных SQL Azure с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="360fa-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="360fa-516">Новые строки добавляются в таблицу toohello каждый час.</span><span class="sxs-lookup"><span data-stu-id="360fa-516">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="360fa-517">**Действие копирования в конвейере с источником BlobSource и приемником SqlDWSink**</span><span class="sxs-lookup"><span data-stu-id="360fa-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="360fa-518">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="360fa-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="360fa-519">В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="360fa-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="360fa-520">Пошаговые инструкции см. в разделе hello. в разделе [загрузить 1 ТБ в хранилище данных SQL Azure в разделе 15 минут с фабрикой данных Azure](data-factory-load-sql-data-warehouse.md) и [загрузки данных с фабрикой данных Azure](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) статьи в hello хранилище данных SQL Azure документация.</span><span class="sxs-lookup"><span data-stu-id="360fa-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="360fa-521">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="360fa-521">Performance and Tuning</span></span>
<span data-ttu-id="360fa-522">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="360fa-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
