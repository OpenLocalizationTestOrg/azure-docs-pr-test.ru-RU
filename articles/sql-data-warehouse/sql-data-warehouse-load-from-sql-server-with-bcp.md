---
title: "aaaLoad данные из SQL Server в хранилище данных SQL Azure (bcp) | Документы Microsoft"
description: "Для данных небольшого объема использует bcp tooexport данные из файлов tooflat SQL Server и импортировать hello данные непосредственно в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="db299-103">Загрузка данных из SQL Server в хранилище данных SQL Azure (неструктурированные файлы)</span><span class="sxs-lookup"><span data-stu-id="db299-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db299-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="db299-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="db299-105">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="db299-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="db299-106">bcp</span><span class="sxs-lookup"><span data-stu-id="db299-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="db299-107">Для небольших наборов данных можно использовать данные tooexport программы командной строки bcp hello из SQL Server и затем загрузить его напрямую tooAzure хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="db299-107">For small data sets, you can use hello bcp command-line utility tooexport data from SQL Server and then load it directly tooAzure SQL Data Warehouse.</span></span>

<span data-ttu-id="db299-108">В этом руководстве описывается, как с помощью bcp выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="db299-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="db299-109">Экспортировать таблицу из из SQL Server с помощью команды bcp hello команды (или создайте простой образец файла)</span><span class="sxs-lookup"><span data-stu-id="db299-109">Export a table from from SQL Server by using hello bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="db299-110">Импорт таблицы hello из неструктурированного файла tooSQL хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="db299-110">Import hello table from a flat file tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="db299-111">Создание статистики для hello загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="db299-111">Create statistics on hello loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="db299-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="db299-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="db299-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="db299-113">Prerequisites</span></span>
<span data-ttu-id="db299-114">toostep изучения этого руководства требуется:</span><span class="sxs-lookup"><span data-stu-id="db299-114">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="db299-115">База данных хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="db299-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="db299-116">Программа командной строки bcp Hello установлен</span><span class="sxs-lookup"><span data-stu-id="db299-116">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="db299-117">Программа командной строки sqlcmd Hello установлен</span><span class="sxs-lookup"><span data-stu-id="db299-117">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="db299-118">Можно загрузить служебные программы bcp и sqlcmd hello hello [центра загрузки Майкрософт][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="db299-118">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="db299-119">Данные в формате ASCII или UTF-16</span><span class="sxs-lookup"><span data-stu-id="db299-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="db299-120">Если вы пытаетесь этот учебник с вашими собственными данными, данные требуют toouse hello ASCII или кодировку UTF-16, так как bcp поддерживает UTF-8.</span><span class="sxs-lookup"><span data-stu-id="db299-120">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="db299-121">PolyBase поддерживает UTF-8, но еще не поддерживает UTF-16.</span><span class="sxs-lookup"><span data-stu-id="db299-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="db299-122">Обратите внимание, что если требуется toocombine bcp с PolyBase вам потребуется hello данных tootransform tooUTF-8 после экспорта из SQL Server.</span><span class="sxs-lookup"><span data-stu-id="db299-122">Note that if you want toocombine bcp with PolyBase you will need tootransform hello data tooUTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="db299-123">1. Создание целевой таблицы</span><span class="sxs-lookup"><span data-stu-id="db299-123">1. Create a destination table</span></span>
<span data-ttu-id="db299-124">Определение таблицы в хранилище данных SQL, который будет hello целевой таблице для загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="db299-124">Define a table in SQL Data Warehouse that will be hello destination table for hello load.</span></span> <span data-ttu-id="db299-125">Hello столбцов в таблице hello должно соответствовать toohello данных в каждой строке файла данных.</span><span class="sxs-lookup"><span data-stu-id="db299-125">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="db299-126">toocreate таблицу, откройте командную строку и использовать hello toorun sqlcmd.exe следующую команду:</span><span class="sxs-lookup"><span data-stu-id="db299-126">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="db299-127">2. Создание файла источника данных</span><span class="sxs-lookup"><span data-stu-id="db299-127">2. Create a source data file</span></span>
<span data-ttu-id="db299-128">Откройте Блокнот и скопируйте hello следующие строки данных в новый текстовый файл и сохраните этот файл tooyour локальный временный каталог, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="db299-128">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="db299-129">Эти данные имеют формат ASCII.</span><span class="sxs-lookup"><span data-stu-id="db299-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="db299-130">(Необязательно) tooexport данные из базы данных SQL Server, откройте командную строку и запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="db299-130">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="db299-131">Замените значения TableName, ServerName, DatabaseName, Username и Password на собственные.</span><span class="sxs-lookup"><span data-stu-id="db299-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a><span data-ttu-id="db299-132">3. Загрузка данных hello</span><span class="sxs-lookup"><span data-stu-id="db299-132">3. Load hello data</span></span>
<span data-ttu-id="db299-133">tooload hello данных, откройте командную строку и запустите hello следующую команду, заменив своих собственных сведений значениями hello имя сервера, имя базы данных, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="db299-133">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="db299-134">Используйте эти данные hello tooverify команда была загружена неправильно</span><span class="sxs-lookup"><span data-stu-id="db299-134">Use this command tooverify hello data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="db299-135">Hello результаты должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db299-135">hello results should look like this:</span></span>

| <span data-ttu-id="db299-136">DateId</span><span class="sxs-lookup"><span data-stu-id="db299-136">DateId</span></span> | <span data-ttu-id="db299-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="db299-137">CalendarQuarter</span></span> | <span data-ttu-id="db299-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="db299-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db299-139">20150101</span><span class="sxs-lookup"><span data-stu-id="db299-139">20150101</span></span> |<span data-ttu-id="db299-140">1</span><span class="sxs-lookup"><span data-stu-id="db299-140">1</span></span> |<span data-ttu-id="db299-141">3</span><span class="sxs-lookup"><span data-stu-id="db299-141">3</span></span> |
| <span data-ttu-id="db299-142">20150201</span><span class="sxs-lookup"><span data-stu-id="db299-142">20150201</span></span> |<span data-ttu-id="db299-143">1</span><span class="sxs-lookup"><span data-stu-id="db299-143">1</span></span> |<span data-ttu-id="db299-144">3</span><span class="sxs-lookup"><span data-stu-id="db299-144">3</span></span> |
| <span data-ttu-id="db299-145">20150301</span><span class="sxs-lookup"><span data-stu-id="db299-145">20150301</span></span> |<span data-ttu-id="db299-146">1</span><span class="sxs-lookup"><span data-stu-id="db299-146">1</span></span> |<span data-ttu-id="db299-147">3</span><span class="sxs-lookup"><span data-stu-id="db299-147">3</span></span> |
| <span data-ttu-id="db299-148">20150401</span><span class="sxs-lookup"><span data-stu-id="db299-148">20150401</span></span> |<span data-ttu-id="db299-149">2</span><span class="sxs-lookup"><span data-stu-id="db299-149">2</span></span> |<span data-ttu-id="db299-150">4</span><span class="sxs-lookup"><span data-stu-id="db299-150">4</span></span> |
| <span data-ttu-id="db299-151">20150501</span><span class="sxs-lookup"><span data-stu-id="db299-151">20150501</span></span> |<span data-ttu-id="db299-152">2</span><span class="sxs-lookup"><span data-stu-id="db299-152">2</span></span> |<span data-ttu-id="db299-153">4</span><span class="sxs-lookup"><span data-stu-id="db299-153">4</span></span> |
| <span data-ttu-id="db299-154">20150601</span><span class="sxs-lookup"><span data-stu-id="db299-154">20150601</span></span> |<span data-ttu-id="db299-155">2</span><span class="sxs-lookup"><span data-stu-id="db299-155">2</span></span> |<span data-ttu-id="db299-156">4</span><span class="sxs-lookup"><span data-stu-id="db299-156">4</span></span> |
| <span data-ttu-id="db299-157">20150701</span><span class="sxs-lookup"><span data-stu-id="db299-157">20150701</span></span> |<span data-ttu-id="db299-158">3</span><span class="sxs-lookup"><span data-stu-id="db299-158">3</span></span> |<span data-ttu-id="db299-159">1</span><span class="sxs-lookup"><span data-stu-id="db299-159">1</span></span> |
| <span data-ttu-id="db299-160">20150801</span><span class="sxs-lookup"><span data-stu-id="db299-160">20150801</span></span> |<span data-ttu-id="db299-161">3</span><span class="sxs-lookup"><span data-stu-id="db299-161">3</span></span> |<span data-ttu-id="db299-162">1</span><span class="sxs-lookup"><span data-stu-id="db299-162">1</span></span> |
| <span data-ttu-id="db299-163">20150801</span><span class="sxs-lookup"><span data-stu-id="db299-163">20150801</span></span> |<span data-ttu-id="db299-164">3</span><span class="sxs-lookup"><span data-stu-id="db299-164">3</span></span> |<span data-ttu-id="db299-165">1</span><span class="sxs-lookup"><span data-stu-id="db299-165">1</span></span> |
| <span data-ttu-id="db299-166">20151001</span><span class="sxs-lookup"><span data-stu-id="db299-166">20151001</span></span> |<span data-ttu-id="db299-167">4</span><span class="sxs-lookup"><span data-stu-id="db299-167">4</span></span> |<span data-ttu-id="db299-168">2</span><span class="sxs-lookup"><span data-stu-id="db299-168">2</span></span> |
| <span data-ttu-id="db299-169">20151101</span><span class="sxs-lookup"><span data-stu-id="db299-169">20151101</span></span> |<span data-ttu-id="db299-170">4</span><span class="sxs-lookup"><span data-stu-id="db299-170">4</span></span> |<span data-ttu-id="db299-171">2</span><span class="sxs-lookup"><span data-stu-id="db299-171">2</span></span> |
| <span data-ttu-id="db299-172">20151201</span><span class="sxs-lookup"><span data-stu-id="db299-172">20151201</span></span> |<span data-ttu-id="db299-173">4</span><span class="sxs-lookup"><span data-stu-id="db299-173">4</span></span> |<span data-ttu-id="db299-174">2</span><span class="sxs-lookup"><span data-stu-id="db299-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="db299-175">4. Создание статистики</span><span class="sxs-lookup"><span data-stu-id="db299-175">4. Create statistics</span></span>
<span data-ttu-id="db299-176">Хранилище данных SQL пока не поддерживает автоматическое создание или автоматическое обновление статистики.</span><span class="sxs-lookup"><span data-stu-id="db299-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="db299-177">tooget hello наилучшую производительность запросов, является важным toocreate статистику для всех столбцов всех таблиц после первой загрузки hello или после любой значительных изменений в данных hello.</span><span class="sxs-lookup"><span data-stu-id="db299-177">tooget hello best query performance, it's important toocreate statistics on all columns of all tables after hello first load or after any substantial changes occur in hello data.</span></span> <span data-ttu-id="db299-178">Дополнительные сведения см. в статье об [управлении статистикой][Statistics].</span><span class="sxs-lookup"><span data-stu-id="db299-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="db299-179">Выполните следующие команды toocreate статистики для вновь загруженных таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="db299-179">Run hello following command toocreate statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="db299-180">5. Экспорт данных из хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="db299-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="db299-181">Для практики можно экспортировать данные hello, которая загружается обратно из хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="db299-181">For fun, you can export hello data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="db299-182">Команда tooexport Hello hello ровно то же, что экспорт из SQL Server.</span><span class="sxs-lookup"><span data-stu-id="db299-182">hello command tooexport is exactly hello same as exporting from SQL Server.</span></span>

<span data-ttu-id="db299-183">Однако есть различия в результатах hello.</span><span class="sxs-lookup"><span data-stu-id="db299-183">However, there is a difference in hello results.</span></span> <span data-ttu-id="db299-184">Поскольку данные hello хранятся в распределенные места в хранилище данных SQL, при экспорте данных каждый вычислительный узел записывает его данных toohello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="db299-184">Since hello data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data toohello output file.</span></span> <span data-ttu-id="db299-185">порядок Hello hello данные в выходной файл hello является вероятностью toobe отличается от порядка hello hello данных во входном файле hello.</span><span class="sxs-lookup"><span data-stu-id="db299-185">hello order of hello data in hello output file is likely toobe different than hello order of hello data in hello input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="db299-186">Экспорт таблицы и сравнение результатов экспорта</span><span class="sxs-lookup"><span data-stu-id="db299-186">Export a table and compare exported results</span></span>
<span data-ttu-id="db299-187">toosee hello экспортированных данных, откройте командную строку и выполните следующую команду, используя свои собственные параметры.</span><span class="sxs-lookup"><span data-stu-id="db299-187">toosee hello exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="db299-188">Имя сервера — имя hello Azure логического сервера SQL.</span><span class="sxs-lookup"><span data-stu-id="db299-188">ServerName is hello name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="db299-189">Вы можете проверить данные были правильно экспортированы путем открытия нового файла hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="db299-189">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="db299-190">Hello данные в файле hello должен соответствовать текст hello ниже, но скорее всего будут отсортированы в порядке, отличающемся:</span><span class="sxs-lookup"><span data-stu-id="db299-190">hello data in hello file should match hello text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-hello-results-of-a-query"></a><span data-ttu-id="db299-191">Экспорт hello результатов запроса</span><span class="sxs-lookup"><span data-stu-id="db299-191">Export hello results of a query</span></span>
<span data-ttu-id="db299-192">Можно использовать hello **queryout** функции bcp tooexport hello результатов запроса, вместо экспорта hello всей таблицы.</span><span class="sxs-lookup"><span data-stu-id="db299-192">You can use hello **queryout** function of bcp tooexport hello results of a query instead of exporting hello entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="db299-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="db299-193">Next steps</span></span>
<span data-ttu-id="db299-194">Общие сведения о загрузке см. в статье [Загрузка данных в хранилище данных SQL][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="db299-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="db299-195">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="db299-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="db299-196">Дополнительные сведения о создании таблицы в хранилище данных SQL см. в статьях, посвященных [таблицам в хранилище данных SQL][Table Overview] и [синтаксису инструкции CREATE TABLE][CREATE TABLE syntax].</span><span class="sxs-lookup"><span data-stu-id="db299-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
