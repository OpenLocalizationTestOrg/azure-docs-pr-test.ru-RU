---
title: "aaaMonitor операции, события и счетчики для балансировки нагрузки | Документы Microsoft"
description: "Узнайте, как tooenable предупреждения события и проверки ведение журнала состояния работоспособности для балансировки нагрузки Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="84211-103">Служба анализа журналов для балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="84211-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="84211-104">Можно использовать различные типы журналов в Azure toomanage и устранение неполадок подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="84211-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="84211-105">Некоторые из этих журналов может осуществляться через портал hello.</span><span class="sxs-lookup"><span data-stu-id="84211-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="84211-106">Также все журналы можно извлечь из хранилища BLOB-объектов Azure, чтобы просматривать их с помощью таких средств, как Excel и Power BI.</span><span class="sxs-lookup"><span data-stu-id="84211-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="84211-107">Дополнительные сведения о различных типах журналов из следующего списка hello hello.</span><span class="sxs-lookup"><span data-stu-id="84211-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="84211-108">**Журналы аудита:** можно использовать [журналов аудита Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (прежнее название — операционные журналы) tooview все операции, отправленные tooyour подписок Azure и их состояние.</span><span class="sxs-lookup"><span data-stu-id="84211-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="84211-109">Журналы аудита включены по умолчанию и можно просмотреть в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="84211-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="84211-110">**Журналы событий на предупреждения:** rasied оповещения tooview этот журнал можно использовать подсистемой балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="84211-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="84211-111">Сбор сведений о состоянии Hello для подсистемы балансировки нагрузки hello каждые пять минут.</span><span class="sxs-lookup"><span data-stu-id="84211-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="84211-112">В этом журнале делается запись, только если возникает событие оповещения балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="84211-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="84211-113">**Журналы проверки работоспособности:** можно использовать этот журнал tooview проблемы, обнаруженные с вашей проверки работоспособности, например hello число экземпляров в пуле серверной части, которые не получает запросы от подсистемы балансировки нагрузки hello из-за сбоев пробы работоспособности.</span><span class="sxs-lookup"><span data-stu-id="84211-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="84211-114">Этот журнал записывается toowhen изменяется состояние проверки работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="84211-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84211-115">Служба Log Analytics в настоящее время работает только для подсистем балансировки нагрузки с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="84211-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="84211-116">Журналы доступны только для ресурсов, развернутых в модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="84211-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="84211-117">Нельзя использовать журналы для ресурсов в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="84211-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="84211-118">Дополнительные сведения о моделях развертывания hello см. в разделе [сведения о диспетчере ресурсов и классического развертывания](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="84211-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="84211-119">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="84211-119">Enable logging</span></span>

<span data-ttu-id="84211-120">Ведение журналов автоматически включается для каждого ресурса Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="84211-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="84211-121">Требуется tooenable событий и toostart ведения журнала проверки работоспособности, сбор данных hello, доступные через эти журналы.</span><span class="sxs-lookup"><span data-stu-id="84211-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="84211-122">Используйте следующие ведения журнала tooenable действия hello.</span><span class="sxs-lookup"><span data-stu-id="84211-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="84211-123">Вход toohello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84211-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="84211-124">Если у вас еще нет балансировщика нагрузки, [создайте балансировщик нагрузки](load-balancer-get-started-internet-arm-ps.md) перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="84211-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="84211-125">На портале hello щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="84211-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="84211-126">Выберите элемент **Подсистемы балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="84211-126">Select **Load Balancers**.</span></span>

    ![портал — балансировщик нагрузки](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="84211-128">Выберите существующую подсистему балансировки нагрузки, затем щелкните **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="84211-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="84211-129">Hello правой части диалогового окна hello под именем hello подсистемы балансировки нагрузки hello, прокрутите слишком**мониторинг**, нажмите кнопку **диагностики**.</span><span class="sxs-lookup"><span data-stu-id="84211-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![портал — балансировщик нагрузки — параметры](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="84211-131">В hello **диагностики** панели в разделе **состояние**выберите **на**.</span><span class="sxs-lookup"><span data-stu-id="84211-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="84211-132">Щелкните элемент **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="84211-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="84211-133">В разделе **Журналы** выберите существующую учетную запись хранения или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="84211-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="84211-134">Используйте ползунок toodetermine hello сколько дней, данные события сохраняются в журналах событий hello.</span><span class="sxs-lookup"><span data-stu-id="84211-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="84211-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="84211-135">Click **Save**.</span></span>

    ![Портал — журналы диагностики](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="84211-137">Для журналов аудита отдельная учетная запись хранения не требуется.</span><span class="sxs-lookup"><span data-stu-id="84211-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="84211-138">Здравствуйте, использования хранилища для событий и работоспособности пробы ведение журнала будет взиматься плата службы.</span><span class="sxs-lookup"><span data-stu-id="84211-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="84211-139">Журнал аудита</span><span class="sxs-lookup"><span data-stu-id="84211-139">Audit log</span></span>

<span data-ttu-id="84211-140">журнал аудита Hello создается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="84211-140">hello audit log is generated by default.</span></span> <span data-ttu-id="84211-141">журналы Hello сохраняются в течение 90 дней в хранилище Azure журналы событий.</span><span class="sxs-lookup"><span data-stu-id="84211-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="84211-142">Дополнительные сведения об этих журналов, считывая hello [просматривать события и журналы аудита](../monitoring-and-diagnostics/insights-debugging-with-events.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="84211-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="84211-143">Журнал событий оповещений</span><span class="sxs-lookup"><span data-stu-id="84211-143">Alert event log</span></span>

<span data-ttu-id="84211-144">Этот журнал создается только в том случае, если он включен для конкретной подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="84211-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="84211-145">Hello событий регистрируется в формате JSON и сохраняется в hello учетной записи хранения, которая была указана при включении ведения журнала hello.</span><span class="sxs-lookup"><span data-stu-id="84211-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="84211-146">Hello ниже приведен пример события.</span><span class="sxs-lookup"><span data-stu-id="84211-146">hello following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="84211-147">Hello JSON выходных данных показано hello *eventname* оповещение создано свойство, описывающий причину hello hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="84211-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="84211-148">В этом случае hello предупреждение создано был должен за источника, который ограничивает IP NAT нехватку портов tooTCP (SNAT).</span><span class="sxs-lookup"><span data-stu-id="84211-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="84211-149">Журнал проверки работоспособности</span><span class="sxs-lookup"><span data-stu-id="84211-149">Health probe log</span></span>

<span data-ttu-id="84211-150">Этот журнал создается только в том случае, если он включен для конкретного балансировщика нагрузки, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="84211-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="84211-151">Hello данные хранятся в учетной записи хранения hello, которая была указана при включении ведения журнала hello.</span><span class="sxs-lookup"><span data-stu-id="84211-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="84211-152">Контейнер с именем «аналитика журналов loadbalancerprobehealthstatus» создается и регистрируется hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="84211-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="84211-153">выходные данные JSON Hello показывает hello свойства поля hello основных сведений о состоянии работоспособности пробы hello.</span><span class="sxs-lookup"><span data-stu-id="84211-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="84211-154">Hello *dipDownCount* показывает общее количество экземпляров hello на Тыловой hello, которой не поступают сетевого трафика из-за toofailed проверки ответов.</span><span class="sxs-lookup"><span data-stu-id="84211-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="84211-155">Просмотр и анализ журналов аудита hello</span><span class="sxs-lookup"><span data-stu-id="84211-155">View and analyze hello audit log</span></span>

<span data-ttu-id="84211-156">Можно просматривать и анализировать данные журнала аудита с помощью любого из следующих методов hello.</span><span class="sxs-lookup"><span data-stu-id="84211-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="84211-157">**Инструменты Azure:** получать сведения из журналов аудита hello через Azure PowerShell, hello Azure интерфейс командной строки (CLI), hello Azure REST API или hello портал предварительной версии Azure.</span><span class="sxs-lookup"><span data-stu-id="84211-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="84211-158">Пошаговые инструкции для каждого метода описаны в hello [аудит операций с помощью диспетчера ресурсов](../azure-resource-manager/resource-group-audit.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="84211-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="84211-159">**Power BI.** Если у вас еще нет учетной записи [Power BI](https://powerbi.microsoft.com/pricing), вы можете использовать бесплатную пробную версию.</span><span class="sxs-lookup"><span data-stu-id="84211-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="84211-160">С помощью hello [журналов аудита Azure пакет содержимого для Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), можно анализировать данные с помощью предварительно настроенных панелей мониторинга или toosuit представлений можно настроить вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="84211-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="84211-161">Просмотр и анализ проверки работоспособности hello и журнал событий</span><span class="sxs-lookup"><span data-stu-id="84211-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="84211-162">Требуется хранилище tooyour tooconnect учетной записи и получения записи журнала hello JSON для проверки журналов событий и работоспособности.</span><span class="sxs-lookup"><span data-stu-id="84211-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="84211-163">После загрузки файлов JSON hello, их можно преобразовать tooCSV и view в Excel, PowerBI или другого средства визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="84211-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="84211-164">Если вы знакомы с Visual Studio и основные понятия, связанные изменения значений константы и переменные в C#, можно использовать hello [входа преобразователь средства](https://github.com/Azure-Samples/networking-dotnet-log-converter) GitHub доступны.</span><span class="sxs-lookup"><span data-stu-id="84211-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84211-165">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="84211-165">Additional resources</span></span>

* <span data-ttu-id="84211-166">[Визуализация журналов аудита Azure с помощью Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .</span><span class="sxs-lookup"><span data-stu-id="84211-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="84211-167">[Просмотр и анализ журналов аудита Azure с помощью Power BI и других средств](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .</span><span class="sxs-lookup"><span data-stu-id="84211-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84211-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84211-168">Next steps</span></span>

[<span data-ttu-id="84211-169">Проверки балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="84211-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
