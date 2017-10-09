---
title: "пакет bAC aaaImport файла toocreate базы данных Azure SQL | Документы Microsoft"
description: "Создайте базу данных SQL Azure, импортировав BACPAC-файл."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>Импорт файла BACPAC tooa новой базы данных SQL Azure

При необходимости tooimport базу данных из архива или при миграции из другой платформы, можно импортировать схему базы данных hello и данные из [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) файла. BACPAC-файл является ZIP-файл с расширением BACPAC, содержащий hello метаданных и данных из базы данных SQL Server. BACPAC-файл можно импортировать из хранилища BLOB-объектов Azure (только уровня "Стандартный") или из локального хранилища. Скорость импорта toomaximize hello, рекомендуется указать выше службы уровня и уровня производительности, такие как P6 и затем масштабирование toodown соответствующим образом, после успешного импорта hello. Кроме того уровень совместимости базы данных hello после импорта hello основан на уровень совместимости базы данных-источника hello hello. 

> [!IMPORTANT] 
> После переноса tooAzure вашей базы данных база данных SQL, вы можете toooperate hello базы данных на текущем уровне совместимости (уровень 100 для базы данных AdventureWorks2008R2 hello) или на более высоком уровне. Дополнительные сведения о последствиях hello и параметры для работы на уровне совместимости базы данных см. в разделе [уровень совместимости инструкции ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). См. также [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) сведения о дополнительных параметрах уровня базы данных, связанных с toocompatibility уровней.   >

> [!NOTE]
> tooimport BACPAC tooa новую базу данных, необходимо сначала создать логический сервер базы данных SQL Azure. Учебник, показывающий, как SQL Server toomigrate базы данных tooAzure базы данных SQL с помощью SQLPackage, в разделе [миграции базы данных SQL Server](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Импорт из BACPAC-файл с помощью портала Azure

Эта статья содержит инструкции по созданию базы данных Azure SQL из BACPAC-файл хранится в хранилище больших двоичных объектов с помощью hello [портал Azure](https://portal.azure.com). Импорт с использованием hello портал Azure поддерживает импортирования BACPAC-файла из хранилища BLOB-объектов Azure.

Здравствуйте tooimport базы данных с помощью портала Azure, Привет открыть страницу для базы данных и нажмите кнопку **импорта** на панели инструментов hello. Укажите учетную запись хранилища hello и контейнер и выберите требуется tooimport hello BACPAC-файл. Выберите размер hello hello новой базы данных (обычно Здравствуйте, же, как источник) и укажите учетные данные SQL Server назначения hello.  

   ![Импорт базы данных](./media/sql-database-import/import.png)

Ход выполнения hello toomonitor hello операции импорта, откройте страницу приветствия hello логический сервер содержащего hello базы. Прокрутите список вниз слишком**операции** и нажмите кнопку **импорта и экспорта** журнала.

### <a name="monitor-hello-progress-of-an-import-operation"></a>Отслеживать ход выполнения операции импорта hello

Ход выполнения hello toomonitor hello операции импорта, откройте страницу приветствия hello логический сервер в какой hello импортировать базу данных импортирован. Прокрутите список вниз слишком**операции** и нажмите кнопку **импорта и экспорта** журнала.
   
   ![Импорт](./media/sql-database-import/import-history.png) ![Состояние импорта](./media/sql-database-import/import-status.png)

База данных hello tooverify находится на сервере hello, щелкните **баз данных SQL** и убедитесь в новую базу данных hello **Online**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>Импорт из BACPAC-файла с помощью SQLPackage

tooimport SQL базы данных с помощью hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) программы командной строки, в разделе [импортировать параметры и свойства](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). Hello программу SQLPackage поставляется с hello последние версии [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) и [SQL Server Data Tools для Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), или hello последнюю версию можно загрузить [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) непосредственно из hello Microsoft центре загрузки.

Рекомендуется использовать hello hello программу SQLPackage для обеспечения масштабирования и производительности в большинстве рабочих средах. SQL Server группа консультантов по блог о миграции с помощью BACPAC-файлов в разделе [миграции с SQL Server tooAzure базы данных SQL с помощью файлов BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

См. следующую команду SQLPackage пример сценария для как hello tooimport hello **AdventureWorks2008R2** базы данных из локального хранилища tooan базы данных SQL Azure логический сервер, называется **mynewserver20170403** в этом примере. Этот сценарий показывает создание новой базы данных с именем hello **myMigratedDatabase**, с уровня обслуживания **Premium**и цель обслуживания **P6**. Измените эти значения как соответствующие tooyour среды.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![Импорт с помощью SqlPackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Логический сервер базы данных SQL Azure прослушивает порт 1433. При попытке tooconnect tooan базы данных SQL Azure логического сервера внутри корпоративного брандмауэра, этот порт должен быть открыт в hello корпоративного брандмауэра для подключения к toosuccessfully вы.
>

В этом примере показано, как tooimport базу данных с помощью SqlPackage.exe с универсальной проверки подлинности Active Directory:

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>Импорт из BACPAC-файла с помощью PowerShell

Используйте hello [New AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) toosubmit командлет import toohello запрос базы данных служба базы данных SQL Azure. В зависимости от размера базы данных hello hello операции импорта может занять некоторое время toocomplete.

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

состояние hello toocheck hello импортировать запрос, использовать hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) командлета. При выполнении этого сразу же после hello запрос обычно возвращает **состояние: выполняется**. При появлении **состояния: успешно** hello Импорт завершен.

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
Еще один пример сценария приведен в разделе [Импорт базы данных из BACPAC-файла](scripts/sql-database-import-from-bacpac-powershell.md).

## <a name="next-steps"></a>Дальнейшие действия
* toolearn tooconnect tooand запрос импортируемой базы данных SQL в статье [подключать tooSQL базы данных SQL Server Management Studio и выполнить пробный запрос T-SQL](sql-database-connect-query-ssms.md).
* SQL Server группа консультантов по блог о миграции с помощью BACPAC-файлов в разделе [миграции с SQL Server tooAzure базы данных SQL с помощью файлов BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Обсуждение hello всего процесса SQL Server базы данных миграции, включая рекомендации по повышению производительности, в разделе [перенести tooAzure базы данных SQL Server база данных SQL](sql-database-cloud-migrate.md).



