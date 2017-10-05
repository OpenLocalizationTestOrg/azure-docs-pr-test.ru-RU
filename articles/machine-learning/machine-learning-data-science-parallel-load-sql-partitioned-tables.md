---
title: "Создание и оптимизация таблиц для быстрого параллельного импорта данных в SQL Server на виртуальной машине Azure | Документация Майкрософт"
description: "Параллельный массовый импорт данных с использованием таблиц секционирования SQL"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: aae4e4f59e76bf48b00a2ee92aedd7d5643ba91a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="82457-103">Параллельный массовый импорт данных с использованием таблиц секционирования SQL</span><span class="sxs-lookup"><span data-stu-id="82457-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="82457-104">В этом документе описывается создание секционированных таблиц для быстрого параллельного массового импорта данных в Базу данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="82457-104">This document describes how to build partitioned tables for fast parallel bulk importing of data to a SQL Server database.</span></span> <span data-ttu-id="82457-105">При загрузке и передаче больших данных в базу данных SQL с помощью *секционированных таблиц и представлений* можно оптимизировать импорт информации в эту базу, а также выполнение последующих запросов.</span><span class="sxs-lookup"><span data-stu-id="82457-105">For big data loading/transfer to a SQL database, importing data to the SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="82457-106">Создание новой базы данных и набора групп файлов</span><span class="sxs-lookup"><span data-stu-id="82457-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="82457-107">[Создайте базу данных](https://technet.microsoft.com/library/ms176061.aspx), если она еще не существует.</span><span class="sxs-lookup"><span data-stu-id="82457-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="82457-108">Добавьте группы файлов базы данных в базу данных, которая будет содержать секционированные физические файлы. Это можно сделать с помощью команды [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) (при создании базы) или команды [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) (если база данных уже существует).</span><span class="sxs-lookup"><span data-stu-id="82457-108">Add database filegroups to the database which will hold the partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if the database exists already.</span></span>
* <span data-ttu-id="82457-109">При необходимости добавьте один или несколько файлов в каждую группу файлов базы данных.</span><span class="sxs-lookup"><span data-stu-id="82457-109">Add one or more files (as needed) to each database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="82457-110">Укажите целевую группу файлов, которая будет содержать данные для этого секционирования, и имена физических файлов базы данных, в которых будут храниться данные группы файлов.</span><span class="sxs-lookup"><span data-stu-id="82457-110">Specify the target filegroup which holds data for this partition and the physical database file name(s) where the filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="82457-111">В следующем примере создается новая база данных с тремя группами файлов в отличие от основных групп и групп журналов, содержащих по одному физическому файлу.</span><span class="sxs-lookup"><span data-stu-id="82457-111">The following example creates a new database with three filegroups other than the primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="82457-112">Файлы базы данных создаются в папке данных SQL Server по умолчанию, настроенной в экземпляре SQL Server.</span><span class="sxs-lookup"><span data-stu-id="82457-112">The database files are created in the default SQL Server Data folder, as configured in the SQL Server instance.</span></span> <span data-ttu-id="82457-113">Дополнительные сведения о расположении файлов по умолчанию см. в статье [Расположение файлов для экземпляра по умолчанию и именованных экземпляров SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="82457-113">For more information about the default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a><span data-ttu-id="82457-114">Создание секционированной таблицы</span><span class="sxs-lookup"><span data-stu-id="82457-114">Create a partitioned table</span></span>
<span data-ttu-id="82457-115">Создайте секционированные таблицы в соответствии со схемой данных, сопоставленной с группами файлов базы данных, созданных на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="82457-115">Create partitioned table(s) according to the data schema, mapped to the database filegroups created in the previous step.</span></span> <span data-ttu-id="82457-116">При массовом импорте данных в секционированные таблицы записи будут распределены между группами файлов в соответствии со схемой секционирования, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="82457-116">When data is bulk imported to the partitioned table(s), records will be distributed among the filegroups according to a partition scheme, as described below.</span></span>

<span data-ttu-id="82457-117">**Чтобы создать таблицу секционирования:**</span><span class="sxs-lookup"><span data-stu-id="82457-117">**To create a partition table, you need to:**</span></span>

* <span data-ttu-id="82457-118">[Создайте функцию секционирования](https://msdn.microsoft.com/library/ms187802.aspx), которая определяет диапазон значений или границ для каждой отдельной таблицы секционирования, чтобы, например, ограничить секции по месяцам (поле\_даты_и\_времени) в 2013 году.</span><span class="sxs-lookup"><span data-stu-id="82457-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines the range of values/boundaries to be included in each individual partition table, e.g., to limit partitions by month(some\_datetime\_field) in the year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="82457-119">[Создайте схему секционирования](https://msdn.microsoft.com/library/ms179854.aspx) , в которой каждый диапазон секционирования в функции секционирования сопоставляется с физической группой файлов, например:</span><span class="sxs-lookup"><span data-stu-id="82457-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in the partition function to a physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> TO (
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="82457-120">Чтобы проверить диапазоны на практике в каждой секции в соответствии с функцией и схемой, выполните следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="82457-120">To verify the ranges in effect in each partition according to the function/scheme, run the following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="82457-121">[Создайте секционированные таблицы](https://msdn.microsoft.com/library/ms174979.aspx)в соответствии со схемой данных и укажите схему секционирования и поле ограничений, используемые для секционирования таблицы, например:</span><span class="sxs-lookup"><span data-stu-id="82457-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according to your data schema, and specify the partition scheme and constraint field used to partition the table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="82457-122">Дополнительные сведения см. в статье [Создание секционированных таблиц и индексов](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="82457-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-the-data-for-each-individual-partition-table"></a><span data-ttu-id="82457-123">Массовый импорт данных для каждой отдельной таблицы секционирования</span><span class="sxs-lookup"><span data-stu-id="82457-123">Bulk import the data for each individual partition table</span></span>
* <span data-ttu-id="82457-124">Можно использовать BCP, BULK INSERT или другие средства, например [мастер миграции SQL Server](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="82457-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="82457-125">В приведенном ниже примере используется метод BCP.</span><span class="sxs-lookup"><span data-stu-id="82457-125">The example provided uses the BCP method.</span></span>
* <span data-ttu-id="82457-126">[Измените базу данных](https://msdn.microsoft.com/library/bb522682.aspx), заменив схему ведения журнала транзакций на BULK_LOGGED, что позволит свести к минимуму нагрузку ведения журнала, например:</span><span class="sxs-lookup"><span data-stu-id="82457-126">[Alter the database](https://msdn.microsoft.com/library/bb522682.aspx) to change transaction logging scheme to BULK_LOGGED to minimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="82457-127">Чтобы ускорить загрузку данных, запустите параллельные операции массового импорта.</span><span class="sxs-lookup"><span data-stu-id="82457-127">To expedite data loading, launch the bulk import operations in parallel.</span></span> <span data-ttu-id="82457-128">Советы по ускорению импорта больших данных в базы SQL Server см. в статье [Загрузка данных емкостью 1 ТБ менее чем за час](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="82457-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="82457-129">В следующем сценарии PowerShell приведен пример параллельной загрузки данных с использованием BCP.</span><span class="sxs-lookup"><span data-stu-id="82457-129">The following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # The example assumes the partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes the input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set the server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match the number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name to be loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-to-optimize-joins-and-query-performance"></a><span data-ttu-id="82457-130">Создание индексов для оптимизации производительности запросов и объединений</span><span class="sxs-lookup"><span data-stu-id="82457-130">Create indexes to optimize joins and query performance</span></span>
* <span data-ttu-id="82457-131">В случае извлечения данных для моделирования из нескольких таблиц создайте индексы для ключей объединений, чтобы повысить производительность объединений.</span><span class="sxs-lookup"><span data-stu-id="82457-131">If you will extract data for modeling from multiple tables, create indexes on the join keys to improve the join performance.</span></span>
* <span data-ttu-id="82457-132">[Создайте индексы](https://technet.microsoft.com/library/ms188783.aspx) (кластеризованные или некластеризованные) для одной и той же целевой группы файлов каждой секции, например:</span><span class="sxs-lookup"><span data-stu-id="82457-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting the same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="82457-133">или</span><span class="sxs-lookup"><span data-stu-id="82457-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="82457-134">Вы можете создать индексы перед массовым импортом данных.</span><span class="sxs-lookup"><span data-stu-id="82457-134">You may choose to create the indexes before bulk importing the data.</span></span> <span data-ttu-id="82457-135">Однако это приведет к замедлению загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="82457-135">Index creation before bulk importing will slow down the data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="82457-136">Расширенный процесс аналитики и технологии в действии: пример</span><span class="sxs-lookup"><span data-stu-id="82457-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="82457-137">Полноценный пошаговый пример применения процесса Cortana Analytics с использованием общедоступного набора данных см. в статье [Процесс обработки и анализа данных группы на практике: использование SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="82457-137">For an end-to-end walkthrough example using the Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

