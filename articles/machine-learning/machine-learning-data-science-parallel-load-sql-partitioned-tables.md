---
title: "aaaBuild и оптимизировать таблицы для быстрого параллельный импорт данных в SQL Server на Виртуальной машине Azure | Документы Microsoft"
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
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="78635-103">Параллельный массовый импорт данных с использованием таблиц секционирования SQL</span><span class="sxs-lookup"><span data-stu-id="78635-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="78635-104">В этом документе описывается, как toobuild секционированных таблиц для быстрого параллельный массовый импорт данных базы данных SQL Server tooa.</span><span class="sxs-lookup"><span data-stu-id="78635-104">This document describes how toobuild partitioned tables for fast parallel bulk importing of data tooa SQL Server database.</span></span> <span data-ttu-id="78635-105">Базы данных SQL tooa загрузки или передачи данных большого размера, импорт данных toohello баз данных SQL Server и последующие запросы, может быть повышена путем использования *секционированных таблиц и представлений*.</span><span class="sxs-lookup"><span data-stu-id="78635-105">For big data loading/transfer tooa SQL database, importing data toohello SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="78635-106">Создание новой базы данных и набора групп файлов</span><span class="sxs-lookup"><span data-stu-id="78635-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="78635-107">[Создайте базу данных](https://technet.microsoft.com/library/ms176061.aspx), если она еще не существует.</span><span class="sxs-lookup"><span data-stu-id="78635-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="78635-108">Добавление базы данных базы данных файловые группы toohello, где будут содержаться hello секционированы физических файлов. Это можно сделать с помощью [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) Если новый или [инструкции ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) Если hello базы данных уже существует.</span><span class="sxs-lookup"><span data-stu-id="78635-108">Add database filegroups toohello database which will hold hello partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if hello database exists already.</span></span>
* <span data-ttu-id="78635-109">Добавьте один или несколько файловых групп базы данных файлы (при необходимости) tooeach.</span><span class="sxs-lookup"><span data-stu-id="78635-109">Add one or more files (as needed) tooeach database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="78635-110">Укажите целевой файловой группе, которая содержит данные для этой секции и hello имена файлов физической базы данных хранения hello файловую группу данных hello.</span><span class="sxs-lookup"><span data-stu-id="78635-110">Specify hello target filegroup which holds data for this partition and hello physical database file name(s) where hello filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="78635-111">Hello следующий пример создает новую базу данных с три файловые группы, отличные от основной hello и группы журналов, содержащие один физический файл в каждом.</span><span class="sxs-lookup"><span data-stu-id="78635-111">hello following example creates a new database with three filegroups other than hello primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="78635-112">Hello файлы базы данных создаются в папке данных SQL Server по умолчанию hello, как настроено в экземпляре SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="78635-112">hello database files are created in hello default SQL Server Data folder, as configured in hello SQL Server instance.</span></span> <span data-ttu-id="78635-113">Дополнительные сведения о hello расположения файлов по умолчанию см. в разделе [расположения файлов по умолчанию и именованных экземпляров SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="78635-113">For more information about hello default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

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

## <a name="create-a-partitioned-table"></a><span data-ttu-id="78635-114">Создание секционированной таблицы</span><span class="sxs-lookup"><span data-stu-id="78635-114">Create a partitioned table</span></span>
<span data-ttu-id="78635-115">Создание секционированных таблиц, в соответствии с toohello данные схемы, сопоставленные toohello файловые группы базы данных на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="78635-115">Create partitioned table(s) according toohello data schema, mapped toohello database filegroups created in hello previous step.</span></span> <span data-ttu-id="78635-116">При массовом импорте данных toohello секционированные таблицы, записи распределяются среди hello файловые группы в соответствии с tooa схему секционирования, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="78635-116">When data is bulk imported toohello partitioned table(s), records will be distributed among hello filegroups according tooa partition scheme, as described below.</span></span>

<span data-ttu-id="78635-117">**toocreate секции таблицы, необходимо:**</span><span class="sxs-lookup"><span data-stu-id="78635-117">**toocreate a partition table, you need to:**</span></span>

* <span data-ttu-id="78635-118">[Создать функцию секционирования](https://msdn.microsoft.com/library/ms187802.aspx) определяющего hello диапазон значений или границы toobe включены в каждой отдельной секции таблицы, например, toolimit секции по месяцам (некоторые\_datetime\_поля) в течение года hello 2013:</span><span class="sxs-lookup"><span data-stu-id="78635-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines hello range of values/boundaries toobe included in each individual partition table, e.g., toolimit partitions by month(some\_datetime\_field) in hello year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="78635-119">[Создание схемы секционирования,](https://msdn.microsoft.com/library/ms179854.aspx) который сопоставляет каждый диапазон секции в hello секции функция tooa физической файловой группы, например:</span><span class="sxs-lookup"><span data-stu-id="78635-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in hello partition function tooa physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="78635-120">диапазоны hello tooverify действует в каждом соответствующим toohello функция и схема секционирования, запустите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="78635-120">tooverify hello ranges in effect in each partition according toohello function/scheme, run hello following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="78635-121">[Создать секционированную таблицу](https://msdn.microsoft.com/library/ms174979.aspx)(s) tooyour данных схемы в соответствии с и использовать схему и ограничение поле hello раздела toopartition hello таблицы, например:</span><span class="sxs-lookup"><span data-stu-id="78635-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according tooyour data schema, and specify hello partition scheme and constraint field used toopartition hello table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="78635-122">Дополнительные сведения см. в статье [Создание секционированных таблиц и индексов](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="78635-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a><span data-ttu-id="78635-123">Массового импорта данных hello для каждой отдельной секции таблицы</span><span class="sxs-lookup"><span data-stu-id="78635-123">Bulk import hello data for each individual partition table</span></span>
* <span data-ttu-id="78635-124">Можно использовать BCP, BULK INSERT или другие средства, например [мастер миграции SQL Server](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="78635-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="78635-125">предоставленный пример Hello метод hello BCP.</span><span class="sxs-lookup"><span data-stu-id="78635-125">hello example provided uses hello BCP method.</span></span>
* <span data-ttu-id="78635-126">[Инструкции ALTER hello database](https://msdn.microsoft.com/library/bb522682.aspx) затраты на toominimize tooBULK_LOGGED схема ведения журнала, например ведение журнала транзакций toochange:</span><span class="sxs-lookup"><span data-stu-id="78635-126">[Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange transaction logging scheme tooBULK_LOGGED toominimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="78635-127">Загрузка, tooexpedite данных запустите hello операций массового импорта в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="78635-127">tooexpedite data loading, launch hello bulk import operations in parallel.</span></span> <span data-ttu-id="78635-128">Советы по ускорению импорта больших данных в базы SQL Server см. в статье [Загрузка данных емкостью 1 ТБ менее чем за час](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="78635-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="78635-129">Hello следующий скрипт PowerShell приведен пример параллельную загрузку с помощью программы BCP данных.</span><span class="sxs-lookup"><span data-stu-id="78635-129">hello following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a><span data-ttu-id="78635-130">Создание индексов toooptimize соединения и производительность запросов</span><span class="sxs-lookup"><span data-stu-id="78635-130">Create indexes toooptimize joins and query performance</span></span>
* <span data-ttu-id="78635-131">Если данные для моделирования будут извлекаться из нескольких таблиц, создайте индексы ключи соединения hello производительности соединения tooimprove hello.</span><span class="sxs-lookup"><span data-stu-id="78635-131">If you will extract data for modeling from multiple tables, create indexes on hello join keys tooimprove hello join performance.</span></span>
* <span data-ttu-id="78635-132">[Создание индексов](https://technet.microsoft.com/library/ms188783.aspx) (кластеризованный или некластеризованный), предназначенных для hello одной файловой группе для каждой секции для например:</span><span class="sxs-lookup"><span data-stu-id="78635-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting hello same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="78635-133">или</span><span class="sxs-lookup"><span data-stu-id="78635-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="78635-134">Вы можете toocreate индексы hello перед массовым импортом данных hello.</span><span class="sxs-lookup"><span data-stu-id="78635-134">You may choose toocreate hello indexes before bulk importing hello data.</span></span> <span data-ttu-id="78635-135">Создание индекса перед массовым импортом замедлится загрузки данных hello.</span><span class="sxs-lookup"><span data-stu-id="78635-135">Index creation before bulk importing will slow down hello data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="78635-136">Расширенный процесс аналитики и технологии в действии: пример</span><span class="sxs-lookup"><span data-stu-id="78635-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="78635-137">Пример Пошаговое руководство с начала до конца, с помощью hello процесса Cortana аналитика с помощью открытого набора данных, в разделе [Analytics процесса Cortana в действии: с помощью SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="78635-137">For an end-to-end walkthrough example using hello Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

