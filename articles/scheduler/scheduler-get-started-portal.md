---
title: "aaaGet к работе с планировщиком Azure на портале Azure | Документы Microsoft"
description: "Начало работы с планировщиком Azure на портале Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="19777-103">Начало работы с планировщиком Azure на портале Azure</span><span class="sxs-lookup"><span data-stu-id="19777-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="19777-104">Это легко toocreate запланированные задания в планировщике Azure.</span><span class="sxs-lookup"><span data-stu-id="19777-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="19777-105">В этом учебнике вы узнаете, как toocreate задания.</span><span class="sxs-lookup"><span data-stu-id="19777-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="19777-106">Также вы изучите возможности мониторинга и управления в планировщике.</span><span class="sxs-lookup"><span data-stu-id="19777-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="19777-107">Создание задания</span><span class="sxs-lookup"><span data-stu-id="19777-107">Create a job</span></span>
1. <span data-ttu-id="19777-108">Войдите в слишком[портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="19777-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="19777-109">Нажмите кнопку **+ создать** > тип *планировщика* в поле поиска hello > выберите **планировщика** в результатах > щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="19777-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="19777-110">Создадим задание, которое будет только открывать сайт http://www.microsoft.com/ с помощью запроса GET.</span><span class="sxs-lookup"><span data-stu-id="19777-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="19777-111">В hello **задания планировщика** экране, введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="19777-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="19777-112">**Имя:** `getmicrosoft`.</span><span class="sxs-lookup"><span data-stu-id="19777-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="19777-113">**Подписка:** ваша подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="19777-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="19777-114">**Коллекция заданий:** выберите существующую коллекцию заданий или щелкните **Создать** и введите имя.</span><span class="sxs-lookup"><span data-stu-id="19777-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="19777-115">Затем в **Настройка действия**, определить hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="19777-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="19777-116">**Тип действия:** ` HTTP`.</span><span class="sxs-lookup"><span data-stu-id="19777-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="19777-117">**Метод:** `GET`.</span><span class="sxs-lookup"><span data-stu-id="19777-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="19777-118">**URL-адрес:** ` http://www.microsoft.com`.</span><span class="sxs-lookup"><span data-stu-id="19777-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="19777-119">И, наконец, определим расписание.</span><span class="sxs-lookup"><span data-stu-id="19777-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="19777-120">Hello задание может быть задан как одноразовым, но выберем расписание повторений:</span><span class="sxs-lookup"><span data-stu-id="19777-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="19777-121">**Периодичность:** `Recurring`.</span><span class="sxs-lookup"><span data-stu-id="19777-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="19777-122">**Начало**: текущая дата.</span><span class="sxs-lookup"><span data-stu-id="19777-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="19777-123">**Повторять каждые:** `12 Hours`.</span><span class="sxs-lookup"><span data-stu-id="19777-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="19777-124">**Окончание**: через два дня после текущей даты.</span><span class="sxs-lookup"><span data-stu-id="19777-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="19777-125">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="19777-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="19777-126">Контроль и мониторинг заданий</span><span class="sxs-lookup"><span data-stu-id="19777-126">Manage and monitor jobs</span></span>
<span data-ttu-id="19777-127">После создания задания, он отображается в панели мониторинга Azure основной hello.</span><span class="sxs-lookup"><span data-stu-id="19777-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="19777-128">Щелкните задание hello и новый откроется окно hello следующие вкладки:</span><span class="sxs-lookup"><span data-stu-id="19777-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="19777-129">Свойства</span><span class="sxs-lookup"><span data-stu-id="19777-129">Properties</span></span>  
2. <span data-ttu-id="19777-130">Параметры действия</span><span class="sxs-lookup"><span data-stu-id="19777-130">Action Settings</span></span>  
3. <span data-ttu-id="19777-131">Расписание</span><span class="sxs-lookup"><span data-stu-id="19777-131">Schedule</span></span>  
4. <span data-ttu-id="19777-132">Журнал</span><span class="sxs-lookup"><span data-stu-id="19777-132">History</span></span>
5. <span data-ttu-id="19777-133">Пользователи</span><span class="sxs-lookup"><span data-stu-id="19777-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="19777-134">Свойства</span><span class="sxs-lookup"><span data-stu-id="19777-134">Properties</span></span>
<span data-ttu-id="19777-135">Эти свойства только для чтения описывать метаданные управления hello hello планировщика заданий.</span><span class="sxs-lookup"><span data-stu-id="19777-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="19777-136">Параметры действия</span><span class="sxs-lookup"><span data-stu-id="19777-136">Action settings</span></span>
<span data-ttu-id="19777-137">Щелкните задание в hello **заданий** экрана позволяет tooconfigure заданию.</span><span class="sxs-lookup"><span data-stu-id="19777-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="19777-138">Это позволяет настроить дополнительные параметры, если не настроить их в hello быстрого создания мастера.</span><span class="sxs-lookup"><span data-stu-id="19777-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="19777-139">Для всех типов действий и можно изменить политику повтора hello hello действие при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="19777-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="19777-140">Для действия задания типов HTTP и HTTPS можно изменить tooany метод hello допускается HTTP-команду.</span><span class="sxs-lookup"><span data-stu-id="19777-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="19777-141">Можно также добавлять, удалить или изменить заголовки hello и обычной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="19777-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="19777-142">Для действий очередей хранения можно изменить учетную запись хранения hello, имя очереди, маркер SAS и текст.</span><span class="sxs-lookup"><span data-stu-id="19777-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="19777-143">Для типов действий шины службы можно изменить hello пространства имен, путь раздела или очереди, параметры проверки подлинности, тип транспорта, свойства сообщения и тело сообщения.</span><span class="sxs-lookup"><span data-stu-id="19777-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="19777-144">Расписание</span><span class="sxs-lookup"><span data-stu-id="19777-144">Schedule</span></span>
<span data-ttu-id="19777-145">Это позволяет повторно настроить расписание hello, при желании toochange hello расписания, созданные в hello мастере быстрого создания.</span><span class="sxs-lookup"><span data-stu-id="19777-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="19777-146">Это возможность toobuild [сложных расписаний и расширенные повторения в задание](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="19777-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="19777-147">Можно изменить hello даты начала и времени, расписание повторений hello конечная дата и время (если hello задание является повторяющимся).</span><span class="sxs-lookup"><span data-stu-id="19777-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="19777-148">Журнал</span><span class="sxs-lookup"><span data-stu-id="19777-148">History</span></span>
<span data-ttu-id="19777-149">Hello **журнал** вкладке отображаются выбранные показатели для каждого выполнения задания в системе hello для выбранного задания hello.</span><span class="sxs-lookup"><span data-stu-id="19777-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="19777-150">Эти показатели предоставляют значения в реальном времени hello работоспособностью планировщика:</span><span class="sxs-lookup"><span data-stu-id="19777-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="19777-151">Состояние</span><span class="sxs-lookup"><span data-stu-id="19777-151">Status</span></span>  
2. <span data-ttu-id="19777-152">Сведения</span><span class="sxs-lookup"><span data-stu-id="19777-152">Details</span></span>  
3. <span data-ttu-id="19777-153">Количество повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="19777-153">Retry attempts</span></span>
4. <span data-ttu-id="19777-154">Периодичность: 1, 2, 3 и т. д.</span><span class="sxs-lookup"><span data-stu-id="19777-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="19777-155">Время начала выполнения.</span><span class="sxs-lookup"><span data-stu-id="19777-155">Start time of execution</span></span>  
6. <span data-ttu-id="19777-156">Время окончания выполнения.</span><span class="sxs-lookup"><span data-stu-id="19777-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="19777-157">Можно щелкнуть выполнения tooview его **сведения истории**, включая hello весь ответ для каждого выполнения.</span><span class="sxs-lookup"><span data-stu-id="19777-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="19777-158">Это диалоговое окно предназначено также позволяет toocopy hello ответа toohello, буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="19777-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="19777-159">Пользователи</span><span class="sxs-lookup"><span data-stu-id="19777-159">Users</span></span>
<span data-ttu-id="19777-160">Управление доступом на основе ролей (RBAC) Azure обеспечивает точное управление доступом для планировщика Azure.</span><span class="sxs-lookup"><span data-stu-id="19777-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="19777-161">как hello toouse вкладку "пользователи" может ссылаться слишком toolearn[контроля доступа](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="19777-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="19777-162">См. также</span><span class="sxs-lookup"><span data-stu-id="19777-162">See also</span></span>
 [<span data-ttu-id="19777-163">Что такое планировщик?</span><span class="sxs-lookup"><span data-stu-id="19777-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="19777-164">Основные понятия, терминология и иерархия сущностей планировщика</span><span class="sxs-lookup"><span data-stu-id="19777-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="19777-165">Планы и выставление счетов в планировщике Azure</span><span class="sxs-lookup"><span data-stu-id="19777-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="19777-166">Как планирует комплексного toobuild и дополнительно повторения с планировщиком Azure</span><span class="sxs-lookup"><span data-stu-id="19777-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="19777-167">Справочник по REST API планировщика</span><span class="sxs-lookup"><span data-stu-id="19777-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="19777-168">Справочник по командлетам PowerShell планировщика</span><span class="sxs-lookup"><span data-stu-id="19777-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="19777-169">Высокая доступность и надежность планировщика</span><span class="sxs-lookup"><span data-stu-id="19777-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="19777-170">Ограничения и значения по умолчанию планировщика</span><span class="sxs-lookup"><span data-stu-id="19777-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="19777-171">Исходящая аутентификация планировщика</span><span class="sxs-lookup"><span data-stu-id="19777-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
