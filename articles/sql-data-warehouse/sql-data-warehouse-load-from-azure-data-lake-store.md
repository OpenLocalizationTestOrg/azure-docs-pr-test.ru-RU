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
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="eebca-103">Загрузка данных из Azure Data Lake Store в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="eebca-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="eebca-104">В этом документе позволяет выбрать все действия, которые следует tooload данные из хранилища Озера Azure данных (ADLS) в хранилище данных SQL с помощью PolyBase.</span><span class="sxs-lookup"><span data-stu-id="eebca-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="eebca-105">При наличии возможности toorun нерегламентированные запросы к hello данным, хранящимся в ADLS, с помощью внешних таблиц hello рекомендуется рекомендуется Импорт hello в hello хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="eebca-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="eebca-106">Примерное время: 10 минут, при условии, что у вас есть необходимые компоненты hello должны toocomplete.</span><span class="sxs-lookup"><span data-stu-id="eebca-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="eebca-107">Из этого учебного курса вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="eebca-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="eebca-108">Создание объектов tooload внешней базы данных из хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="eebca-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="eebca-109">Подключите tooan каталог хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="eebca-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="eebca-110">Загрузка данных в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="eebca-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eebca-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="eebca-111">Before you begin</span></span>
<span data-ttu-id="eebca-112">toorun этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="eebca-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="eebca-113">Azure toouse приложение Active Directory для проверки подлинности службы для службы.</span><span class="sxs-lookup"><span data-stu-id="eebca-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="eebca-114">toocreate, выполните [проверки подлинности Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="eebca-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="eebca-115">Требуется идентификатор клиента hello, ключ и значение маркера конечной точки OAuth2.0 из вашего приложения Active Directory tooconnect tooyour Озера данных Azure из хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="eebca-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="eebca-116">Сведения, как tooget эти значения устанавливаются в hello ссылку выше.</span><span class="sxs-lookup"><span data-stu-id="eebca-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="eebca-117">Примечание для регистрации приложения Azure Active Directory служит hello «Идентификатор приложения» hello идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="eebca-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="eebca-118">SQL Server Management Studio или SQL Server Data Tools, toodownload SSMS и подключения см. в разделе [SSMS запроса](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="eebca-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="eebca-119">Хранилище данных SQL Azure, выполните один toocreate: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="eebca-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="eebca-120">Хранилище Azure Data Lake Store, в котором используется или не используется шифрование.</span><span class="sxs-lookup"><span data-stu-id="eebca-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="eebca-121">выполните один toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="eebca-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="eebca-122">Настройка источника данных hello</span><span class="sxs-lookup"><span data-stu-id="eebca-122">Configure hello data source</span></span>
<span data-ttu-id="eebca-123">PolyBase использует расположение hello toodefine внешние объекты T-SQL и атрибутов hello внешних данных.</span><span class="sxs-lookup"><span data-stu-id="eebca-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="eebca-124">Hello внешние объекты хранятся в хранилище данных SQL и ссылки hello данных th сохраняется во внешнем файле.</span><span class="sxs-lookup"><span data-stu-id="eebca-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="eebca-125">Создание учетных данных</span><span class="sxs-lookup"><span data-stu-id="eebca-125">Create a credential</span></span>
<span data-ttu-id="eebca-126">tooaccess хранения в Azure Озера данных, вы должны будете toocreate tooencrypt главного ключа базы данных на секретные учетные данные используются в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="eebca-127">Создайте учетные данные уровня базы данных, где хранятся hello основной учетные данные службы в AAD.</span><span class="sxs-lookup"><span data-stu-id="eebca-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="eebca-128">Для тех, кто использовали tooWindows tooconnect PolyBase BLOB-объектов хранилища Azure, обратите внимание, что hello учетных данных синтаксис отличается.</span><span class="sxs-lookup"><span data-stu-id="eebca-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="eebca-129">tooAzure tooconnect хранилища Озера данных, необходимо **первый** создать приложение Azure Active Directory, создайте ключ доступа и предоставьте ресурса Озера данных Azure toohello доступа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="eebca-130">Instrucitons tooperform эти шаги приведены [здесь](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="eebca-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

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


### <a name="create-hello-external-data-source"></a><span data-ttu-id="eebca-131">Создайте hello внешний источник данных</span><span class="sxs-lookup"><span data-stu-id="eebca-131">Create hello external data source</span></span>
<span data-ttu-id="eebca-132">Этот метод следует использовать [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] команды toostore hello расположение данных hello и hello тип данных.</span><span class="sxs-lookup"><span data-stu-id="eebca-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="eebca-133">Hello ADL URI можно найти в hello портал Azure и www.portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="eebca-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

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



## <a name="configure-data-format"></a><span data-ttu-id="eebca-134">Настройка формата данных</span><span class="sxs-lookup"><span data-stu-id="eebca-134">Configure data format</span></span>
<span data-ttu-id="eebca-135">данные hello tooimport из ADLS, необходимо формата внешнего файла toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="eebca-136">Эта команда имеет toodescribe параметры формата данных.</span><span class="sxs-lookup"><span data-stu-id="eebca-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="eebca-137">Ниже приведен пример распространенного формата — текстовый файл с разделителями "вертикальная черта".</span><span class="sxs-lookup"><span data-stu-id="eebca-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="eebca-138">В документации по T-SQL можно найти полный список форматов, доступных для команды [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="eebca-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

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

## <a name="create-hello-external-tables"></a><span data-ttu-id="eebca-139">Создание внешних таблиц hello</span><span class="sxs-lookup"><span data-stu-id="eebca-139">Create hello external tables</span></span>
<span data-ttu-id="eebca-140">Теперь, были выбраны hello данных источника и формат файла все готово toocreate hello внешних таблиц.</span><span class="sxs-lookup"><span data-stu-id="eebca-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="eebca-141">Внешние таблицы являются методом взаимодействия с внешними данными.</span><span class="sxs-lookup"><span data-stu-id="eebca-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="eebca-142">PolyBase использует tooread прохождения рекурсивной directory всех файлов во всех подкаталогах hello каталог, указанный в параметре расположение hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="eebca-143">Кроме того hello в следующем примере показано, как toocreate hello объекта.</span><span class="sxs-lookup"><span data-stu-id="eebca-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="eebca-144">Необходимо toowork инструкции hello toocustomize с данными hello вами ADLS.</span><span class="sxs-lookup"><span data-stu-id="eebca-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

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

## <a name="external-table-considerations"></a><span data-ttu-id="eebca-145">Рекомендации по внешним таблицам</span><span class="sxs-lookup"><span data-stu-id="eebca-145">External Table Considerations</span></span>
<span data-ttu-id="eebca-146">Создание внешней таблицы не представляет сложностей, но существуют некоторые особенности, требующие toobe описано.</span><span class="sxs-lookup"><span data-stu-id="eebca-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="eebca-147">Загрузка данных с помощью PolyBase строго типизирована.</span><span class="sxs-lookup"><span data-stu-id="eebca-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="eebca-148">Это означает, что каждая строка данных hello полученный должны удовлетворять hello определение схемы таблицы.</span><span class="sxs-lookup"><span data-stu-id="eebca-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="eebca-149">Если данная строка не соответствует определению схемы hello, строка hello отклоняется hello загрузки.</span><span class="sxs-lookup"><span data-stu-id="eebca-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="eebca-150">Hello REJECT_TYPE и REJECT_VALUE параметры позволяют toodefine количество строк или процент hello данных должны присутствовать в окончательной таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="eebca-151">Во время загрузки, при достижении hello отклоняемое значение hello загрузка завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="eebca-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="eebca-152">Наиболее распространенной причиной Hello отклоненных строк несоответствие определение схемы.</span><span class="sxs-lookup"><span data-stu-id="eebca-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="eebca-153">Например если столбец неправильно задан hello схемы типа int при hello данные в файле hello представляет собой строку, каждая строка завершится ошибкой tooload.</span><span class="sxs-lookup"><span data-stu-id="eebca-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="eebca-154">Hello расположение указывает hello верхний каталог, который вы хотите tooread данные из.</span><span class="sxs-lookup"><span data-stu-id="eebca-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="eebca-155">В этом случае при отсутствии вложенных /DimProduct/ PolyBase импорта всех данных hello в подкаталогах hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="eebca-156">Загрузка данных hello</span><span class="sxs-lookup"><span data-stu-id="eebca-156">Load hello data</span></span>
<span data-ttu-id="eebca-157">tooload данные из хранилища Озера данных Azure используйте hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] инструкции.</span><span class="sxs-lookup"><span data-stu-id="eebca-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="eebca-158">Загрузка с CTAS hello использует строго типизированными внешней таблицы, который был создан.</span><span class="sxs-lookup"><span data-stu-id="eebca-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="eebca-159">CTAS создает новую таблицу и заполняет ее hello результаты инструкции select.</span><span class="sxs-lookup"><span data-stu-id="eebca-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="eebca-160">CTAS определяет новые таблицы toohave hello hello же столбцы и типы данных, как инструкция select hello результаты hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="eebca-161">При выборе всех столбцов hello из внешней таблицы hello новая таблица является репликой hello столбцы и типы данных в таблице внешних hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="eebca-162">В нашем примере мы создаем распределенную хэш-таблицу с именем DimProduct на основе внешней таблицы DimProduct_external.</span><span class="sxs-lookup"><span data-stu-id="eebca-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="eebca-163">Оптимизация сжатия columnstore</span><span class="sxs-lookup"><span data-stu-id="eebca-163">Optimize columnstore compression</span></span>
<span data-ttu-id="eebca-164">По умолчанию хранилище данных SQL хранит hello таблицы как кластеризованного индекса columnstore.</span><span class="sxs-lookup"><span data-stu-id="eebca-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="eebca-165">После завершения загрузки, некоторые из строк данных hello может не сжаты в hello columnstore.</span><span class="sxs-lookup"><span data-stu-id="eebca-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="eebca-166">Это может происходить по ряду причин.</span><span class="sxs-lookup"><span data-stu-id="eebca-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="eebca-167">toolearn более, в разделе [Управление индексами columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="eebca-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="eebca-168">toooptimize производительность запросов и сжатие columnstore после загрузки, перестройте индекс hello таблицы tooforce hello columnstore toocompress все строки hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="eebca-169">Дополнительные сведения о поддержании индексов columnstore см. в разделе hello [Управление индексами columnstore] [ manage columnstore indexes] статьи.</span><span class="sxs-lookup"><span data-stu-id="eebca-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="eebca-170">Оптимизация статистики</span><span class="sxs-lookup"><span data-stu-id="eebca-170">Optimize statistics</span></span>
<span data-ttu-id="eebca-171">Это наиболее статистику по отдельным столбцам toocreate сразу после загрузки.</span><span class="sxs-lookup"><span data-stu-id="eebca-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="eebca-172">Существует несколько вариантов статистики.</span><span class="sxs-lookup"><span data-stu-id="eebca-172">There are some choices for statistics.</span></span> <span data-ttu-id="eebca-173">Например при создании статистики по отдельным столбцам в каждом столбце может занять toorebuild долго вся статистика hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="eebca-174">Если известно, что некоторые столбцы не будут toobe в предикатах запросов, можно пропустить создание статистики для этих столбцов.</span><span class="sxs-lookup"><span data-stu-id="eebca-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="eebca-175">Если вы решите toocreate статистику по отдельным столбцам для каждого столбца в каждой таблице, можно использовать образец кода хранимой процедуры hello `prc_sqldw_create_stats` в hello [статистики] [ statistics] статьи.</span><span class="sxs-lookup"><span data-stu-id="eebca-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="eebca-176">Привет, следующий пример является хорошей отправной точкой для создания статистики.</span><span class="sxs-lookup"><span data-stu-id="eebca-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="eebca-177">Статистика по отдельным столбцам создается для каждого столбца в таблице измерения hello и на каждом соединяющийся столбец в таблицах фактов hello.</span><span class="sxs-lookup"><span data-stu-id="eebca-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="eebca-178">Всегда столбцами таблицы фактов для одного или нескольких столбцов статистики tooother можно добавить позднее.</span><span class="sxs-lookup"><span data-stu-id="eebca-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="eebca-179">Победа!</span><span class="sxs-lookup"><span data-stu-id="eebca-179">Achievement unlocked!</span></span>
<span data-ttu-id="eebca-180">Данные успешно загружены в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="eebca-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="eebca-181">Отличная работа!</span><span class="sxs-lookup"><span data-stu-id="eebca-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="eebca-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eebca-182">Next Steps</span></span>
<span data-ttu-id="eebca-183">Загрузка данных — hello первый шаг toodeveloping решения хранилища данных с помощью хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="eebca-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="eebca-184">Ознакомьтесь с документацией для разработчиков, посвященной [таблицам](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) и [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="eebca-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
