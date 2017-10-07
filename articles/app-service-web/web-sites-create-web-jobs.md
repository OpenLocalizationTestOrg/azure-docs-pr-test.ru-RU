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
# <a name="run-background-tasks-with-webjobs"></a>Выполнение фоновых задач с веб-заданиями
## <a name="overview"></a>Обзор
Программы или сценарии можно выполнять в веб-заданиях в веб-приложении [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) тремя способами: по запросу, непрерывно или по расписанию. Нет без дополнительных затрат toouse веб-заданий.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

В этой статье показано, как hello toodeploy веб-заданий с помощью [портала Azure](https://portal.azure.com). Сведения о том, как toodeploy с помощью Visual Studio или процесс непрерывной поставки, в разделе [как веб-заданий Azure tooDeploy tooWeb приложения](websites-dotnet-deploy-webjobs.md).

Hello Azure SDK веб-заданий упрощает многие задачи программирования веб-заданий. Дополнительные сведения см. в разделе [возможности hello SDK веб-задания](websites-dotnet-webjobs-sdk.md).

 Функции Azure предоставляет другим способом toorun программ и сценариев, в данной среде или из приложения службы приложений. Дополнительные сведения см. в статье [Обзор функций Azure](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Допустимые типы файлов для скриптов и программ
Допустимы следующие типы файлов Hello:

* .cmd, .bat, .exe (с использованием командной строки windows)
* .ps1 (с использованием powershell)
* .sh (с использованием bash)
* .PHP (с использованием php)
* .py (с использованием python)
* .js (с использованием node)
* .jar (с использованием java)

## <a name="CreateOnDemand"></a>Создание веб-задания по запросу на портале hello
1. В hello **веб-приложения** колонке hello [портала Azure](https://portal.azure.com), нажмите кнопку **все параметры > веб-заданий** tooshow hello **веб-заданий** колонку.
   
    ![Колонка "Веб-задания"](./media/web-sites-create-web-jobs/wjblade.png)
2. Щелкните **Добавить**. Hello **добавить веб-задание** откроется диалоговое окно.
   
    ![Колонка "Добавление веб-задания"](./media/web-sites-create-web-jobs/addwjblade.png)
3. В разделе **имя**, введите имя для hello веб-задания. Hello имя должно начинаться с буквы или цифры и не может содержать специальные символы, отличные от «-» и «_».
4. В hello **как tooRun** выберите **выполнять по требованию**.
5. В hello **отправки файлов** щелкните значок папки hello и обзор toohello ZIP-файла, содержащего сценарий. Hello ZIP-файл должен содержать исполняемый файл (.exe .cmd .bat .sh .php .py .js) и все вспомогательные файлы, необходимые toorun hello программы или сценария.
6. Проверьте **создать** tooupload hello сценария tooyour веб-приложения. 
   
    Hello имя, указанное для hello веб-задания отображается в списке hello на hello **веб-заданий** колонку.
7. hello toorun веб-задание, щелкните правой кнопкой мыши его имя в списке hello и нажать кнопку **запуска**.
   
    ![Запуск веб-задания](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Создание непрерывно выполняющегося веб-задания
1. toocreate непрерывно выполняющегося веб-задания, выполните hello же шаги для создания веб-задание, выполняемое один раз, но в hello **как tooRun** выберите **Continuous**.
2. toostart или остановить непрерывные веб-задание, щелкните правой кнопкой мыши hello веб-задание в списке hello и нажмите кнопку **запустить** или **остановить**.

> [!NOTE]
> Если веб-приложение работает на нескольких экземплярах, непрерывно выполняемое веб-задание будет работать на всех экземплярах. Веб-задания по требованию и запланированные задачи запускаются на отдельном экземпляре, выбранном Microsoft Azure для балансировки нагрузки.
> 
> Для непрерывных веб-заданий toorun надежно и на всех экземплярах включить hello Always On * параметр конфигурации для hello веб-приложения в противном случае они для остановки выполнения после бездействия слишком долго hello SCM хост-сайта.
> 
> 

## <a name="CreateScheduledCRON"></a>Создание запланированного веб-задания с использованием выражения CRON
Этот метод доступен tooWeb приложения, выполняющиеся в режиме Basic, Standard или Premium и требует hello **Always On** параметр toobe включена приложение hello.

просто включите tooturn по запросу веб-задания в запланированные веб-задания `settings.job` файла в корне hello ZIP-файл веб-задания. JSON-файл должен содержать свойство `schedule` с [выражением CRON](https://en.wikipedia.org/wiki/Cron), как в примере ниже.

Hello CRON-выражение состоит из полей 6: `{second} {minute} {hour} {day} {month} {day of hello week}`.

Например, tootrigger веб-задание каждые 15 минут вашей `settings.job` будет иметь:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Другие примеры расписания для выражения CRON:

* Каждый час (т. е. когда hello число минут — 0):`0 0 * * * *` 
* Каждый час из too5 9: 00 PM:`0 0 9-17 * * *` 
* Каждый день в 9:30: `0 30 9 * * *`
* Каждый рабочий день в 9:30: `0 30 9 * * 1-5`

**Примечание**: при развертывании веб-задания из Visual Studio, убедитесь, что toomark вашей `settings.job` свойства файла как «Копировать более позднюю версию».

## <a name="CreateScheduled"></a>Создание запланированного веб-задания с помощью планировщика Azure hello
Здравствуйте, следуя альтернативный способ использует hello планировщика Azure. В этом случае веб-задание осведомлено прямой hello расписания. Вместо этого hello планировщика Azure возвращает настроенное tootrigger веб-задание по расписанию. 

Hello портала Azure пока еще не имеет возможности toocreate hello запланированных веб-задания, но пока не будет добавлен этот компонент это можно сделать с помощью hello [классический портал](http://manage.windowsazure.com).

1. В hello [классический портал](http://manage.windowsazure.com) переход на страницу веб-задания toohello и нажмите кнопку **добавить**.
2. В hello **как tooRun** выберите **по расписанию**.
   
    ![Новое запланированное задание][NewScheduledJob]
3. Выберите hello **область планировщика** для задания и нажмите стрелку hello hello нижней правой части hello диалоговое окно tooproceed toohello следующий экран.
4. В hello **создать задание** диалоговое окно, выберите тип hello **повторения** требуется: **Однократное задание** или **повторяющееся задание**.
   
    ![Запланированное повторение][SchdRecurrence]
5. Кроме того, выберите время запуска в разделе **Запуск**: **Сейчас** или **В определенное время**.
   
    ![Время начала по расписанию][SchdStart]
6. Toostart в определенное время, выберите ваш начальные значения времени в группе **запуск на**.
   
    ![Расписание запуска в определенное время][SchdStartOn]
7. Если вы выбрали повторяющееся задание, у вас есть hello **Повторять каждые** параметр toospecify hello частоту повторения и hello **заканчивается на** параметр toospecify время окончания.
   
    ![Запланированное повторение][SchdRecurEvery]
8. При выборе **недели**, можно выбрать hello **на определенное расписание** и укажите hello дни недели hello, который будет hello toorun задания.
   
    ![Расписание дни недели hello][SchdWeeksOnParticular]
9. При выборе **месяцев** и выберите hello **на определенное расписание** поле, можно задать toorun hello задания на конкретный номерами **дней** в месяце hello. 
   
    ![Запланировать определенных дат в месяце hello][SchdMonthsOnPartDays]
10. При выборе **дни недели**, можно выбрать какой день или дни недели hello требуется hello toorun задания в месяц hello.
    
     ![Планирование определенных дней недели в месяце][SchdMonthsOnPartWeekDays]
11. Наконец, можно также использовать hello **вхождений** toochoose параметр недель в месяце hello (первый, второй, третьего и т.д.) требуется hello toorun задания на hello дней недели.
    
    ![Планирование определенных дней недели в определенные недели месяца][SchdMonthsOnPartWeekDaysOccurences]
12. После создания одного или нескольких заданий их имена будут отображаться на вкладке hello веб-заданий с их состояние, тип расписания и другие сведения. Данные предыстории для hello последние 30 веб-заданий сохраняется.
    
    ![Список заданий][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Запланированные задания и планировщик Azure
Запланированные задания можно в дальнейшем можно настроить на страницах планировщика Azure hello hello [классический портал](http://manage.windowsazure.com).

1. На странице приветствия веб-заданий, выберите hello задание **расписание** страницы портала планировщика Azure toohello toonavigate ссылку. 
   
   ![Связать tooAzure планировщика][LinkToScheduler]
2. На странице приветствия планировщика выберите задание hello.
   
    ![Задание на странице портала hello планировщика][SchedulerPortal]
3. Hello **действия задания** откроется, где можно продолжить настройку задания hello страница. 
   
    ![Страница "Действие задания" в планировщике][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Просмотр журнала заданий hello
1. tooview hello журнал выполнения задания, включая задания, созданные с hello SDK веб-заданий, щелкните его соответствующую ссылку в поле hello **журналы** столбца колонка hello веб-заданий. (Hello буфер обмена toocopy hello URL-адрес значка hello страницы файла журнала toohello буфера обмена можно использовать при желании.)
   
    ![Ссылка на журналы](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Щелкнув ссылку hello открывается страница сведений о hello для hello веб-задания. В этом страницы отображаются hello имя hello выполнения команды, hello последний раз, когда он был запущен и его успешность. В разделе **недавно выполненные задания**, выберите время toosee подробные сведения.
   
    ![Сведения о веб-задании][WebJobDetails]
3. Hello **сведения о выполнении веб-задания** появится страница. Нажмите кнопку **переключить вывод** toosee текст hello hello содержимое журнала. Hello вывод журнала имеет текстовый формат. 
   
    ![Сведения о выполнении веб-задания][WebJobRunDetails]
4. toosee hello выходного текста в отдельном окне браузера, щелкните hello **загрузки** ссылку. toodownload hello самого текста, щелкните правой кнопкой мыши ссылку hello и использовать ваш содержимое файла параметров toosave браузера hello.
   
    ![Загрузка выходных данных журнала][DownloadLogOutput]
5. Hello **веб-заданий** ссылку вверху hello страницы приветствия перечень удобный способ tooget tooa веб-заданий на панели мониторинга журнала hello.
   
    ![Список tooWebJobs ссылок][WebJobsLinkToDashboardList]
   
    ![Список веб-заданий на панели мониторинга журнала][WebJobsListInJobsDashboard]
   
    Выбрав одну из этих ссылок принимает страницу сведений о веб-задания toohello для hello задание, которое вы выбрали.

## <a name="WHPNotes"></a>Примечания
* Веб-приложений в бесплатном режиме истечь время ожидания через 20 минут, при наличии узел диспетчера управления службами (развертывание) toohello без запросов и не открыт в Azure портал hello веб-приложения. Фактический сайт toohello запросы не сбрасываются это.
* Код непрерывно выполняющегося задания должен toobe языке toorun бесконечного цикла.
* Задания выполняются непрерывно, только если hello веб-приложение работает.
* Основные и стандартные режимы предложение hello всегда на компонент, при включении предотвращает переходящих в состояние простоя веб-приложений.
* Можно отладить только те веб-задания, которые выполняются непрерывно. Отладка веб-заданий, выполняющихся по расписанию или по требованию, не поддерживается.

## <a name="NextSteps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе [Рекомендуемые ресурсы для веб-заданий Azure][WebJobsRecommendedResources].

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

