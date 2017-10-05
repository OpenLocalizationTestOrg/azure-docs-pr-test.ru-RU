---
title: "Загрузка данных из SQL Server в хранилище данных SQL Azure (PolyBase) | Документация Майкрософт"
description: "Экспорт данных из SQL Server в неструктурированные файлы, AZCopy, а также импорт данных в хранилище BLOB-объектов Azure и PolyBase для приема данных в хранилище данных SQL Azure с помощью программы bcp."
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
ms.openlocfilehash: 966100094f98bae41bf90df500d005fa78b31ec3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="006d9-103">Загрузка данных в хранилище данных SQL с помощью PolyBase</span><span class="sxs-lookup"><span data-stu-id="006d9-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="006d9-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="006d9-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="006d9-105">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="006d9-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="006d9-106">bcp</span><span class="sxs-lookup"><span data-stu-id="006d9-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="006d9-107">В этом руководстве показано, как загрузить данные в хранилище данных SQL с помощью AzCopy и PolyBase.</span><span class="sxs-lookup"><span data-stu-id="006d9-107">This tutorial shows how to load data into SQL Data Warehouse by using AzCopy and PolyBase.</span></span> <span data-ttu-id="006d9-108">Изучив руководство, вы будете знать:</span><span class="sxs-lookup"><span data-stu-id="006d9-108">When finished, you will know how to:</span></span>

* <span data-ttu-id="006d9-109">как использовать AzCopy для копирования данных в хранилище больших двоичных объектов;</span><span class="sxs-lookup"><span data-stu-id="006d9-109">Use AzCopy to copy data to Azure blob storage</span></span>
* <span data-ttu-id="006d9-110">как создавать объекты базы данных для определения данных;</span><span class="sxs-lookup"><span data-stu-id="006d9-110">Create database objects to define the data</span></span>
* <span data-ttu-id="006d9-111">как выполнять запросы T-SQL для загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="006d9-111">Run a T-SQL query to load the data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="006d9-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="006d9-112">Prerequisites</span></span>
<span data-ttu-id="006d9-113">Для выполнения этих действий необходимо иметь следующее.</span><span class="sxs-lookup"><span data-stu-id="006d9-113">To step through this tutorial, you need</span></span>

* <span data-ttu-id="006d9-114">База данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="006d9-114">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="006d9-115">Учетная запись хранилища Azure типа Standard-LRS (локально избыточное хранилище уровня «Стандартный»), Standard-GRS (геоизбыточное хранилище уровня «Стандартный») или Standard-RAGRS (геоизбыточное хранилище с доступом для чтения уровня «Стандартный»).</span><span class="sxs-lookup"><span data-stu-id="006d9-115">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="006d9-116">Служебная программа командной строки AzCopy.</span><span class="sxs-lookup"><span data-stu-id="006d9-116">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="006d9-117">Скачайте и установите [последнюю версию AzCopy][latest version of AzCopy], которая входит в состав средств службы хранилища Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="006d9-117">Download and install the [latest version of AzCopy][latest version of AzCopy] which is installed with the Microsoft Azure Storage Tools.</span></span>
  
    ![Средства хранилища Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-to-azure-blob-storage"></a><span data-ttu-id="006d9-119">Шаг 1. Добавление данных в хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="006d9-119">Step 1: Add sample data to Azure blob storage</span></span>
<span data-ttu-id="006d9-120">Чтобы загрузить данные, нам нужно сначала поместить демонстрационные данные в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="006d9-120">In order to load data, we need to put some sample data into an Azure blob storage.</span></span> <span data-ttu-id="006d9-121">На этом шаге мы заполним демонстрационными данными большой двоичный объект хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="006d9-121">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="006d9-122">Затем с помощью PolyBase мы загрузим эти данные в базу данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="006d9-122">Later, we will use PolyBase to load this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="006d9-123">О.</span><span class="sxs-lookup"><span data-stu-id="006d9-123">A.</span></span> <span data-ttu-id="006d9-124">Подготовка примера текстового файла</span><span class="sxs-lookup"><span data-stu-id="006d9-124">Prepare a sample text file</span></span>
<span data-ttu-id="006d9-125">Создайте пример текстового файла следующим образом.</span><span class="sxs-lookup"><span data-stu-id="006d9-125">To prepare a sample text file:</span></span>

1. <span data-ttu-id="006d9-126">Откройте Блокнот и скопируйте следующие строки данных в новый файл.</span><span class="sxs-lookup"><span data-stu-id="006d9-126">Open Notepad and copy the following lines of data into a new file.</span></span> <span data-ttu-id="006d9-127">Сохраните файл в локальный каталог с именем %temp%\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="006d9-127">Save this to your local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="006d9-128">B.</span><span class="sxs-lookup"><span data-stu-id="006d9-128">B.</span></span> <span data-ttu-id="006d9-129">Поиск адреса конечной точки службы BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="006d9-129">Find your blob service endpoint</span></span>
<span data-ttu-id="006d9-130">Найдите конечную точку службы BLOB-объектов следующим образом.</span><span class="sxs-lookup"><span data-stu-id="006d9-130">To find your blob service endpoint:</span></span>

1. <span data-ttu-id="006d9-131">На портале Azure выберите **Обзор** > **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="006d9-131">From the Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="006d9-132">Щелкните учетную запись хранения, которую хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="006d9-132">Click the storage account you want to use.</span></span>
3. <span data-ttu-id="006d9-133">В колонке учетной записи хранения выберите «BLOB-объекты».</span><span class="sxs-lookup"><span data-stu-id="006d9-133">In the Storage account blade, click Blobs</span></span>
   
    ![Выбор BLOB-объектов](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="006d9-135">Сохраните URL-адрес конечной точки службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="006d9-135">Save your blob service endpoint URL for later.</span></span>
   
    ![Конечная точка службы BLOB-объектов](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="006d9-137">C.</span><span class="sxs-lookup"><span data-stu-id="006d9-137">C.</span></span> <span data-ttu-id="006d9-138">Поиск ключа к хранилищу данных Azure</span><span class="sxs-lookup"><span data-stu-id="006d9-138">Find your Azure storage key</span></span>
<span data-ttu-id="006d9-139">Найдите ключ к хранилищу данных Azure следующим образом.</span><span class="sxs-lookup"><span data-stu-id="006d9-139">To find your Azure storage key:</span></span>

1. <span data-ttu-id="006d9-140">На портале Azure выберите **Обзор** > **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="006d9-140">From the Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="006d9-141">Щелкните учетную запись хранения, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="006d9-141">Click on the storage account you want to use.</span></span>
3. <span data-ttu-id="006d9-142">Выберите **Все параметры** > **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="006d9-142">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="006d9-143">Скопируйте один из ключей доступа в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="006d9-143">Click the copy box to copy one of your access keys to the clipboard.</span></span>
   
    ![Копирование ключа к хранилищу данных Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-the-sample-file-to-azure-blob-storage"></a><span data-ttu-id="006d9-145">D.</span><span class="sxs-lookup"><span data-stu-id="006d9-145">D.</span></span> <span data-ttu-id="006d9-146">Копирование примера файла в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="006d9-146">Copy the sample file to Azure blob storage</span></span>
<span data-ttu-id="006d9-147">Скопируйте сохраненные данные в хранилище BLOB-объектов Azure следующим образом.</span><span class="sxs-lookup"><span data-stu-id="006d9-147">To copy your data to Azure blob storage:</span></span>

1. <span data-ttu-id="006d9-148">Откройте командную строку и перейдите в каталог, в котором установлена программа AzCopy.</span><span class="sxs-lookup"><span data-stu-id="006d9-148">Open a command prompt, and change directories to the AzCopy installation directory.</span></span> <span data-ttu-id="006d9-149">Эта команда выполняет переход в каталог установки, который по умолчанию используется на 64-разрядной версии Windows.</span><span class="sxs-lookup"><span data-stu-id="006d9-149">This command changes to the default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="006d9-150">Выполните следующую команду, чтобы передать файл:</span><span class="sxs-lookup"><span data-stu-id="006d9-150">Run the following command to upload the file.</span></span> <span data-ttu-id="006d9-151">Укажите URL-адрес конечной точки службы BLOB-объектов вместо <blob service endpoint URL> и ключ учетной записи хранения Azure вместо <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="006d9-151">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="006d9-152">См. также статью [Приступая к работе со служебной программой командной строки AzCopy][latest version of AzCopy].</span><span class="sxs-lookup"><span data-stu-id="006d9-152">See also [Getting Started with the AzCopy Command-Line Utility][latest version of AzCopy].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="006d9-153">E.</span><span class="sxs-lookup"><span data-stu-id="006d9-153">E.</span></span> <span data-ttu-id="006d9-154">Просмотр содержимого контейнера хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="006d9-154">Explore your blob storage container</span></span>
<span data-ttu-id="006d9-155">Проверьте загрузку файла в хранилище BLOB-объектов следующим образом.</span><span class="sxs-lookup"><span data-stu-id="006d9-155">To see the file you uploaded to blob storage:</span></span>

1. <span data-ttu-id="006d9-156">Вернитесь к колонке службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="006d9-156">Go back to your Blob service blade.</span></span>
2. <span data-ttu-id="006d9-157">В разделе «Контейнеры» дважды щелкните **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="006d9-157">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="006d9-158">Щелкните папку **datedimension**, где хранятся ваши данные, и найдите там загруженный файл **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="006d9-158">To explore the path to your data, click the folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="006d9-159">Чтобы просмотреть его свойства, щелкните **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="006d9-159">To view properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="006d9-160">Обратите внимание, что в колонке свойств BLOB-объекта есть возможность загрузки и удаления файла.</span><span class="sxs-lookup"><span data-stu-id="006d9-160">Note that in the Blob properties blade, you can download or delete the file.</span></span>
   
    ![Просмотр хранилища BLOB-объектов Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-the-sample-data"></a><span data-ttu-id="006d9-162">Шаг 2. Создание внешней таблицы для демонстрационных данных</span><span class="sxs-lookup"><span data-stu-id="006d9-162">Step 2: Create an external table for the sample data</span></span>
<span data-ttu-id="006d9-163">В этом разделе мы создадим внешнюю таблицу, которая определяет демонстрационные данные.</span><span class="sxs-lookup"><span data-stu-id="006d9-163">In this section we create an external table that defines the sample data.</span></span>

<span data-ttu-id="006d9-164">PolyBase использует внешние таблицы для доступа к данным в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="006d9-164">PolyBase uses external tables to access data in Azure blob storage.</span></span> <span data-ttu-id="006d9-165">Поскольку данные хранятся не в хранилище данных SQL, PolyBase выполняет проверку подлинности для доступа к внешним данным с помощью учетных данных, заданных для базы данных.</span><span class="sxs-lookup"><span data-stu-id="006d9-165">Since the data is not stored within SQL Data Warehouse, PolyBase handles authentication to the external data by using a database-scoped credential.</span></span>

<span data-ttu-id="006d9-166">На этом шаге нашего примера мы выполним несколько инструкций Transact-SQL для создания внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="006d9-166">The example in this step uses these Transact-SQL statements to create an external table.</span></span>

* <span data-ttu-id="006d9-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)]: шифрование секрета учетных данных, заданных для базы данных.</span><span class="sxs-lookup"><span data-stu-id="006d9-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] to encrypt the secret of your database scoped credential.</span></span>
* <span data-ttu-id="006d9-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)]: предоставление сведений для аутентификации учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="006d9-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] to specify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="006d9-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)]: определение расположения хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="006d9-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] to specify the location of your Azure blob storage.</span></span>
* <span data-ttu-id="006d9-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)]: определение формата данных.</span><span class="sxs-lookup"><span data-stu-id="006d9-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] to specify the format of your data.</span></span>
* <span data-ttu-id="006d9-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)]: определение таблицы и расположения данных.</span><span class="sxs-lookup"><span data-stu-id="006d9-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] to specify the table definition and location of the data.</span></span>

<span data-ttu-id="006d9-172">Выполните этот запрос к вашей базе данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="006d9-172">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="006d9-173">В схеме dbo будет создана внешняя таблица с именем DimDate2External, которая указывает на файл с демонстрационными данными DimDate2.txt в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="006d9-173">It will create an external table named DimDate2External in the dbo schema that points to the DimDate2.txt sample data in the Azure blob storage.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

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


-- E: Create the external table
-- Specify column names and data types. This needs to match the data in the sample file.
-- LOCATION: Specify path to file or directory that contains the data (relative to the blob container).
-- To point to all files under the blob container, use LOCATION='.'

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


-- Run a query on the external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="006d9-174">В обозревателе объектов SQL Server в Visual Studio можно просмотреть формат внешнего файла, внешний источник данных и таблицу DimDate2External.</span><span class="sxs-lookup"><span data-stu-id="006d9-174">In SQL Server Object Explorer in Visual Studio, you can see the external file format, external data source, and the DimDate2External table.</span></span>

![Просмотр внешней таблицы](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="006d9-176">Шаг 3. Загрузка данных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="006d9-176">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="006d9-177">После создания внешней таблицы вы можете загрузить данные в новую таблицу или вставить в уже существующую.</span><span class="sxs-lookup"><span data-stu-id="006d9-177">Once the external table is created, you can either load the data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="006d9-178">Чтобы загрузить данные в новую таблицу, выполните инструкцию [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="006d9-178">To load the data into a new table, run the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="006d9-179">В новую таблицу будут включены столбцы с именами, указанными в запросе.</span><span class="sxs-lookup"><span data-stu-id="006d9-179">The new table will have the columns named in the query.</span></span> <span data-ttu-id="006d9-180">Типы данных столбцов будут соответствовать типам данных в определении внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="006d9-180">The data types of the columns will match the data types in the external table definition.</span></span>
* <span data-ttu-id="006d9-181">Чтобы загрузить данные в существующую таблицу, выполните инструкцию [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="006d9-181">To load the data into an existing table, use the [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load the data from Azure blob storage to SQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="006d9-182">Шаг 4. Создание статистики для только что загруженных данных</span><span class="sxs-lookup"><span data-stu-id="006d9-182">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="006d9-183">Хранилище данных SQL не создает и не обновляет статистику автоматически.</span><span class="sxs-lookup"><span data-stu-id="006d9-183">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="006d9-184">Поэтому после первой загрузки нужно создать статистику для каждого столбца каждой таблицы, чтобы обеспечить высокую производительность.</span><span class="sxs-lookup"><span data-stu-id="006d9-184">Therefore, to achieve high query performance, it's important to create statistics on each column of each table after the first load.</span></span> <span data-ttu-id="006d9-185">Также важно обновлять статистику после существенных изменений данных.</span><span class="sxs-lookup"><span data-stu-id="006d9-185">It's also important to update statistics after substantial changes in the data.</span></span>

<span data-ttu-id="006d9-186">Этот пример создает статистику по отдельным столбцам для новой таблицы DimDate2.</span><span class="sxs-lookup"><span data-stu-id="006d9-186">This example creates single-column statistics on the new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="006d9-187">Дополнительные сведения см. в статье [Управление статистикой таблиц в хранилище данных SQL][Statistics].</span><span class="sxs-lookup"><span data-stu-id="006d9-187">To learn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="006d9-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="006d9-188">Next steps</span></span>
<span data-ttu-id="006d9-189">При разработке решений на основе PolyBase будет полезно изучить [руководство по PolyBase][PolyBase guide].</span><span class="sxs-lookup"><span data-stu-id="006d9-189">See the [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

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
