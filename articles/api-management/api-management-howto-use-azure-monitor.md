---
title: "Наблюдение за управлением API с помощью Azure Monitor | Документация Майкрософт"
description: "Узнайте, как наблюдать за службой управления API Azure с помощью Azure Monitor."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="a0099-103">Наблюдение за управлением API с помощью Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="a0099-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="a0099-104">Azure Monitor — это служба Azure, которая предоставляет единый источник данных для наблюдения за всеми ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="a0099-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="a0099-105">С помощью Azure Monitor можно визуализировать, запрашивать, маршрутизировать, архивировать метрики и журналы, полученные от ресурсов Azure, таких как управление API, а также реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="a0099-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="a0099-106">В следующем видео показано, как отслеживать управление API с помощью Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a0099-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="a0099-107">Дополнительные сведения об Azure Monitor см. в статье [Приступая к работе с Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="a0099-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="a0099-108">Метрики</span><span class="sxs-lookup"><span data-stu-id="a0099-108">Metrics</span></span>
<span data-ttu-id="a0099-109">Сейчас управление API передает пять метрик. В будущем мы планируем добавить больше метрик.</span><span class="sxs-lookup"><span data-stu-id="a0099-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="a0099-110">Эти метрики передаются ежеминутно, что позволяет в близком к реальному времени отслеживать состояние и работоспособность интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="a0099-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="a0099-111">Ниже приведены сводные сведения о метриках.</span><span class="sxs-lookup"><span data-stu-id="a0099-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="a0099-112">Общее количество запросов к шлюзу. Количество запросов API за период.</span><span class="sxs-lookup"><span data-stu-id="a0099-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="a0099-113">Успешные запросы к шлюзу. Количество запросов API, которые успешно получили коды ответов HTTP, включая 304, 307 и все, что меньше, чем 301 (например, 200).</span><span class="sxs-lookup"><span data-stu-id="a0099-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="a0099-114">Неудачные запросы к шлюзу. Количество запросов API, которые получили ошибочные коды ответов HTTP, включая 400 и все, что больше, чем 500.</span><span class="sxs-lookup"><span data-stu-id="a0099-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="a0099-115">Неавторизованные запросы к шлюзу. Количество запросов API, которые получили коды ответов HTTP, включая 401, 403 и 429.</span><span class="sxs-lookup"><span data-stu-id="a0099-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="a0099-116">Другие запросы к шлюзу. Количество запросов API, которые получили коды ответов HTTP, не принадлежащие ни к одной из указанных выше категорий (например, 418).</span><span class="sxs-lookup"><span data-stu-id="a0099-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="a0099-117">Вы можете получить доступ к метрикам в службе управления API или получить доступ к метрикам всех ресурсов Azure в Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a0099-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="a0099-118">Чтобы просмотреть метрики в службе управления API, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a0099-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="a0099-119">Перейдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a0099-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="a0099-120">Перейдите к службе управления API.</span><span class="sxs-lookup"><span data-stu-id="a0099-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="a0099-121">Щелкните **Метрики**.</span><span class="sxs-lookup"><span data-stu-id="a0099-121">Click **Metrics**.</span></span>

![Колонка метрик][metrics-blade]

<span data-ttu-id="a0099-123">Дополнительные сведения об использовании метрик см. в статье [Обзор метрик в Microsoft Azure].</span><span class="sxs-lookup"><span data-stu-id="a0099-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="a0099-124">Журналы действий</span><span class="sxs-lookup"><span data-stu-id="a0099-124">Activity Logs</span></span>
<span data-ttu-id="a0099-125">Журналы действий позволяют подробно проанализировать операции, выполненные в службах управления API.</span><span class="sxs-lookup"><span data-stu-id="a0099-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="a0099-126">Ранее они назывались журналами аудита или журналами операций.</span><span class="sxs-lookup"><span data-stu-id="a0099-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="a0099-127">С помощью журналов изменений можно ответить на вопросы "что? кто? когда?" о любой операции записи (PUT, POST, DELETE) в службах управления API.</span><span class="sxs-lookup"><span data-stu-id="a0099-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="a0099-128">Журналы действий не содержат операций чтения (GET), операций, выполненных на классическом портале издателя или с помощью исходных API управления.</span><span class="sxs-lookup"><span data-stu-id="a0099-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="a0099-129">Вы можете получить доступ к журналам действий в службе управления API или получить доступ к журналам всех ресурсов Azure в Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a0099-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="a0099-130">Чтобы просмотреть журналы действий в службе управления API, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a0099-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="a0099-131">Перейдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a0099-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="a0099-132">Перейдите к службе управления API.</span><span class="sxs-lookup"><span data-stu-id="a0099-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="a0099-133">Щелкните **Журнал действий**.</span><span class="sxs-lookup"><span data-stu-id="a0099-133">Click **Activity log**.</span></span>

![Колонка журналов действий][activity-logs-blade]

<span data-ttu-id="a0099-135">Дополнительные сведения об использовании метрик см. в статье [Общие сведения о журнале действий Azure].</span><span class="sxs-lookup"><span data-stu-id="a0099-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="a0099-136">Оповещения</span><span class="sxs-lookup"><span data-stu-id="a0099-136">Alerts</span></span>
<span data-ttu-id="a0099-137">Вы можете настроить получение уведомлений на основе метрик и журналов действий.</span><span class="sxs-lookup"><span data-stu-id="a0099-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="a0099-138">Azure Monitor позволяет настроить действие, выполняемое при активации оповещения:</span><span class="sxs-lookup"><span data-stu-id="a0099-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="a0099-139">Отправка уведомления по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="a0099-139">Send an email notification</span></span>
* <span data-ttu-id="a0099-140">Вызов webhook.</span><span class="sxs-lookup"><span data-stu-id="a0099-140">Call a webhook</span></span>
* <span data-ttu-id="a0099-141">Вызов приложения логики Azure.</span><span class="sxs-lookup"><span data-stu-id="a0099-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="a0099-142">Правила оповещений можно настроить в службе управления API или в Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a0099-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="a0099-143">Чтобы настроить их в службе управления API:</span><span class="sxs-lookup"><span data-stu-id="a0099-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="a0099-144">Перейдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a0099-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="a0099-145">Перейдите к службе управления API.</span><span class="sxs-lookup"><span data-stu-id="a0099-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="a0099-146">Щелкните **Правила оповещения**.</span><span class="sxs-lookup"><span data-stu-id="a0099-146">Click **Alert rules**.</span></span>

![Колонка "Правила оповещения"][alert-rules-blade]

<span data-ttu-id="a0099-148">Дополнительные сведения об использовании оповещений см. в статье [Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure].</span><span class="sxs-lookup"><span data-stu-id="a0099-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="a0099-149">Журналы диагностики</span><span class="sxs-lookup"><span data-stu-id="a0099-149">Diagnostic Logs</span></span>
<span data-ttu-id="a0099-150">Журналы диагностики предоставляют подробные сведения об операциях и ошибках, которые важны для аудита, а также для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="a0099-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="a0099-151">Журналы диагностики отличаются от журналов действий.</span><span class="sxs-lookup"><span data-stu-id="a0099-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="a0099-152">Журналы действий позволяют подробно проанализировать операции, выполненные с ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="a0099-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="a0099-153">Журналы диагностики дают представление об операциях, выполняемых самим ресурсом.</span><span class="sxs-lookup"><span data-stu-id="a0099-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="a0099-154">Сейчас управление API предоставляет журналы диагностики (выполняемые в пакетном режиме каждый час) отдельных запросов API со следующей структурой каждой записи:</span><span class="sxs-lookup"><span data-stu-id="a0099-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="a0099-155">Вы можете получить доступ к журналам диагностики в службе управления API или получить доступ к журналам всех ресурсов Azure в Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a0099-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="a0099-156">Чтобы просмотреть журналы диагностики в службе управления API, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a0099-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="a0099-157">Перейдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a0099-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="a0099-158">Перейдите к службе управления API.</span><span class="sxs-lookup"><span data-stu-id="a0099-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="a0099-159">Щелкните **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="a0099-159">Click **Diagnostic log**.</span></span>

![Колонка "Журналы диагностики"][diagnostic-logs-blade]

<span data-ttu-id="a0099-161">Дополнительные сведения об использовании метрик см. в статье [Сбор и использование диагностических данных из ресурсов Azure].</span><span class="sxs-lookup"><span data-stu-id="a0099-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="a0099-162">Дальнейшее действие</span><span class="sxs-lookup"><span data-stu-id="a0099-162">Next Step</span></span>

* <span data-ttu-id="a0099-163">[Приступая к работе с Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="a0099-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="a0099-164">[Обзор метрик в Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="a0099-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="a0099-165">[Общие сведения о журнале действий Azure]</span><span class="sxs-lookup"><span data-stu-id="a0099-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="a0099-166">[Сбор и использование диагностических данных из ресурсов Azure]</span><span class="sxs-lookup"><span data-stu-id="a0099-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="a0099-167">[Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure]</span><span class="sxs-lookup"><span data-stu-id="a0099-167">[Overview of Alerts]</span></span>

<span data-ttu-id="a0099-168">[Приступая к работе с Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="a0099-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="a0099-169">[Обзор метрик в Microsoft Azure]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="a0099-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="a0099-170">[Общие сведения о журнале действий Azure]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="a0099-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="a0099-171">[Сбор и использование диагностических данных из ресурсов Azure]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="a0099-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="a0099-172">[Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="a0099-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
