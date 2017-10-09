---
title: "состояние aaaCheck, настройте ведение журнала и получать оповещения - приложения логики Azure | Документы Microsoft"
description: "Мониторинг состояния и производительности приложений логики, запись ведения журнала диагностики и настройка оповещений"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="3bd93-103">Мониторинг состояния, настройка ведения журнала диагностики и включение предупреждений для Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3bd93-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="3bd93-104">После [создания и запуска приложения логики](../logic-apps/logic-apps-create-a-logic-app.md) можно проверить его журнал запусков, журнал триггеров, состояние и производительность.</span><span class="sxs-lookup"><span data-stu-id="3bd93-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="3bd93-105">Для мониторинга событий в режиме реального времени и отладки можно настроить [ведение журнала диагностики](#azure-diagnostics) для приложения логики.</span><span class="sxs-lookup"><span data-stu-id="3bd93-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="3bd93-106">Это позволит [выполнять поиск и просматривать события](#find-events), такие как события триггера, события выполнения и события действия.</span><span class="sxs-lookup"><span data-stu-id="3bd93-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="3bd93-107">Также можно [использовать полученные диагностические данные в других службах](#extend-diagnostic-data), таких как служба хранилища Azure и концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd93-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="3bd93-108">Настройка tooget уведомлений о сбоях или других возможных проблемах [предупреждения](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="3bd93-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="3bd93-109">Например, можно создать оповещение, которое обнаруживает "более пяти запусков в течение часа, которые завершились сбоем".</span><span class="sxs-lookup"><span data-stu-id="3bd93-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="3bd93-110">Можно также настроить мониторинг, отслеживание и ведение журнала программными средствами с помощью [параметров и свойств событий системы диагностики Azure](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="3bd93-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="3bd93-111">Просмотр сведений о выполнении и журнале триггеров для приложения логики</span><span class="sxs-lookup"><span data-stu-id="3bd93-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="3bd93-112">toofind логику приложения в hello [портал Azure](https://portal.azure.com), на hello главного меню Azure, выберите **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="3bd93-113">В поле поиска hello, найдите «логику приложений» и нажмите кнопку **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Поиск приложения логики](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="3bd93-115">Hello портал Azure показывает все приложения hello логики, которые связаны с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd93-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="3bd93-116">Выберите приложение логики, а затем нажмите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="3bd93-117">Hello портал Azure показывает hello запусков журнал и журнал триггер для логики приложения.</span><span class="sxs-lookup"><span data-stu-id="3bd93-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="3bd93-118">Например:</span><span class="sxs-lookup"><span data-stu-id="3bd93-118">For example:</span></span>

   ![Журнал запусков и журнал триггеров для приложения логики](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="3bd93-120">**Запускает журнал** показывает все фрагменты hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="3bd93-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="3bd93-121">**Активировать журнал** показывает все действия триггера hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="3bd93-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="3bd93-122">Описание состояний см. в разделе [Устранение неполадок в работе приложения логики](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="3bd93-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="3bd93-123">Если вы не нашли hello появились ожидаемые данные, на панели инструментов hello, выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="3bd93-124">tooview hello шаги из конкретного запуска в разделе **журнала выполняется**, выберите запуска.</span><span class="sxs-lookup"><span data-stu-id="3bd93-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="3bd93-125">Hello монитора отображается каждый шаг в течение данного запуска.</span><span class="sxs-lookup"><span data-stu-id="3bd93-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="3bd93-126">Например:</span><span class="sxs-lookup"><span data-stu-id="3bd93-126">For example:</span></span>

   ![Действия для определенного запуска](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="3bd93-128">выберите Дополнительные сведения о запуске hello tooget **сведения о выполнении**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="3bd93-129">Эти сведения представлены шаги hello, состояния входных данных, и запустите выходные данные для hello.</span><span class="sxs-lookup"><span data-stu-id="3bd93-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   ![Выберите "Подробности о запуске"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="3bd93-131">Например, можно получить hello запуска **идентификатор корреляции**, которой может потребоваться при использовании hello [API-интерфейса REST для логики приложений](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="3bd93-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="3bd93-132">tooget подробности о конкретных шагах, щелкните этот шаг.</span><span class="sxs-lookup"><span data-stu-id="3bd93-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="3bd93-133">После этого можно просмотреть такие сведения для данного этапа, как входные данные, выходные данные и все ошибки.</span><span class="sxs-lookup"><span data-stu-id="3bd93-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="3bd93-134">Например:</span><span class="sxs-lookup"><span data-stu-id="3bd93-134">For example:</span></span>

   ![Сведения об этапе](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="3bd93-136">Все сведения о времени выполнения и событиях, шифруются в hello логику приложения службы.</span><span class="sxs-lookup"><span data-stu-id="3bd93-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="3bd93-137">Они расшифровываются только в том случае, когда пользователь запрашивает tooview этих данных.</span><span class="sxs-lookup"><span data-stu-id="3bd93-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="3bd93-138">Можно также контролировать доступ к событиям toothese с [Azure Role-Based управления доступом (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="3bd93-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="3bd93-139">tooget сведений о событии триггера, вернитесь к предыдущему окну toohello **Обзор** области.</span><span class="sxs-lookup"><span data-stu-id="3bd93-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="3bd93-140">В разделе **активировать журнал**выберите событие триггера hello.</span><span class="sxs-lookup"><span data-stu-id="3bd93-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="3bd93-141">Теперь можно просмотреть такие сведения, как входные и выходные данные, например:</span><span class="sxs-lookup"><span data-stu-id="3bd93-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Выходные данные события триггера](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="3bd93-143">Включение ведения журнала диагностики для приложения логики</span><span class="sxs-lookup"><span data-stu-id="3bd93-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="3bd93-144">Для отладки с использованием сведений о среде выполнения и событиях можно настроить ведение журнала диагностики с помощью [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3bd93-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="3bd93-145">Аналитика журналов представляет собой службу в [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) , отслеживает облачных и локальных сред toohelp Ведение их доступности и производительности.</span><span class="sxs-lookup"><span data-stu-id="3bd93-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="3bd93-146">Прежде чем начать, необходимо toohave рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="3bd93-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="3bd93-147">Дополнительные сведения [как toocreate рабочей области OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3bd93-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="3bd93-148">В hello [портал Azure](https://portal.azure.com), найдите и выберите логику приложения.</span><span class="sxs-lookup"><span data-stu-id="3bd93-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="3bd93-149">Меню hello логику приложения колонке под **мониторинг**, выберите **диагностики** > **параметров диагностики**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Go tooMonitoring диагностики, диагностические параметры](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="3bd93-151">В разделе **Параметры диагностики** выберите **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Включение журналов диагностики](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="3bd93-153">Теперь выберите hello OMS рабочей области и категории событий для ведения журнала, как показано:</span><span class="sxs-lookup"><span data-stu-id="3bd93-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="3bd93-154">Выберите **отправки tooLog Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="3bd93-155">В разделе **Log Analytics** выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="3bd93-156">В разделе **рабочих областей OMS**, выберите toouse рабочей области OMS hello для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="3bd93-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="3bd93-157">В разделе **журнала**выберите hello **WorkflowRuntime** категории.</span><span class="sxs-lookup"><span data-stu-id="3bd93-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="3bd93-158">Выберите метрики интервал приветствия.</span><span class="sxs-lookup"><span data-stu-id="3bd93-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="3bd93-159">Когда все будет готово, нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-159">When you're done, choose **Save**.</span></span>

   ![Выберите рабочую область OMS и данные для ведения журнала](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="3bd93-161">Теперь можно выполнять поиск событий и других данных, таких как события триггера, события выполнения и события действия.</span><span class="sxs-lookup"><span data-stu-id="3bd93-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="3bd93-162">Поиск событий и данных для приложения логики</span><span class="sxs-lookup"><span data-stu-id="3bd93-162">Find events and data for your logic app</span></span>

<span data-ttu-id="3bd93-163">toofind и представление события в приложении логику как события триггера, запускать события и действие, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3bd93-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="3bd93-164">В hello [портал Azure](https://portal.azure.com), выберите **более служб**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="3bd93-165">Введите в поле поиска "log analytics" и выберите **Log Analytics**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3bd93-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Выберите "Log Analytics"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="3bd93-167">В разделе **Log Analytics** найдите и выберите рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="3bd93-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Выбор рабочей области OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="3bd93-169">В разделе **Управление** выберите **Портал OMS**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Выберите "Портал OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="3bd93-171">На домашней странице OMS выберите **Поиск по журналам**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-171">On your OMS home page, choose **Log Search**.</span></span>

   ![На домашней странице OMS выберите "Поиск по журналам"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="3bd93-173">-или-</span><span class="sxs-lookup"><span data-stu-id="3bd93-173">-or-</span></span>

   ![Hello OMS выберите пункт меню «Поиск журналов»](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="3bd93-175">В поле поиска hello, укажите поля, которые должны toofind и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="3bd93-176">При вводе OMS предлагает возможные совпадения и операции, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="3bd93-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="3bd93-177">Например, toofind hello первые 10 событий, возникших, введите и выберите этот запрос поиска: **категории = WorkflowRuntime | top 10**</span><span class="sxs-lookup"><span data-stu-id="3bd93-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Введите строку поиска](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="3bd93-179">Дополнительные сведения о [как toofind данных в службе анализа журналов](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="3bd93-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="3bd93-180">На странице результатов hello hello левой панели выберите hello промежуток времени, которые должны tooview.</span><span class="sxs-lookup"><span data-stu-id="3bd93-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="3bd93-181">Выберите запрос, добавив фильтр, toorefine **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![Выберите период времени для результатов запроса](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="3bd93-183">В разделе **добавить фильтры**, введите имя фильтра hello, чтобы найти нужный фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="3bd93-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="3bd93-184">Выберите фильтр hello и выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="3bd93-185">Этот пример использует hello toofind слово «состояние» сбой события внутри **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="3bd93-186">Здесь hello фильтр для **status_s** уже выбрана.</span><span class="sxs-lookup"><span data-stu-id="3bd93-186">Here hello filter for **status_s** is already selected.</span></span>

   ![Выбор фильтра](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="3bd93-188">Hello левой панели выберите значение фильтра hello, toouse и задайте **применить**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![Выберите значение фильтра, нажмите кнопку "Применить"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="3bd93-190">Теперь возвращают toohello запрос, для которого выполняется сборка.</span><span class="sxs-lookup"><span data-stu-id="3bd93-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="3bd93-191">Запрос был обновлен с учетом выбранных фильтра и значения.</span><span class="sxs-lookup"><span data-stu-id="3bd93-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="3bd93-192">Предыдущие результаты теперь также отфильтрованы.</span><span class="sxs-lookup"><span data-stu-id="3bd93-192">Your previous results are now filtered too.</span></span>

   ![Возвращает запрос tooyour с отфильтрованные результаты](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="3bd93-194">Выберите запрос для использования в будущем toosave **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3bd93-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="3bd93-195">Дополнительные сведения [как toosave запроса](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="3bd93-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="3bd93-196">Расширение возможностей использования диагностических данных в других службах</span><span class="sxs-lookup"><span data-stu-id="3bd93-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="3bd93-197">Помимо Azure Log Analytics, можно расширить возможности использования диагностических данных приложения логики в других службах Azure, например:</span><span class="sxs-lookup"><span data-stu-id="3bd93-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="3bd93-198">Архивация журналов диагностики Azure в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="3bd93-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="3bd93-199">Журналы диагностики Azure поток tooAzure концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="3bd93-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="3bd93-200">После этого можно организовать мониторинг в режиме реального времени с помощью данных телеметрии и аналитики из других служб, таких как [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) и [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="3bd93-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="3bd93-201">Например:</span><span class="sxs-lookup"><span data-stu-id="3bd93-201">For example:</span></span>

* [<span data-ttu-id="3bd93-202">Поток данных из концентраторов событий tooStream аналитика</span><span class="sxs-lookup"><span data-stu-id="3bd93-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="3bd93-203">Анализ потоковой передачи данных с помощью Stream Analytics и создание панели мониторинга в Power BI для анализа данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="3bd93-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="3bd93-204">На основании hello параметры настройки, убедитесь, что вы первый [создать учетную запись хранилища Azure](../storage/common/storage-create-storage-account.md) или [создать концентратор событий Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="3bd93-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="3bd93-205">Затем выберите параметры hello место toosend диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="3bd93-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![Отправка данных tooAzure хранилища учетной записи или события концентратора](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="3bd93-207">Сроки хранения применяются только в том случае, при выборе toouse учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="3bd93-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="3bd93-208">Настройка оповещений для приложения логики</span><span class="sxs-lookup"><span data-stu-id="3bd93-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="3bd93-209">Настройка определенных показателей toomonitor или превышены пороговые значения для логики приложения, [оповещения в Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="3bd93-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="3bd93-210">Узнайте подробнее о [метриках в Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="3bd93-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="3bd93-211">tooset предупреждений без [Azure Log Analytics](../log-analytics/log-analytics-overview.md), выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3bd93-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="3bd93-212">Для расширенных критериев оповещений и действий необходимо также [настроить Log Analytics](#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="3bd93-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="3bd93-213">Меню hello логику приложения колонке под **мониторинг**, выберите **диагностики** > **предупреждения правила** > **добавить оповещение**как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="3bd93-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Добавление оповещения для приложения логики](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="3bd93-215">На hello **Добавление правила оповещения** колонки, создать предупреждение, как показано:</span><span class="sxs-lookup"><span data-stu-id="3bd93-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="3bd93-216">В разделе **Ресурс** выберите приложение логики, если оно еще выбрано.</span><span class="sxs-lookup"><span data-stu-id="3bd93-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="3bd93-217">Укажите имя и описание для оповещения.</span><span class="sxs-lookup"><span data-stu-id="3bd93-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="3bd93-218">Выберите **метрика** или события, которые должны tootrack.</span><span class="sxs-lookup"><span data-stu-id="3bd93-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="3bd93-219">Выберите **условие**, укажите **пороговое значение** метрика hello и выберите hello **период** для мониторинга эта метрика.</span><span class="sxs-lookup"><span data-stu-id="3bd93-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="3bd93-220">Укажите, требуется ли toosend почты для hello предупреждения.</span><span class="sxs-lookup"><span data-stu-id="3bd93-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="3bd93-221">Укажите адреса электронной почты для отправки предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="3bd93-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="3bd93-222">Можно также указать URL-адрес веб-перехватчика место toosend hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="3bd93-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="3bd93-223">Например, это правило отправляет оповещение после пяти или более сбоев выполнения в течение часа:</span><span class="sxs-lookup"><span data-stu-id="3bd93-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Создание правила оповещения для метрики](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="3bd93-225">приложения логики toorun из оповещения, можно включить hello [триггер запроса](../connectors/connectors-native-reqres.md) в рабочем процессе, которая позволяет выполнять такие задачи, как эти примеры:</span><span class="sxs-lookup"><span data-stu-id="3bd93-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="3bd93-226">POST tooSlack</span><span class="sxs-lookup"><span data-stu-id="3bd93-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="3bd93-227">Отправка текста</span><span class="sxs-lookup"><span data-stu-id="3bd93-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="3bd93-228">Добавить tooa очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="3bd93-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="3bd93-229">Параметры события диагностики Azure и подробные сведения о нем</span><span class="sxs-lookup"><span data-stu-id="3bd93-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="3bd93-230">Каждое событие диагностики содержит подробные сведения о приложении логики и данного события, например, состояние hello, время начала, время окончания и т. д.</span><span class="sxs-lookup"><span data-stu-id="3bd93-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="3bd93-231">tooprogrammatically настроить мониторинг, отслеживания и ведения журнала, подразделение можно использовать эти сведения с hello [REST API для приложения логики Azure](https://docs.microsoft.com/rest/api/logic) и hello [REST API для диагностики Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="3bd93-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="3bd93-232">Здравствуйте, например, `ActionCompleted` событие имеет hello `clientTrackingId` и `trackedProperties` свойства, которые можно использовать для отслеживания и наблюдения:</span><span class="sxs-lookup"><span data-stu-id="3bd93-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="3bd93-233">`clientTrackingId`: Если не указан, Azure автоматически создает этот идентификатор и корреляцию событий между логику приложения будут работать, включая все вложенные рабочие процессы, вызываются из приложения hello логики.</span><span class="sxs-lookup"><span data-stu-id="3bd93-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="3bd93-234">Можно вручную задать этот код из триггера, передав `x-ms-client-tracking-id` заголовок с пользовательское значение идентификатора в запросе hello триггера.</span><span class="sxs-lookup"><span data-stu-id="3bd93-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="3bd93-235">Можно использовать триггер запроса, триггер HTTP или триггер веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="3bd93-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="3bd93-236">`trackedProperties`: tootrack входные и выходные данные в данные диагностики, tooactions отслеживаемых свойств можно добавить в определение приложения логики JSON.</span><span class="sxs-lookup"><span data-stu-id="3bd93-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="3bd93-237">Отслеживаемых свойств можно отслеживать только входные и выходные данные одного действия, но можно использовать hello `correlation` свойства toocorrelate события для действий в сеансе.</span><span class="sxs-lookup"><span data-stu-id="3bd93-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="3bd93-238">tootrack добавить одно или несколько свойств hello `trackedProperties` раздел и hello свойства, которые хотите toohello определение действия.</span><span class="sxs-lookup"><span data-stu-id="3bd93-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="3bd93-239">Например предположим, что требуется tootrack данные, такие как «Идентификатор заказа» в телеметрии:</span><span class="sxs-lookup"><span data-stu-id="3bd93-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="3bd93-240">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3bd93-240">Next steps</span></span>

* [<span data-ttu-id="3bd93-241">Создание шаблонов для развертывания приложений логики и управления выпусками</span><span class="sxs-lookup"><span data-stu-id="3bd93-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="3bd93-242">Сценарии B2B с пакетом интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="3bd93-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="3bd93-243">Мониторинг сообщений B2B</span><span class="sxs-lookup"><span data-stu-id="3bd93-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)