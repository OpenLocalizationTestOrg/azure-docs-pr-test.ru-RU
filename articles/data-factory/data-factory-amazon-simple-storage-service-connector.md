---
title: "aaaMove данные из Amazon Simple Storage Service с помощью фабрики данных | Документы Microsoft"
description: "Дополнительные сведения о том, как данные toomove из Amazon Simple Storage Service (S3) с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="d5d6e-103">Перемещение данных из Amazon Simple Storage Service с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="d5d6e-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="d5d6e-104">В этой статье объясняется, как toouse hello в действии копирования данных toomove фабрики данных Azure из Amazon Simple Storage Service (S3).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="d5d6e-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="d5d6e-106">Можно скопировать данные из хранилища Amazon S3 tooany поддерживается приемник данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="d5d6e-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d5d6e-108">Фабрика данных в настоящее время поддерживает только перемещения данных из хранилищ данных tooother Amazon S3, но не перемещения данных из других данных хранит tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="d5d6e-109">Необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="d5d6e-109">Required permissions</span></span>
<span data-ttu-id="d5d6e-110">toocopy данные из Amazon S3, убедитесь, что предоставлены следующие разрешения hello:</span><span class="sxs-lookup"><span data-stu-id="d5d6e-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="d5d6e-111">`s3:GetObject` и `s3:GetObjectVersion` для операций с объектами Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="d5d6e-112">`s3:ListBucket` для операций в контейнере Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="d5d6e-113">Если вы используете приветствия мастера копирования фабрики данных, `s3:ListAllMyBuckets` также является обязательным.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="d5d6e-114">Дополнительные сведения о hello полный список разрешений Amazon S3 см [указание разрешений в политике](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="d5d6e-115">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="d5d6e-115">Getting started</span></span>
<span data-ttu-id="d5d6e-116">Вы можете создать конвейер с действием копирования, которое перемещает данные из источника Amazon S3 с помощью различных средств или API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="d5d6e-117">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d5d6e-118">Краткое пошаговое руководство представлено в разделе [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="d5d6e-119">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d5d6e-120">Пошаговые инструкции toocreate конвейер с операции копирования, в разделе hello [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="d5d6e-121">Используется ли инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello:</span><span class="sxs-lookup"><span data-stu-id="d5d6e-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="d5d6e-122">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="d5d6e-123">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="d5d6e-124">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="d5d6e-125">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d5d6e-126">При использовании средств или API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="d5d6e-127">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных Amazon S3 в разделе hello [пример JSON: копирование данных из tooAzure Amazon S3 большого двоичного объекта](#json-example-copy-data-from-amazon-s3-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="d5d6e-128">Подробные сведения о поддерживаемых форматах файлов и сжатия для действия копирования см. в разделе [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="d5d6e-129">Hello в следующих разделах приведены сведения о JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d5d6e-130">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="d5d6e-130">Linked service properties</span></span>
<span data-ttu-id="d5d6e-131">Связанная служба связывает фабрику данных tooa хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="d5d6e-132">Создание связанной службы типа **AwsAccessKey** toolink данных Amazon S3 хранения tooyour фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="d5d6e-133">службу описание для конкретных tooAmazon элементы JSON S3 (AwsAccessKey) связан обеспечивает Hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="d5d6e-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="d5d6e-134">Property</span></span> | <span data-ttu-id="d5d6e-135">Описание</span><span class="sxs-lookup"><span data-stu-id="d5d6e-135">Description</span></span> | <span data-ttu-id="d5d6e-136">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="d5d6e-136">Allowed values</span></span> | <span data-ttu-id="d5d6e-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5d6e-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5d6e-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="d5d6e-138">accessKeyID</span></span> |<span data-ttu-id="d5d6e-139">Идентификатор hello доступа секретного ключа.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-139">ID of hello secret access key.</span></span> |<span data-ttu-id="d5d6e-140">string</span><span class="sxs-lookup"><span data-stu-id="d5d6e-140">string</span></span> |<span data-ttu-id="d5d6e-141">Да</span><span class="sxs-lookup"><span data-stu-id="d5d6e-141">Yes</span></span> |
| <span data-ttu-id="d5d6e-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="d5d6e-142">secretAccessKey</span></span> |<span data-ttu-id="d5d6e-143">Hello секретный доступа самого ключа.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-143">hello secret access key itself.</span></span> |<span data-ttu-id="d5d6e-144">Зашифрованная строка секрета</span><span class="sxs-lookup"><span data-stu-id="d5d6e-144">Encrypted secret string</span></span> |<span data-ttu-id="d5d6e-145">Да</span><span class="sxs-lookup"><span data-stu-id="d5d6e-145">Yes</span></span> |

<span data-ttu-id="d5d6e-146">Пример:</span><span class="sxs-lookup"><span data-stu-id="d5d6e-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d5d6e-147">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="d5d6e-147">Dataset properties</span></span>
<span data-ttu-id="d5d6e-148">toospecify dataset toorepresent входные данные в хранилище больших двоичных объектов Azure, задать свойство типа hello hello набора данных, слишком**AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="d5d6e-149">Набор hello **linkedServiceName** toohello имя набора данных hello hello Amazon S3 свойство связанной службы.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="d5d6e-150">Полный список разделов и свойств, доступных для определения наборов данных, см. в разделе [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="d5d6e-151">Разделы structure, availability и policy одинаковы для всех типов наборов данных (таких как базы данных SQL, большие двоичные объекты Azure и таблицы Azure).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="d5d6e-152">Hello **typeProperties** разделе отличается для каждого типа набора данных, а также содержит сведения о месте hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="d5d6e-153">Hello **typeProperties** раздел для набора данных типа **AmazonS3** (включает набор данных hello Amazon S3) имеет следующие свойства hello:</span><span class="sxs-lookup"><span data-stu-id="d5d6e-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="d5d6e-154">Свойство</span><span class="sxs-lookup"><span data-stu-id="d5d6e-154">Property</span></span> | <span data-ttu-id="d5d6e-155">Описание</span><span class="sxs-lookup"><span data-stu-id="d5d6e-155">Description</span></span> | <span data-ttu-id="d5d6e-156">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="d5d6e-156">Allowed values</span></span> | <span data-ttu-id="d5d6e-157">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5d6e-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5d6e-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="d5d6e-158">bucketName</span></span> |<span data-ttu-id="d5d6e-159">Имя сегмента Hello S3.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-159">hello S3 bucket name.</span></span> |<span data-ttu-id="d5d6e-160">Строка</span><span class="sxs-lookup"><span data-stu-id="d5d6e-160">String</span></span> |<span data-ttu-id="d5d6e-161">Да</span><span class="sxs-lookup"><span data-stu-id="d5d6e-161">Yes</span></span> |
| <span data-ttu-id="d5d6e-162">key</span><span class="sxs-lookup"><span data-stu-id="d5d6e-162">key</span></span> |<span data-ttu-id="d5d6e-163">ключ объекта Hello S3.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-163">hello S3 object key.</span></span> |<span data-ttu-id="d5d6e-164">Строка</span><span class="sxs-lookup"><span data-stu-id="d5d6e-164">String</span></span> |<span data-ttu-id="d5d6e-165">Нет</span><span class="sxs-lookup"><span data-stu-id="d5d6e-165">No</span></span> |
| <span data-ttu-id="d5d6e-166">prefix</span><span class="sxs-lookup"><span data-stu-id="d5d6e-166">prefix</span></span> |<span data-ttu-id="d5d6e-167">Префикс для ключа объекта S3 hello.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="d5d6e-168">Выбираются объекты, ключи которых начинаются с этого префикса.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="d5d6e-169">Применяется, только если ключ пустой.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-169">Applies only when key is empty.</span></span> |<span data-ttu-id="d5d6e-170">string</span><span class="sxs-lookup"><span data-stu-id="d5d6e-170">String</span></span> |<span data-ttu-id="d5d6e-171">Нет</span><span class="sxs-lookup"><span data-stu-id="d5d6e-171">No</span></span> |
| <span data-ttu-id="d5d6e-172">версия</span><span class="sxs-lookup"><span data-stu-id="d5d6e-172">version</span></span> |<span data-ttu-id="d5d6e-173">версия Hello hello S3 объекта, если включено управление версиями S3.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="d5d6e-174">Строка</span><span class="sxs-lookup"><span data-stu-id="d5d6e-174">String</span></span> |<span data-ttu-id="d5d6e-175">Нет</span><span class="sxs-lookup"><span data-stu-id="d5d6e-175">No</span></span> |
| <span data-ttu-id="d5d6e-176">свойства</span><span class="sxs-lookup"><span data-stu-id="d5d6e-176">format</span></span> | <span data-ttu-id="d5d6e-177">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d5d6e-178">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d5d6e-179">Дополнительные сведения см. в разделе hello [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формат JSON](data-factory-supported-file-and-compression-formats.md#json-format), [формат Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формат Orc](data-factory-supported-file-and-compression-formats.md#orc-format), и [Parquet формат ](data-factory-supported-file-and-compression-formats.md#parquet-format) разделы.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d5d6e-180">Если требуется, чтобы файлы toocopy как — между файловых хранилищ (двоичного копирования), skip hello формат раздела оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d5d6e-181">Нет</span><span class="sxs-lookup"><span data-stu-id="d5d6e-181">No</span></span> | |
| <span data-ttu-id="d5d6e-182">compression</span><span class="sxs-lookup"><span data-stu-id="d5d6e-182">compression</span></span> | <span data-ttu-id="d5d6e-183">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d5d6e-184">Hello поддерживаемые типы: **GZip**, **Deflate**, **BZip2**, и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d5d6e-185">уровни Hello поддерживается: **оптимальный** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d5d6e-186">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d5d6e-187">Нет</span><span class="sxs-lookup"><span data-stu-id="d5d6e-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="d5d6e-188">**bucketName + клавиша** указывает расположение hello объекта hello S3, где контейнеров — hello корневой контейнер для объектов S3 и ключ — объект toohello S3 hello полный путь.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="d5d6e-189">Пример набора данных с префиксом</span><span class="sxs-lookup"><span data-stu-id="d5d6e-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="d5d6e-190">Пример набора данных (с версией)</span><span class="sxs-lookup"><span data-stu-id="d5d6e-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="d5d6e-191">Динамические пути для S3</span><span class="sxs-lookup"><span data-stu-id="d5d6e-191">Dynamic paths for S3</span></span>
<span data-ttu-id="d5d6e-192">Hello предыдущего примера использует фиксированные значения для hello **ключ** и **bucketName** свойства в наборе данных hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="d5d6e-193">Можно настроить фабрику данных для динамического вычисления значений этих свойств во время выполнения с помощью системных переменных, например SliceStart.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="d5d6e-194">Можно сделать hello одинаково для hello **префикс** свойства набора данных Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="d5d6e-195">Список поддерживаемых функций и переменных см. в статье [Функции и системные переменные фабрики данных](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="d5d6e-196">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="d5d6e-196">Copy activity properties</span></span>
<span data-ttu-id="d5d6e-197">Полный список разделов и свойств, доступных для определения действий, см. в разделе [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="d5d6e-198">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="d5d6e-199">Свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="d5d6e-200">Для действия копирования hello свойства зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="d5d6e-201">Если источник в действии копирования hello имеет тип **FileSystemSource** (включая Amazon S3), hello следующие свойства доступны в **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="d5d6e-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="d5d6e-202">Свойство</span><span class="sxs-lookup"><span data-stu-id="d5d6e-202">Property</span></span> | <span data-ttu-id="d5d6e-203">Описание</span><span class="sxs-lookup"><span data-stu-id="d5d6e-203">Description</span></span> | <span data-ttu-id="d5d6e-204">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="d5d6e-204">Allowed values</span></span> | <span data-ttu-id="d5d6e-205">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5d6e-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5d6e-206">recursive</span><span class="sxs-lookup"><span data-stu-id="d5d6e-206">recursive</span></span> |<span data-ttu-id="d5d6e-207">Указывает объекты ли список toorecursively S3 hello в каталоге.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="d5d6e-208">True или false</span><span class="sxs-lookup"><span data-stu-id="d5d6e-208">true/false</span></span> |<span data-ttu-id="d5d6e-209">Нет</span><span class="sxs-lookup"><span data-stu-id="d5d6e-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="d5d6e-210">Пример JSON: копирование данных из tooAzure Amazon S3 хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="d5d6e-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="d5d6e-211">В этом примере показано, как данные toocopy из tooan Amazon S3 хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="d5d6e-212">Тем не менее, данные можно скопировать непосредственно слишком[любой hello приемников, которые поддерживаются](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью действия копирования hello в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="d5d6e-213">Образец Hello предоставляет определения JSON для hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="d5d6e-214">Можно использовать эти определения toocreate toocopy конвейера данных из хранилища tooBlob Amazon S3, с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="d5d6e-215">Связанная служба типа [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="d5d6e-216">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="d5d6e-217">Входной [набор данных](data-factory-create-datasets.md) типа [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="d5d6e-218">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="d5d6e-219">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d5d6e-220">Образец Hello копирует данные из tooan Amazon S3 BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="d5d6e-221">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="d5d6e-222">Связанная служба Amazon S3</span><span class="sxs-lookup"><span data-stu-id="d5d6e-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="d5d6e-223">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="d5d6e-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="d5d6e-224">Входной набор данных Amazon S3</span><span class="sxs-lookup"><span data-stu-id="d5d6e-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="d5d6e-225">Установка **«external»: true** информирует служба фабрики данных hello hello набор данных является фабрикой toohello внешних данных.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="d5d6e-226">Задайте это свойство tootrue для входного набора данных, который не был создан из действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="d5d6e-227">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="d5d6e-227">Azure Blob output dataset</span></span>

<span data-ttu-id="d5d6e-228">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d5d6e-229">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d5d6e-230">путь к папке Hello использует hello года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="d5d6e-231">Действие копирования в конвейере с Amazon S3 в качестве источника и BLOB-объектом в качестве приемника</span><span class="sxs-lookup"><span data-stu-id="d5d6e-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="d5d6e-232">Hello конвейера содержит операции копирования, настроенные toouse hello наборы входных и выходных данных, а — запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="d5d6e-233">В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource**, и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="d5d6e-234">разделе toomap столбцы из источника toocolumns набора данных, из набора приемника [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d5d6e-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5d6e-235">Next steps</span></span>
<span data-ttu-id="d5d6e-236">См. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="d5d6e-236">See hello following articles:</span></span>

* <span data-ttu-id="d5d6e-237">toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных и различных способов toooptimize, разделе hello [копирование действия производительности и руководство по настройке](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="d5d6e-238">Пошаговые инструкции для создания конвейера с помощью операции копирования см. в разделе hello [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d5d6e-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
