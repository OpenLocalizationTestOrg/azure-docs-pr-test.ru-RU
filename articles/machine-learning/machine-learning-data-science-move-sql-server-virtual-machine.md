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
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>Перемещение данных tooSQL Server на виртуальной машине Azure
В этом разделе описаны параметры hello для перемещения данных из неструктурированных файлов (форматы CSV или TSV) или из локального SQL Server tooSQL Server на виртуальной машине Azure. Эти задачи для облака toohello перемещение данных являются частью hello командного процесса обработки и анализа данных.

Раздел, описывающий параметры hello tooan перемещения данных базы данных SQL Azure для машинного обучения, в разделе [перемещение данных tooan базы данных SQL Azure для машинного обучения Azure](machine-learning-data-science-move-sql-azure.md).

Hello **меню** ниже tootopics ссылки, которые описывают, как tooingest данных в других целевых средах, где hello данные могут храниться и обрабатываться во время hello процесса обработки и анализа данных Team (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hello следующей таблице перечислены параметры hello для перемещения данных tooSQL Server на виртуальной машине Azure.

| <b>ИСТОЧНИК</b> | <b>НАЗНАЧЕНИЕ: SQL Server на виртуальной машине Azure</b> |
| --- | --- |
| <b>Неструктурированный файл</b> |1. <a href="#insert-tables-bcp">Служебная программа командной строки для массового копирования (BCP)</a><br> 2. <a href="#insert-tables-bulkquery">SQL-запрос на массовую вставку</a><br> 3. <a href="#sql-builtin-utilities">Графические служебные программы, встроенные в SQL Server.</a> |
| <b>Локальный сервер SQL Server</b> |1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Развертывание виртуальной Машины Microsoft Azure мастер tooa базы данных SQL Server</a><br> 2. <a href="#export-flat-file">Экспорт tooa неструктурированного файла</a><br> 3. <a href="#sql-migration">Мастер миграции баз данных SQL</a> <br> 4. <a href="#sql-backup">Архивация и восстановление базы данных</a><br> |

Обратите внимание на то, что в этом документе предполагается выполнение команд SQL в среде SQL Server Management Studio или в обозревателе базы данных Visual Studio.

> [!TIP]
> В качестве альтернативы можно использовать [фабрики данных Azure](https://azure.microsoft.com/services/data-factory/) toocreate и запланировать конвейера, который будет перемещен tooa данных виртуальной Машины SQL Server в Azure. Дополнительные сведения см. в статье [Перемещение данных с помощью действия копирования](../data-factory/data-factory-data-movement-activities.md).
>
>

## <a name="prereqs"></a>Предварительные требования
Для выполнения действий, описанных в этом учебнике, вам необходимо следующее.

* <seg>
  **Подписка Azure**.</seg> Если у вас нет подписки, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).
* **Azure storage account**. Учетная запись хранилища Azure используется для хранения данных hello в этом учебнике. При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи. После создания учетной записи хранилища hello потребуется tooobtain hello от имени учетной записи хранилища hello tooaccess использования ключа. Ознакомьтесь с разделом [Управление ключами доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Подготовленный **SQL Server на виртуальной машине Azure**. Инструкции см. в статье [Настройка SQL Server на виртуальной машине Azure как сервера IPython Notebook для расширенной аналитики](machine-learning-data-science-setup-sql-server-virtual-machine.md).
* Установленная и настроенная локальная среда **Azure PowerShell**. Инструкции см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

## <a name="filesource_to_sqlonazurevm"></a>Перемещение данных из неструктурированного файла источника tooSQL Server на Виртуальной машине Azure
Если данные хранятся в неструктурированном файле (упорядочены в формате строк и столбцов), его можно перемещать tooSQL сервера виртуальной Машины в Azure через следующие методы hello:

1. [Служебная программа командной строки для массового копирования (BCP)](#insert-tables-bcp)
2. [SQL-запрос на массовую вставку ](#insert-tables-bulkquery)
3. [Графические служебные программы, встроенные в SQL Server (импорт или экспорт, службы SSIS)](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>Служебная программа командной строки для массового копирования (BCP)
BCP — программа командной строки, установленных с SQL Server и является одним из hello быстрый способов toomove данных. Она работает во всех трех вариантах SQL Server (в локальном SQL Server, SQL Azure и виртуальной машине SQL Server в Azure).

> [!NOTE]
> **Где следует размещать данные для программы BCP?**  
> Хотя это не обязательно наличие файлов, содержащий источник данных, расположенных на компьютере hello целевого SQL Server позволяет быстрее hello передает (скорость vs дискового ввода-ВЫВОДА скорость сети). Можно переместить hello неструктурированных файлов, содержащий компьютер toohello данных там, где установлен сервер SQL Server с помощью различных копирование файлов средства, такие как [AZCopy](../storage/common/storage-use-azcopy.md), [обозреватель хранилищ Azure](http://storageexplorer.com/) или скопируйте и вставьте windows через удаленное Протокол рабочего стола (RDP).
>
>

1. Нужно обеспечить создание hello базы данных и таблиц hello в базе данных SQL Server целевого hello. Ниже приведен пример того, как toodo Здравствуйте, что использование `Create Database` и `Create Table` команды:

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. Создайте hello файл форматирования, описывающий hello схемы для таблицы hello, выполнив следующую команду из командной строки машины hello hello hello установленным bcp.

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. Вставка данных hello в hello базы данных с помощью команды bcp hello следующим образом. Это должно работать из командной строки hello, предполагая, что hello SQL Server установлен на одном компьютере:

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **Оптимизация вставляет BCP** можно найти hello следующей статьей [«Рекомендации по оптимизации массового импорта»](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize такие вставляет.
>
>

### <a name="insert-tables-bulkquery-parallel"></a>Распараллеливание операций вставки для ускорения перемещения данных
При перемещении данных hello имеет большой размер, можно ускорить вещей, одновременное выполнение нескольких команд BCP параллельно в скрипте PowerShell.

> [!NOTE]
> **Большие наборы данных приема** загрузки для наборов данных и очень больших данных toooptimize секционирование таблиц логические и физические базы данных с использованием нескольких файловых групп и секционирования таблиц. Дополнительные сведения о создании и загрузке данных таблицы toopartition см. в разделе [таблицы разделов SQL параллельной нагрузки](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
>
>

Hello сценарий PowerShell ниже демонстрируют параллельной вставки, с помощью программы bcp.

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


### <a name="insert-tables-bulkquery"></a>SQL-запрос на массовую вставку
[Массовая вставка SQL-запроса](https://msdn.microsoft.com/library/ms188365) tooimport используемые данные в базу данных hello из строк и столбцов на основе файлов (hello поддерживаемые типы описаны в[Подготовка данных к массовому экспорту или импорту (SQL Server)](https://msdn.microsoft.com/library/ms188609)) раздела.

Ниже приведены некоторые примеры команд для массовой вставки:  

1. Анализ данных и задать любые пользовательские параметры перед импортом toomake том, что база данных SQL Server, hello предполагает hello в том же формате, для всех специальных полей, например дат. Ниже приведен пример как tooset hello формат даты как год месяц день (если данные содержат hello Дата в формате год месяц день):

        SET DATEFORMAT ymd;    
2. Импорт данных с помощью операторов массового импорта:

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>Служебные программы, встроенные в SQL Server
Данные tooimport служб интеграции SQL Server (SSIS) можно использовать в виртуальной Машине SQL Server в Azure из неструктурированного файла.
Службы SSIS доступны в двух средах Studio. Дополнительные сведения см. в статье [Разработка Integration Services (SSIS) и средства управления](https://technet.microsoft.com/library/ms140028.aspx):

* сведения о SQL Server Data Tools см. в статье [Скачать SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/data/tools.aspx);  
* Дополнительные сведения о приветствия мастера импорта и экспорта см [SQL Server Импорт и экспорт](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>Перемещение данных из tooSQL локального сервера SQL Server на Виртуальной машине Azure
Можно также использовать следующие стратегии миграции hello:

1. [Развертывание виртуальной Машины Microsoft Azure мастер tooa базы данных SQL Server](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [Экспорт файла tooFlat](#export-flat-file)
3. [Мастер миграции баз данных SQL](#sql-migration)
4. [Архивация и восстановление базы данных](#sql-backup)

Описание каждого из этих способов см. ниже.

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>Развертывание виртуальной Машины Microsoft Azure мастер tooa базы данных SQL Server
Hello **развертывание виртуальной Машины Microsoft Azure мастер tooa базы данных SQL Server** является простой и рекомендуемый способ toomove данных из локальной tooSQL экземпляр сервера SQL Server на Виртуальной машине Azure. Подробное описание действий, а также обсуждение альтернативные см. в разделе [перенести tooSQL базы данных сервера на Виртуальной машине Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).

### <a name="export-flat-file"></a>Экспорт файла tooFlat
Различные методы могут быть используется toobulk экспорта данных из локального SQL Server описаны в hello [массовый импорт и экспорт данных (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) раздела. В этом документе мы рассмотрим hello программы массового копирования (BCP) в качестве примера. После экспорта данных в неструктурированный файл его можно импортированных tooanother SQL server, с помощью массового импорта.

1. Экспорт данных hello в локальной среде SQL Server tooa файла с помощью программы bcp hello следующим образом

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. Создание базы данных hello и hello таблицы на виртуальной Машине SQL Server в Azure с помощью hello `create database` и `create table` для схемы таблицы hello, экспортированный на шаге 1.
3. Создайте файл форматирования для описания hello схемы таблицы данных hello экспорта или импорта. Сведения о формате файла hello описаны в [Создание файла форматирования (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).

    Создание файла формата при под управлением BCP из hello машины SQL Server

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    Создание файла форматирования при удаленном запуске BCP для SQL Server

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. Используйте любой из методов hello, описанные в разделе [перенос данных из файла источника](#filesource_to_sqlonazurevm) toomove hello данные в неструктурированные файлы tooa SQL Server.

### <a name="sql-migration"></a>Мастер миграции баз данных SQL
[Мастер миграции баз данных SQL Server](http://sqlazuremw.codeplex.com/) предоставляет toomove понятным способом данные между двумя экземплярами SQL server. Он позволяет схемы hello пользователя toomap hello данных между источниками и целевые таблицы, выберите типы столбцов и различные функциональные возможности. На деле hello в нем массового копирования (BCP). Снимок экрана приветствия Добро пожаловать экран приветствия ниже показан мастер миграции баз данных SQL.  

![Мастер миграции SQL Server][2]

### <a name="sql-backup"></a>Архивация и восстановление базы данных
SQL Server поддерживает:

1. [База данных резервного копирования и восстановления](https://msdn.microsoft.com/library/ms187048.aspx) (оба tooa локальный файл или bacpac экспорта tooblob) и [приложений уровня данных](https://msdn.microsoft.com/library/ee210546.aspx) (с помощью bacpac).
2. Возможность toodirectly Создание виртуальных машин SQL Server в Azure с копии базы данных или копирования tooan SQL Azure базы данных. Дополнительные сведения см. в разделе [hello использования мастера копирования баз данных](https://msdn.microsoft.com/library/ms188664.aspx).

Снимок экрана приветствия базу данных обратно вверх или восстановить параметры из среды SQL Server Management Studio показано ниже.

![Средство импорта данных из SQL Server][1]

## <a name="resources"></a>Ресурсы
[Перенос базы данных tooSQL Server на Виртуальной машине Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Приступая к работе с SQL Server в виртуальных машинах Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
