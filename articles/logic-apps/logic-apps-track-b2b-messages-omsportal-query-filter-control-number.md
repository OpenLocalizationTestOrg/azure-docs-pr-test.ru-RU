---
title: "Запрос сообщений B2B с помощью Operations Management Suite в Azure Logic Apps | Документы Майкрософт"
description: "Отслеживание сообщений AS2, X12 и EDIFACT на портале Operations Management Suite с помощью запросов"
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
ms.openlocfilehash: 2748d3d3daf7c13dca05f663a4a088598e1b3605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-the-microsoft-operations-management-suite-oms"></a><span data-ttu-id="25fbb-103">Запрос сообщений AS2, X 12 и EDIFACT в Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="25fbb-103">Query for AS2, X12, and EDIFACT messages in the Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="25fbb-104">Чтобы найти сообщения AS2, X12 или EDIFACT, которые отслеживаются с помощью [Azure Log Analytics](../log-analytics/log-analytics-overview.md) в [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), можно создавать запросы, применяющие фильтры к действиям на основе заданных критериев.</span><span class="sxs-lookup"><span data-stu-id="25fbb-104">To find the AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="25fbb-105">Например, можно найти сообщения с определенным контрольным номером обмена.</span><span class="sxs-lookup"><span data-stu-id="25fbb-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="25fbb-106">Требования</span><span class="sxs-lookup"><span data-stu-id="25fbb-106">Requirements</span></span>

* <span data-ttu-id="25fbb-107">Приложение логики, настроенное на ведение журнала диагностики.</span><span class="sxs-lookup"><span data-stu-id="25fbb-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="25fbb-108">Узнайте подробнее о [создании приложения логики](../logic-apps/logic-apps-create-a-logic-app.md) и [настройке ведения журнала для такого приложения логики](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="25fbb-108">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="25fbb-109">Учетная запись интеграции, настроенная для мониторинга и ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="25fbb-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="25fbb-110">Узнайте подробнее о [создании учетной записи интеграции](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) и [настройке мониторинга и ведения журнала для этой учетной записи](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="25fbb-110">Learn [how to create an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how to set up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="25fbb-111">Если это еще не сделано, [опубликуйте диагностические данные в службе Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) и [настройте отслеживание сообщений в OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="25fbb-111">If you haven't already, [publish diagnostic data to Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="25fbb-112">Помимо соблюдения всех указанных выше требований, у вас должна иметься рабочая область в [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25fbb-112">After you've met the previous requirements, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="25fbb-113">Для отслеживания взаимодействия B2B в OMS следует использовать одну и ту же рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="25fbb-113">You should use the same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="25fbb-114">Если у вас нет рабочей области OMS, узнайте о том, [как ее создать](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="25fbb-114">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-the-operations-management-suite-portal"></a><span data-ttu-id="25fbb-115">Создание запросов сообщений с фильтрами на портале Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="25fbb-115">Create message queries with filters in the Operations Management Suite portal</span></span>

<span data-ttu-id="25fbb-116">В этом примере показано, как найти сообщение по контрольному номеру обмена.</span><span class="sxs-lookup"><span data-stu-id="25fbb-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="25fbb-117">Если известно имя рабочей области OMS, перейдите на домашнюю страницу рабочей области (`https://{your-workspace-name}.portal.mms.microsoft.com`) и перейдите к шагу 4.</span><span class="sxs-lookup"><span data-stu-id="25fbb-117">If you know your OMS workspace name, go to your workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="25fbb-118">В противном случае начните с шага 1.</span><span class="sxs-lookup"><span data-stu-id="25fbb-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="25fbb-119">На [портале Azure](https://portal.azure.com) щелкните **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-119">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="25fbb-120">Введите в поле поиска "log analytics" и выберите **Log Analytics**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="25fbb-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Поиск Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="25fbb-122">В разделе **Log Analytics** найдите и выберите рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="25fbb-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Выбор рабочей области OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="25fbb-124">В разделе **Управление** выберите **Портал OMS**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Выбор портала OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="25fbb-126">На домашней странице OMS выберите **Поиск по журналам**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-126">On your OMS home page, choose **Log Search**.</span></span>

   ![На домашней странице OMS выберите "Поиск по журналам"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="25fbb-128">-или-</span><span class="sxs-lookup"><span data-stu-id="25fbb-128">-or-</span></span>

   ![В меню OMS выберите "Поиск по журналам"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="25fbb-130">В поле поиска введите поле, которое требуется найти, и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-130">In the search box, enter a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="25fbb-131">При вводе OMS предлагает возможные совпадения и операции, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="25fbb-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="25fbb-132">Узнайте подробнее о [способах поиска данных в Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="25fbb-132">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="25fbb-133">В этом примере выполняется поиск событий с параметром **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Начните вводить строку запроса](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="25fbb-135">На панели слева выберите период времени, данные за который вы хотите просмотреть.</span><span class="sxs-lookup"><span data-stu-id="25fbb-135">In the left bar, choose the timeframe that you want to view.</span></span> <span data-ttu-id="25fbb-136">Чтобы добавить фильтр к запросу, нажмите **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-136">To add a filter to your query, choose **+Add**.</span></span>

   ![Добавление фильтра к запросу](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="25fbb-138">В разделе **Добавить фильтры** введите имя фильтра, чтобы найти нужный фильтр.</span><span class="sxs-lookup"><span data-stu-id="25fbb-138">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="25fbb-139">Выберите фильтр и нажмите **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-139">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="25fbb-140">Чтобы найти контрольный номер обмена, в этом примере выполняется поиск по слову "interchange", а в качестве фильтра выбирается параметр **event_record_messageProperties_interchangeControlNumber_s**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-140">To find the interchange control number, this example searches for the word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as the filter.</span></span>

   ![Выбор фильтра](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="25fbb-142">На панели слева выберите значение фильтра, которое требуется использовать, а затем нажмите **Применить**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-142">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   <span data-ttu-id="25fbb-143">В этом примере выбирается контрольный номер обмена для требуемых сообщений.</span><span class="sxs-lookup"><span data-stu-id="25fbb-143">This example selects the interchange control number for the messages we want.</span></span>

   ![Выбор значения фильтра](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="25fbb-145">Теперь вернитесь к запросу, который вы создаете.</span><span class="sxs-lookup"><span data-stu-id="25fbb-145">Now return to the query that you're building.</span></span> <span data-ttu-id="25fbb-146">Запрос был обновлен с учетом выбранных фильтра событий и значения.</span><span class="sxs-lookup"><span data-stu-id="25fbb-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="25fbb-147">Предыдущие результаты теперь также отфильтрованы.</span><span class="sxs-lookup"><span data-stu-id="25fbb-147">Your previous results are now filtered too.</span></span>

    ![Возврат к запросу с отфильтрованными результатами](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="25fbb-149">Сохранение запроса для использования в будущем</span><span class="sxs-lookup"><span data-stu-id="25fbb-149">Save your query for future use</span></span>

1. <span data-ttu-id="25fbb-150">В запросе на странице **Поиск по журналам** нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-150">From your query on the **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="25fbb-151">Присвойте запросу имя, выберите категорию и нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Присвойте запросу имя и категорию](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="25fbb-153">Чтобы просмотреть запрос, выберите **Избранное**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-153">To view your query, choose **Favorites**.</span></span>

   ![Выберите "Избранное"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="25fbb-155">В разделе **Сохраненные условия поиска** выберите запрос, чтобы просмотреть его результаты.</span><span class="sxs-lookup"><span data-stu-id="25fbb-155">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="25fbb-156">Чтобы обновить запрос и найти другие результаты, измените запрос.</span><span class="sxs-lookup"><span data-stu-id="25fbb-156">To update the query so you can find different results, edit the query.</span></span>

   ![Выбор запроса](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-the-operations-management-suite-portal"></a><span data-ttu-id="25fbb-158">Поиск и запуск сохраненных запросов на портале Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="25fbb-158">Find and run saved queries in the Operations Management Suite portal</span></span>

1. <span data-ttu-id="25fbb-159">Откройте домашнюю страницу рабочей области OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) и выберите **Поиск по журналам**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![На домашней странице OMS выберите "Поиск по журналам"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="25fbb-161">-или-</span><span class="sxs-lookup"><span data-stu-id="25fbb-161">-or-</span></span>

   ![В меню OMS выберите "Поиск по журналам"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="25fbb-163">На домашней странице **Поиск по журналам** выберите **Избранное**.</span><span class="sxs-lookup"><span data-stu-id="25fbb-163">On the **Log Search** home page, choose **Favorites**.</span></span>

   ![Выберите "Избранное"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="25fbb-165">В разделе **Сохраненные условия поиска** выберите запрос, чтобы просмотреть его результаты.</span><span class="sxs-lookup"><span data-stu-id="25fbb-165">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="25fbb-166">Чтобы обновить запрос и найти другие результаты, измените запрос.</span><span class="sxs-lookup"><span data-stu-id="25fbb-166">To update the query so you can find different results, edit the query.</span></span>

   ![Выбор запроса](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="25fbb-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25fbb-168">Next steps</span></span>

* [<span data-ttu-id="25fbb-169">Схемы отслеживания AS2</span><span class="sxs-lookup"><span data-stu-id="25fbb-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="25fbb-170">Схемы отслеживания X12</span><span class="sxs-lookup"><span data-stu-id="25fbb-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="25fbb-171">Настраиваемые схемы отслеживания</span><span class="sxs-lookup"><span data-stu-id="25fbb-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)