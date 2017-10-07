---
title: "aaaGuide по использованию PolyBase в хранилище данных SQL | Документы Microsoft"
description: "Правила и рекомендации по использованию PolyBase в сценариях с хранилищем данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="6b0f1-103">Руководство по использованию PolyBase в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="6b0f1-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="6b0f1-104">Это руководство содержит практические сведения об использовании PolyBase в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="6b0f1-105">tooget работы см. в разделе hello [загрузки данных с помощью PolyBase] [ Load data with PolyBase] учебника.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-105">tooget started, see hello [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="6b0f1-106">Ротация ключей хранилищ данных</span><span class="sxs-lookup"><span data-stu-id="6b0f1-106">Rotating storage keys</span></span>
<span data-ttu-id="6b0f1-107">Из tootime времени требуется хранилище больших двоичных объектов tooyour ключа доступа hello toochange по соображениям безопасности.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-107">From time tootime you will want toochange hello access key tooyour blob storage for security reasons.</span></span>

<span data-ttu-id="6b0f1-108">Здравствуйте, элегантный tooperform способом, эта задача является toofollow процесса, известного как «смена ключей hello».</span><span class="sxs-lookup"><span data-stu-id="6b0f1-108">hello most elegant way tooperform this task is toofollow a process known as "rotating hello keys".</span></span> <span data-ttu-id="6b0f1-109">Возможно, вы уже заметили, что для учетной записи хранения больших двоичных объектов имеется два ключа хранения.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="6b0f1-110">Это необходимо для перехода</span><span class="sxs-lookup"><span data-stu-id="6b0f1-110">This is so that you can transition</span></span>

<span data-ttu-id="6b0f1-111">Ротация ключей учетной записи хранения Azure представляет собой простой процесс из трех шагов</span><span class="sxs-lookup"><span data-stu-id="6b0f1-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="6b0f1-112">Создайте второй учетные данные уровня базы данных, на основе ключа доступа к дополнительному хранилищу hello</span><span class="sxs-lookup"><span data-stu-id="6b0f1-112">Create second database scoped credential based on hello secondary storage access key</span></span>
2. <span data-ttu-id="6b0f1-113">Создайте второй внешний источник данных, основанных на этих учетных данных</span><span class="sxs-lookup"><span data-stu-id="6b0f1-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="6b0f1-114">Удалите и создайте hello внешних таблиц, указывающий toohello новый внешний источник данных</span><span class="sxs-lookup"><span data-stu-id="6b0f1-114">Drop and create hello external table(s) pointing toohello new external data source</span></span>

<span data-ttu-id="6b0f1-115">Если вы перенесли все внешние таблицы toohello новый внешний источник данных можно выполнять hello Очистка задачи:</span><span class="sxs-lookup"><span data-stu-id="6b0f1-115">When you have migrated all your external tables toohello new external data source then you can perform hello clean up tasks:</span></span>

1. <span data-ttu-id="6b0f1-116">Удалите первый внешний источник данных</span><span class="sxs-lookup"><span data-stu-id="6b0f1-116">Drop first external data source</span></span>
2. <span data-ttu-id="6b0f1-117">Области DROP первой базы данных на основе ключа доступа hello основного хранилища учетных данных</span><span class="sxs-lookup"><span data-stu-id="6b0f1-117">Drop first database scoped credential based on hello primary storage access key</span></span>
3. <span data-ttu-id="6b0f1-118">Войдите в Azure и выполните повторное формирование hello первичный ключ доступа к hello в следующий раз</span><span class="sxs-lookup"><span data-stu-id="6b0f1-118">Log into Azure and regenerate hello primary access key ready for hello next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="6b0f1-119">Отправка запроса для данных хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="6b0f1-119">Query Azure blob storage data</span></span>
<span data-ttu-id="6b0f1-120">Запросы к внешним таблицам просто использовать имя таблицы hello так, будто он был реляционной таблице.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-120">Queries against external tables simply use hello table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="6b0f1-121">Запрос на внешнюю таблицу может завершиться с ошибкой hello *«запрос прерван — Достигнуто пороговое значение отклонения максимальное hello при чтении из внешнего источника»*.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-121">A query on an external table can fail with hello error *"Query aborted-- hello maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="6b0f1-122">Это означает, что внешние данные содержат *«грязные»* записи.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="6b0f1-123">Запись данных считается «грязных», если hello фактические данные типы и количество столбцов не соответствуют определений столбцов hello hello внешней таблицы или hello данные не соответствуют toohello формат указанного внешнего файла.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-123">A data record is considered 'dirty' if hello actual data types/number of columns do not match hello column definitions of hello external table or if hello data doesn't conform toohello specified external file format.</span></span> <span data-ttu-id="6b0f1-124">toofix это, убедитесь, что ваш внешней таблицы и определения формата внешнего файла указаны правильно и определения toothese соответствует данных из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-124">toofix this, ensure that your external table and external file format definitions are correct and your external data conforms toothese definitions.</span></span> <span data-ttu-id="6b0f1-125">В случае подмножество записей внешние данные "грязные", вы можете tooreject эти записи для запросов с помощью параметров отклонить hello в CREATE DDL ВНЕШНЕЙ таблицы.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-125">In case a subset of external data records are dirty, you can choose tooreject these records for your queries by using hello reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="6b0f1-126">Загрузка данных из хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="6b0f1-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="6b0f1-127">В этом примере загружает данные из базы данных хранилища tooSQL хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-127">This example loads data from Azure blob storage tooSQL Data Warehouse database.</span></span>

<span data-ttu-id="6b0f1-128">Хранение данных непосредственно удаляет hello время передачи данных для запросов.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-128">Storing data directly removes hello data transfer time for queries.</span></span> <span data-ttu-id="6b0f1-129">Хранение данных с индексом columnstore повышает производительность запросов для анализа запросов путем копирования too10x.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-129">Storing data with a columnstore index improves query performance for analysis queries by up too10x.</span></span>

<span data-ttu-id="6b0f1-130">В этом примере данные tooload инструкции CREATE TABLE AS SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-130">This example uses hello CREATE TABLE AS SELECT statement tooload data.</span></span> <span data-ttu-id="6b0f1-131">Новая таблица Hello наследует hello столбцы с именем в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-131">hello new table inherits hello columns named in hello query.</span></span> <span data-ttu-id="6b0f1-132">Определение внешней таблицы hello наследование hello типы данных этих столбцов.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-132">It inherits hello data types of those columns from hello external table definition.</span></span>

<span data-ttu-id="6b0f1-133">CREATE TABLE AS SELECT является высокопроизводительных инструкции Transact-SQL, который загружает данные hello в параллельных tooall hello вычислительные узлы хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads hello data in parallel tooall hello compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="6b0f1-134">Оно было разработано для обработчика расширенной параллельной обработке (MPP) hello в Analytics Platform System и находится в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-134">It was originally developed for  hello massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="6b0f1-135">Ознакомьтесь с разделом [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="6b0f1-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="6b0f1-136">Создание статистики для вновь загруженных данных</span><span class="sxs-lookup"><span data-stu-id="6b0f1-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="6b0f1-137">Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="6b0f1-138">В порядке tooget hello наилучшей производительности запросов очень важно создать статистику для всех столбцов всех таблиц после первой загрузки hello или любые существенные изменения происходят в данных hello.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-138">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="6b0f1-139">Подробное описание статистики см. в разделе hello [статистики] [ Statistics] раздела hello разработка группы разделов.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-139">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>  <span data-ttu-id="6b0f1-140">Ниже приведен краткий пример порядка загрузки toocreate статистики по возвращающая hello в этом примере.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-140">Below is a quick example of how toocreate statistics on hello tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a><span data-ttu-id="6b0f1-141">Экспорт хранилища BLOB-объект данных tooAzure</span><span class="sxs-lookup"><span data-stu-id="6b0f1-141">Export data tooAzure blob storage</span></span>
<span data-ttu-id="6b0f1-142">В этом разделе показано, как tooexport данные из хранилища данных SQL tooAzure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-142">This section shows how tooexport data from SQL Data Warehouse tooAzure blob storage.</span></span> <span data-ttu-id="6b0f1-143">В этом примере используется CREATE EXTERNAL TABLE AS SELECT передаются высокой высокопроизводительных Transact-SQL инструкции tooexport hello данные в параллельном режиме из всех hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement tooexport hello data in parallel from all hello compute nodes.</span></span>

<span data-ttu-id="6b0f1-144">Hello пример создает внешнюю таблицу Weblogs2014 с помощью определения столбцов и данных из dbo. Таблица диалоги.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-144">hello following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="6b0f1-145">Определение внешней таблицы Hello хранится в хранилище данных SQL и hello результаты инструкции SELECT hello, экспортированный toohello каталог «/ архивировать/log2014 /» в указанный источником данных hello контейнер больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-145">hello external table definition is stored in SQL Data Warehouse and hello results of hello SELECT statement are exported toohello "/archive/log2014/" directory under hello blob container specified by hello data source.</span></span> <span data-ttu-id="6b0f1-146">Hello данные экспортируются в формате файла указанный текст hello.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-146">hello data is exported in hello specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="6b0f1-147">Ограничение возможности загрузки для пользователей</span><span class="sxs-lookup"><span data-stu-id="6b0f1-147">Isolate Loading Users</span></span>
<span data-ttu-id="6b0f1-148">Обычно имеется toohave необходимость нескольких пользователей, которые можно загружать данные в хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-148">There is often a need toohave multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="6b0f1-149">Поскольку hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] требуются разрешения УПРАВЛЕНИЯ hello базы данных, вы получите нескольких пользователей с помощью управления доступом по всем схемам.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-149">Because hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of hello database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="6b0f1-150">toolimit это, можно с помощью инструкции DENY УПРАВЛЕНИЯ hello.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-150">toolimit this, you can use hello DENY CONTROL statement.</span></span>

<span data-ttu-id="6b0f1-151">Пример. Рассмотрим схемы базы данных schema_A для отдела A и schema_B для отдела B. Задайте пользователей базы данных user_A и user_B в качестве пользователей для загрузки PolyBase в отделе A и B соответственно.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="6b0f1-152">Им обоим предоставлены разрешения CONTROL для базы данных.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="6b0f1-153">Создатели Hello схемы A и B теперь заблокировать их схем с помощью DENY:</span><span class="sxs-lookup"><span data-stu-id="6b0f1-153">hello creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 <span data-ttu-id="6b0f1-154">Таким образом, user_A и user_B должны теперь блокировке hello схемы других подразделений.</span><span class="sxs-lookup"><span data-stu-id="6b0f1-154">With this, user_A and user_B should now be locked out from hello other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="6b0f1-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b0f1-155">Next steps</span></span>
<span data-ttu-id="6b0f1-156">toolearn Дополнительные сведения о tooSQL перемещение данных хранилища данных. в разделе hello [Общие сведения о миграции данных][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="6b0f1-156">toolearn more about moving data tooSQL Data Warehouse, see hello [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
