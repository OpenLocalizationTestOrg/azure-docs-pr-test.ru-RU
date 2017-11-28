---
title: "Начало работы с заданиями обработки эластичных баз данных | Документация Майкрософт"
description: "как использовать задания обработки эластичных баз данных"
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
ms.openlocfilehash: 05c20e880d4eb1eacdecc0c4c7e7491dfe1e6a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="ddd4c-103">Начало работы с заданиями обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="ddd4c-104">Задания обработки эластичных баз данных (предварительная версия) для Базы данных SQL Azure позволяют надежно выполнять сценарии T-SQL, относящиеся к нескольким базам данных, автоматически повторяя попытки и обеспечивая гарантии успешного завершения.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="ddd4c-105">Дополнительные сведения о функции заданий обработки эластичных баз данных см. на [странице с обзором функций](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ddd4c-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="ddd4c-106">В этом разделе более подробно рассматривается пример из раздела [Приступая к работе с инструментами эластичных баз данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ddd4c-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="ddd4c-107">Прочитав эту статью, вы узнаете, как создавать и настраивать задания, которые управляют группой связанных баз данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="ddd4c-108">Чтобы воспользоваться преимуществами заданий обработки эластичных БД, не обязательно использовать инструменты эластичного масштабирования.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddd4c-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ddd4c-109">Prerequisites</span></span>
<span data-ttu-id="ddd4c-110">Загрузите и запустите пример [Приступая к работе с инструментами эластичной базы данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ddd4c-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="ddd4c-111">Создание диспетчера сопоставления сегментов с помощью примера приложения </span><span class="sxs-lookup"><span data-stu-id="ddd4c-111">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="ddd4c-112">Здесь мы создадим диспетчер сопоставления сегментов вместе с несколькими сегментами, а затем выполним вставку данных в сегменты.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="ddd4c-113">Если вы уже настроили сегменты с помощью сегментированных данных, описанные ниже действия можно пропустить и перейти к следующему разделу.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="ddd4c-114">Постройте и запустите пример приложения **Приступая к работе с инструментами эластичной базы данных** .</span><span class="sxs-lookup"><span data-stu-id="ddd4c-114">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="ddd4c-115">Следуйте инструкциям до шага 7 в разделе [Загрузка и запуск примера приложения](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="ddd4c-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="ddd4c-116">В конце шага 7 появится следующее окно командной строки:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-116">At the end of Step 7, you will see the following command prompt:</span></span>

   ![окно командной строки.](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="ddd4c-118">В окне команд введите "1" и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-118">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="ddd4c-119">Это позволит создать диспетчер сопоставления сегментов и добавить два сегмента на сервер.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-119">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="ddd4c-120">Затем введите 3 и нажмите клавишу **ВВОД**. Повторите это действие четыре раза.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="ddd4c-121">Это позволит вставить строки демонстрационных данных в свои сегменты.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="ddd4c-122">На [портале Azure](https://portal.azure.com) должны появиться три новые базы данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Подтверждение Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="ddd4c-124">На этом этапе мы создадим семейство баз данных, которое включает все базы данных в карте сегментов.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span></span> <span data-ttu-id="ddd4c-125">Это позволит нам создать и выполнить задание, которое добавит новую таблицу в сегменты.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-125">This will allow us to create and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="ddd4c-126">Здесь обычно создается целевая карта сегментов с помощью командлета **New-AzureSqlJobTarget** .</span><span class="sxs-lookup"><span data-stu-id="ddd4c-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="ddd4c-127">Для этого необходимо указать управляющую базу данных карт сегментов как целевую базу данных, а затем указать в качестве цели конкретную карту сегментов.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span></span> <span data-ttu-id="ddd4c-128">Вместо этого мы перечислим все базы данных на сервере и добавим базы данных в новое семейство, за исключением базы данных master.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-the-server-to-the-custom-collection-target-with-the-exception-of-master"></a><span data-ttu-id="ddd4c-129">Создание пользовательской коллекции и добавление всех баз данных на сервере в пользовательскую целевую коллекцию за исключением базы данных master</span><span class="sxs-lookup"><span data-stu-id="ddd4c-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span></span>
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
             Write-Host $currentdb "is already in the custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="ddd4c-130">Создание сценария T-SQL для выполнения между базами данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-the-job-to-execute-a-script-across-the-custom-group-of-databases"></a><span data-ttu-id="ddd4c-131">Создание задания для выполнения сценария в пользовательской группе баз данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-131">Create the job to execute a script across the custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-the-job"></a><span data-ttu-id="ddd4c-132">Выполнение задания</span><span class="sxs-lookup"><span data-stu-id="ddd4c-132">Execute the job</span></span>
<span data-ttu-id="ddd4c-133">Следующий сценарий PowerShell позволяет выполнить существующее задание:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-133">The following PowerShell script can be used to execute an existing job:</span></span>

<span data-ttu-id="ddd4c-134">Измените следующую переменную в соответствии с именем выполняемого задания:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-134">Update the following variable to reflect the desired job name to have executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="ddd4c-135">Получение состояния выполнения одного задания</span><span class="sxs-lookup"><span data-stu-id="ddd4c-135">Retrieve the state of a single job execution</span></span>
<span data-ttu-id="ddd4c-136">Чтобы узнать состояние выполнения дочерних заданий, в частности состояние каждого задания в каждой целевой базе данных, используйте тот же командлет **Get-AzureSqlJobExecution** с параметром **IncludeChildren**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-the-state-across-multiple-job-executions"></a><span data-ttu-id="ddd4c-137">Просмотр состояния выполнения нескольких заданий</span><span class="sxs-lookup"><span data-stu-id="ddd4c-137">View the state across multiple job executions</span></span>
<span data-ttu-id="ddd4c-138">У командлета **Get-AzureSqlJobExecution** есть несколько необязательных параметров, позволяющих увидеть ход выполнения нескольких заданий, отфильтрованных по указанным параметрам.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="ddd4c-139">Ниже показаны некоторые из возможных способов использования командлета Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="ddd4c-140">Получение сведений о выполнении всех активных заданий верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="ddd4c-141">Получение сведений о выполнении всех заданий верхнего уровня, включая неактивные задания:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="ddd4c-142">Получение состояния выполнения всех дочерних заданий, включая неактивные, по указанному идентификатору выполнения задания:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="ddd4c-143">Получение состояния выполнения всех заданий, созданных с помощью сочетания расписания и задания, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="ddd4c-144">Получение сведения обо всех заданиях в указанной карте сегментов, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="ddd4c-145">Получение сведения обо всех заданиях в указанном пользовательском семействе, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="ddd4c-146">Получение списка выполнения задач в определенном задании:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-146">Retrieve the list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="ddd4c-147">Получение сведений о выполнении задачи:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="ddd4c-148">Следующий сценарий PowerShell позволяет просмотреть сведения о выполнении задачи, что особенно полезно при отладке сбоев выполнения.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="ddd4c-149">Получение ошибок при выполнении задач</span><span class="sxs-lookup"><span data-stu-id="ddd4c-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="ddd4c-150">Объект JobTaskExecution включает свойство Lifecycle для жизненного цикла задачи и свойство Message.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span></span> <span data-ttu-id="ddd4c-151">В случае сбоя при выполнении задачи свойство Lifecycle принимает значение *Failed* , а свойство Message содержит сообщение об исключении и его стек.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="ddd4c-152">Если задание завершилось неудачно, важно просмотреть сведения задачах, которые не были выполнены в определенном задании.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-to-complete"></a><span data-ttu-id="ddd4c-153">Ожидание завершения выполнения задания</span><span class="sxs-lookup"><span data-stu-id="ddd4c-153">Waiting for a job execution to complete</span></span>
<span data-ttu-id="ddd4c-154">Следующий сценарий PowerShell позволяет дождаться завершения задачи:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-154">The following PowerShell script can be used to wait for a job task to complete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="ddd4c-155">Создание пользовательской политики выполнения</span><span class="sxs-lookup"><span data-stu-id="ddd4c-155">Create a custom execution policy</span></span>
<span data-ttu-id="ddd4c-156">Задания обработки эластичных баз данных поддерживают создание пользовательских политик выполнения, которые можно применять при запуске заданий.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="ddd4c-157">В настоящий момент политики выполнения позволяют задать следующее:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="ddd4c-158">Имя: идентификатор политики выполнения.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-158">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="ddd4c-159">Время ожидания задания: общее время до отмены задания службой заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="ddd4c-160">Исходный интервал повторных попыток: интервал ожидания до первой повторной попытки.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-160">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="ddd4c-161">Максимальный интервал повторных попыток: предел используемых интервалов повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-161">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="ddd4c-162">Коэффициент роста интервала повторных попыток: коэффициент, используемый для вычисления следующего интервала между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="ddd4c-163">Используется следующая формула: (Исходный интервал повторных попыток) * Math.pow((Коэффициент роста интервала), (Число повторных попыток) - 2).</span><span class="sxs-lookup"><span data-stu-id="ddd4c-163">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="ddd4c-164">Максимальное число попыток: максимальное число повторных попыток, выполняемых в задании.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="ddd4c-165">В политике выполнения по умолчанию используются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-165">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="ddd4c-166">Имя: политика выполнения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ddd4c-166">Name: Default execution policy</span></span>
* <span data-ttu-id="ddd4c-167">Время ожидания задания: 1 неделя</span><span class="sxs-lookup"><span data-stu-id="ddd4c-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="ddd4c-168">Исходный интервал повторных попыток: 100 миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="ddd4c-169">Максимальный интервал повторных попыток: 30 минут</span><span class="sxs-lookup"><span data-stu-id="ddd4c-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="ddd4c-170">Коэффициент интервала повторных попыток: 2</span><span class="sxs-lookup"><span data-stu-id="ddd4c-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="ddd4c-171">Максимальное число попыток: 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="ddd4c-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="ddd4c-172">Создайте нужную политику выполнения:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-172">Create the desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="ddd4c-173">Изменение пользовательской политики выполнения</span><span class="sxs-lookup"><span data-stu-id="ddd4c-173">Update a custom execution policy</span></span>
<span data-ttu-id="ddd4c-174">Измените нужную политику выполнения:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-174">Update the desired execution policy to update:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="ddd4c-175">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="ddd4c-175">Cancel a job</span></span>
<span data-ttu-id="ddd4c-176">Задания обработки эластичных баз данных поддерживают запросы на отмену заданий.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="ddd4c-177">Если служба заданий обработки эластичных баз данных обнаружат запрос на отмену выполняемого задания, она попытается остановить задачу.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="ddd4c-178">Служба заданий обработки эластичных баз данных может выполнить отмену двумя разными способами:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="ddd4c-179">Отмена выполняющихся заданий: если отмена обнаружена во время выполнения задачи, произойдет попытка отмены в существующем аспекте задачи.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="ddd4c-180">Например: если при попытке отмены выполняются длинный запрос, произойдет попытка его отмены.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="ddd4c-181">Отмена повторных попыток задач: если поток управления обнаружит отмену, он не будет запускать задачу и объявит запрос отмененным.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="ddd4c-182">В случае запроса отмены родительского задания этот запрос будет выполнен для родительского задания и всех его дочерних заданий.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="ddd4c-183">Чтобы отправить запрос на отмену, используйте командлет **Stop-AzureSqlJobExecution** с параметром **JobExecutionId**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-the-jobs-history"></a><span data-ttu-id="ddd4c-184">Удаление задания по имени и журналу</span><span class="sxs-lookup"><span data-stu-id="ddd4c-184">Delete a job by name and the job's history</span></span>
<span data-ttu-id="ddd4c-185">Задания обработки эластичных баз данных поддерживают асинхронное удаление заданий.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="ddd4c-186">Задания могут быть отмечены для удаления, а система удалит задание и весь его журнал после завершения всех выполнений задания.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="ddd4c-187">Система не будет автоматически отменять активные выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-187">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="ddd4c-188">Вместо этого необходимо вызвать командлет Stop-AzureSqlJobExecution, чтобы отменить активные выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span></span>

<span data-ttu-id="ddd4c-189">Чтобы запустить удаление задания, выполните командлет **Remove-AzureSqlJob** с параметром **JobName**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="ddd4c-190">Создание пользовательской целевой базы данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-190">Create a custom database target</span></span>
<span data-ttu-id="ddd4c-191">В заданиях обработки эластичных баз данных можно задать пользовательские целевые базы данных, которые можно использовать либо для непосредственного выполнения, либо для включения в пользовательскую группу баз данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="ddd4c-192">Так как **эластичные пулы** еще не поддерживаются API-интерфейсами PowerShell напрямую, достаточно просто создать пользовательскую целевую коллекцию баз данных, охватив таким образом все базы данных в пуле.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="ddd4c-193">Задайте следующие переменные в соответствии с нужными сведениями о базе данных:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-193">Set the following variables to reflect the desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="ddd4c-194">Создание пользовательского целевого семейства баз данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-194">Create a custom database collection target</span></span>
<span data-ttu-id="ddd4c-195">Вы можете указать собственное целевое семейство в нескольких целевых базах данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="ddd4c-196">После создания группы баз данных можно связывать их с пользовательским целевым семейством.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-196">After a database group is created, databases can be associated to the custom collection target.</span></span>

<span data-ttu-id="ddd4c-197">Задайте следующие переменные в соответствии с нужной конфигурацией пользовательского семейства:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-197">Set the following variables to reflect the desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="ddd4c-198">Добавление баз данных в пользовательское целевое семейство баз данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-198">Add databases to a custom database collection target</span></span>
<span data-ttu-id="ddd4c-199">Целевые базы данных можно связывать с целевыми пользовательскими семействами для создания группы баз данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-199">Database targets can be associated with custom database collection targets to create a group of databases.</span></span> <span data-ttu-id="ddd4c-200">При создании задания с целевым пользовательским семейством баз данных оно будет расширено до баз данных, связанных с группой во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span></span>

<span data-ttu-id="ddd4c-201">Добавление нужной базы данных в определенное пользовательское семейство:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-201">Add the desired database to a specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="ddd4c-202">Просмотр баз данных в целевом пользовательском семействе баз данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-202">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="ddd4c-203">Используйте командлет **Get-AzureSqlJobTarget** , чтобы получить дочерние базы данных в пользовательском семействе.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="ddd4c-204">Создание задания для выполнения сценария в пользовательском семействе баз данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-204">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="ddd4c-205">Используйте командлет **New-AzureSqlJob** , чтобы создать задание в группе баз данных, определенной пользовательским семейством баз данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="ddd4c-206">Задания обработки эластичных баз данных расширят задание до нескольких дочерних заданий, каждое из которых соответствует базе данных, связанной с целевым пользовательским семейством, и обеспечивают выполнение сценария для каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="ddd4c-207">Как и ранее, важно, чтобы сценарии были идемпотентными и защищенными от повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-207">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="ddd4c-208">Сбор данных между базами данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-208">Data collection across databases</span></span>
<span data-ttu-id="ddd4c-209">**Задания обработки эластичных баз данных** поддерживают выполнение запроса для группы баз данных и отправку результатов в таблицу указанной базы данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span></span> <span data-ttu-id="ddd4c-210">Позже можно отправить таблице запрос, чтобы увидеть результаты запроса из каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-210">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="ddd4c-211">Это обеспечивает асинхронный механизм выполнения запроса для множества баз данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-211">This provides an asynchronous mechanism to execute a query across many databases.</span></span> <span data-ttu-id="ddd4c-212">Аварийные ситуации, например временная недоступность одной из баз данных, обрабатываются автоматически с помощью повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="ddd4c-213">Указанная целевая таблица будет автоматически создана (если ее еще не существует) в соответствии со схемой возвращенного результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span></span> <span data-ttu-id="ddd4c-214">Если после выполнения сценария возвращается несколько наборов результатов, задания обработки эластичных баз данных будут отправлять в указанную целевую таблицу только первый из них.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span></span>

<span data-ttu-id="ddd4c-215">Следующий сценарий PowerShell можно использовать для выполнения сценария и сбора результатов в указанную таблицу.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span></span> <span data-ttu-id="ddd4c-216">В этом сценарии предполагается, что были созданы сценарий T-SQL, который выводит один набор результатов, и целевое пользовательское семейство баз данных.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="ddd4c-217">Задайте следующие переменные в соответствии с нужными сценарием, учетными данными и целью выполнения:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-217">Set the following to reflect the desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="ddd4c-218">Создание и запуск задания для сбора данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="ddd4c-219">Создание расписания выполнения заданий с помощью триггера</span><span class="sxs-lookup"><span data-stu-id="ddd4c-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="ddd4c-220">Следующий сценарий PowerShell позволяет создать повторяющееся расписание.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-220">The following PowerShell script can be used to create a reoccurring schedule.</span></span> <span data-ttu-id="ddd4c-221">В этом сценарии используется интервал в одну минуту, но командлет New-AzureSqlJobSchedule также поддерживает параметры -DayInterval, -HourInterval, -MonthInterval и -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="ddd4c-222">Расписания, которые выполняются только один раз, можно создавать с помощью параметра -OneTime.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="ddd4c-223">Создание нового расписания</span><span class="sxs-lookup"><span data-stu-id="ddd4c-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-to-have-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="ddd4c-224">Создание триггера для выполнения задания по расписанию</span><span class="sxs-lookup"><span data-stu-id="ddd4c-224">Create a job trigger to have a job executed on a time schedule</span></span>
<span data-ttu-id="ddd4c-225">Вы можете определить триггер задания, который будет выполнять задание согласно расписанию.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-225">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="ddd4c-226">Следующий сценарий PowerShell позволяет создать триггер задания.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-226">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="ddd4c-227">Задайте следующие переменные в соответствии с нужными заданием и расписанием:</span><span class="sxs-lookup"><span data-stu-id="ddd4c-227">Set the following variables to correspond to the desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="ddd4c-228">Удаление запланированной связи для остановки выполнения задания по расписанию</span><span class="sxs-lookup"><span data-stu-id="ddd4c-228">Remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="ddd4c-229">Чтобы остановить регулярное выполнение задания с помощью триггера, можно удалить триггер.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span>
<span data-ttu-id="ddd4c-230">Чтобы удалить триггер и остановить выполнение задания по расписанию, используйте командлет **Remove-AzureSqlJobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="ddd4c-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="ddd4c-231">Импорт в Excel результатов запроса к эластичной базе данных</span><span class="sxs-lookup"><span data-stu-id="ddd4c-231">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="ddd4c-232">Результаты запроса можно импортировать в файл Excel.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-232">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="ddd4c-233">Запустите Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="ddd4c-234">Перейдите на ленту **Данные** .</span><span class="sxs-lookup"><span data-stu-id="ddd4c-234">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="ddd4c-235">Щелкните **Из других источников**, а затем — **Из SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Импорт в Excel из других источников](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="ddd4c-237">В **мастере подключения к данным** введите имя сервера и учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-237">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="ddd4c-238">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-238">Then click **Next**.</span></span>
5. <span data-ttu-id="ddd4c-239">В диалоговом окне **Выберите базу данных, содержащую нужные сведения** выберите базу данных **ElasticDBQuery**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="ddd4c-240">Выберите таблицу **Клиенты** в представлении списка и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-240">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="ddd4c-241">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="ddd4c-242">В форме **Импорт данных** в разделе **Выберите, как следует просматривать эти данные в книге** выберите **Таблица** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="ddd4c-243">Все строки из таблицы **Клиенты** , хранящиеся в различных сегментах, попадают на лист Excel.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddd4c-244">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ddd4c-244">Next steps</span></span>
<span data-ttu-id="ddd4c-245">Теперь можно использовать функции обработки данных Excel.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="ddd4c-246">Для подключения к эластичной базе данных своих инструментов бизнес-аналитики и интеграции данных можно использовать строку подключения с именем сервера, именем базы данных и учетными данными.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="ddd4c-247">Убедитесь, что в качестве источника данных для вашего инструмента поддерживается SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="ddd4c-248">На запрос к эластичной базе данных и внешние таблицы можно ссылаться таким же образом, как и на любую другую базу данных SQL Server и таблицы SQL Server, которые вы хотите подключить с помощью своего инструмента.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="ddd4c-249">Стоимость</span><span class="sxs-lookup"><span data-stu-id="ddd4c-249">Cost</span></span>
<span data-ttu-id="ddd4c-250">Дополнительная плата за использование функции запросов к эластичной базе данных отсутствует.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-250">There is no additional charge for using the Elastic Database query feature.</span></span> <span data-ttu-id="ddd4c-251">Однако в настоящее время эта функция доступна только в базах данных premium как конечная точка, а сегменты могут находиться на любом уровне служб.</span><span class="sxs-lookup"><span data-stu-id="ddd4c-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span></span>

<span data-ttu-id="ddd4c-252">Сведения о ценах см. на [странице с ценами на базу данных SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="ddd4c-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
