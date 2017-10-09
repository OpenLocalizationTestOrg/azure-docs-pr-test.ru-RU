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
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a>Код целевого файла событий для расширенных событий в Базе данных SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Полный пример кода, необходимой для надежного toocapture и сообщения сведений для расширенного события.

В Microsoft SQL Server hello [целевого файла событий](http://msdn.microsoft.com/library/ff878115.aspx) — используется toostore выходов событий в файл с локального жесткого диска. Но таких файлов не tooAzure доступные базы данных SQL. Вместо этого мы используем целевой файл событий hello toosupport обслуживания hello хранилища Azure.

В этом разделе представлен пример двухэтапного кода.

* PowerShell toocreate контейнер службы хранилища Azure в облаке hello.
* Transact-SQL:
  
  * tooassign hello хранилища Azure контейнер tooan событий целевой файл.
  * toocreate и запуска сеанса событий hello и т. д.

## <a name="prerequisites"></a>Предварительные требования

* Учетная запись и подписка Azure. Вы можете зарегистрироваться, чтобы получить [бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/).
* Любая база данных, позволяющая создать таблицу.
  
  * При необходимости вы можете быстро [создать демонстрационную базу данных **AdventureWorksLT**](sql-database-get-started.md).
* SQL Server Management Studio (ssms.exe), в идеале — последняя ежемесячная версия обновления. 
  Вы можете скачать последнюю ssms.exe hello из:
  
  * Статья [Скачивание SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Для загрузки toohello прямую ссылку.](http://go.microsoft.com/fwlink/?linkid=616025)
* Необходимо иметь hello [модули Azure PowerShell](http://go.microsoft.com/?linkid=9811175) установлен.
  
  * Hello модули предоставляют команды, такие как - **New AzureStorageAccount**.

## <a name="phase-1-powershell-code-for-azure-storage-container"></a>Этап 1. Код PowerShell для контейнера хранилища Azure

Эту команду PowerShell представляет этап 1 образец hello двухфазной кода.

Hello сценарий начинается с команды tooclean после предыдущего возможного и rerunnable.

1. Вставьте сценарий PowerShell hello в простой текстовый редактор, например Notepad.exe и сохраните скрипт hello как файл с расширением hello **.ps1**.
2. Запустите PowerShell ISE от имени администратора.
3. Введите в строке приветствия<br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/>и нажмите клавишу ВВОД.
4. В PowerShell ISE откройте свой файл **PS1** . Запустите сценарий hello.
5. сценарий Hello сначала запускает новое окно, в котором необходимо войти в tooAzure.
   
   * При повторном запуске скрипта hello без приостановки сеанса, у вас есть удобный вариант закомментирования hello hello **Add-AzureAccount** команды.

![Интегрированная среда Сценариев PowerShell, Azure использует модуль установлен, готов toorun сценария.][30_powershell_ise]


### <a name="powershell-code"></a>Код PowerShell

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


Запишите hello несколько именованных значений, которые выводит hello сценарий PowerShell по ее завершении. Необходимо изменить эти значения в hello сценарий Transact-SQL, следующее за как этап 2.

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a>Этап 2. Код Transact-SQL, использующий контейнер хранилища Azure

* На первом этапе этот образец кода запуска сценария PowerShell toocreate контейнер службы хранилища Azure.
* Далее на этапе 2 hello следующий сценарий Transact-SQL необходимо использовать контейнер hello.

Hello сценарий начинается с команды tooclean после предыдущего возможного и rerunnable.

Hello сценарий PowerShell на печать несколько именованных значений после его окончания. Toouse сценарий Transact-SQL hello необходимо изменить эти значения. Найти **TODO** точек редактирования hello toolocate сценария hello Transact-SQL.

1. Откройте SQL Server Management Studio (ssms.exe).
2. Подключение базы данных SQL Azure tooyour базы данных.
3. Щелкните tooopen новой панели запросов.
4. Вставьте следующий сценарий Transact-SQL в панель запроса hello hello.
5. Найти каждый **TODO** в hello скрипт и внесите соответствующие изменения hello.
6. Сохраните и запустите скрипт hello.


> [!WARNING]
> значение ключа SAS, созданный hello, предшествующий сценарий PowerShell Hello может начинаться с "?" (вопросительный знак). При использовании ключа SAS hello hello, выполнив сценарий T-SQL, необходимо *удалить hello символа "?"* . В противном случае система безопасности может заблокировать ваши действия.


### <a name="transact-sql-code"></a>Код Transact-SQL

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


В случае целевой hello tooattach при запуске, необходимо остановить и перезапустить сеанс событий hello:

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a>Выходные данные

После завершения hello сценарий Transact-SQL, щелкните ячейку в hello **event_data_XML** заголовок столбца. Один из отображенных элементов **<event>** содержит инструкцию UPDATE.

Ниже приведен один из элементов **<event>** , сформированных в процессе тестирования.


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


Hello предшествующий следующие системы функция tooread hello event_file hello скрипт, использованный для Transact-SQL:

* [sys.fn_xe_file_target_read_file (Transact-SQL)](http://msdn.microsoft.com/library/cc280743.aspx)

Описание дополнительных параметров для hello просмотра данных из расширенных событий доступна на:

* [Advanced Viewing of Target Data from Extended Events in SQL Server (Дополнительные параметры просмотра целевых данных из расширенных событий в SQL Server)](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a>Преобразование hello toorun образца кода на сервере SQL Server

Предположим, что требуется, чтобы toorun hello предшествующий пример Transact-SQL в Microsoft SQL Server.

* Для простоты нужно использование замены toocompletely hello контейнер хранилища Azure с простой файл например **C:\myeventdata.xel**. файл Hello записываются в локальный жесткий диск toohello hello компьютера, на котором размещается SQL Server.
* Инструкции Transact-SQL **CREATE MASTER KEY** и **CREATE CREDENTIAL** в этом случае не понадобятся.
* В hello **CREATE EVENT SESSION** инструкции в его **ADD TARGET** предложение, замените значение Http hello внесенные слишком**filename =** со строкой полный путь, например  **C:\MyFile.xel**.
  
  * Учетная запись хранения Azure при этом не нужна.

## <a name="more-information"></a>Дополнительные сведения

Дополнительные сведения об учетных записях и контейнеры в hello службе хранилища Azure см. в разделе:

* [Как toouse хранилища BLOB-объектов из .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [Работа с корневым контейнером hello](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [Урок 1. Создание хранимой политики доступа и подписанного URL-адреса для контейнера Azure](http://msdn.microsoft.com/library/dn466430.aspx)
  * [Урок 2. Создание учетных данных SQL Server с использованием подписанного URL-адреса](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

