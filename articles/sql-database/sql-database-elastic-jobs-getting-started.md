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
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="7891d-103">Начало работы с заданиями обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="7891d-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="7891d-104">Заданий эластичных баз данных (Предварительная версия) для базы данных SQL Azure позволяет tooreliability выполнения скриптов T-SQL, которые охватывают несколько баз данных при автоматическим повтором попытки и гарантирует предоставление возможном завершении.</span><span class="sxs-lookup"><span data-stu-id="7891d-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="7891d-105">Дополнительные сведения о функции задания hello эластичной базы данных см. в разделе hello [страницу Обзор компонента](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7891d-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="7891d-106">В этом разделе расширяет образец hello в [Приступая к работе со средствами эластичной базы данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7891d-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="7891d-107">После завершения вы будете: Узнайте, как toocreate и управлять заданиями, управлять группой связанных баз данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="7891d-108">Это не требуется toouse средства гибкого масштабирования hello в порядке tootake преимуществами hello эластичной заданий.</span><span class="sxs-lookup"><span data-stu-id="7891d-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7891d-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7891d-109">Prerequisites</span></span>
<span data-ttu-id="7891d-110">Загрузите и запустите hello [Приступая к работе с образцом эластичной базы данных средства](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7891d-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="7891d-111">Создать пример приложения hello с помощью диспетчера карты сегментов</span><span class="sxs-lookup"><span data-stu-id="7891d-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="7891d-112">Здесь вы создадите карта сегментов manager вместе с несколькими сегментами, следуют вставки данных в сегментах hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="7891d-113">При наличии сегментов с сегментированных данных в них можно пропустить следующие шаги hello и переместить следующий раздел toohello.</span><span class="sxs-lookup"><span data-stu-id="7891d-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="7891d-114">Построение и запуск hello **Приступая к работе со средствами эластичной базы данных** образец приложения.</span><span class="sxs-lookup"><span data-stu-id="7891d-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="7891d-115">Выполните действия hello до шага 7 в разделе "hello" [загрузить и запустить пример приложения hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="7891d-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="7891d-116">В конце hello шаг 7 вы увидите hello, выполнив в командной строке:</span><span class="sxs-lookup"><span data-stu-id="7891d-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![окно командной строки.](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="7891d-118">В окне приветствия командной строки, введите «1» и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7891d-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="7891d-119">Это создает диспетчера карты сегментов hello и добавляет два сервера toohello сегментов.</span><span class="sxs-lookup"><span data-stu-id="7891d-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="7891d-120">Затем введите 3 и нажмите клавишу **ВВОД**. Повторите это действие четыре раза.</span><span class="sxs-lookup"><span data-stu-id="7891d-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="7891d-121">Это позволит вставить строки демонстрационных данных в свои сегменты.</span><span class="sxs-lookup"><span data-stu-id="7891d-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="7891d-122">Hello [портала Azure](https://portal.azure.com) должно отображаться три новых баз данных:</span><span class="sxs-lookup"><span data-stu-id="7891d-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Подтверждение Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="7891d-124">На этом этапе мы создадим коллекцию пользовательской базе данных, которая отражает все базы данных hello в карте сегментов hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="7891d-125">Это позволит нам toocreate и выполнить задание, добавить новую таблицу в по сегментам.</span><span class="sxs-lookup"><span data-stu-id="7891d-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="7891d-126">Здесь мы обычно создать целевой объект карты сегментов, с помощью hello **New AzureSqlJobTarget** командлета.</span><span class="sxs-lookup"><span data-stu-id="7891d-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="7891d-127">базы данных диспетчера карты сегментов Hello должен быть задан как целевой базы данных, а затем hello конкретных сегментов карты задается в качестве целевого объекта.</span><span class="sxs-lookup"><span data-stu-id="7891d-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="7891d-128">Вместо этого мы tooenumerate переход всех базах данных hello hello server и добавить hello баз данных toohello новой пользовательской коллекции с исключением hello базы данных master.</span><span class="sxs-lookup"><span data-stu-id="7891d-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="7891d-129">Создает пользовательскую коллекцию и добавьте все базы данных в целевом hello server toohello пользовательской коллекции с исключением hello базы данных master.</span><span class="sxs-lookup"><span data-stu-id="7891d-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
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
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="7891d-130">Создание сценария T-SQL для выполнения в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="7891d-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="7891d-131">Создать сценарий tooexecute hello задания для hello пользовательскую группу баз данных</span><span class="sxs-lookup"><span data-stu-id="7891d-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="7891d-132">Выполнить задание hello</span><span class="sxs-lookup"><span data-stu-id="7891d-132">Execute hello job</span></span>
<span data-ttu-id="7891d-133">Hello следующий сценарий PowerShell можно использовать tooexecute существующего задания:</span><span class="sxs-lookup"><span data-stu-id="7891d-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="7891d-134">Обновите следующие переменной tooreflect задания требуемого hello имя toohave выполнена hello:</span><span class="sxs-lookup"><span data-stu-id="7891d-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="7891d-135">Получить состояние hello выполнения одного задания</span><span class="sxs-lookup"><span data-stu-id="7891d-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="7891d-136">Используйте hello же **Get AzureSqlJobExecution** командлет с hello **IncludeChildren** параметр tooview hello состояние выполнения дочерние задания, а именно: hello определенное состояние при каждом выполнении задания для каждой База данных целевой заданием hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="7891d-137">Просмотр состояния hello выполнения нескольких заданий</span><span class="sxs-lookup"><span data-stu-id="7891d-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="7891d-138">Hello **Get AzureSqlJobExecution** командлет имеет несколько необязательных параметров, которые можно использовать toodisplay выполнения нескольких заданий, фильтрации с помощью hello предоставленных параметров.</span><span class="sxs-lookup"><span data-stu-id="7891d-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="7891d-139">Hello ниже показаны некоторые из способов hello toouse Get AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="7891d-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="7891d-140">Получение сведений о выполнении всех активных заданий верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="7891d-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="7891d-141">Получение сведений о выполнении всех заданий верхнего уровня, включая неактивные задания:</span><span class="sxs-lookup"><span data-stu-id="7891d-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="7891d-142">Получение состояния выполнения всех дочерних заданий, включая неактивные, по указанному идентификатору выполнения задания:</span><span class="sxs-lookup"><span data-stu-id="7891d-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="7891d-143">Получение состояния выполнения всех заданий, созданных с помощью сочетания расписания и задания, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="7891d-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="7891d-144">Получение сведения обо всех заданиях в указанной карте сегментов, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="7891d-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="7891d-145">Получение сведения обо всех заданиях в указанном пользовательском семействе, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="7891d-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="7891d-146">Получаете список hello завершений задач во время выполнения конкретного задания:</span><span class="sxs-lookup"><span data-stu-id="7891d-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="7891d-147">Получение сведений о выполнении задачи:</span><span class="sxs-lookup"><span data-stu-id="7891d-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="7891d-148">Следующий сценарий PowerShell Hello может быть сведения hello используется tooview выполнения задачи задания, что особенно полезно при отладке ошибок выполнения.</span><span class="sxs-lookup"><span data-stu-id="7891d-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="7891d-149">Получение ошибок при выполнении задач</span><span class="sxs-lookup"><span data-stu-id="7891d-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="7891d-150">Hello объекта JobTaskExecution включает свойство для жизненного цикла задачи hello вместе со свойством сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="7891d-151">Если сбой выполнения задачи задания, hello жизненного цикла свойства будет установлено слишком*сбой* и будет установлено свойство сообщения hello toohello результирующее сообщение об исключении и его стека.</span><span class="sxs-lookup"><span data-stu-id="7891d-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="7891d-152">Если задание завершилось неудачей, это tooview важные сведения hello задания задач, которые не были успешно выполнены для данного задания.</span><span class="sxs-lookup"><span data-stu-id="7891d-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="7891d-153">Ожидание выполнения задания toocomplete</span><span class="sxs-lookup"><span data-stu-id="7891d-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="7891d-154">Следующий сценарий PowerShell Hello может быть toowait используется для задания задач toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7891d-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="7891d-155">Создание пользовательской политики выполнения</span><span class="sxs-lookup"><span data-stu-id="7891d-155">Create a custom execution policy</span></span>
<span data-ttu-id="7891d-156">Задания обработки эластичных баз данных поддерживают создание пользовательских политик выполнения, которые можно применять при запуске заданий.</span><span class="sxs-lookup"><span data-stu-id="7891d-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="7891d-157">В настоящий момент политики выполнения позволяют задать следующее:</span><span class="sxs-lookup"><span data-stu-id="7891d-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="7891d-158">Имя: Идентификатор для политики выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="7891d-159">Время ожидания задания: общее время до отмены задания службой заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="7891d-160">Начальный интервал повторных попыток: Toowait интервал перед первой повторной попытки.</span><span class="sxs-lookup"><span data-stu-id="7891d-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="7891d-161">Максимальный интервал повторных попыток: Лимит в размере toouse интервалы повтора.</span><span class="sxs-lookup"><span data-stu-id="7891d-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="7891d-162">Коэффициент отсрочки интервал повторных попыток: Коэффициент используется toocalculate hello следующий интервал между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="7891d-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="7891d-163">Hello используется следующая формула: (начальной интервал повтора) * Math.pow ((интервал отсрочки коэффициент) (число повторов) - 2).</span><span class="sxs-lookup"><span data-stu-id="7891d-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="7891d-164">Максимальное попыток: hello максимальное число tooperform попыток повтора в задании.</span><span class="sxs-lookup"><span data-stu-id="7891d-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="7891d-165">политика выполнения по умолчанию Hello использует hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="7891d-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="7891d-166">Имя: политика выполнения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7891d-166">Name: Default execution policy</span></span>
* <span data-ttu-id="7891d-167">Время ожидания задания: 1 неделя</span><span class="sxs-lookup"><span data-stu-id="7891d-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="7891d-168">Исходный интервал повторных попыток: 100 миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="7891d-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="7891d-169">Максимальный интервал повторных попыток: 30 минут</span><span class="sxs-lookup"><span data-stu-id="7891d-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="7891d-170">Коэффициент интервала повторных попыток: 2</span><span class="sxs-lookup"><span data-stu-id="7891d-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="7891d-171">Максимальное число попыток: 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="7891d-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="7891d-172">Создайте политику выполнения требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-172">Create hello desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="7891d-173">Изменение пользовательской политики выполнения</span><span class="sxs-lookup"><span data-stu-id="7891d-173">Update a custom execution policy</span></span>
<span data-ttu-id="7891d-174">Обновление hello требуемого tooupdate политики выполнения:</span><span class="sxs-lookup"><span data-stu-id="7891d-174">Update hello desired execution policy tooupdate:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="7891d-175">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="7891d-175">Cancel a job</span></span>
<span data-ttu-id="7891d-176">Задания обработки эластичных баз данных поддерживают запросы на отмену заданий.</span><span class="sxs-lookup"><span data-stu-id="7891d-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="7891d-177">Если заданий эластичных баз данных обнаруживает запрос отмены задания, выполняемые, он попытается toostop hello задания.</span><span class="sxs-lookup"><span data-stu-id="7891d-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="7891d-178">Служба заданий обработки эластичных баз данных может выполнить отмену двумя разными способами:</span><span class="sxs-lookup"><span data-stu-id="7891d-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="7891d-179">Отмена в данный момент задачи: во время задачи в случае обнаружения отмены будет предпринята попытка отмены в hello аспектом задачу hello в данный момент.</span><span class="sxs-lookup"><span data-stu-id="7891d-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="7891d-180">Например: в случае долго выполняющийся запрос, выполняемый в настоящее время при попытке отмены будет попытка toocancel hello запроса.</span><span class="sxs-lookup"><span data-stu-id="7891d-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="7891d-181">Отмена попытки выполнения задачи: Отмены в случае обнаружения потоком управления hello перед запуском задачи для выполнения потока управления hello будет избежать запуска задачи hello и объявить hello запрос отменен.</span><span class="sxs-lookup"><span data-stu-id="7891d-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="7891d-182">При поступлении запроса отмены задания для задания родительского запроса отмены hello будет обрабатываться родительским заданием hello и всех его дочерние задания.</span><span class="sxs-lookup"><span data-stu-id="7891d-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="7891d-183">запрос отмены toosubmit использовать hello **Stop AzureSqlJobExecution** командлета и набор hello **JobExecutionId** параметра.</span><span class="sxs-lookup"><span data-stu-id="7891d-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="7891d-184">Удаление задания по имени и журнал заданий hello</span><span class="sxs-lookup"><span data-stu-id="7891d-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="7891d-185">Задания обработки эластичных баз данных поддерживают асинхронное удаление заданий.</span><span class="sxs-lookup"><span data-stu-id="7891d-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="7891d-186">Задания могут быть помечены для удаления и hello система удаляет задание hello и ее журнал заданий после завершения выполнения всех заданий для задания hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="7891d-187">Hello системы не будет автоматически отменить выполнение активных заданий.</span><span class="sxs-lookup"><span data-stu-id="7891d-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="7891d-188">Вместо этого AzureSqlJobExecution остановки должно быть выполнений вызванный toocancel активных заданий.</span><span class="sxs-lookup"><span data-stu-id="7891d-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="7891d-189">удаления tootrigger задания, используйте hello **AzureSqlJob удаление** командлета и набор hello **JobName** параметра.</span><span class="sxs-lookup"><span data-stu-id="7891d-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="7891d-190">Создание пользовательской целевой базы данных</span><span class="sxs-lookup"><span data-stu-id="7891d-190">Create a custom database target</span></span>
<span data-ttu-id="7891d-191">В заданиях обработки эластичных баз данных можно задать пользовательские целевые базы данных, которые можно использовать либо для непосредственного выполнения, либо для включения в пользовательскую группу баз данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="7891d-192">Поскольку **эластичные пулы** не еще напрямую поддерживаются через hello API-интерфейсов PowerShell, достаточно просто создать целевой объект пользовательские базы данных и целевой объект коллекции пользовательские базы данных, который включает все базы данных hello в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="7891d-193">Задайте следующие переменные tooreflect hello требуемого базы данных сведения hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="7891d-194">Создание пользовательского целевого семейства баз данных</span><span class="sxs-lookup"><span data-stu-id="7891d-194">Create a custom database collection target</span></span>
<span data-ttu-id="7891d-195">Целевой объект коллекции пользовательские базы данных может быть определенный tooenable выполнение нескольких целевых объектов базы данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="7891d-196">После создания базы данных группы баз данных может быть целевой объект пользовательские коллекции связанных toohello.</span><span class="sxs-lookup"><span data-stu-id="7891d-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="7891d-197">Следующие переменные tooreflect hello hello набор требуемого пользовательской коллекции целевую конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="7891d-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="7891d-198">Добавьте целевой объект коллекции баз данных tooa пользовательские базы данных</span><span class="sxs-lookup"><span data-stu-id="7891d-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="7891d-199">Целевые объекты базы данных можно связать с пользовательской базе данных коллекции целевых объектов toocreate группы баз данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="7891d-200">Каждый раз, когда создается задание, целью является целевой объект коллекции пользовательской базе данных, она будет группы связанных toohello развернутой tootarget hello баз данных во время выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="7891d-201">Добавьте hello требуемого базы данных tooa определенной пользовательской коллекции:</span><span class="sxs-lookup"><span data-stu-id="7891d-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="7891d-202">Просмотрите hello баз данных в пользовательской базе данных целевого объекта коллекции</span><span class="sxs-lookup"><span data-stu-id="7891d-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="7891d-203">Используйте hello **Get AzureSqlJobTarget** командлет tooretrieve hello дочерних баз данных в пользовательской базе данных целевого объекта коллекции.</span><span class="sxs-lookup"><span data-stu-id="7891d-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="7891d-204">Создать сценарий tooexecute задания для целевого объекта коллекции пользовательские базы данных</span><span class="sxs-lookup"><span data-stu-id="7891d-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="7891d-205">Используйте hello **New AzureSqlJob** toocreate командлет задания для группы баз данных, определенных в пользовательской базе данных целевого объекта коллекции.</span><span class="sxs-lookup"><span data-stu-id="7891d-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="7891d-206">Заданий эластичных баз данных будет расширяться hello задания на несколько дочерних каждой соответствующей tooa базы данных, связанная с целевой объект коллекции hello пользовательские базы данных и убедитесь, что hello сценарий выполняется для каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="7891d-207">Опять же очень важно, скрипты являются устойчивыми tooretries toobe идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="7891d-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="7891d-208">Сбор данных из нескольких баз данных</span><span class="sxs-lookup"><span data-stu-id="7891d-208">Data collection across databases</span></span>
<span data-ttu-id="7891d-209">**Заданий эластичных баз данных** поддерживает выполнение запроса между несколькими базами данных и отправляет hello результаты tooa указанной базы данных таблицы.</span><span class="sxs-lookup"><span data-stu-id="7891d-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="7891d-210">можно запрашивать таблицы Hello после toosee hello hello фактов запроса результаты из каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="7891d-211">Это предоставляет механизм асинхронной tooexecute запрос через несколько баз данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="7891d-212">Случаи сбоев, таких как одна из баз данных hello, временно недоступна, автоматически обрабатываются через повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="7891d-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="7891d-213">Hello указанной целевой таблицы автоматически создается, если он еще не существует, соответствующая схема hello объекта hello вернул результирующий набор.</span><span class="sxs-lookup"><span data-stu-id="7891d-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="7891d-214">Если выполнение скрипта возвращает несколько результирующих наборов, заданий эластичных баз данных будет отправлять hello первый один toohello указанный целевой таблицы.</span><span class="sxs-lookup"><span data-stu-id="7891d-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="7891d-215">Следующий сценарий PowerShell Hello может быть tooexecute используется сценарий сбор его результаты в указанной таблице.</span><span class="sxs-lookup"><span data-stu-id="7891d-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="7891d-216">В этом сценарии предполагается, что были созданы сценарий T-SQL, который выводит один набор результатов, и целевое пользовательское семейство баз данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="7891d-217">Задать следующий скрипт hello требуемого tooreflect, учетные данные и выполнение целевого hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="7891d-218">Создание и запуск задания для сбора данных</span><span class="sxs-lookup"><span data-stu-id="7891d-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="7891d-219">Создание расписания выполнения заданий с помощью триггера</span><span class="sxs-lookup"><span data-stu-id="7891d-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="7891d-220">Hello следующий сценарий PowerShell можно использовать toocreate повторяющегося расписания.</span><span class="sxs-lookup"><span data-stu-id="7891d-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="7891d-221">В этом сценарии используется интервал в одну минуту, но командлет New-AzureSqlJobSchedule также поддерживает параметры -DayInterval, -HourInterval, -MonthInterval и -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="7891d-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="7891d-222">Расписания, которые выполняются только один раз, можно создавать с помощью параметра -OneTime.</span><span class="sxs-lookup"><span data-stu-id="7891d-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="7891d-223">Создание нового расписания</span><span class="sxs-lookup"><span data-stu-id="7891d-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="7891d-224">Создать задание выполняется по расписанию время toohave триггера задания</span><span class="sxs-lookup"><span data-stu-id="7891d-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="7891d-225">Триггер задания может быть определенный toohave соответствующим tooa расписание задания времени.</span><span class="sxs-lookup"><span data-stu-id="7891d-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="7891d-226">Hello следующий сценарий PowerShell можно использовать toocreate триггер задания.</span><span class="sxs-lookup"><span data-stu-id="7891d-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="7891d-227">Следующие переменные toocorrespond toohello hello набор требуемого задания и расписания:</span><span class="sxs-lookup"><span data-stu-id="7891d-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="7891d-228">Удалить задание toostop запланированных связь из выполнения по расписанию</span><span class="sxs-lookup"><span data-stu-id="7891d-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="7891d-229">toodiscontinue повторения задания операционной системы с помощью триггера задания hello триггера задания могут быть удалены.</span><span class="sxs-lookup"><span data-stu-id="7891d-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="7891d-230">Удалить задание триггера toostop задания из выполняемой соответствующим tooa расписание, с помощью hello **AzureSqlJobTrigger удаление** командлета.</span><span class="sxs-lookup"><span data-stu-id="7891d-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="7891d-231">Импорт tooExcel результаты запроса эластичной базы данных</span><span class="sxs-lookup"><span data-stu-id="7891d-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="7891d-232">Можно импортировать результаты hello из файла Excel tooan запроса.</span><span class="sxs-lookup"><span data-stu-id="7891d-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="7891d-233">Запустите Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="7891d-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="7891d-234">Перейдите toohello **данные** ленты.</span><span class="sxs-lookup"><span data-stu-id="7891d-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="7891d-235">Щелкните **Из других источников**, а затем — **Из SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7891d-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Импорт в Excel из других источников](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="7891d-237">В hello **мастер подключения данных** введите учетные данные имя и имя входа сервера hello.</span><span class="sxs-lookup"><span data-stu-id="7891d-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="7891d-238">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7891d-238">Then click **Next**.</span></span>
5. <span data-ttu-id="7891d-239">В диалоговом окне приветствия **hello выберите базу данных, содержащую данные hello**выберите hello **ElasticDBQuery** базы данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="7891d-240">Выберите hello **клиентов** из таблицы в представлении списка hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7891d-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="7891d-241">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="7891d-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="7891d-242">В hello **импорта данных** форме, в разделе **выберите способ tooview эти данные в книге**выберите **таблицы** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7891d-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="7891d-243">Здравствуйте, все строки из **клиентов** листа Excel hello заполнение таблицы, хранимые в разных сегментах.</span><span class="sxs-lookup"><span data-stu-id="7891d-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7891d-244">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7891d-244">Next steps</span></span>
<span data-ttu-id="7891d-245">Теперь можно использовать функции обработки данных Excel.</span><span class="sxs-lookup"><span data-stu-id="7891d-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="7891d-246">Используйте строку подключения hello именем сервера, имя базы данных и учетные данные tooconnect бизнес-Аналитики и данные интеграции средства toohello запроса эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="7891d-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="7891d-247">Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7891d-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="7891d-248">См. toohello эластичной запрос к базе данных и внешних таблиц так же, как и любой другой базы данных SQL Server и таблицах SQL Server, то для подключения toowith средством.</span><span class="sxs-lookup"><span data-stu-id="7891d-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="7891d-249">Стоимость</span><span class="sxs-lookup"><span data-stu-id="7891d-249">Cost</span></span>
<span data-ttu-id="7891d-250">Без дополнительной платы для использования функции запросов hello эластичной базы данных не существует.</span><span class="sxs-lookup"><span data-stu-id="7891d-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="7891d-251">В настоящее время эта функция доступна только для расширенных баз данных как конечную точку, однако hello сегментов могут быть любого уровня службы.</span><span class="sxs-lookup"><span data-stu-id="7891d-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="7891d-252">Сведения о ценах см. на [странице с ценами на базу данных SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="7891d-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
