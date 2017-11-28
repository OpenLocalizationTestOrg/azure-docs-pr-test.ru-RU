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
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="f5e12-103">Создание заданий обработки эластичных баз данных базы данных SQL и управление ими с помощью PowerShell (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="f5e12-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="f5e12-104">Hello API-интерфейсов PowerShell для **заданий эластичных баз данных** (в предварительной версии), позволяют определить группы баз данных, для которых они будут выполняться.</span><span class="sxs-lookup"><span data-stu-id="f5e12-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="f5e12-105">В этой статье показано, как toocreate и управление ими **заданий эластичных баз данных** с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5e12-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="f5e12-106">См. статью [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5e12-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f5e12-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f5e12-107">Prerequisites</span></span>
* <span data-ttu-id="f5e12-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="f5e12-108">An Azure subscription.</span></span> <span data-ttu-id="f5e12-109">Зарегистрироваться в пробной версии, которая доступна бесплатно в течение одного месяца, можно [здесь](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5e12-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f5e12-110">Набор баз данных, созданных с помощью средств hello эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="f5e12-111">См. статью [Приступая к работе с инструментами эластичных баз данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f5e12-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="f5e12-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5e12-112">Azure PowerShell.</span></span> <span data-ttu-id="f5e12-113">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f5e12-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="f5e12-114">**Задания обработки эластичных баз данных.** Пакет PowerShell. См. статью [Обзор установки заданий обработки эластичных баз данных](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="f5e12-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="f5e12-115">Выбор подписки Azure</span><span class="sxs-lookup"><span data-stu-id="f5e12-115">Select your Azure subscription</span></span>
<span data-ttu-id="f5e12-116">tooselect hello подписки требуется идентификатор подписки (**- SubscriptionId**) или имя подписки (**- SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="f5e12-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="f5e12-117">Если у вас несколько подписок можно запустить hello **Get AzureRmSubscription** командлета и скопируйте hello требуемого hello результирующий набор сведения о подписках.</span><span class="sxs-lookup"><span data-stu-id="f5e12-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="f5e12-118">После получения сведений о подписке, запустите следующий командлет tooset hello этой подписки по умолчанию hello, Здравствуйте целевой объект для создания и управления заданиями, а именно:</span><span class="sxs-lookup"><span data-stu-id="f5e12-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="f5e12-119">Hello [интегрированной среды Сценариев PowerShell](https://technet.microsoft.com/library/dd315244.aspx) рекомендуется для использования toodevelop и выполнения скриптов PowerShell для задания hello эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="f5e12-120">Объекты заданий обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="f5e12-121">Здравствуйте, следующие таблице приводится список всех типов hello объекта из **заданий эластичных баз данных** вместе с ее описание и соответствующие API-интерфейсов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5e12-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="f5e12-122">Тип объекта</span><span class="sxs-lookup"><span data-stu-id="f5e12-122">Object Type</span></span></th>
    <th><span data-ttu-id="f5e12-123">Описание</span><span class="sxs-lookup"><span data-stu-id="f5e12-123">Description</span></span></th>
    <th><span data-ttu-id="f5e12-124">Связанные API-интерфейсы PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5e12-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e12-125">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="f5e12-125">Credential</span></span></td>
    <td><span data-ttu-id="f5e12-126">Имя пользователя и пароль toouse при подключении toodatabases для выполнения сценариев или приложений из файлов DACPAC.</span><span class="sxs-lookup"><span data-stu-id="f5e12-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="f5e12-127">Hello пароль шифруется перед отправкой tooand хранение в базе данных hello заданий эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="f5e12-128">Hello пароль будет расшифрован при hello службы заданий эластичных баз данных по третьему hello создан и загружен с hello сценария установки.</span><span class="sxs-lookup"><span data-stu-id="f5e12-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="f5e12-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="f5e12-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="f5e12-130">New-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="f5e12-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="f5e12-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="f5e12-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="f5e12-132">Скрипт</span><span class="sxs-lookup"><span data-stu-id="f5e12-132">Script</span></span></td>
    <td><span data-ttu-id="f5e12-133">Toobe сценарий Transact-SQL, используемая для выполнения в нескольких базах данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="f5e12-134">Hello скрипт должен быть идемпотентными созданные toobe, так как hello служба будет повторять выполнение скрипта hello после сбоев.</span><span class="sxs-lookup"><span data-stu-id="f5e12-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="f5e12-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="f5e12-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="f5e12-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="f5e12-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="f5e12-137">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="f5e12-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="f5e12-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="f5e12-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="f5e12-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="f5e12-139">DACPAC</span></span></td>
    <td><span data-ttu-id="f5e12-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Приложения уровня данных </a> пакета toobe применяется в нескольких базах данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="f5e12-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="f5e12-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="f5e12-142">New-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="f5e12-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="f5e12-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="f5e12-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e12-144">Целевая база данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-144">Database Target</span></span></td>
    <td><span data-ttu-id="f5e12-145">Базы данных и сервера имя указывающего tooan базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f5e12-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="f5e12-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f5e12-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="f5e12-147">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f5e12-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e12-148">Целевая карта сегментов</span><span class="sxs-lookup"><span data-stu-id="f5e12-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="f5e12-149">Сочетание целевой базы данных и toobe учетных данных используется toodetermine информации, сохраняемой в карте сегментов эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="f5e12-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f5e12-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="f5e12-151">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f5e12-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="f5e12-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f5e12-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="f5e12-153">Целевая пользовательская коллекция</span><span class="sxs-lookup"><span data-stu-id="f5e12-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="f5e12-154">Заданная группа toocollectively баз данных используется для выполнения.</span><span class="sxs-lookup"><span data-stu-id="f5e12-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="f5e12-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f5e12-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="f5e12-156">New-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="f5e12-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="f5e12-157">Целевая дочерняя пользовательская коллекция</span><span class="sxs-lookup"><span data-stu-id="f5e12-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="f5e12-158">Целевая база данных, на которую ссылается пользовательская коллекция.</span><span class="sxs-lookup"><span data-stu-id="f5e12-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="f5e12-159">Add-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="f5e12-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="f5e12-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="f5e12-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="f5e12-161">Задание</span><span class="sxs-lookup"><span data-stu-id="f5e12-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="f5e12-162">Определение параметров для задания, которое может быть выполнения используется tootrigger или toofulfill расписание.</span><span class="sxs-lookup"><span data-stu-id="f5e12-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f5e12-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="f5e12-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="f5e12-164">New-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="f5e12-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="f5e12-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="f5e12-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="f5e12-166">Выполнение заданий</span><span class="sxs-lookup"><span data-stu-id="f5e12-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="f5e12-167">Контейнер toofulfill необходимые задачи, выполнение сценария или применения целевой tooa пакета DAC, используя учетные данные для подключения к базе данных с ошибками обрабатываются в соответствии tooan выполнения политики.</span><span class="sxs-lookup"><span data-stu-id="f5e12-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f5e12-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f5e12-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f5e12-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f5e12-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f5e12-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f5e12-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f5e12-171">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f5e12-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="f5e12-172">Выполнение задач</span><span class="sxs-lookup"><span data-stu-id="f5e12-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="f5e12-173">Одна единица работы toofulfill задания.</span><span class="sxs-lookup"><span data-stu-id="f5e12-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="f5e12-174">Если задание не может toosuccessfully выполнение, hello результирующее сообщение об исключении будут регистрироваться и нового сопоставления задание будет создавать и выполнять в соответствии toohello указан политику выполнения.</span><span class="sxs-lookup"><span data-stu-id="f5e12-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="f5e12-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f5e12-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f5e12-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f5e12-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f5e12-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f5e12-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="f5e12-178">Wait-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="f5e12-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="f5e12-179">Политика выполнения заданий</span><span class="sxs-lookup"><span data-stu-id="f5e12-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="f5e12-180">Управляет временем ожидания выполнения заданий, максимальными количествами повторных попыток и интервалами между ними.</span><span class="sxs-lookup"><span data-stu-id="f5e12-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="f5e12-181">Задания обработки эластичных баз данных включают стандартную политику выполнения, которая вызывает практически неограниченное число повторных попыток в случае сбоя задач с экспоненциально растущим интервалом между ними.</span><span class="sxs-lookup"><span data-stu-id="f5e12-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f5e12-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="f5e12-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="f5e12-183">New-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="f5e12-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="f5e12-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="f5e12-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="f5e12-185">Расписание</span><span class="sxs-lookup"><span data-stu-id="f5e12-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="f5e12-186">Время от спецификация месте tootake выполнения повторяющегося интервала или за один раз.</span><span class="sxs-lookup"><span data-stu-id="f5e12-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f5e12-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="f5e12-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="f5e12-188">New-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="f5e12-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="f5e12-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="f5e12-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="f5e12-190">Триггеры заданий</span><span class="sxs-lookup"><span data-stu-id="f5e12-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="f5e12-191">Сопоставление между задания и расписания toohello в соответствии с выполнением задания tootrigger расписания.</span><span class="sxs-lookup"><span data-stu-id="f5e12-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="f5e12-192">New-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="f5e12-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="f5e12-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="f5e12-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="f5e12-194">Поддерживаемые типы групп заданий обработки эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="f5e12-195">Задание Hello выполняет скрипты Transact-SQL (T-SQL) или приложение файлов DACPAC между несколькими базами данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="f5e12-196">Задание — отправленной toobe выполняется через группу баз данных, задание hello» расширяет «hello в дочерние задания, где каждое из которых выполняет hello запросить выполнение на одной базы данных в группе hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="f5e12-197">Вы можете создать группу одного из двух типов.</span><span class="sxs-lookup"><span data-stu-id="f5e12-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="f5e12-198">[Карта сегментов](sql-database-elastic-scale-shard-map-management.md) группы: когда задание отправленной tootarget карта сегментов, задание hello запрашивает toodetermine карты сегментов hello свой текущий набор сегментов, а затем создает дочерние задания для каждого сегмента в карте сегментов hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="f5e12-199">Группа «Пользовательская коллекция»: определяемый пользователем набор баз данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="f5e12-200">При задания предназначен для настраиваемой коллекции, он создает дочерние задания для каждой базы данных в настоящее время в пользовательской коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="f5e12-201">hello tooset подключения заданий эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="f5e12-202">Соединение должно toobe Настройка toohello заданий *базы данных системы управления* hello toousing предыдущего задания API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="f5e12-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="f5e12-203">Запустить этот командлет инициирует toopop окно учетных данных, копирование запроса hello имя пользователя и пароль, созданный при установке заданий эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="f5e12-204">Во всех примерах из этого раздела предполагается, что первый этап уже выполнен.</span><span class="sxs-lookup"><span data-stu-id="f5e12-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="f5e12-205">Откройте подключение toohello эластичной базы данных:</span><span class="sxs-lookup"><span data-stu-id="f5e12-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="f5e12-206">Зашифрованные учетные данные в рамках задания hello эластичной базы данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="f5e12-207">Учетные данные базы данных могут быть вставлены в заданий hello *базы данных системы управления* с ее пароль шифрования.</span><span class="sxs-lookup"><span data-stu-id="f5e12-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="f5e12-208">Это toostore необходимые учетные данные tooenable заданий toobe выполнен на более позднее время (с помощью расписания заданий).</span><span class="sxs-lookup"><span data-stu-id="f5e12-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="f5e12-209">Шифрование работает через сертификат, созданный как часть сценария установки hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="f5e12-210">Создает скрипт установки Hello и передачи сертификата hello в hello Azure облачной службы для расшифровки hello хранятся зашифрованные пароли.</span><span class="sxs-lookup"><span data-stu-id="f5e12-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="f5e12-211">Hello позже для облачной службы Azure сохраняет hello открытый ключ в рамках задания hello *базы данных системы управления* без необходимости hello сертификата, который позволяет hello PowerShell API или классический портал Azure интерфейс tooencrypt указанного пароля toobe на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f5e12-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="f5e12-212">пароли учетных данных Hello зашифровано и от пользователей с объектами заданий базы данных tooElastic доступ только для чтения.</span><span class="sxs-lookup"><span data-stu-id="f5e12-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="f5e12-213">Однако существует возможность пользователю-злоумышленнику с tooextract объектов пароль для доступа на чтение запись tooElastic заданий базы данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="f5e12-214">Учетные данные, разработанной toobe повторно между выполнениями задания.</span><span class="sxs-lookup"><span data-stu-id="f5e12-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="f5e12-215">Учетные данные передаются tootarget баз данных при выполнении подключения.</span><span class="sxs-lookup"><span data-stu-id="f5e12-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="f5e12-216">В настоящее время нет никаких ограничений на целевые hello базы данных, используемый для каждой учетной записи, злонамеренный пользователь может добавить целевой объект базы данных для базы данных в группе управления hello злонамеренный пользователь.</span><span class="sxs-lookup"><span data-stu-id="f5e12-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="f5e12-217">Hello пользователь впоследствии удалось запустить задания, предназначенные для этой базы данных toogain hello учетных данных пароля.</span><span class="sxs-lookup"><span data-stu-id="f5e12-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="f5e12-218">При работе с заданиями обработки эластичных баз данных мы рекомендуем использовать такие меры безопасности.</span><span class="sxs-lookup"><span data-stu-id="f5e12-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="f5e12-219">Ограничить использование hello API-интерфейсы tootrusted лиц.</span><span class="sxs-lookup"><span data-stu-id="f5e12-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="f5e12-220">Учетные данные должны иметь hello наименьших привилегий необходимые tooperform hello рабочее задание.</span><span class="sxs-lookup"><span data-stu-id="f5e12-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="f5e12-221">Дополнительные сведения см. на сайте MSDN в статье [Проверка прав доступа и разрешений в SQL Server](https://msdn.microsoft.com/library/bb669084.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5e12-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="f5e12-222">toocreate зашифрованных учетных данных для выполнения заданий по базам данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="f5e12-223">toocreate новый шифрования учетных данных, hello [ **командлета Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) запрашивает имя пользователя и пароль, который может быть передан toohello [ **New AzureSqlJobCredential командлет**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="f5e12-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="f5e12-224">учетные данные tooupdate</span><span class="sxs-lookup"><span data-stu-id="f5e12-224">tooupdate credentials</span></span>
<span data-ttu-id="f5e12-225">При изменении паролей, использовать hello [ **командлета Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) и набор hello **CredentialName** параметра.</span><span class="sxs-lookup"><span data-stu-id="f5e12-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="f5e12-226">toodefine целевой карты сегментов эластичной базы данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="f5e12-227">tooexecute задания для всех баз данных в наборе сегментов (созданные с помощью [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md)), использовать в качестве целевой базы данных hello карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="f5e12-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="f5e12-228">Для этого примера требуются сегментированных приложений, созданных с помощью клиентской библиотеки hello эластичной базы данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="f5e12-229">См. статью [Приступая к работе с инструментами эластичных баз данных](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f5e12-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="f5e12-230">База данных диспетчера карты сегментов Hello должен быть задан как целевой базы данных и затем hello конкретных сегментов карты должен быть указан как целевой объект.</span><span class="sxs-lookup"><span data-stu-id="f5e12-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="f5e12-231">Создание сценария T-SQL для выполнения в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="f5e12-232">При создании скриптов T-SQL для выполнения, настоятельно рекомендуется toobuild их toobe [идемпотентными](https://en.wikipedia.org/wiki/Idempotence) и устойчивы к сбоям.</span><span class="sxs-lookup"><span data-stu-id="f5e12-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="f5e12-233">При каждом выполнении возникнет ошибка, независимо от классификации hello сбоя hello заданий эластичных баз данных будет повторять попытки выполнения сценария.</span><span class="sxs-lookup"><span data-stu-id="f5e12-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="f5e12-234">Используйте hello [ **командлет New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate и сохранить скрипт для выполнения и задайте hello **- ContentName** и **- CommandText**параметры.</span><span class="sxs-lookup"><span data-stu-id="f5e12-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

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

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="f5e12-235">Создание нового сценария из файла</span><span class="sxs-lookup"><span data-stu-id="f5e12-235">Create a new script from a file</span></span>
<span data-ttu-id="f5e12-236">Если hello скрипт T-SQL, определенные в файле, используйте этот скрипт hello tooimport:</span><span class="sxs-lookup"><span data-stu-id="f5e12-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="f5e12-237">скрипт tooupdate T-SQL для выполнения в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="f5e12-238">Этот сценарий обновляет PowerShell hello текст команды T-SQL для существующего скрипта.</span><span class="sxs-lookup"><span data-stu-id="f5e12-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="f5e12-239">Следующие переменные tooreflect hello hello набор требуемого набора toobe Определение сценария:</span><span class="sxs-lookup"><span data-stu-id="f5e12-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

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

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="f5e12-240">существующий скрипт определения hello tooan tooupdate</span><span class="sxs-lookup"><span data-stu-id="f5e12-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="f5e12-241">toocreate tooexecute задания скрипта по карте сегментов</span><span class="sxs-lookup"><span data-stu-id="f5e12-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="f5e12-242">Приведенный ниже сценарий PowerShell запускает задание, которое выполнит сценарий в каждом сегменте карты с динамическим масштабированием.</span><span class="sxs-lookup"><span data-stu-id="f5e12-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="f5e12-243">Следующие переменные tooreflect hello hello набор требуемого скрипта и целевой:</span><span class="sxs-lookup"><span data-stu-id="f5e12-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="f5e12-244">tooexecute задания</span><span class="sxs-lookup"><span data-stu-id="f5e12-244">tooexecute a job</span></span>
<span data-ttu-id="f5e12-245">Приведенный ниже сценарий PowerShell выполняет существующее задание.</span><span class="sxs-lookup"><span data-stu-id="f5e12-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="f5e12-246">Обновите следующие переменной tooreflect задания требуемого hello имя toohave выполнена hello:</span><span class="sxs-lookup"><span data-stu-id="f5e12-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="f5e12-247">состояние hello tooretrieve выполнения одного задания</span><span class="sxs-lookup"><span data-stu-id="f5e12-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="f5e12-248">Используйте hello [ **командлет Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) и набор hello **JobExecutionId** параметр tooview hello состояние выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="f5e12-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="f5e12-249">Используйте hello же **Get AzureSqlJobExecution** командлет с hello **IncludeChildren** параметр tooview hello состояние выполнения дочерние задания, а именно: hello определенное состояние при каждом выполнении задания для каждой База данных целевой заданием hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="f5e12-250">состояние hello tooview между несколькими выполнениями задания</span><span class="sxs-lookup"><span data-stu-id="f5e12-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="f5e12-251">Hello [ **командлет Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) имеет несколько необязательных параметров, которые можно использовать toodisplay выполнения нескольких заданий, фильтрации с помощью hello предоставленных параметров.</span><span class="sxs-lookup"><span data-stu-id="f5e12-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="f5e12-252">Hello ниже показаны некоторые из способов hello toouse Get AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="f5e12-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="f5e12-253">Получение сведений о выполнении всех активных заданий верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="f5e12-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="f5e12-254">Получение сведений о выполнении всех заданий верхнего уровня, включая неактивные задания:</span><span class="sxs-lookup"><span data-stu-id="f5e12-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="f5e12-255">Получение состояния выполнения всех дочерних заданий, включая неактивные, по указанному идентификатору выполнения задания:</span><span class="sxs-lookup"><span data-stu-id="f5e12-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="f5e12-256">Получение состояния выполнения всех заданий, созданных с помощью сочетания расписания и задания, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="f5e12-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="f5e12-257">Получение сведения обо всех заданиях в указанной карте сегментов, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="f5e12-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="f5e12-258">Получение сведения обо всех заданиях в указанном пользовательском семействе, включая неактивные:</span><span class="sxs-lookup"><span data-stu-id="f5e12-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="f5e12-259">Получаете список hello завершений задач во время выполнения конкретного задания:</span><span class="sxs-lookup"><span data-stu-id="f5e12-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="f5e12-260">Получение сведений о выполнении задачи:</span><span class="sxs-lookup"><span data-stu-id="f5e12-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="f5e12-261">Следующий сценарий PowerShell Hello может быть сведения hello используется tooview выполнения задачи задания, что особенно полезно при отладке ошибок выполнения.</span><span class="sxs-lookup"><span data-stu-id="f5e12-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="f5e12-262">tooretrieve сбоев в рамках выполнения задачи задания</span><span class="sxs-lookup"><span data-stu-id="f5e12-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="f5e12-263">Hello **JobTaskExecution объекта** включает свойство для hello жизненного цикла задачи hello вместе со свойством сообщения.</span><span class="sxs-lookup"><span data-stu-id="f5e12-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="f5e12-264">Если произошел сбой выполнения задания задачи: hello жизненного цикла будет установлено слишком*сбой* и будет установлено свойство сообщение hello toohello результирующее сообщение об исключении и его стека.</span><span class="sxs-lookup"><span data-stu-id="f5e12-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="f5e12-265">Если задание завершилось неудачей, это tooview важные сведения hello задания задач, которые не были успешно выполнены для данного задания.</span><span class="sxs-lookup"><span data-stu-id="f5e12-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="f5e12-266">toowait для выполнения задания toocomplete</span><span class="sxs-lookup"><span data-stu-id="f5e12-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="f5e12-267">Следующий сценарий PowerShell Hello может быть toowait используется для задания задач toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f5e12-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="f5e12-268">Создание пользовательской политики выполнения</span><span class="sxs-lookup"><span data-stu-id="f5e12-268">Create a custom execution policy</span></span>
<span data-ttu-id="f5e12-269">Задания обработки эластичных баз данных поддерживают создание пользовательских политик выполнения, которые можно применять при запуске заданий.</span><span class="sxs-lookup"><span data-stu-id="f5e12-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="f5e12-270">В настоящий момент политики выполнения позволяют задать следующее:</span><span class="sxs-lookup"><span data-stu-id="f5e12-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="f5e12-271">Имя: Идентификатор для политики выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="f5e12-272">Время ожидания задания: общее время до отмены задания службой заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="f5e12-273">Начальный интервал повторных попыток: Toowait интервал перед первой повторной попытки.</span><span class="sxs-lookup"><span data-stu-id="f5e12-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="f5e12-274">Максимальный интервал повторных попыток: Лимит в размере toouse интервалы повтора.</span><span class="sxs-lookup"><span data-stu-id="f5e12-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="f5e12-275">Коэффициент отсрочки интервал повторных попыток: Коэффициент используется toocalculate hello следующий интервал между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="f5e12-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="f5e12-276">Hello используется следующая формула: (начальной интервал повтора) * Math.pow ((интервал отсрочки коэффициент) (число повторов) - 2).</span><span class="sxs-lookup"><span data-stu-id="f5e12-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="f5e12-277">Максимальное попыток: hello максимальное число tooperform попыток повтора в задании.</span><span class="sxs-lookup"><span data-stu-id="f5e12-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="f5e12-278">политика выполнения по умолчанию Hello использует hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="f5e12-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="f5e12-279">Имя: политика выполнения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="f5e12-279">Name: Default execution policy</span></span>
* <span data-ttu-id="f5e12-280">Время ожидания задания: 1 неделя</span><span class="sxs-lookup"><span data-stu-id="f5e12-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="f5e12-281">Исходный интервал повторных попыток: 100 миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="f5e12-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="f5e12-282">Максимальный интервал повторных попыток: 30 минут</span><span class="sxs-lookup"><span data-stu-id="f5e12-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="f5e12-283">Коэффициент интервала повторных попыток: 2</span><span class="sxs-lookup"><span data-stu-id="f5e12-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="f5e12-284">Максимальное число попыток: 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="f5e12-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="f5e12-285">Создайте политику выполнения требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="f5e12-286">Изменение пользовательской политики выполнения</span><span class="sxs-lookup"><span data-stu-id="f5e12-286">Update a custom execution policy</span></span>
<span data-ttu-id="f5e12-287">Обновление hello требуемого tooupdate политики выполнения:</span><span class="sxs-lookup"><span data-stu-id="f5e12-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="f5e12-288">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="f5e12-288">Cancel a job</span></span>
<span data-ttu-id="f5e12-289">Задания обработки эластичных баз данных поддерживают запросы на отмену заданий.</span><span class="sxs-lookup"><span data-stu-id="f5e12-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="f5e12-290">Если заданий эластичных баз данных обнаруживает запрос отмены задания, выполняемые, он попытается toostop hello задания.</span><span class="sxs-lookup"><span data-stu-id="f5e12-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="f5e12-291">Служба заданий обработки эластичных баз данных может выполнить отмену двумя разными способами:</span><span class="sxs-lookup"><span data-stu-id="f5e12-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="f5e12-292">Отмена задачи в данный момент: Если Отмена обнаруживается во время задачи, будет предпринята попытка отмены в hello аспектом задачу hello в данный момент.</span><span class="sxs-lookup"><span data-stu-id="f5e12-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="f5e12-293">Например: в случае долго выполняющийся запрос, выполняемый в настоящее время при попытке отмены будет попытка toocancel hello запроса.</span><span class="sxs-lookup"><span data-stu-id="f5e12-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="f5e12-294">Отмена попытки выполнения задачи: отмены в случае обнаружения потоком управления hello перед запуском задачи для выполнения потока управления hello избежать запуска задачи hello и объявить hello запрос отменен.</span><span class="sxs-lookup"><span data-stu-id="f5e12-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="f5e12-295">При поступлении запроса отмены задания для задания родительского запроса отмены hello будет обрабатываться родительским заданием hello и всех его дочерние задания.</span><span class="sxs-lookup"><span data-stu-id="f5e12-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="f5e12-296">запрос отмены toosubmit использовать hello [ **командлет Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) и набор hello **JobExecutionId** параметра.</span><span class="sxs-lookup"><span data-stu-id="f5e12-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="f5e12-297">toodelete задания и журнал заданий асинхронно</span><span class="sxs-lookup"><span data-stu-id="f5e12-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="f5e12-298">Задания обработки эластичных баз данных поддерживают асинхронное удаление заданий.</span><span class="sxs-lookup"><span data-stu-id="f5e12-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="f5e12-299">Задания могут быть помечены для удаления и hello система удаляет задание hello и ее журнал заданий после завершения выполнения всех заданий для задания hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="f5e12-300">Hello системы не будет автоматически отменить выполнение активных заданий.</span><span class="sxs-lookup"><span data-stu-id="f5e12-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="f5e12-301">Вызвать [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel выполнение активных заданий.</span><span class="sxs-lookup"><span data-stu-id="f5e12-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="f5e12-302">Удаление задания tootrigger, используйте hello [ **командлет Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) и набор hello **JobName** параметра.</span><span class="sxs-lookup"><span data-stu-id="f5e12-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="f5e12-303">toocreate целевой объект пользовательские базы данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-303">toocreate a custom database target</span></span>
<span data-ttu-id="f5e12-304">Вы можете определять целевые объекты пользовательской базы данных для выполнения напрямую или для включения в группу пользовательских баз данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="f5e12-305">Например так как **эластичные пулы** , еще не поддерживается напрямую с помощью API-интерфейсов PowerShell, можно создать пользовательские базы данных целевой объект и целевой объект коллекции пользовательские базы данных, который включает все базы данных hello в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="f5e12-306">Задайте следующие переменные tooreflect hello требуемого базы данных сведения hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="f5e12-307">toocreate целевой объект коллекции пользовательские базы данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="f5e12-308">Используйте hello [ **New AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine командлет выполнение пользовательской базе данных коллекции целевых объектов tooenable несколько целевых объектов базы данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="f5e12-309">После создания группы базы данных можно связать с hello пользовательской коллекции целевой базы данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="f5e12-310">Следующие переменные tooreflect hello hello набор требуемого пользовательской коллекции целевую конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="f5e12-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="f5e12-311">целевой объект коллекции tooadd баз данных tooa пользовательские базы данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="f5e12-312">использовать tooadd базы данных tooa определенной пользовательской коллекции hello [ **добавить AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) командлета.</span><span class="sxs-lookup"><span data-stu-id="f5e12-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="f5e12-313">Просмотрите hello баз данных в пользовательской базе данных целевого объекта коллекции</span><span class="sxs-lookup"><span data-stu-id="f5e12-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="f5e12-314">Используйте hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) командлет tooretrieve hello дочерних баз данных в пользовательской базе данных целевого объекта коллекции.</span><span class="sxs-lookup"><span data-stu-id="f5e12-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="f5e12-315">Создать сценарий tooexecute задания для целевого объекта коллекции пользовательские базы данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="f5e12-316">Используйте hello [ **New AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate командлет задания для группы баз данных, определенных в пользовательской базе данных целевого объекта коллекции.</span><span class="sxs-lookup"><span data-stu-id="f5e12-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="f5e12-317">Заданий эластичных баз данных будет расширяться hello задания на несколько дочерних каждой соответствующей tooa базы данных, связанная с целевой объект коллекции hello пользовательские базы данных и убедитесь, что hello сценарий выполняется для каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="f5e12-318">Опять же очень важно, скрипты являются устойчивыми tooretries toobe идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="f5e12-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="f5e12-319">Сбор данных из нескольких баз данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-319">Data collection across databases</span></span>
<span data-ttu-id="f5e12-320">Можно использовать задание tooexecute запрос между несколькими базами данных и отправки hello результаты tooa конкретной таблицы.</span><span class="sxs-lookup"><span data-stu-id="f5e12-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="f5e12-321">можно запрашивать таблицы Hello после toosee hello hello фактов запроса результаты из каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="f5e12-322">Это предоставляет асинхронный метод tooexecute запрос через несколько баз данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="f5e12-323">После неудачной попытки автоматически выполняется повторная попытка.</span><span class="sxs-lookup"><span data-stu-id="f5e12-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="f5e12-324">Hello указанной целевой таблицы будут создаваться автоматически, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="f5e12-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="f5e12-325">Новая таблица Hello соответствует hello схему hello вернул результирующий набор.</span><span class="sxs-lookup"><span data-stu-id="f5e12-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="f5e12-326">Если сценарий возвращает несколько результирующих наборов, эластичной базы данных заданий будет отправлять hello первый toohello целевой таблицы.</span><span class="sxs-lookup"><span data-stu-id="f5e12-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="f5e12-327">Hello следующий скрипт PowerShell выполняет скрипт и объединяет результаты в указанной таблице.</span><span class="sxs-lookup"><span data-stu-id="f5e12-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="f5e12-328">В этом сценарии предполагается, что у вас уже есть сценарий T-SQL, который возвращает один набор результатов, и целевой объект пользовательской коллекции баз данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="f5e12-329">Этот скрипт использует hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) командлета.</span><span class="sxs-lookup"><span data-stu-id="f5e12-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="f5e12-330">Задайте параметры hello для сценария, учетные данные и целевой выполнения:</span><span class="sxs-lookup"><span data-stu-id="f5e12-330">Set hello parameters for script, credentials, and execution target:</span></span>

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

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="f5e12-331">toocreate и запуск задания для сценарии сбора данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="f5e12-332">Этот скрипт использует hello [ **начала AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) командлета.</span><span class="sxs-lookup"><span data-stu-id="f5e12-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

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

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="f5e12-333">tooschedule выполнения триггера задания</span><span class="sxs-lookup"><span data-stu-id="f5e12-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="f5e12-334">Следующий сценарий PowerShell Hello может быть используется toocreate повторяющемуся расписанию.</span><span class="sxs-lookup"><span data-stu-id="f5e12-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="f5e12-335">В этом скрипте используется интервал в минутах, но командлет [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) также поддерживает параметры -DayInterval, -HourInterval, -MonthInterval и -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="f5e12-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="f5e12-336">Расписания, которые выполняются только один раз, можно создавать с помощью параметра -OneTime.</span><span class="sxs-lookup"><span data-stu-id="f5e12-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="f5e12-337">Создание нового расписания</span><span class="sxs-lookup"><span data-stu-id="f5e12-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="f5e12-338">tootrigger задание выполняется по расписанию</span><span class="sxs-lookup"><span data-stu-id="f5e12-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="f5e12-339">Триггер задания может быть определенный toohave соответствующим tooa расписание задания времени.</span><span class="sxs-lookup"><span data-stu-id="f5e12-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="f5e12-340">Hello следующий сценарий PowerShell можно использовать toocreate триггер задания.</span><span class="sxs-lookup"><span data-stu-id="f5e12-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="f5e12-341">Используйте [New AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) и набор hello следующие переменные toocorrespond toohello нужного задания и расписания:</span><span class="sxs-lookup"><span data-stu-id="f5e12-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="f5e12-342">tooremove toostop ассоциации запланированного задания из выполнения по расписанию</span><span class="sxs-lookup"><span data-stu-id="f5e12-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="f5e12-343">toodiscontinue повторения задания операционной системы с помощью триггера задания hello триггера задания могут быть удалены.</span><span class="sxs-lookup"><span data-stu-id="f5e12-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="f5e12-344">Удалить задание триггера toostop задания из выполняемой соответствующим tooa расписание, с помощью hello [ **командлет Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="f5e12-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="f5e12-345">Получить расписание время привязанного tooa триггеров задания</span><span class="sxs-lookup"><span data-stu-id="f5e12-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="f5e12-346">Следующий сценарий PowerShell Hello можно использовать tooobtain и отображения расписания определенный момент времени зарегистрированных tooa триггеры задания hello.</span><span class="sxs-lookup"><span data-stu-id="f5e12-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="f5e12-347">триггеры задания tooretrieve привязан tooa задания</span><span class="sxs-lookup"><span data-stu-id="f5e12-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="f5e12-348">Используйте [Get AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain и отображения расписания, содержащая зарегистрированные задания.</span><span class="sxs-lookup"><span data-stu-id="f5e12-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="f5e12-349">toocreate приложения уровня данных (DACPAC) для выполнения в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="f5e12-350">toocreate пакета DAC, в разделе [приложений уровня данных](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5e12-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="f5e12-351">toodeploy пакета DAC, используйте hello [командлет New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="f5e12-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="f5e12-352">Hello DACPAC должен быть доступен toohello службой.</span><span class="sxs-lookup"><span data-stu-id="f5e12-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="f5e12-353">Это рекомендуется tooupload созданный tooAzure DACPAC хранилища и создать [подписи общего доступа](../storage/common/storage-dotnet-shared-access-signature-part-1.md) для hello DACPAC.</span><span class="sxs-lookup"><span data-stu-id="f5e12-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="f5e12-354">tooupdate приложения уровня данных (DACPAC) для выполнения в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="f5e12-355">Существующие пакеты DACPAC, зарегистрированные в заданий эластичных баз данных может быть обновленные toopoint toonew идентификаторы URI.</span><span class="sxs-lookup"><span data-stu-id="f5e12-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="f5e12-356">Используйте hello [ **командлета Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello URI пакета DAC на существующем зарегистрированные DACPAC:</span><span class="sxs-lookup"><span data-stu-id="f5e12-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="f5e12-357">toocreate задание tooapply приложения уровня данных (DACPAC) в нескольких базах данных</span><span class="sxs-lookup"><span data-stu-id="f5e12-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="f5e12-358">После создания пакета DAC в заданий эластичных баз данных задания могут создаваться tooapply hello DACPAC между несколькими базами данных.</span><span class="sxs-lookup"><span data-stu-id="f5e12-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="f5e12-359">Следующий сценарий PowerShell Hello может быть используется toocreate задания DACPAC через пользовательский набор баз данных:</span><span class="sxs-lookup"><span data-stu-id="f5e12-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

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
