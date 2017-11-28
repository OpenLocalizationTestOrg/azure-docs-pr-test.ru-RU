---
title: "Отслеживание транзакций B2B и настройка ведения журнала с помощью Azure Logic Apps | Документы Майкрософт"
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
ms.openlocfilehash: f717dae9a70a96944b623f22b90cf8c5a943f382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="1ff7c-103">Мониторинг и настройка ведения журнала диагностики для взаимодействия B2B в учетных записях интеграции</span><span class="sxs-lookup"><span data-stu-id="1ff7c-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="1ff7c-104">После настройки взаимодействия B2B между двумя выполняющимися бизнес-процессами или приложениями с помощью учетной записи интеграции эти сущности могут обмениваться сообщениями друг с другом.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="1ff7c-105">Чтобы убедиться в том, что это взаимодействие осуществляется должным образом, можно настроить мониторинг сообщений AS2, X12 и EDIFACT, а также ведение журналов диагностики для учетной записи интеграции с помощью службы [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-105">To confirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through the [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="1ff7c-106">Эта служба в [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) отслеживает облачную и локальную среды, помогая обеспечить их доступность и производительность, а также собирает сведения о времени выполнения и событиях для отладки.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="1ff7c-107">Также можно [использовать полученные диагностические данные в других службах](#extend-diagnostic-data), таких как служба хранилища Azure и концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="1ff7c-108">Требования</span><span class="sxs-lookup"><span data-stu-id="1ff7c-108">Requirements</span></span>

* <span data-ttu-id="1ff7c-109">Приложение логики, настроенное на ведение журнала диагностики.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="1ff7c-110">Узнайте о том, [как настроить ведение журнала для этого приложения логики](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-110">Learn [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="1ff7c-111">Помимо соблюдения этого требования, у вас должна иметься рабочая область в [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-111">After you've met this requirement, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="1ff7c-112">При настройке ведения журнала для своей учетной записи интеграции следует использовать одну и ту же рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-112">You should use the same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="1ff7c-113">Если у вас нет рабочей области OMS, узнайте о том, [как ее создать](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-113">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="1ff7c-114">Учетная запись интеграции, связанная с приложением логики.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-114">An integration account that's linked to your logic app.</span></span> <span data-ttu-id="1ff7c-115">Узнайте, [как создать учетную запись интеграции и связать ее с приложениями логики](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-115">Learn [how to create an integration account with a link to your logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="1ff7c-116">Включение ведения журнала диагностики для учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="1ff7c-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="1ff7c-117">Вы можете включить ведение журнала либо непосредственно в учетной записи интеграции, либо в [службе Azure Monitor](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-117">You can turn on logging either directly from your integration account or [through the Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="1ff7c-118">Служба Azure Monitor предоставляет основные функции мониторинга с помощью данных на уровне инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="1ff7c-119">Узнайте подробнее о службе [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="1ff7c-120">Включение ведения журнала диагностики в учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="1ff7c-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="1ff7c-121">На [портале Azure](https://portal.azure.com) найдите и выберите свою учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-121">In the [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="1ff7c-122">В разделе **Мониторинг** выберите **Журналы диагностики**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Найдите и выберите учетную запись интеграции, а затем — "Журналы диагностики"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="1ff7c-124">После выбора учетной записи интеграции автоматически выбираются следующие значения.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-124">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="1ff7c-125">Если эти значения верны, выберите **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="1ff7c-126">В противном случае выберите необходимые значения.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-126">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="1ff7c-127">В поле **Подписка** выберите подписку Azure, которую хотите использовать для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-127">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="1ff7c-128">В поле **Группа ресурсов** выберите группу ресурсов, которую хотите использовать для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-128">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="1ff7c-129">В раскрывающемся списке **Тип ресурса** выберите **Учетные записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="1ff7c-130">В раскрывающемся списке **Ресурс** выберите учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="1ff7c-131">Выберите **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-131">Choose **Turn on diagnostics**.</span></span>

   ![Настройка системы диагностики для учетной записи интеграции](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="1ff7c-133">В разделе **Параметры диагностики** > **Состояние** выберите **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Включение системы диагностики Microsoft Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="1ff7c-135">Теперь выберите рабочую область OMS и данные, которые необходимо использовать для ведения журнала, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="1ff7c-135">Now select the OMS workspace and data to use for logging as shown:</span></span>

   1. <span data-ttu-id="1ff7c-136">Установите флажок **Отправить в Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-136">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="1ff7c-137">В разделе **Log Analytics** выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="1ff7c-138">В разделе **Рабочие области OMS** выберите рабочую область OMS для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-138">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="1ff7c-139">В разделе **Журнал** выберите категорию **IntegrationAccountTrackingEvents**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-139">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="1ff7c-140">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-140">Choose **Save**.</span></span>

   ![Настройка Log Analytics для отправки диагностических данных в журнал](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="1ff7c-142">Теперь [настройте отслеживание сообщений B2B в OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="1ff7c-143">Включение ведения журнала диагностики в службе Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="1ff7c-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="1ff7c-144">На [портале Azure](https://portal.azure.com) в главном меню Azure выберите **Мониторинг**, **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-144">In the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="1ff7c-145">Затем выберите учетную запись интеграции, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="1ff7c-145">Then select your integration account as shown here:</span></span>

   ![Выберите "Мониторинг", "Журналы диагностики", выберите свою учетную запись интеграции](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="1ff7c-147">После выбора учетной записи интеграции автоматически выбираются следующие значения.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-147">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="1ff7c-148">Если эти значения верны, выберите **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="1ff7c-149">В противном случае выберите необходимые значения.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-149">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="1ff7c-150">В поле **Подписка** выберите подписку Azure, которую хотите использовать для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-150">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="1ff7c-151">В поле **Группа ресурсов** выберите группу ресурсов, которую хотите использовать для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-151">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="1ff7c-152">В раскрывающемся списке **Тип ресурса** выберите **Учетные записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="1ff7c-153">В раскрывающемся списке **Ресурс** выберите учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="1ff7c-154">Выберите **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-154">Choose **Turn on diagnostics**.</span></span>

   ![Настройка системы диагностики для учетной записи интеграции](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="1ff7c-156">В разделе **Параметры диагностики** выберите **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Включение системы диагностики Microsoft Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="1ff7c-158">Теперь выберите рабочую область OMS и категорию событий, которые необходимо использовать для ведения журнала, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="1ff7c-158">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="1ff7c-159">Установите флажок **Отправить в Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-159">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="1ff7c-160">В разделе **Log Analytics** выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="1ff7c-161">В разделе **Рабочие области OMS** выберите рабочую область OMS для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-161">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="1ff7c-162">В разделе **Журнал** выберите категорию **IntegrationAccountTrackingEvents**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-162">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="1ff7c-163">Когда все будет готово, нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-163">When you're done, choose **Save**.</span></span>

   ![Настройка Log Analytics для отправки диагностических данных в журнал](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="1ff7c-165">Теперь [настройте отслеживание сообщений B2B в OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="1ff7c-166">Расширение возможностей использования диагностических данных в других службах</span><span class="sxs-lookup"><span data-stu-id="1ff7c-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="1ff7c-167">Помимо Azure Log Analytics, можно расширить возможности использования диагностических данных приложения логики в других службах Azure, например:</span><span class="sxs-lookup"><span data-stu-id="1ff7c-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="1ff7c-168">Архивация журналов диагностики Azure в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="1ff7c-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="1ff7c-169">Потоковая передача журналов диагностики в концентраторы событий Azure</span><span class="sxs-lookup"><span data-stu-id="1ff7c-169">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="1ff7c-170">После этого можно организовать мониторинг в режиме реального времени с помощью данных телеметрии и аналитики из других служб, таких как [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) и [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="1ff7c-171">Например:</span><span class="sxs-lookup"><span data-stu-id="1ff7c-171">For example:</span></span>

* [<span data-ttu-id="1ff7c-172">Потоковая передача данных из концентраторов событий в Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1ff7c-172">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="1ff7c-173">Анализ потоковой передачи данных с помощью Stream Analytics и создание панели мониторинга в Power BI для анализа данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="1ff7c-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="1ff7c-174">В зависимости от вариантов использования, которые нужно настроить, сначала необходимо [создать учетную запись хранения Azure](../storage/common/storage-create-storage-account.md) или [создать концентратор событий Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="1ff7c-174">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="1ff7c-175">Затем выберите варианты отправки данных диагностики:</span><span class="sxs-lookup"><span data-stu-id="1ff7c-175">Then select the options for where you want to send diagnostic data:</span></span>

![Отправка данных в учетную запись хранения Azure или в концентратор событий](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="1ff7c-177">Сроки хранения применяются только в том случае, если вы решили использовать учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-177">Retention periods apply only when you choose to use a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="1ff7c-178">Поддерживаемые схемы отслеживания</span><span class="sxs-lookup"><span data-stu-id="1ff7c-178">Supported tracking schemas</span></span>

<span data-ttu-id="1ff7c-179">Azure поддерживает приведенные ниже типы схем отслеживания. Все схемы, за исключением настраиваемой, являются фиксированными.</span><span class="sxs-lookup"><span data-stu-id="1ff7c-179">Azure supports these tracking schema types, which all have fixed schemas except the Custom type.</span></span>

* [<span data-ttu-id="1ff7c-180">Схема отслеживания AS2</span><span class="sxs-lookup"><span data-stu-id="1ff7c-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="1ff7c-181">Схема отслеживания X12</span><span class="sxs-lookup"><span data-stu-id="1ff7c-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="1ff7c-182">Настраиваемая схема отслеживания</span><span class="sxs-lookup"><span data-stu-id="1ff7c-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="1ff7c-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ff7c-183">Next steps</span></span>

* [<span data-ttu-id="1ff7c-184">Отслеживание сообщений B2B в OMS</span><span class="sxs-lookup"><span data-stu-id="1ff7c-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Отслеживание сообщений B2B в OMS")
* [<span data-ttu-id="1ff7c-185">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="1ff7c-185">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise")

