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
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Параллельный массовый импорт данных с использованием таблиц секционирования SQL
В этом документе описывается, как toobuild секционированных таблиц для быстрого параллельный массовый импорт данных базы данных SQL Server tooa. Базы данных SQL tooa загрузки или передачи данных большого размера, импорт данных toohello баз данных SQL Server и последующие запросы, может быть повышена путем использования *секционированных таблиц и представлений*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Создание новой базы данных и набора групп файлов
* [Создайте базу данных](https://technet.microsoft.com/library/ms176061.aspx), если она еще не существует.
* Добавление базы данных базы данных файловые группы toohello, где будут содержаться hello секционированы физических файлов. Это можно сделать с помощью [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) Если новый или [инструкции ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) Если hello базы данных уже существует.
* Добавьте один или несколько файловых групп базы данных файлы (при необходимости) tooeach.
  
  > [!NOTE]
  > Укажите целевой файловой группе, которая содержит данные для этой секции и hello имена файлов физической базы данных хранения hello файловую группу данных hello.
  > 
  > 

Hello следующий пример создает новую базу данных с три файловые группы, отличные от основной hello и группы журналов, содержащие один физический файл в каждом. Hello файлы базы данных создаются в папке данных SQL Server по умолчанию hello, как настроено в экземпляре SQL Server hello. Дополнительные сведения о hello расположения файлов по умолчанию см. в разделе [расположения файлов по умолчанию и именованных экземпляров SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

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

## <a name="create-a-partitioned-table"></a>Создание секционированной таблицы
Создание секционированных таблиц, в соответствии с toohello данные схемы, сопоставленные toohello файловые группы базы данных на предыдущем шаге hello. При массовом импорте данных toohello секционированные таблицы, записи распределяются среди hello файловые группы в соответствии с tooa схему секционирования, как описано ниже.

**toocreate секции таблицы, необходимо:**

* [Создать функцию секционирования](https://msdn.microsoft.com/library/ms187802.aspx) определяющего hello диапазон значений или границы toobe включены в каждой отдельной секции таблицы, например, toolimit секции по месяцам (некоторые\_datetime\_поля) в течение года hello 2013:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [Создание схемы секционирования,](https://msdn.microsoft.com/library/ms179854.aspx) который сопоставляет каждый диапазон секции в hello секции функция tooa физической файловой группы, например:
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  диапазоны hello tooverify действует в каждом соответствующим toohello функция и схема секционирования, запустите приветствия при следующем запросе:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [Создать секционированную таблицу](https://msdn.microsoft.com/library/ms174979.aspx)(s) tooyour данных схемы в соответствии с и использовать схему и ограничение поле hello раздела toopartition hello таблицы, например:
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Дополнительные сведения см. в статье [Создание секционированных таблиц и индексов](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>Массового импорта данных hello для каждой отдельной секции таблицы
* Можно использовать BCP, BULK INSERT или другие средства, например [мастер миграции SQL Server](http://sqlazuremw.codeplex.com/). предоставленный пример Hello метод hello BCP.
* [Инструкции ALTER hello database](https://msdn.microsoft.com/library/bb522682.aspx) затраты на toominimize tooBULK_LOGGED схема ведения журнала, например ведение журнала транзакций toochange:
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* Загрузка, tooexpedite данных запустите hello операций массового импорта в параллельном режиме. Советы по ускорению импорта больших данных в базы SQL Server см. в статье [Загрузка данных емкостью 1 ТБ менее чем за час](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Hello следующий скрипт PowerShell приведен пример параллельную загрузку с помощью программы BCP данных.

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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>Создание индексов toooptimize соединения и производительность запросов
* Если данные для моделирования будут извлекаться из нескольких таблиц, создайте индексы ключи соединения hello производительности соединения tooimprove hello.
* [Создание индексов](https://technet.microsoft.com/library/ms188783.aspx) (кластеризованный или некластеризованный), предназначенных для hello одной файловой группе для каждой секции для например:
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  или
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > Вы можете toocreate индексы hello перед массовым импортом данных hello. Создание индекса перед массовым импортом замедлится загрузки данных hello.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Расширенный процесс аналитики и технологии в действии: пример
Пример Пошаговое руководство с начала до конца, с помощью hello процесса Cortana аналитика с помощью открытого набора данных, в разделе [Analytics процесса Cortana в действии: с помощью SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

