---
title: "aaaGetting к выполнению заданий эластичных баз данных | Документы Microsoft"
description: "способ задания toouse эластичной базы данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a>Начало работы с заданиями обработки эластичных баз данных
Заданий эластичных баз данных (Предварительная версия) для базы данных SQL Azure позволяет tooreliability выполнения скриптов T-SQL, которые охватывают несколько баз данных при автоматическим повтором попытки и гарантирует предоставление возможном завершении. Дополнительные сведения о функции задания hello эластичной базы данных см. в разделе hello [страницу Обзор компонента](sql-database-elastic-jobs-overview.md).

В этом разделе расширяет образец hello в [Приступая к работе со средствами эластичной базы данных](sql-database-elastic-scale-get-started.md). После завершения вы будете: Узнайте, как toocreate и управлять заданиями, управлять группой связанных баз данных. Это не требуется toouse средства гибкого масштабирования hello в порядке tootake преимуществами hello эластичной заданий.

## <a name="prerequisites"></a>Предварительные требования
Загрузите и запустите hello [Приступая к работе с образцом эластичной базы данных средства](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Создать пример приложения hello с помощью диспетчера карты сегментов
Здесь вы создадите карта сегментов manager вместе с несколькими сегментами, следуют вставки данных в сегментах hello. При наличии сегментов с сегментированных данных в них можно пропустить следующие шаги hello и переместить следующий раздел toohello.

1. Построение и запуск hello **Приступая к работе со средствами эластичной базы данных** образец приложения. Выполните действия hello до шага 7 в разделе "hello" [загрузить и запустить пример приложения hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). В конце hello шаг 7 вы увидите hello, выполнив в командной строке:

   ![окно командной строки.](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. В окне приветствия командной строки, введите «1» и нажмите клавишу **ввод**. Это создает диспетчера карты сегментов hello и добавляет два сервера toohello сегментов. Затем введите 3 и нажмите клавишу **ВВОД**. Повторите это действие четыре раза. Это позволит вставить строки демонстрационных данных в свои сегменты.
3. Hello [портала Azure](https://portal.azure.com) должно отображаться три новых баз данных:

   ![Подтверждение Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   На этом этапе мы создадим коллекцию пользовательской базе данных, которая отражает все базы данных hello в карте сегментов hello. Это позволит нам toocreate и выполнить задание, добавить новую таблицу в по сегментам.

Здесь мы обычно создать целевой объект карты сегментов, с помощью hello **New AzureSqlJobTarget** командлета. базы данных диспетчера карты сегментов Hello должен быть задан как целевой базы данных, а затем hello конкретных сегментов карты задается в качестве целевого объекта. Вместо этого мы tooenumerate переход всех базах данных hello hello server и добавить hello баз данных toohello новой пользовательской коллекции с исключением hello базы данных master.

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a>Создает пользовательскую коллекцию и добавьте все базы данных в целевом hello server toohello пользовательской коллекции с исключением hello базы данных master.
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Создание сценария T-SQL для выполнения в нескольких базах данных
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a>Создать сценарий tooexecute hello задания для hello пользовательскую группу баз данных

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a>Выполнить задание hello
Hello следующий сценарий PowerShell можно использовать tooexecute существующего задания:

Обновите следующие переменной tooreflect задания требуемого hello имя toohave выполнена hello:

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a>Получить состояние hello выполнения одного задания
Используйте hello же **Get AzureSqlJobExecution** командлет с hello **IncludeChildren** параметр tooview hello состояние выполнения дочерние задания, а именно: hello определенное состояние при каждом выполнении задания для каждой База данных целевой заданием hello.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a>Просмотр состояния hello выполнения нескольких заданий
Hello **Get AzureSqlJobExecution** командлет имеет несколько необязательных параметров, которые можно использовать toodisplay выполнения нескольких заданий, фильтрации с помощью hello предоставленных параметров. Hello ниже показаны некоторые из способов hello toouse Get AzureSqlJobExecution:

Получение сведений о выполнении всех активных заданий верхнего уровня:

   ```
    Get-AzureSqlJobExecution
   ```

Получение сведений о выполнении всех заданий верхнего уровня, включая неактивные задания:

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

Получение состояния выполнения всех дочерних заданий, включая неактивные, по указанному идентификатору выполнения задания:

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

Получение состояния выполнения всех заданий, созданных с помощью сочетания расписания и задания, включая неактивные:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

Получение сведения обо всех заданиях в указанной карте сегментов, включая неактивные:

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Получение сведения обо всех заданиях в указанном пользовательском семействе, включая неактивные:

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Получаете список hello завершений задач во время выполнения конкретного задания:

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

Получение сведений о выполнении задачи:

Следующий сценарий PowerShell Hello может быть сведения hello используется tooview выполнения задачи задания, что особенно полезно при отладке ошибок выполнения.
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a>Получение ошибок при выполнении задач
Hello объекта JobTaskExecution включает свойство для жизненного цикла задачи hello вместе со свойством сообщение hello. Если сбой выполнения задачи задания, hello жизненного цикла свойства будет установлено слишком*сбой* и будет установлено свойство сообщения hello toohello результирующее сообщение об исключении и его стека. Если задание завершилось неудачей, это tooview важные сведения hello задания задач, которые не были успешно выполнены для данного задания.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-toocomplete"></a>Ожидание выполнения задания toocomplete
Следующий сценарий PowerShell Hello может быть toowait используется для задания задач toocomplete:

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

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

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a>Изменение пользовательской политики выполнения
Обновление hello требуемого tooupdate политики выполнения:

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a>Отмена задания
Задания обработки эластичных баз данных поддерживают запросы на отмену заданий.  Если заданий эластичных баз данных обнаруживает запрос отмены задания, выполняемые, он попытается toostop hello задания.

Служба заданий обработки эластичных баз данных может выполнить отмену двумя разными способами:

1. Отмена в данный момент задачи: во время задачи в случае обнаружения отмены будет предпринята попытка отмены в hello аспектом задачу hello в данный момент.  Например: в случае долго выполняющийся запрос, выполняемый в настоящее время при попытке отмены будет попытка toocancel hello запроса.
2. Отмена попытки выполнения задачи: Отмены в случае обнаружения потоком управления hello перед запуском задачи для выполнения потока управления hello будет избежать запуска задачи hello и объявить hello запрос отменен.

При поступлении запроса отмены задания для задания родительского запроса отмены hello будет обрабатываться родительским заданием hello и всех его дочерние задания.

запрос отмены toosubmit использовать hello **Stop AzureSqlJobExecution** командлета и набор hello **JobExecutionId** параметра.

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a>Удаление задания по имени и журнал заданий hello
Задания обработки эластичных баз данных поддерживают асинхронное удаление заданий. Задания могут быть помечены для удаления и hello система удаляет задание hello и ее журнал заданий после завершения выполнения всех заданий для задания hello. Hello системы не будет автоматически отменить выполнение активных заданий.  

Вместо этого AzureSqlJobExecution остановки должно быть выполнений вызванный toocancel активных заданий.

удаления tootrigger задания, используйте hello **AzureSqlJob удаление** командлета и набор hello **JobName** параметра.

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a>Создание пользовательской целевой базы данных
В заданиях обработки эластичных баз данных можно задать пользовательские целевые базы данных, которые можно использовать либо для непосредственного выполнения, либо для включения в пользовательскую группу баз данных. Поскольку **эластичные пулы** не еще напрямую поддерживаются через hello API-интерфейсов PowerShell, достаточно просто создать целевой объект пользовательские базы данных и целевой объект коллекции пользовательские базы данных, который включает все базы данных hello в пуле hello.

Задайте следующие переменные tooreflect hello требуемого базы данных сведения hello.

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a>Создание пользовательского целевого семейства баз данных
Целевой объект коллекции пользовательские базы данных может быть определенный tooenable выполнение нескольких целевых объектов базы данных. После создания базы данных группы баз данных может быть целевой объект пользовательские коллекции связанных toohello.

Следующие переменные tooreflect hello hello набор требуемого пользовательской коллекции целевую конфигурацию:

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a>Добавьте целевой объект коллекции баз данных tooa пользовательские базы данных
Целевые объекты базы данных можно связать с пользовательской базе данных коллекции целевых объектов toocreate группы баз данных. Каждый раз, когда создается задание, целью является целевой объект коллекции пользовательской базе данных, она будет группы связанных toohello развернутой tootarget hello баз данных во время выполнения hello.

Добавьте hello требуемого базы данных tooa определенной пользовательской коллекции:

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Просмотрите hello баз данных в пользовательской базе данных целевого объекта коллекции
Используйте hello **Get AzureSqlJobTarget** командлет tooretrieve hello дочерних баз данных в пользовательской базе данных целевого объекта коллекции.

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Создать сценарий tooexecute задания для целевого объекта коллекции пользовательские базы данных
Используйте hello **New AzureSqlJob** toocreate командлет задания для группы баз данных, определенных в пользовательской базе данных целевого объекта коллекции. Заданий эластичных баз данных будет расширяться hello задания на несколько дочерних каждой соответствующей tooa базы данных, связанная с целевой объект коллекции hello пользовательские базы данных и убедитесь, что hello сценарий выполняется для каждой базы данных. Опять же очень важно, скрипты являются устойчивыми tooretries toobe идемпотентными.

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a>Сбор данных из нескольких баз данных
**Заданий эластичных баз данных** поддерживает выполнение запроса между несколькими базами данных и отправляет hello результаты tooa указанной базы данных таблицы. можно запрашивать таблицы Hello после toosee hello hello фактов запроса результаты из каждой базы данных. Это предоставляет механизм асинхронной tooexecute запрос через несколько баз данных. Случаи сбоев, таких как одна из баз данных hello, временно недоступна, автоматически обрабатываются через повторных попыток.

Hello указанной целевой таблицы автоматически создается, если он еще не существует, соответствующая схема hello объекта hello вернул результирующий набор. Если выполнение скрипта возвращает несколько результирующих наборов, заданий эластичных баз данных будет отправлять hello первый один toohello указанный целевой таблицы.

Следующий сценарий PowerShell Hello может быть tooexecute используется сценарий сбор его результаты в указанной таблице. В этом сценарии предполагается, что были созданы сценарий T-SQL, который выводит один набор результатов, и целевое пользовательское семейство баз данных.

Задать следующий скрипт hello требуемого tooreflect, учетные данные и выполнение целевого hello.

   ```
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
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a>Создание и запуск задания для сбора данных
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a>Создание расписания выполнения заданий с помощью триггера
Hello следующий сценарий PowerShell можно использовать toocreate повторяющегося расписания. В этом сценарии используется интервал в одну минуту, но командлет New-AzureSqlJobSchedule также поддерживает параметры -DayInterval, -HourInterval, -MonthInterval и -WeekInterval. Расписания, которые выполняются только один раз, можно создавать с помощью параметра -OneTime.

Создание нового расписания
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a>Создать задание выполняется по расписанию время toohave триггера задания
Триггер задания может быть определенный toohave соответствующим tooa расписание задания времени. Hello следующий сценарий PowerShell можно использовать toocreate триггер задания.

Следующие переменные toocorrespond toohello hello набор требуемого задания и расписания:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>Удалить задание toostop запланированных связь из выполнения по расписанию
toodiscontinue повторения задания операционной системы с помощью триггера задания hello триггера задания могут быть удалены.
Удалить задание триггера toostop задания из выполняемой соответствующим tooa расписание, с помощью hello **AzureSqlJobTrigger удаление** командлета.

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a>Импорт tooExcel результаты запроса эластичной базы данных
 Можно импортировать результаты hello из файла Excel tooan запроса.

1. Запустите Excel 2013.
2. Перейдите toohello **данные** ленты.
3. Щелкните **Из других источников**, а затем — **Из SQL Server**.

   ![Импорт в Excel из других источников](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. В hello **мастер подключения данных** введите учетные данные имя и имя входа сервера hello. Нажмите кнопку **Далее**.
5. В диалоговом окне приветствия **hello выберите базу данных, содержащую данные hello**выберите hello **ElasticDBQuery** базы данных.
6. Выберите hello **клиентов** из таблицы в представлении списка hello и нажмите кнопку **Далее**. Нажмите кнопку **Готово**.
7. В hello **импорта данных** форме, в разделе **выберите способ tooview эти данные в книге**выберите **таблицы** и нажмите кнопку **ОК**.

Здравствуйте, все строки из **клиентов** листа Excel hello заполнение таблицы, хранимые в разных сегментах.

## <a name="next-steps"></a>Дальнейшие действия
Теперь можно использовать функции обработки данных Excel. Используйте строку подключения hello именем сервера, имя базы данных и учетные данные tooconnect бизнес-Аналитики и данные интеграции средства toohello запроса эластичной базы данных. Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server. См. toohello эластичной запрос к базе данных и внешних таблиц так же, как и любой другой базы данных SQL Server и таблицах SQL Server, то для подключения toowith средством.

### <a name="cost"></a>Стоимость
Без дополнительной платы для использования функции запросов hello эластичной базы данных не существует. В настоящее время эта функция доступна только для расширенных баз данных как конечную точку, однако hello сегментов могут быть любого уровня службы.

Сведения о ценах см. на [странице с ценами на базу данных SQL](https://azure.microsoft.com/pricing/details/sql-database/).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
