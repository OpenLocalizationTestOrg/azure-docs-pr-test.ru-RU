---
title: "Код файла событий для базы данных SQL aaaXEvent | Документы Microsoft"
description: "Предоставляет пример двухфазной кода, демонстрирующий hello целевого файла событий в расширенные события в базе данных SQL Azure PowerShell и Transact-SQL. Обязательной частью данного сценария является хранилище Azure."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="dc62e-104">Код целевого файла событий для расширенных событий в Базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="dc62e-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="dc62e-105">Полный пример кода, необходимой для надежного toocapture и сообщения сведений для расширенного события.</span><span class="sxs-lookup"><span data-stu-id="dc62e-105">You want a complete code sample for a robust way toocapture and report information for an extended event.</span></span>

<span data-ttu-id="dc62e-106">В Microsoft SQL Server hello [целевого файла событий](http://msdn.microsoft.com/library/ff878115.aspx) — используется toostore выходов событий в файл с локального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="dc62e-106">In Microsoft SQL Server, hello [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used toostore event outputs into a local hard drive file.</span></span> <span data-ttu-id="dc62e-107">Но таких файлов не tooAzure доступные базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="dc62e-107">But such files are not available tooAzure SQL Database.</span></span> <span data-ttu-id="dc62e-108">Вместо этого мы используем целевой файл событий hello toosupport обслуживания hello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="dc62e-108">Instead we use hello Azure Storage service toosupport hello Event File target.</span></span>

<span data-ttu-id="dc62e-109">В этом разделе представлен пример двухэтапного кода.</span><span class="sxs-lookup"><span data-stu-id="dc62e-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="dc62e-110">PowerShell toocreate контейнер службы хранилища Azure в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="dc62e-110">PowerShell, toocreate an Azure Storage container in hello cloud.</span></span>
* <span data-ttu-id="dc62e-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="dc62e-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="dc62e-112">tooassign hello хранилища Azure контейнер tooan событий целевой файл.</span><span class="sxs-lookup"><span data-stu-id="dc62e-112">tooassign hello Azure Storage container tooan Event File target.</span></span>
  * <span data-ttu-id="dc62e-113">toocreate и запуска сеанса событий hello и т. д.</span><span class="sxs-lookup"><span data-stu-id="dc62e-113">toocreate and start hello event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc62e-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dc62e-114">Prerequisites</span></span>

* <span data-ttu-id="dc62e-115">Учетная запись и подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="dc62e-115">An Azure account and subscription.</span></span> <span data-ttu-id="dc62e-116">Вы можете зарегистрироваться, чтобы получить [бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc62e-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="dc62e-117">Любая база данных, позволяющая создать таблицу.</span><span class="sxs-lookup"><span data-stu-id="dc62e-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="dc62e-118">При необходимости вы можете быстро [создать демонстрационную базу данных **AdventureWorksLT**](sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dc62e-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="dc62e-119">SQL Server Management Studio (ssms.exe), в идеале — последняя ежемесячная версия обновления.</span><span class="sxs-lookup"><span data-stu-id="dc62e-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="dc62e-120">Вы можете скачать последнюю ssms.exe hello из:</span><span class="sxs-lookup"><span data-stu-id="dc62e-120">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="dc62e-121">Статья [Скачивание SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc62e-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="dc62e-122">Для загрузки toohello прямую ссылку.</span><span class="sxs-lookup"><span data-stu-id="dc62e-122">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="dc62e-123">Необходимо иметь hello [модули Azure PowerShell](http://go.microsoft.com/?linkid=9811175) установлен.</span><span class="sxs-lookup"><span data-stu-id="dc62e-123">You must have hello [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="dc62e-124">Hello модули предоставляют команды, такие как - **New AzureStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="dc62e-124">hello modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="dc62e-125">Этап 1. Код PowerShell для контейнера хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="dc62e-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="dc62e-126">Эту команду PowerShell представляет этап 1 образец hello двухфазной кода.</span><span class="sxs-lookup"><span data-stu-id="dc62e-126">This PowerShell is phase 1 of hello two-phase code sample.</span></span>

<span data-ttu-id="dc62e-127">Hello сценарий начинается с команды tooclean после предыдущего возможного и rerunnable.</span><span class="sxs-lookup"><span data-stu-id="dc62e-127">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="dc62e-128">Вставьте сценарий PowerShell hello в простой текстовый редактор, например Notepad.exe и сохраните скрипт hello как файл с расширением hello **.ps1**.</span><span class="sxs-lookup"><span data-stu-id="dc62e-128">Paste hello PowerShell script into a simple text editor such as Notepad.exe, and save hello script as a file with hello extension **.ps1**.</span></span>
2. <span data-ttu-id="dc62e-129">Запустите PowerShell ISE от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="dc62e-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="dc62e-130">Введите в строке приветствия</span><span class="sxs-lookup"><span data-stu-id="dc62e-130">At hello prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="dc62e-131">и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="dc62e-131">and then press Enter.</span></span>
4. <span data-ttu-id="dc62e-132">В PowerShell ISE откройте свой файл **PS1** .</span><span class="sxs-lookup"><span data-stu-id="dc62e-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="dc62e-133">Запустите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="dc62e-133">Run hello script.</span></span>
5. <span data-ttu-id="dc62e-134">сценарий Hello сначала запускает новое окно, в котором необходимо войти в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dc62e-134">hello script first starts a new window in which you log in tooAzure.</span></span>
   
   * <span data-ttu-id="dc62e-135">При повторном запуске скрипта hello без приостановки сеанса, у вас есть удобный вариант закомментирования hello hello **Add-AzureAccount** команды.</span><span class="sxs-lookup"><span data-stu-id="dc62e-135">If you rerun hello script without disrupting your session, you have hello convenient option of commenting out hello **Add-AzureAccount** command.</span></span>

![Интегрированная среда Сценариев PowerShell, Azure использует модуль установлен, готов toorun сценария.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="dc62e-137">Код PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc62e-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


<span data-ttu-id="dc62e-138">Запишите hello несколько именованных значений, которые выводит hello сценарий PowerShell по ее завершении.</span><span class="sxs-lookup"><span data-stu-id="dc62e-138">Take note of hello few named values that hello PowerShell script prints when it ends.</span></span> <span data-ttu-id="dc62e-139">Необходимо изменить эти значения в hello сценарий Transact-SQL, следующее за как этап 2.</span><span class="sxs-lookup"><span data-stu-id="dc62e-139">You must edit those values into hello Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="dc62e-140">Этап 2. Код Transact-SQL, использующий контейнер хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="dc62e-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="dc62e-141">На первом этапе этот образец кода запуска сценария PowerShell toocreate контейнер службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="dc62e-141">In phase 1 of this code sample, you ran a PowerShell script toocreate an Azure Storage container.</span></span>
* <span data-ttu-id="dc62e-142">Далее на этапе 2 hello следующий сценарий Transact-SQL необходимо использовать контейнер hello.</span><span class="sxs-lookup"><span data-stu-id="dc62e-142">Next in phase 2, hello following Transact-SQL script must use hello container.</span></span>

<span data-ttu-id="dc62e-143">Hello сценарий начинается с команды tooclean после предыдущего возможного и rerunnable.</span><span class="sxs-lookup"><span data-stu-id="dc62e-143">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="dc62e-144">Hello сценарий PowerShell на печать несколько именованных значений после его окончания.</span><span class="sxs-lookup"><span data-stu-id="dc62e-144">hello PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="dc62e-145">Toouse сценарий Transact-SQL hello необходимо изменить эти значения.</span><span class="sxs-lookup"><span data-stu-id="dc62e-145">You must edit hello Transact-SQL script toouse those values.</span></span> <span data-ttu-id="dc62e-146">Найти **TODO** точек редактирования hello toolocate сценария hello Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="dc62e-146">Find **TODO** in hello Transact-SQL script toolocate hello edit points.</span></span>

1. <span data-ttu-id="dc62e-147">Откройте SQL Server Management Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="dc62e-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="dc62e-148">Подключение базы данных SQL Azure tooyour базы данных.</span><span class="sxs-lookup"><span data-stu-id="dc62e-148">Connect tooyour Azure SQL Database database.</span></span>
3. <span data-ttu-id="dc62e-149">Щелкните tooopen новой панели запросов.</span><span class="sxs-lookup"><span data-stu-id="dc62e-149">Click tooopen a new query pane.</span></span>
4. <span data-ttu-id="dc62e-150">Вставьте следующий сценарий Transact-SQL в панель запроса hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc62e-150">Paste hello following Transact-SQL script into hello query pane.</span></span>
5. <span data-ttu-id="dc62e-151">Найти каждый **TODO** в hello скрипт и внесите соответствующие изменения hello.</span><span class="sxs-lookup"><span data-stu-id="dc62e-151">Find every **TODO** in hello script and make hello appropriate edits.</span></span>
6. <span data-ttu-id="dc62e-152">Сохраните и запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="dc62e-152">Save, and then run hello script.</span></span>


> [!WARNING]
> <span data-ttu-id="dc62e-153">значение ключа SAS, созданный hello, предшествующий сценарий PowerShell Hello может начинаться с "?" (вопросительный знак).</span><span class="sxs-lookup"><span data-stu-id="dc62e-153">hello SAS key value generated by hello preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="dc62e-154">При использовании ключа SAS hello hello, выполнив сценарий T-SQL, необходимо *удалить hello символа "?"* .</span><span class="sxs-lookup"><span data-stu-id="dc62e-154">When you use hello SAS key in hello following T-SQL script, you must *remove hello leading '?'*.</span></span> <span data-ttu-id="dc62e-155">В противном случае система безопасности может заблокировать ваши действия.</span><span class="sxs-lookup"><span data-stu-id="dc62e-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="dc62e-156">Код Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="dc62e-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


<span data-ttu-id="dc62e-157">В случае целевой hello tooattach при запуске, необходимо остановить и перезапустить сеанс событий hello:</span><span class="sxs-lookup"><span data-stu-id="dc62e-157">If hello target fails tooattach when you run, you must stop and restart hello event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="dc62e-158">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="dc62e-158">Output</span></span>

<span data-ttu-id="dc62e-159">После завершения hello сценарий Transact-SQL, щелкните ячейку в hello **event_data_XML** заголовок столбца.</span><span class="sxs-lookup"><span data-stu-id="dc62e-159">When hello Transact-SQL script completes, click a cell under hello **event_data_XML** column header.</span></span> <span data-ttu-id="dc62e-160">Один из отображенных элементов **<event>** содержит инструкцию UPDATE.</span><span class="sxs-lookup"><span data-stu-id="dc62e-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="dc62e-161">Ниже приведен один из элементов **<event>** , сформированных в процессе тестирования.</span><span class="sxs-lookup"><span data-stu-id="dc62e-161">Here is one **<event>** element that was generated during testing:</span></span>


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


<span data-ttu-id="dc62e-162">Hello предшествующий следующие системы функция tooread hello event_file hello скрипт, использованный для Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="dc62e-162">hello preceding Transact-SQL script used hello following system function tooread hello event_file:</span></span>

* [<span data-ttu-id="dc62e-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="dc62e-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="dc62e-164">Описание дополнительных параметров для hello просмотра данных из расширенных событий доступна на:</span><span class="sxs-lookup"><span data-stu-id="dc62e-164">An explanation of advanced options for hello viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="dc62e-165">Advanced Viewing of Target Data from Extended Events in SQL Server (Дополнительные параметры просмотра целевых данных из расширенных событий в SQL Server)</span><span class="sxs-lookup"><span data-stu-id="dc62e-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a><span data-ttu-id="dc62e-166">Преобразование hello toorun образца кода на сервере SQL Server</span><span class="sxs-lookup"><span data-stu-id="dc62e-166">Converting hello code sample toorun on SQL Server</span></span>

<span data-ttu-id="dc62e-167">Предположим, что требуется, чтобы toorun hello предшествующий пример Transact-SQL в Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dc62e-167">Suppose you wanted toorun hello preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="dc62e-168">Для простоты нужно использование замены toocompletely hello контейнер хранилища Azure с простой файл например **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="dc62e-168">For simplicity, you would want toocompletely replace use of hello Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="dc62e-169">файл Hello записываются в локальный жесткий диск toohello hello компьютера, на котором размещается SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dc62e-169">hello file would be written toohello local hard drive of hello computer that hosts SQL Server.</span></span>
* <span data-ttu-id="dc62e-170">Инструкции Transact-SQL **CREATE MASTER KEY** и **CREATE CREDENTIAL** в этом случае не понадобятся.</span><span class="sxs-lookup"><span data-stu-id="dc62e-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="dc62e-171">В hello **CREATE EVENT SESSION** инструкции в его **ADD TARGET** предложение, замените значение Http hello внесенные слишком**filename =** со строкой полный путь, например  **C:\MyFile.xel**.</span><span class="sxs-lookup"><span data-stu-id="dc62e-171">In hello **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace hello Http value assigned made too**filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="dc62e-172">Учетная запись хранения Azure при этом не нужна.</span><span class="sxs-lookup"><span data-stu-id="dc62e-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="dc62e-173">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="dc62e-173">More information</span></span>

<span data-ttu-id="dc62e-174">Дополнительные сведения об учетных записях и контейнеры в hello службе хранилища Azure см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="dc62e-174">For more info about accounts and containers in hello Azure Storage service, see:</span></span>

* [<span data-ttu-id="dc62e-175">Как toouse хранилища BLOB-объектов из .NET</span><span class="sxs-lookup"><span data-stu-id="dc62e-175">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="dc62e-176">Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них</span><span class="sxs-lookup"><span data-stu-id="dc62e-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="dc62e-177">Работа с корневым контейнером hello</span><span class="sxs-lookup"><span data-stu-id="dc62e-177">Working with hello Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="dc62e-178">Урок 1. Создание хранимой политики доступа и подписанного URL-адреса для контейнера Azure</span><span class="sxs-lookup"><span data-stu-id="dc62e-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="dc62e-179">Урок 2. Создание учетных данных SQL Server с использованием подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="dc62e-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

