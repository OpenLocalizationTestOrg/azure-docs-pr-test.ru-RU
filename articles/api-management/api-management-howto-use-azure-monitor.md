---
title: "Управление API с помощью монитора Azure aaaMonitor | Документы Microsoft"
description: "Узнайте, как службы с помощью монитора Azure toomonitor API управления Azure."
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
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="2eeeb-103">Наблюдение за управлением API с помощью Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="2eeeb-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="2eeeb-104">Azure Monitor — это служба Azure, которая предоставляет единый источник данных для наблюдения за всеми ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="2eeeb-105">Монитор Azure можно визуализировать, запрос, маршрутизации, архивировать и выполнять действия с метриками hello и журналы, полученные из ресурсов Azure, такие как управление API.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="2eeeb-106">Здравствуйте, следуя видео показано, как toomonitor управления API, с помощью монитора Azure.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="2eeeb-107">Дополнительные сведения об Azure Monitor см. в статье [Приступая к работе с Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="2eeeb-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="2eeeb-108">Метрики</span><span class="sxs-lookup"><span data-stu-id="2eeeb-108">Metrics</span></span>
<span data-ttu-id="2eeeb-109">Управление API в настоящее время создает пять показателей, мы планируем в будущем hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="2eeeb-110">Эти показатели создаются каждую минуту, предоставляя почти в реальном времени отслеживать в состоянии hello и работоспособности собственные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="2eeeb-111">Ниже приводится сводка hello метрик:</span><span class="sxs-lookup"><span data-stu-id="2eeeb-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="2eeeb-112">Общее количество запросов шлюза: hello количество API запрашивает в период hello.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="2eeeb-113">Количество успешных запросов шлюза: число hello запросы API, которые получены успешно коды ответа HTTP, включая 304, 307 и меньший, чем 301 (например, 200).</span><span class="sxs-lookup"><span data-stu-id="2eeeb-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="2eeeb-114">Количество неудачных запросов шлюза: hello число запросы API, которые получены ошибочные коды ответа HTTP, включая 400 и ничего больше 500.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="2eeeb-115">Неавторизованных запросов шлюза: номер hello запросов API, которые получены коды ответа HTTP 401, 403, а 429.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="2eeeb-116">Других шлюза запросов: номер hello запросы API, которые получены коды ответа HTTP, не принадлежащие tooany из hello предшествующий категории (например, 418).</span><span class="sxs-lookup"><span data-stu-id="2eeeb-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="2eeeb-117">Вы можете получить доступ к метрикам в службе управления API или получить доступ к метрикам всех ресурсов Azure в Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="2eeeb-118">метрики tooview в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="2eeeb-119">Здравствуйте, откройте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="2eeeb-120">Go tooyour службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="2eeeb-121">Щелкните **Метрики**.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-121">Click **Metrics**.</span></span>

![Колонка метрик][metrics-blade]

<span data-ttu-id="2eeeb-123">Дополнительные сведения о том, как toouse метрик, в разделе [Обзор метрик].</span><span class="sxs-lookup"><span data-stu-id="2eeeb-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="2eeeb-124">Журналы действий</span><span class="sxs-lookup"><span data-stu-id="2eeeb-124">Activity Logs</span></span>
<span data-ttu-id="2eeeb-125">Журналы действий глубже понять hello операций, которые были выполнены на ваши службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="2eeeb-126">Ранее они назывались журналами аудита или журналами операций.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="2eeeb-127">Используя журналы действий, можно определить hello», кто и когда» для любой записи операций (PUT, POST, DELETE), затраченное на ваши службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="2eeeb-128">Журналы действий не включать операции чтения (GET) или операций, выполняемых в hello классический портал издателя или с помощью hello исходного API-интерфейсы управления.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="2eeeb-129">Вы можете получить доступ к журналам действий в службе управления API или получить доступ к журналам всех ресурсов Azure в Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="2eeeb-130">Действие tooview регистрирует в службе управления API:</span><span class="sxs-lookup"><span data-stu-id="2eeeb-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="2eeeb-131">Здравствуйте, откройте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="2eeeb-132">Go tooyour службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="2eeeb-133">Щелкните **Журнал действий**.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-133">Click **Activity log**.</span></span>

![Колонка журналов действий][activity-logs-blade]

<span data-ttu-id="2eeeb-135">Дополнительные сведения о том, как toouse метрик, в разделе [Общие сведения о журналах активности].</span><span class="sxs-lookup"><span data-stu-id="2eeeb-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="2eeeb-136">Оповещения</span><span class="sxs-lookup"><span data-stu-id="2eeeb-136">Alerts</span></span>
<span data-ttu-id="2eeeb-137">Можно настроить предупреждения tooreceive, основанные на журналах метрик и действия.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="2eeeb-138">Монитор Azure позволяет tooconfigure предупреждения toodo hello следующие при инициировании:</span><span class="sxs-lookup"><span data-stu-id="2eeeb-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="2eeeb-139">Отправка уведомления по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-139">Send an email notification</span></span>
* <span data-ttu-id="2eeeb-140">Вызов webhook.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-140">Call a webhook</span></span>
* <span data-ttu-id="2eeeb-141">Вызов приложения логики Azure.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="2eeeb-142">Правила оповещений можно настроить в службе управления API или в Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="2eeeb-143">tooconfigure их в службе управления API:</span><span class="sxs-lookup"><span data-stu-id="2eeeb-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="2eeeb-144">Здравствуйте, откройте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="2eeeb-145">Go tooyour службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="2eeeb-146">Щелкните **Правила оповещения**.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-146">Click **Alert rules**.</span></span>

![Колонка "Правила оповещения"][alert-rules-blade]

<span data-ttu-id="2eeeb-148">Дополнительные сведения об использовании оповещений см. в статье [Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure].</span><span class="sxs-lookup"><span data-stu-id="2eeeb-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="2eeeb-149">Журналы диагностики</span><span class="sxs-lookup"><span data-stu-id="2eeeb-149">Diagnostic Logs</span></span>
<span data-ttu-id="2eeeb-150">Журналы диагностики предоставляют подробные сведения об операциях и ошибках, которые важны для аудита, а также для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="2eeeb-151">Журналы диагностики отличаются от журналов действий.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="2eeeb-152">Журналы действий получить представление о hello операций, которые были выполнены на ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="2eeeb-153">Журналы диагностики дают представление об операциях, выполняемых самим ресурсом.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="2eeeb-154">API управления в данный момент предоставляет диагностики журналы отдельных API (в пакетном режиме каждый час) запрос с каждой записи, наличие hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="2eeeb-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

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

<span data-ttu-id="2eeeb-155">Вы можете получить доступ к журналам диагностики в службе управления API или получить доступ к журналам всех ресурсов Azure в Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="2eeeb-156">журналы диагностики tooview в службе управления API:</span><span class="sxs-lookup"><span data-stu-id="2eeeb-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="2eeeb-157">Здравствуйте, откройте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="2eeeb-158">Go tooyour службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="2eeeb-159">Щелкните **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="2eeeb-159">Click **Diagnostic log**.</span></span>

![Колонка "Журналы диагностики"][diagnostic-logs-blade]

<span data-ttu-id="2eeeb-161">Дополнительные сведения о том, как toouse метрик, в разделе [Обзор журналов диагностики].</span><span class="sxs-lookup"><span data-stu-id="2eeeb-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="2eeeb-162">Дальнейшее действие</span><span class="sxs-lookup"><span data-stu-id="2eeeb-162">Next Step</span></span>

* <span data-ttu-id="2eeeb-163">[Приступая к работе с Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="2eeeb-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="2eeeb-164">[Обзор метрик]</span><span class="sxs-lookup"><span data-stu-id="2eeeb-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="2eeeb-165">[Общие сведения о журналах активности]</span><span class="sxs-lookup"><span data-stu-id="2eeeb-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="2eeeb-166">[Обзор журналов диагностики]</span><span class="sxs-lookup"><span data-stu-id="2eeeb-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="2eeeb-167">[Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure]</span><span class="sxs-lookup"><span data-stu-id="2eeeb-167">[Overview of Alerts]</span></span>

[Приступая к работе с Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[Обзор метрик]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[Общие сведения о журналах активности]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[Обзор журналов диагностики]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
