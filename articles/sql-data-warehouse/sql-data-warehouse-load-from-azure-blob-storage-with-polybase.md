---
title: "aaaLoad из хранилища данных BLOB-объектов Azure tooAzure | Документы Microsoft"
description: "Узнайте, как данные tooload toouse PolyBase из Azure хранилище больших двоичных объектов в хранилище данных SQL. Загрузить несколько таблиц из открытых данных в схему хранилища данных Contoso Retail hello."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="df370-104">Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="df370-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="df370-105">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="df370-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="df370-106">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="df370-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="df370-107">Используйте T-SQL и PolyBase команды tooload данных из хранилища BLOB-объектов Azure в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df370-107">Use PolyBase and T-SQL commands tooload data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="df370-108">tookeep простой, этот учебник загружает две таблицы из открытых больших двоичных объектов Azure хранилища в схему хранилища данных Contoso Retail hello.</span><span class="sxs-lookup"><span data-stu-id="df370-108">tookeep it simple, this tutorial loads two tables from a public Azure Storage Blob into hello Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="df370-109">tooload hello полный набор данных, выполнить пример hello [нагрузки hello полный хранилища данных Contoso Retail] [ Load hello full Contoso Retail Data Warehouse] из репозитория hello образцы Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="df370-109">tooload hello full data set, run hello example [Load hello full Contoso Retail Data Warehouse][Load hello full Contoso Retail Data Warehouse] from hello Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="df370-110">Изучив данный учебник, вы научитесь:</span><span class="sxs-lookup"><span data-stu-id="df370-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="df370-111">Настройка PolyBase tooload из хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="df370-111">Configure PolyBase tooload from Azure blob storage</span></span>
2. <span data-ttu-id="df370-112">загружать общедоступные данные в базу данных;</span><span class="sxs-lookup"><span data-stu-id="df370-112">Load public data into your database</span></span>
3. <span data-ttu-id="df370-113">После завершения загрузки hello, выполните оптимизацию.</span><span class="sxs-lookup"><span data-stu-id="df370-113">Perform optimizations after hello load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="df370-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="df370-114">Before you begin</span></span>
<span data-ttu-id="df370-115">toorun этого учебника требуется учетная запись Azure уже есть база данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="df370-115">toorun this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="df370-116">Если у вас ее нет, ознакомьтесь с разделом [Создание хранилища данных SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="df370-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-hello-data-source"></a><span data-ttu-id="df370-117">1. Настройка источника данных hello</span><span class="sxs-lookup"><span data-stu-id="df370-117">1. Configure hello data source</span></span>
<span data-ttu-id="df370-118">PolyBase использует расположение hello toodefine внешние объекты T-SQL и атрибутов hello внешних данных.</span><span class="sxs-lookup"><span data-stu-id="df370-118">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="df370-119">определения внешних объектов Hello хранятся в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="df370-119">hello external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="df370-120">сами данные Hello сохраняется во внешнем файле.</span><span class="sxs-lookup"><span data-stu-id="df370-120">hello data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="df370-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="df370-121">1.1.</span></span> <span data-ttu-id="df370-122">Создание учетных данных</span><span class="sxs-lookup"><span data-stu-id="df370-122">Create a credential</span></span>
<span data-ttu-id="df370-123">**Пропустите этот шаг** при загрузке hello Contoso общих данных.</span><span class="sxs-lookup"><span data-stu-id="df370-123">**Skip this step** if you are loading hello Contoso public data.</span></span> <span data-ttu-id="df370-124">Так как оно уже доступен tooanyone общие данные о toohello безопасный доступ не требуется.</span><span class="sxs-lookup"><span data-stu-id="df370-124">You don't need secure access toohello public data since it is already accessible tooanyone.</span></span>

<span data-ttu-id="df370-125">**Не пропускайте этот шаг** , если вы используете этот учебник как шаблон для загрузки собственных данных.</span><span class="sxs-lookup"><span data-stu-id="df370-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="df370-126">tooaccess данных с помощью учетных данных, используйте hello после сценариев toocreate уровня базы данных учетных данных и затем использовать его при определении hello расположение источника данных hello.</span><span class="sxs-lookup"><span data-stu-id="df370-126">tooaccess data through a credential, use hello following script toocreate a database-scoped credential, and then use it when defining hello location of hello data source.</span></span>

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
```

<span data-ttu-id="df370-127">Пропустите toostep 2.</span><span class="sxs-lookup"><span data-stu-id="df370-127">Skip toostep 2.</span></span>

### <a name="12-create-hello-external-data-source"></a><span data-ttu-id="df370-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="df370-128">1.2.</span></span> <span data-ttu-id="df370-129">Создайте hello внешний источник данных</span><span class="sxs-lookup"><span data-stu-id="df370-129">Create hello external data source</span></span>
<span data-ttu-id="df370-130">Этот метод следует использовать [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] команды toostore hello расположение данных hello и hello тип данных.</span><span class="sxs-lookup"><span data-stu-id="df370-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="df370-131">При выборе toomake общедоступные контейнеры хранилища BLOB-объектов azure, помните, что владельцем данных hello вы будет взиматься плата за данных расходов на исходящие данные, когда данные покидают hello центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="df370-131">If you choose toomake your azure blob storage containers public, remember that as hello data owner you will be charged for data egress charges when data leaves hello data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="df370-132">2. Настройка формата данных</span><span class="sxs-lookup"><span data-stu-id="df370-132">2. Configure data format</span></span>
<span data-ttu-id="df370-133">Hello данные хранятся в текстовые файлы в хранилище больших двоичных объектов, и каждое поле отделяется с разделителем.</span><span class="sxs-lookup"><span data-stu-id="df370-133">hello data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="df370-134">Выполните этот [CREATE EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] команда toospecify hello формат данных hello в текстовых файлах hello.</span><span class="sxs-lookup"><span data-stu-id="df370-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command toospecify hello format of hello data in hello text files.</span></span> <span data-ttu-id="df370-135">несжатый Hello данных Contoso и с разделителями канала.</span><span class="sxs-lookup"><span data-stu-id="df370-135">hello Contoso data is uncompressed and pipe delimited.</span></span>

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-hello-external-tables"></a><span data-ttu-id="df370-136">3. Создание внешних таблиц hello</span><span class="sxs-lookup"><span data-stu-id="df370-136">3. Create hello external tables</span></span>
<span data-ttu-id="df370-137">Теперь, были выбраны hello данных источника и формат файла все готово toocreate hello внешних таблиц.</span><span class="sxs-lookup"><span data-stu-id="df370-137">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> 

### <a name="31-create-a-schema-for-hello-data"></a><span data-ttu-id="df370-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="df370-138">3.1.</span></span> <span data-ttu-id="df370-139">Создайте схему для данных hello.</span><span class="sxs-lookup"><span data-stu-id="df370-139">Create a schema for hello data.</span></span>
<span data-ttu-id="df370-140">toocreate hello toostore месте Contoso данных в базе данных, создать схему.</span><span class="sxs-lookup"><span data-stu-id="df370-140">toocreate a place toostore hello Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a><span data-ttu-id="df370-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="df370-141">3.2.</span></span> <span data-ttu-id="df370-142">Создание внешних таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="df370-142">Create hello external tables.</span></span>
<span data-ttu-id="df370-143">Запустите этот скрипт toocreate hello DimProduct и FactOnlineSales внешних таблиц.</span><span class="sxs-lookup"><span data-stu-id="df370-143">Run this script toocreate hello DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="df370-144">Все, что мы здесь делаем определения имен столбцов и типов данных и привязывая их toohello расположение и формат файлов хранилища BLOB-объектов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="df370-144">All we are doing here is defining column names and data types, and binding them toohello location and format of hello Azure blob storage files.</span></span> <span data-ttu-id="df370-145">Определение Hello хранится в хранилище данных SQL и hello данных по-прежнему hello BLOB-объекта хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="df370-145">hello definition is stored in SQL Data Warehouse and hello data is still in hello Azure Storage Blob.</span></span>

<span data-ttu-id="df370-146">Hello **РАСПОЛОЖЕНИЕ** параметр является hello папку в корневой папке hello в hello BLOB-объекта хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="df370-146">hello  **LOCATION** parameter is hello folder under hello root folder in hello Azure Storage Blob.</span></span> <span data-ttu-id="df370-147">Все таблицы находятся в разных папках.</span><span class="sxs-lookup"><span data-stu-id="df370-147">Each table is in a different folder.</span></span>

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-hello-data"></a><span data-ttu-id="df370-148">4. Загрузка данных hello</span><span class="sxs-lookup"><span data-stu-id="df370-148">4. Load hello data</span></span>
<span data-ttu-id="df370-149">Нет внешних данных tooaccess различными способами.</span><span class="sxs-lookup"><span data-stu-id="df370-149">There's different ways tooaccess external data.</span></span>  <span data-ttu-id="df370-150">Можно запрашивать данные непосредственно из внешней таблицы hello, загрузка данных hello в новые таблицы базы данных или добавлять таблицы tooexisting внешних данных.</span><span class="sxs-lookup"><span data-stu-id="df370-150">You can query data directly from hello external table, load hello data into new database tables, or add external data tooexisting database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="df370-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="df370-151">4.1.</span></span> <span data-ttu-id="df370-152">Создание схемы</span><span class="sxs-lookup"><span data-stu-id="df370-152">Create a new schema</span></span>
<span data-ttu-id="df370-153">Компонент CTAS создает новую таблицу с данными.</span><span class="sxs-lookup"><span data-stu-id="df370-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="df370-154">Во-первых создайте схему для данных contoso hello.</span><span class="sxs-lookup"><span data-stu-id="df370-154">First, create a schema for hello contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a><span data-ttu-id="df370-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="df370-155">4.2.</span></span> <span data-ttu-id="df370-156">Загрузка данных hello в новые таблицы</span><span class="sxs-lookup"><span data-stu-id="df370-156">Load hello data into new tables</span></span>
<span data-ttu-id="df370-157">хранилище больших двоичных объектов и сохраните его в таблице внутри базы данных, используйте hello tooload данные из Azure [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] инструкции.</span><span class="sxs-lookup"><span data-stu-id="df370-157">tooload data from Azure blob storage and save it in a table inside of your database, use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="df370-158">Загрузка с CTAS использует hello со строго типизированными внешних таблиц, у вас есть только created.tooload hello данных в новые таблицы, используйте один [CTAS] [ CTAS] инструкции на таблицу.</span><span class="sxs-lookup"><span data-stu-id="df370-158">Loading with CTAS leverages hello strongly typed external tables you have just created.tooload hello data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="df370-159">CTAS создает новую таблицу и заполняет ее hello результаты инструкции select.</span><span class="sxs-lookup"><span data-stu-id="df370-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="df370-160">CTAS определяет новые таблицы toohave hello hello же столбцы и типы данных, как инструкция select hello результаты hello.</span><span class="sxs-lookup"><span data-stu-id="df370-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="df370-161">При выборе всех столбцов hello из внешней таблицы hello новая таблица будет реплики hello столбцов и типов данных в hello внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="df370-161">If you select all hello columns from an external table, hello new table will be a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="df370-162">В этом примере создайте hello измерения и таблицы фактов hello качестве хэш-таблицы, распределенные.</span><span class="sxs-lookup"><span data-stu-id="df370-162">In this example, we create both hello dimension and hello fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a><span data-ttu-id="df370-163">4.3 отслеживания хода выполнения загрузки hello</span><span class="sxs-lookup"><span data-stu-id="df370-163">4.3 Track hello load progress</span></span>
<span data-ttu-id="df370-164">Вы можете отслеживать ход выполнения hello нагрузки с помощью динамических административных представлений (DMV).</span><span class="sxs-lookup"><span data-stu-id="df370-164">You can track hello progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="df370-165">5. Оптимизация сжатия columnstore</span><span class="sxs-lookup"><span data-stu-id="df370-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="df370-166">По умолчанию хранилище данных SQL хранит hello таблицы как кластеризованного индекса columnstore.</span><span class="sxs-lookup"><span data-stu-id="df370-166">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="df370-167">После завершения загрузки, некоторые из строк данных hello может не сжаты в hello columnstore.</span><span class="sxs-lookup"><span data-stu-id="df370-167">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="df370-168">Это может происходить по ряду причин.</span><span class="sxs-lookup"><span data-stu-id="df370-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="df370-169">toolearn более, в разделе [Управление индексами columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="df370-169">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="df370-170">toooptimize производительность запросов и сжатие columnstore после загрузки, перестройте индекс hello таблицы tooforce hello columnstore toocompress все строки hello.</span><span class="sxs-lookup"><span data-stu-id="df370-170">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="df370-171">Дополнительные сведения о поддержании индексов columnstore см. в разделе hello [Управление индексами columnstore] [ manage columnstore indexes] статьи.</span><span class="sxs-lookup"><span data-stu-id="df370-171">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="df370-172">6. Оптимизация статистики</span><span class="sxs-lookup"><span data-stu-id="df370-172">6. Optimize statistics</span></span>
<span data-ttu-id="df370-173">Это наиболее статистику по отдельным столбцам toocreate сразу после загрузки.</span><span class="sxs-lookup"><span data-stu-id="df370-173">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="df370-174">Существует несколько вариантов статистики.</span><span class="sxs-lookup"><span data-stu-id="df370-174">There are some choices for statistics.</span></span> <span data-ttu-id="df370-175">Например при создании статистики по отдельным столбцам в каждом столбце может занять toorebuild долго вся статистика hello.</span><span class="sxs-lookup"><span data-stu-id="df370-175">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="df370-176">Если известно, что некоторые столбцы не будут toobe в предикатах запросов, можно пропустить создание статистики для этих столбцов.</span><span class="sxs-lookup"><span data-stu-id="df370-176">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="df370-177">Если вы решите toocreate статистику по отдельным столбцам для каждого столбца в каждой таблице, можно использовать образец кода хранимой процедуры hello `prc_sqldw_create_stats` в hello [статистики] [ statistics] статьи.</span><span class="sxs-lookup"><span data-stu-id="df370-177">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="df370-178">Привет, следующий пример является хорошей отправной точкой для создания статистики.</span><span class="sxs-lookup"><span data-stu-id="df370-178">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="df370-179">Статистика по отдельным столбцам создается для каждого столбца в таблице измерения hello и на каждом соединяющийся столбец в таблицах фактов hello.</span><span class="sxs-lookup"><span data-stu-id="df370-179">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="df370-180">Всегда столбцами таблицы фактов для одного или нескольких столбцов статистики tooother можно добавить позднее.</span><span class="sxs-lookup"><span data-stu-id="df370-180">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a><span data-ttu-id="df370-181">Победа!</span><span class="sxs-lookup"><span data-stu-id="df370-181">Achievement unlocked!</span></span>
<span data-ttu-id="df370-182">Общедоступные данные успешно загружены в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="df370-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="df370-183">Отличная работа!</span><span class="sxs-lookup"><span data-stu-id="df370-183">Great job!</span></span>

<span data-ttu-id="df370-184">Теперь вы можете запустить запрос hello таблиц с помощью запросов hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="df370-184">You can now start querying hello tables using queries like hello following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="df370-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df370-185">Next steps</span></span>
<span data-ttu-id="df370-186">tooload hello полные хранилища данных Contoso Retail данные, используйте сценарий hello в дополнительные советы по разработке см. в разделе [Общие сведения о разработке хранилище данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="df370-186">tooload hello full Contoso Retail Data Warehouse data, use hello script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
