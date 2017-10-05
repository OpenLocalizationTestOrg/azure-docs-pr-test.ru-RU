---
title: "Мониторинг выполнения приложений логики и получение аналитических сведений о них с помощью OMS в Azure Logic Apps | Документация Майкрософт"
description: "Мониторинг выполнения приложений логики с помощью Log Analytics и Operations Management Suite (OMS). Получение аналитических сведений и более подробных данных отладки для устранения неполадок и диагностики."
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: 0e9f0ef3c87b5c0da1cc4ad16d37178c8f5c9625
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="76599-103">Мониторинг выполнения приложений логики и получение аналитических сведений о них с помощью Operations Management Suite (OMS) и Log Analytics</span><span class="sxs-lookup"><span data-stu-id="76599-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="76599-104">Для мониторинга и получения более подробных данных отладки при создании приложения логики можно включить Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="76599-104">For monitoring and richer debugging information, you can turn on Log Analytics at the same time when you create a logic app.</span></span> <span data-ttu-id="76599-105">Служба Log Analytics предоставляет ведение журнала диагностики и мониторинг выполнения приложений логики на портале Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="76599-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through the Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="76599-106">При добавлении решения Logic Apps Management в OMS вы получаете обобщенные сведения о выполнении приложений логики, а также некоторые подробные данные, такие как состояние приложения, время выполнения, состояние повторной отправки и идентификаторы корреляции.</span><span class="sxs-lookup"><span data-stu-id="76599-106">When you add the Logic Apps Management solution to OMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="76599-107">В этом разделе показано, как включить службу Log Analytics или установить решение Logic Apps Management в OMS, чтобы вы могли просматривать события и данные среды выполнения, относящиеся к выполнению ваших приложений логики.</span><span class="sxs-lookup"><span data-stu-id="76599-107">This topic shows how to turn on Log Analytics or install the Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="76599-108">Чтобы отслеживать существующие приложения логики, выполните следующие действия для [включения ведения журнала диагностики и отправки данных среды выполнения приложений логики в OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="76599-108">To monitor your existing logic apps, follow these steps to [turn on diagnostic logging and send logic app runtime data to OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="76599-109">Требования</span><span class="sxs-lookup"><span data-stu-id="76599-109">Requirements</span></span>

<span data-ttu-id="76599-110">Прежде чем начать, необходимо иметь рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="76599-110">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="76599-111">Узнайте о том, [как создать ее](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="76599-111">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="76599-112">Включение ведения журнала диагностики при создании приложений логики</span><span class="sxs-lookup"><span data-stu-id="76599-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="76599-113">На [портале Azure](https://portal.azure.com) создайте приложение логики.</span><span class="sxs-lookup"><span data-stu-id="76599-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="76599-114">Выберите **Создать** > **Интеграция Enterprise** > **Приложение логики** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="76599-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Создайте приложение логики](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="76599-116">На странице **Создание приложения логики** выполните показанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="76599-116">In the **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="76599-117">Введите имя приложения логики и выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="76599-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="76599-118">Создайте или выберите существующую группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="76599-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="76599-119">Установите переключатель **Log Analytics** в положение **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="76599-119">Set **Log Analytics** to **On**.</span></span> 
   <span data-ttu-id="76599-120">Выберите рабочую область OMS, в которую будут отправляться данные, относящиеся к выполнению приложений логики.</span><span class="sxs-lookup"><span data-stu-id="76599-120">Select the OMS workspace where you want to send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="76599-121">Когда вы будете готовы, установите флажок **Закрепить на панели мониторинга** >  и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="76599-121">When you're ready, choose **Pin to dashboard** > **Create**.</span></span>

      ![Создание приложения логики](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="76599-123">По завершении этого шага Azure создает приложение логики, которое теперь связано с рабочей областью OMS.</span><span class="sxs-lookup"><span data-stu-id="76599-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="76599-124">На этом шаге в рабочую область OMS также автоматически устанавливается решение Logic Apps Management.</span><span class="sxs-lookup"><span data-stu-id="76599-124">Also, this step also automatically installs the Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="76599-125">Чтобы просмотреть сведения о выполнении приложений логики в OMS, [выполните следующие действия](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="76599-125">To view your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-the-logic-apps-management-solution-in-oms"></a><span data-ttu-id="76599-126">Установка решения Logic Apps Management в OMS</span><span class="sxs-lookup"><span data-stu-id="76599-126">Install the Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="76599-127">Если вы уже включили Log Analytics при создании приложения логики, то пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="76599-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="76599-128">Решение Logic Apps Management у вас уже установлено в OMS.</span><span class="sxs-lookup"><span data-stu-id="76599-128">You already have the Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="76599-129">На [портале Azure](https://portal.azure.com) щелкните **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="76599-129">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="76599-130">В поле поиска введите словосочетание "log analytics" в качестве фильтра и выберите **Log Analytics**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="76599-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Выберите "Log Analytics"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="76599-132">В разделе **Log Analytics** найдите и выберите рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="76599-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Выбор рабочей области OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="76599-134">В разделе **Управление** выберите **Портал OMS**.</span><span class="sxs-lookup"><span data-stu-id="76599-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Выберите "Портал OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="76599-136">Если на домашней странице OMS отображается баннер обновления, щелкните его, чтобы сначала обновить рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="76599-136">On your OMS homepage, if the upgrade banner appears, choose the banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="76599-137">Затем выберите **Коллекция решений**.</span><span class="sxs-lookup"><span data-stu-id="76599-137">Then choose **Solutions Gallery**.</span></span>

   ![Выбор "Коллекции решений"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="76599-139">В разделе **Все решения** найдите и выберите элемент решения **Logic Apps Management**.</span><span class="sxs-lookup"><span data-stu-id="76599-139">Under **All solutions**, find and choose the tile for the **Logic Apps Management** solution.</span></span>

   ![Выбор Logic Apps Management](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="76599-141">Чтобы установить решение в рабочую область OMS, нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="76599-141">To install the solution in your OMS workspace, choose **Add**.</span></span>

   ![Кнопка "Добавить" для Logic Apps Management](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="76599-143">Просмотр сведений о выполнении приложений логики в рабочей области OMS</span><span class="sxs-lookup"><span data-stu-id="76599-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="76599-144">Чтобы просмотреть число и состояние выполнений приложений логики, перейдите на страницу обзора своей рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="76599-144">To view the count and status for your logic app runs, go to the overview page for your OMS workspace.</span></span> <span data-ttu-id="76599-145">Просмотрите сведения в элементе **Logic Apps Management**.</span><span class="sxs-lookup"><span data-stu-id="76599-145">Review the details on the **Logic Apps Management** tile.</span></span>

   ![Элемент обзора, показывающий количество и состояние выполнений приложений логики](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="76599-147">Если баннер обновления отображается вместо элемента "Logic Apps Management" (Управление Logic Apps), щелкните баннер, чтобы сначала обновить рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="76599-147">If this upgrade banner appears instead of the Logic Apps Management tile, choose the banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Обновление рабочей области OMS](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="76599-149">Чтобы просмотреть сводку с более подробными сведениями о выполнении приложений логики, выберите элемент **Logic Apps Management**.</span><span class="sxs-lookup"><span data-stu-id="76599-149">To view a summary with more details about your logic app runs, choose the **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="76599-150">Здесь сведения о выполнении приложений логики группируются по имени или по состоянию выполнения.</span><span class="sxs-lookup"><span data-stu-id="76599-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Сводные данные о состоянии выполнения приложений логики](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="76599-152">Чтобы просмотреть все сведения о выполнении конкретного приложения логики или о конкретном состоянии, выберите строку с соответствующим приложением логики или состоянием.</span><span class="sxs-lookup"><span data-stu-id="76599-152">To view all the runs for a specific logic app or status, select the row for a logic app or a status.</span></span>

   <span data-ttu-id="76599-153">Ниже приведен пример, в котором показаны все сведения о выполнении конкретного приложения логики.</span><span class="sxs-lookup"><span data-stu-id="76599-153">Here is an example that shows all the runs for a specific logic app:</span></span>

   ![Просмотр сведений о выполнении по приложению логики или по состоянию](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="76599-155">В столбце **Resubmission** (Повторная отправка) отображается "Да", если выполнение является результатом повторного выполнения.</span><span class="sxs-lookup"><span data-stu-id="76599-155">The **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="76599-156">Чтобы отфильтровать эти результаты, можно применить фильтр как на стороне клиента, так и на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="76599-156">To filter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="76599-157">Клиентский фильтр: для каждого столбца выберите необходимые фильтры.</span><span class="sxs-lookup"><span data-stu-id="76599-157">Client-side filter: For each column, choose the filters that you want.</span></span> 
   <span data-ttu-id="76599-158">Ниже приведены некоторые примеры:</span><span class="sxs-lookup"><span data-stu-id="76599-158">Here are some examples:</span></span>

     ![Пример фильтров столбцов](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="76599-160">Серверный фильтр: чтобы выбрать определенное временное окно или ограничить отображаемое количество выполнений, воспользуйтесь элементом ограничения области в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="76599-160">Server-side filter: To choose a specific time window or to limit the number of runs that appear, use the scope control at the top of the page.</span></span> 
   <span data-ttu-id="76599-161">По умолчанию за раз отображается только 1000 записей.</span><span class="sxs-lookup"><span data-stu-id="76599-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Изменение временного окна](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="76599-163">Чтобы просмотреть все действия и сведения о них для определенного выполнения, выберите строку. В результате откроется страница поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="76599-163">To view all the actions and their details for a specific run, select a row, which opens the Log Search page.</span></span> 

   * <span data-ttu-id="76599-164">Чтобы просмотреть эти сведения в формате таблицы, выберите **Таблица**.</span><span class="sxs-lookup"><span data-stu-id="76599-164">To view this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="76599-165">Чтобы изменить запрос, отредактируйте строку запроса на панели поиска.</span><span class="sxs-lookup"><span data-stu-id="76599-165">To change the query, you can edit the query string in the search bar.</span></span> 
   <span data-ttu-id="76599-166">Для доступа к дополнительным функциональным возможностям выберите **Расширенная аналитика**.</span><span class="sxs-lookup"><span data-stu-id="76599-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Просмотр действий и сведений о них для выполнения приложения логики](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="76599-168">На открывшейся странице Azure Log Analytics можно обновить запросы и просмотреть результаты из таблицы.</span><span class="sxs-lookup"><span data-stu-id="76599-168">Here on the Azure Log Analytics page, you can update queries and view the results from the table.</span></span> 
     <span data-ttu-id="76599-169">В этом запросе используется [язык запросов Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), который можно изменять, если требуется просмотреть другие результаты.</span><span class="sxs-lookup"><span data-stu-id="76599-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want to view different results.</span></span> 

     ![Представление запросов в Azure Log Analytics](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="76599-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="76599-171">Next steps</span></span>

* [<span data-ttu-id="76599-172">Мониторинг сообщений B2B</span><span class="sxs-lookup"><span data-stu-id="76599-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
