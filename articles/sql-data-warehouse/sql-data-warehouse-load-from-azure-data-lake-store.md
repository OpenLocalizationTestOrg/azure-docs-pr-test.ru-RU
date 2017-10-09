---
title: "aaaLoad - tooSQL хранилища Озера данных Azure хранилища данных | Документы Microsoft"
description: "Узнайте, как toouse PolyBase внешние таблицы tooload данные из хранилища Озера данных Azure в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>Загрузка данных из Azure Data Lake Store в хранилище данных SQL
В этом документе позволяет выбрать все действия, которые следует tooload данные из хранилища Озера Azure данных (ADLS) в хранилище данных SQL с помощью PolyBase.
При наличии возможности toorun нерегламентированные запросы к hello данным, хранящимся в ADLS, с помощью внешних таблиц hello рекомендуется рекомендуется Импорт hello в hello хранилище данных SQL.
Примерное время: 10 минут, при условии, что у вас есть необходимые компоненты hello должны toocomplete.
Из этого учебного курса вы узнаете следующее:

1. Создание объектов tooload внешней базы данных из хранилища Озера данных Azure.
2. Подключите tooan каталог хранилища Озера данных Azure.
3. Загрузка данных в хранилище данных SQL Azure.

## <a name="before-you-begin"></a>Перед началом работы
toorun этого учебника, необходимо:

* Azure toouse приложение Active Directory для проверки подлинности службы для службы. toocreate, выполните [проверки подлинности Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> Требуется идентификатор клиента hello, ключ и значение маркера конечной точки OAuth2.0 из вашего приложения Active Directory tooconnect tooyour Озера данных Azure из хранилища данных SQL. Сведения, как tooget эти значения устанавливаются в hello ссылку выше.
>Примечание для регистрации приложения Azure Active Directory служит hello «Идентификатор приложения» hello идентификатор клиента.

* SQL Server Management Studio или SQL Server Data Tools, toodownload SSMS и подключения см. в разделе [SSMS запроса](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Хранилище данных SQL Azure, выполните один toocreate: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* Хранилище Azure Data Lake Store, в котором используется или не используется шифрование. выполните один toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Настройка источника данных hello
PolyBase использует расположение hello toodefine внешние объекты T-SQL и атрибутов hello внешних данных. Hello внешние объекты хранятся в хранилище данных SQL и ссылки hello данных th сохраняется во внешнем файле.


###  <a name="create-a-credential"></a>Создание учетных данных
tooaccess хранения в Azure Озера данных, вы должны будете toocreate tooencrypt главного ключа базы данных на секретные учетные данные используются в следующем шаге hello.
Создайте учетные данные уровня базы данных, где хранятся hello основной учетные данные службы в AAD. Для тех, кто использовали tooWindows tooconnect PolyBase BLOB-объектов хранилища Azure, обратите внимание, что hello учетных данных синтаксис отличается.
tooAzure tooconnect хранилища Озера данных, необходимо **первый** создать приложение Azure Active Directory, создайте ключ доступа и предоставьте ресурса Озера данных Azure toohello доступа приложения hello. Instrucitons tooperform эти шаги приведены [здесь](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a>Создайте hello внешний источник данных
Этот метод следует использовать [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] команды toostore hello расположение данных hello и hello тип данных.
Hello ADL URI можно найти в hello портал Azure и www.portal.azure.com.

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a>Настройка формата данных
данные hello tooimport из ADLS, необходимо формата внешнего файла toospecify hello. Эта команда имеет toodescribe параметры формата данных.
Ниже приведен пример распространенного формата — текстовый файл с разделителями "вертикальная черта".
В документации по T-SQL можно найти полный список форматов, доступных для команды [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

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

## <a name="create-hello-external-tables"></a>Создание внешних таблиц hello
Теперь, были выбраны hello данных источника и формат файла все готово toocreate hello внешних таблиц. Внешние таблицы являются методом взаимодействия с внешними данными. PolyBase использует tooread прохождения рекурсивной directory всех файлов во всех подкаталогах hello каталог, указанный в параметре расположение hello. Кроме того hello в следующем примере показано, как toocreate hello объекта. Необходимо toowork инструкции hello toocustomize с данными hello вами ADLS.

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a>Рекомендации по внешним таблицам
Создание внешней таблицы не представляет сложностей, но существуют некоторые особенности, требующие toobe описано.

Загрузка данных с помощью PolyBase строго типизирована. Это означает, что каждая строка данных hello полученный должны удовлетворять hello определение схемы таблицы.
Если данная строка не соответствует определению схемы hello, строка hello отклоняется hello загрузки.

Hello REJECT_TYPE и REJECT_VALUE параметры позволяют toodefine количество строк или процент hello данных должны присутствовать в окончательной таблицы hello.
Во время загрузки, при достижении hello отклоняемое значение hello загрузка завершится ошибкой. Наиболее распространенной причиной Hello отклоненных строк несоответствие определение схемы.
Например если столбец неправильно задан hello схемы типа int при hello данные в файле hello представляет собой строку, каждая строка завершится ошибкой tooload.

Hello расположение указывает hello верхний каталог, который вы хотите tooread данные из.
В этом случае при отсутствии вложенных /DimProduct/ PolyBase импорта всех данных hello в подкаталогах hello.

## <a name="load-hello-data"></a>Загрузка данных hello
tooload данные из хранилища Озера данных Azure используйте hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] инструкции. Загрузка с CTAS hello использует строго типизированными внешней таблицы, который был создан.

CTAS создает новую таблицу и заполняет ее hello результаты инструкции select. CTAS определяет новые таблицы toohave hello hello же столбцы и типы данных, как инструкция select hello результаты hello. При выборе всех столбцов hello из внешней таблицы hello новая таблица является репликой hello столбцы и типы данных в таблице внешних hello.

В нашем примере мы создаем распределенную хэш-таблицу с именем DimProduct на основе внешней таблицы DimProduct_external.

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>Оптимизация сжатия columnstore
По умолчанию хранилище данных SQL хранит hello таблицы как кластеризованного индекса columnstore. После завершения загрузки, некоторые из строк данных hello может не сжаты в hello columnstore.  Это может происходить по ряду причин. toolearn более, в разделе [Управление индексами columnstore][manage columnstore indexes].

toooptimize производительность запросов и сжатие columnstore после загрузки, перестройте индекс hello таблицы tooforce hello columnstore toocompress все строки hello.

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

Дополнительные сведения о поддержании индексов columnstore см. в разделе hello [Управление индексами columnstore] [ manage columnstore indexes] статьи.

## <a name="optimize-statistics"></a>Оптимизация статистики
Это наиболее статистику по отдельным столбцам toocreate сразу после загрузки. Существует несколько вариантов статистики. Например при создании статистики по отдельным столбцам в каждом столбце может занять toorebuild долго вся статистика hello. Если известно, что некоторые столбцы не будут toobe в предикатах запросов, можно пропустить создание статистики для этих столбцов.

Если вы решите toocreate статистику по отдельным столбцам для каждого столбца в каждой таблице, можно использовать образец кода хранимой процедуры hello `prc_sqldw_create_stats` в hello [статистики] [ statistics] статьи.

Привет, следующий пример является хорошей отправной точкой для создания статистики. Статистика по отдельным столбцам создается для каждого столбца в таблице измерения hello и на каждом соединяющийся столбец в таблицах фактов hello. Всегда столбцами таблицы фактов для одного или нескольких столбцов статистики tooother можно добавить позднее.


## <a name="achievement-unlocked"></a>Победа!
Данные успешно загружены в хранилище данных SQL Azure. Отличная работа!

##<a name="next-steps"></a>Дальнейшие действия
Загрузка данных — hello первый шаг toodeveloping решения хранилища данных с помощью хранилища данных SQL. Ознакомьтесь с документацией для разработчиков, посвященной [таблицам](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) и [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).


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
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
