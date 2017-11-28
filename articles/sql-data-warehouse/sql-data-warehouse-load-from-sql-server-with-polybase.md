---
title: "aaaLoad данные из SQL Server в хранилище данных SQL Azure (PolyBase) | Документы Microsoft"
description: "Использует данные bcp tooexport tooflat файлов и SQL Server, хранилище больших двоичных объектов tooAzure данных tooimport AZCopy, PolyBase tooingest hello данных в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 860c86e0-90f7-492c-9a84-1bdd3d1735cd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1346fb016e0538a44426671bf4e29358cb24f7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="32ba5-103">Загрузка данных в хранилище данных SQL с помощью PolyBase</span><span class="sxs-lookup"><span data-stu-id="32ba5-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32ba5-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="32ba5-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="32ba5-105">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="32ba5-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="32ba5-106">bcp</span><span class="sxs-lookup"><span data-stu-id="32ba5-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="32ba5-107">В этом учебнике показано как tooload данных в хранилище данных SQL с помощью AzCopy и PolyBase.</span><span class="sxs-lookup"><span data-stu-id="32ba5-107">This tutorial shows how tooload data into SQL Data Warehouse by using AzCopy and PolyBase.</span></span> <span data-ttu-id="32ba5-108">Изучив руководство, вы будете знать:</span><span class="sxs-lookup"><span data-stu-id="32ba5-108">When finished, you will know how to:</span></span>

* <span data-ttu-id="32ba5-109">Использовать хранилище больших двоичных объектов tooAzure данных toocopy AzCopy</span><span class="sxs-lookup"><span data-stu-id="32ba5-109">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="32ba5-110">Создание объектов базы данных toodefine hello данных</span><span class="sxs-lookup"><span data-stu-id="32ba5-110">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="32ba5-111">Запускайте данных hello tooload запрос T-SQL</span><span class="sxs-lookup"><span data-stu-id="32ba5-111">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="32ba5-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="32ba5-112">Prerequisites</span></span>
<span data-ttu-id="32ba5-113">требуется toostep этого учебника</span><span class="sxs-lookup"><span data-stu-id="32ba5-113">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="32ba5-114">База данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="32ba5-114">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="32ba5-115">Учетная запись хранилища Azure типа Standard-LRS (локально избыточное хранилище уровня «Стандартный»), Standard-GRS (геоизбыточное хранилище уровня «Стандартный») или Standard-RAGRS (геоизбыточное хранилище с доступом для чтения уровня «Стандартный»).</span><span class="sxs-lookup"><span data-stu-id="32ba5-115">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="32ba5-116">Служебная программа командной строки AzCopy.</span><span class="sxs-lookup"><span data-stu-id="32ba5-116">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="32ba5-117">Загрузите и установите hello [последнюю версию AzCopy] [ latest version of AzCopy] который устанавливается вместе с hello инструментов хранилища Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="32ba5-117">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Средства хранилища Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="32ba5-119">Шаг 1: Добавьте хранилище больших двоичных объектов tooAzure образца данных</span><span class="sxs-lookup"><span data-stu-id="32ba5-119">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="32ba5-120">В данные о заказах tooload мы должны tooput некоторые демонстрационные данные в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="32ba5-120">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="32ba5-121">На этом шаге мы заполним демонстрационными данными большой двоичный объект хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="32ba5-121">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="32ba5-122">Более поздней версии мы будем использовать PolyBase tooload следующий образец данных в базу данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="32ba5-122">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="32ba5-123">О.</span><span class="sxs-lookup"><span data-stu-id="32ba5-123">A.</span></span> <span data-ttu-id="32ba5-124">Подготовка примера текстового файла</span><span class="sxs-lookup"><span data-stu-id="32ba5-124">Prepare a sample text file</span></span>
<span data-ttu-id="32ba5-125">tooprepare пример текстового файла:</span><span class="sxs-lookup"><span data-stu-id="32ba5-125">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="32ba5-126">Откройте Блокнот и скопируйте hello следующие строки данных в новый файл.</span><span class="sxs-lookup"><span data-stu-id="32ba5-126">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="32ba5-127">Сохранение этого локального каталога temp tooyour % temp%\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="32ba5-127">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="32ba5-128">B.</span><span class="sxs-lookup"><span data-stu-id="32ba5-128">B.</span></span> <span data-ttu-id="32ba5-129">Поиск адреса конечной точки службы BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="32ba5-129">Find your blob service endpoint</span></span>
<span data-ttu-id="32ba5-130">toofind конечной точки службы BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="32ba5-130">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="32ba5-131">Hello портала Azure выберите **Обзор** > **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="32ba5-131">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="32ba5-132">Выберите учетную запись хранилища hello, требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="32ba5-132">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="32ba5-133">В колонке hello учетной записи хранилища щелкните больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="32ba5-133">In hello Storage account blade, click Blobs</span></span>
   
    ![Выбор BLOB-объектов](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="32ba5-135">Сохраните URL-адрес конечной точки службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="32ba5-135">Save your blob service endpoint URL for later.</span></span>
   
    ![Конечная точка службы BLOB-объектов](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="32ba5-137">C.</span><span class="sxs-lookup"><span data-stu-id="32ba5-137">C.</span></span> <span data-ttu-id="32ba5-138">Поиск ключа к хранилищу данных Azure</span><span class="sxs-lookup"><span data-stu-id="32ba5-138">Find your Azure storage key</span></span>
<span data-ttu-id="32ba5-139">toofind ключа хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="32ba5-139">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="32ba5-140">Hello портал Azure, выберите **Обзор** > **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="32ba5-140">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="32ba5-141">Щелкните hello, требуется toouse учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="32ba5-141">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="32ba5-142">Выберите **Все параметры** > **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="32ba5-142">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="32ba5-143">Щелкните поле toocopy hello копирования, один из буфера обмена toohello ключи доступа.</span><span class="sxs-lookup"><span data-stu-id="32ba5-143">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Копирование ключа к хранилищу данных Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="32ba5-145">D.</span><span class="sxs-lookup"><span data-stu-id="32ba5-145">D.</span></span> <span data-ttu-id="32ba5-146">Скопируйте хранилища больших двоичных объектов tooAzure файла образца hello</span><span class="sxs-lookup"><span data-stu-id="32ba5-146">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="32ba5-147">toocopy tooAzure больших двоичных объектов хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="32ba5-147">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="32ba5-148">Откройте командную строку и изменении каталога установки AzCopy toohello каталоги.</span><span class="sxs-lookup"><span data-stu-id="32ba5-148">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="32ba5-149">Эта команда изменяет toohello каталог установки по умолчанию на клиенте Windows x 64.</span><span class="sxs-lookup"><span data-stu-id="32ba5-149">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="32ba5-150">Выполните следующие команды tooupload hello файл hello.</span><span class="sxs-lookup"><span data-stu-id="32ba5-150">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="32ba5-151">Укажите URL-адрес конечной точки службы BLOB-объектов вместо <blob service endpoint URL> и ключ учетной записи хранения Azure вместо <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="32ba5-151">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="32ba5-152">См. также [Приступая к работе с hello служебной программы командной строки AzCopy][latest version of AzCopy].</span><span class="sxs-lookup"><span data-stu-id="32ba5-152">See also [Getting Started with hello AzCopy Command-Line Utility][latest version of AzCopy].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="32ba5-153">E.</span><span class="sxs-lookup"><span data-stu-id="32ba5-153">E.</span></span> <span data-ttu-id="32ba5-154">Просмотр содержимого контейнера хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="32ba5-154">Explore your blob storage container</span></span>
<span data-ttu-id="32ba5-155">файл hello toosee загруженный tooblob хранилища:</span><span class="sxs-lookup"><span data-stu-id="32ba5-155">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="32ba5-156">Вы можете вернуться колонке службы tooyour больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="32ba5-156">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="32ba5-157">В разделе «Контейнеры» дважды щелкните **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="32ba5-157">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="32ba5-158">tooexplore данных tooyour hello контура, щелкните папку hello **datedimension** и вы увидите загруженный файл **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="32ba5-158">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="32ba5-159">Нажмите кнопку Свойства tooview **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="32ba5-159">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="32ba5-160">Обратите внимание, что в колонке свойства большого двоичного объекта hello, можно загрузить или удалить файл hello.</span><span class="sxs-lookup"><span data-stu-id="32ba5-160">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Просмотр хранилища BLOB-объектов Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="32ba5-162">Шаг 2: Создание внешней таблицы для hello образца данных</span><span class="sxs-lookup"><span data-stu-id="32ba5-162">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="32ba5-163">В этом разделе мы создать внешнюю таблицу, которая определяет hello образцов данных.</span><span class="sxs-lookup"><span data-stu-id="32ba5-163">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="32ba5-164">PolyBase использует внешние таблицы tooaccess данные в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="32ba5-164">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="32ba5-165">Поскольку hello данные не хранятся в хранилище данных SQL, PolyBase обрабатывает внешние данные toohello проверки подлинности с помощью учетных данных области базы данных.</span><span class="sxs-lookup"><span data-stu-id="32ba5-165">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="32ba5-166">пример Hello в этот шаг использует эти toocreate инструкций Transact-SQL внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="32ba5-166">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="32ba5-167">[Создайте главный ключ (Transact-SQL)] [ Create Master Key (Transact-SQL)] учетные данные области секрет hello tooencrypt базы данных.</span><span class="sxs-lookup"><span data-stu-id="32ba5-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="32ba5-168">[Создание базы данных учетных данных (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify сведения для проверки подлинности для вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="32ba5-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="32ba5-169">[Создание внешнего источника данных (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify hello расположение хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="32ba5-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="32ba5-170">[Создайте формат внешнего файла (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify hello формат данных.</span><span class="sxs-lookup"><span data-stu-id="32ba5-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="32ba5-171">[Создайте внешнюю таблицу (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify определение таблицы hello и расположение hello данных.</span><span class="sxs-lookup"><span data-stu-id="32ba5-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="32ba5-172">Выполните этот запрос к вашей базе данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="32ba5-172">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="32ba5-173">Оно создает внешнюю таблицу с именем DimDate2External в схеме dbo hello, которая указывает toohello DimDate2.txt образец данных в хранилище больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="32ba5-173">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="32ba5-174">В обозревателе объектов SQL Server в Visual Studio вы увидите формата внешнего файла hello, внешний источник данных и таблиц DimDate2External hello.</span><span class="sxs-lookup"><span data-stu-id="32ba5-174">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Просмотр внешней таблицы](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="32ba5-176">Шаг 3. Загрузка данных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="32ba5-176">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="32ba5-177">После создания hello внешней таблицы можно загрузить данные hello в новую таблицу или вставить его в существующую таблицу.</span><span class="sxs-lookup"><span data-stu-id="32ba5-177">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="32ba5-178">tooload hello данных в новую таблицу, выполнить hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] инструкции.</span><span class="sxs-lookup"><span data-stu-id="32ba5-178">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="32ba5-179">Hello новая таблица будет иметь hello столбцы с именем в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="32ba5-179">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="32ba5-180">типы данных Hello hello столбцов будет соответствовать типам данных hello в определении внешней таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="32ba5-180">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="32ba5-181">tooload hello данных в существующую таблицу, используйте hello [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] инструкции.</span><span class="sxs-lookup"><span data-stu-id="32ba5-181">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="32ba5-182">Шаг 4. Создание статистики для только что загруженных данных</span><span class="sxs-lookup"><span data-stu-id="32ba5-182">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="32ba5-183">Хранилище данных SQL не создает и не обновляет статистику автоматически.</span><span class="sxs-lookup"><span data-stu-id="32ba5-183">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="32ba5-184">Таким образом tooachieve высокую производительность запросов, очень важно, сначала загрузите toocreate статистику для каждого столбца в каждой таблице после hello.</span><span class="sxs-lookup"><span data-stu-id="32ba5-184">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="32ba5-185">Это также важно tooupdate статистику после значительных изменений в данных hello.</span><span class="sxs-lookup"><span data-stu-id="32ba5-185">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="32ba5-186">Этот пример создает статистику по отдельным столбцам для новых таблиц DimDate2 hello.</span><span class="sxs-lookup"><span data-stu-id="32ba5-186">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="32ba5-187">toolearn более, в разделе [статистики][Statistics].</span><span class="sxs-lookup"><span data-stu-id="32ba5-187">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="32ba5-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32ba5-188">Next steps</span></span>
<span data-ttu-id="32ba5-189">В разделе hello [руководство по PolyBase] [ PolyBase guide] для получения дополнительных сведений, которые следует знать при разработке решения, использующего PolyBase.</span><span class="sxs-lookup"><span data-stu-id="32ba5-189">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
