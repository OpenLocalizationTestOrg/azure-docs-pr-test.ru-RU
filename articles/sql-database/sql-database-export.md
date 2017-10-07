---
title: "aaaExport файл BACPAC tooa базы данных Azure SQL | Документы Microsoft"
description: "Экспорт файла BACPAC tooa базы данных Azure SQL, с помощью портала Azure hello"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Экспорт файла BACPAC tooa базы данных Azure SQL

Если вам требуется tooexport базы данных для архивации или для перемещения tooanother платформы, можно экспортировать tooa схемы и данных базы данных hello [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) файла. BACPAC-файл является ZIP-файл с расширением BACPAC, содержащий hello метаданных и данных из базы данных SQL Server. BACPAC-файл можно сохранить в хранилище BLOB-объектов Azure или локальном хранилище, а затем импортировать обратно в базу данных SQL Azure или локальный экземпляр SQL Server. 

> [!IMPORTANT] 
> Автоматический экспорт базы данных SQL Azure не используется с 1 марта 2017 года. Можно использовать [долгосрочного хранения резервной копии](sql-database-long-term-retention.md
) или [автоматизации Azure](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically баз данных SQL архив с помощью PowerShell, в соответствии с расписанием tooa по своему усмотрению. Загрузите образец hello [образец скрипта PowerShell](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) из Github.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Рекомендации при экспорте базы данных SQL Azure

* При экспорте toobe транзакционно согласованной, необходимо убедиться, либо, что запись неактивна во время экспорта hello или что вы экспортируете из [транзакционно согласованной копии](sql-database-copy.md) вашей базы данных Azure SQL.
* При экспорте tooblob хранилище, максимальный размер hello BACPAC-файла составляет 200 ГБ. tooarchive размером BACPAC-файл, экспортируйте toolocal хранилища.
* Экспорт BACPAC tooAzure premium хранения файлов с помощью методов hello, рассматриваемые в данной статье не поддерживается.
* Операции экспорта hello из базы данных SQL Azure превышает 20 часов, может быть отменена. tooincrease производительности во время экспорта, можно сделать следующее.
  * Временно повысить уровень служб.
  * Прекращение все чтения и записи действий во время экспорта hello.
  * Используйте для всех больших таблиц [кластеризованный индекс](https://msdn.microsoft.com/library/ms190457.aspx) со значениями, отличными от NULL. Без кластеризованных индексов экспорт может завершиться ошибкой, если он длится больше 6–12 часов. Это так, как служба экспорта hello должна toocomplete таблицы сканирования tootry tooexport всей таблицы. Toodetermine удобным, если таблицы оптимизированы для экспорта — toorun **DBCC SHOW_STATISTICS** и убедитесь, что hello *RANGE_HI_KEY* не равно null и его значение имеет хорошее распределение. Дополнительную информацию см. в разделе [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> Bacpac не предполагаемого toobe, используемое для операций резервного копирования и восстановления. База данных SQL Azure автоматически создает резервные копии для каждой пользовательской базы данных. Дополнительные сведения см. в статьях [Обзор обеспечения непрерывности бизнес-процессов с помощью базы данных SQL Azure](sql-database-business-continuity.md) и[Подробнее о резервном копировании базы данных SQL](sql-database-automated-backups.md).  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>С помощью портала Azure hello tooa BACPAC-файла экспорта

Здравствуйте, tooexport базы данных с помощью [портал Azure](https://portal.azure.com)откройте страницу приветствия для базы данных и нажмите кнопку **Экспорт** на панели инструментов hello. Укажите имя файла BACPAC hello, укажите учетную запись хранилища Azure hello и контейнер для экспорта hello и предоставить hello учетные данные tooconnect toohello базы данных-источника.  

![Экспорт базы данных](./media/sql-database-export/database-export.png)

Ход выполнения hello toomonitor hello операции экспорта, откройте страницу приветствия hello логический сервер содержащего hello базы данных выполняется экспорт. Прокрутите список вниз слишком**операции** и нажмите кнопку **импорта и экспорта** журнала.

![журнал экспорта](./media/sql-database-export/export-history.png)
![состояние журнала экспорта](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>С помощью служебной программы hello SQLPackage tooa BACPAC-файла экспорта

tooexport SQL базы данных с помощью hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) программы командной строки, в разделе [экспортировать параметры и свойства](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). Hello программу SQLPackage поставляется с hello последние версии [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) и [SQL Server Data Tools для Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), или hello последнюю версию можно загрузить [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) непосредственно из hello Microsoft центре загрузки.

Рекомендуется использовать hello hello программу SQLPackage для обеспечения масштабирования и производительности в большинстве рабочих средах. SQL Server группа консультантов по блог о миграции с помощью BACPAC-файлов в разделе [миграции с SQL Server tooAzure базы данных SQL с помощью файлов BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

В этом примере показано, как tooexport базу данных с помощью SqlPackage.exe с универсальной проверки подлинности Active Directory:

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>Экспорт файла BACPAC tooa, с помощью SQL Server Management Studio (SSMS)

последние версии SQL Server Management Studio Hello предоставляют tooexport мастер BACPAC-файла tooa базы данных SQL Azure. В разделе hello [Экспорт приложения уровня данных](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="export-tooa-bacpac-file-using-powershell"></a>Экспорт файла BACPAC tooa с помощью PowerShell

Используйте hello [New AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) toosubmit командлет export toohello запрос базы данных служба базы данных SQL Azure. В зависимости от размера базы данных hello hello экспорта операция может занять некоторое время toocomplete.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

состояние hello toocheck hello запрос на экспорт, использовать hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) командлета. При выполнении этого сразу же после hello запрос обычно возвращает **состояние: выполняется**. При появлении **состояния: успешно** hello экспорт будет завершен.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>Дальнейшие действия

* toolearn о долгосрочного хранения резервных копий данных из резервной копии базы данных Azure SQL как альтернативный tooexported базы данных в целях архива в разделе [долгосрочного хранения резервной копии](sql-database-long-term-retention.md).
- SQL Server группа консультантов по блог о миграции с помощью BACPAC-файлов в разделе [миграции с SQL Server tooAzure базы данных SQL с помощью файлов BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* toolearn об импорте BACPAC tooa базы данных SQL Server, в разделе [импорта базы данных SQL Server tooa BACPCAC](https://msdn.microsoft.com/library/hh710052.aspx).
* toolearn об экспорте BACPAC из базы данных SQL Server, в разделе [Экспорт приложения уровня данных](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) и [переноса первой базы данных](sql-database-migrate-your-sql-server-database.md).
* Если осуществляется экспорт из SQL Server как tooAzure toomigration prelude базы данных SQL, см. раздел [перенести tooAzure базы данных SQL Server база данных SQL](sql-database-cloud-migrate.md).
