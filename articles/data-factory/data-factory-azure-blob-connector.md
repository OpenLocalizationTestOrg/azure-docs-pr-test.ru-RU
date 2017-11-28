---
title: "aaaCopy данных из хранилища больших двоичных объектов | Документы Microsoft"
description: "Узнайте, как toocopy данные большого двоичного объекта в фабрике данных Azure. Используйте приведенный образец: как toocopy tooand данных из хранилища больших двоичных объектов и базы данных SQL Azure."
keywords: "данные BLOB-объектов, копирование BLOB-объекта Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="cc4db-105">Tooor копирования данных из хранилища больших двоичных объектов Azure, с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="cc4db-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="cc4db-106">В этой статье объясняется, как toouse hello действие копирования в tooand данных toocopy фабрики данных Azure из хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="cc4db-107">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="cc4db-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="cc4db-108">Overview</span></span>
<span data-ttu-id="cc4db-109">Можно скопировать данные из любого поддерживаемого источника данных хранения tooAzure хранилища BLOB-объектов или из хранилища больших двоичных объектов поддерживается tooany приемник данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="cc4db-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="cc4db-110">Hello Следующая таблица содержит перечень хранилищ данных, поддерживаемые в качестве источников или приемники действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="cc4db-111">Например, вы можете переместить данные **из** базы данных SQL Server или SQL Azure **в** хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="cc4db-112">Вы также можете копировать данные **из** хранилища BLOB-объектов Azure **в** хранилище данных SQL Azure или в коллекцию Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cc4db-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="cc4db-113">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="cc4db-113">Supported scenarios</span></span>
<span data-ttu-id="cc4db-114">Можно скопировать данные **из хранилища больших двоичных объектов** toohello следующие хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="cc4db-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="cc4db-115">Можно скопировать данные из hello, следуя хранилищ данных **tooAzure хранилища больших двоичных объектов**:</span><span class="sxs-lookup"><span data-stu-id="cc4db-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="cc4db-116">Действие копирования поддерживает копирование данных из / tooboth общего назначения хранилища Azure, учетные записи и горячей/охлаждение хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="cc4db-117">Действие Hello поддерживает **чтение из блока, добавить или страничные большие двоичные объекты**, но поддерживает **записи tooonly блочных больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="cc4db-118">Хранилище Azure класса Premium нельзя использовать в качестве приемника, так как оно поддерживается страничными BLOB-объектами.</span><span class="sxs-lookup"><span data-stu-id="cc4db-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="cc4db-119">Действие копирования не удаляет данные из источника hello, скопировав hello данных равен успешно toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="cc4db-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="cc4db-120">При необходимости после успешной копии toodelete исходных данных, создать [пользовательское действие](data-factory-use-custom-activities.md) toodelete hello данных и используйте действие hello в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="cc4db-121">Пример см. в разделе hello [пример удаления BLOB-объектов или папки на GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="cc4db-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="cc4db-122">Начало работы</span><span class="sxs-lookup"><span data-stu-id="cc4db-122">Get started</span></span>
<span data-ttu-id="cc4db-123">Можно создать конвейер с действием копирования, которое перемещает данные из хранилища BLOB-объектов Azure или в него с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="cc4db-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="cc4db-124">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="cc4db-125">Данная статья содержит [Пошаговое руководство](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) для создания конвейера toocopy данных из хранилища больших двоичных объектов расположение tooanother расположение хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="cc4db-126">Учебник по созданию toocopy конвейера данных из хранилища больших двоичных объектов tooAzure базы данных SQL см. в разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="cc4db-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="cc4db-127">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cc4db-128">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="cc4db-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="cc4db-129">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="cc4db-130">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-130">Create a **data factory**.</span></span> <span data-ttu-id="cc4db-131">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="cc4db-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="cc4db-132">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="cc4db-133">Например при копировании данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure, создается два связанных служб toolink вашей учетной записи хранилища Azure и фабрики данных tooyour базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="cc4db-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="cc4db-134">Свойства связанной службы, определенные tooAzure хранилища больших двоичных объектов, в разделе [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="cc4db-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="cc4db-135">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="cc4db-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="cc4db-136">В примере hello, упомянутые в последнем шаге hello создать контейнер больших двоичных объектов dataset toospecify hello и папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="cc4db-137">И создайте другую таблицу SQL hello toospecify набора данных в базе данных Azure SQL hello, содержащий hello данные, скопированные из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="cc4db-138">Свойства набора данных, определенных tooAzure хранилища больших двоичных объектов, в разделе [свойства набора данных](#dataset-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="cc4db-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="cc4db-139">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="cc4db-140">В примере hello приведенные выше используются BlobSource в исходной и SqlSink в приемник для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="cc4db-141">Аналогично Если копируются из базы данных SQL Azure tooAzure хранилища больших двоичных объектов, использовать SqlSource и BlobSink в действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="cc4db-142">Свойства действия копирования, определенные tooAzure хранилища больших двоичных объектов, в разделе [скопировать свойства действия](#copy-activity-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="cc4db-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="cc4db-143">Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="cc4db-144">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="cc4db-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="cc4db-145">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="cc4db-146">Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища больших двоичных объектов Azure см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-blob-storage  ) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="cc4db-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="cc4db-147">Hello в следующих разделах приведены сведения о JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cc4db-148">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="cc4db-148">Linked service properties</span></span>
<span data-ttu-id="cc4db-149">Существует два типа связанных служб можно использовать toolink фабрикой данных Azure tooan хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="cc4db-150">**AzureStorage** и **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="cc4db-151">Hello связанной службой хранилища Azure обеспечивает для фабрики данных hello с toohello глобальный доступ к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="cc4db-152">В то время как связанные hello SAS хранилища Azure (подпись общего доступа) службы обеспечивает для фабрики данных hello с toohello ограничен или ограниченным временем доступа хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="cc4db-153">Других различий между этими связанными службами нет.</span><span class="sxs-lookup"><span data-stu-id="cc4db-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="cc4db-154">Выберите службу hello связаны, которая соответствует вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="cc4db-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="cc4db-155">Hello следующие подразделы содержат дополнительные сведения в этих двух связанных служб.</span><span class="sxs-lookup"><span data-stu-id="cc4db-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="cc4db-156">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="cc4db-156">Dataset properties</span></span>
<span data-ttu-id="cc4db-157">toospecify dataset toorepresent входных или выходных данных в хранилище BLOB-объектов Azure, задайте свойство типа hello hello набора данных для: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="cc4db-158">Набор hello **linkedServiceName** свойство toohello имя набора данных hello hello хранилища Azure или SAS хранилища Azure связанной службы.</span><span class="sxs-lookup"><span data-stu-id="cc4db-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="cc4db-159">свойства типа Hello hello набора данных укажите hello **контейнер больших двоичных объектов** и hello **папки** в хранилище больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="cc4db-160">Полный список разделов JSON и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="cc4db-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cc4db-161">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="cc4db-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="cc4db-162">Фабрика данных поддерживает следующие CLS-совместимым .NET на основе типа значения для предоставления информации о типах в «структура» для источников данных схемы на чтение как BLOB-объектов Azure hello: Int16, Int32, Int64, единый, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="cc4db-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="cc4db-163">Фабрика данных автоматически выполняет преобразования типов при перемещении данных из источника данных в хранилище tooa приемник данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="cc4db-164">Hello **typeProperties** разделе отличается для каждого типа набора данных и содержатся сведения о местоположении hello, форматирования и т.д., hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="cc4db-165">Hello typeProperties статьи для набора данных типа **AzureBlob** набор данных имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="cc4db-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="cc4db-166">Свойство</span><span class="sxs-lookup"><span data-stu-id="cc4db-166">Property</span></span> | <span data-ttu-id="cc4db-167">Описание</span><span class="sxs-lookup"><span data-stu-id="cc4db-167">Description</span></span> | <span data-ttu-id="cc4db-168">Обязательно</span><span class="sxs-lookup"><span data-stu-id="cc4db-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc4db-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="cc4db-169">folderPath</span></span> |<span data-ttu-id="cc4db-170">Контейнер toohello путь к папке, в hello хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="cc4db-171">Пример: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="cc4db-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="cc4db-172">Да</span><span class="sxs-lookup"><span data-stu-id="cc4db-172">Yes</span></span> |
| <span data-ttu-id="cc4db-173">fileName</span><span class="sxs-lookup"><span data-stu-id="cc4db-173">fileName</span></span> |<span data-ttu-id="cc4db-174">Имя большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-174">Name of hello blob.</span></span> <span data-ttu-id="cc4db-175">Свойство fileName является необязательным и в нем учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="cc4db-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="cc4db-176">При указании имени файла, hello деятельности (включая копирования) работает на hello определенным BLOB-объектом.</span><span class="sxs-lookup"><span data-stu-id="cc4db-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="cc4db-177">Если не указано имя файла, копирования включает все большие двоичные объекты в folderPath hello для входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="cc4db-178">Когда **fileName** не указано для выходной набор данных и **preserveHierarchy** не указан в приемник действие hello имя hello созданный файл будет в следующем формате hello: данные.<Guid>. txt (например:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="cc4db-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="cc4db-179">Нет</span><span class="sxs-lookup"><span data-stu-id="cc4db-179">No</span></span> |
| <span data-ttu-id="cc4db-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="cc4db-180">partitionedBy</span></span> |<span data-ttu-id="cc4db-181">Необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="cc4db-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="cc4db-182">Можно использовать его toospecify динамического folderPath и filename для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="cc4db-183">Например, путь к папке (значение folderPath) каждый час может быть другим.</span><span class="sxs-lookup"><span data-stu-id="cc4db-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="cc4db-184">В разделе hello [с помощью свойства раздела partitionedBy](#using-partitionedBy-property) подробные сведения и примеры.</span><span class="sxs-lookup"><span data-stu-id="cc4db-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="cc4db-185">Нет</span><span class="sxs-lookup"><span data-stu-id="cc4db-185">No</span></span> |
| <span data-ttu-id="cc4db-186">свойства</span><span class="sxs-lookup"><span data-stu-id="cc4db-186">format</span></span> | <span data-ttu-id="cc4db-187">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="cc4db-188">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="cc4db-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="cc4db-189">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="cc4db-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="cc4db-190">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="cc4db-191">Нет</span><span class="sxs-lookup"><span data-stu-id="cc4db-191">No</span></span> |
| <span data-ttu-id="cc4db-192">compression</span><span class="sxs-lookup"><span data-stu-id="cc4db-192">compression</span></span> | <span data-ttu-id="cc4db-193">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="cc4db-194">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="cc4db-195">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="cc4db-196">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="cc4db-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="cc4db-197">Нет</span><span class="sxs-lookup"><span data-stu-id="cc4db-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="cc4db-198">Использование свойства partitionedBy</span><span class="sxs-lookup"><span data-stu-id="cc4db-198">Using partitionedBy property</span></span>
<span data-ttu-id="cc4db-199">Как упоминалось в предыдущем разделе hello, можно указать динамического folderPath и filename для временного ряда данных с hello **partitionedBy** свойства [функции фабрики данных, а системные переменные hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="cc4db-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="cc4db-200">Дополнительные сведения о наборах данных временных рядов, планировании и срезах см. в статьях [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md) и [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="cc4db-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="cc4db-201">Пример 1</span><span class="sxs-lookup"><span data-stu-id="cc4db-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="cc4db-202">В этом примере {Slice} заменяется hello значение системной переменной фабрики данных SliceStart в формате hello (ГГГГММДДЧЧ) указан.</span><span class="sxs-lookup"><span data-stu-id="cc4db-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="cc4db-203">Hello SliceStart ссылается toostart время hello среза.</span><span class="sxs-lookup"><span data-stu-id="cc4db-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="cc4db-204">Hello folderPath отличается для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="cc4db-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="cc4db-205">Например: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="cc4db-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="cc4db-206">Пример 2</span><span class="sxs-lookup"><span data-stu-id="cc4db-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="cc4db-207">В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые в свойствах folderPath и fileName.</span><span class="sxs-lookup"><span data-stu-id="cc4db-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="cc4db-208">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="cc4db-208">Copy activity properties</span></span>
<span data-ttu-id="cc4db-209">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="cc4db-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cc4db-210">Свойства, например имя, описание, входные и выходные таблицы, политики и т. д., доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="cc4db-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="cc4db-211">В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="cc4db-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="cc4db-212">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="cc4db-213">При перемещении данных из хранилища больших двоичных объектов Azure установке hello исходного типа в действие копирования hello слишком**BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="cc4db-214">Аналогичным образом, при перемещении данных tooan хранилища больших двоичных объектов, установке тип приемника hello в действии копирования hello слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="cc4db-215">Этот раздел содержит список свойств, поддерживаемых типами BlobSource и BlobSink.</span><span class="sxs-lookup"><span data-stu-id="cc4db-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="cc4db-216">**BlobSource** поддерживает следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="cc4db-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="cc4db-217">Свойство</span><span class="sxs-lookup"><span data-stu-id="cc4db-217">Property</span></span> | <span data-ttu-id="cc4db-218">Описание</span><span class="sxs-lookup"><span data-stu-id="cc4db-218">Description</span></span> | <span data-ttu-id="cc4db-219">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="cc4db-219">Allowed values</span></span> | <span data-ttu-id="cc4db-220">Обязательно</span><span class="sxs-lookup"><span data-stu-id="cc4db-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cc4db-221">recursive</span><span class="sxs-lookup"><span data-stu-id="cc4db-221">recursive</span></span> |<span data-ttu-id="cc4db-222">Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="cc4db-223">True (значение по умолчанию), False</span><span class="sxs-lookup"><span data-stu-id="cc4db-223">True (default value), False</span></span> |<span data-ttu-id="cc4db-224">Нет</span><span class="sxs-lookup"><span data-stu-id="cc4db-224">No</span></span> |

<span data-ttu-id="cc4db-225">**BlobSink** поддерживает следующие свойства hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="cc4db-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="cc4db-226">Свойство</span><span class="sxs-lookup"><span data-stu-id="cc4db-226">Property</span></span> | <span data-ttu-id="cc4db-227">Описание</span><span class="sxs-lookup"><span data-stu-id="cc4db-227">Description</span></span> | <span data-ttu-id="cc4db-228">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="cc4db-228">Allowed values</span></span> | <span data-ttu-id="cc4db-229">Обязательно</span><span class="sxs-lookup"><span data-stu-id="cc4db-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cc4db-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="cc4db-230">copyBehavior</span></span> |<span data-ttu-id="cc4db-231">Определяет поведение копирования hello, когда источник hello BlobSource или файловой системы.</span><span class="sxs-lookup"><span data-stu-id="cc4db-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="cc4db-232"><b>PreserveHierarchy</b>: сохраняет hello иерархию файлов в целевой папке hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="cc4db-233">Hello относительный путь к исходной папке toosource файла представляет идентичные toohello относительный путь папки tootarget целевого файла.</span><span class="sxs-lookup"><span data-stu-id="cc4db-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="cc4db-234"><b>FlattenHierarchy</b>: все файлы из исходной папки hello в hello сначала уровень целевую папку.</span><span class="sxs-lookup"><span data-stu-id="cc4db-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="cc4db-235">файлы целевой Hello иметь автоматически созданное имя.</span><span class="sxs-lookup"><span data-stu-id="cc4db-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="cc4db-236"><b>MergeFiles</b>: объединяет все файлы из папки tooone hello исходного файла.</span><span class="sxs-lookup"><span data-stu-id="cc4db-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="cc4db-237">Если указано имя файла или большого двоичного объекта hello hello объединенный файл будет hello указанным именем. в противном случае будет автоматически формируемого имени файла.</span><span class="sxs-lookup"><span data-stu-id="cc4db-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="cc4db-238">Нет</span><span class="sxs-lookup"><span data-stu-id="cc4db-238">No</span></span> |

<span data-ttu-id="cc4db-239">**BlobSource** также поддерживает эти два свойства для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="cc4db-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="cc4db-240">**treatEmptyAsNull**: Указывает, является ли tootreat null или пустую строку как значение null.</span><span class="sxs-lookup"><span data-stu-id="cc4db-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="cc4db-241">**skipHeaderLineCount** указывает, сколько строк необходимо пропустить.</span><span class="sxs-lookup"><span data-stu-id="cc4db-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="cc4db-242">Применяется, только когда для входного набора данных используется TextFormat.</span><span class="sxs-lookup"><span data-stu-id="cc4db-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="cc4db-243">Аналогичным образом **BlobSink** поддерживает hello следующие свойства для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="cc4db-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="cc4db-244">**blobWriterAddHeader**: Указывает, является ли заголовок определений столбцов при записи tooan tooadd выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="cc4db-245">Наборы данных теперь поддержки hello следующие свойства, которые реализуют hello же функциональные возможности: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="cc4db-246">Hello следующей таблице приведены инструкции по использованию hello новые свойства набора данных, вместо этих свойств большого двоичного объекта источника и приемника.</span><span class="sxs-lookup"><span data-stu-id="cc4db-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="cc4db-247">Свойство "Действие копирования"</span><span class="sxs-lookup"><span data-stu-id="cc4db-247">Copy Activity property</span></span> | <span data-ttu-id="cc4db-248">Свойство "Набор данных"</span><span class="sxs-lookup"><span data-stu-id="cc4db-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="cc4db-249">skipHeaderLineCount в BlobSource</span><span class="sxs-lookup"><span data-stu-id="cc4db-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="cc4db-250">skipLineCount и firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="cc4db-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="cc4db-251">Строки пропускаются сначала и читается hello первую строку как заголовок.</span><span class="sxs-lookup"><span data-stu-id="cc4db-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="cc4db-252">treatEmptyAsNull в BlobSource</span><span class="sxs-lookup"><span data-stu-id="cc4db-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="cc4db-253">treatEmptyAsNull во входном наборе данных</span><span class="sxs-lookup"><span data-stu-id="cc4db-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="cc4db-254">blobWriterAddHeader в BlobSink</span><span class="sxs-lookup"><span data-stu-id="cc4db-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="cc4db-255">firstRowAsHeader в выходном наборе данных</span><span class="sxs-lookup"><span data-stu-id="cc4db-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="cc4db-256">Подробную информацию об этих свойствах см. в разделе [Определение TextFormat](data-factory-supported-file-and-compression-formats.md#text-format).</span><span class="sxs-lookup"><span data-stu-id="cc4db-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="cc4db-257">Примеры recursive и copyBehavior</span><span class="sxs-lookup"><span data-stu-id="cc4db-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="cc4db-258">Этот раздел описывает поведение функции hello операции копирования для различных сочетаний значений рекурсивные и copyBehavior hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="cc4db-259">recursive</span><span class="sxs-lookup"><span data-stu-id="cc4db-259">recursive</span></span> | <span data-ttu-id="cc4db-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="cc4db-260">copyBehavior</span></span> | <span data-ttu-id="cc4db-261">Результаты выполнения операции</span><span class="sxs-lookup"><span data-stu-id="cc4db-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc4db-262">Да</span><span class="sxs-lookup"><span data-stu-id="cc4db-262">true</span></span> |<span data-ttu-id="cc4db-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="cc4db-263">preserveHierarchy</span></span> |<span data-ttu-id="cc4db-264">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="cc4db-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc4db-265">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-265">Folder1</span></span><br/><span data-ttu-id="cc4db-266">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="cc4db-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc4db-267">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="cc4db-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc4db-268">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc4db-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="cc4db-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc4db-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="cc4db-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc4db-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="cc4db-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc4db-272">Hello целевую папку Folder1 создается с таким же структуру как исходной hello hello</span><span class="sxs-lookup"><span data-stu-id="cc4db-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="cc4db-273">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-273">Folder1</span></span><br/><span data-ttu-id="cc4db-274">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="cc4db-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc4db-275">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="cc4db-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc4db-276">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc4db-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="cc4db-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc4db-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="cc4db-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc4db-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="cc4db-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="cc4db-280">Да</span><span class="sxs-lookup"><span data-stu-id="cc4db-280">true</span></span> |<span data-ttu-id="cc4db-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="cc4db-281">flattenHierarchy</span></span> |<span data-ttu-id="cc4db-282">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="cc4db-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc4db-283">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-283">Folder1</span></span><br/><span data-ttu-id="cc4db-284">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="cc4db-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc4db-285">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="cc4db-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc4db-286">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc4db-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="cc4db-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc4db-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="cc4db-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc4db-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="cc4db-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc4db-290">целевой Hello папка1 создана следующая структура hello:</span><span class="sxs-lookup"><span data-stu-id="cc4db-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc4db-291">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-291">Folder1</span></span><br/><span data-ttu-id="cc4db-292">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="cc4db-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="cc4db-293">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="cc4db-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="cc4db-294">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл3"</span><span class="sxs-lookup"><span data-stu-id="cc4db-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="cc4db-295">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл4"</span><span class="sxs-lookup"><span data-stu-id="cc4db-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="cc4db-296">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл5"</span><span class="sxs-lookup"><span data-stu-id="cc4db-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="cc4db-297">Да</span><span class="sxs-lookup"><span data-stu-id="cc4db-297">true</span></span> |<span data-ttu-id="cc4db-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="cc4db-298">mergeFiles</span></span> |<span data-ttu-id="cc4db-299">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="cc4db-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc4db-300">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-300">Folder1</span></span><br/><span data-ttu-id="cc4db-301">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="cc4db-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc4db-302">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="cc4db-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc4db-303">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc4db-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="cc4db-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc4db-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="cc4db-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc4db-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="cc4db-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc4db-307">целевой Hello папка1 создана следующая структура hello:</span><span class="sxs-lookup"><span data-stu-id="cc4db-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc4db-308">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-308">Folder1</span></span><br/><span data-ttu-id="cc4db-309">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1", "Файл2", "Файл3", "Файл4" и "Файл5" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="cc4db-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="cc4db-310">нет</span><span class="sxs-lookup"><span data-stu-id="cc4db-310">false</span></span> |<span data-ttu-id="cc4db-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="cc4db-311">preserveHierarchy</span></span> |<span data-ttu-id="cc4db-312">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="cc4db-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc4db-313">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-313">Folder1</span></span><br/><span data-ttu-id="cc4db-314">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="cc4db-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc4db-315">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="cc4db-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc4db-316">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc4db-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="cc4db-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc4db-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="cc4db-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc4db-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="cc4db-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc4db-320">Hello целевую папку Folder1 создается с следующая структура hello</span><span class="sxs-lookup"><span data-stu-id="cc4db-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="cc4db-321">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-321">Folder1</span></span><br/><span data-ttu-id="cc4db-322">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="cc4db-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc4db-323">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="cc4db-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="cc4db-324">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="cc4db-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="cc4db-325">нет</span><span class="sxs-lookup"><span data-stu-id="cc4db-325">false</span></span> |<span data-ttu-id="cc4db-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="cc4db-326">flattenHierarchy</span></span> |<span data-ttu-id="cc4db-327">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="cc4db-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="cc4db-328">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-328">Folder1</span></span><br/><span data-ttu-id="cc4db-329">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="cc4db-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc4db-330">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="cc4db-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc4db-331">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc4db-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="cc4db-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc4db-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="cc4db-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc4db-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="cc4db-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc4db-335">Hello целевую папку Folder1 создается с следующая структура hello</span><span class="sxs-lookup"><span data-stu-id="cc4db-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="cc4db-336">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-336">Folder1</span></span><br/><span data-ttu-id="cc4db-337">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="cc4db-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="cc4db-338">&nbsp;&nbsp;&nbsp;&nbsp;Автоматически созданное имя для "Файл2"</span><span class="sxs-lookup"><span data-stu-id="cc4db-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="cc4db-339">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="cc4db-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="cc4db-340">нет</span><span class="sxs-lookup"><span data-stu-id="cc4db-340">false</span></span> |<span data-ttu-id="cc4db-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="cc4db-341">mergeFiles</span></span> |<span data-ttu-id="cc4db-342">Для исходной папки Folder1 с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="cc4db-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="cc4db-343">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-343">Folder1</span></span><br/><span data-ttu-id="cc4db-344">&nbsp;&nbsp;&nbsp;&nbsp;Файл1</span><span class="sxs-lookup"><span data-stu-id="cc4db-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc4db-345">&nbsp;&nbsp;&nbsp;&nbsp;Файл2</span><span class="sxs-lookup"><span data-stu-id="cc4db-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc4db-346">&nbsp;&nbsp;&nbsp;&nbsp;Вложенная_папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc4db-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл3</span><span class="sxs-lookup"><span data-stu-id="cc4db-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc4db-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл4</span><span class="sxs-lookup"><span data-stu-id="cc4db-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc4db-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Файл5</span><span class="sxs-lookup"><span data-stu-id="cc4db-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc4db-350">Hello целевую папку Folder1 создается с следующая структура hello</span><span class="sxs-lookup"><span data-stu-id="cc4db-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="cc4db-351">Папка1</span><span class="sxs-lookup"><span data-stu-id="cc4db-351">Folder1</span></span><br/><span data-ttu-id="cc4db-352">&nbsp;&nbsp;&nbsp;&nbsp;Содержимое файлов "Файл1" и "Файл2" объединяется в один файл с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="cc4db-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="cc4db-353">Автоматически созданное имя для "Файл1"</span><span class="sxs-lookup"><span data-stu-id="cc4db-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="cc4db-354">Папка "Вложенная_папка1" с файлами "Файл3", "Файл4" и "Файл5" не будет включена в эту папку.</span><span class="sxs-lookup"><span data-stu-id="cc4db-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="cc4db-355">Пошаговое руководство: Использование мастера копирования toocopy данных из хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cc4db-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="cc4db-356">Давайте взглянем на как tooquickly копирование данных из Azure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="cc4db-357">В этом пошаговом руководстве используются исходное и целевое хранилища данных типа хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="cc4db-358">Hello конвейера в этом пошаговом руководстве копирует данные из tooanother папки в hello же контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="cc4db-359">В этом пошаговом руководстве будет намеренно простые tooshow параметры или свойства при использовании хранилища BLOB-объектов в качестве источника или приемника.</span><span class="sxs-lookup"><span data-stu-id="cc4db-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="cc4db-360">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cc4db-360">Prerequisites</span></span>
1. <span data-ttu-id="cc4db-361">Создайте **учетную запись хранения Azure** общего назначения, если у вас ее нет.</span><span class="sxs-lookup"><span data-stu-id="cc4db-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="cc4db-362">Использовать хранилище больших двоичных объектов hello как **источника** и **назначения** хранилище данных в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="cc4db-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="cc4db-363">При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи для действия toocreate один.</span><span class="sxs-lookup"><span data-stu-id="cc4db-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="cc4db-364">Создание контейнера BLOB-объекта с именем **adfblobconnector** в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="cc4db-365">Создайте папку с именем **ввода** в hello **adfblobconnector** контейнера.</span><span class="sxs-lookup"><span data-stu-id="cc4db-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="cc4db-366">Создайте файл с именем **emp.txt** с hello после содержимого и передать его toohello **ввода** папки с помощью средств, таких как [обозреватель хранилищ Azure](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="cc4db-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="cc4db-367">Создание фабрики данных hello</span><span class="sxs-lookup"><span data-stu-id="cc4db-367">Create hello data factory</span></span>
1. <span data-ttu-id="cc4db-368">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc4db-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cc4db-369">Нажмите кнопку **+ создать** в левом верхнем углу hello, выберите **аналитики + аналитика**и нажмите кнопку **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="cc4db-370">В hello **новую фабрику данных** колонки:</span><span class="sxs-lookup"><span data-stu-id="cc4db-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="cc4db-371">Введите **ADFBlobConnectorDF** для hello **имя**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="cc4db-372">Имя фабрики данных Azure hello Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="cc4db-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="cc4db-373">Если ошибка hello: `*Data factory name “ADFBlobConnectorDF” is not available`, измените имя hello hello фабрики данных (например, yournameADFBlobConnectorDF) и повторите попытку создания.</span><span class="sxs-lookup"><span data-stu-id="cc4db-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="cc4db-374">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="cc4db-375">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="cc4db-376">Группа ресурсов выберите **использовать существующие** tooselect для существующих ресурсов группы (или) выберите **создать новый** tooenter имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="cc4db-377">Выберите **расположение** для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="cc4db-378">Выберите **toodashboard ПИН-код** флажок hello нижней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="cc4db-379">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-379">Click **Create**.</span></span>
3. <span data-ttu-id="cc4db-380">После завершения создания hello, вы видите hello **фабрики данных** колонки, как показано в hello после изображения: ![Домашняя страница фабрики данных](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="cc4db-381">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="cc4db-381">Copy Wizard</span></span>
1. <span data-ttu-id="cc4db-382">На домашней странице hello фабрики данных, нажмите кнопку hello **копирование данных [Предварительная версия]** плитки toolaunch **мастер копирования данных** на отдельной вкладке.</span><span class="sxs-lookup"><span data-stu-id="cc4db-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="cc4db-383">При появлении этого веб-браузер hello застряла в «Авторизации...», отключить или снимите **блокировать сторонние файлы cookie и данным сайта** параметра (или) Оставьте включенным и создание исключения для **login.microsoftonline.com**, затем попытайтесь еще раз запустить мастер hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="cc4db-384">В hello **свойства** страницы:</span><span class="sxs-lookup"><span data-stu-id="cc4db-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="cc4db-385">Введите **CopyPipeline** в качестве **имени задачи**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="cc4db-386">Имя задачи Hello — имя hello hello конвейера в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="cc4db-387">Введите **описание** для задачи «hello» (необязательно).</span><span class="sxs-lookup"><span data-stu-id="cc4db-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="cc4db-388">Для **последовательность задач или расписании задач**, сохранить hello **регулярно выполнять по расписанию** параметр.</span><span class="sxs-lookup"><span data-stu-id="cc4db-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="cc4db-389">Toorun многократно выполнять эту задачу только один раз, а не по расписанию, установите **выполнить один раз**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="cc4db-390">Если выбрать переключатель **Run once now** (Выполнить один раз), будет создан [одноразовый конвейер](data-factory-create-pipelines.md#onetime-pipeline).</span><span class="sxs-lookup"><span data-stu-id="cc4db-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="cc4db-391">Сохраните параметры hello для **шаблон периодически**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="cc4db-392">Эта задача выполняется ежедневно чтобы между hello, начала и окончания раз можно указать в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="cc4db-393">Изменение hello **Дата-время начала** слишком**04/21/2017 г.**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="cc4db-394">Изменение hello **время Дата окончания** слишком**04/25/2017 г.**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="cc4db-395">Вы можете tootype hello даты вместо перехода через hello календаря.</span><span class="sxs-lookup"><span data-stu-id="cc4db-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="cc4db-396">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-396">Click **Next**.</span></span>
      <span data-ttu-id="cc4db-397">![Средство копирования — страница "Свойства"](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="cc4db-398">На hello **хранилище данных источника** щелкните **хранилища больших двоичных объектов** плитки.</span><span class="sxs-lookup"><span data-stu-id="cc4db-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="cc4db-399">Использовать хранилище страницы toospecify hello источника данных для копирования задачу hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="cc4db-400">Вы можете использовать существующую связанную службу хранилища данных или указать новое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="cc4db-401">toouse существующей связанной службы, необходимо выбрать **из СУЩЕСТВУЮЩИХ СВЯЗАННЫХ СЛУЖБ** и выберите hello правой связанной службы.</span><span class="sxs-lookup"><span data-stu-id="cc4db-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="cc4db-402">![Средство копирования — страница "Исходное хранилище данных"](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="cc4db-403">На hello **укажите учетную запись хранилища больших двоичных объектов Azure hello** страницы:</span><span class="sxs-lookup"><span data-stu-id="cc4db-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="cc4db-404">Сохранить hello автоматически созданным именем для **имя подключения**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="cc4db-405">Имя подключения Hello является именем hello hello связанной службы типа: хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="cc4db-406">Убедитесь, что в качестве **метода выбора учетной записи** выбран вариант **From Azure subscriptions** (Из подписок Azure).</span><span class="sxs-lookup"><span data-stu-id="cc4db-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="cc4db-407">В поле **Подписка Azure** выберите свою подписку Azure или оставьте значение **Select all** (Выбрать все).</span><span class="sxs-lookup"><span data-stu-id="cc4db-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="cc4db-408">Выберите **учетной записи хранилища Azure** из hello список хранилища Azure учетные записи, доступные в hello выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="cc4db-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="cc4db-409">Можно также выбрать tooenter параметры учетной записи хранилища вручную, выбрав **вручную ввести** параметр для hello **учетной записи метод выбора**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="cc4db-410">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-410">Click **Next**.</span></span> 
      <span data-ttu-id="cc4db-411">![Средство копирования — указать учетную запись хранилища больших двоичных объектов Azure hello](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="cc4db-412">На **выбрать hello входной файл или папку** страницы:</span><span class="sxs-lookup"><span data-stu-id="cc4db-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="cc4db-413">Дважды щелкните **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="cc4db-414">Выберите **input** и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="cc4db-415">В этом пошаговом руководстве выбирается hello папка входных данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="cc4db-416">Можно также выбрать hello emp.txt файл в папке hello вместо него.</span><span class="sxs-lookup"><span data-stu-id="cc4db-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="cc4db-417">![Средство копирования: Выбор hello входного файла или папки](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="cc4db-418">На hello **выбрать hello входной файл или папку** страницы:</span><span class="sxs-lookup"><span data-stu-id="cc4db-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="cc4db-419">Убедитесь, что hello **файла или папки** задано слишком**adfblobconnector или ввода**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="cc4db-420">Если hello файлы во вложенных папках, например, 2017 г/04/01 2017 г/04/02 и т. д., введите adfblobconnector/входные данные / {year} / {month} / {day} для файла или папки.</span><span class="sxs-lookup"><span data-stu-id="cc4db-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="cc4db-421">При нажатии клавиши TAB вне hello текстовое поле, вы увидите три формата tooselect раскрывающиеся списки года (гггг), month (MM) и день (dd).</span><span class="sxs-lookup"><span data-stu-id="cc4db-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="cc4db-422">Не устанавливайте флажок **Copy file recursively** (Копировать файл рекурсивно).</span><span class="sxs-lookup"><span data-stu-id="cc4db-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="cc4db-423">Выберите перекрестной toorecursively этот параметр по папкам для назначения копируются toohello toobe файлов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="cc4db-424">Здравствуйте, не **двоичного копирования** параметр.</span><span class="sxs-lookup"><span data-stu-id="cc4db-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="cc4db-425">Выберите этот параметр tooperform двоичные копию исходного файла toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="cc4db-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="cc4db-426">Не устанавливайте в данном пошаговом руководстве, чтобы вы могли видеть дополнительные параметры в следующих страницах hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="cc4db-427">Убедитесь, что hello **тип сжатия** задано слишком**нет**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="cc4db-428">Выберите значение для этого параметра, если исходные файлы будут сжаты в одном из форматов hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="cc4db-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="cc4db-429">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-429">Click **Next**.</span></span>
    <span data-ttu-id="cc4db-430">![Средство копирования: Выбор hello входного файла или папки](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="cc4db-431">На hello **настроек формата файла** страницы, появятся разделители hello и hello схему, которая определяется автоматически мастером hello путем синтаксического анализа файла hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="cc4db-432">Подтвердите hello следующие варианты:.</span><span class="sxs-lookup"><span data-stu-id="cc4db-432">Confirm hello following options: a.</span></span> <span data-ttu-id="cc4db-433">Hello **формат файла** задано слишком**текстовом формате**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="cc4db-434">Вы увидите все форматы hello поддерживается в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="cc4db-435">Например, JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="cc4db-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="cc4db-436">b.</span><span class="sxs-lookup"><span data-stu-id="cc4db-436">b.</span></span> <span data-ttu-id="cc4db-437">Hello **разделитель столбцов** задано слишком`Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="cc4db-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="cc4db-438">Вы увидите hello другие поддерживаемые фабрикой данных в раскрывающемся списке hello разделители столбцов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="cc4db-439">Вы также можете указать пользовательский разделитель.</span><span class="sxs-lookup"><span data-stu-id="cc4db-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="cc4db-440">c.</span><span class="sxs-lookup"><span data-stu-id="cc4db-440">c.</span></span> <span data-ttu-id="cc4db-441">Hello **разделитель строк** задано слишком`Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="cc4db-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="cc4db-442">Вы увидите hello другие поддерживаемые фабрикой данных в раскрывающемся списке hello разделителей строк.</span><span class="sxs-lookup"><span data-stu-id="cc4db-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="cc4db-443">Вы также можете указать пользовательский разделитель.</span><span class="sxs-lookup"><span data-stu-id="cc4db-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="cc4db-444">d.</span><span class="sxs-lookup"><span data-stu-id="cc4db-444">d.</span></span> <span data-ttu-id="cc4db-445">Hello **пропустить число строк** задано слишком**0**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="cc4db-446">Если требуется несколько toobe строк пропущен в начале hello hello файла, введите здесь номер hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="cc4db-447">д.</span><span class="sxs-lookup"><span data-stu-id="cc4db-447">e.</span></span>  <span data-ttu-id="cc4db-448">Hello **первая строка данных содержит имена столбцов** не задано.</span><span class="sxs-lookup"><span data-stu-id="cc4db-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="cc4db-449">Если исходные файлы hello содержат имена столбцов в первой строке hello, выберите этот параметр.</span><span class="sxs-lookup"><span data-stu-id="cc4db-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="cc4db-450">f.</span><span class="sxs-lookup"><span data-stu-id="cc4db-450">f.</span></span> <span data-ttu-id="cc4db-451">Hello **значение пустой столбец рассматривается как null** был установлен.</span><span class="sxs-lookup"><span data-stu-id="cc4db-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="cc4db-452">Разверните **Дополнительные параметры** toosee дополнительный параметр доступен.</span><span class="sxs-lookup"><span data-stu-id="cc4db-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="cc4db-453">Hello нижней части страницы приветствия, в разделе hello **предварительного просмотра** данных из файла emp.txt hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="cc4db-454">Нажмите кнопку **СХЕМЫ** tab в hello нижней toosee hello схем, мастер копирования hello вывести путем просмотра данных hello в исходном файле hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="cc4db-455">Нажмите кнопку **Далее** после проверки разделители hello и предварительного просмотра данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="cc4db-456">![Средство копирования — параметры формата файла](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="cc4db-457">На hello **хранения данных назначения страницы**выберите **хранилища больших двоичных объектов**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="cc4db-458">Оба hello исходного и конечного хранилищ данных в этом пошаговом руководстве используются hello хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="cc4db-459">![Мастер копирования — выбор целевого хранилища данных](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="cc4db-460">На **укажите учетную запись хранилища больших двоичных объектов Azure hello** страницы:</span><span class="sxs-lookup"><span data-stu-id="cc4db-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="cc4db-461">Введите **AzureStorageLinkedService** для hello **имя подключения** поля.</span><span class="sxs-lookup"><span data-stu-id="cc4db-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="cc4db-462">Убедитесь, что в качестве **метода выбора учетной записи** выбран вариант **From Azure subscriptions** (Из подписок Azure).</span><span class="sxs-lookup"><span data-stu-id="cc4db-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="cc4db-463">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="cc4db-464">Выберите свою учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="cc4db-465">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-465">Click **Next**.</span></span>     
10. <span data-ttu-id="cc4db-466">На hello **hello Выбор выходного файла или папки** страницы:</span><span class="sxs-lookup"><span data-stu-id="cc4db-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="cc4db-467">В поле **Путь к папке** укажите **adfblobconnector/output/{год}/{месяц}/{день}**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="cc4db-468">Нажмите клавишу **TAB**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="cc4db-469">Для hello **года**выберите **гггг**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="cc4db-470">Для hello **месяц**, убедитесь, что оно задано слишком**мм**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="cc4db-471">Для hello **день**, убедитесь, что оно задано слишком**дд**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="cc4db-472">Убедитесь, что hello **тип сжатия** задано слишком**нет**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="cc4db-473">Убедитесь, что hello **скопируйте поведение** задано слишком**выполнить слияние файлов**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="cc4db-474">Если hello выходной файл с таким же именем уже существует hello, hello новое содержимое будет добавлено toohello тот же файл в конце hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="cc4db-475">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-475">Click **Next**.</span></span>
    <span data-ttu-id="cc4db-476">![Средство копирования — выбор выходного файла или папки](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="cc4db-477">На hello **настроек формата файла** , проверьте параметры hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="cc4db-478">Одна из hello здесь дополнительные параметры — tooadd файл заголовка toohello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="cc4db-479">Если выбран этот параметр, строку заголовка добавляется с именами столбцов hello из схемы hello hello источника.</span><span class="sxs-lookup"><span data-stu-id="cc4db-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="cc4db-480">Имена столбцов по умолчанию hello можно переименовать при просмотре hello схему для источника hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="cc4db-481">Например можно изменить hello tooFirst первого столбца Name и второй столбец tooLast имя.</span><span class="sxs-lookup"><span data-stu-id="cc4db-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="cc4db-482">Затем hello выходной файл создается с заголовком с этими именами, как имена столбцов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="cc4db-483">![Средство копирования — параметры формата файла для назначения](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="cc4db-484">На hello **параметры производительности** убедитесь, что **облако единицы** и **параллельные копии** заданы слишком**автоматически**и нажмите кнопку Далее.</span><span class="sxs-lookup"><span data-stu-id="cc4db-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="cc4db-485">Дополнительные сведения об этих параметрах см. в [руководстве по производительности и настройке действия копирования](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="cc4db-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="cc4db-486">![Средство копирования — параметры производительности](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="cc4db-487">На hello **Сводка** , просмотрите все параметры (свойства задачи, параметры для источника и назначения и копии) и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="cc4db-488">![Средство копирования — страница "Сводка"](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="cc4db-489">Просмотрите сведения в hello **Сводка** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="cc4db-490">Hello мастер создает две связанные службы, два набора данных (ввода и вывода) и один конвейер в фабрике данных hello (из которой запущено приветствия мастера копирования).</span><span class="sxs-lookup"><span data-stu-id="cc4db-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="cc4db-491">![Средство копирования — страница "Развертывание"](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="cc4db-492">Монитор hello конвейера (задача copy)</span><span class="sxs-lookup"><span data-stu-id="cc4db-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="cc4db-493">Щелкните ссылку hello `Click here toomonitor copy pipeline` на hello **развертывания** страницы.</span><span class="sxs-lookup"><span data-stu-id="cc4db-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="cc4db-494">Вы увидите hello **отслеживать и контролировать приложения** на отдельной вкладке.  ![Приложение для мониторинга и управления](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="cc4db-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="cc4db-495">Изменение hello **запустить** время вверху hello слишком`04/19/2017` и **окончания** время слишком`04/27/2017`и нажмите кнопку **применить**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="cc4db-496">Вы увидите пять окон действий в hello **действия WINDOWS** списка.</span><span class="sxs-lookup"><span data-stu-id="cc4db-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="cc4db-497">Hello **WindowStart** раз должен охватывать все дней после окончания toopipeline начало конвейера.</span><span class="sxs-lookup"><span data-stu-id="cc4db-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="cc4db-498">Нажмите кнопку **обновление** кнопки для hello **действия WINDOWS** несколько раз, пока не увидите hello состояние всех окон действие hello установлено tooReady.</span><span class="sxs-lookup"><span data-stu-id="cc4db-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="cc4db-499">Теперь убедитесь, что hello выходные файлы создаются в выходной папке hello adfblobconnector контейнера.</span><span class="sxs-lookup"><span data-stu-id="cc4db-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="cc4db-500">Вы должны увидеть hello следующая структура папок в выходной папке hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="cc4db-501">Подробные сведения о мониторинге фабрик данных и управлении ими см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="cc4db-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="cc4db-502">Сущности фабрики данных</span><span class="sxs-lookup"><span data-stu-id="cc4db-502">Data Factory entities</span></span>
<span data-ttu-id="cc4db-503">Перейдите назад toohello вкладка с домашней страницы приветствия фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="cc4db-504">Обратите внимание, что в фабрике данных теперь есть две связанные службы, два набора данных и один конвейер.</span><span class="sxs-lookup"><span data-stu-id="cc4db-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Домашняя страница фабрики данных с сущностями](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="cc4db-506">Нажмите кнопку **автор и развернуть** toolaunch редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Редактор фабрики данных](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="cc4db-508">Вы должны увидеть hello, следуя фабрики данных сущности в вашей фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="cc4db-509">Две связанные службы:</span><span class="sxs-lookup"><span data-stu-id="cc4db-509">Two linked services.</span></span> <span data-ttu-id="cc4db-510">Одно для источника hello и hello, другой для назначения hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="cc4db-511">Обе службы hello связаны ссылаться toohello учетную запись хранилища Azure в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="cc4db-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="cc4db-512">Два набора данных:</span><span class="sxs-lookup"><span data-stu-id="cc4db-512">Two datasets.</span></span> <span data-ttu-id="cc4db-513">входной и выходной.</span><span class="sxs-lookup"><span data-stu-id="cc4db-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="cc4db-514">В этом пошаговом руководстве используются hello же больших двоичных объектов контейнера, но ссылаться toodifferent папок (ввода и вывода).</span><span class="sxs-lookup"><span data-stu-id="cc4db-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="cc4db-515">Один конвейер.</span><span class="sxs-lookup"><span data-stu-id="cc4db-515">A pipeline.</span></span> <span data-ttu-id="cc4db-516">конвейер Hello содержит операции копирования, которая использует источник больших двоичных объектов и данных BLOB-объект приемника toocopy из tooanother расположение BLOB-объектов Azure расположение BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="cc4db-517">Hello следующих разделах содержатся дополнительные сведения об этих сущностях.</span><span class="sxs-lookup"><span data-stu-id="cc4db-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="cc4db-518">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="cc4db-518">Linked services</span></span>
<span data-ttu-id="cc4db-519">Вы должны видеть две связанные службы:</span><span class="sxs-lookup"><span data-stu-id="cc4db-519">You should see two linked services.</span></span> <span data-ttu-id="cc4db-520">Одно для источника hello и hello, другой для назначения hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="cc4db-521">В этом пошаговом руководстве представлены оба вида определения hello таким же за исключением имен hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="cc4db-522">Hello **тип** hello связанной службы задано слишком**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="cc4db-523">Наиболее важные свойства определения службы hello связаны — hello **connectionString**, который используется для tooyour tooconnect фабрики данных учетной записи хранилища Azure во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="cc4db-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="cc4db-524">Игнорируйте свойство hubName hello в определении hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="cc4db-525">Связанная служба исходного хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cc4db-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="cc4db-526">Связанная служба выходного хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cc4db-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="cc4db-527">Дополнительные сведения о связанной службе хранилища Azure см. в разделе [Свойства связанной службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="cc4db-528">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="cc4db-528">Datasets</span></span>
<span data-ttu-id="cc4db-529">Есть два набора данных: входной и выходной.</span><span class="sxs-lookup"><span data-stu-id="cc4db-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="cc4db-530">Тип Hello hello набора данных установлен слишком**AzureBlob** для обоих.</span><span class="sxs-lookup"><span data-stu-id="cc4db-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="cc4db-531">Входной набор данных Hello указывает toohello **ввода** папки hello **adfblobconnector** контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="cc4db-532">Hello **внешних** задано слишком**true** для этого набора данных как hello данные не создаются конвейером hello действием копирования hello, которое принимает этот набор данных в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="cc4db-533">Hello выходной набор данных точек toohello **выходные данные** папки hello же контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="cc4db-534">Hello выходной набор данных также использует hello год, месяц и день hello **SliceStart** переменных toodynamically системы оценки hello путь для выходного файла hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="cc4db-535">Список функций и системных переменных, поддерживаемых фабрикой данных Azure, см. в [этой статье](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="cc4db-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="cc4db-536">Hello **внешних** задано слишком**false** (значение по умолчанию), так как этот набор данных создается путем hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="cc4db-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="cc4db-537">Дополнительные сведения о свойствах, поддерживаемых набором данных большого двоичного объекта Azure, см. в разделе [свойств набора данных](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="cc4db-538">Входной набор данных</span><span class="sxs-lookup"><span data-stu-id="cc4db-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
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
}
```

##### <a name="output-dataset"></a><span data-ttu-id="cc4db-539">Выходной набор данных</span><span class="sxs-lookup"><span data-stu-id="cc4db-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="cc4db-540">Конвейер</span><span class="sxs-lookup"><span data-stu-id="cc4db-540">Pipeline</span></span>
<span data-ttu-id="cc4db-541">конвейер Hello содержит только одно действие.</span><span class="sxs-lookup"><span data-stu-id="cc4db-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="cc4db-542">Hello **тип** hello действие задано слишком**копирования**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="cc4db-543">В свойства типа hello для действия "hello" существует два раздела: один для источника и hello, другой для приемника.</span><span class="sxs-lookup"><span data-stu-id="cc4db-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="cc4db-544">Тип источника Hello задано слишком**BlobSource** как hello действие копирование данных из хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="cc4db-545">Hello тип приемника задано слишком**BlobSink** как копирование больших двоичных объектов хранилища данных tooa действие hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="cc4db-546">Действие копирования Hello InputDataset z4y принимает в качестве входных данных hello и OutputDataset-z4y в качестве выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="cc4db-547">Дополнительные сведения о свойствах, поддерживаемых BlobSource и BlobSink, см. в разделе [свойств действия копирования](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
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
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="cc4db-548">Примеры JSON для копирования данных tooand из хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cc4db-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="cc4db-549">Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cc4db-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="cc4db-550">Они показывают как toocopy tooand данных из хранилища больших двоичных объектов и базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="cc4db-551">Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4db-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="cc4db-552">Пример JSON: Копирование данных из хранилища больших двоичных объектов tooSQL базы данных</span><span class="sxs-lookup"><span data-stu-id="cc4db-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="cc4db-553">Hello следующем образце показано:</span><span class="sxs-lookup"><span data-stu-id="cc4db-553">hello following sample shows:</span></span>

1. <span data-ttu-id="cc4db-554">Связанная служба типа [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="cc4db-555">Связанная служба типа [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="cc4db-556">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="cc4db-557">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cc4db-558">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](#copy-activity-properties) и [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cc4db-559">Образец Hello копирует временных рядов данных из таблиц Azure SQL tooan BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="cc4db-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="cc4db-560">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cc4db-561">**Связанная служба SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="cc4db-561">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="cc4db-562">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="cc4db-562">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="cc4db-563">Фабрика данных Azure поддерживает два типа связанных служб хранилища Azure: **AzureStorage** и **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="cc4db-564">Для hello первый, укажите строку подключения hello, содержащую ключ учетной записи hello и для hello позже у одного укажите hello Uri подписи общего доступа (SAS).</span><span class="sxs-lookup"><span data-stu-id="cc4db-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="cc4db-565">Дополнительные сведения см. в разделе [Связанные службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="cc4db-566">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="cc4db-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="cc4db-567">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="cc4db-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cc4db-568">Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="cc4db-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="cc4db-569">путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="cc4db-570">«external»: параметр «true» сообщает фабрики данных, таблица hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
<span data-ttu-id="cc4db-571">**Выходной набор данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="cc4db-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="cc4db-572">Образец Hello копирует tooa таблицу данных, с именем «MyTable» в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="cc4db-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="cc4db-573">Создать таблицу hello в базе данных Azure SQL с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cc4db-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="cc4db-574">Новые строки добавляются в таблицу toohello каждый час.</span><span class="sxs-lookup"><span data-stu-id="cc4db-574">New rows are added toohello table every hour.</span></span>

```json
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
<span data-ttu-id="cc4db-575">**Действие копирования в конвейере с BLOB-объектом в качестве источника и базой данных SQL в качестве приемника:**</span><span class="sxs-lookup"><span data-stu-id="cc4db-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="cc4db-576">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="cc4db-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="cc4db-577">В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
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
            "type": "BlobSource"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="cc4db-578">Пример JSON: Копирование данных из Azure SQL tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cc4db-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="cc4db-579">Hello следующем образце показано:</span><span class="sxs-lookup"><span data-stu-id="cc4db-579">hello following sample shows:</span></span>

1. <span data-ttu-id="cc4db-580">Связанная служба типа [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="cc4db-581">Связанная служба типа [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="cc4db-582">Входной [набор данных](data-factory-create-datasets.md) типа [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="cc4db-583">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="cc4db-584">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) и [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="cc4db-585">Образец Hello копирует данные временного ряда из tooan таблицы Azure SQL BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="cc4db-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="cc4db-586">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cc4db-587">**Связанная служба SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="cc4db-587">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="cc4db-588">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="cc4db-588">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="cc4db-589">Фабрика данных Azure поддерживает два типа связанных служб хранилища Azure: **AzureStorage** и **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="cc4db-590">Для hello первый, укажите строку подключения hello, содержащую ключ учетной записи hello и для hello позже у одного укажите hello Uri подписи общего доступа (SAS).</span><span class="sxs-lookup"><span data-stu-id="cc4db-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="cc4db-591">Дополнительные сведения см. в разделе [Связанные службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc4db-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="cc4db-592">**Входной набор данных SQL Azure**</span><span class="sxs-lookup"><span data-stu-id="cc4db-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="cc4db-593">Образец Hello предполагается создания таблицы «MyTable» в Azure SQL и содержит столбец с именем «timestampcolumn» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="cc4db-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="cc4db-594">Параметр «external»: «true» уведомляет службу фабрики данных, что таблица hello внешних toohello фабрики данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
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

<span data-ttu-id="cc4db-595">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="cc4db-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="cc4db-596">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="cc4db-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cc4db-597">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="cc4db-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="cc4db-598">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="cc4db-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
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
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

<span data-ttu-id="cc4db-599">**Действие копирования в конвейере с базой данных SQL в качестве источника и BLOB-объектом в качестве приемника:**</span><span class="sxs-lookup"><span data-stu-id="cc4db-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="cc4db-600">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="cc4db-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="cc4db-601">В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cc4db-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="cc4db-602">запрос SQL Hello, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="cc4db-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
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

> [!NOTE]
> <span data-ttu-id="cc4db-603">toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="cc4db-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="cc4db-604">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="cc4db-604">Performance and Tuning</span></span>
<span data-ttu-id="cc4db-605">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="cc4db-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
