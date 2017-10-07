---
title: "aaaQuery B2B сообщений в Operations Management Suite - приложения логики Azure | Документы Microsoft"
description: "Создание запросов tootrack AS2, X 12 и EDIFACT сообщений в hello Operations Management Suite"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="df96c-103">Запрос для AS2, X 12 и EDIFACT сообщений hello Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="df96c-103">Query for AS2, X12, and EDIFACT messages in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="df96c-104">hello toofind AS2, X 12 и EDIFACT сообщений, которые отслеживаются с [Azure Log Analytics](../log-analytics/log-analytics-overview.md) в hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), можно создавать запросы, которые фильтруют действия в зависимости от конкретных критерии.</span><span class="sxs-lookup"><span data-stu-id="df96c-104">toofind hello AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="df96c-105">Например, можно найти сообщения с определенным контрольным номером обмена.</span><span class="sxs-lookup"><span data-stu-id="df96c-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="df96c-106">Требования</span><span class="sxs-lookup"><span data-stu-id="df96c-106">Requirements</span></span>

* <span data-ttu-id="df96c-107">Приложение логики, настроенное на ведение журнала диагностики.</span><span class="sxs-lookup"><span data-stu-id="df96c-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="df96c-108">Дополнительные сведения [как toocreate приложения логики](../logic-apps/logic-apps-create-a-logic-app.md) и [как tooset ведение журнала для данного приложения логики](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="df96c-108">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="df96c-109">Учетная запись интеграции, настроенная для мониторинга и ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="df96c-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="df96c-110">Дополнительные сведения [как toocreate учетной записи интеграции](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) и [как tooset мониторинга и ведения журнала для этой учетной записи](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="df96c-110">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="df96c-111">Если это еще не сделано, [публикации tooLog диагностических данных аналитики](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) и [Настройка отслеживания в OMS сообщений](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="df96c-111">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="df96c-112">После hello предыдущих требования соблюдены, должно быть рабочей hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="df96c-112">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="df96c-113">Следует использовать одну рабочую область OMS для отслеживания B2B связи в OMS hello.</span><span class="sxs-lookup"><span data-stu-id="df96c-113">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="df96c-114">Если у вас нет рабочей области OMS, узнайте [как toocreate рабочей области OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="df96c-114">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a><span data-ttu-id="df96c-115">Создание запросов сообщений с фильтрами в портал Operations Management Suite hello</span><span class="sxs-lookup"><span data-stu-id="df96c-115">Create message queries with filters in hello Operations Management Suite portal</span></span>

<span data-ttu-id="df96c-116">В этом примере показано, как найти сообщение по контрольному номеру обмена.</span><span class="sxs-lookup"><span data-stu-id="df96c-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="df96c-117">Если известно имя рабочей области OMS, перейдите Домашняя страница рабочей области tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) и запустить на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="df96c-117">If you know your OMS workspace name, go tooyour workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="df96c-118">В противном случае начните с шага 1.</span><span class="sxs-lookup"><span data-stu-id="df96c-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="df96c-119">В hello [портал Azure](https://portal.azure.com), выберите **более служб**.</span><span class="sxs-lookup"><span data-stu-id="df96c-119">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="df96c-120">Введите в поле поиска "log analytics" и выберите **Log Analytics**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="df96c-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Поиск Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="df96c-122">В разделе **Log Analytics** найдите и выберите рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="df96c-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Выбор рабочей области OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="df96c-124">В разделе **Управление** выберите **Портал OMS**.</span><span class="sxs-lookup"><span data-stu-id="df96c-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Выбор портала OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="df96c-126">На домашней странице OMS выберите **Поиск по журналам**.</span><span class="sxs-lookup"><span data-stu-id="df96c-126">On your OMS home page, choose **Log Search**.</span></span>

   ![На домашней странице OMS выберите "Поиск по журналам"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="df96c-128">-или-</span><span class="sxs-lookup"><span data-stu-id="df96c-128">-or-</span></span>

   ![Hello OMS выберите пункт меню «Поиск журналов»](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="df96c-130">Введите в поле поиска hello, поля, которые должны toofind и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="df96c-130">In hello search box, enter a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="df96c-131">При вводе OMS предлагает возможные совпадения и операции, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="df96c-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="df96c-132">Дополнительные сведения о [как toofind данных в службе анализа журналов](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="df96c-132">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="df96c-133">В этом примере выполняется поиск событий с параметром **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="df96c-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Начните вводить строку запроса](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="df96c-135">В левой панели hello, выберите период hello, которые должны tooview.</span><span class="sxs-lookup"><span data-stu-id="df96c-135">In hello left bar, choose hello timeframe that you want tooview.</span></span> <span data-ttu-id="df96c-136">Выберите tooadd tooyour запрос фильтра **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="df96c-136">tooadd a filter tooyour query, choose **+Add**.</span></span>

   ![Добавить фильтр tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="df96c-138">В разделе **добавить фильтры**, введите имя фильтра hello, чтобы найти нужный фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="df96c-138">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="df96c-139">Выберите фильтр hello и выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="df96c-139">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="df96c-140">toofind hello контрольного числа, в этом примере ищет слово hello «сообщения» и выбирает **event_record_messageProperties_interchangeControlNumber_s** как фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="df96c-140">toofind hello interchange control number, this example searches for hello word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as hello filter.</span></span>

   ![Выбор фильтра](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="df96c-142">Hello левой панели выберите значение фильтра hello, toouse и задайте **применить**.</span><span class="sxs-lookup"><span data-stu-id="df96c-142">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   <span data-ttu-id="df96c-143">В этом примере выбирает hello контрольное число сообщения hello нужным нам.</span><span class="sxs-lookup"><span data-stu-id="df96c-143">This example selects hello interchange control number for hello messages we want.</span></span>

   ![Выбор значения фильтра](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="df96c-145">Теперь возвращают toohello запрос, для которого выполняется сборка.</span><span class="sxs-lookup"><span data-stu-id="df96c-145">Now return toohello query that you're building.</span></span> <span data-ttu-id="df96c-146">Запрос был обновлен с учетом выбранных фильтра событий и значения.</span><span class="sxs-lookup"><span data-stu-id="df96c-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="df96c-147">Предыдущие результаты теперь также отфильтрованы.</span><span class="sxs-lookup"><span data-stu-id="df96c-147">Your previous results are now filtered too.</span></span>

    ![Возвращает запрос tooyour с отфильтрованные результаты](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="df96c-149">Сохранение запроса для использования в будущем</span><span class="sxs-lookup"><span data-stu-id="df96c-149">Save your query for future use</span></span>

1. <span data-ttu-id="df96c-150">Из запроса на hello **поиска журналов** выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df96c-150">From your query on hello **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="df96c-151">Присвойте запросу имя, выберите категорию и нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df96c-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Присвойте запросу имя и категорию](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="df96c-153">tooview ваш запрос, выберите **Избранное**.</span><span class="sxs-lookup"><span data-stu-id="df96c-153">tooview your query, choose **Favorites**.</span></span>

   ![Выберите "Избранное"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="df96c-155">В разделе **сохраненные поиски**, выберите запрос, можно просмотреть результаты hello.</span><span class="sxs-lookup"><span data-stu-id="df96c-155">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="df96c-156">запрос hello редактировать tooupdate hello запрос, чтобы найти другие результаты.</span><span class="sxs-lookup"><span data-stu-id="df96c-156">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Выбор запроса](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a><span data-ttu-id="df96c-158">Найдите и запустите сохраненные запросы в портал Operations Management Suite hello</span><span class="sxs-lookup"><span data-stu-id="df96c-158">Find and run saved queries in hello Operations Management Suite portal</span></span>

1. <span data-ttu-id="df96c-159">Откройте домашнюю страницу рабочей области OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) и выберите **Поиск по журналам**.</span><span class="sxs-lookup"><span data-stu-id="df96c-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![На домашней странице OMS выберите "Поиск по журналам"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="df96c-161">-или-</span><span class="sxs-lookup"><span data-stu-id="df96c-161">-or-</span></span>

   ![Hello OMS выберите пункт меню «Поиск журналов»](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="df96c-163">На hello **поиска журналов** домашнюю страницу, выберите **Избранное**.</span><span class="sxs-lookup"><span data-stu-id="df96c-163">On hello **Log Search** home page, choose **Favorites**.</span></span>

   ![Выберите "Избранное"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="df96c-165">В разделе **сохраненные поиски**, выберите запрос, можно просмотреть результаты hello.</span><span class="sxs-lookup"><span data-stu-id="df96c-165">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="df96c-166">запрос hello редактировать tooupdate hello запрос, чтобы найти другие результаты.</span><span class="sxs-lookup"><span data-stu-id="df96c-166">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Выбор запроса](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="df96c-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df96c-168">Next steps</span></span>

* [<span data-ttu-id="df96c-169">Схемы отслеживания AS2</span><span class="sxs-lookup"><span data-stu-id="df96c-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="df96c-170">Схемы отслеживания X12</span><span class="sxs-lookup"><span data-stu-id="df96c-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="df96c-171">Настраиваемые схемы отслеживания</span><span class="sxs-lookup"><span data-stu-id="df96c-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)