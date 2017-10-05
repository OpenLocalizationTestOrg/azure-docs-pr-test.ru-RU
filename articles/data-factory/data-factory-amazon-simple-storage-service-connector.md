---
title: "Перемещение данных из Amazon Simple Storage Service с помощью фабрики данных | Документы Майкрософт"
description: "Вы можете узнать, как переместить данные из Amazon Simple Storage Service (S3) с помощью фабрики данных Azure."
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
ms.openlocfilehash: 3e21f7dfccc3b235071344a28c7d94f65e6bf9ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="5f946-103">Перемещение данных из Amazon Simple Storage Service с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="5f946-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="5f946-104">В этой статье описано, как с помощью действия копирования в фабрике данных Azure перемещать данные из службы хранения Amazon Simple Storage Service (S3).</span><span class="sxs-lookup"><span data-stu-id="5f946-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="5f946-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="5f946-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="5f946-106">Данные из Amazon S3 можно скопировать в любое хранилище данных, поддерживаемое в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="5f946-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="5f946-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, см. в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="5f946-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="5f946-108">Сейчас фабрика данных поддерживает только перемещение данных из Amazon S3 в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="5f946-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="5f946-109">Необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="5f946-109">Required permissions</span></span>
<span data-ttu-id="5f946-110">Чтобы скопировать данные из Amazon S3, убедитесь, что вы предоставили следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="5f946-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="5f946-111">`s3:GetObject` и `s3:GetObjectVersion` для операций с объектами Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="5f946-112">`s3:ListBucket` для операций в контейнере Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="5f946-113">Если вы используете мастер копирования фабрики данных, также требуется разрешение `s3:ListAllMyBuckets`.</span><span class="sxs-lookup"><span data-stu-id="5f946-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="5f946-114">Полный список разрешений Amazon S3 см. в статье, посвященной [назначению разрешений в политике](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="5f946-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="5f946-115">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="5f946-115">Getting started</span></span>
<span data-ttu-id="5f946-116">Вы можете создать конвейер с действием копирования, которое перемещает данные из источника Amazon S3 с помощью различных средств или API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="5f946-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="5f946-117">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="5f946-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="5f946-118">Краткое пошаговое руководство представлено в разделе [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="5f946-119">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="5f946-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5f946-120">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="5f946-121">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="5f946-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="5f946-122">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="5f946-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="5f946-123">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="5f946-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="5f946-124">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="5f946-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="5f946-125">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="5f946-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="5f946-126">При использовании средств или интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="5f946-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="5f946-127">Пример определений JSON для сущностей фабрики данных, которые используются для копирования данных из хранилища данных Amazon S3, вы найдете в разделе [Пример JSON. Копирование данных из Amazon S3 в хранилище BLOB-объектов Azure](#json-example-copy-data-from-amazon-s3-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="5f946-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="5f946-128">Подробные сведения о поддерживаемых форматах файлов и сжатия для действия копирования см. в разделе [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="5f946-129">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5f946-130">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="5f946-130">Linked service properties</span></span>
<span data-ttu-id="5f946-131">Связанная служба привязывает хранилище данных к фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="5f946-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="5f946-132">Для связи хранилища данных Amazon S3 с фабрикой данных следует создать связанную службу типа **AwsAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="5f946-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="5f946-133">В таблице ниже приведено описание элементов JSON, которые относятся к связанной службе Amazon S3 (AwsAccessKey).</span><span class="sxs-lookup"><span data-stu-id="5f946-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="5f946-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="5f946-134">Property</span></span> | <span data-ttu-id="5f946-135">Описание</span><span class="sxs-lookup"><span data-stu-id="5f946-135">Description</span></span> | <span data-ttu-id="5f946-136">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="5f946-136">Allowed values</span></span> | <span data-ttu-id="5f946-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5f946-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f946-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="5f946-138">accessKeyID</span></span> |<span data-ttu-id="5f946-139">Идентификатор секретного ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="5f946-139">ID of the secret access key.</span></span> |<span data-ttu-id="5f946-140">string</span><span class="sxs-lookup"><span data-stu-id="5f946-140">string</span></span> |<span data-ttu-id="5f946-141">Да</span><span class="sxs-lookup"><span data-stu-id="5f946-141">Yes</span></span> |
| <span data-ttu-id="5f946-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="5f946-142">secretAccessKey</span></span> |<span data-ttu-id="5f946-143">Сам секретный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="5f946-143">The secret access key itself.</span></span> |<span data-ttu-id="5f946-144">Зашифрованная строка секрета</span><span class="sxs-lookup"><span data-stu-id="5f946-144">Encrypted secret string</span></span> |<span data-ttu-id="5f946-145">Да</span><span class="sxs-lookup"><span data-stu-id="5f946-145">Yes</span></span> |

<span data-ttu-id="5f946-146">Пример:</span><span class="sxs-lookup"><span data-stu-id="5f946-146">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="5f946-147">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="5f946-147">Dataset properties</span></span>
<span data-ttu-id="5f946-148">Чтобы указать набор данных, представляющий входные данные в хранилище BLOB-объектов Azure, присвойте свойству типа набора данных значение **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="5f946-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="5f946-149">Для свойства **linkedServiceName** набора данных задайте имя связанной службы Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="5f946-150">Полный список разделов и свойств, доступных для определения наборов данных, см. в разделе [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="5f946-151">Разделы structure, availability и policy одинаковы для всех типов наборов данных (таких как базы данных SQL, большие двоичные объекты Azure и таблицы Azure).</span><span class="sxs-lookup"><span data-stu-id="5f946-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="5f946-152">Раздел **typeProperties** во всех типах наборов данных разный. Он содержит сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="5f946-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="5f946-153">Раздел **typeProperties** набора данных типа **AmazonS3** (который включает в себя набор данных Amazon S3) содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="5f946-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="5f946-154">Свойство</span><span class="sxs-lookup"><span data-stu-id="5f946-154">Property</span></span> | <span data-ttu-id="5f946-155">Описание</span><span class="sxs-lookup"><span data-stu-id="5f946-155">Description</span></span> | <span data-ttu-id="5f946-156">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="5f946-156">Allowed values</span></span> | <span data-ttu-id="5f946-157">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5f946-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f946-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="5f946-158">bucketName</span></span> |<span data-ttu-id="5f946-159">Имя контейнера S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-159">The S3 bucket name.</span></span> |<span data-ttu-id="5f946-160">string</span><span class="sxs-lookup"><span data-stu-id="5f946-160">String</span></span> |<span data-ttu-id="5f946-161">Да</span><span class="sxs-lookup"><span data-stu-id="5f946-161">Yes</span></span> |
| <span data-ttu-id="5f946-162">key</span><span class="sxs-lookup"><span data-stu-id="5f946-162">key</span></span> |<span data-ttu-id="5f946-163">Ключ объекта S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-163">The S3 object key.</span></span> |<span data-ttu-id="5f946-164">string</span><span class="sxs-lookup"><span data-stu-id="5f946-164">String</span></span> |<span data-ttu-id="5f946-165">Нет</span><span class="sxs-lookup"><span data-stu-id="5f946-165">No</span></span> |
| <span data-ttu-id="5f946-166">prefix</span><span class="sxs-lookup"><span data-stu-id="5f946-166">prefix</span></span> |<span data-ttu-id="5f946-167">Префикс для ключа объекта S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="5f946-168">Выбираются объекты, ключи которых начинаются с этого префикса.</span><span class="sxs-lookup"><span data-stu-id="5f946-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="5f946-169">Применяется, только если ключ пустой.</span><span class="sxs-lookup"><span data-stu-id="5f946-169">Applies only when key is empty.</span></span> |<span data-ttu-id="5f946-170">string</span><span class="sxs-lookup"><span data-stu-id="5f946-170">String</span></span> |<span data-ttu-id="5f946-171">Нет</span><span class="sxs-lookup"><span data-stu-id="5f946-171">No</span></span> |
| <span data-ttu-id="5f946-172">версия</span><span class="sxs-lookup"><span data-stu-id="5f946-172">version</span></span> |<span data-ttu-id="5f946-173">Версия объекта S3, если включено управление версиями S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="5f946-174">string</span><span class="sxs-lookup"><span data-stu-id="5f946-174">String</span></span> |<span data-ttu-id="5f946-175">Нет</span><span class="sxs-lookup"><span data-stu-id="5f946-175">No</span></span> |
| <span data-ttu-id="5f946-176">свойства</span><span class="sxs-lookup"><span data-stu-id="5f946-176">format</span></span> | <span data-ttu-id="5f946-177">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="5f946-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="5f946-178">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="5f946-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="5f946-179">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате JSON](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="5f946-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="5f946-180">Если требуется скопировать файлы между файловыми хранилищами как есть (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="5f946-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="5f946-181">Нет</span><span class="sxs-lookup"><span data-stu-id="5f946-181">No</span></span> | |
| <span data-ttu-id="5f946-182">compression</span><span class="sxs-lookup"><span data-stu-id="5f946-182">compression</span></span> | <span data-ttu-id="5f946-183">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="5f946-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="5f946-184">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="5f946-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="5f946-185">Поддерживаемые уровни: **Optimal** (Оптимальный) и **Fastest** (Самый быстрый).</span><span class="sxs-lookup"><span data-stu-id="5f946-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="5f946-186">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="5f946-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="5f946-187">Нет</span><span class="sxs-lookup"><span data-stu-id="5f946-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="5f946-188">**Свойства bucketName и key** указывают расположение объекта S3, где контейнер — это корневой контейнер для объектов S3, а ключ — полный путь к объекту S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="5f946-189">Пример набора данных с префиксом</span><span class="sxs-lookup"><span data-stu-id="5f946-189">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="5f946-190">Пример набора данных (с версией)</span><span class="sxs-lookup"><span data-stu-id="5f946-190">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="5f946-191">Динамические пути для S3</span><span class="sxs-lookup"><span data-stu-id="5f946-191">Dynamic paths for S3</span></span>
<span data-ttu-id="5f946-192">В предыдущем примере используются фиксированные значения для свойств **key** и **bucketName** в наборе данных Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="5f946-193">Можно настроить фабрику данных для динамического вычисления значений этих свойств во время выполнения с помощью системных переменных, например SliceStart.</span><span class="sxs-lookup"><span data-stu-id="5f946-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="5f946-194">То же самое можно сделать и для свойства **prefix** набора данных Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="5f946-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="5f946-195">Список поддерживаемых функций и переменных см. в статье [Функции и системные переменные фабрики данных](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="5f946-196">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="5f946-196">Copy activity properties</span></span>
<span data-ttu-id="5f946-197">Полный список разделов и свойств, доступных для определения действий, см. в разделе [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="5f946-198">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="5f946-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="5f946-199">Свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="5f946-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="5f946-200">Для действия копирования свойства различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="5f946-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="5f946-201">Когда источник действия копирования имеет тип **FileSystemSource** (который включает в себя Amazon S3), в разделе **typeProperties** доступно приведенное ниже свойство.</span><span class="sxs-lookup"><span data-stu-id="5f946-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="5f946-202">Свойство</span><span class="sxs-lookup"><span data-stu-id="5f946-202">Property</span></span> | <span data-ttu-id="5f946-203">Описание</span><span class="sxs-lookup"><span data-stu-id="5f946-203">Description</span></span> | <span data-ttu-id="5f946-204">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="5f946-204">Allowed values</span></span> | <span data-ttu-id="5f946-205">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5f946-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5f946-206">recursive</span><span class="sxs-lookup"><span data-stu-id="5f946-206">recursive</span></span> |<span data-ttu-id="5f946-207">Указывает, следует ли отображать рекурсивный список объектов S3 в каталоге.</span><span class="sxs-lookup"><span data-stu-id="5f946-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="5f946-208">True или false</span><span class="sxs-lookup"><span data-stu-id="5f946-208">true/false</span></span> |<span data-ttu-id="5f946-209">Нет</span><span class="sxs-lookup"><span data-stu-id="5f946-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="5f946-210">Пример JSON. Копирование данных из Amazon S3 в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="5f946-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="5f946-211">В этом примере показано, как скопировать данные из Amazon S3 в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5f946-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="5f946-212">Тем не менее данные можно копировать непосредственно в [любой из поддерживаемых приемников](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Для этого применяется действие копирования в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="5f946-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="5f946-213">Пример содержит определения JSON для следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="5f946-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="5f946-214">Используя эти определения, вы можете создать конвейер для копирования данных из Amazon S3 в хранилище BLOB-объектов с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="5f946-215">Связанная служба типа [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5f946-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="5f946-216">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5f946-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5f946-217">Входной [набор данных](data-factory-create-datasets.md) типа [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5f946-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="5f946-218">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5f946-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5f946-219">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5f946-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5f946-220">В этом примере данные из Amazon S3 каждый час копируются в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="5f946-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="5f946-221">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="5f946-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="5f946-222">Связанная служба Amazon S3</span><span class="sxs-lookup"><span data-stu-id="5f946-222">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="5f946-223">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="5f946-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="5f946-224">Входной набор данных Amazon S3</span><span class="sxs-lookup"><span data-stu-id="5f946-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="5f946-225">Если параметру **external** присвоить значение true, то фабрика данных воспримет этот набор данных как внешний.</span><span class="sxs-lookup"><span data-stu-id="5f946-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="5f946-226">Присвойте значение true этому параметру входного набора данных, который не является результатом какого-либо действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="5f946-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="5f946-227">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="5f946-227">Azure Blob output dataset</span></span>

<span data-ttu-id="5f946-228">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="5f946-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5f946-229">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="5f946-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="5f946-230">В пути к папке используются год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="5f946-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="5f946-231">Действие копирования в конвейере с Amazon S3 в качестве источника и BLOB-объектом в качестве приемника</span><span class="sxs-lookup"><span data-stu-id="5f946-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="5f946-232">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="5f946-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="5f946-233">В определении JSON конвейера для типа **source** установлено значение **FileSystemSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5f946-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="5f946-234">Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в статье [Сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5f946-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f946-235">Next steps</span></span>
<span data-ttu-id="5f946-236">Ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="5f946-236">See the following articles:</span></span>

* <span data-ttu-id="5f946-237">Сведения о ключевых факторах, влияющих на производительность перемещения данных (действие копирования) в фабрике данных, и различных способах оптимизации этого процесса см. в [руководстве по настройке производительности действия копирования](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="5f946-238">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="5f946-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
