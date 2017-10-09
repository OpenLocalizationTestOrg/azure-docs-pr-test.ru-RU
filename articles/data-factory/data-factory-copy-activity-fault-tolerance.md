---
title: "aaaAdd устойчивость к сбоям в действии копирования фабрики данных Azure, пропустив несовместимые строк | Документы Microsoft"
description: "Узнайте, как tooadd отказоустойчивость в действии копирования фабрики данных Azure, пропустив несовместимые строк во время копирования"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="20b83-103">Обеспечение отказоустойчивости для действия копирования с помощью пропуска несовместимых строк</span><span class="sxs-lookup"><span data-stu-id="20b83-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="20b83-104">Фабрика данных Azure [действие копирования](data-factory-data-movement-activities.md) предлагает два способа toohandle несовместимые строк при копировании данных между хранилищами данных источника и приемника:</span><span class="sxs-lookup"><span data-stu-id="20b83-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="20b83-105">Можно прервать и сбой копирования hello действии при несовместимые данные произошла (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="20b83-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="20b83-106">Вы можете продолжить toocopy все данные hello, добавив отказоустойчивость и пропуск несовместимые данные строк.</span><span class="sxs-lookup"><span data-stu-id="20b83-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="20b83-107">Кроме того вы можете войти hello несовместимые строк хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="20b83-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="20b83-108">Затем можно проверить hello журнала toolearn hello причину hello, исправить hello данные в источнике данных hello и повторите действие копирования hello.</span><span class="sxs-lookup"><span data-stu-id="20b83-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="20b83-109">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="20b83-109">Supported scenarios</span></span>
<span data-ttu-id="20b83-110">Действие копирования поддерживает три сценария для обработки несовместимых данных: обнаружение, пропуск и запись в журнал.</span><span class="sxs-lookup"><span data-stu-id="20b83-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="20b83-111">**Несовместимость hello исходного типа данных и собственный тип приемника hello**</span><span class="sxs-lookup"><span data-stu-id="20b83-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="20b83-112">Например: копирование данных из CSV-файла в tooa хранилища больших двоичных объектов SQL базы данных с помощью определения схемы, содержащий три **INT** столбцов типа.</span><span class="sxs-lookup"><span data-stu-id="20b83-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="20b83-113">Здравствуйте строк файла CSV, содержащих числовые данные, такие как `123,456,789` успешно скопированы toohello приемника хранилища.</span><span class="sxs-lookup"><span data-stu-id="20b83-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="20b83-114">Однако hello строки, которые содержат нечисловые значения, такие как `123,456,abc` определяются как несовместимые и пропускаются.</span><span class="sxs-lookup"><span data-stu-id="20b83-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="20b83-115">**Несоответствие числа hello столбцы между hello источника и приемника hello**</span><span class="sxs-lookup"><span data-stu-id="20b83-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="20b83-116">Например: копирование данных из CSV-файла в tooa хранилища больших двоичных объектов SQL базы данных с помощью определения схемы, который содержит шесть столбцов.</span><span class="sxs-lookup"><span data-stu-id="20b83-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="20b83-117">Hello CSV-файла, строки, содержащие шесть столбцов будут успешно скопированы toohello приемника хранилища.</span><span class="sxs-lookup"><span data-stu-id="20b83-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="20b83-118">Hello CSV файла строк, содержащих столбцы более или менее шести определяются как несовместимый и пропускаются.</span><span class="sxs-lookup"><span data-stu-id="20b83-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="20b83-119">**Нарушения первичного ключа при написании tooa реляционной базы данных**</span><span class="sxs-lookup"><span data-stu-id="20b83-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="20b83-120">Например: копирование данных из базы данных SQL tooa SQL server.</span><span class="sxs-lookup"><span data-stu-id="20b83-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="20b83-121">Определен первичный ключ в базе данных SQL приемник hello, но такой первичный ключ определен в hello исходному серверу SQL server.</span><span class="sxs-lookup"><span data-stu-id="20b83-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="20b83-122">Hello повторяющиеся строки, которые существуют в источнике hello не может быть скопированный toohello приемника.</span><span class="sxs-lookup"><span data-stu-id="20b83-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="20b83-123">Действие копирования копирует только hello первая строка hello источника данных в приемник hello.</span><span class="sxs-lookup"><span data-stu-id="20b83-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="20b83-124">Hello последующие исходные строки, содержащие hello повторяющиеся значения первичного ключа определяются как несовместимый и пропускаются.</span><span class="sxs-lookup"><span data-stu-id="20b83-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="20b83-125">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="20b83-125">Configuration</span></span>
<span data-ttu-id="20b83-126">Hello следующий пример возвращает tooconfigure определение JSON, пропуск hello несовместимые строк в действии копирования:</span><span class="sxs-lookup"><span data-stu-id="20b83-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="20b83-127">Свойство</span><span class="sxs-lookup"><span data-stu-id="20b83-127">Property</span></span> | <span data-ttu-id="20b83-128">Описание</span><span class="sxs-lookup"><span data-stu-id="20b83-128">Description</span></span> | <span data-ttu-id="20b83-129">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="20b83-129">Allowed values</span></span> | <span data-ttu-id="20b83-130">Обязательно</span><span class="sxs-lookup"><span data-stu-id="20b83-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="20b83-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="20b83-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="20b83-132">Включить или отключить пропуск несовместимых строк во время копирования.</span><span class="sxs-lookup"><span data-stu-id="20b83-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="20b83-133">Да</span><span class="sxs-lookup"><span data-stu-id="20b83-133">True</span></span><br/><span data-ttu-id="20b83-134">False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="20b83-134">False (default)</span></span> | <span data-ttu-id="20b83-135">Нет</span><span class="sxs-lookup"><span data-stu-id="20b83-135">No</span></span> |
| <span data-ttu-id="20b83-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="20b83-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="20b83-137">Группа свойств, которые могут быть указан при необходимости toolog hello несовместимые строк.</span><span class="sxs-lookup"><span data-stu-id="20b83-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="20b83-138">Нет</span><span class="sxs-lookup"><span data-stu-id="20b83-138">No</span></span> |
| <span data-ttu-id="20b83-139">**linkedServiceName (имя связанной службы)**</span><span class="sxs-lookup"><span data-stu-id="20b83-139">**linkedServiceName**</span></span> | <span data-ttu-id="20b83-140">Hello связанная служба хранилища Azure toostore hello журнала, содержащей hello пропущенных строк.</span><span class="sxs-lookup"><span data-stu-id="20b83-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="20b83-141">Имя Hello [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) или [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) связанной службы, который ссылается toohello экземпляра хранилища, что требуется файл журнала toouse toostore hello.</span><span class="sxs-lookup"><span data-stu-id="20b83-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="20b83-142">Нет</span><span class="sxs-lookup"><span data-stu-id="20b83-142">No</span></span> |
| <span data-ttu-id="20b83-143">**path**</span><span class="sxs-lookup"><span data-stu-id="20b83-143">**path**</span></span> | <span data-ttu-id="20b83-144">путь Hello hello файла журнала, содержащий hello пропущен строк.</span><span class="sxs-lookup"><span data-stu-id="20b83-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="20b83-145">Укажите путь к хранилищу больших двоичных объектов hello нужных toouse toolog hello несовместимые данные.</span><span class="sxs-lookup"><span data-stu-id="20b83-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="20b83-146">Если путь не предоставляется, hello службы создает контейнер.</span><span class="sxs-lookup"><span data-stu-id="20b83-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="20b83-147">Нет</span><span class="sxs-lookup"><span data-stu-id="20b83-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="20b83-148">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="20b83-148">Monitoring</span></span>
<span data-ttu-id="20b83-149">После завершения выполнения действия копирования hello видно hello количество пропущенных строк в hello мониторинга раздела:</span><span class="sxs-lookup"><span data-stu-id="20b83-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![Мониторинг пропущенных несовместимых строк](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="20b83-151">При настройке toolog hello несовместимые строк, можно найти файл журнала hello по этому пути: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` в файле журнала hello, вы можете просмотреть hello строк, которые были пропущены и hello основной причиной несовместимости hello.</span><span class="sxs-lookup"><span data-stu-id="20b83-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="20b83-152">Исходные данные hello и hello соответствующая ошибка записи в файл hello.</span><span class="sxs-lookup"><span data-stu-id="20b83-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="20b83-153">Ниже приведен пример содержимого файла журнала hello:</span><span class="sxs-lookup"><span data-stu-id="20b83-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="20b83-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20b83-154">Next steps</span></span>
<span data-ttu-id="20b83-155">toolearn Дополнительные сведения о действии копирования фабрики данных Azure, в разделе [перемещения данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="20b83-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
