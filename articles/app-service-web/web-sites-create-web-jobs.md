---
title: "aaaRun фоновых задач с веб-заданий"
description: "Узнайте, как toorun фоновые задачи в Azure веб-приложений."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="51872-103">Выполнение фоновых задач с веб-заданиями</span><span class="sxs-lookup"><span data-stu-id="51872-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="51872-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="51872-104">Overview</span></span>
<span data-ttu-id="51872-105">Программы или сценарии можно выполнять в веб-заданиях в веб-приложении [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) тремя способами: по запросу, непрерывно или по расписанию.</span><span class="sxs-lookup"><span data-stu-id="51872-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="51872-106">Нет без дополнительных затрат toouse веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="51872-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="51872-107">В этой статье показано, как hello toodeploy веб-заданий с помощью [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="51872-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="51872-108">Сведения о том, как toodeploy с помощью Visual Studio или процесс непрерывной поставки, в разделе [как веб-заданий Azure tooDeploy tooWeb приложения](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="51872-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="51872-109">Hello Azure SDK веб-заданий упрощает многие задачи программирования веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="51872-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="51872-110">Дополнительные сведения см. в разделе [возможности hello SDK веб-задания](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="51872-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="51872-111">Функции Azure предоставляет другим способом toorun программ и сценариев, в данной среде или из приложения службы приложений.</span><span class="sxs-lookup"><span data-stu-id="51872-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="51872-112">Дополнительные сведения см. в статье [Обзор функций Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51872-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="51872-113"><a name="acceptablefiles"></a>Допустимые типы файлов для скриптов и программ</span><span class="sxs-lookup"><span data-stu-id="51872-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="51872-114">Допустимы следующие типы файлов Hello:</span><span class="sxs-lookup"><span data-stu-id="51872-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="51872-115">.cmd, .bat, .exe (с использованием командной строки windows)</span><span class="sxs-lookup"><span data-stu-id="51872-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="51872-116">.ps1 (с использованием powershell)</span><span class="sxs-lookup"><span data-stu-id="51872-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="51872-117">.sh (с использованием bash)</span><span class="sxs-lookup"><span data-stu-id="51872-117">.sh (using bash)</span></span>
* <span data-ttu-id="51872-118">.PHP (с использованием php)</span><span class="sxs-lookup"><span data-stu-id="51872-118">.php (using php)</span></span>
* <span data-ttu-id="51872-119">.py (с использованием python)</span><span class="sxs-lookup"><span data-stu-id="51872-119">.py (using python)</span></span>
* <span data-ttu-id="51872-120">.js (с использованием node)</span><span class="sxs-lookup"><span data-stu-id="51872-120">.js (using node)</span></span>
* <span data-ttu-id="51872-121">.jar (с использованием java)</span><span class="sxs-lookup"><span data-stu-id="51872-121">.jar (using java)</span></span>

## <span data-ttu-id="51872-122"><a name="CreateOnDemand"></a>Создание веб-задания по запросу на портале hello</span><span class="sxs-lookup"><span data-stu-id="51872-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="51872-123">В hello **веб-приложения** колонке hello [портала Azure](https://portal.azure.com), нажмите кнопку **все параметры > веб-заданий** tooshow hello **веб-заданий** колонку.</span><span class="sxs-lookup"><span data-stu-id="51872-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![Колонка "Веб-задания"](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="51872-125">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="51872-125">Click **Add**.</span></span> <span data-ttu-id="51872-126">Hello **добавить веб-задание** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="51872-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![Колонка "Добавление веб-задания"](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="51872-128">В разделе **имя**, введите имя для hello веб-задания.</span><span class="sxs-lookup"><span data-stu-id="51872-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="51872-129">Hello имя должно начинаться с буквы или цифры и не может содержать специальные символы, отличные от «-» и «_».</span><span class="sxs-lookup"><span data-stu-id="51872-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="51872-130">В hello **как tooRun** выберите **выполнять по требованию**.</span><span class="sxs-lookup"><span data-stu-id="51872-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="51872-131">В hello **отправки файлов** щелкните значок папки hello и обзор toohello ZIP-файла, содержащего сценарий.</span><span class="sxs-lookup"><span data-stu-id="51872-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="51872-132">Hello ZIP-файл должен содержать исполняемый файл (.exe .cmd .bat .sh .php .py .js) и все вспомогательные файлы, необходимые toorun hello программы или сценария.</span><span class="sxs-lookup"><span data-stu-id="51872-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="51872-133">Проверьте **создать** tooupload hello сценария tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="51872-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="51872-134">Hello имя, указанное для hello веб-задания отображается в списке hello на hello **веб-заданий** колонку.</span><span class="sxs-lookup"><span data-stu-id="51872-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="51872-135">hello toorun веб-задание, щелкните правой кнопкой мыши его имя в списке hello и нажать кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="51872-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![Запуск веб-задания](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="51872-137"><a name="CreateContinuous"></a>Создание непрерывно выполняющегося веб-задания</span><span class="sxs-lookup"><span data-stu-id="51872-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="51872-138">toocreate непрерывно выполняющегося веб-задания, выполните hello же шаги для создания веб-задание, выполняемое один раз, но в hello **как tooRun** выберите **Continuous**.</span><span class="sxs-lookup"><span data-stu-id="51872-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="51872-139">toostart или остановить непрерывные веб-задание, щелкните правой кнопкой мыши hello веб-задание в списке hello и нажмите кнопку **запустить** или **остановить**.</span><span class="sxs-lookup"><span data-stu-id="51872-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="51872-140">Если веб-приложение работает на нескольких экземплярах, непрерывно выполняемое веб-задание будет работать на всех экземплярах.</span><span class="sxs-lookup"><span data-stu-id="51872-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="51872-141">Веб-задания по требованию и запланированные задачи запускаются на отдельном экземпляре, выбранном Microsoft Azure для балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="51872-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="51872-142">Для непрерывных веб-заданий toorun надежно и на всех экземплярах включить hello Always On * параметр конфигурации для hello веб-приложения в противном случае они для остановки выполнения после бездействия слишком долго hello SCM хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="51872-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="51872-143"><a name="CreateScheduledCRON"></a>Создание запланированного веб-задания с использованием выражения CRON</span><span class="sxs-lookup"><span data-stu-id="51872-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="51872-144">Этот метод доступен tooWeb приложения, выполняющиеся в режиме Basic, Standard или Premium и требует hello **Always On** параметр toobe включена приложение hello.</span><span class="sxs-lookup"><span data-stu-id="51872-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="51872-145">просто включите tooturn по запросу веб-задания в запланированные веб-задания `settings.job` файла в корне hello ZIP-файл веб-задания.</span><span class="sxs-lookup"><span data-stu-id="51872-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="51872-146">JSON-файл должен содержать свойство `schedule` с [выражением CRON](https://en.wikipedia.org/wiki/Cron), как в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="51872-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="51872-147">Hello CRON-выражение состоит из полей 6: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span><span class="sxs-lookup"><span data-stu-id="51872-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="51872-148">Например, tootrigger веб-задание каждые 15 минут вашей `settings.job` будет иметь:</span><span class="sxs-lookup"><span data-stu-id="51872-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="51872-149">Другие примеры расписания для выражения CRON:</span><span class="sxs-lookup"><span data-stu-id="51872-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="51872-150">Каждый час (т. е. когда hello число минут — 0):`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="51872-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="51872-151">Каждый час из too5 9: 00 PM:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="51872-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="51872-152">Каждый день в 9:30: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="51872-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="51872-153">Каждый рабочий день в 9:30: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="51872-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="51872-154">**Примечание**: при развертывании веб-задания из Visual Studio, убедитесь, что toomark вашей `settings.job` свойства файла как «Копировать более позднюю версию».</span><span class="sxs-lookup"><span data-stu-id="51872-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="51872-155"><a name="CreateScheduled"></a>Создание запланированного веб-задания с помощью планировщика Azure hello</span><span class="sxs-lookup"><span data-stu-id="51872-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="51872-156">Здравствуйте, следуя альтернативный способ использует hello планировщика Azure.</span><span class="sxs-lookup"><span data-stu-id="51872-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="51872-157">В этом случае веб-задание осведомлено прямой hello расписания.</span><span class="sxs-lookup"><span data-stu-id="51872-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="51872-158">Вместо этого hello планировщика Azure возвращает настроенное tootrigger веб-задание по расписанию.</span><span class="sxs-lookup"><span data-stu-id="51872-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="51872-159">Hello портала Azure пока еще не имеет возможности toocreate hello запланированных веб-задания, но пока не будет добавлен этот компонент это можно сделать с помощью hello [классический портал](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="51872-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="51872-160">В hello [классический портал](http://manage.windowsazure.com) переход на страницу веб-задания toohello и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="51872-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="51872-161">В hello **как tooRun** выберите **по расписанию**.</span><span class="sxs-lookup"><span data-stu-id="51872-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![Новое запланированное задание][NewScheduledJob]
3. <span data-ttu-id="51872-163">Выберите hello **область планировщика** для задания и нажмите стрелку hello hello нижней правой части hello диалоговое окно tooproceed toohello следующий экран.</span><span class="sxs-lookup"><span data-stu-id="51872-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="51872-164">В hello **создать задание** диалоговое окно, выберите тип hello **повторения** требуется: **Однократное задание** или **повторяющееся задание**.</span><span class="sxs-lookup"><span data-stu-id="51872-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Запланированное повторение][SchdRecurrence]
5. <span data-ttu-id="51872-166">Кроме того, выберите время запуска в разделе **Запуск**: **Сейчас** или **В определенное время**.</span><span class="sxs-lookup"><span data-stu-id="51872-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Время начала по расписанию][SchdStart]
6. <span data-ttu-id="51872-168">Toostart в определенное время, выберите ваш начальные значения времени в группе **запуск на**.</span><span class="sxs-lookup"><span data-stu-id="51872-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Расписание запуска в определенное время][SchdStartOn]
7. <span data-ttu-id="51872-170">Если вы выбрали повторяющееся задание, у вас есть hello **Повторять каждые** параметр toospecify hello частоту повторения и hello **заканчивается на** параметр toospecify время окончания.</span><span class="sxs-lookup"><span data-stu-id="51872-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![Запланированное повторение][SchdRecurEvery]
8. <span data-ttu-id="51872-172">При выборе **недели**, можно выбрать hello **на определенное расписание** и укажите hello дни недели hello, который будет hello toorun задания.</span><span class="sxs-lookup"><span data-stu-id="51872-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![Расписание дни недели hello][SchdWeeksOnParticular]
9. <span data-ttu-id="51872-174">При выборе **месяцев** и выберите hello **на определенное расписание** поле, можно задать toorun hello задания на конкретный номерами **дней** в месяце hello.</span><span class="sxs-lookup"><span data-stu-id="51872-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![Запланировать определенных дат в месяце hello][SchdMonthsOnPartDays]
10. <span data-ttu-id="51872-176">При выборе **дни недели**, можно выбрать какой день или дни недели hello требуется hello toorun задания в месяц hello.</span><span class="sxs-lookup"><span data-stu-id="51872-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![Планирование определенных дней недели в месяце][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="51872-178">Наконец, можно также использовать hello **вхождений** toochoose параметр недель в месяце hello (первый, второй, третьего и т.д.) требуется hello toorun задания на hello дней недели.</span><span class="sxs-lookup"><span data-stu-id="51872-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![Планирование определенных дней недели в определенные недели месяца][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="51872-180">После создания одного или нескольких заданий их имена будут отображаться на вкладке hello веб-заданий с их состояние, тип расписания и другие сведения.</span><span class="sxs-lookup"><span data-stu-id="51872-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="51872-181">Данные предыстории для hello последние 30 веб-заданий сохраняется.</span><span class="sxs-lookup"><span data-stu-id="51872-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![Список заданий][WebJobsListWithSeveralJobs]

### <span data-ttu-id="51872-183"><a name="Scheduler"></a>Запланированные задания и планировщик Azure</span><span class="sxs-lookup"><span data-stu-id="51872-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="51872-184">Запланированные задания можно в дальнейшем можно настроить на страницах планировщика Azure hello hello [классический портал](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="51872-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="51872-185">На странице приветствия веб-заданий, выберите hello задание **расписание** страницы портала планировщика Azure toohello toonavigate ссылку.</span><span class="sxs-lookup"><span data-stu-id="51872-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![Связать tooAzure планировщика][LinkToScheduler]
2. <span data-ttu-id="51872-187">На странице приветствия планировщика выберите задание hello.</span><span class="sxs-lookup"><span data-stu-id="51872-187">On hello Scheduler page, click hello job.</span></span>
   
    ![Задание на странице портала hello планировщика][SchedulerPortal]
3. <span data-ttu-id="51872-189">Hello **действия задания** откроется, где можно продолжить настройку задания hello страница.</span><span class="sxs-lookup"><span data-stu-id="51872-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![Страница "Действие задания" в планировщике][JobActionPageInScheduler]

## <span data-ttu-id="51872-191"><a name="ViewJobHistory"></a>Просмотр журнала заданий hello</span><span class="sxs-lookup"><span data-stu-id="51872-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="51872-192">tooview hello журнал выполнения задания, включая задания, созданные с hello SDK веб-заданий, щелкните его соответствующую ссылку в поле hello **журналы** столбца колонка hello веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="51872-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="51872-193">(Hello буфер обмена toocopy hello URL-адрес значка hello страницы файла журнала toohello буфера обмена можно использовать при желании.)</span><span class="sxs-lookup"><span data-stu-id="51872-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![Ссылка на журналы](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="51872-195">Щелкнув ссылку hello открывается страница сведений о hello для hello веб-задания.</span><span class="sxs-lookup"><span data-stu-id="51872-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="51872-196">В этом страницы отображаются hello имя hello выполнения команды, hello последний раз, когда он был запущен и его успешность.</span><span class="sxs-lookup"><span data-stu-id="51872-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="51872-197">В разделе **недавно выполненные задания**, выберите время toosee подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="51872-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![Сведения о веб-задании][WebJobDetails]
3. <span data-ttu-id="51872-199">Hello **сведения о выполнении веб-задания** появится страница.</span><span class="sxs-lookup"><span data-stu-id="51872-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="51872-200">Нажмите кнопку **переключить вывод** toosee текст hello hello содержимое журнала.</span><span class="sxs-lookup"><span data-stu-id="51872-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="51872-201">Hello вывод журнала имеет текстовый формат.</span><span class="sxs-lookup"><span data-stu-id="51872-201">hello output log is in text format.</span></span> 
   
    ![Сведения о выполнении веб-задания][WebJobRunDetails]
4. <span data-ttu-id="51872-203">toosee hello выходного текста в отдельном окне браузера, щелкните hello **загрузки** ссылку.</span><span class="sxs-lookup"><span data-stu-id="51872-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="51872-204">toodownload hello самого текста, щелкните правой кнопкой мыши ссылку hello и использовать ваш содержимое файла параметров toosave браузера hello.</span><span class="sxs-lookup"><span data-stu-id="51872-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![Загрузка выходных данных журнала][DownloadLogOutput]
5. <span data-ttu-id="51872-206">Hello **веб-заданий** ссылку вверху hello страницы приветствия перечень удобный способ tooget tooa веб-заданий на панели мониторинга журнала hello.</span><span class="sxs-lookup"><span data-stu-id="51872-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![Список tooWebJobs ссылок][WebJobsLinkToDashboardList]
   
    ![Список веб-заданий на панели мониторинга журнала][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="51872-209">Выбрав одну из этих ссылок принимает страницу сведений о веб-задания toohello для hello задание, которое вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="51872-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="51872-210"><a name="WHPNotes"></a>Примечания</span><span class="sxs-lookup"><span data-stu-id="51872-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="51872-211">Веб-приложений в бесплатном режиме истечь время ожидания через 20 минут, при наличии узел диспетчера управления службами (развертывание) toohello без запросов и не открыт в Azure портал hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="51872-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="51872-212">Фактический сайт toohello запросы не сбрасываются это.</span><span class="sxs-lookup"><span data-stu-id="51872-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="51872-213">Код непрерывно выполняющегося задания должен toobe языке toorun бесконечного цикла.</span><span class="sxs-lookup"><span data-stu-id="51872-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="51872-214">Задания выполняются непрерывно, только если hello веб-приложение работает.</span><span class="sxs-lookup"><span data-stu-id="51872-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="51872-215">Основные и стандартные режимы предложение hello всегда на компонент, при включении предотвращает переходящих в состояние простоя веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="51872-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="51872-216">Можно отладить только те веб-задания, которые выполняются непрерывно.</span><span class="sxs-lookup"><span data-stu-id="51872-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="51872-217">Отладка веб-заданий, выполняющихся по расписанию или по требованию, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="51872-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="51872-218"><a name="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="51872-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="51872-219">Дополнительные сведения см. в разделе [Рекомендуемые ресурсы для веб-заданий Azure][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="51872-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

