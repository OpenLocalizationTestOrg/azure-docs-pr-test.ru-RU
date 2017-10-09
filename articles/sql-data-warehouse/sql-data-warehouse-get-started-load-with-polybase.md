---
title: "aaaPolyBase в учебнике хранилища данных SQL | Документы Microsoft"
description: "Сведения о возможностях PolyBase и как toouse его для сценариев хранилища данных."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a>Загрузка данных в хранилище данных SQL с помощью PolyBase
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Фабрика данных](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase;](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

В этом учебнике показано как tooload данных в хранилище данных SQL с помощью AzCopy и PolyBase. Изучив руководство, вы будете знать:

* Использовать хранилище больших двоичных объектов tooAzure данных toocopy AzCopy
* Создание объектов базы данных toodefine hello данных
* Запускайте данных hello tooload запрос T-SQL

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Предварительные требования
требуется toostep этого учебника

* База данных хранилища данных SQL.
* Учетная запись хранилища Azure типа Standard-LRS (локально избыточное хранилище уровня «Стандартный»), Standard-GRS (геоизбыточное хранилище уровня «Стандартный») или Standard-RAGRS (геоизбыточное хранилище с доступом для чтения уровня «Стандартный»).
* Служебная программа командной строки AzCopy. Загрузите и установите hello [последнюю версию AzCopy] [ latest version of AzCopy] который устанавливается вместе с hello инструментов хранилища Microsoft Azure.
  
    ![Средства хранилища Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a>Шаг 1: Добавьте хранилище больших двоичных объектов tooAzure образца данных
В данные о заказах tooload мы должны tooput некоторые демонстрационные данные в хранилище больших двоичных объектов. На этом шаге мы заполним демонстрационными данными большой двоичный объект хранилища Azure. Более поздней версии мы будем использовать PolyBase tooload следующий образец данных в базу данных хранилища данных SQL.

### <a name="a-prepare-a-sample-text-file"></a>О. Подготовка примера текстового файла
tooprepare пример текстового файла:

1. Откройте Блокнот и скопируйте hello следующие строки данных в новый файл. Сохранение этого локального каталога temp tooyour % temp%\DimDate2.txt.

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

### <a name="b-find-your-blob-service-endpoint"></a>B. Поиск адреса конечной точки службы BLOB-объектов
toofind конечной точки службы BLOB-объектов:

1. Hello портала Azure выберите **Обзор** > **учетные записи хранения**.
2. Выберите учетную запись хранилища hello, требуется toouse.
3. В колонке hello учетной записи хранилища щелкните больших двоичных объектов
   
    ![Выбор BLOB-объектов](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. Сохраните URL-адрес конечной точки службы BLOB-объектов.
   
    ![Конечная точка службы BLOB-объектов](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a>C. Поиск ключа к хранилищу данных Azure
toofind ключа хранилища Azure:

1. Hello портал Azure, выберите **Обзор** > **учетные записи хранения**.
2. Щелкните hello, требуется toouse учетной записи хранилища.
3. Выберите **Все параметры** > **Ключи доступа**.
4. Щелкните поле toocopy hello копирования, один из буфера обмена toohello ключи доступа.
   
    ![Копирование ключа к хранилищу данных Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a>D. Скопируйте хранилища больших двоичных объектов tooAzure файла образца hello
toocopy tooAzure больших двоичных объектов хранилища данных:

1. Откройте командную строку и изменении каталога установки AzCopy toohello каталоги. Эта команда изменяет toohello каталог установки по умолчанию на клиенте Windows x 64.
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. Выполните следующие команды tooupload hello файл hello. Укажите URL-адрес конечной точки службы BLOB-объектов вместо <blob service endpoint URL> и ключ учетной записи хранения Azure вместо <azure_storage_account_key>.
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

См. также [Приступая к работе с hello служебной программы командной строки AzCopy][Getting Started with hello AzCopy Command-Line Utility].

### <a name="e-explore-your-blob-storage-container"></a>E. Просмотр содержимого контейнера хранилища BLOB-объектов
файл hello toosee загруженный tooblob хранилища:

1. Вы можете вернуться колонке службы tooyour больших двоичных объектов.
2. В разделе «Контейнеры» дважды щелкните **datacontainer**.
3. tooexplore данных tooyour hello контура, щелкните папку hello **datedimension** и вы увидите загруженный файл **DimDate2.txt**.
4. Нажмите кнопку Свойства tooview **DimDate2.txt**.
5. Обратите внимание, что в колонке свойства большого двоичного объекта hello, можно загрузить или удалить файл hello.
   
    ![Просмотр хранилища BLOB-объектов Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a>Шаг 2: Создание внешней таблицы для hello образца данных
В этом разделе мы создать внешнюю таблицу, которая определяет hello образцов данных.

PolyBase использует внешние таблицы tooaccess данные в хранилище больших двоичных объектов. Поскольку hello данные не хранятся в хранилище данных SQL, PolyBase обрабатывает внешние данные toohello проверки подлинности с помощью учетных данных области базы данных.

пример Hello в этот шаг использует эти toocreate инструкций Transact-SQL внешней таблицы.

* [Создайте главный ключ (Transact-SQL)] [ Create Master Key (Transact-SQL)] учетные данные области секрет hello tooencrypt базы данных.
* [Создание базы данных учетных данных (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify сведения для проверки подлинности для вашей учетной записи хранилища Azure.
* [Создание внешнего источника данных (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify hello расположение хранилища BLOB-объектов Azure.
* [Создайте формат внешнего файла (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify hello формат данных.
* [Создайте внешнюю таблицу (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify определение таблицы hello и расположение hello данных.

Выполните этот запрос к вашей базе данных хранилища данных SQL. Оно создает внешнюю таблицу с именем DimDate2External в схеме dbo hello, которая указывает toohello DimDate2.txt образец данных в хранилище больших двоичных объектов hello.

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


В обозревателе объектов SQL Server в Visual Studio вы увидите формата внешнего файла hello, внешний источник данных и таблиц DimDate2External hello.

![Просмотр внешней таблицы](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a>Шаг 3. Загрузка данных в хранилище данных SQL
После создания hello внешней таблицы можно загрузить данные hello в новую таблицу или вставить его в существующую таблицу.

* tooload hello данных в новую таблицу, выполнить hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] инструкции. Hello новая таблица будет иметь hello столбцы с именем в запросе hello. типы данных Hello hello столбцов будет соответствовать типам данных hello в определении внешней таблицы hello.
* tooload hello данных в существующую таблицу, используйте hello [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] инструкции.

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

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Шаг 4. Создание статистики для только что загруженных данных
Хранилище данных SQL не создает и не обновляет статистику автоматически. Таким образом tooachieve высокую производительность запросов, очень важно, сначала загрузите toocreate статистику для каждого столбца в каждой таблице после hello. Это также важно tooupdate статистику после значительных изменений в данных hello.

Этот пример создает статистику по отдельным столбцам для новых таблиц DimDate2 hello.

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

toolearn более, в разделе [статистики][Statistics].  

## <a name="next-steps"></a>Дальнейшие действия
В разделе hello [руководство по PolyBase] [ PolyBase guide] для получения дополнительных сведений, которые следует знать при разработке решения, использующего PolyBase.

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
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
