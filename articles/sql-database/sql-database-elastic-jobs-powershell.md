---
title: "aaaCreate эластичной заданий с помощью PowerShell и управление ими | Документы Microsoft"
description: "PowerShell используются пулы toomanage базы данных SQL Azure"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>Создание заданий обработки эластичных баз данных базы данных SQL и управление ими с помощью PowerShell (предварительная версия)

Hello API-интерфейсов PowerShell для **заданий эластичных баз данных** (в предварительной версии), позволяют определить группы баз данных, для которых они будут выполняться. В этой статье показано, как toocreate и управление ими **заданий эластичных баз данных** с помощью командлетов PowerShell. См. статью [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Предварительные требования
* Подписка Azure. Зарегистрироваться в пробной версии, которая доступна бесплатно в течение одного месяца, можно [здесь](https://azure.microsoft.com/pricing/free-trial/).
* Набор баз данных, созданных с помощью средств hello эластичной базы данных. См. статью [Приступая к работе с инструментами эластичных баз данных](sql-database-elastic-scale-get-started.md).
* Azure PowerShell. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
* **Задания обработки эластичных баз данных.** Пакет PowerShell. См. статью [Обзор установки заданий обработки эластичных баз данных](sql-database-elastic-jobs-service-installation.md).

### <a name="select-your-azure-subscription"></a>Выбор подписки Azure
tooselect hello подписки требуется идентификатор подписки (**- SubscriptionId**) или имя подписки (**- SubscriptionName**). Если у вас несколько подписок можно запустить hello **Get AzureRmSubscription** командлета и скопируйте hello требуемого hello результирующий набор сведения о подписках. После получения сведений о подписке, запустите следующий командлет tooset hello этой подписки по умолчанию hello, Здравствуйте целевой объект для создания и управления заданиями, а именно:

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

Hello [интегрированной среды Сценариев PowerShell](https://technet.microsoft.com/library/dd315244.aspx) рекомендуется для использования toodevelop и выполнения скриптов PowerShell для задания hello эластичной базы данных.

## <a name="elastic-database-jobs-objects"></a>Объекты заданий обработки эластичных баз данных
Здравствуйте, следующие таблице приводится список всех типов hello объекта из **заданий эластичных баз данных** вместе с ее описание и соответствующие API-интерфейсов PowerShell.

<table style="width:100%">
  <tr>
    <th>Тип объекта</th>
    <th>Описание</th>
    <th>Связанные API-интерфейсы PowerShell</th>
  </tr>
  <tr>
    <td>Учетные данные</td>
    <td>Имя пользователя и пароль toouse при подключении toodatabases для выполнения сценариев или приложений из файлов DACPAC. <p>Hello пароль шифруется перед отправкой tooand хранение в базе данных hello заданий эластичных баз данных.  Hello пароль будет расшифрован при hello службы заданий эластичных баз данных по третьему hello создан и загружен с hello сценария установки.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>New-AzureSqlJobCredential</p><p>Set-AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>Скрипт</td>
    <td>Toobe сценарий Transact-SQL, используемая для выполнения в нескольких базах данных.  Hello скрипт должен быть идемпотентными созданные toobe, так как hello служба будет повторять выполнение скрипта hello после сбоев.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">Приложения уровня данных </a> пакета toobe применяется в нескольких базах данных.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>Целевая база данных</td>
    <td>Базы данных и сервера имя указывающего tooan базы данных SQL Azure.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>Целевая карта сегментов</td>
    <td>Сочетание целевой базы данных и toobe учетных данных используется toodetermine информации, сохраняемой в карте сегментов эластичной базы данных.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    <p>Set-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Целевая пользовательская коллекция</td>
    <td>Заданная группа toocollectively баз данных используется для выполнения.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Целевая дочерняя пользовательская коллекция</td>
    <td>Целевая база данных, на которую ссылается пользовательская коллекция.</td>
    <td>
    <p>Add-AzureSqlJobChildTarget</p>
    <p>Remove-AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>Задание</td>
    <td>
    <p>Определение параметров для задания, которое может быть выполнения используется tootrigger или toofulfill расписание.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>New-AzureSqlJob</p>
    <p>Set-AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>Выполнение заданий</td>
    <td>
    <p>Контейнер toofulfill необходимые задачи, выполнение сценария или применения целевой tooa пакета DAC, используя учетные данные для подключения к базе данных с ошибками обрабатываются в соответствии tooan выполнения политики.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Выполнение задач</td>
    <td>
    <p>Одна единица работы toofulfill задания.</p>
    <p>Если задание не может toosuccessfully выполнение, hello результирующее сообщение об исключении будут регистрироваться и нового сопоставления задание будет создавать и выполнять в соответствии toohello указан политику выполнения.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Политика выполнения заданий</td>
    <td>
    <p>Управляет временем ожидания выполнения заданий, максимальными количествами повторных попыток и интервалами между ними.</p>
    <p>Задания обработки эластичных баз данных включают стандартную политику выполнения, которая вызывает практически неограниченное число повторных попыток в случае сбоя задач с экспоненциально растущим интервалом между ними.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>New-AzureSqlJobExecutionPolicy</p>
    <p>Set-AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>Расписание</td>
    <td>
    <p>Время от спецификация месте tootake выполнения повторяющегося интервала или за один раз.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>New-AzureSqlJobSchedule</p>
    <p>Set-AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>Триггеры заданий</td>
    <td>
    <p>Сопоставление между задания и расписания toohello в соответствии с выполнением задания tootrigger расписания.</p>
    </td>
    <td>
    <p>New-AzureSqlJobTrigger</p>
    <p>Remove-AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>Поддерживаемые типы групп заданий обработки эластичных баз данных
Задание Hello выполняет скрипты Transact-SQL (T-SQL) или приложение файлов DACPAC между несколькими базами данных. Задание — отправленной toobe выполняется через группу баз данных, задание hello» расширяет «hello в дочерние задания, где каждое из которых выполняет hello запросить выполнение на одной базы данных в группе hello. 

Вы можете создать группу одного из двух типов. 

* [Карта сегментов](sql-database-elastic-scale-shard-map-management.md) группы: когда задание отправленной tootarget карта сегментов, задание hello запрашивает toodetermine карты сегментов hello свой текущий набор сегментов, а затем создает дочерние задания для каждого сегмента в карте сегментов hello.
* Группа «Пользовательская коллекция»: определяемый пользователем набор баз данных. При задания предназначен для настраиваемой коллекции, он создает дочерние задания для каждой базы данных в настоящее время в пользовательской коллекции hello.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>hello tooset подключения заданий эластичных баз данных
Соединение должно toobe Настройка toohello заданий *базы данных системы управления* hello toousing предыдущего задания API-интерфейсы. Запустить этот командлет инициирует toopop окно учетных данных, копирование запроса hello имя пользователя и пароль, созданный при установке заданий эластичных баз данных. Во всех примерах из этого раздела предполагается, что первый этап уже выполнен.

Откройте подключение toohello эластичной базы данных:

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Зашифрованные учетные данные в рамках задания hello эластичной базы данных
Учетные данные базы данных могут быть вставлены в заданий hello *базы данных системы управления* с ее пароль шифрования. Это toostore необходимые учетные данные tooenable заданий toobe выполнен на более позднее время (с помощью расписания заданий).

Шифрование работает через сертификат, созданный как часть сценария установки hello. Создает скрипт установки Hello и передачи сертификата hello в hello Azure облачной службы для расшифровки hello хранятся зашифрованные пароли. Hello позже для облачной службы Azure сохраняет hello открытый ключ в рамках задания hello *базы данных системы управления* без необходимости hello сертификата, который позволяет hello PowerShell API или классический портал Azure интерфейс tooencrypt указанного пароля toobe на локальном компьютере.

пароли учетных данных Hello зашифровано и от пользователей с объектами заданий базы данных tooElastic доступ только для чтения. Однако существует возможность пользователю-злоумышленнику с tooextract объектов пароль для доступа на чтение запись tooElastic заданий базы данных. Учетные данные, разработанной toobe повторно между выполнениями задания. Учетные данные передаются tootarget баз данных при выполнении подключения. В настоящее время нет никаких ограничений на целевые hello базы данных, используемый для каждой учетной записи, злонамеренный пользователь может добавить целевой объект базы данных для базы данных в группе управления hello злонамеренный пользователь. Hello пользователь впоследствии удалось запустить задания, предназначенные для этой базы данных toogain hello учетных данных пароля.

При работе с заданиями обработки эластичных баз данных мы рекомендуем использовать такие меры безопасности.

* Ограничить использование hello API-интерфейсы tootrusted лиц.
* Учетные данные должны иметь hello наименьших привилегий необходимые tooperform hello рабочее задание.  Дополнительные сведения см. на сайте MSDN в статье [Проверка прав доступа и разрешений в SQL Server](https://msdn.microsoft.com/library/bb669084.aspx).

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate зашифрованных учетных данных для выполнения заданий по базам данных
toocreate новый шифрования учетных данных, hello [ **командлета Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) запрашивает имя пользователя и пароль, который может быть передан toohello [ **New AzureSqlJobCredential командлет**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>учетные данные tooupdate
При изменении паролей, использовать hello [ **командлета Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) и набор hello **CredentialName** параметра.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine целевой карты сегментов эластичной базы данных
tooexecute задания для всех баз данных в наборе сегментов (созданные с помощью [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md)), использовать в качестве целевой базы данных hello карты сегментов. Для этого примера требуются сегментированных приложений, созданных с помощью клиентской библиотеки hello эластичной базы данных. См. статью [Приступая к работе с инструментами эластичных баз данных](sql-database-elastic-scale-get-started.md).

База данных диспетчера карты сегментов Hello должен быть задан как целевой базы данных и затем hello конкретных сегментов карты должен быть указан как целевой объект.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Создание сценария T-SQL для выполнения в нескольких базах данных
При создании скриптов T-SQL для выполнения, настоятельно рекомендуется toobuild их toobe [идемпотентными](https://en.wikipedia.org/wiki/Idempotence) и устойчивы к сбоям. При каждом выполнении возникнет ошибка, независимо от классификации hello сбоя hello заданий эластичных баз данных будет повторять попытки выполнения сценария.

Используйте hello [ **командлет New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate и сохранить скрипт для выполнения и задайте hello **- ContentName** и **- CommandText**параметры.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>Создание нового сценария из файла
Если hello скрипт T-SQL, определенные в файле, используйте этот скрипт hello tooimport:

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>скрипт tooupdate T-SQL для выполнения в нескольких базах данных
Этот сценарий обновляет PowerShell hello текст команды T-SQL для существующего скрипта.

Следующие переменные tooreflect hello hello набор требуемого набора toobe Определение сценария:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>существующий скрипт определения hello tooan tooupdate
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate tooexecute задания скрипта по карте сегментов
Приведенный ниже сценарий PowerShell запускает задание, которое выполнит сценарий в каждом сегменте карты с динамическим масштабированием.

Следующие переменные tooreflect hello hello набор требуемого скрипта и целевой:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute задания
Приведенный ниже сценарий PowerShell выполняет существующее задание.

Обновите следующие переменной tooreflect задания требуемого hello имя toohave выполнена hello:

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>состояние hello tooretrieve выполнения одного задания
Используйте hello [ **командлет Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) и набор hello **JobExecutionId** параметр tooview hello состояние выполнения задания.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

Используйте hello же **Get AzureSqlJobExecution** командлет с hello **IncludeChildren** параметр tooview hello состояние выполнения дочерние задания, а именно: hello определенное состояние при каждом выполнении задания для каждой База данных целевой заданием hello.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>состояние hello tooview между несколькими выполнениями задания
Hello [ **командлет Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) имеет несколько необязательных параметров, которые можно использовать toodisplay выполнения нескольких заданий, фильтрации с помощью hello предоставленных параметров. Hello ниже показаны некоторые из способов hello toouse Get AzureSqlJobExecution:

Получение сведений о выполнении всех активных заданий верхнего уровня:

    Get-AzureSqlJobExecution

Получение сведений о выполнении всех заданий верхнего уровня, включая неактивные задания:

    Get-AzureSqlJobExecution -IncludeInactive

Получение состояния выполнения всех дочерних заданий, включая неактивные, по указанному идентификатору выполнения задания:

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

Получение состояния выполнения всех заданий, созданных с помощью сочетания расписания и задания, включая неактивные:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

Получение сведения обо всех заданиях в указанной карте сегментов, включая неактивные:

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Получение сведения обо всех заданиях в указанном пользовательском семействе, включая неактивные:

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Получаете список hello завершений задач во время выполнения конкретного задания:

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

Получение сведений о выполнении задачи:

Следующий сценарий PowerShell Hello может быть сведения hello используется tooview выполнения задачи задания, что особенно полезно при отладке ошибок выполнения.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>tooretrieve сбоев в рамках выполнения задачи задания
Hello **JobTaskExecution объекта** включает свойство для hello жизненного цикла задачи hello вместе со свойством сообщения. Если произошел сбой выполнения задания задачи: hello жизненного цикла будет установлено слишком*сбой* и будет установлено свойство сообщение hello toohello результирующее сообщение об исключении и его стека. Если задание завершилось неудачей, это tooview важные сведения hello задания задач, которые не были успешно выполнены для данного задания.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>toowait для выполнения задания toocomplete
Следующий сценарий PowerShell Hello может быть toowait используется для задания задач toocomplete:

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a>Создание пользовательской политики выполнения
Задания обработки эластичных баз данных поддерживают создание пользовательских политик выполнения, которые можно применять при запуске заданий.

В настоящий момент политики выполнения позволяют задать следующее:

* Имя: Идентификатор для политики выполнения hello.
* Время ожидания задания: общее время до отмены задания службой заданий обработки эластичных баз данных.
* Начальный интервал повторных попыток: Toowait интервал перед первой повторной попытки.
* Максимальный интервал повторных попыток: Лимит в размере toouse интервалы повтора.
* Коэффициент отсрочки интервал повторных попыток: Коэффициент используется toocalculate hello следующий интервал между повторными попытками.  Hello используется следующая формула: (начальной интервал повтора) * Math.pow ((интервал отсрочки коэффициент) (число повторов) - 2). 
* Максимальное попыток: hello максимальное число tooperform попыток повтора в задании.

политика выполнения по умолчанию Hello использует hello следующие значения:

* Имя: политика выполнения по умолчанию
* Время ожидания задания: 1 неделя
* Исходный интервал повторных попыток: 100 миллисекунд.
* Максимальный интервал повторных попыток: 30 минут
* Коэффициент интервала повторных попыток: 2
* Максимальное число попыток: 2 147 483 647

Создайте политику выполнения требуемого hello.

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>Изменение пользовательской политики выполнения
Обновление hello требуемого tooupdate политики выполнения:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>Отмена задания
Задания обработки эластичных баз данных поддерживают запросы на отмену заданий.  Если заданий эластичных баз данных обнаруживает запрос отмены задания, выполняемые, он попытается toostop hello задания.

Служба заданий обработки эластичных баз данных может выполнить отмену двумя разными способами:

1. Отмена задачи в данный момент: Если Отмена обнаруживается во время задачи, будет предпринята попытка отмены в hello аспектом задачу hello в данный момент.  Например: в случае долго выполняющийся запрос, выполняемый в настоящее время при попытке отмены будет попытка toocancel hello запроса.
2. Отмена попытки выполнения задачи: отмены в случае обнаружения потоком управления hello перед запуском задачи для выполнения потока управления hello избежать запуска задачи hello и объявить hello запрос отменен.

При поступлении запроса отмены задания для задания родительского запроса отмены hello будет обрабатываться родительским заданием hello и всех его дочерние задания.

запрос отмены toosubmit использовать hello [ **командлет Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) и набор hello **JobExecutionId** параметра.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>toodelete задания и журнал заданий асинхронно
Задания обработки эластичных баз данных поддерживают асинхронное удаление заданий. Задания могут быть помечены для удаления и hello система удаляет задание hello и ее журнал заданий после завершения выполнения всех заданий для задания hello. Hello системы не будет автоматически отменить выполнение активных заданий.  

Вызвать [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel выполнение активных заданий.

Удаление задания tootrigger, используйте hello [ **командлет Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) и набор hello **JobName** параметра.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>toocreate целевой объект пользовательские базы данных
Вы можете определять целевые объекты пользовательской базы данных для выполнения напрямую или для включения в группу пользовательских баз данных. Например так как **эластичные пулы** , еще не поддерживается напрямую с помощью API-интерфейсов PowerShell, можно создать пользовательские базы данных целевой объект и целевой объект коллекции пользовательские базы данных, который включает все базы данных hello в пуле hello.

Задайте следующие переменные tooreflect hello требуемого базы данных сведения hello.

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate целевой объект коллекции пользовательские базы данных
Используйте hello [ **New AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine командлет выполнение пользовательской базе данных коллекции целевых объектов tooenable несколько целевых объектов базы данных. После создания группы базы данных можно связать с hello пользовательской коллекции целевой базы данных.

Следующие переменные tooreflect hello hello набор требуемого пользовательской коллекции целевую конфигурацию:

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>целевой объект коллекции tooadd баз данных tooa пользовательские базы данных
использовать tooadd базы данных tooa определенной пользовательской коллекции hello [ **добавить AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) командлета.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Просмотрите hello баз данных в пользовательской базе данных целевого объекта коллекции
Используйте hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) командлет tooretrieve hello дочерних баз данных в пользовательской базе данных целевого объекта коллекции. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Создать сценарий tooexecute задания для целевого объекта коллекции пользовательские базы данных
Используйте hello [ **New AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate командлет задания для группы баз данных, определенных в пользовательской базе данных целевого объекта коллекции. Заданий эластичных баз данных будет расширяться hello задания на несколько дочерних каждой соответствующей tooa базы данных, связанная с целевой объект коллекции hello пользовательские базы данных и убедитесь, что hello сценарий выполняется для каждой базы данных. Опять же очень важно, скрипты являются устойчивыми tooretries toobe идемпотентными.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>Сбор данных из нескольких баз данных
Можно использовать задание tooexecute запрос между несколькими базами данных и отправки hello результаты tooa конкретной таблицы. можно запрашивать таблицы Hello после toosee hello hello фактов запроса результаты из каждой базы данных. Это предоставляет асинхронный метод tooexecute запрос через несколько баз данных. После неудачной попытки автоматически выполняется повторная попытка.

Hello указанной целевой таблицы будут создаваться автоматически, если он еще не существует. Новая таблица Hello соответствует hello схему hello вернул результирующий набор. Если сценарий возвращает несколько результирующих наборов, эластичной базы данных заданий будет отправлять hello первый toohello целевой таблицы.

Hello следующий скрипт PowerShell выполняет скрипт и объединяет результаты в указанной таблице. В этом сценарии предполагается, что у вас уже есть сценарий T-SQL, который возвращает один набор результатов, и целевой объект пользовательской коллекции баз данных.

Этот скрипт использует hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) командлета. Задайте параметры hello для сценария, учетные данные и целевой выполнения:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate и запуск задания для сценарии сбора данных
Этот скрипт использует hello [ **начала AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) командлета.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>tooschedule выполнения триггера задания
Следующий сценарий PowerShell Hello может быть используется toocreate повторяющемуся расписанию. В этом скрипте используется интервал в минутах, но командлет [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) также поддерживает параметры -DayInterval, -HourInterval, -MonthInterval и -WeekInterval. Расписания, которые выполняются только один раз, можно создавать с помощью параметра -OneTime.

Создание нового расписания

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>tootrigger задание выполняется по расписанию
Триггер задания может быть определенный toohave соответствующим tooa расписание задания времени. Hello следующий сценарий PowerShell можно использовать toocreate триггер задания.

Используйте [New AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) и набор hello следующие переменные toocorrespond toohello нужного задания и расписания:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove toostop ассоциации запланированного задания из выполнения по расписанию
toodiscontinue повторения задания операционной системы с помощью триггера задания hello триггера задания могут быть удалены. Удалить задание триггера toostop задания из выполняемой соответствующим tooa расписание, с помощью hello [ **командлет Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>Получить расписание время привязанного tooa триггеров задания
Следующий сценарий PowerShell Hello можно использовать tooobtain и отображения расписания определенный момент времени зарегистрированных tooa триггеры задания hello.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>триггеры задания tooretrieve привязан tooa задания
Используйте [Get AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain и отображения расписания, содержащая зарегистрированные задания.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>toocreate приложения уровня данных (DACPAC) для выполнения в нескольких базах данных
toocreate пакета DAC, в разделе [приложений уровня данных](https://msdn.microsoft.com/library/ee210546.aspx). toodeploy пакета DAC, используйте hello [командлет New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent). Hello DACPAC должен быть доступен toohello службой. Это рекомендуется tooupload созданный tooAzure DACPAC хранилища и создать [подписи общего доступа](../storage/common/storage-dotnet-shared-access-signature-part-1.md) для hello DACPAC.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>tooupdate приложения уровня данных (DACPAC) для выполнения в нескольких базах данных
Существующие пакеты DACPAC, зарегистрированные в заданий эластичных баз данных может быть обновленные toopoint toonew идентификаторы URI. Используйте hello [ **командлета Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello URI пакета DAC на существующем зарегистрированные DACPAC:

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate задание tooapply приложения уровня данных (DACPAC) в нескольких базах данных
После создания пакета DAC в заданий эластичных баз данных задания могут создаваться tooapply hello DACPAC между несколькими базами данных. Следующий сценарий PowerShell Hello может быть используется toocreate задания DACPAC через пользовательский набор баз данных:

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
