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
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a>Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)
> [!div class="op_single_selector"]
> * [Фабрика данных](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase;](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

Используйте T-SQL и PolyBase команды tooload данных из хранилища BLOB-объектов Azure в хранилище данных SQL Azure. 

tookeep простой, этот учебник загружает две таблицы из открытых больших двоичных объектов Azure хранилища в схему хранилища данных Contoso Retail hello. tooload hello полный набор данных, выполнить пример hello [нагрузки hello полный хранилища данных Contoso Retail] [ Load hello full Contoso Retail Data Warehouse] из репозитория hello образцы Microsoft SQL Server.

Изучив данный учебник, вы научитесь:

1. Настройка PolyBase tooload из хранилища BLOB-объектов Azure
2. загружать общедоступные данные в базу данных;
3. После завершения загрузки hello, выполните оптимизацию.

## <a name="before-you-begin"></a>Перед началом работы
toorun этого учебника требуется учетная запись Azure уже есть база данных хранилища данных SQL. Если у вас ее нет, ознакомьтесь с разделом [Создание хранилища данных SQL][Create a SQL Data Warehouse].

## <a name="1-configure-hello-data-source"></a>1. Настройка источника данных hello
PolyBase использует расположение hello toodefine внешние объекты T-SQL и атрибутов hello внешних данных. определения внешних объектов Hello хранятся в хранилище данных SQL. сами данные Hello сохраняется во внешнем файле.

### <a name="11-create-a-credential"></a>1.1. Создание учетных данных
**Пропустите этот шаг** при загрузке hello Contoso общих данных. Так как оно уже доступен tooanyone общие данные о toohello безопасный доступ не требуется.

**Не пропускайте этот шаг** , если вы используете этот учебник как шаблон для загрузки собственных данных. tooaccess данных с помощью учетных данных, используйте hello после сценариев toocreate уровня базы данных учетных данных и затем использовать его при определении hello расположение источника данных hello.

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

Пропустите toostep 2.

### <a name="12-create-hello-external-data-source"></a>1.2. Создайте hello внешний источник данных
Этот метод следует использовать [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] команды toostore hello расположение данных hello и hello тип данных. 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> При выборе toomake общедоступные контейнеры хранилища BLOB-объектов azure, помните, что владельцем данных hello вы будет взиматься плата за данных расходов на исходящие данные, когда данные покидают hello центра обработки данных. 
> 
> 

## <a name="2-configure-data-format"></a>2. Настройка формата данных
Hello данные хранятся в текстовые файлы в хранилище больших двоичных объектов, и каждое поле отделяется с разделителем. Выполните этот [CREATE EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] команда toospecify hello формат данных hello в текстовых файлах hello. несжатый Hello данных Contoso и с разделителями канала.

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

## <a name="3-create-hello-external-tables"></a>3. Создание внешних таблиц hello
Теперь, были выбраны hello данных источника и формат файла все готово toocreate hello внешних таблиц. 

### <a name="31-create-a-schema-for-hello-data"></a>3.1. Создайте схему для данных hello.
toocreate hello toostore месте Contoso данных в базе данных, создать схему.

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a>3.2. Создание внешних таблиц hello.
Запустите этот скрипт toocreate hello DimProduct и FactOnlineSales внешних таблиц. Все, что мы здесь делаем определения имен столбцов и типов данных и привязывая их toohello расположение и формат файлов хранилища BLOB-объектов Azure hello. Определение Hello хранится в хранилище данных SQL и hello данных по-прежнему hello BLOB-объекта хранилища Azure.

Hello **РАСПОЛОЖЕНИЕ** параметр является hello папку в корневой папке hello в hello BLOB-объекта хранилища Azure. Все таблицы находятся в разных папках.

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

## <a name="4-load-hello-data"></a>4. Загрузка данных hello
Нет внешних данных tooaccess различными способами.  Можно запрашивать данные непосредственно из внешней таблицы hello, загрузка данных hello в новые таблицы базы данных или добавлять таблицы tooexisting внешних данных.  

### <a name="41-create-a-new-schema"></a>4.1. Создание схемы
Компонент CTAS создает новую таблицу с данными.  Во-первых создайте схему для данных contoso hello.

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a>4.2. Загрузка данных hello в новые таблицы
хранилище больших двоичных объектов и сохраните его в таблице внутри базы данных, используйте hello tooload данные из Azure [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] инструкции. Загрузка с CTAS использует hello со строго типизированными внешних таблиц, у вас есть только created.tooload hello данных в новые таблицы, используйте один [CTAS] [ CTAS] инструкции на таблицу. 
 
CTAS создает новую таблицу и заполняет ее hello результаты инструкции select. CTAS определяет новые таблицы toohave hello hello же столбцы и типы данных, как инструкция select hello результаты hello. При выборе всех столбцов hello из внешней таблицы hello новая таблица будет реплики hello столбцов и типов данных в hello внешней таблицы.

В этом примере создайте hello измерения и таблицы фактов hello качестве хэш-таблицы, распределенные. 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a>4.3 отслеживания хода выполнения загрузки hello
Вы можете отслеживать ход выполнения hello нагрузки с помощью динамических административных представлений (DMV). 

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

## <a name="5-optimize-columnstore-compression"></a>5. Оптимизация сжатия columnstore
По умолчанию хранилище данных SQL хранит hello таблицы как кластеризованного индекса columnstore. После завершения загрузки, некоторые из строк данных hello может не сжаты в hello columnstore.  Это может происходить по ряду причин. toolearn более, в разделе [Управление индексами columnstore][manage columnstore indexes].

toooptimize производительность запросов и сжатие columnstore после загрузки, перестройте индекс hello таблицы tooforce hello columnstore toocompress все строки hello. 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

Дополнительные сведения о поддержании индексов columnstore см. в разделе hello [Управление индексами columnstore] [ manage columnstore indexes] статьи.

## <a name="6-optimize-statistics"></a>6. Оптимизация статистики
Это наиболее статистику по отдельным столбцам toocreate сразу после загрузки. Существует несколько вариантов статистики. Например при создании статистики по отдельным столбцам в каждом столбце может занять toorebuild долго вся статистика hello. Если известно, что некоторые столбцы не будут toobe в предикатах запросов, можно пропустить создание статистики для этих столбцов.

Если вы решите toocreate статистику по отдельным столбцам для каждого столбца в каждой таблице, можно использовать образец кода хранимой процедуры hello `prc_sqldw_create_stats` в hello [статистики] [ statistics] статьи.

Привет, следующий пример является хорошей отправной точкой для создания статистики. Статистика по отдельным столбцам создается для каждого столбца в таблице измерения hello и на каждом соединяющийся столбец в таблицах фактов hello. Всегда столбцами таблицы фактов для одного или нескольких столбцов статистики tooother можно добавить позднее.

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

## <a name="achievement-unlocked"></a>Победа!
Общедоступные данные успешно загружены в хранилище данных SQL Azure. Отличная работа!

Теперь вы можете запустить запрос hello таблиц с помощью запросов hello следующим образом:

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a>Дальнейшие действия
tooload hello полные хранилища данных Contoso Retail данные, используйте сценарий hello в дополнительные советы по разработке см. в разделе [Общие сведения о разработке хранилище данных SQL][SQL Data Warehouse development overview].

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
