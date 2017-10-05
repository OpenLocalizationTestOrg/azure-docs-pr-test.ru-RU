---
title: "Создание заданий обработки эластичных баз данных и управление ими с помощью PowerShell | Документация Майкрософт"
description: "Управление пулами базы данных SQL Azure с помощью PowerShell"
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
ms.openlocfilehash: b4c97e8f51581f9a3f7c5a8d8e82562255fe7b48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="22848-103">Создание заданий обработки эластичных баз данных базы данных SQL и управление ими с помощью PowerShell (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="22848-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="22848-104">С помощью API-интерфейсов PowerShell для **заданий обработки эластичных баз данных** (в предварительной версии) вы можете определить группу баз данных, для которых будут выполняться скрипты.</span><span class="sxs-lookup"><span data-stu-id="22848-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="22848-105">В этой статье рассказывается, как создавать **задания обработки эластичных баз данных** и управлять ими с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22848-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="22848-106">См. статью [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22848-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="22848-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="22848-107">Prerequisites</span></span>
* <span data-ttu-id="22848-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="22848-108">An Azure subscription.</span></span> <span data-ttu-id="22848-109">Зарегистрироваться в пробной версии, которая доступна бесплатно в течение одного месяца, можно [здесь](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22848-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="22848-110">Набор баз данных, созданных с помощью инструментов эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-110">A set of databases created with the Elastic Database tools.</span></span> <span data-ttu-id="22848-111">См. статью [Приступая к работе с инструментами эластичных баз данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="22848-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="22848-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22848-112">Azure PowerShell.</span></span> <span data-ttu-id="22848-113">Дополнительные сведения можно узнать в статье [Установка и настройка Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22848-113">For detailed information, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="22848-114">**Задания обработки эластичных баз данных.** Пакет PowerShell. См. статью [Обзор установки заданий обработки эластичных баз данных](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="22848-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="22848-115">Выбор подписки Azure</span><span class="sxs-lookup"><span data-stu-id="22848-115">Select your Azure subscription</span></span>
<span data-ttu-id="22848-116">Для выбора подписки вам понадобится идентификатор (**-SubscriptionId**) или имя подписки (**-SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="22848-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="22848-117">Если у вас несколько подписок, то можно выполнить командлет **Get-AzureRmSubscription** и скопировать необходимые сведения о подписке из результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="22848-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span></span> <span data-ttu-id="22848-118">Получив сведения о подписке, выполните следующий командлет, чтобы сделать ее подпиской по умолчанию, то есть целью для создания заданий и управления ими.</span><span class="sxs-lookup"><span data-stu-id="22848-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="22848-119">Для написания и выполнения сценариев PowerShell в рамках заданий обработки эластичных баз данных рекомендуется использовать [интегрированную среду сценариев PowerShell](https://technet.microsoft.com/library/dd315244.aspx) .</span><span class="sxs-lookup"><span data-stu-id="22848-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="22848-120">Объекты заданий обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="22848-121">В следующей таблице перечислены все типы объектов **заданий обработки эластичных баз данных** , а также приведены их описания и связанные API PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22848-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="22848-122">Тип объекта</span><span class="sxs-lookup"><span data-stu-id="22848-122">Object Type</span></span></th>
    <th><span data-ttu-id="22848-123">Описание</span><span class="sxs-lookup"><span data-stu-id="22848-123">Description</span></span></th>
    <th><span data-ttu-id="22848-124">Связанные API-интерфейсы PowerShell</span><span class="sxs-lookup"><span data-stu-id="22848-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="22848-125">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="22848-125">Credential</span></span></td>
    <td><span data-ttu-id="22848-126">Имя пользователя и пароль, используемые при подключении к базам данных для выполнения сценариев или применением файлов DACPAC.</span><span class="sxs-lookup"><span data-stu-id="22848-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="22848-127">Пароль зашифровывается перед отправкой в базу данных заданий обработки эластичных баз данных и хранения в ней.</span><span class="sxs-lookup"><span data-stu-id="22848-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span></span>  <span data-ttu-id="22848-128">Пароль шифруется службой заданий обработки эластичных баз данных с помощью учетных данных, созданных и отправленных из сценария установки.</span><span class="sxs-lookup"><span data-stu-id="22848-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span></span></td>
    <td><p><span data-ttu-id="22848-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="22848-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="22848-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="22848-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="22848-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="22848-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="22848-132">Скрипт</span><span class="sxs-lookup"><span data-stu-id="22848-132">Script</span></span></td>
    <td><span data-ttu-id="22848-133">Сценарий Transact-SQL для выполнения между базами данных.</span><span class="sxs-lookup"><span data-stu-id="22848-133">Transact-SQL script to be used for execution across databases.</span></span>  <span data-ttu-id="22848-134">Сценарий должен быть создан идемпотентным, так как служба будет повторять попытку выполнения сценария в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="22848-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="22848-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="22848-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="22848-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="22848-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="22848-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="22848-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="22848-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="22848-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="22848-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="22848-139">DACPAC</span></span></td>
    <td><span data-ttu-id="22848-140">Пакет <a href="https://msdn.microsoft.com/library/ee210546.aspx">приложения уровня данных</a>, применяемый между базами данных.</span><span class="sxs-lookup"><span data-stu-id="22848-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="22848-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="22848-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="22848-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="22848-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="22848-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="22848-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="22848-144">Целевая база данных</span><span class="sxs-lookup"><span data-stu-id="22848-144">Database Target</span></span></td>
    <td><span data-ttu-id="22848-145">База данных и имя сервера, указывающие на Базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="22848-145">Database and server name pointing to an Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="22848-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="22848-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="22848-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="22848-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="22848-148">Целевая карта сегментов</span><span class="sxs-lookup"><span data-stu-id="22848-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="22848-149">Сочетание целевой базы данных и учетных данных, используемое для определения сведений, хранящихся в карте сегментов эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="22848-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="22848-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="22848-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="22848-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="22848-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="22848-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="22848-153">Целевая пользовательская коллекция</span><span class="sxs-lookup"><span data-stu-id="22848-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="22848-154">Группа баз данных, заданная для коллективного выполнения.</span><span class="sxs-lookup"><span data-stu-id="22848-154">Defined group of databases to collectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="22848-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="22848-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="22848-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="22848-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="22848-157">Целевая дочерняя пользовательская коллекция</span><span class="sxs-lookup"><span data-stu-id="22848-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="22848-158">Целевая база данных, на которую ссылается пользовательская коллекция.</span><span class="sxs-lookup"><span data-stu-id="22848-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="22848-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="22848-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="22848-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="22848-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="22848-161">Задание</span><span class="sxs-lookup"><span data-stu-id="22848-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="22848-162">Определение параметров для задания, которое можно использовать для выполнения или исполнения расписания.</span><span class="sxs-lookup"><span data-stu-id="22848-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="22848-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="22848-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="22848-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="22848-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="22848-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="22848-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="22848-166">Выполнение заданий</span><span class="sxs-lookup"><span data-stu-id="22848-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="22848-167">Контейнер заданий, которые необходимо выполнить с помощью сценария или применения файла DACPAC к цели с помощью учетных данных для подключений к базам данных с обработкой сбоев в соответствии с политикой выполнения.</span><span class="sxs-lookup"><span data-stu-id="22848-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="22848-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="22848-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="22848-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="22848-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="22848-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="22848-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="22848-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="22848-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="22848-172">Выполнение задач</span><span class="sxs-lookup"><span data-stu-id="22848-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="22848-173">Одна единица работы для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="22848-173">Single unit of work to fulfill a job.</span></span></p>
    <p><span data-ttu-id="22848-174">Если задаче не удается успешно выполниться, соответствующее сообщение об исключении будет записано в журнал и будет создана новая идентичная задача, которая выполняется в соответствии с указанной политикой выполнения.</span><span class="sxs-lookup"><span data-stu-id="22848-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="22848-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="22848-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="22848-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="22848-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="22848-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="22848-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="22848-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="22848-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="22848-179">Политика выполнения заданий</span><span class="sxs-lookup"><span data-stu-id="22848-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="22848-180">Управляет временем ожидания выполнения заданий, максимальными количествами повторных попыток и интервалами между ними.</span><span class="sxs-lookup"><span data-stu-id="22848-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="22848-181">Задания обработки эластичных баз данных включают стандартную политику выполнения, которая вызывает практически неограниченное число повторных попыток в случае сбоя задач с экспоненциально растущим интервалом между ними.</span><span class="sxs-lookup"><span data-stu-id="22848-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="22848-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="22848-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="22848-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="22848-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="22848-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="22848-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="22848-185">Расписание</span><span class="sxs-lookup"><span data-stu-id="22848-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="22848-186">Выбор выполнения с определенным интервалом или один раз.</span><span class="sxs-lookup"><span data-stu-id="22848-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="22848-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="22848-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="22848-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="22848-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="22848-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="22848-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="22848-190">Триггеры заданий</span><span class="sxs-lookup"><span data-stu-id="22848-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="22848-191">Сопоставление для выполнения задания по расписанию.</span><span class="sxs-lookup"><span data-stu-id="22848-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="22848-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="22848-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="22848-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="22848-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="22848-194">Поддерживаемые типы групп заданий обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="22848-195">Задания позволяют выполнять сценарии Transact-SQL (T-SQL) или применять файлы DACPAC в группе баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="22848-196">Когда задание отправляется на выполнение в группе баз данных, оно «разбивается» на дочерние задания, каждое из которых выполняет нужную задачу в отдельной базе данных из группы.</span><span class="sxs-lookup"><span data-stu-id="22848-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span></span> 

<span data-ttu-id="22848-197">Вы можете создать группу одного из двух типов.</span><span class="sxs-lookup"><span data-stu-id="22848-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="22848-198">Группа [Карта сегментов](sql-database-elastic-scale-shard-map-management.md). Когда задание отправляется для обработки карты сегментов, оно сначала отправляет карте сегментов запрос, чтобы определить текущий набор сегментов, а затем создает дочерние задания для каждого сегмента в карте.</span><span class="sxs-lookup"><span data-stu-id="22848-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span></span>
* <span data-ttu-id="22848-199">Группа «Пользовательская коллекция»: определяемый пользователем набор баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="22848-200">Задание, целью которого является пользовательская коллекция, создает дочерние задания для каждой базы данных в пользовательской коллекции.</span><span class="sxs-lookup"><span data-stu-id="22848-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span></span>

## <a name="to-set-the-elastic-database-jobs-connection"></a><span data-ttu-id="22848-201">Настройка подключения к заданиям обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-201">To set the Elastic Database jobs connection</span></span>
<span data-ttu-id="22848-202">Чтобы использовать API-интерфейсы заданий, сначала нужно настроить подключение к *управляющей базе данных* заданий.</span><span class="sxs-lookup"><span data-stu-id="22848-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span></span> <span data-ttu-id="22848-203">При вызове приведенного ниже командлета открывается окно ввода учетных данных, где пользователь должен указать имя и пароль, предоставленные во время установки заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="22848-204">Во всех примерах из этого раздела предполагается, что первый этап уже выполнен.</span><span class="sxs-lookup"><span data-stu-id="22848-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="22848-205">Откройте подключение к заданиям обработки эластичных баз данных:</span><span class="sxs-lookup"><span data-stu-id="22848-205">Open a connection to the Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-the-elastic-database-jobs"></a><span data-ttu-id="22848-206">Зашифрованные учетные данные в заданиях обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-206">Encrypted credentials within the Elastic Database jobs</span></span>
<span data-ttu-id="22848-207">Учетные данные баз данных можно вставлять в *управляющую базу данных* заданий с зашифрованным паролем.</span><span class="sxs-lookup"><span data-stu-id="22848-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="22848-208">Такая возможность полезна для хранения учетных данных, что позволяет выполнять задания позже (с использованием расписаний заданий).</span><span class="sxs-lookup"><span data-stu-id="22848-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="22848-209">Шифрование работает с помощью сертификата, созданного сценарием установки.</span><span class="sxs-lookup"><span data-stu-id="22848-209">Encryption works through a certificate created as part of the installation script.</span></span> <span data-ttu-id="22848-210">Сценарий установки создает и отправляет сертификат в облачную службу Azure для шифрования сохраненных паролей шифрования.</span><span class="sxs-lookup"><span data-stu-id="22848-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span></span> <span data-ttu-id="22848-211">Потом облачная служба Azure сохраняет открытый ключ в *управляющей базе данных* заданий, что позволяет API-интерфейсу PowerShell или интерфейсу классического портала Azure шифровать предоставленный пароль и не требовать наличия локально установленного сертификата.</span><span class="sxs-lookup"><span data-stu-id="22848-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span></span>

<span data-ttu-id="22848-212">Пароли учетных данных шифруются и защищаются от пользователей, которые могут только читать объекты заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span></span> <span data-ttu-id="22848-213">Однако злоумышленник, имеющий права читать и записывать объекты заданий обработки эластичных баз данных, вероятно, сможет извлечь пароль.</span><span class="sxs-lookup"><span data-stu-id="22848-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span></span> <span data-ttu-id="22848-214">Учетные данные рассчитаны на повторное использования при разных запусках задания.</span><span class="sxs-lookup"><span data-stu-id="22848-214">Credentials are designed to be reused across job executions.</span></span> <span data-ttu-id="22848-215">Учетные данные передаются целевым базам данных при установке соединений.</span><span class="sxs-lookup"><span data-stu-id="22848-215">Credentials are passed to target databases when establishing connections.</span></span> <span data-ttu-id="22848-216">В настоящее время не существует ограничений для целевых баз данных, используемых для каждого набора учетных данных, и злоумышленник может добавлять целевые объекты для базы данных, которой он управляет.</span><span class="sxs-lookup"><span data-stu-id="22848-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span></span> <span data-ttu-id="22848-217">Пользователь может впоследствии запустить задание для этой базы данных, чтобы получить пароль для входа в учетную запись.</span><span class="sxs-lookup"><span data-stu-id="22848-217">The user could subsequently start a job targeting this database to gain the credential's password.</span></span>

<span data-ttu-id="22848-218">При работе с заданиями обработки эластичных баз данных мы рекомендуем использовать такие меры безопасности.</span><span class="sxs-lookup"><span data-stu-id="22848-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="22848-219">Предоставляйте доступ к API-интерфейсам только доверенным лицам.</span><span class="sxs-lookup"><span data-stu-id="22848-219">Limit usage of the APIs to trusted individuals.</span></span>
* <span data-ttu-id="22848-220">Учетные данные должны иметь только те права, которые необходимы для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="22848-220">Credentials should have the least privileges necessary to perform the job task.</span></span>  <span data-ttu-id="22848-221">Дополнительные сведения см. на сайте MSDN в статье [Проверка прав доступа и разрешений в SQL Server](https://msdn.microsoft.com/library/bb669084.aspx).</span><span class="sxs-lookup"><span data-stu-id="22848-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="to-create-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="22848-222">Создание зашифрованных учетных данных для выполнения заданий в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="22848-222">To create an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="22848-223">Чтобы создать новые зашифрованные учетные данные, командлет [**Get-Credential**](https://technet.microsoft.com/library/hh849815.aspx) запрашивает имя пользователя и пароль, которые можно передать в командлет [**New-AzureSqlJobCredential**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="22848-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="to-update-credentials"></a><span data-ttu-id="22848-224">Изменение учетных данных</span><span class="sxs-lookup"><span data-stu-id="22848-224">To update credentials</span></span>
<span data-ttu-id="22848-225">При изменении пароля используйте командлет [**Set-AzureSqlJobCredential**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) с параметром **CredentialName**.</span><span class="sxs-lookup"><span data-stu-id="22848-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set the **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="to-define-an-elastic-database-shard-map-target"></a><span data-ttu-id="22848-226">Определение целевого объекта карты сегментов эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-226">To define an Elastic Database shard map target</span></span>
<span data-ttu-id="22848-227">Чтобы выполнить задание во всех базах данных в карте сегментов (созданной с помощью [клиентской библиотеки эластичных баз данных](sql-database-elastic-database-client-library.md)), используйте в качестве целевого объекта базы данных карту сегментов.</span><span class="sxs-lookup"><span data-stu-id="22848-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span></span> <span data-ttu-id="22848-228">Для этого примера требуется сегментированное приложение, созданное с помощью клиентской библиотеки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-228">This example requires a sharded application created using the Elastic Database client library.</span></span> <span data-ttu-id="22848-229">См. статью [Приступая к работе с инструментами эластичных баз данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="22848-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="22848-230">Для этого базу данных диспетчера карт сегментов необходимо указать как целевой объект базы данных, а затем в качестве целевого объекта указать конкретную карту сегментов.</span><span class="sxs-lookup"><span data-stu-id="22848-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="22848-231">Создание сценария T-SQL для выполнения в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="22848-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="22848-232">При создании сценариев T-SQL мы настоятельно рекомендуется делать их [идемпотентными](https://en.wikipedia.org/wiki/Idempotence) и защищенными от сбоев.</span><span class="sxs-lookup"><span data-stu-id="22848-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="22848-233">Задания обработки эластичных баз данных повторяют попытку выполнения сценария в случае сбоя, независимо от типа ошибки.</span><span class="sxs-lookup"><span data-stu-id="22848-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span></span>

<span data-ttu-id="22848-234">С помощью командлета [**New-AzureSqlJobContent**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent), указав параметры **-ContentName** и **-CommandText**, создайте и сохраните нужный скрипт.</span><span class="sxs-lookup"><span data-stu-id="22848-234">Use the [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span></span>

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

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="22848-235">Создание нового сценария из файла</span><span class="sxs-lookup"><span data-stu-id="22848-235">Create a new script from a file</span></span>
<span data-ttu-id="22848-236">Если сценарий T-SQL определен в файле, импортируйте сценарий с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="22848-236">If the T-SQL script is defined within a file, use this to import the script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path to SQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="to-update-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="22848-237">Изменение сценария T-SQL, который должен выполняться в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="22848-237">To update a T-SQL script for execution across databases</span></span>
<span data-ttu-id="22848-238">Приведенный ниже сценарий PowerShell изменяет текст команды T-SQL для существующего сценария.</span><span class="sxs-lookup"><span data-stu-id="22848-238">This PowerShell script updates the T-SQL command text for an existing script.</span></span>

<span data-ttu-id="22848-239">Задайте следующие переменные в соответствии с нужным определением сценария:</span><span class="sxs-lookup"><span data-stu-id="22848-239">Set the following variables to reflect the desired script definition to be set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column to TestTable"
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

### <a name="to-update-the-definition-to-an-existing-script"></a><span data-ttu-id="22848-240">Изменение определения в соответствии с существующим сценарием</span><span class="sxs-lookup"><span data-stu-id="22848-240">To update the definition to an existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="to-create-a-job-to-execute-a-script-across-a-shard-map"></a><span data-ttu-id="22848-241">Создание задания, которое будет выполнять сценарий в карте сегментов</span><span class="sxs-lookup"><span data-stu-id="22848-241">To create a job to execute a script across a shard map</span></span>
<span data-ttu-id="22848-242">Приведенный ниже сценарий PowerShell запускает задание, которое выполнит сценарий в каждом сегменте карты с динамическим масштабированием.</span><span class="sxs-lookup"><span data-stu-id="22848-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="22848-243">Задайте следующие переменные в соответствии с нужными сценарием и целью:</span><span class="sxs-lookup"><span data-stu-id="22848-243">Set the following variables to reflect the desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="to-execute-a-job"></a><span data-ttu-id="22848-244">Выполнение задания</span><span class="sxs-lookup"><span data-stu-id="22848-244">To execute a job</span></span>
<span data-ttu-id="22848-245">Приведенный ниже сценарий PowerShell выполняет существующее задание.</span><span class="sxs-lookup"><span data-stu-id="22848-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="22848-246">Измените следующую переменную в соответствии с именем выполняемого задания:</span><span class="sxs-lookup"><span data-stu-id="22848-246">Update the following variable to reflect the desired job name to have executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="to-retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="22848-247">Получение сведений о состоянии выполнения одного задания</span><span class="sxs-lookup"><span data-stu-id="22848-247">To retrieve the state of a single job execution</span></span>
<span data-ttu-id="22848-248">Чтобы просмотреть сведения о состоянии выполнения задания, выполните командлет [**Get-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) с параметром **JobExecutionId**.</span><span class="sxs-lookup"><span data-stu-id="22848-248">Use the [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set the **JobExecutionId** parameter to view the state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="22848-249">Чтобы узнать состояние выполнения дочерних заданий, в частности состояние каждого задания в каждой целевой базе данных, используйте тот же командлет **Get-AzureSqlJobExecution** с параметром **IncludeChildren**.</span><span class="sxs-lookup"><span data-stu-id="22848-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="to-view-the-state-across-multiple-job-executions"></a><span data-ttu-id="22848-250">Просмотр сведений о состоянии выполнения нескольких заданий</span><span class="sxs-lookup"><span data-stu-id="22848-250">To view the state across multiple job executions</span></span>
<span data-ttu-id="22848-251">У командлета [**Get-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/new-azuresqljob) есть несколько необязательных параметров, позволяющих увидеть ход выполнения нескольких заданий, отфильтрованных по указанным параметрам.</span><span class="sxs-lookup"><span data-stu-id="22848-251">The [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="22848-252">Ниже показаны некоторые из возможных способов использования командлета Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="22848-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="22848-253">Получение сведений о выполнении всех активных заданий верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="22848-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="22848-254">Получение сведений о выполнении всех заданий верхнего уровня, включая неактивные задания:</span><span class="sxs-lookup"><span data-stu-id="22848-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="22848-255">Получение состояния выполнения всех дочерних заданий, включая неактивные, по указанному идентификатору выполнения задания:</span><span class="sxs-lookup"><span data-stu-id="22848-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="22848-256">Получение состояния выполнения всех заданий, созданных с помощью сочетания расписания и задания, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="22848-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="22848-257">Получение сведения обо всех заданиях в указанной карте сегментов, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="22848-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="22848-258">Получение сведения обо всех заданиях в указанном пользовательском семействе, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="22848-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="22848-259">Получение списка выполнения задач в определенном задании:</span><span class="sxs-lookup"><span data-stu-id="22848-259">Retrieve the list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="22848-260">Получение сведений о выполнении задачи:</span><span class="sxs-lookup"><span data-stu-id="22848-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="22848-261">Следующий сценарий PowerShell позволяет просмотреть сведения о выполнении задачи, что особенно полезно при отладке сбоев выполнения.</span><span class="sxs-lookup"><span data-stu-id="22848-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="to-retrieve-failures-within-job-task-executions"></a><span data-ttu-id="22848-262">Получение ошибок при выполнении задач</span><span class="sxs-lookup"><span data-stu-id="22848-262">To retrieve failures within job task executions</span></span>
<span data-ttu-id="22848-263">Объект **JobTaskExecution** содержит свойство жизненного цикла задачи (Lifecycle) и свойство сообщения (Message).</span><span class="sxs-lookup"><span data-stu-id="22848-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span></span> <span data-ttu-id="22848-264">Если выполнение какой-либо задачи задания завершилось сбоем, свойство Lifecycle принимает значение *Failed* , а свойство Message — сообщение об исключении и его стек.</span><span class="sxs-lookup"><span data-stu-id="22848-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="22848-265">Если задание завершилось неудачно, важно просмотреть сведения задачах, которые не были выполнены в определенном задании.</span><span class="sxs-lookup"><span data-stu-id="22848-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="to-wait-for-a-job-execution-to-complete"></a><span data-ttu-id="22848-266">Ожидание завершения выполнения задания</span><span class="sxs-lookup"><span data-stu-id="22848-266">To wait for a job execution to complete</span></span>
<span data-ttu-id="22848-267">Следующий сценарий PowerShell позволяет дождаться завершения задачи:</span><span class="sxs-lookup"><span data-stu-id="22848-267">The following PowerShell script can be used to wait for a job task to complete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="22848-268">Создание пользовательской политики выполнения</span><span class="sxs-lookup"><span data-stu-id="22848-268">Create a custom execution policy</span></span>
<span data-ttu-id="22848-269">Задания обработки эластичных баз данных поддерживают создание пользовательских политик выполнения, которые можно применять при запуске заданий.</span><span class="sxs-lookup"><span data-stu-id="22848-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="22848-270">В настоящий момент политики выполнения позволяют задать следующее:</span><span class="sxs-lookup"><span data-stu-id="22848-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="22848-271">Имя: идентификатор политики выполнения.</span><span class="sxs-lookup"><span data-stu-id="22848-271">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="22848-272">Время ожидания задания: общее время до отмены задания службой заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="22848-273">Исходный интервал повторных попыток: интервал ожидания до первой повторной попытки.</span><span class="sxs-lookup"><span data-stu-id="22848-273">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="22848-274">Максимальный интервал повторных попыток: предел используемых интервалов повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="22848-274">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="22848-275">Коэффициент роста интервала повторных попыток: коэффициент, используемый для вычисления следующего интервала между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="22848-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="22848-276">Используется следующая формула: (Исходный интервал повторных попыток) * Math.pow((Коэффициент роста интервала), (Число повторных попыток) - 2).</span><span class="sxs-lookup"><span data-stu-id="22848-276">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="22848-277">Максимальное число попыток: максимальное число повторных попыток, выполняемых в задании.</span><span class="sxs-lookup"><span data-stu-id="22848-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="22848-278">В политике выполнения по умолчанию используются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="22848-278">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="22848-279">Имя: политика выполнения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="22848-279">Name: Default execution policy</span></span>
* <span data-ttu-id="22848-280">Время ожидания задания: 1 неделя</span><span class="sxs-lookup"><span data-stu-id="22848-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="22848-281">Исходный интервал повторных попыток: 100 миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="22848-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="22848-282">Максимальный интервал повторных попыток: 30 минут</span><span class="sxs-lookup"><span data-stu-id="22848-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="22848-283">Коэффициент интервала повторных попыток: 2</span><span class="sxs-lookup"><span data-stu-id="22848-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="22848-284">Максимальное число попыток: 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="22848-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="22848-285">Создайте нужную политику выполнения:</span><span class="sxs-lookup"><span data-stu-id="22848-285">Create the desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="22848-286">Изменение пользовательской политики выполнения</span><span class="sxs-lookup"><span data-stu-id="22848-286">Update a custom execution policy</span></span>
<span data-ttu-id="22848-287">Измените нужную политику выполнения:</span><span class="sxs-lookup"><span data-stu-id="22848-287">Update the desired execution policy to update:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="22848-288">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="22848-288">Cancel a job</span></span>
<span data-ttu-id="22848-289">Задания обработки эластичных баз данных поддерживают запросы на отмену заданий.</span><span class="sxs-lookup"><span data-stu-id="22848-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="22848-290">Если служба заданий обработки эластичных баз данных обнаружат запрос на отмену выполняемого задания, она попытается остановить задачу.</span><span class="sxs-lookup"><span data-stu-id="22848-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="22848-291">Служба заданий обработки эластичных баз данных может выполнить отмену двумя разными способами:</span><span class="sxs-lookup"><span data-stu-id="22848-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="22848-292">Отмена выполняющихся задач. Если отмена обнаружена во время выполнения задачи, система пытается отменить выполняющийся аспект задачи.</span><span class="sxs-lookup"><span data-stu-id="22848-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="22848-293">Например: если при попытке отмены выполняется длинный запрос, произойдет попытка его отмены.</span><span class="sxs-lookup"><span data-stu-id="22848-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="22848-294">Отмена повторных попыток выполнения задачи. Если управляющий поток обнаружит отмену до начала выполнения задачи, он не будет запускать задачу и объявит запрос отмененным.</span><span class="sxs-lookup"><span data-stu-id="22848-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="22848-295">В случае запроса отмены родительского задания этот запрос будет выполнен для родительского задания и всех его дочерних заданий.</span><span class="sxs-lookup"><span data-stu-id="22848-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="22848-296">Чтобы отправить запрос на отмену, используйте командлет [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) с параметром **JobExecutionId**.</span><span class="sxs-lookup"><span data-stu-id="22848-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set the **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="to-delete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="22848-297">Асинхронное удаление задания и журнала заданий</span><span class="sxs-lookup"><span data-stu-id="22848-297">To delete a job and job history asynchronously</span></span>
<span data-ttu-id="22848-298">Задания обработки эластичных баз данных поддерживают асинхронное удаление заданий.</span><span class="sxs-lookup"><span data-stu-id="22848-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="22848-299">Задания могут быть отмечены для удаления, а система удалит задание и весь его журнал после завершения всех выполнений задания.</span><span class="sxs-lookup"><span data-stu-id="22848-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="22848-300">Система не будет автоматически отменять активные выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="22848-300">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="22848-301">Чтобы отменить уже выполняющиеся задания, выполните командлет [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution).</span><span class="sxs-lookup"><span data-stu-id="22848-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) to cancel active job executions.</span></span>

<span data-ttu-id="22848-302">Чтобы запустить удаление задания, выполните командлет [**Remove-AzureSqlJob**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) с параметром **JobName**.</span><span class="sxs-lookup"><span data-stu-id="22848-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set the **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="to-create-a-custom-database-target"></a><span data-ttu-id="22848-303">Создание целевого объекта пользовательской базы данных</span><span class="sxs-lookup"><span data-stu-id="22848-303">To create a custom database target</span></span>
<span data-ttu-id="22848-304">Вы можете определять целевые объекты пользовательской базы данных для выполнения напрямую или для включения в группу пользовательских баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="22848-305">Например, так как **пулы эластичных баз данных** пока нельзя использовать напрямую через API-интерфейсы PowerShell, вы можете создать пользовательское целевое семейство баз данных, охватив, таким образом, все базы данных в пуле.</span><span class="sxs-lookup"><span data-stu-id="22848-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="22848-306">Задайте следующие переменные в соответствии с нужными сведениями о базе данных:</span><span class="sxs-lookup"><span data-stu-id="22848-306">Set the following variables to reflect the desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="to-create-a-custom-database-collection-target"></a><span data-ttu-id="22848-307">Создание целевого объекта пользовательской коллекции баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-307">To create a custom database collection target</span></span>
<span data-ttu-id="22848-308">Чтобы определить целевой объект пользовательской коллекции баз данных и разрешить выполнение задания в нескольких определенных целевых объектах баз данных, используйте командлет [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget).</span><span class="sxs-lookup"><span data-stu-id="22848-308">Use the [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="22848-309">После создания группы баз данных их можно связать с целевым объектом пользовательской коллекции.</span><span class="sxs-lookup"><span data-stu-id="22848-309">After creating a database group, databases can be associated with the custom collection target.</span></span>

<span data-ttu-id="22848-310">Задайте следующие переменные в соответствии с нужной конфигурацией пользовательского семейства:</span><span class="sxs-lookup"><span data-stu-id="22848-310">Set the following variables to reflect the desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="to-add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="22848-311">Добавление баз данных в целевой объект пользовательской коллекции баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-311">To add databases to a custom database collection target</span></span>
<span data-ttu-id="22848-312">Чтобы добавить базу данных в определенную пользовательскую коллекцию, используйте командлет [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget).</span><span class="sxs-lookup"><span data-stu-id="22848-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="22848-313">Просмотр баз данных в целевом объекте пользовательской коллекции баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-313">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="22848-314">Используйте командлет [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget), чтобы получить дочерние базы данных в пользовательском семействе.</span><span class="sxs-lookup"><span data-stu-id="22848-314">Use the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to retrieve the child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="22848-315">Создание задания для выполнения сценария в пользовательской коллекции баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-315">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="22848-316">Используйте командлет [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob), чтобы создать задание в группе баз данных, определенной пользовательским семейством баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-316">Use the [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="22848-317">Задания обработки эластичных баз данных расширят задание до нескольких дочерних заданий, каждое из которых соответствует базе данных, связанной с целевым пользовательским семейством, и обеспечивают выполнение сценария для каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="22848-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="22848-318">Как и ранее, важно, чтобы сценарии были идемпотентными и защищенными от повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="22848-318">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="22848-319">Сбор данных из нескольких баз данных</span><span class="sxs-lookup"><span data-stu-id="22848-319">Data collection across databases</span></span>
<span data-ttu-id="22848-320">С помощью задания вы можете выполнить запрос в группе баз данных и отправить результаты в специальную таблицу.</span><span class="sxs-lookup"><span data-stu-id="22848-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span></span> <span data-ttu-id="22848-321">Позже можно отправить таблице запрос, чтобы увидеть результаты запроса из каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="22848-321">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="22848-322">Это обеспечивает асинхронный механизм выполнения запроса для множества баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-322">This provides an asynchronous method to execute a query across many databases.</span></span> <span data-ttu-id="22848-323">После неудачной попытки автоматически выполняется повторная попытка.</span><span class="sxs-lookup"><span data-stu-id="22848-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="22848-324">Указанная целевая таблица создается автоматически (если она еще не создана).</span><span class="sxs-lookup"><span data-stu-id="22848-324">The specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="22848-325">Новая таблица соответствует схеме возвращенного результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="22848-325">The new table matches the schema of the returned result set.</span></span> <span data-ttu-id="22848-326">Если сценарий возвращает несколько наборов результатов, задания обработки эластичных баз данных отправляют в указанную целевую таблицу только первый набор.</span><span class="sxs-lookup"><span data-stu-id="22848-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span></span>

<span data-ttu-id="22848-327">Приведенный ниже сценарий PowerShell выполняет сценарий и собирает результаты в указанную таблицу.</span><span class="sxs-lookup"><span data-stu-id="22848-327">The following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="22848-328">В этом сценарии предполагается, что у вас уже есть сценарий T-SQL, который возвращает один набор результатов, и целевой объект пользовательской коллекции баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="22848-329">В этом скрипте используется командлет [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget).</span><span class="sxs-lookup"><span data-stu-id="22848-329">This script uses the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="22848-330">Укажите параметры для сценария, учетные данные и целевой объект задания.</span><span class="sxs-lookup"><span data-stu-id="22848-330">Set the parameters for script, credentials, and execution target:</span></span>

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

### <a name="to-create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="22848-331">Создание и запуск задания для сбора данных</span><span class="sxs-lookup"><span data-stu-id="22848-331">To create and start a job for data collection scenarios</span></span>
<span data-ttu-id="22848-332">В этом скрипте используется командлет [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution).</span><span class="sxs-lookup"><span data-stu-id="22848-332">This script uses the [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

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

## <a name="to-schedule-a-job-execution-trigger"></a><span data-ttu-id="22848-333">Создание расписания для задания</span><span class="sxs-lookup"><span data-stu-id="22848-333">To schedule a job execution trigger</span></span>
<span data-ttu-id="22848-334">Приведенный ниже сценарий PowerShell можно использовать для создания повторяющегося расписания.</span><span class="sxs-lookup"><span data-stu-id="22848-334">The following PowerShell script can be used to create a recurring schedule.</span></span> <span data-ttu-id="22848-335">В этом скрипте используется интервал в минутах, но командлет [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) также поддерживает параметры -DayInterval, -HourInterval, -MonthInterval и -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="22848-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="22848-336">Расписания, которые выполняются только один раз, можно создавать с помощью параметра -OneTime.</span><span class="sxs-lookup"><span data-stu-id="22848-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="22848-337">Создание нового расписания</span><span class="sxs-lookup"><span data-stu-id="22848-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="to-trigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="22848-338">Активация задания по расписанию</span><span class="sxs-lookup"><span data-stu-id="22848-338">To trigger a job executed on a time schedule</span></span>
<span data-ttu-id="22848-339">Вы можете определить триггер задания, который будет выполнять задание согласно расписанию.</span><span class="sxs-lookup"><span data-stu-id="22848-339">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="22848-340">Следующий сценарий PowerShell позволяет создать триггер задания.</span><span class="sxs-lookup"><span data-stu-id="22848-340">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="22848-341">Используйте командлет [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) и задайте переменные в соответствии с нужными заданием и расписанием.</span><span class="sxs-lookup"><span data-stu-id="22848-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set the following variables to correspond to the desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="to-remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="22848-342">Удаление расписания задания</span><span class="sxs-lookup"><span data-stu-id="22848-342">To remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="22848-343">Чтобы остановить повторяющееся выполнение задания по расписанию, можно удалить расписание.</span><span class="sxs-lookup"><span data-stu-id="22848-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span> <span data-ttu-id="22848-344">Чтобы удалить триггер и остановить выполнение задания по расписанию, используйте командлет [**Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="22848-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-to-a-time-schedule"></a><span data-ttu-id="22848-345">Получение триггеров заданий, связанных с расписанием</span><span class="sxs-lookup"><span data-stu-id="22848-345">Retrieve job triggers bound to a time schedule</span></span>
<span data-ttu-id="22848-346">Следующий сценарий PowerShell позволяет получить и вывести на экран триггеры заданий, зарегистрированных с определенным расписанием.</span><span class="sxs-lookup"><span data-stu-id="22848-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="to-retrieve-job-triggers-bound-to-a-job"></a><span data-ttu-id="22848-347">Получение триггеров, связанных с заданием</span><span class="sxs-lookup"><span data-stu-id="22848-347">To retrieve job triggers bound to a job</span></span>
<span data-ttu-id="22848-348">Чтобы получить и отобразить расписания, содержащие зарегистрированное задание, используйте командлет [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) .</span><span class="sxs-lookup"><span data-stu-id="22848-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) to obtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="to-create-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="22848-349">Создание приложения уровня данных (DACPAC) для выполнения в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="22848-349">To create a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="22848-350">Сведения о создании пакета DACPAC см. в статье [Приложения уровня данных](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="22848-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="22848-351">Чтобы развернуть пакет DACPAC, используйте командлет [New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="22848-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="22848-352">Пакет DACPAC должен быть доступен для службы.</span><span class="sxs-lookup"><span data-stu-id="22848-352">The DACPAC must be accessible to the service.</span></span> <span data-ttu-id="22848-353">Созданный пакет DACPAC рекомендуется отправить в хранилище Azure и создать для него [подписанный URL-адрес](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="22848-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="to-update-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="22848-354">Изменение приложения уровня данных (DACPAC) для его выполнения в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="22848-354">To update a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="22848-355">Имеющиеся файлы DACPAC, зарегистрированные в заданиях обработки эластичных баз данных, можно изменить, чтобы они указывали на новые URI.</span><span class="sxs-lookup"><span data-stu-id="22848-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span></span> <span data-ttu-id="22848-356">Чтобы изменить URI имеющегося зарегистрированного пакета DACPAC, используйте командлет [**Set-AzureSqlJobContentDefinition**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition).</span><span class="sxs-lookup"><span data-stu-id="22848-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) to update the DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="to-create-a-job-to-apply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="22848-357">Создание задания для применения пакета DACPAC в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="22848-357">To create a job to apply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="22848-358">После создания DACPAC в службе заданий обработки эластичных баз данных можно создать задание для применения DACPAC к группе баз данных.</span><span class="sxs-lookup"><span data-stu-id="22848-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span></span> <span data-ttu-id="22848-359">Следующий сценарий PowerShell позволяет создать задание DACPAC в пользовательском семействе баз данных:</span><span class="sxs-lookup"><span data-stu-id="22848-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span></span>

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
