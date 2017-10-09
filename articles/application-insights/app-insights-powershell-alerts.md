---
title: "оповещения tooset aaaUse Powershell в Application Insights | Документы Microsoft"
description: "Автоматизируйте настройку tooget Application Insights по электронной почте о изменениях метрики."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="11f1d-103">Используйте PowerShell tooset предупреждения в Application Insights</span><span class="sxs-lookup"><span data-stu-id="11f1d-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="11f1d-104">Можно автоматизировать настройку hello [оповещения](app-insights-alerts.md) в [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11f1d-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="11f1d-105">Кроме того, вы можете [задать оповещения tooan ответа веб-перехватчиков tooautomate](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="11f1d-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11f1d-106">Если требуется toocreate ресурсы и оповещения на hello таким же времени, рассмотрите возможность [с помощью шаблона Azure Resource Manager](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="11f1d-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="11f1d-107">Однократная настройка</span><span class="sxs-lookup"><span data-stu-id="11f1d-107">One-time setup</span></span>
<span data-ttu-id="11f1d-108">Если вы ранее не использовали PowerShell для подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="11f1d-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="11f1d-109">Установка модуля Azure Powershell hello на hello компьютер, где toorun hello скриптов.</span><span class="sxs-lookup"><span data-stu-id="11f1d-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="11f1d-110">Установите [установщик веб-платформы Майкрософт (версии 5 или более поздней)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="11f1d-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="11f1d-111">Используйте его tooinstall Microsoft Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="11f1d-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="11f1d-112">Подключение tooAzure</span><span class="sxs-lookup"><span data-stu-id="11f1d-112">Connect tooAzure</span></span>
<span data-ttu-id="11f1d-113">Запустите Azure PowerShell и [подключения подписки tooyour](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="11f1d-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="11f1d-114">Получение оповещений</span><span class="sxs-lookup"><span data-stu-id="11f1d-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="11f1d-115">Добавление оповещения</span><span class="sxs-lookup"><span data-stu-id="11f1d-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="11f1d-116">Пример 1</span><span class="sxs-lookup"><span data-stu-id="11f1d-116">Example 1</span></span>
<span data-ttu-id="11f1d-117">Отправить мне электронное сообщение, если выполняется медленнее, чем 1 секунду запросов tooHTTP ответа сервера hello, Усредненное за 5 минут.</span><span class="sxs-lookup"><span data-stu-id="11f1d-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="11f1d-118">Мой ресурс Application Insights называется IceCreamWebApp, и он находится в группе ресурсов Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="11f1d-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="11f1d-119">Я hello владельца hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="11f1d-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="11f1d-120">Hello GUID — идентификатор подписки hello (не hello ключ инструментирования приложения hello).</span><span class="sxs-lookup"><span data-stu-id="11f1d-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="11f1d-121">Пример 2</span><span class="sxs-lookup"><span data-stu-id="11f1d-121">Example 2</span></span>
<span data-ttu-id="11f1d-122">У меня есть приложение, в котором используется [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport метрику с именем «salesPerHour.»</span><span class="sxs-lookup"><span data-stu-id="11f1d-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="11f1d-123">Отправьте сообщение электронной почты toomy коллег, если «salesPerHour» становится меньше 100, Усредненное более 24 часов.</span><span class="sxs-lookup"><span data-stu-id="11f1d-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="11f1d-124">такие же правила можно использовать для метрики hello Hello отчет с помощью hello [измерения параметра](app-insights-api-custom-events-metrics.md#properties) отслеживания другого вызова, например TrackEvent или trackPageView.</span><span class="sxs-lookup"><span data-stu-id="11f1d-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="11f1d-125">Имена метрик</span><span class="sxs-lookup"><span data-stu-id="11f1d-125">Metric names</span></span>
| <span data-ttu-id="11f1d-126">Имя метрики</span><span class="sxs-lookup"><span data-stu-id="11f1d-126">Metric name</span></span> | <span data-ttu-id="11f1d-127">Имя экрана</span><span class="sxs-lookup"><span data-stu-id="11f1d-127">Screen name</span></span> | <span data-ttu-id="11f1d-128">Описание</span><span class="sxs-lookup"><span data-stu-id="11f1d-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="11f1d-129">Исключения браузера</span><span class="sxs-lookup"><span data-stu-id="11f1d-129">Browser exceptions</span></span> |<span data-ttu-id="11f1d-130">Число неперехваченных исключений в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="11f1d-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="11f1d-131">Исключения сервера</span><span class="sxs-lookup"><span data-stu-id="11f1d-131">Server exceptions</span></span> |<span data-ttu-id="11f1d-132">Число необработанных исключений выданных приложение hello</span><span class="sxs-lookup"><span data-stu-id="11f1d-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="11f1d-133">Время обработки клиента</span><span class="sxs-lookup"><span data-stu-id="11f1d-133">Client processing time</span></span> |<span data-ttu-id="11f1d-134">Время между получением hello получения последнего байта документа до загрузки модели DOM hello.</span><span class="sxs-lookup"><span data-stu-id="11f1d-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="11f1d-135">Обработка асинхронных запросов может продолжаться.</span><span class="sxs-lookup"><span data-stu-id="11f1d-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="11f1d-136">Время подключения к сети при загрузке страницы</span><span class="sxs-lookup"><span data-stu-id="11f1d-136">Page load network connect time</span></span> |<span data-ttu-id="11f1d-137">Браузер hello времени занимает tooconnect toohello сети.</span><span class="sxs-lookup"><span data-stu-id="11f1d-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="11f1d-138">Может быть 0, если страница в кэше.</span><span class="sxs-lookup"><span data-stu-id="11f1d-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="11f1d-139">Время получения ответа</span><span class="sxs-lookup"><span data-stu-id="11f1d-139">Receiving response time</span></span> |<span data-ttu-id="11f1d-140">Время между браузера при отправке ответа tooreceive toostarting запрос.</span><span class="sxs-lookup"><span data-stu-id="11f1d-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="11f1d-141">Время отправки запроса</span><span class="sxs-lookup"><span data-stu-id="11f1d-141">Send request time</span></span> |<span data-ttu-id="11f1d-142">Время выполнения запроса toosend обозревателя.</span><span class="sxs-lookup"><span data-stu-id="11f1d-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="11f1d-143">Время загрузки страницы в браузере</span><span class="sxs-lookup"><span data-stu-id="11f1d-143">Browser page load time</span></span> |<span data-ttu-id="11f1d-144">Время с момента отправки запроса пользователя до загрузки DOM, таблиц стилей, сценариев и изображений.</span><span class="sxs-lookup"><span data-stu-id="11f1d-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="11f1d-145">Объем доступной памяти</span><span class="sxs-lookup"><span data-stu-id="11f1d-145">Available memory</span></span> |<span data-ttu-id="11f1d-146">Физическая память, доступная для использования процессами или системой.</span><span class="sxs-lookup"><span data-stu-id="11f1d-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="11f1d-147">Скорость обработки операций ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="11f1d-147">Process IO Rate</span></span> |<span data-ttu-id="11f1d-148">Всего байт на второй чтения и записи toofiles, сети и устройства.</span><span class="sxs-lookup"><span data-stu-id="11f1d-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="11f1d-149">Частота порождения исключений</span><span class="sxs-lookup"><span data-stu-id="11f1d-149">exception rate</span></span> |<span data-ttu-id="11f1d-150">Количество исключений, порождаемых в секунду.</span><span class="sxs-lookup"><span data-stu-id="11f1d-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="11f1d-151">Обработка ЦП</span><span class="sxs-lookup"><span data-stu-id="11f1d-151">Process CPU</span></span> |<span data-ttu-id="11f1d-152">Процент времени, затраченного всеми потоками процесса, используемые инструкции tooexecution hello процессора для процесса приложения hello Hello.</span><span class="sxs-lookup"><span data-stu-id="11f1d-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="11f1d-153">Процессорное время</span><span class="sxs-lookup"><span data-stu-id="11f1d-153">Processor time</span></span> |<span data-ttu-id="11f1d-154">Hello процент времени, hello процессора, затраченного в активные потоки.</span><span class="sxs-lookup"><span data-stu-id="11f1d-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="11f1d-155">Количество байтов исключительного использования процессов</span><span class="sxs-lookup"><span data-stu-id="11f1d-155">Process private bytes</span></span> |<span data-ttu-id="11f1d-156">Память, исключительно назначенная toohello мониторинг процессов приложения.</span><span class="sxs-lookup"><span data-stu-id="11f1d-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="11f1d-157">Время выполнения запроса ASP.NET</span><span class="sxs-lookup"><span data-stu-id="11f1d-157">ASP.NET request execution time</span></span> |<span data-ttu-id="11f1d-158">Время выполнения последнего запроса hello.</span><span class="sxs-lookup"><span data-stu-id="11f1d-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="11f1d-159">Число запросов ASP.NET в очереди выполнения</span><span class="sxs-lookup"><span data-stu-id="11f1d-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="11f1d-160">Длина очереди запросов приложения hello.</span><span class="sxs-lookup"><span data-stu-id="11f1d-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="11f1d-161">Частота запросов ASP.NET</span><span class="sxs-lookup"><span data-stu-id="11f1d-161">ASP.NET request rate</span></span> |<span data-ttu-id="11f1d-162">Скорость всех запросов toohello приложение в секунду из ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="11f1d-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="11f1d-163">Ошибки зависимости</span><span class="sxs-lookup"><span data-stu-id="11f1d-163">Dependency failures</span></span> |<span data-ttu-id="11f1d-164">Количество неудачных вызовов, сделанных ресурсы tooexternal hello сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="11f1d-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="11f1d-165">Время ответа от сервера</span><span class="sxs-lookup"><span data-stu-id="11f1d-165">Server response time</span></span> |<span data-ttu-id="11f1d-166">Время между получения HTTP-запроса и завершением отправки ответа hello.</span><span class="sxs-lookup"><span data-stu-id="11f1d-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="11f1d-167">Частота запросов</span><span class="sxs-lookup"><span data-stu-id="11f1d-167">Request rate</span></span> |<span data-ttu-id="11f1d-168">Частота всех запросов, toohello приложение в секунду.</span><span class="sxs-lookup"><span data-stu-id="11f1d-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="11f1d-169">Failed requests (Неудачные запросы)</span><span class="sxs-lookup"><span data-stu-id="11f1d-169">Failed requests</span></span> |<span data-ttu-id="11f1d-170">Число HTTP-запросов, приведших к отображению кода ответа >= 400.</span><span class="sxs-lookup"><span data-stu-id="11f1d-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="11f1d-171">Просмотры страниц</span><span class="sxs-lookup"><span data-stu-id="11f1d-171">Page views</span></span> |<span data-ttu-id="11f1d-172">Количество клиентских запросов пользователя для веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="11f1d-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="11f1d-173">Искусственный трафик отфильтровывается.</span><span class="sxs-lookup"><span data-stu-id="11f1d-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="11f1d-174">{имя пользовательской метрики}</span><span class="sxs-lookup"><span data-stu-id="11f1d-174">{your custom metric name}</span></span> |<span data-ttu-id="11f1d-175">{имя метрики}</span><span class="sxs-lookup"><span data-stu-id="11f1d-175">{Your metric name}</span></span> |<span data-ttu-id="11f1d-176">Сообщаемые вашей значение метрики [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) или в hello [параметр измерения отслеживания вызова](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="11f1d-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="11f1d-177">метрики Hello не будут отправлены в разных телеметрии модули:</span><span class="sxs-lookup"><span data-stu-id="11f1d-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="11f1d-178">Группа метрик</span><span class="sxs-lookup"><span data-stu-id="11f1d-178">Metric group</span></span> | <span data-ttu-id="11f1d-179">Модуль сборщика</span><span class="sxs-lookup"><span data-stu-id="11f1d-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="11f1d-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="11f1d-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="11f1d-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="11f1d-181">clientPerformance,</span></span><br/><span data-ttu-id="11f1d-182">view</span><span class="sxs-lookup"><span data-stu-id="11f1d-182">view</span></span> |[<span data-ttu-id="11f1d-183">Browser JavaScript</span><span class="sxs-lookup"><span data-stu-id="11f1d-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="11f1d-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="11f1d-184">performanceCounter</span></span> |[<span data-ttu-id="11f1d-185">Производительность</span><span class="sxs-lookup"><span data-stu-id="11f1d-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="11f1d-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="11f1d-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="11f1d-187">Dependency</span><span class="sxs-lookup"><span data-stu-id="11f1d-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="11f1d-188">request,</span><span class="sxs-lookup"><span data-stu-id="11f1d-188">request,</span></span><br/><span data-ttu-id="11f1d-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="11f1d-189">requestFailed</span></span> |[<span data-ttu-id="11f1d-190">Server request</span><span class="sxs-lookup"><span data-stu-id="11f1d-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="11f1d-191">Объекты Webhook</span><span class="sxs-lookup"><span data-stu-id="11f1d-191">Webhooks</span></span>
<span data-ttu-id="11f1d-192">Вы можете [автоматизировать оповещения tooan ответ](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="11f1d-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="11f1d-193">При возникновении оповещения Azure будет вызывать выбранный вами веб-адрес.</span><span class="sxs-lookup"><span data-stu-id="11f1d-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="11f1d-194">См. также</span><span class="sxs-lookup"><span data-stu-id="11f1d-194">See also</span></span>
* [<span data-ttu-id="11f1d-195">Сценарий tooconfigure Application Insights</span><span class="sxs-lookup"><span data-stu-id="11f1d-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="11f1d-196">Создание ресурсов Application Insights и веб-тестов на основе шаблонов</span><span class="sxs-lookup"><span data-stu-id="11f1d-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="11f1d-197">Автоматизация взаимозависимость аналитики tooApplication системы диагностики Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="11f1d-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="11f1d-198">Автоматизация оповещения tooan ответа</span><span class="sxs-lookup"><span data-stu-id="11f1d-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
