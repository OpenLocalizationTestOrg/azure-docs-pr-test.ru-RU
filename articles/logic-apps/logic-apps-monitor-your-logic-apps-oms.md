---
title: "aaaMonitor и получения ценной информации о приложении логики выполняется с помощью OMS - приложения логики Azure | Документы Microsoft"
description: "Мониторинг работы логики приложения с мнениями tooget анализа журналов и Operations Management Suite (OMS) и более полных сведений отладки для диагностики и устранения неполадок"
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
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="9bb37-103">Мониторинг выполнения приложений логики и получение аналитических сведений о них с помощью Operations Management Suite (OMS) и Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9bb37-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="9bb37-104">Для мониторинга и расширенные сведения по отладке, можно включить аналитики журналов в hello одновременно при создании приложения логики.</span><span class="sxs-lookup"><span data-stu-id="9bb37-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="9bb37-105">Предоставляет службы анализа журналов диагностики, ведение журнала и мониторинг для логики приложения выполняется через портал Operations Management Suite (OMS) hello.</span><span class="sxs-lookup"><span data-stu-id="9bb37-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="9bb37-106">При добавлении tooOMS решение управления логику приложения hello, вы получаете обобщенное состояние для вашей запусков логику приложения и конкретные сведения, как состояние, время выполнения, состояние повторной передачи и идентификаторы корреляции.</span><span class="sxs-lookup"><span data-stu-id="9bb37-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="9bb37-107">В этом разделе показано, как tooturn для анализа журналов или установите hello решения по управлению приложениями логики в OMS можно просматривать события среды выполнения и запуска данных логики приложения.</span><span class="sxs-lookup"><span data-stu-id="9bb37-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="9bb37-108">toomonitor существующие логики приложения, выполните следующие действия слишком [включить ведение журнала диагностики и отправка логики приложения среды выполнения данных tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="9bb37-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="9bb37-109">Требования</span><span class="sxs-lookup"><span data-stu-id="9bb37-109">Requirements</span></span>

<span data-ttu-id="9bb37-110">Прежде чем начать, необходимо toohave рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="9bb37-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="9bb37-111">Дополнительные сведения [как toocreate рабочей области OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9bb37-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="9bb37-112">Включение ведения журнала диагностики при создании приложений логики</span><span class="sxs-lookup"><span data-stu-id="9bb37-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="9bb37-113">На [портале Azure](https://portal.azure.com) создайте приложение логики.</span><span class="sxs-lookup"><span data-stu-id="9bb37-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="9bb37-114">Выберите **Создать** > **Интеграция Enterprise** > **Приложение логики** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bb37-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Создайте приложение логики](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="9bb37-116">В hello **создать логику приложение** выполните следующие задачи, как показано:</span><span class="sxs-lookup"><span data-stu-id="9bb37-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="9bb37-117">Введите имя приложения логики и выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="9bb37-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="9bb37-118">Создайте или выберите существующую группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="9bb37-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="9bb37-119">Задать **анализа журналов** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="9bb37-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="9bb37-120">Рабочая область OMS выберите hello место слишком отправки данных для логики приложения выполняется.</span><span class="sxs-lookup"><span data-stu-id="9bb37-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="9bb37-121">Когда вы будете готовы, нажмите кнопку **toodashboard ПИН-код** > **создать**.</span><span class="sxs-lookup"><span data-stu-id="9bb37-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![Создание приложения логики](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="9bb37-123">По завершении этого шага Azure создает приложение логики, которое теперь связано с рабочей областью OMS.</span><span class="sxs-lookup"><span data-stu-id="9bb37-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="9bb37-124">Кроме того этот шаг также автоматически устанавливает решение по управлению приложениями логики hello в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="9bb37-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="9bb37-125">логика приложения выполняется в OMS, tooview [выполните следующие действия](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="9bb37-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="9bb37-126">Установка решения управления логику приложения hello в OMS</span><span class="sxs-lookup"><span data-stu-id="9bb37-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="9bb37-127">Если вы уже включили Log Analytics при создании приложения логики, то пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="9bb37-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="9bb37-128">Уже имеется решение управления логику приложения hello в OMS.</span><span class="sxs-lookup"><span data-stu-id="9bb37-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="9bb37-129">В hello [портал Azure](https://portal.azure.com), выберите **более служб**.</span><span class="sxs-lookup"><span data-stu-id="9bb37-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="9bb37-130">В поле поиска введите словосочетание "log analytics" в качестве фильтра и выберите **Log Analytics**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9bb37-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Выберите "Log Analytics"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="9bb37-132">В разделе **Log Analytics** найдите и выберите рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="9bb37-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Выбор рабочей области OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="9bb37-134">В разделе **Управление** выберите **Портал OMS**.</span><span class="sxs-lookup"><span data-stu-id="9bb37-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Выберите "Портал OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="9bb37-136">На главной странице OMS Если отображается баннер обновления hello, нажмите баннер hello, чтобы сначала обновить рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="9bb37-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="9bb37-137">Затем выберите **Коллекция решений**.</span><span class="sxs-lookup"><span data-stu-id="9bb37-137">Then choose **Solutions Gallery**.</span></span>

   ![Выбор "Коллекции решений"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="9bb37-139">В разделе **все решения**, найдите и выберите плитку hello для hello **управления приложениями логики** решения.</span><span class="sxs-lookup"><span data-stu-id="9bb37-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![Выбор Logic Apps Management](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="9bb37-141">Выберите решение tooinstall hello в рабочую область OMS **добавить**.</span><span class="sxs-lookup"><span data-stu-id="9bb37-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![Кнопка "Добавить" для Logic Apps Management](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="9bb37-143">Просмотр сведений о выполнении приложений логики в рабочей области OMS</span><span class="sxs-lookup"><span data-stu-id="9bb37-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="9bb37-144">число tooview hello и состояние для логики приложения выполняется, последовательно выберите toohello страница обзора для рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="9bb37-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="9bb37-145">Просмотрите сведения об hello на hello **управления приложениями логики** плитки.</span><span class="sxs-lookup"><span data-stu-id="9bb37-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![Элемент обзора, показывающий количество и состояние выполнений приложений логики](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="9bb37-147">Если это обновление баннера отображается вместо плитки управления логику приложения hello, выберите баннер hello, чтобы сначала обновить рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="9bb37-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Обновление рабочей области OMS](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="9bb37-149">tooview Сводка более подробные данные о работы логики приложения выберите hello **управления приложениями логики** плитки.</span><span class="sxs-lookup"><span data-stu-id="9bb37-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="9bb37-150">Здесь сведения о выполнении приложений логики группируются по имени или по состоянию выполнения.</span><span class="sxs-lookup"><span data-stu-id="9bb37-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Сводные данные о состоянии выполнения приложений логики](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="9bb37-152">tooview, все hello выполняется для логики, специфичной для приложения или состояние, выберите hello строку приложения логики или состояние.</span><span class="sxs-lookup"><span data-stu-id="9bb37-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="9bb37-153">Ниже приведен пример, в котором показаны все фрагменты hello для логики, специфичной для приложения:</span><span class="sxs-lookup"><span data-stu-id="9bb37-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![Просмотр сведений о выполнении по приложению логики или по состоянию](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="9bb37-155">Hello **повторной передачи** столбце отображается «Да» для выполнения, возникающие в результате повторно отправлено выполнения.</span><span class="sxs-lookup"><span data-stu-id="9bb37-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="9bb37-156">toofilter эти результаты, можно выполнить фильтрацию клиентские и серверные.</span><span class="sxs-lookup"><span data-stu-id="9bb37-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="9bb37-157">Клиентский фильтр: для каждого столбца выберите hello фильтры, которые нужно.</span><span class="sxs-lookup"><span data-stu-id="9bb37-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="9bb37-158">Ниже приведены некоторые примеры:</span><span class="sxs-lookup"><span data-stu-id="9bb37-158">Here are some examples:</span></span>

     ![Пример фильтров столбцов](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="9bb37-160">Серверный фильтр: toochoose число запусков, которые отображаются, используйте элемент управления области hello вверху hello страницы приветствия определенное время окна или toolimit hello.</span><span class="sxs-lookup"><span data-stu-id="9bb37-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="9bb37-161">По умолчанию за раз отображается только 1000 записей.</span><span class="sxs-lookup"><span data-stu-id="9bb37-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Период времени изменения hello](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="9bb37-163">все tooview hello действия и сведения о них конкретного выполнения, выберите строку, откроется страница поиска журналов hello.</span><span class="sxs-lookup"><span data-stu-id="9bb37-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="9bb37-164">tooview эти сведения в таблице, выберите **таблицы**.</span><span class="sxs-lookup"><span data-stu-id="9bb37-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="9bb37-165">запрос toochange hello, можно изменить строку запроса hello в строке поиска hello.</span><span class="sxs-lookup"><span data-stu-id="9bb37-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="9bb37-166">Для доступа к дополнительным функциональным возможностям выберите **Расширенная аналитика**.</span><span class="sxs-lookup"><span data-stu-id="9bb37-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Просмотр действий и сведений о них для выполнения приложения логики](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="9bb37-168">Здесь на странице приветствия анализа журналов Azure, можно обновить запросы и представления hello результаты из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="9bb37-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="9bb37-169">В этом запросе используется [язык запросов Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), его можно изменить, если требуется tooview различные результаты.</span><span class="sxs-lookup"><span data-stu-id="9bb37-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Представление запросов в Azure Log Analytics](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="9bb37-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9bb37-171">Next steps</span></span>

* [<span data-ttu-id="9bb37-172">Мониторинг сообщений B2B</span><span class="sxs-lookup"><span data-stu-id="9bb37-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
