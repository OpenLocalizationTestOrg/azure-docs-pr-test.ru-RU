---
title: "tooSQL aaaMove данных сервера на виртуальной машине Azure | Документы Microsoft"
description: "Перемещение данных из неструктурированных файлов или из локального SQL Server tooSQL Server на виртуальной Машине Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="cd3a9-103">Перемещение данных tooSQL Server на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="cd3a9-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="cd3a9-104">В этом разделе описаны параметры hello для перемещения данных из неструктурированных файлов (форматы CSV или TSV) или из локального SQL Server tooSQL Server на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="cd3a9-105">Эти задачи для облака toohello перемещение данных являются частью hello командного процесса обработки и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="cd3a9-106">Раздел, описывающий параметры hello tooan перемещения данных базы данных SQL Azure для машинного обучения, в разделе [перемещение данных tooan базы данных SQL Azure для машинного обучения Azure](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="cd3a9-107">Hello **меню** ниже tootopics ссылки, которые описывают, как tooingest данных в других целевых средах, где hello данные могут храниться и обрабатываться во время hello процесса обработки и анализа данных Team (TDSP).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="cd3a9-108">Hello следующей таблице перечислены параметры hello для перемещения данных tooSQL Server на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="cd3a9-109"><b>ИСТОЧНИК</b></span><span class="sxs-lookup"><span data-stu-id="cd3a9-109"><b>SOURCE</b></span></span> | <span data-ttu-id="cd3a9-110"><b>НАЗНАЧЕНИЕ: SQL Server на виртуальной машине Azure</b></span><span class="sxs-lookup"><span data-stu-id="cd3a9-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="cd3a9-111"><b>Неструктурированный файл</b></span><span class="sxs-lookup"><span data-stu-id="cd3a9-111"><b>Flat File</b></span></span> |<span data-ttu-id="cd3a9-112">1. <a href="#insert-tables-bcp">Служебная программа командной строки для массового копирования (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="cd3a9-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="cd3a9-113">2. <a href="#insert-tables-bulkquery">SQL-запрос на массовую вставку</a></span><span class="sxs-lookup"><span data-stu-id="cd3a9-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="cd3a9-114">3. <a href="#sql-builtin-utilities">Графические служебные программы, встроенные в SQL Server.</a></span><span class="sxs-lookup"><span data-stu-id="cd3a9-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="cd3a9-115"><b>Локальный сервер SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="cd3a9-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="cd3a9-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Развертывание виртуальной Машины Microsoft Azure мастер tooa базы данных SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="cd3a9-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="cd3a9-117">2. <a href="#export-flat-file">Экспорт tooa неструктурированного файла</a></span><span class="sxs-lookup"><span data-stu-id="cd3a9-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="cd3a9-118">3. <a href="#sql-migration">Мастер миграции баз данных SQL</a></span><span class="sxs-lookup"><span data-stu-id="cd3a9-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="cd3a9-119">4. <a href="#sql-backup">Архивация и восстановление базы данных</a></span><span class="sxs-lookup"><span data-stu-id="cd3a9-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="cd3a9-120">Обратите внимание на то, что в этом документе предполагается выполнение команд SQL в среде SQL Server Management Studio или в обозревателе базы данных Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="cd3a9-121">В качестве альтернативы можно использовать [фабрики данных Azure](https://azure.microsoft.com/services/data-factory/) toocreate и запланировать конвейера, который будет перемещен tooa данных виртуальной Машины SQL Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="cd3a9-122">Дополнительные сведения см. в статье [Перемещение данных с помощью действия копирования](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="cd3a9-123"><a name="prereqs"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cd3a9-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="cd3a9-124">Для выполнения действий, описанных в этом учебнике, вам необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="cd3a9-125"><seg>
  **Подписка Azure**.</seg></span><span class="sxs-lookup"><span data-stu-id="cd3a9-125">An **Azure subscription**.</span></span> <span data-ttu-id="cd3a9-126">Если у вас нет подписки, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cd3a9-127">**Azure storage account**.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-127">An **Azure storage account**.</span></span> <span data-ttu-id="cd3a9-128">Учетная запись хранилища Azure используется для хранения данных hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="cd3a9-129">При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="cd3a9-130">После создания учетной записи хранилища hello потребуется tooobtain hello от имени учетной записи хранилища hello tooaccess использования ключа.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="cd3a9-131">Ознакомьтесь с разделом [Управление ключами доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="cd3a9-132">Подготовленный **SQL Server на виртуальной машине Azure**.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="cd3a9-133">Инструкции см. в статье [Настройка SQL Server на виртуальной машине Azure как сервера IPython Notebook для расширенной аналитики](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="cd3a9-134">Установленная и настроенная локальная среда **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="cd3a9-135">Инструкции см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="cd3a9-136"><a name="filesource_to_sqlonazurevm"></a>Перемещение данных из неструктурированного файла источника tooSQL Server на Виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="cd3a9-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="cd3a9-137">Если данные хранятся в неструктурированном файле (упорядочены в формате строк и столбцов), его можно перемещать tooSQL сервера виртуальной Машины в Azure через следующие методы hello:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="cd3a9-138">Служебная программа командной строки для массового копирования (BCP)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="cd3a9-139">SQL-запрос на массовую вставку </span><span class="sxs-lookup"><span data-stu-id="cd3a9-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="cd3a9-140">Графические служебные программы, встроенные в SQL Server (импорт или экспорт, службы SSIS)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="cd3a9-141"><a name="insert-tables-bcp"></a>Служебная программа командной строки для массового копирования (BCP)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="cd3a9-142">BCP — программа командной строки, установленных с SQL Server и является одним из hello быстрый способов toomove данных.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="cd3a9-143">Она работает во всех трех вариантах SQL Server (в локальном SQL Server, SQL Azure и виртуальной машине SQL Server в Azure).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="cd3a9-144">**Где следует размещать данные для программы BCP?**</span><span class="sxs-lookup"><span data-stu-id="cd3a9-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="cd3a9-145">Хотя это не обязательно наличие файлов, содержащий источник данных, расположенных на компьютере hello целевого SQL Server позволяет быстрее hello передает (скорость vs дискового ввода-ВЫВОДА скорость сети).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="cd3a9-146">Можно переместить hello неструктурированных файлов, содержащий компьютер toohello данных там, где установлен сервер SQL Server с помощью различных копирование файлов средства, такие как [AZCopy](../storage/common/storage-use-azcopy.md), [обозреватель хранилищ Azure](http://storageexplorer.com/) или скопируйте и вставьте windows через удаленное Протокол рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="cd3a9-147">Нужно обеспечить создание hello базы данных и таблиц hello в базе данных SQL Server целевого hello.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="cd3a9-148">Ниже приведен пример того, как toodo Здравствуйте, что использование `Create Database` и `Create Table` команды:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="cd3a9-149">Создайте hello файл форматирования, описывающий hello схемы для таблицы hello, выполнив следующую команду из командной строки машины hello hello hello установленным bcp.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="cd3a9-150">Вставка данных hello в hello базы данных с помощью команды bcp hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="cd3a9-151">Это должно работать из командной строки hello, предполагая, что hello SQL Server установлен на одном компьютере:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="cd3a9-152">**Оптимизация вставляет BCP** можно найти hello следующей статьей [«Рекомендации по оптимизации массового импорта»](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize такие вставляет.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="cd3a9-153"><a name="insert-tables-bulkquery-parallel"></a>Распараллеливание операций вставки для ускорения перемещения данных</span><span class="sxs-lookup"><span data-stu-id="cd3a9-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="cd3a9-154">При перемещении данных hello имеет большой размер, можно ускорить вещей, одновременное выполнение нескольких команд BCP параллельно в скрипте PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="cd3a9-155">**Большие наборы данных приема** загрузки для наборов данных и очень больших данных toooptimize секционирование таблиц логические и физические базы данных с использованием нескольких файловых групп и секционирования таблиц.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="cd3a9-156">Дополнительные сведения о создании и загрузке данных таблицы toopartition см. в разделе [таблицы разделов SQL параллельной нагрузки](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="cd3a9-157">Hello сценарий PowerShell ниже демонстрируют параллельной вставки, с помощью программы bcp.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <span data-ttu-id="cd3a9-158"><a name="insert-tables-bulkquery"></a>SQL-запрос на массовую вставку</span><span class="sxs-lookup"><span data-stu-id="cd3a9-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="cd3a9-159">[Массовая вставка SQL-запроса](https://msdn.microsoft.com/library/ms188365) tooimport используемые данные в базу данных hello из строк и столбцов на основе файлов (hello поддерживаемые типы описаны в[Подготовка данных к массовому экспорту или импорту (SQL Server)](https://msdn.microsoft.com/library/ms188609)) раздела.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="cd3a9-160">Ниже приведены некоторые примеры команд для массовой вставки:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="cd3a9-161">Анализ данных и задать любые пользовательские параметры перед импортом toomake том, что база данных SQL Server, hello предполагает hello в том же формате, для всех специальных полей, например дат.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="cd3a9-162">Ниже приведен пример как tooset hello формат даты как год месяц день (если данные содержат hello Дата в формате год месяц день):</span><span class="sxs-lookup"><span data-stu-id="cd3a9-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="cd3a9-163">Импорт данных с помощью операторов массового импорта:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="cd3a9-164"><a name="sql-builtin-utilities"></a>Служебные программы, встроенные в SQL Server</span><span class="sxs-lookup"><span data-stu-id="cd3a9-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="cd3a9-165">Данные tooimport служб интеграции SQL Server (SSIS) можно использовать в виртуальной Машине SQL Server в Azure из неструктурированного файла.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="cd3a9-166">Службы SSIS доступны в двух средах Studio.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="cd3a9-167">Дополнительные сведения см. в статье [Разработка Integration Services (SSIS) и средства управления](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="cd3a9-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="cd3a9-168">сведения о SQL Server Data Tools см. в статье [Скачать SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/data/tools.aspx);</span><span class="sxs-lookup"><span data-stu-id="cd3a9-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="cd3a9-169">Дополнительные сведения о приветствия мастера импорта и экспорта см [SQL Server Импорт и экспорт](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="cd3a9-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="cd3a9-170"><a name="sqlonprem_to_sqlonazurevm"></a>Перемещение данных из tooSQL локального сервера SQL Server на Виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="cd3a9-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="cd3a9-171">Можно также использовать следующие стратегии миграции hello:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="cd3a9-172">Развертывание виртуальной Машины Microsoft Azure мастер tooa базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="cd3a9-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="cd3a9-173">Экспорт файла tooFlat</span><span class="sxs-lookup"><span data-stu-id="cd3a9-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="cd3a9-174">Мастер миграции баз данных SQL</span><span class="sxs-lookup"><span data-stu-id="cd3a9-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="cd3a9-175">Архивация и восстановление базы данных</span><span class="sxs-lookup"><span data-stu-id="cd3a9-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="cd3a9-176">Описание каждого из этих способов см. ниже.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="cd3a9-177">Развертывание виртуальной Машины Microsoft Azure мастер tooa базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="cd3a9-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="cd3a9-178">Hello **развертывание виртуальной Машины Microsoft Azure мастер tooa базы данных SQL Server** является простой и рекомендуемый способ toomove данных из локальной tooSQL экземпляр сервера SQL Server на Виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="cd3a9-179">Подробное описание действий, а также обсуждение альтернативные см. в разделе [перенести tooSQL базы данных сервера на Виртуальной машине Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="cd3a9-180"><a name="export-flat-file"></a>Экспорт файла tooFlat</span><span class="sxs-lookup"><span data-stu-id="cd3a9-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="cd3a9-181">Различные методы могут быть используется toobulk экспорта данных из локального SQL Server описаны в hello [массовый импорт и экспорт данных (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="cd3a9-182">В этом документе мы рассмотрим hello программы массового копирования (BCP) в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="cd3a9-183">После экспорта данных в неструктурированный файл его можно импортированных tooanother SQL server, с помощью массового импорта.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="cd3a9-184">Экспорт данных hello в локальной среде SQL Server tooa файла с помощью программы bcp hello следующим образом</span><span class="sxs-lookup"><span data-stu-id="cd3a9-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="cd3a9-185">Создание базы данных hello и hello таблицы на виртуальной Машине SQL Server в Azure с помощью hello `create database` и `create table` для схемы таблицы hello, экспортированный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="cd3a9-186">Создайте файл форматирования для описания hello схемы таблицы данных hello экспорта или импорта.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="cd3a9-187">Сведения о формате файла hello описаны в [Создание файла форматирования (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="cd3a9-188">Создание файла формата при под управлением BCP из hello машины SQL Server</span><span class="sxs-lookup"><span data-stu-id="cd3a9-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="cd3a9-189">Создание файла форматирования при удаленном запуске BCP для SQL Server</span><span class="sxs-lookup"><span data-stu-id="cd3a9-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="cd3a9-190">Используйте любой из методов hello, описанные в разделе [перенос данных из файла источника](#filesource_to_sqlonazurevm) toomove hello данные в неструктурированные файлы tooa SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="cd3a9-191"><a name="sql-migration"></a>Мастер миграции баз данных SQL</span><span class="sxs-lookup"><span data-stu-id="cd3a9-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="cd3a9-192">[Мастер миграции баз данных SQL Server](http://sqlazuremw.codeplex.com/) предоставляет toomove понятным способом данные между двумя экземплярами SQL server.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="cd3a9-193">Он позволяет схемы hello пользователя toomap hello данных между источниками и целевые таблицы, выберите типы столбцов и различные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="cd3a9-194">На деле hello в нем массового копирования (BCP).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="cd3a9-195">Снимок экрана приветствия Добро пожаловать экран приветствия ниже показан мастер миграции баз данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![Мастер миграции SQL Server][2]

### <span data-ttu-id="cd3a9-197"><a name="sql-backup"></a>Архивация и восстановление базы данных</span><span class="sxs-lookup"><span data-stu-id="cd3a9-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="cd3a9-198">SQL Server поддерживает:</span><span class="sxs-lookup"><span data-stu-id="cd3a9-198">SQL Server supports:</span></span>

1. <span data-ttu-id="cd3a9-199">[База данных резервного копирования и восстановления](https://msdn.microsoft.com/library/ms187048.aspx) (оба tooa локальный файл или bacpac экспорта tooblob) и [приложений уровня данных](https://msdn.microsoft.com/library/ee210546.aspx) (с помощью bacpac).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="cd3a9-200">Возможность toodirectly Создание виртуальных машин SQL Server в Azure с копии базы данных или копирования tooan SQL Azure базы данных.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="cd3a9-201">Дополнительные сведения см. в разделе [hello использования мастера копирования баз данных](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd3a9-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="cd3a9-202">Снимок экрана приветствия базу данных обратно вверх или восстановить параметры из среды SQL Server Management Studio показано ниже.</span><span class="sxs-lookup"><span data-stu-id="cd3a9-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Средство импорта данных из SQL Server][1]

## <a name="resources"></a><span data-ttu-id="cd3a9-204">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="cd3a9-204">Resources</span></span>
[<span data-ttu-id="cd3a9-205">Перенос базы данных tooSQL Server на Виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="cd3a9-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="cd3a9-206">Приступая к работе с SQL Server в виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="cd3a9-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
