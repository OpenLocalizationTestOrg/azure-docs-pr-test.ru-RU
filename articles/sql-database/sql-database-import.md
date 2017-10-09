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
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="60ae8-103">Импорт файла BACPAC tooa новой базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="60ae8-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="60ae8-104">При необходимости tooimport базу данных из архива или при миграции из другой платформы, можно импортировать схему базы данных hello и данные из [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) файла.</span><span class="sxs-lookup"><span data-stu-id="60ae8-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="60ae8-105">BACPAC-файл является ZIP-файл с расширением BACPAC, содержащий hello метаданных и данных из базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="60ae8-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="60ae8-106">BACPAC-файл можно импортировать из хранилища BLOB-объектов Azure (только уровня "Стандартный") или из локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="60ae8-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="60ae8-107">Скорость импорта toomaximize hello, рекомендуется указать выше службы уровня и уровня производительности, такие как P6 и затем масштабирование toodown соответствующим образом, после успешного импорта hello.</span><span class="sxs-lookup"><span data-stu-id="60ae8-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="60ae8-108">Кроме того уровень совместимости базы данных hello после импорта hello основан на уровень совместимости базы данных-источника hello hello.</span><span class="sxs-lookup"><span data-stu-id="60ae8-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="60ae8-109">После переноса tooAzure вашей базы данных база данных SQL, вы можете toooperate hello базы данных на текущем уровне совместимости (уровень 100 для базы данных AdventureWorks2008R2 hello) или на более высоком уровне.</span><span class="sxs-lookup"><span data-stu-id="60ae8-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="60ae8-110">Дополнительные сведения о последствиях hello и параметры для работы на уровне совместимости базы данных см. в разделе [уровень совместимости инструкции ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="60ae8-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="60ae8-111">См. также [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) сведения о дополнительных параметрах уровня базы данных, связанных с toocompatibility уровней.</span><span class="sxs-lookup"><span data-stu-id="60ae8-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="60ae8-112">tooimport BACPAC tooa новую базу данных, необходимо сначала создать логический сервер базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="60ae8-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="60ae8-113">Учебник, показывающий, как SQL Server toomigrate базы данных tooAzure базы данных SQL с помощью SQLPackage, в разделе [миграции базы данных SQL Server](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="60ae8-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="60ae8-114">Импорт из BACPAC-файл с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="60ae8-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="60ae8-115">Эта статья содержит инструкции по созданию базы данных Azure SQL из BACPAC-файл хранится в хранилище больших двоичных объектов с помощью hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60ae8-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="60ae8-116">Импорт с использованием hello портал Azure поддерживает импортирования BACPAC-файла из хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="60ae8-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="60ae8-117">Здравствуйте tooimport базы данных с помощью портала Azure, Привет открыть страницу для базы данных и нажмите кнопку **импорта** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="60ae8-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="60ae8-118">Укажите учетную запись хранилища hello и контейнер и выберите требуется tooimport hello BACPAC-файл.</span><span class="sxs-lookup"><span data-stu-id="60ae8-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="60ae8-119">Выберите размер hello hello новой базы данных (обычно Здравствуйте, же, как источник) и укажите учетные данные SQL Server назначения hello.</span><span class="sxs-lookup"><span data-stu-id="60ae8-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![Импорт базы данных](./media/sql-database-import/import.png)

<span data-ttu-id="60ae8-121">Ход выполнения hello toomonitor hello операции импорта, откройте страницу приветствия hello логический сервер содержащего hello базы.</span><span class="sxs-lookup"><span data-stu-id="60ae8-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="60ae8-122">Прокрутите список вниз слишком**операции** и нажмите кнопку **импорта и экспорта** журнала.</span><span class="sxs-lookup"><span data-stu-id="60ae8-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="60ae8-123">Отслеживать ход выполнения операции импорта hello</span><span class="sxs-lookup"><span data-stu-id="60ae8-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="60ae8-124">Ход выполнения hello toomonitor hello операции импорта, откройте страницу приветствия hello логический сервер в какой hello импортировать базу данных импортирован.</span><span class="sxs-lookup"><span data-stu-id="60ae8-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="60ae8-125">Прокрутите список вниз слишком**операции** и нажмите кнопку **импорта и экспорта** журнала.</span><span class="sxs-lookup"><span data-stu-id="60ae8-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="60ae8-126">![Импорт](./media/sql-database-import/import-history.png) ![Состояние импорта](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="60ae8-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="60ae8-127">База данных hello tooverify находится на сервере hello, щелкните **баз данных SQL** и убедитесь в новую базу данных hello **Online**.</span><span class="sxs-lookup"><span data-stu-id="60ae8-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="60ae8-128">Импорт из BACPAC-файла с помощью SQLPackage</span><span class="sxs-lookup"><span data-stu-id="60ae8-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="60ae8-129">tooimport SQL базы данных с помощью hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) программы командной строки, в разделе [импортировать параметры и свойства](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="60ae8-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="60ae8-130">Hello программу SQLPackage поставляется с hello последние версии [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) и [SQL Server Data Tools для Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), или hello последнюю версию можно загрузить [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) непосредственно из hello Microsoft центре загрузки.</span><span class="sxs-lookup"><span data-stu-id="60ae8-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="60ae8-131">Рекомендуется использовать hello hello программу SQLPackage для обеспечения масштабирования и производительности в большинстве рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="60ae8-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="60ae8-132">SQL Server группа консультантов по блог о миграции с помощью BACPAC-файлов в разделе [миграции с SQL Server tooAzure базы данных SQL с помощью файлов BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="60ae8-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="60ae8-133">См. следующую команду SQLPackage пример сценария для как hello tooimport hello **AdventureWorks2008R2** базы данных из локального хранилища tooan базы данных SQL Azure логический сервер, называется **mynewserver20170403** в этом примере.</span><span class="sxs-lookup"><span data-stu-id="60ae8-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="60ae8-134">Этот сценарий показывает создание новой базы данных с именем hello **myMigratedDatabase**, с уровня обслуживания **Premium**и цель обслуживания **P6**.</span><span class="sxs-lookup"><span data-stu-id="60ae8-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="60ae8-135">Измените эти значения как соответствующие tooyour среды.</span><span class="sxs-lookup"><span data-stu-id="60ae8-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![Импорт с помощью SqlPackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="60ae8-137">Логический сервер базы данных SQL Azure прослушивает порт 1433.</span><span class="sxs-lookup"><span data-stu-id="60ae8-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="60ae8-138">При попытке tooconnect tooan базы данных SQL Azure логического сервера внутри корпоративного брандмауэра, этот порт должен быть открыт в hello корпоративного брандмауэра для подключения к toosuccessfully вы.</span><span class="sxs-lookup"><span data-stu-id="60ae8-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="60ae8-139">В этом примере показано, как tooimport базу данных с помощью SqlPackage.exe с универсальной проверки подлинности Active Directory:</span><span class="sxs-lookup"><span data-stu-id="60ae8-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="60ae8-140">Импорт из BACPAC-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="60ae8-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="60ae8-141">Используйте hello [New AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) toosubmit командлет import toohello запрос базы данных служба базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="60ae8-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="60ae8-142">В зависимости от размера базы данных hello hello операции импорта может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="60ae8-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

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

<span data-ttu-id="60ae8-143">состояние hello toocheck hello импортировать запрос, использовать hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) командлета.</span><span class="sxs-lookup"><span data-stu-id="60ae8-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="60ae8-144">При выполнении этого сразу же после hello запрос обычно возвращает **состояние: выполняется**.</span><span class="sxs-lookup"><span data-stu-id="60ae8-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="60ae8-145">При появлении **состояния: успешно** hello Импорт завершен.</span><span class="sxs-lookup"><span data-stu-id="60ae8-145">When you see **Status: Succeeded** hello import is complete.</span></span>

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
<span data-ttu-id="60ae8-146">Еще один пример сценария приведен в разделе [Импорт базы данных из BACPAC-файла](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="60ae8-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60ae8-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60ae8-147">Next steps</span></span>
* <span data-ttu-id="60ae8-148">toolearn tooconnect tooand запрос импортируемой базы данных SQL в статье [подключать tooSQL базы данных SQL Server Management Studio и выполнить пробный запрос T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="60ae8-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="60ae8-149">SQL Server группа консультантов по блог о миграции с помощью BACPAC-файлов в разделе [миграции с SQL Server tooAzure базы данных SQL с помощью файлов BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="60ae8-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="60ae8-150">Обсуждение hello всего процесса SQL Server базы данных миграции, включая рекомендации по повышению производительности, в разделе [перенести tooAzure базы данных SQL Server база данных SQL](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="60ae8-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



