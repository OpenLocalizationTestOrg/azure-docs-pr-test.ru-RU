---
title: "Копирование данных в базу данных SQL Azure и из нее | Документация Майкрософт"
description: "Узнайте, как копировать данные в базу данных SQL Azure и из нее с помощью фабрики данных Azure."
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
ms.openlocfilehash: a64d13fa7dc5f50c259b98774be80b603dce400a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="392c7-103">Копирование данных в базу данных SQL Azure и из нее с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="392c7-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="392c7-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure перемещать данные в базу данных SQL и обратно.</span><span class="sxs-lookup"><span data-stu-id="392c7-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="392c7-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="392c7-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="392c7-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="392c7-106">Supported scenarios</span></span>
<span data-ttu-id="392c7-107">Данные можно скопировать **из базы данных SQL Azure** в следующие хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="392c7-107">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="392c7-108">Данные можно скопировать **в базу данных SQL Azure** из следующих хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="392c7-108">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="392c7-109">Поддерживаемый тип проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="392c7-109">Supported authentication type</span></span>
<span data-ttu-id="392c7-110">Соединитель базы данных SQL Azure поддерживает обычную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="392c7-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="392c7-111">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="392c7-111">Getting started</span></span>
<span data-ttu-id="392c7-112">Можно создать конвейер с действием копирования, которое перемещает данные из базы данных SQL Azure или в нее с помощью различных инструментов и API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="392c7-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="392c7-113">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="392c7-113">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="392c7-114">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="392c7-115">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="392c7-115">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="392c7-116">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="392c7-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="392c7-117">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="392c7-117">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="392c7-118">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="392c7-118">Create a **data factory**.</span></span> <span data-ttu-id="392c7-119">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="392c7-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="392c7-120">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-120">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="392c7-121">Например, при копировании данных из хранилища BLOB-объектов Azure в базу данных SQL Azure создайте две связанные службы, чтобы связать учетную запись хранения Azure и базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-121">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="392c7-122">Сведения о свойствах связанной службы, относящихся к базе данных SQL Azure, см. в разделе [Свойства связанной службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-122">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="392c7-123">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="392c7-123">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="392c7-124">В примере, упомянутом в последнем шаге, создайте набор данных, чтобы указать контейнер BLOB-объектов и папку, содержащую входные данные.</span><span class="sxs-lookup"><span data-stu-id="392c7-124">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="392c7-125">И создайте другой набор данных, чтобы в установить таблицу SQL в базе данных SQL Azure, содержащую данные, скопированные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="392c7-125">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="392c7-126">Сведения о свойствах набора данных, относящихся к Azure Data Lake Store, см. в разделе [Свойства набора данных](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-126">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="392c7-127">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="392c7-128">В примере выше BlobSource используется как источник, а SqlSink — как приемник для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="392c7-128">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="392c7-129">Аналогично, при копировании из базы данных SQL Azure в хранилище BLOB-объектов Azure в действии копирования используются SqlSource и BlobSink.</span><span class="sxs-lookup"><span data-stu-id="392c7-129">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="392c7-130">Сведения о свойствах действия копирования, относящихся к базе данных SQL Azure, см. в разделе [Свойства действия копирования](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-130">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="392c7-131">Для получения сведений о том, как использовать хранилище данных как источник или приемник, щелкните ссылку в предыдущем разделе об источнике данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-131">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="392c7-132">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="392c7-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="392c7-133">При использовании средств и API-интерфейсов (за исключением .NET API) эти сущности фабрики данных определяются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="392c7-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="392c7-134">Примеры с определениями JSON для сущностей фабрики данных, которые используются для копирования данных из базы данных SQL Azure, см. в разделе [Примеры определений JSON](#json-examples-for-copying-data-to-and-from-sql-database) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="392c7-134">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="392c7-135">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="392c7-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="392c7-136">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="392c7-136">Linked service properties</span></span>
<span data-ttu-id="392c7-137">Связанная служба Azure SQL связывает базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-137">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="392c7-138">В таблице ниже приведено описание элементов JSON, которые относятся к связанной службе SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="392c7-138">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="392c7-139">Свойство</span><span class="sxs-lookup"><span data-stu-id="392c7-139">Property</span></span> | <span data-ttu-id="392c7-140">Описание</span><span class="sxs-lookup"><span data-stu-id="392c7-140">Description</span></span> | <span data-ttu-id="392c7-141">Обязательно</span><span class="sxs-lookup"><span data-stu-id="392c7-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="392c7-142">type</span><span class="sxs-lookup"><span data-stu-id="392c7-142">type</span></span> |<span data-ttu-id="392c7-143">Для свойства type необходимо задать значение **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="392c7-143">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="392c7-144">Да</span><span class="sxs-lookup"><span data-stu-id="392c7-144">Yes</span></span> |
| <span data-ttu-id="392c7-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="392c7-145">connectionString</span></span> |<span data-ttu-id="392c7-146">В свойстве connectionString указываются сведения, необходимые для подключения к экземпляру базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="392c7-146">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="392c7-147">Поддерживается только обычная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="392c7-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="392c7-148">Да</span><span class="sxs-lookup"><span data-stu-id="392c7-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="392c7-149">[Брандмауэр базы данных SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) необходимо настроить, чтобы [разрешить службам Azure получать доступ к серверу](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="392c7-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="392c7-150">Кроме того, при копировании данных в базу данных SQL Azure из внешнего по отношению к Azure источника, включая локальные источники данных, с помощью шлюза фабрики данных необходимо настроить соответствующий диапазон IP-адресов для компьютера, который отправляет данные в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="392c7-150">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="392c7-151">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="392c7-151">Dataset properties</span></span>
<span data-ttu-id="392c7-152">Чтобы указать набор данных, представляющий входные или выходные данные в базе данных SQL Azure, присвойте свойству типа набора данных значение **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="392c7-152">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="392c7-153">Для свойства **linkedServiceName** набора данных задайте имя связанной службы Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="392c7-153">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="392c7-154">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="392c7-154">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="392c7-155">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="392c7-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="392c7-156">Раздел typeProperties во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-156">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="392c7-157">Раздел **typeProperties** набора данных с типом **AzureSqlTable** содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="392c7-157">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="392c7-158">Свойство</span><span class="sxs-lookup"><span data-stu-id="392c7-158">Property</span></span> | <span data-ttu-id="392c7-159">Описание</span><span class="sxs-lookup"><span data-stu-id="392c7-159">Description</span></span> | <span data-ttu-id="392c7-160">Обязательно</span><span class="sxs-lookup"><span data-stu-id="392c7-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="392c7-161">tableName</span><span class="sxs-lookup"><span data-stu-id="392c7-161">tableName</span></span> |<span data-ttu-id="392c7-162">Имя таблицы или представления в экземпляре базы данных SQL Azure, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="392c7-162">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="392c7-163">Да</span><span class="sxs-lookup"><span data-stu-id="392c7-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="392c7-164">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="392c7-164">Copy activity properties</span></span>
<span data-ttu-id="392c7-165">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="392c7-165">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="392c7-166">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="392c7-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="392c7-167">Действие копирования принимает только один набор входных данных и возвращает только один набор выходных.</span><span class="sxs-lookup"><span data-stu-id="392c7-167">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="392c7-168">В свою очередь свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="392c7-168">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="392c7-169">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="392c7-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="392c7-170">При перемещении данных из Базы данных SQL Azure в действии копирования задается тип источника **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="392c7-170">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="392c7-171">Аналогично, при перемещении данных в Базу данных SQL Azure в действии копирования задается тип источника **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="392c7-171">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="392c7-172">Этот раздел содержит список свойств, поддерживаемых типами SqlSource и SqlSink.</span><span class="sxs-lookup"><span data-stu-id="392c7-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="392c7-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="392c7-173">SqlSource</span></span>
<span data-ttu-id="392c7-174">Для действия копирования, если источник относится к типу **SqlSource**, в разделе **typeProperties** доступны указанные ниже свойства:</span><span class="sxs-lookup"><span data-stu-id="392c7-174">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="392c7-175">Свойство</span><span class="sxs-lookup"><span data-stu-id="392c7-175">Property</span></span> | <span data-ttu-id="392c7-176">Описание</span><span class="sxs-lookup"><span data-stu-id="392c7-176">Description</span></span> | <span data-ttu-id="392c7-177">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="392c7-177">Allowed values</span></span> | <span data-ttu-id="392c7-178">Обязательно</span><span class="sxs-lookup"><span data-stu-id="392c7-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="392c7-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="392c7-179">sqlReaderQuery</span></span> |<span data-ttu-id="392c7-180">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-180">Use the custom query to read data.</span></span> |<span data-ttu-id="392c7-181">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="392c7-181">SQL query string.</span></span> <span data-ttu-id="392c7-182">Пример: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="392c7-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="392c7-183">Нет</span><span class="sxs-lookup"><span data-stu-id="392c7-183">No</span></span> |
| <span data-ttu-id="392c7-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="392c7-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="392c7-185">Имя хранимой процедуры, которая считывает данные из исходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="392c7-185">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="392c7-186">Имя хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="392c7-186">Name of the stored procedure.</span></span> <span data-ttu-id="392c7-187">Последней инструкцией SQL должна быть инструкция SELECT в хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="392c7-187">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="392c7-188">Нет</span><span class="sxs-lookup"><span data-stu-id="392c7-188">No</span></span> |
| <span data-ttu-id="392c7-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="392c7-189">storedProcedureParameters</span></span> |<span data-ttu-id="392c7-190">Параметры для хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="392c7-190">Parameters for the stored procedure.</span></span> |<span data-ttu-id="392c7-191">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="392c7-191">Name/value pairs.</span></span> <span data-ttu-id="392c7-192">Имена и регистр параметров должны совпадать с именами и регистром параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="392c7-192">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="392c7-193">Нет</span><span class="sxs-lookup"><span data-stu-id="392c7-193">No</span></span> |

<span data-ttu-id="392c7-194">Если для SqlSource указано **sqlReaderQuery** , то действие копирования выполняет этот запрос для источника базы данных SQL Azure для получения данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-194">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="392c7-195">Кроме того, можно создать хранимую процедуру, указав **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="392c7-195">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="392c7-196">Если не указать sqlReaderQuery или sqlReaderStoredProcedureName, то для построения запроса (`select column1, column2 from mytable`) к базе данных SQL Azure будут использованы столбцы, определенные в разделе структуры набора данных JSON.</span><span class="sxs-lookup"><span data-stu-id="392c7-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="392c7-197">Если у определения набора данных нет структуры, выбираются все столбцы из таблицы.</span><span class="sxs-lookup"><span data-stu-id="392c7-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="392c7-198">При использовании **sqlReaderStoredProcedureName** по-прежнему необходимо указать значение свойства **tableName** в наборе данных JSON.</span><span class="sxs-lookup"><span data-stu-id="392c7-198">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="392c7-199">Хотя какие-либо проверки этой таблицы отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="392c7-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="392c7-200">Пример SqlSource</span><span class="sxs-lookup"><span data-stu-id="392c7-200">SqlSource example</span></span>

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

<span data-ttu-id="392c7-201">**Определение хранимой процедуры:**</span><span class="sxs-lookup"><span data-stu-id="392c7-201">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="392c7-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="392c7-202">SqlSink</span></span>
<span data-ttu-id="392c7-203">**SqlSink** поддерживает указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="392c7-203">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="392c7-204">Свойство</span><span class="sxs-lookup"><span data-stu-id="392c7-204">Property</span></span> | <span data-ttu-id="392c7-205">Описание</span><span class="sxs-lookup"><span data-stu-id="392c7-205">Description</span></span> | <span data-ttu-id="392c7-206">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="392c7-206">Allowed values</span></span> | <span data-ttu-id="392c7-207">Обязательно</span><span class="sxs-lookup"><span data-stu-id="392c7-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="392c7-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="392c7-208">writeBatchTimeout</span></span> |<span data-ttu-id="392c7-209">Время ожидания до выполнения операции пакетной вставки, пока не завершится срок ее действия.</span><span class="sxs-lookup"><span data-stu-id="392c7-209">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="392c7-210">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="392c7-210">timespan</span></span><br/><br/> <span data-ttu-id="392c7-211">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="392c7-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="392c7-212">Нет</span><span class="sxs-lookup"><span data-stu-id="392c7-212">No</span></span> |
| <span data-ttu-id="392c7-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="392c7-213">writeBatchSize</span></span> |<span data-ttu-id="392c7-214">Вставляет данные в таблицу SQL, когда размер буфера достигает значения writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="392c7-214">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="392c7-215">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="392c7-215">Integer (number of rows)</span></span> |<span data-ttu-id="392c7-216">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="392c7-216">No (default: 10000)</span></span> |
| <span data-ttu-id="392c7-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="392c7-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="392c7-218">Укажите запрос на выполнение действия копирования, позволяющий убедиться в том, что данные конкретного среза очищены.</span><span class="sxs-lookup"><span data-stu-id="392c7-218">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="392c7-219">Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="392c7-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="392c7-220">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="392c7-220">A query statement.</span></span> |<span data-ttu-id="392c7-221">Нет</span><span class="sxs-lookup"><span data-stu-id="392c7-221">No</span></span> |
| <span data-ttu-id="392c7-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="392c7-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="392c7-223">Укажите имя столбца, в которое действие копирования добавляет автоматически созданный идентификатор среза. Этот идентификатор используется для очистки данных конкретного среза при повторном запуске.</span><span class="sxs-lookup"><span data-stu-id="392c7-223">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="392c7-224">Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="392c7-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="392c7-225">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="392c7-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="392c7-226">Нет</span><span class="sxs-lookup"><span data-stu-id="392c7-226">No</span></span> |
| <span data-ttu-id="392c7-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="392c7-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="392c7-228">Имя хранимой процедуры, обновляющей данные или вставляющей их в целевую таблицу.</span><span class="sxs-lookup"><span data-stu-id="392c7-228">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="392c7-229">Имя хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="392c7-229">Name of the stored procedure.</span></span> |<span data-ttu-id="392c7-230">Нет</span><span class="sxs-lookup"><span data-stu-id="392c7-230">No</span></span> |
| <span data-ttu-id="392c7-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="392c7-231">storedProcedureParameters</span></span> |<span data-ttu-id="392c7-232">Параметры для хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="392c7-232">Parameters for the stored procedure.</span></span> |<span data-ttu-id="392c7-233">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="392c7-233">Name/value pairs.</span></span> <span data-ttu-id="392c7-234">Имена и регистр параметров должны совпадать с именами и регистром параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="392c7-234">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="392c7-235">Нет</span><span class="sxs-lookup"><span data-stu-id="392c7-235">No</span></span> |
| <span data-ttu-id="392c7-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="392c7-236">sqlWriterTableType</span></span> |<span data-ttu-id="392c7-237">Укажите имя типа таблицы для использования в хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="392c7-237">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="392c7-238">Действие копирования делает перемещаемые данные доступными во временной таблице этого типа.</span><span class="sxs-lookup"><span data-stu-id="392c7-238">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="392c7-239">Код хранимой процедуры затем можно использовать для объединения копируемых и существующих данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-239">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="392c7-240">Имя типа таблицы.</span><span class="sxs-lookup"><span data-stu-id="392c7-240">A table type name.</span></span> |<span data-ttu-id="392c7-241">Нет</span><span class="sxs-lookup"><span data-stu-id="392c7-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="392c7-242">Пример SqlSink</span><span class="sxs-lookup"><span data-stu-id="392c7-242">SqlSink example</span></span>

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

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="392c7-243">Примеры JSON для копирования данных в базу данных SQL и обратно</span><span class="sxs-lookup"><span data-stu-id="392c7-243">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="392c7-244">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="392c7-244">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="392c7-245">В них показано, как копировать данные в базу данных SQL Azure и хранилище BLOB-объектов Azure и обратно.</span><span class="sxs-lookup"><span data-stu-id="392c7-245">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="392c7-246">Тем не менее данные можно копировать **непосредственно** из любых источников в любой указанный [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемник. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="392c7-246">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="392c7-247">Пример. Копирование данных из базы данных SQL Azure в BLOB-объект Azure</span><span class="sxs-lookup"><span data-stu-id="392c7-247">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="392c7-248">Образец определяет следующие сущности фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-248">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="392c7-249">Связанная служба типа [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="392c7-250">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="392c7-251">Входной [набор данных](data-factory-create-datasets.md) типа [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="392c7-252">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="392c7-253">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="392c7-254">В этом примере данные, относящиеся к одному временному ряду (за каждый час, каждый день и т. д.), каждый час копируются из таблицы в базе данных SQL Azure в большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="392c7-254">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="392c7-255">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="392c7-255">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="392c7-256">**Связанная служба базы данных SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="392c7-256">**Azure SQL Database linked service:**</span></span>

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
<span data-ttu-id="392c7-257">Список свойств, поддерживаемых этой связанной службой, приведен в разделе [Связанная служба SQL Azure](#linked-service) .</span><span class="sxs-lookup"><span data-stu-id="392c7-257">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="392c7-258">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="392c7-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="392c7-259">Список свойств, поддерживаемых этой связанной службой, приведен в разделе [Большой двоичный объект Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="392c7-259">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="392c7-260">**Входной набор данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="392c7-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="392c7-261">В примере предполагается, что таблица MyTable уже создана в SQL Azure и содержит столбец с именем timestampcolumn для данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="392c7-261">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="392c7-262">Если параметру external присвоить значение true, фабрика данных Azure воспримет этот набор данных как внешний и созданный не в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="392c7-262">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="392c7-263">Список свойств, поддерживаемых этим типом набора данных, приведен в разделе [Свойства типа «Набор данных Azure SQL»](#dataset) .</span><span class="sxs-lookup"><span data-stu-id="392c7-263">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="392c7-264">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="392c7-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="392c7-265">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="392c7-265">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="392c7-266">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="392c7-266">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="392c7-267">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="392c7-267">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="392c7-268">Список свойств, поддерживаемых этим типом набора данных, приведен в разделе [Свойства типа «Набор данных большого двоичного объекта Azure»](data-factory-azure-blob-connector.md#dataset-properties) .</span><span class="sxs-lookup"><span data-stu-id="392c7-268">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="392c7-269">**Действие копирования в конвейере с базой данных SQL в качестве источника и BLOB-объектом в качестве приемника:**</span><span class="sxs-lookup"><span data-stu-id="392c7-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="392c7-270">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="392c7-270">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="392c7-271">В определении JSON конвейера для типа **source** установлено значение **SqlSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="392c7-271">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="392c7-272">SQL-запрос, указанный для свойства **SqlReaderQuery** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="392c7-272">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="392c7-273">В этом примере для свойства SqlSource указано **sqlReaderQuery** .</span><span class="sxs-lookup"><span data-stu-id="392c7-273">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="392c7-274">Действие копирования выполняет этот запрос для источника базы данных SQL Azure для получения данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-274">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="392c7-275">Кроме того, можно создать хранимую процедуру, указав **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="392c7-275">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="392c7-276">Если не указать sqlReaderQuery или sqlReaderStoredProcedureName, то для построения запроса к базе данных SQL Azure будут использованы столбцы, определенные в разделе структуры набора данных JSON.</span><span class="sxs-lookup"><span data-stu-id="392c7-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="392c7-277">Например, `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="392c7-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="392c7-278">Если у определения набора данных нет структуры, выбираются все столбцы из таблицы.</span><span class="sxs-lookup"><span data-stu-id="392c7-278">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="392c7-279">Список свойств, поддерживаемых SqlSource и BlobSink, см. в разделах [SqlSource](#sqlsource) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-279">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="392c7-280">Пример. Копирование данных из BLOB-объекта Azure в базу данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="392c7-280">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="392c7-281">Образец определяет следующие сущности фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-281">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="392c7-282">Связанная служба типа [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="392c7-283">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="392c7-284">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="392c7-285">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="392c7-286">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="392c7-287">В этом примере данные, относящиеся к одному временному ряду (за каждый час, каждый день и т. д.), каждый час копируются из большого двоичного объекта Azure в таблицу в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="392c7-287">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="392c7-288">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="392c7-288">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="392c7-289">**Связанная служба SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="392c7-289">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="392c7-290">Список свойств, поддерживаемых этой связанной службой, приведен в разделе [Связанная служба SQL Azure](#linked-service) .</span><span class="sxs-lookup"><span data-stu-id="392c7-290">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="392c7-291">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="392c7-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="392c7-292">Список свойств, поддерживаемых этой связанной службой, приведен в разделе [Большой двоичный объект Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="392c7-292">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="392c7-293">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="392c7-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="392c7-294">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="392c7-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="392c7-295">Путь к папке с BLOB-объектом и имя файла вычисляются динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="392c7-295">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="392c7-296">В пути к папке используется год, месяц и день начала, а в имени файла — час начала.</span><span class="sxs-lookup"><span data-stu-id="392c7-296">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="392c7-297">Когда для параметра external задано значение true, служба фабрики данных считает эту таблицу внешней и созданной не в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="392c7-297">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="392c7-298">Список свойств, поддерживаемых этим типом набора данных, приведен в разделе [Свойства типа «Набор данных большого двоичного объекта Azure»](data-factory-azure-blob-connector.md#dataset-properties) .</span><span class="sxs-lookup"><span data-stu-id="392c7-298">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="392c7-299">**Выходной набор данных базы данных SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="392c7-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="392c7-300">В этом примере данные копируются в таблицу MyTable, которая создана в SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="392c7-300">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="392c7-301">Создайте таблицу в базе данных SQL Azure с тем количеством столбцов, которое должно быть в CSV-файле большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="392c7-301">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="392c7-302">Новые строки добавляются в таблицу каждый час.</span><span class="sxs-lookup"><span data-stu-id="392c7-302">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="392c7-303">Список свойств, поддерживаемых этим типом набора данных, приведен в разделе [Свойства типа «Набор данных Azure SQL»](#dataset) .</span><span class="sxs-lookup"><span data-stu-id="392c7-303">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="392c7-304">**Действие копирования в конвейере с BLOB-объектом в качестве источника и базой данных SQL в качестве приемника:**</span><span class="sxs-lookup"><span data-stu-id="392c7-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="392c7-305">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="392c7-305">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="392c7-306">В определении JSON конвейера для типа **source** установлено значение **BlobSource**, а для типа **sink** — значение **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="392c7-306">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
<span data-ttu-id="392c7-307">Список свойств, поддерживаемых SqlSink и BlobSource, см. в разделах [SqlSink](#sqlsink) и [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="392c7-307">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="392c7-308">Столбцы идентификаторов в целевой базе данных</span><span class="sxs-lookup"><span data-stu-id="392c7-308">Identity columns in the target database</span></span>
<span data-ttu-id="392c7-309">В этом разделе приведен пример копирования данных из исходной таблицы без столбца идентификаторов в целевую таблицу со столбцом идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="392c7-309">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="392c7-310">**Исходная таблица:**</span><span class="sxs-lookup"><span data-stu-id="392c7-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="392c7-311">**Целевая таблица:**</span><span class="sxs-lookup"><span data-stu-id="392c7-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="392c7-312">Обратите внимание, что в целевой таблице есть столбец идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="392c7-312">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="392c7-313">**Определение JSON исходного набора данных**</span><span class="sxs-lookup"><span data-stu-id="392c7-313">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="392c7-314">**Определение JSON целевого набора данных**</span><span class="sxs-lookup"><span data-stu-id="392c7-314">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="392c7-315">Обратите внимание, что у исходной и целевой таблиц разные схемы (в целевой есть дополнительный столбец с идентификаторами).</span><span class="sxs-lookup"><span data-stu-id="392c7-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="392c7-316">В этом случае необходимо указать свойство **structure** в определении целевого набора данных, которое не включает в себя столбец идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="392c7-316">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="392c7-317">Вызов хранимой процедуры из приемника SQL</span><span class="sxs-lookup"><span data-stu-id="392c7-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="392c7-318">Пример вызова хранимой процедуры из приемника SQL в действии копирования в конвейере приведен в статье [Invoke stored procedure from copy activity in Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md) (Вызов хранимой процедуры из действия копирования в фабрике данных Azure).</span><span class="sxs-lookup"><span data-stu-id="392c7-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="392c7-319">Сопоставление типов для базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="392c7-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="392c7-320">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="392c7-320">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="392c7-321">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="392c7-321">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="392c7-322">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="392c7-322">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="392c7-323">Когда данные перемещаются в базу данных SQL Azure и обратно, для преобразования типа SQL в тип .NET и наоборот используются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="392c7-323">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="392c7-324">Сопоставление аналогично сопоставлению типов данных SQL Server для ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="392c7-324">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="392c7-325">Тип ядра СУБД SQL Server</span><span class="sxs-lookup"><span data-stu-id="392c7-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="392c7-326">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="392c7-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="392c7-327">bigint</span><span class="sxs-lookup"><span data-stu-id="392c7-327">bigint</span></span> |<span data-ttu-id="392c7-328">Int64</span><span class="sxs-lookup"><span data-stu-id="392c7-328">Int64</span></span> |
| <span data-ttu-id="392c7-329">binary;</span><span class="sxs-lookup"><span data-stu-id="392c7-329">binary</span></span> |<span data-ttu-id="392c7-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="392c7-330">Byte[]</span></span> |
| <span data-ttu-id="392c7-331">bit</span><span class="sxs-lookup"><span data-stu-id="392c7-331">bit</span></span> |<span data-ttu-id="392c7-332">Логический</span><span class="sxs-lookup"><span data-stu-id="392c7-332">Boolean</span></span> |
| <span data-ttu-id="392c7-333">char;</span><span class="sxs-lookup"><span data-stu-id="392c7-333">char</span></span> |<span data-ttu-id="392c7-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="392c7-334">String, Char[]</span></span> |
| <span data-ttu-id="392c7-335">дата</span><span class="sxs-lookup"><span data-stu-id="392c7-335">date</span></span> |<span data-ttu-id="392c7-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="392c7-336">DateTime</span></span> |
| <span data-ttu-id="392c7-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="392c7-337">Datetime</span></span> |<span data-ttu-id="392c7-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="392c7-338">DateTime</span></span> |
| <span data-ttu-id="392c7-339">datetime2;</span><span class="sxs-lookup"><span data-stu-id="392c7-339">datetime2</span></span> |<span data-ttu-id="392c7-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="392c7-340">DateTime</span></span> |
| <span data-ttu-id="392c7-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="392c7-341">Datetimeoffset</span></span> |<span data-ttu-id="392c7-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="392c7-342">DateTimeOffset</span></span> |
| <span data-ttu-id="392c7-343">Decimal</span><span class="sxs-lookup"><span data-stu-id="392c7-343">Decimal</span></span> |<span data-ttu-id="392c7-344">Decimal</span><span class="sxs-lookup"><span data-stu-id="392c7-344">Decimal</span></span> |
| <span data-ttu-id="392c7-345">Атрибут FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="392c7-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="392c7-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="392c7-346">Byte[]</span></span> |
| <span data-ttu-id="392c7-347">Float</span><span class="sxs-lookup"><span data-stu-id="392c7-347">Float</span></span> |<span data-ttu-id="392c7-348">Double</span><span class="sxs-lookup"><span data-stu-id="392c7-348">Double</span></span> |
| <span data-ttu-id="392c7-349">изображение</span><span class="sxs-lookup"><span data-stu-id="392c7-349">image</span></span> |<span data-ttu-id="392c7-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="392c7-350">Byte[]</span></span> |
| <span data-ttu-id="392c7-351">int</span><span class="sxs-lookup"><span data-stu-id="392c7-351">int</span></span> |<span data-ttu-id="392c7-352">Int32</span><span class="sxs-lookup"><span data-stu-id="392c7-352">Int32</span></span> |
| <span data-ttu-id="392c7-353">money;</span><span class="sxs-lookup"><span data-stu-id="392c7-353">money</span></span> |<span data-ttu-id="392c7-354">Decimal</span><span class="sxs-lookup"><span data-stu-id="392c7-354">Decimal</span></span> |
| <span data-ttu-id="392c7-355">nchar;</span><span class="sxs-lookup"><span data-stu-id="392c7-355">nchar</span></span> |<span data-ttu-id="392c7-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="392c7-356">String, Char[]</span></span> |
| <span data-ttu-id="392c7-357">ntext</span><span class="sxs-lookup"><span data-stu-id="392c7-357">ntext</span></span> |<span data-ttu-id="392c7-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="392c7-358">String, Char[]</span></span> |
| <span data-ttu-id="392c7-359">numeric</span><span class="sxs-lookup"><span data-stu-id="392c7-359">numeric</span></span> |<span data-ttu-id="392c7-360">Decimal</span><span class="sxs-lookup"><span data-stu-id="392c7-360">Decimal</span></span> |
| <span data-ttu-id="392c7-361">nvarchar;</span><span class="sxs-lookup"><span data-stu-id="392c7-361">nvarchar</span></span> |<span data-ttu-id="392c7-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="392c7-362">String, Char[]</span></span> |
| <span data-ttu-id="392c7-363">real;</span><span class="sxs-lookup"><span data-stu-id="392c7-363">real</span></span> |<span data-ttu-id="392c7-364">Single</span><span class="sxs-lookup"><span data-stu-id="392c7-364">Single</span></span> |
| <span data-ttu-id="392c7-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="392c7-365">rowversion</span></span> |<span data-ttu-id="392c7-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="392c7-366">Byte[]</span></span> |
| <span data-ttu-id="392c7-367">smalldatetime;</span><span class="sxs-lookup"><span data-stu-id="392c7-367">smalldatetime</span></span> |<span data-ttu-id="392c7-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="392c7-368">DateTime</span></span> |
| <span data-ttu-id="392c7-369">smallint;</span><span class="sxs-lookup"><span data-stu-id="392c7-369">smallint</span></span> |<span data-ttu-id="392c7-370">Int16</span><span class="sxs-lookup"><span data-stu-id="392c7-370">Int16</span></span> |
| <span data-ttu-id="392c7-371">smallmoney;</span><span class="sxs-lookup"><span data-stu-id="392c7-371">smallmoney</span></span> |<span data-ttu-id="392c7-372">Decimal</span><span class="sxs-lookup"><span data-stu-id="392c7-372">Decimal</span></span> |
| <span data-ttu-id="392c7-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="392c7-373">sql_variant</span></span> |<span data-ttu-id="392c7-374">Object *</span><span class="sxs-lookup"><span data-stu-id="392c7-374">Object *</span></span> |
| <span data-ttu-id="392c7-375">text</span><span class="sxs-lookup"><span data-stu-id="392c7-375">text</span></span> |<span data-ttu-id="392c7-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="392c7-376">String, Char[]</span></span> |
| <span data-ttu-id="392c7-377">time</span><span class="sxs-lookup"><span data-stu-id="392c7-377">time</span></span> |<span data-ttu-id="392c7-378">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="392c7-378">TimeSpan</span></span> |
| <span data-ttu-id="392c7-379">Timestamp</span><span class="sxs-lookup"><span data-stu-id="392c7-379">timestamp</span></span> |<span data-ttu-id="392c7-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="392c7-380">Byte[]</span></span> |
| <span data-ttu-id="392c7-381">tinyint;</span><span class="sxs-lookup"><span data-stu-id="392c7-381">tinyint</span></span> |<span data-ttu-id="392c7-382">Byte</span><span class="sxs-lookup"><span data-stu-id="392c7-382">Byte</span></span> |
| <span data-ttu-id="392c7-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="392c7-383">uniqueidentifier</span></span> |<span data-ttu-id="392c7-384">Guid</span><span class="sxs-lookup"><span data-stu-id="392c7-384">Guid</span></span> |
| <span data-ttu-id="392c7-385">varbinary;</span><span class="sxs-lookup"><span data-stu-id="392c7-385">varbinary</span></span> |<span data-ttu-id="392c7-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="392c7-386">Byte[]</span></span> |
| <span data-ttu-id="392c7-387">varchar.</span><span class="sxs-lookup"><span data-stu-id="392c7-387">varchar</span></span> |<span data-ttu-id="392c7-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="392c7-388">String, Char[]</span></span> |
| <span data-ttu-id="392c7-389">xml</span><span class="sxs-lookup"><span data-stu-id="392c7-389">xml</span></span> |<span data-ttu-id="392c7-390">xml</span><span class="sxs-lookup"><span data-stu-id="392c7-390">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="392c7-391">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="392c7-391">Map source to sink columns</span></span>
<span data-ttu-id="392c7-392">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="392c7-392">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="392c7-393">Повторяющаяся операция копирования</span><span class="sxs-lookup"><span data-stu-id="392c7-393">Repeatable copy</span></span>
<span data-ttu-id="392c7-394">При копировании данных в базу данных SQL Server действие копирования по умолчанию добавляет данные в таблицу приемника.</span><span class="sxs-lookup"><span data-stu-id="392c7-394">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="392c7-395">Чтобы вместо этого выполнить операцию UPSERT, изучите раздел [Повторяемая запись в SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink).</span><span class="sxs-lookup"><span data-stu-id="392c7-395">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="392c7-396">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="392c7-396">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="392c7-397">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="392c7-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="392c7-398">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="392c7-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="392c7-399">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="392c7-399">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="392c7-400">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="392c7-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="392c7-401">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="392c7-401">Performance and Tuning</span></span>
<span data-ttu-id="392c7-402">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="392c7-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
