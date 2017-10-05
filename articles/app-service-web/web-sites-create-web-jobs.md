---
title: "Выполнение фоновых задач с веб-заданиями"
description: "Узнайте, как выполнять фоновые задачи в веб-приложениях Azure."
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
ms.openlocfilehash: 3f8ae748e3d9c6b4e342536926a52b4e8f37ee51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="68189-103">Выполнение фоновых задач с веб-заданиями</span><span class="sxs-lookup"><span data-stu-id="68189-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="68189-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="68189-104">Overview</span></span>
<span data-ttu-id="68189-105">Программы или сценарии можно выполнять в веб-заданиях в веб-приложении [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) тремя способами: по запросу, непрерывно или по расписанию.</span><span class="sxs-lookup"><span data-stu-id="68189-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="68189-106">Для использования веб-заданий дополнительные затраты не требуются.</span><span class="sxs-lookup"><span data-stu-id="68189-106">There is no additional cost to use WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="68189-107">В данной статье показано, как развернуть веб-задания с помощью [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68189-107">This article shows how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="68189-108">Информацию о развертывании с помощью Visual Studio или процесса непрерывной доставки см. в разделе [Развертывание веб-заданий с помощью Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="68189-108">For information about how to deploy by using Visual Studio or a continuous delivery process, see [How to Deploy Azure WebJobs to Web Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="68189-109">Пакет SDK веб-заданий Azure упрощает многие задачи программирования для веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="68189-109">The Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="68189-110">Дополнительные сведения см. в разделе [Информация о пакете SDK веб-заданий](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="68189-110">For more information, see [What is the WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="68189-111">Функции Azure предоставляют еще один способ запуска программ и сценариев из безсерверной среды или приложения службы приложений.</span><span class="sxs-lookup"><span data-stu-id="68189-111">Azure Functions provides another way to run programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="68189-112">Дополнительные сведения см. в статье [Обзор функций Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68189-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="68189-113"><a name="acceptablefiles"></a>Допустимые типы файлов для скриптов и программ</span><span class="sxs-lookup"><span data-stu-id="68189-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="68189-114">Допустимы следующие типы файлов:</span><span class="sxs-lookup"><span data-stu-id="68189-114">The following file types are accepted:</span></span>

* <span data-ttu-id="68189-115">.cmd, .bat, .exe (с использованием командной строки windows)</span><span class="sxs-lookup"><span data-stu-id="68189-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="68189-116">.ps1 (с использованием powershell)</span><span class="sxs-lookup"><span data-stu-id="68189-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="68189-117">.sh (с использованием bash)</span><span class="sxs-lookup"><span data-stu-id="68189-117">.sh (using bash)</span></span>
* <span data-ttu-id="68189-118">.PHP (с использованием php)</span><span class="sxs-lookup"><span data-stu-id="68189-118">.php (using php)</span></span>
* <span data-ttu-id="68189-119">.py (с использованием python)</span><span class="sxs-lookup"><span data-stu-id="68189-119">.py (using python)</span></span>
* <span data-ttu-id="68189-120">.js (с использованием node)</span><span class="sxs-lookup"><span data-stu-id="68189-120">.js (using node)</span></span>
* <span data-ttu-id="68189-121">.jar (с использованием java)</span><span class="sxs-lookup"><span data-stu-id="68189-121">.jar (using java)</span></span>

## <span data-ttu-id="68189-122"><a name="CreateOnDemand"></a>Создание веб-задания по запросу на портале</span><span class="sxs-lookup"><span data-stu-id="68189-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in the portal</span></span>
1. <span data-ttu-id="68189-123">В колонке **Веб-приложение** на [портале Azure](https://portal.azure.com) щелкните **Все параметры > Веб-задания** для отображения колонки **Веб-задания**.</span><span class="sxs-lookup"><span data-stu-id="68189-123">In the **Web App** blade of the [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** to show the **WebJobs** blade.</span></span>
   
    ![Колонка "Веб-задания"](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="68189-125">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="68189-125">Click **Add**.</span></span> <span data-ttu-id="68189-126">Появится диалоговое окно **Добавление веб-задания** .</span><span class="sxs-lookup"><span data-stu-id="68189-126">The **Add WebJob** dialog appears.</span></span>
   
    ![Колонка "Добавление веб-задания"](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="68189-128">В поле **Имя**укажите имя веб-задания.</span><span class="sxs-lookup"><span data-stu-id="68189-128">Under **Name**, provide a name for the WebJob.</span></span> <span data-ttu-id="68189-129">Имя должно начинаться с буквы или цифры и не может содержать специальные символы, отличные от "-" и "_".</span><span class="sxs-lookup"><span data-stu-id="68189-129">The name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="68189-130">В поле **Как выполнить** выберите пункт **Выполнять по требованию**.</span><span class="sxs-lookup"><span data-stu-id="68189-130">In the **How to Run** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="68189-131">В поле **Отправка файла** щелкните значок папки и перейдите к ZIP-файлу, который содержит скрипт.</span><span class="sxs-lookup"><span data-stu-id="68189-131">In the **File Upload** box, click the folder icon and browse to the zip file that contains your script.</span></span> <span data-ttu-id="68189-132">ZIP-файл должен содержать исполняемый файл (.exe .cmd .bat .sh .php .py .js), а также все вспомогательные файлы, необходимые для запуска программы или скрипта.</span><span class="sxs-lookup"><span data-stu-id="68189-132">The zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed to run the program or script.</span></span>
6. <span data-ttu-id="68189-133">Поставьте флажок **Создать** , чтобы передать скрипт в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="68189-133">Check **Create** to upload the script to your web app.</span></span> 
   
    <span data-ttu-id="68189-134">Имя, которое вы присвоили веб-заданию, появится в списке, приведенном в колонке **Веб-задания** .</span><span class="sxs-lookup"><span data-stu-id="68189-134">The name you specified for the WebJob appears in the list on the **WebJobs** blade.</span></span>
7. <span data-ttu-id="68189-135">Чтобы запустить веб-задание, щелкните правой кнопкой мыши его имя в списке и нажмите **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="68189-135">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![Запуск веб-задания](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="68189-137"><a name="CreateContinuous"></a>Создание непрерывно выполняющегося веб-задания</span><span class="sxs-lookup"><span data-stu-id="68189-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="68189-138">Чтобы создать непрерывно выполняющееся веб-задание, следуйте инструкциям по созданию задания, которое запускается один раз, только в поле **Как выполнить** выберите значение **Непрерывно**.</span><span class="sxs-lookup"><span data-stu-id="68189-138">To create a continuously executing WebJob, follow the same steps for creating a WebJob that runs once, but in the **How to Run** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="68189-139">Чтобы запустить или остановить непрерывное веб-задание, щелкните правой кнопкой мыши веб-задание в списке и выберите **Запустить** или **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="68189-139">To start or stop a continuous WebJob, right-click the WebJob in the list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="68189-140">Если веб-приложение работает на нескольких экземплярах, непрерывно выполняемое веб-задание будет работать на всех экземплярах.</span><span class="sxs-lookup"><span data-stu-id="68189-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="68189-141">Веб-задания по требованию и запланированные задачи запускаются на отдельном экземпляре, выбранном Microsoft Azure для балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="68189-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="68189-142">Для надежной работы непрерывных веб-заданий на всех экземплярах включите параметр конфигурации "Всегда включено*" для веб-приложения, иначе они могут прекращать работу при слишком долгом простое сайта-хоста SCM.</span><span class="sxs-lookup"><span data-stu-id="68189-142">For Continuous WebJobs to run reliably and on all instances, enable the Always On* configuration setting for the web app otherwise they can stop running when the SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="68189-143"><a name="CreateScheduledCRON"></a>Создание запланированного веб-задания с использованием выражения CRON</span><span class="sxs-lookup"><span data-stu-id="68189-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="68189-144">Этот метод можно использовать для веб-приложений, работающих в режимах "Базовый", "Стандартный" или "Премиум". В этом случае в приложении необходимо включить параметр **Всегда включено**.</span><span class="sxs-lookup"><span data-stu-id="68189-144">This technique is available to Web Apps running in Basic, Standard or Premium mode, and requires the **Always On** setting to be enabled on the app.</span></span>

<span data-ttu-id="68189-145">Чтобы превратить веб-задание по запросу в запланированное веб-задание, просто добавьте файл `settings.job` в корень ZIP-файла веб-задания.</span><span class="sxs-lookup"><span data-stu-id="68189-145">To turn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at the root of your WebJob zip file.</span></span> <span data-ttu-id="68189-146">JSON-файл должен содержать свойство `schedule` с [выражением CRON](https://en.wikipedia.org/wiki/Cron), как в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="68189-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="68189-147">Выражение CRON состоит из 6 полей: `{second} {minute} {hour} {day} {month} {day of the week}`.</span><span class="sxs-lookup"><span data-stu-id="68189-147">The CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="68189-148">Например, чтобы веб-задание активировалось каждые 15 минут, `settings.job` должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="68189-148">For example, to trigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="68189-149">Другие примеры расписания для выражения CRON:</span><span class="sxs-lookup"><span data-stu-id="68189-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="68189-150">Каждый час (т. е. когда количество минут — 0): `0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="68189-150">Every hour (i.e. whenever the count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="68189-151">Каждый час с 9:00 до 17:00: `0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="68189-151">Every hour from 9 AM to 5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="68189-152">Каждый день в 9:30: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="68189-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="68189-153">Каждый рабочий день в 9:30: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="68189-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="68189-154">**Примечание**. При развертывании веб-задания из Visual Studio для свойств файла `settings.job` установите значение "Копировать, если новее".</span><span class="sxs-lookup"><span data-stu-id="68189-154">**Note**: when deploying a WebJob from Visual Studio, make sure to mark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="68189-155"><a name="CreateScheduled"></a>Создание запланированного веб-задания с использованием планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="68189-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using the Azure Scheduler</span></span>
<span data-ttu-id="68189-156">В следующем альтернативном методе используется планировщик Azure.</span><span class="sxs-lookup"><span data-stu-id="68189-156">The following alternate technique makes use of the Azure Scheduler.</span></span> <span data-ttu-id="68189-157">В этом случае у веб-задания нет достоверных данных о расписании.</span><span class="sxs-lookup"><span data-stu-id="68189-157">In this case, your WebJob does not have any direct knowledge of the schedule.</span></span> <span data-ttu-id="68189-158">Вместо этого планировщик Azure активирует веб-задания по расписанию.</span><span class="sxs-lookup"><span data-stu-id="68189-158">Instead, the Azure Scheduler gets configured to trigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="68189-159">На классическом портале Azure еще нет возможности создавать запланированные веб-задания, но, пока эта функция не добавлена, вы можете использовать для создания запланированного веб-задания [классический портал](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="68189-159">The Azure Portal doesn't yet have the ability to create a scheduled WebJob, but until that feature is added you can do it by using the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="68189-160">На [классическом портале](http://manage.windowsazure.com) перейдите на страницу веб-задания и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="68189-160">In the [classic portal](http://manage.windowsazure.com) go to the WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="68189-161">В поле **Как выполнить** выберите **Выполнять по расписанию**.</span><span class="sxs-lookup"><span data-stu-id="68189-161">In the **How to Run** box, choose **Run on a schedule**.</span></span>
   
    ![Новое запланированное задание][NewScheduledJob]
3. <span data-ttu-id="68189-163">Выберите **Регион планировщика** для задания и нажмите кнопку со стрелкой в правом нижнем углу диалогового окна, чтобы перейти к следующему экрану.</span><span class="sxs-lookup"><span data-stu-id="68189-163">Choose the **Scheduler Region** for your job, and then click the arrow on the bottom right of the dialog to proceed to the next screen.</span></span>
4. <span data-ttu-id="68189-164">В диалоговом окне **Создать задание** выберите нужный тип в разделе **Повторение**: **Разовое задание** или **Повторяющееся задание**.</span><span class="sxs-lookup"><span data-stu-id="68189-164">In the **Create Job** dialog, choose the type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Запланированное повторение][SchdRecurrence]
5. <span data-ttu-id="68189-166">Кроме того, выберите время запуска в разделе **Запуск**: **Сейчас** или **В определенное время**.</span><span class="sxs-lookup"><span data-stu-id="68189-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Время начала по расписанию][SchdStart]
6. <span data-ttu-id="68189-168">Если необходимо начать в определенное время, выберите значения времени запуска в поле **Начало в**.</span><span class="sxs-lookup"><span data-stu-id="68189-168">If you want to start at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Расписание запуска в определенное время][SchdStartOn]
7. <span data-ttu-id="68189-170">Если выбрано повторяющееся задание, с помощью параметра **Повторять каждые** можно указать частоту повторения, а с помощью параметра **Заканчивается** – время завершения.</span><span class="sxs-lookup"><span data-stu-id="68189-170">If you chose a recurring job, you have the **Recur Every** option to specify the frequency of occurrence and the **Ending On** option to specify an ending time.</span></span>
   
    ![Запланированное повторение][SchdRecurEvery]
8. <span data-ttu-id="68189-172">При выборе значения **Недели** можно выбрать поле **В определенном расписании** и указать дни недели, в которые должно запускаться это задание.</span><span class="sxs-lookup"><span data-stu-id="68189-172">If you choose **Weeks**, you can select the **On a Particular Schedule** box and specify the days of the week that you want the job to run.</span></span>
   
    ![Запланированные дни недели][SchdWeeksOnParticular]
9. <span data-ttu-id="68189-174">При выборе значения **Месяцы** и выбора поля **В определенном расписании** можно определить запуск задания в определенные, пронумерованные **дни** месяца.</span><span class="sxs-lookup"><span data-stu-id="68189-174">If you choose **Months** and select the **On a Particular Schedule** box, you can set the job to run on particular numbered **Days** in the month.</span></span> 
   
    ![Планирование определенных дат месяца][SchdMonthsOnPartDays]
10. <span data-ttu-id="68189-176">При выборе значения **Дни недели**можно выбрать, в какой день или в какие дни недели месяца необходимо запускать задание.</span><span class="sxs-lookup"><span data-stu-id="68189-176">If you choose **Week Days**, you can select which day or days of the week in the month you want the job to run on.</span></span>
    
     ![Планирование определенных дней недели в месяце][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="68189-178">Наконец, можно также использовать параметр **Вхождения** для выбора недели месяца (первая, вторая, третья и т. д.), во время которой задание должно выполняться в указанные дни недели.</span><span class="sxs-lookup"><span data-stu-id="68189-178">Finally, you can also use the **Occurrences** option to choose which week in the month (first, second, third etc.) you want the job to run on the week days you specified.</span></span>
    
    ![Планирование определенных дней недели в определенные недели месяца][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="68189-180">Имена созданных заданий будут отображаться на вкладке "Веб-задания" вместе с данными об их состоянии, типе расписания и прочей информацией.</span><span class="sxs-lookup"><span data-stu-id="68189-180">After you have created one or more jobs, their names will appear on the WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="68189-181">Сохраняются журнальные данные для последних 30 выполненных веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="68189-181">Historical information for the last 30  WebJobs is maintained.</span></span>
    
    ![Список заданий][WebJobsListWithSeveralJobs]

### <span data-ttu-id="68189-183"><a name="Scheduler"></a>Запланированные задания и планировщик Azure</span><span class="sxs-lookup"><span data-stu-id="68189-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="68189-184">На страницах планировщика Azure на [классическом портале](http://manage.windowsazure.com)можно выполнить дополнительную настройку запланированных заданий.</span><span class="sxs-lookup"><span data-stu-id="68189-184">Scheduled jobs can be further configured in the Azure Scheduler pages of the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="68189-185">Чтобы перейти на страницу портала планировщика Azure, щелкните **расписание** задания на странице "Веб-задания".</span><span class="sxs-lookup"><span data-stu-id="68189-185">On the WebJobs page, click the job's **schedule** link to navigate to the Azure Scheduler portal page.</span></span> 
   
   ![Ссылка на планировщик Azure][LinkToScheduler]
2. <span data-ttu-id="68189-187">Выберите задание на странице планировщика.</span><span class="sxs-lookup"><span data-stu-id="68189-187">On the Scheduler page, click the job.</span></span>
   
    ![Задание на странице портала планировщика][SchedulerPortal]
3. <span data-ttu-id="68189-189">Откроется страница **Действие задания** , на которой можно выполнить дополнительную настройку задания.</span><span class="sxs-lookup"><span data-stu-id="68189-189">The **Job Action** page opens, where you can further configure the job.</span></span> 
   
    ![Страница "Действие задания" в планировщике][JobActionPageInScheduler]

## <span data-ttu-id="68189-191"><a name="ViewJobHistory"></a>Просмотр журнала заданий</span><span class="sxs-lookup"><span data-stu-id="68189-191"><a name="ViewJobHistory"></a>View the job history</span></span>
1. <span data-ttu-id="68189-192">Чтобы просмотреть журнал выполнения задания, включая задания, созданные с помощью пакета SDK для веб-заданий, щелкните соответствующую ссылку в столбце **Журналы** колонки "Веб-задания".</span><span class="sxs-lookup"><span data-stu-id="68189-192">To view the execution history of a job, including jobs created with the WebJobs SDK, click  its corresponding link under the **Logs** column of the WebJobs blade.</span></span> <span data-ttu-id="68189-193">Можно также использовать значок буфера обмена для копирования URL-адреса страницы файла журнала в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="68189-193">(You can use the clipboard icon to copy the URL of the log file page to the clipboard if you wish.)</span></span>
   
    ![Ссылка на журналы](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="68189-195">При щелчке ссылки открывается страница информации о веб-задании.</span><span class="sxs-lookup"><span data-stu-id="68189-195">Clicking the link opens the details page for the WebJob.</span></span> <span data-ttu-id="68189-196">На этой странице отображаются имя выполненной команды, время ее последнего выполнения, а также сведения об успешности выполнения.</span><span class="sxs-lookup"><span data-stu-id="68189-196">This page shows you the name of the command run, the last times it ran, and its success or failure.</span></span> <span data-ttu-id="68189-197">Укажите время в разделе **Недавно выполненные задания**, чтобы просмотреть дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="68189-197">Under **Recent job runs**, click a time to see further details.</span></span>
   
    ![Сведения о веб-задании][WebJobDetails]
3. <span data-ttu-id="68189-199">Откроется страница **Сведения о выполнении WebJob** .</span><span class="sxs-lookup"><span data-stu-id="68189-199">The **WebJob Run Details** page appears.</span></span> <span data-ttu-id="68189-200">Щелкните **Переключить вывод** , чтобы просмотреть текст журнала.</span><span class="sxs-lookup"><span data-stu-id="68189-200">Click **Toggle Output** to see the text of the log contents.</span></span> <span data-ttu-id="68189-201">Журнал выводится в текстовом формате.</span><span class="sxs-lookup"><span data-stu-id="68189-201">The output log is in text format.</span></span> 
   
    ![Сведения о выполнении веб-задания][WebJobRunDetails]
4. <span data-ttu-id="68189-203">Чтобы просмотреть текст вывода в отдельном окне браузера, щелкните ссылку **скачать** .</span><span class="sxs-lookup"><span data-stu-id="68189-203">To see the output text in a separate browser window, click the **download** link.</span></span> <span data-ttu-id="68189-204">Чтобы загрузить текст, щелкните ссылку правой кнопкой мыши и выберите команду для сохранения содержимого файла в контекстном меню браузера.</span><span class="sxs-lookup"><span data-stu-id="68189-204">To download the text itself, right-click the link and use your browser options to save the file contents.</span></span>
   
    ![Загрузка выходных данных журнала][DownloadLogOutput]
5. <span data-ttu-id="68189-206">Чтобы получить список веб-заданий на панели мониторинга журнала, вы можете воспользоваться ссылкой **Веб-задания** вверху страницы.</span><span class="sxs-lookup"><span data-stu-id="68189-206">The **WebJobs** link at the top of the page provides a convenient way to get to a list of WebJobs on the history dashboard.</span></span>
   
    ![Ссылка на список веб-заданий][WebJobsLinkToDashboardList]
   
    ![Список веб-заданий на панели мониторинга журнала][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="68189-209">При щелчке одной из этих ссылок открывается страница "Сведения о веб-задании" для выбранного задания.</span><span class="sxs-lookup"><span data-stu-id="68189-209">Clicking one of these links takes you to the WebJob Details page for the job you selected.</span></span>

## <span data-ttu-id="68189-210"><a name="WHPNotes"></a>Примечания</span><span class="sxs-lookup"><span data-stu-id="68189-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="68189-211">В бесплатном режиме веб-приложений время ожидания может истекать, если в Azure не открыт портал веб-приложения и запросы к сайту SCM (развертывание) не поступают в течение 20 минут.</span><span class="sxs-lookup"><span data-stu-id="68189-211">Web apps in Free mode can time out after 20 minutes if there are no requests to the scm (deployment) site and the web app's portal is not open in Azure.</span></span> <span data-ttu-id="68189-212">При этом такое поведение наблюдается даже при наличии запросов к фактическому сайту.</span><span class="sxs-lookup"><span data-stu-id="68189-212">Requests to the actual site will not reset this.</span></span>
* <span data-ttu-id="68189-213">Код непрерывно выполняющегося задания должен выполняться в бесконечном цикле.</span><span class="sxs-lookup"><span data-stu-id="68189-213">Code for a continuous job needs to be written to run in an endless loop.</span></span>
* <span data-ttu-id="68189-214">Задания выполняются непрерывно только во время работы веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="68189-214">Continuous jobs run continuously only when the web app is up.</span></span>
* <span data-ttu-id="68189-215">В базовом и стандартном режимах реализована функция "Всегда включено", которая позволяет предотвратить переход веб-приложений в неактивное состояние.</span><span class="sxs-lookup"><span data-stu-id="68189-215">Basic and Standard modes offer the Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="68189-216">Можно отладить только те веб-задания, которые выполняются непрерывно.</span><span class="sxs-lookup"><span data-stu-id="68189-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="68189-217">Отладка веб-заданий, выполняющихся по расписанию или по требованию, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="68189-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="68189-218"><a name="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68189-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="68189-219">Дополнительные сведения см. в разделе [Рекомендуемые ресурсы для веб-заданий Azure][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="68189-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

