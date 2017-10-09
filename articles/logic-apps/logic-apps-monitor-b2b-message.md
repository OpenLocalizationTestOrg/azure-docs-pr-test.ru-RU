---
title: "транзакции aaaMonitor B2B и настройте ведение журнала - приложения логики Azure | Документы Microsoft"
description: "Мониторинг сообщений AS2, X 12 и EDIFACT, запуск ведения журнала диагностики для учетной записи интеграции"
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
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="376da-103">Мониторинг и настройка ведения журнала диагностики для взаимодействия B2B в учетных записях интеграции</span><span class="sxs-lookup"><span data-stu-id="376da-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="376da-104">После настройки взаимодействия B2B между двумя выполняющимися бизнес-процессами или приложениями с помощью учетной записи интеграции эти сущности могут обмениваться сообщениями друг с другом.</span><span class="sxs-lookup"><span data-stu-id="376da-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="376da-105">tooconfirm это взаимодействие работает надлежащим образом, можно настроить наблюдение за AS2, X12, и сообщения EDIFACT, а также ведение журнала диагностики для вашей учетной записи интеграции через hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) службы.</span><span class="sxs-lookup"><span data-stu-id="376da-105">tooconfirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="376da-106">Эта служба в [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) отслеживает облачную и локальную среды, помогая обеспечить их доступность и производительность, а также собирает сведения о времени выполнения и событиях для отладки.</span><span class="sxs-lookup"><span data-stu-id="376da-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="376da-107">Также можно [использовать полученные диагностические данные в других службах](#extend-diagnostic-data), таких как служба хранилища Azure и концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="376da-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="376da-108">Требования</span><span class="sxs-lookup"><span data-stu-id="376da-108">Requirements</span></span>

* <span data-ttu-id="376da-109">Приложение логики, настроенное на ведение журнала диагностики.</span><span class="sxs-lookup"><span data-stu-id="376da-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="376da-110">Дополнительные сведения [как tooset ведение журнала для данного приложения логики](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="376da-110">Learn [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="376da-111">После этого требования соблюдены, должно быть рабочей hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="376da-111">After you've met this requirement, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="376da-112">Следует использовать одну рабочую область OMS hello, при настройке ведения журнала для вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="376da-112">You should use hello same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="376da-113">Если у вас нет рабочей области OMS, узнайте [как toocreate рабочей области OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="376da-113">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="376da-114">Учетная запись интеграции со связанными tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="376da-114">An integration account that's linked tooyour logic app.</span></span> <span data-ttu-id="376da-115">Дополнительные сведения [учетной записи toocreate интеграцию с приложениями логики tooyour ссылку](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="376da-115">Learn [how toocreate an integration account with a link tooyour logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="376da-116">Включение ведения журнала диагностики для учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="376da-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="376da-117">Вы можете включить ведение журнала, либо непосредственно от учетной записи интеграции или [через hello Azure мониторинг службы](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="376da-117">You can turn on logging either directly from your integration account or [through hello Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="376da-118">Служба Azure Monitor предоставляет основные функции мониторинга с помощью данных на уровне инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="376da-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="376da-119">Узнайте подробнее о службе [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="376da-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="376da-120">Включение ведения журнала диагностики в учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="376da-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="376da-121">В hello [портал Azure](https://portal.azure.com), найдите и выберите свою учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="376da-121">In hello [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="376da-122">В разделе **Мониторинг** выберите **Журналы диагностики**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="376da-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Найдите и выберите учетную запись интеграции, а затем — "Журналы диагностики"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="376da-124">После выбора учетной записи интеграции hello последующих значений будут выбраны автоматически.</span><span class="sxs-lookup"><span data-stu-id="376da-124">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="376da-125">Если эти значения верны, выберите **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="376da-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="376da-126">В противном случае выберите необходимые значения hello:</span><span class="sxs-lookup"><span data-stu-id="376da-126">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="376da-127">В разделе **подписки**, выберите hello подписки Azure, используемой с вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="376da-127">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="376da-128">В разделе **группы ресурсов**выберите hello группы ресурсов, используемой с вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="376da-128">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="376da-129">В раскрывающемся списке **Тип ресурса** выберите **Учетные записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="376da-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="376da-130">В раскрывающемся списке **Ресурс** выберите учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="376da-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="376da-131">Выберите **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="376da-131">Choose **Turn on diagnostics**.</span></span>

   ![Настройка системы диагностики для учетной записи интеграции](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="376da-133">В разделе **Параметры диагностики** > **Состояние** выберите **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="376da-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Включение системы диагностики Microsoft Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="376da-135">Теперь выберите hello OMS рабочей области и данных toouse для ведения журнала, как показано:</span><span class="sxs-lookup"><span data-stu-id="376da-135">Now select hello OMS workspace and data toouse for logging as shown:</span></span>

   1. <span data-ttu-id="376da-136">Выберите **отправки tooLog Analytics**.</span><span class="sxs-lookup"><span data-stu-id="376da-136">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="376da-137">В разделе **Log Analytics** выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="376da-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="376da-138">В разделе **рабочих областей OMS**, выберите toouse рабочей области OMS hello для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="376da-138">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="376da-139">В разделе **журнала**выберите hello **IntegrationAccountTrackingEvents** категории.</span><span class="sxs-lookup"><span data-stu-id="376da-139">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="376da-140">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="376da-140">Choose **Save**.</span></span>

   ![Настройка аналитики журналов для отправки журналов tooa данных диагностики](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="376da-142">Теперь [настройте отслеживание сообщений B2B в OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="376da-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="376da-143">Включение ведения журнала диагностики в службе Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="376da-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="376da-144">В hello [портал Azure](https://portal.azure.com), на hello главного меню Azure, выберите **монитор**, **журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="376da-144">In hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="376da-145">Затем выберите учетную запись интеграции, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="376da-145">Then select your integration account as shown here:</span></span>

   ![Выберите "Мониторинг", "Журналы диагностики", выберите свою учетную запись интеграции](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="376da-147">После выбора учетной записи интеграции hello последующих значений будут выбраны автоматически.</span><span class="sxs-lookup"><span data-stu-id="376da-147">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="376da-148">Если эти значения верны, выберите **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="376da-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="376da-149">В противном случае выберите необходимые значения hello:</span><span class="sxs-lookup"><span data-stu-id="376da-149">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="376da-150">В разделе **подписки**, выберите hello подписки Azure, используемой с вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="376da-150">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="376da-151">В разделе **группы ресурсов**выберите hello группы ресурсов, используемой с вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="376da-151">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="376da-152">В раскрывающемся списке **Тип ресурса** выберите **Учетные записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="376da-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="376da-153">В раскрывающемся списке **Ресурс** выберите учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="376da-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="376da-154">Выберите **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="376da-154">Choose **Turn on diagnostics**.</span></span>

   ![Настройка системы диагностики для учетной записи интеграции](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="376da-156">В разделе **Параметры диагностики** выберите **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="376da-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Включение системы диагностики Microsoft Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="376da-158">Теперь выберите hello OMS рабочей области и категории событий для ведения журнала, как показано:</span><span class="sxs-lookup"><span data-stu-id="376da-158">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="376da-159">Выберите **отправки tooLog Analytics**.</span><span class="sxs-lookup"><span data-stu-id="376da-159">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="376da-160">В разделе **Log Analytics** выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="376da-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="376da-161">В разделе **рабочих областей OMS**, выберите toouse рабочей области OMS hello для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="376da-161">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="376da-162">В разделе **журнала**выберите hello **IntegrationAccountTrackingEvents** категории.</span><span class="sxs-lookup"><span data-stu-id="376da-162">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="376da-163">Когда все будет готово, нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="376da-163">When you're done, choose **Save**.</span></span>

   ![Настройка аналитики журналов для отправки журналов tooa данных диагностики](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="376da-165">Теперь [настройте отслеживание сообщений B2B в OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="376da-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="376da-166">Расширение возможностей использования диагностических данных в других службах</span><span class="sxs-lookup"><span data-stu-id="376da-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="376da-167">Помимо Azure Log Analytics, можно расширить возможности использования диагностических данных приложения логики в других службах Azure, например:</span><span class="sxs-lookup"><span data-stu-id="376da-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="376da-168">Архивация журналов диагностики Azure в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="376da-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="376da-169">Журналы диагностики Azure поток tooAzure концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="376da-169">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="376da-170">После этого можно организовать мониторинг в режиме реального времени с помощью данных телеметрии и аналитики из других служб, таких как [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) и [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="376da-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="376da-171">Например:</span><span class="sxs-lookup"><span data-stu-id="376da-171">For example:</span></span>

* [<span data-ttu-id="376da-172">Поток данных из концентраторов событий tooStream аналитика</span><span class="sxs-lookup"><span data-stu-id="376da-172">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="376da-173">Анализ потоковой передачи данных с помощью Stream Analytics и создание панели мониторинга в Power BI для анализа данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="376da-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="376da-174">На основании hello параметры настройки, убедитесь, что вы первый [создать учетную запись хранилища Azure](../storage/common/storage-create-storage-account.md) или [создать концентратор событий Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="376da-174">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="376da-175">Затем выберите параметры hello место toosend диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="376da-175">Then select hello options for where you want toosend diagnostic data:</span></span>

![Отправка данных tooAzure хранилища учетной записи или события концентратора](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="376da-177">Сроки хранения применяются только в том случае, при выборе toouse учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="376da-177">Retention periods apply only when you choose toouse a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="376da-178">Поддерживаемые схемы отслеживания</span><span class="sxs-lookup"><span data-stu-id="376da-178">Supported tracking schemas</span></span>

<span data-ttu-id="376da-179">Azure поддерживает эти типы схемы, которые имеют фиксированное схемы, за исключением hello пользовательский тип отслеживания.</span><span class="sxs-lookup"><span data-stu-id="376da-179">Azure supports these tracking schema types, which all have fixed schemas except hello Custom type.</span></span>

* [<span data-ttu-id="376da-180">Схема отслеживания AS2</span><span class="sxs-lookup"><span data-stu-id="376da-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="376da-181">Схема отслеживания X12</span><span class="sxs-lookup"><span data-stu-id="376da-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="376da-182">Настраиваемая схема отслеживания</span><span class="sxs-lookup"><span data-stu-id="376da-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="376da-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="376da-183">Next steps</span></span>

* [<span data-ttu-id="376da-184">Отслеживание сообщений B2B в OMS</span><span class="sxs-lookup"><span data-stu-id="376da-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Отслеживание сообщений B2B в OMS")
* [<span data-ttu-id="376da-185">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="376da-185">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")

