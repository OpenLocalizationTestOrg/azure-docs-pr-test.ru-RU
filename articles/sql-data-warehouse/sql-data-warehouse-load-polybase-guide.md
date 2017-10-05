---
title: "Руководство по использованию PolyBase в хранилище данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="ea093-103">Руководство по использованию PolyBase в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="ea093-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="ea093-104">Это руководство содержит практические сведения об использовании PolyBase в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ea093-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="ea093-105">Инструкции по началу работы см. в руководстве [Загрузка данных в хранилище данных SQL с помощью PolyBase][Load data with PolyBase].</span><span class="sxs-lookup"><span data-stu-id="ea093-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="ea093-106">Ротация ключей хранилищ данных</span><span class="sxs-lookup"><span data-stu-id="ea093-106">Rotating storage keys</span></span>
<span data-ttu-id="ea093-107">Время от времени вам потребуется изменять ключи доступа к хранилищу больших двоичных объектов по соображениям безопасности.</span><span class="sxs-lookup"><span data-stu-id="ea093-107">From time to time you will want to change the access key to your blob storage for security reasons.</span></span>

<span data-ttu-id="ea093-108">Самым элегантным способом выполнить эту задачу является процесс, который называется "ротация ключей".</span><span class="sxs-lookup"><span data-stu-id="ea093-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span></span> <span data-ttu-id="ea093-109">Возможно, вы уже заметили, что для учетной записи хранения больших двоичных объектов имеется два ключа хранения.</span><span class="sxs-lookup"><span data-stu-id="ea093-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="ea093-110">Это необходимо для перехода</span><span class="sxs-lookup"><span data-stu-id="ea093-110">This is so that you can transition</span></span>

<span data-ttu-id="ea093-111">Ротация ключей учетной записи хранения Azure представляет собой простой процесс из трех шагов</span><span class="sxs-lookup"><span data-stu-id="ea093-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="ea093-112">Создайте второй набор учетных данных на уровне базы данных на основе вторичного ключа доступа к хранилищу</span><span class="sxs-lookup"><span data-stu-id="ea093-112">Create second database scoped credential based on the secondary storage access key</span></span>
2. <span data-ttu-id="ea093-113">Создайте второй внешний источник данных, основанных на этих учетных данных</span><span class="sxs-lookup"><span data-stu-id="ea093-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="ea093-114">Удалите и создайте внешнюю таблицу или таблицы, указывающие на только что созданный внешний источник данных</span><span class="sxs-lookup"><span data-stu-id="ea093-114">Drop and create the external table(s) pointing to the new external data source</span></span>

<span data-ttu-id="ea093-115">После переноса всех внешних таблиц во внешний источник данных вы можете выполнить задачи очистки.</span><span class="sxs-lookup"><span data-stu-id="ea093-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span></span>

1. <span data-ttu-id="ea093-116">Удалите первый внешний источник данных</span><span class="sxs-lookup"><span data-stu-id="ea093-116">Drop first external data source</span></span>
2. <span data-ttu-id="ea093-117">Удалите первые учетные данные, собранные в базе данных, основанные на основном ключе доступа к хранилищу</span><span class="sxs-lookup"><span data-stu-id="ea093-117">Drop first database scoped credential based on the primary storage access key</span></span>
3. <span data-ttu-id="ea093-118">Выполните вход в Azure и снова создайте основной ключ доступа хранилища, который будет готов к следующему переходу</span><span class="sxs-lookup"><span data-stu-id="ea093-118">Log into Azure and regenerate the primary access key ready for the next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="ea093-119">Отправка запроса для данных хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="ea093-119">Query Azure blob storage data</span></span>
<span data-ttu-id="ea093-120">Запросы к внешним таблицам используют имя таблицы так, как будто это реляционная таблица.</span><span class="sxs-lookup"><span data-stu-id="ea093-120">Queries against external tables simply use the table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="ea093-121">Запрос к внешней таблице может завершиться с ошибкой *«Запрос прерван — достигнуто максимальное число отклонений при чтении из внешнего источника»*.</span><span class="sxs-lookup"><span data-stu-id="ea093-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="ea093-122">Это означает, что внешние данные содержат *«грязные»* записи.</span><span class="sxs-lookup"><span data-stu-id="ea093-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="ea093-123">Запись данных считается "грязной", если фактические типы данных и количество столбцов не соответствуют определениям столбцов из внешней таблицы или если данные не соответствуют указанному формату внешнего файла.</span><span class="sxs-lookup"><span data-stu-id="ea093-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span></span> <span data-ttu-id="ea093-124">Чтобы устранить эту проблему, убедитесь в правильности определений внешней таблицы и формата внешнего файла, а также в том, что внешние данные соответствуют этим определениям.</span><span class="sxs-lookup"><span data-stu-id="ea093-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span></span> <span data-ttu-id="ea093-125">Если подмножество записей внешних данных "грязные", можно отклонить эти записи для запросов с помощью параметров отклонения в CREATE EXTERNAL TABLE DDL.</span><span class="sxs-lookup"><span data-stu-id="ea093-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="ea093-126">Загрузка данных из хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="ea093-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="ea093-127">В этом примере данные загружаются из хранилища больших двоичных объектов Azure в базу данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ea093-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span></span>

<span data-ttu-id="ea093-128">Прямое хранение данных сокращает время переноса данных для запроса.</span><span class="sxs-lookup"><span data-stu-id="ea093-128">Storing data directly removes the data transfer time for queries.</span></span> <span data-ttu-id="ea093-129">Хранение данных с индексом columnstore повышает производительность аналитических запросов до 10 раз.</span><span class="sxs-lookup"><span data-stu-id="ea093-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span></span>

<span data-ttu-id="ea093-130">В этом примере для загрузки данных используется инструкция CREATE TABLE AS SELECT.</span><span class="sxs-lookup"><span data-stu-id="ea093-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span></span> <span data-ttu-id="ea093-131">Новая таблица наследует столбцы с именами, указанные в запросе.</span><span class="sxs-lookup"><span data-stu-id="ea093-131">The new table inherits the columns named in the query.</span></span> <span data-ttu-id="ea093-132">Таблица наследует типы данных столбцов из определения внешней таблицы.</span><span class="sxs-lookup"><span data-stu-id="ea093-132">It inherits the data types of those columns from the external table definition.</span></span>

<span data-ttu-id="ea093-133">CREATE TABLE AS SELECT — это высокопроизводительная инструкция Transact-SQL, которая загружает данные одновременно во все вычислительные узлы вашего хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ea093-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="ea093-134">Изначально указания были разработаны для подсистемы вычислений с массовым параллелизмом (MPP) в Analytics Platform System и теперь используются в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ea093-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

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

<span data-ttu-id="ea093-135">Ознакомьтесь с разделом [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="ea093-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="ea093-136">Создание статистики для вновь загруженных данных</span><span class="sxs-lookup"><span data-stu-id="ea093-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="ea093-137">Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.</span><span class="sxs-lookup"><span data-stu-id="ea093-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="ea093-138">Чтобы добиться максимально высокой производительности запросов, крайне важно сформировать статистические данные для всех столбцов всех таблиц после первой загрузки или после любых значительных изменений в данных.</span><span class="sxs-lookup"><span data-stu-id="ea093-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="ea093-139">Подробные сведения о работе со статистикой см. в статье [Управление статистикой таблиц в хранилище данных SQL][Statistics].</span><span class="sxs-lookup"><span data-stu-id="ea093-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>  <span data-ttu-id="ea093-140">Ниже приведен краткий пример создания статистики по табличным данным, загруженным в этом примере.</span><span class="sxs-lookup"><span data-stu-id="ea093-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a><span data-ttu-id="ea093-141">Экспорт данных в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="ea093-141">Export data to Azure blob storage</span></span>
<span data-ttu-id="ea093-142">В этом разделе рассказывается, как экспортировать данные из хранилища данных SQL в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ea093-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span></span> <span data-ttu-id="ea093-143">В этом примере для экспорта данных в параллельном режиме из всех вычислительных узлов используется высокопроизводительная инструкция Transact-SQL CREATE EXTERNAL TABLE AS SELECT.</span><span class="sxs-lookup"><span data-stu-id="ea093-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span></span>

<span data-ttu-id="ea093-144">В следующем примере создается внешняя таблица Weblogs2014 с помощью определений столбцов и данных из таблицы dbo.Weblogs.</span><span class="sxs-lookup"><span data-stu-id="ea093-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="ea093-145">Определение внешней таблицы хранится в хранилище данных SQL, а результаты инструкции SELECT экспортируются в каталог /archive/log2014/ контейнера BLOB-объектов, указанного в источнике данных.</span><span class="sxs-lookup"><span data-stu-id="ea093-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span></span> <span data-ttu-id="ea093-146">Данные экспортируются в указанном текстовом формате.</span><span class="sxs-lookup"><span data-stu-id="ea093-146">The data is exported in the specified text file format.</span></span>

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
## <a name="isolate-loading-users"></a><span data-ttu-id="ea093-147">Ограничение возможности загрузки для пользователей</span><span class="sxs-lookup"><span data-stu-id="ea093-147">Isolate Loading Users</span></span>
<span data-ttu-id="ea093-148">Зачастую необходимо иметь несколько пользователей, которые могут загрузить данные в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ea093-148">There is often a need to have multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="ea093-149">Так как для использования инструкции [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] требуются разрешения на управление базой данных, в результате у вас будет несколько пользователей с контролем доступа во всех схемах.</span><span class="sxs-lookup"><span data-stu-id="ea093-149">Because the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of the database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="ea093-150">Чтобы ограничить это, можно использовать инструкцию DENY CONTROL.</span><span class="sxs-lookup"><span data-stu-id="ea093-150">To limit this, you can use the DENY CONTROL statement.</span></span>

<span data-ttu-id="ea093-151">Пример. Рассмотрим схемы базы данных schema_A для отдела A и schema_B для отдела B. Задайте пользователей базы данных user_A и user_B в качестве пользователей для загрузки PolyBase в отделе A и B соответственно.</span><span class="sxs-lookup"><span data-stu-id="ea093-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="ea093-152">Им обоим предоставлены разрешения CONTROL для базы данных.</span><span class="sxs-lookup"><span data-stu-id="ea093-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="ea093-153">Теперь создатели схем A и B блокируют свои схемы, используя инструкцию DENY:</span><span class="sxs-lookup"><span data-stu-id="ea093-153">The creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 <span data-ttu-id="ea093-154">Таким образом для user_A и user_B теперь должен быть заблокирован доступ к схеме другого отдела.</span><span class="sxs-lookup"><span data-stu-id="ea093-154">With this, user_A and user_B should now be locked out from the other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="ea093-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ea093-155">Next steps</span></span>
<span data-ttu-id="ea093-156">Дополнительные сведения о перемещении данных в хранилище данных SQL см. в статье [Перенос решения в хранилище данных SQL][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="ea093-156">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span></span>

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
