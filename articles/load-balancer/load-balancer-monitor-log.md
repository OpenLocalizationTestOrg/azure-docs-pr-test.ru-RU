---
title: "Мониторинг операций, событий и счетчиков для балансировки нагрузки | Документация Майкрософт"
description: "Узнайте, как включить ведение журналов событий оповещений и проверки работоспособности для балансировщика нагрузки Azure"
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
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="a57af-103">Служба анализа журналов для балансировщика нагрузки Azure</span><span class="sxs-lookup"><span data-stu-id="a57af-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="a57af-104">В Azure можно использовать различные виды журналов для управления балансировщиками нагрузки и устранения возникающих в них неполадок.</span><span class="sxs-lookup"><span data-stu-id="a57af-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="a57af-105">Доступ к некоторым из этих журналов можно получить через портал.</span><span class="sxs-lookup"><span data-stu-id="a57af-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="a57af-106">Также все журналы можно извлечь из хранилища BLOB-объектов Azure, чтобы просматривать их с помощью таких средств, как Excel и Power BI.</span><span class="sxs-lookup"><span data-stu-id="a57af-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="a57af-107">В списке ниже приведены дополнительные сведения о различных типах журналов.</span><span class="sxs-lookup"><span data-stu-id="a57af-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="a57af-108">**Журналы аудита.** В [журналах аудита Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (прежнее название — операционные журналы) можно просмотреть все операции, отправляемые в ваши подписки Azure, и состояние этих операций.</span><span class="sxs-lookup"><span data-stu-id="a57af-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="a57af-109">По умолчанию журналы аудита включены, и их можно просмотреть на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a57af-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="a57af-110">**Журналы событий оповещений**. Эти журналы можно использовать для просмотра оповещений, создаваемых для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a57af-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="a57af-111">Данные о состоянии балансировщика нагрузки собираются каждые пять минут.</span><span class="sxs-lookup"><span data-stu-id="a57af-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="a57af-112">В этом журнале делается запись, только если возникает событие оповещения балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a57af-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="a57af-113">**Журналы проверки работоспособности**. Эти журналы можно использовать для просмотра проблем, обнаруженных при проверке работоспособности, включая сведения о числе экземпляров во внутреннем пуле, которые не получают запросы от подсистемы балансировки нагрузки из-за ошибок проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="a57af-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="a57af-114">Эти журналы записываются при изменении состояния в ходе проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="a57af-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a57af-115">Служба Log Analytics в настоящее время работает только для подсистем балансировки нагрузки с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="a57af-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="a57af-116">Журналы доступны только для ресурсов, развернутых в модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a57af-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="a57af-117">Журналы нельзя использовать для ресурсов в классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="a57af-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="a57af-118">Дополнительные сведения о моделях развертывания см. в статье, посвященной [развертыванию с помощью Resource Manager и классическому развертыванию](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a57af-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="a57af-119">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="a57af-119">Enable logging</span></span>

<span data-ttu-id="a57af-120">Ведение журналов автоматически включается для каждого ресурса Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a57af-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="a57af-121">Чтобы начать сбор соответствующих данных, необходимо включить ведение журналов событий и проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="a57af-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="a57af-122">Вот как можно включить ведение журнала:</span><span class="sxs-lookup"><span data-stu-id="a57af-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="a57af-123">Войдите на [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a57af-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="a57af-124">Если у вас еще нет балансировщика нагрузки, [создайте балансировщик нагрузки](load-balancer-get-started-internet-arm-ps.md) перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="a57af-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="a57af-125">На портале нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="a57af-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="a57af-126">Выберите элемент **Подсистемы балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="a57af-126">Select **Load Balancers**.</span></span>

    ![портал — балансировщик нагрузки](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="a57af-128">Выберите существующую подсистему балансировки нагрузки, затем щелкните **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="a57af-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="a57af-129">В правой части диалогового окна, под названием подсистемы балансировки нагрузки, прокрутите до элемента **Мониторинг** и щелкните **Диагностика**.</span><span class="sxs-lookup"><span data-stu-id="a57af-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![портал — балансировщик нагрузки — параметры](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="a57af-131">На панели **Диагностика** в разделе **Состояние** щелкните **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="a57af-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="a57af-132">Щелкните элемент **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="a57af-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="a57af-133">В разделе **Журналы** выберите существующую учетную запись хранения или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="a57af-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="a57af-134">С помощью ползунка определите, сколько дней данные о событиях будут храниться в журналах событий.</span><span class="sxs-lookup"><span data-stu-id="a57af-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="a57af-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a57af-135">Click **Save**.</span></span>

    ![Портал — журналы диагностики](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="a57af-137">Для журналов аудита отдельная учетная запись хранения не требуется.</span><span class="sxs-lookup"><span data-stu-id="a57af-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="a57af-138">За использование хранилища для журналов событий и проверки работоспособности взимается плата.</span><span class="sxs-lookup"><span data-stu-id="a57af-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="a57af-139">Журнал аудита</span><span class="sxs-lookup"><span data-stu-id="a57af-139">Audit log</span></span>

<span data-ttu-id="a57af-140">Журнал аудита создается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a57af-140">The audit log is generated by default.</span></span> <span data-ttu-id="a57af-141">Журналы хранятся в течение 90 дней в хранилище журналов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="a57af-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="a57af-142">Дополнительные сведения об этих журналах см. в статье [Просмотр журналов событий и аудита](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span><span class="sxs-lookup"><span data-stu-id="a57af-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="a57af-143">Журнал событий оповещений</span><span class="sxs-lookup"><span data-stu-id="a57af-143">Alert event log</span></span>

<span data-ttu-id="a57af-144">Этот журнал создается только в том случае, если он включен для конкретной подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a57af-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="a57af-145">События регистрируются в формате JSON и хранятся в учетной записи хранения, указанной при включении ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="a57af-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="a57af-146">Ниже приведен пример события.</span><span class="sxs-lookup"><span data-stu-id="a57af-146">The following is an example of an event.</span></span>

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

<span data-ttu-id="a57af-147">В выходных данных JSON отображается свойство *eventname* , описывающее причину создания оповещения балансировщиком нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a57af-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="a57af-148">В этом случае оповещение было создано из-за нехватки порта TCP, вызванной ограничениями преобразования исходных сетевых адресов (SNAT).</span><span class="sxs-lookup"><span data-stu-id="a57af-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="a57af-149">Журнал проверки работоспособности</span><span class="sxs-lookup"><span data-stu-id="a57af-149">Health probe log</span></span>

<span data-ttu-id="a57af-150">Этот журнал создается только в том случае, если он включен для конкретного балансировщика нагрузки, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="a57af-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="a57af-151">Данные хранятся в учетной записи хранения, указанной при включении ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="a57af-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="a57af-152">Создается контейнер с именем insights-logs-loadbalancerprobehealthstatus, и в журнал записываются следующие данные.</span><span class="sxs-lookup"><span data-stu-id="a57af-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

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

<span data-ttu-id="a57af-153">В выходных данных JSON в поле свойств отображаются основные сведения о состоянии проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="a57af-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="a57af-154">Свойство *DipDownCount* показывает общее количество экземпляров в серверной части, которые не получают сетевой трафик из-за неудачных ответов проверки.</span><span class="sxs-lookup"><span data-stu-id="a57af-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="a57af-155">Просмотр и анализ журнала аудита</span><span class="sxs-lookup"><span data-stu-id="a57af-155">View and analyze the audit log</span></span>

<span data-ttu-id="a57af-156">Данные журнала аудита можно просматривать и анализировать с помощью любого из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="a57af-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="a57af-157">**Средства Azure.** Информацию из журналов аудита можно получать с помощью Azure PowerShell, интерфейса командной строки (CLI) Azure, интерфейса REST API Azure или портала предварительной версии Azure.</span><span class="sxs-lookup"><span data-stu-id="a57af-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="a57af-158">Пошаговые инструкции для каждого метода подробно описаны в статье [Операции аудита с помощью диспетчера ресурсов](../azure-resource-manager/resource-group-audit.md) .</span><span class="sxs-lookup"><span data-stu-id="a57af-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="a57af-159">**Power BI.** Если у вас еще нет учетной записи [Power BI](https://powerbi.microsoft.com/pricing), вы можете использовать бесплатную пробную версию.</span><span class="sxs-lookup"><span data-stu-id="a57af-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="a57af-160">Используя [пакет содержимого "Журналы аудита Azure" для Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), можно анализировать данные с помощью предварительно настроенных панелей мониторинга или дополнительно настроить представление данных в зависимости от своих потребностей.</span><span class="sxs-lookup"><span data-stu-id="a57af-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="a57af-161">Просмотр и анализ журналов событий и проверки работоспособности</span><span class="sxs-lookup"><span data-stu-id="a57af-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="a57af-162">Вам потребуется подключиться к учетной записи хранения и извлечь записи журнала JSON для журналов событий и проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="a57af-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="a57af-163">После загрузки JSON-файлов их можно преобразовать в формат CSV и просматривать в Excel, PowerBI или другом средстве визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="a57af-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="a57af-164">Если вы знакомы с Visual Studio и основными понятиями изменения значений констант и переменных в C#, можно использовать [инструменты преобразования журналов](https://github.com/Azure-Samples/networking-dotnet-log-converter), доступные на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="a57af-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a57af-165">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a57af-165">Additional resources</span></span>

* <span data-ttu-id="a57af-166">[Визуализация журналов аудита Azure с помощью Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a57af-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="a57af-167">[Просмотр и анализ журналов аудита Azure с помощью Power BI и других средств](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .</span><span class="sxs-lookup"><span data-stu-id="a57af-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a57af-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a57af-168">Next steps</span></span>

[<span data-ttu-id="a57af-169">Проверки балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="a57af-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
