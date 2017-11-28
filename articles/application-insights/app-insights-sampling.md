---
title: "Выборка данных телеметрии в Azure Application Insights | Документация Майкрософт"
description: "Как управлять объемом данных телеметрии."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: ceaeced414c9c302fba335b4578bcdcbfaef0410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="3c90c-103">Выборка в Application Insights</span><span class="sxs-lookup"><span data-stu-id="3c90c-103">Sampling in Application Insights</span></span>


<span data-ttu-id="3c90c-104">Выборка — это функция [Azure Application Insights](app-insights-overview.md),</span><span class="sxs-lookup"><span data-stu-id="3c90c-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="3c90c-105">которую мы рекомендуем использовать для сокращения трафика телеметрии и хранения. Эта функция также поддерживает статистически правильный анализ данных приложения.</span><span class="sxs-lookup"><span data-stu-id="3c90c-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="3c90c-106">Фильтр выбирает связанные элементы, позволяя переходить между ними при диагностике.</span><span class="sxs-lookup"><span data-stu-id="3c90c-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="3c90c-107">Отображаемые на портале счетчики метрик перенормированы с учетом выборки, чтобы их влияние на статистику было минимальным.</span><span class="sxs-lookup"><span data-stu-id="3c90c-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span></span>

<span data-ttu-id="3c90c-108">Выборка сокращает расходы, связанные с использованием трафика и данных, помогая избежать регулирования.</span><span class="sxs-lookup"><span data-stu-id="3c90c-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="3c90c-109">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="3c90c-109">In brief:</span></span>
* <span data-ttu-id="3c90c-110">Выборка сохраняет 1 в  *n*  записи и игнорирует остальные.</span><span class="sxs-lookup"><span data-stu-id="3c90c-110">Sampling retains 1 in *n* records and discards the rest.</span></span> <span data-ttu-id="3c90c-111">Например, при частоте выборки 20 % сохраняется 1 из 5 событий.</span><span class="sxs-lookup"><span data-stu-id="3c90c-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="3c90c-112">Если приложение отправляет большие объемы данных телеметрии, выборка происходит автоматически (в приложениях веб-сервера ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="3c90c-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="3c90c-113">Выборку можно также настроить вручную на портале на странице цен или в пакете SDK для ASP.NET в CONFIG-файле, что также позволяет сократить сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="3c90c-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span></span>
* <span data-ttu-id="3c90c-114">Если при регистрации пользовательских событий необходимо убедиться, что набор событий сохранен или отклонен полностью, проверьте, одинаковое ли у них значение идентификатора операции.</span><span class="sxs-lookup"><span data-stu-id="3c90c-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span></span>
* <span data-ttu-id="3c90c-115">Делитель выборки  *n*  сообщается в каждой записи в свойстве `itemCount`, которой в поиске отображается понятное имя «количество запросов» или «счетчик событий».</span><span class="sxs-lookup"><span data-stu-id="3c90c-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span></span> <span data-ttu-id="3c90c-116">Если выборка не выполняется, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="3c90c-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="3c90c-117">При написании запросов аналитики необходимо [учитывать выборку](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="3c90c-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="3c90c-118">В частности, вместо простого подсчета записей следует использовать функцию `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="3c90c-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="3c90c-119">Типы выборки</span><span class="sxs-lookup"><span data-stu-id="3c90c-119">Types of sampling</span></span>
<span data-ttu-id="3c90c-120">Существует три альтернативных метода выборки.</span><span class="sxs-lookup"><span data-stu-id="3c90c-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="3c90c-121">**Адаптивная выборка** автоматически корректирует объем данных телеметрии, отправляемых из пакета SDK в приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3c90c-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span></span> <span data-ttu-id="3c90c-122">По умолчанию используется SDK версии 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="3c90c-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="3c90c-123">Сейчас этот модуль доступен только в рамках серверной телеметрии ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3c90c-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="3c90c-124">**Выборка с фиксированной частотой** уменьшает объем данных телеметрии, отправляемых с сервера ASP.NET и из браузеров пользователей.</span><span class="sxs-lookup"><span data-stu-id="3c90c-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="3c90c-125">Частоту вы задаете сами.</span><span class="sxs-lookup"><span data-stu-id="3c90c-125">You set the rate.</span></span> <span data-ttu-id="3c90c-126">Благодаря тому, что клиент и сервер будут синхронизировать свои выборки, при поиске вы сможете перемещаться между связанными представлениями страниц и запросами.</span><span class="sxs-lookup"><span data-stu-id="3c90c-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="3c90c-127">**Выборка приема**, поддерживаемая на портале Azure,</span><span class="sxs-lookup"><span data-stu-id="3c90c-127">**Ingestion sampling** works in the Azure portal.</span></span> <span data-ttu-id="3c90c-128">отклоняет некоторые данные телеметрии, поступающие из приложения, с заданной скоростью.</span><span class="sxs-lookup"><span data-stu-id="3c90c-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="3c90c-129">Она не уменьшает трафик телеметрии, но помогает оставаться в пределах месячной квоты.</span><span class="sxs-lookup"><span data-stu-id="3c90c-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="3c90c-130">Существенное преимущество выборки приема заключается в том, что ее можно задать без повторного развертывания приложения и она работает одинаково для всех серверов и клиентов.</span><span class="sxs-lookup"><span data-stu-id="3c90c-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="3c90c-131">Если выполняется адаптивная или фиксированная выборка, выборка приема отключена.</span><span class="sxs-lookup"><span data-stu-id="3c90c-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="3c90c-132">Выборка приема</span><span class="sxs-lookup"><span data-stu-id="3c90c-132">Ingestion sampling</span></span>
<span data-ttu-id="3c90c-133">Этот вид выборки работает в точке, где данные телеметрии с веб-сервера, браузеров и устройств достигают конечной точки службы Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3c90c-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span></span> <span data-ttu-id="3c90c-134">Несмотря на то, что трафик телеметрии, отправляемой из приложения, такая выборка не уменьшает, она сокращает объем данных для обработки и сохранения в службе Application Insights, а значит и размер оплаты.</span><span class="sxs-lookup"><span data-stu-id="3c90c-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="3c90c-135">Используйте этот тип выборки, если ваше приложение часто выходит за рамки ежемесячной квоты, а возможности использовать один из типов выборки на основе SDK нет.</span><span class="sxs-lookup"><span data-stu-id="3c90c-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span></span> 

<span data-ttu-id="3c90c-136">Частота выборки задается в колонке квот и ценообразования:</span><span class="sxs-lookup"><span data-stu-id="3c90c-136">Set the sampling rate in the Quotas and Pricing blade:</span></span>

![В колонке общих сведений о приложении щелкните "Параметры", "Квота", "Выборки", выберите частоту выборки и щелкните "Обновить".](./media/app-insights-sampling/04.png)

<span data-ttu-id="3c90c-138">Как и в других типах выборки, алгоритм сохраняет связанные элементы телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-138">Like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="3c90c-139">Например, при проверке телеметрии в поиске это позволит найти запрос, связанный с определенным исключением.</span><span class="sxs-lookup"><span data-stu-id="3c90c-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> <span data-ttu-id="3c90c-140">Правильно сохраняются счетчики метрик, например частота запросов и частота исключений.</span><span class="sxs-lookup"><span data-stu-id="3c90c-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="3c90c-141">Точки данных, отклоненные выборкой, доступны не во всех функциях Application Insights, например [Непрерывный экспорт](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="3c90c-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="3c90c-142">Выборка приема не работает во время действия адаптивной или фиксированной выборки на основе пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="3c90c-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="3c90c-143">Если частота выборки в пакете SDK меньше 100 %, заданная частота выборки приема не учитывается.</span><span class="sxs-lookup"><span data-stu-id="3c90c-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="3c90c-144">Значение, отображаемое на плитке, обозначает значение, которое вы задали для выборки приема.</span><span class="sxs-lookup"><span data-stu-id="3c90c-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span></span> <span data-ttu-id="3c90c-145">Оно не отражает фактическую частоту выборки, если действует выборка пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="3c90c-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="3c90c-146">Адаптивная выборка на веб-сервере</span><span class="sxs-lookup"><span data-stu-id="3c90c-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="3c90c-147">Адаптивная выборка доступна в пакете SDK Application Insights для ASP.NET 2.0.0-beta3 или более поздней версии и по умолчанию включена.</span><span class="sxs-lookup"><span data-stu-id="3c90c-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="3c90c-148">Адаптивная выборка влияет на объем данных телеметрии, отправляемых в службу Application Insights из приложения веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="3c90c-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span></span> <span data-ttu-id="3c90c-149">Том автоматически настраивается на работу с заданным максимальным объемом трафика.</span><span class="sxs-lookup"><span data-stu-id="3c90c-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="3c90c-150">Он не работает с небольшими объемами данных телеметрии и не затрагивается при отладке приложения или веб-узла с низкой нагрузкой.</span><span class="sxs-lookup"><span data-stu-id="3c90c-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="3c90c-151">Для получения целевого тома некоторые формируемые данные телеметрии игнорируются.</span><span class="sxs-lookup"><span data-stu-id="3c90c-151">To achieve the target volume, some of the telemetry generated is discarded.</span></span> <span data-ttu-id="3c90c-152">Однако, как и в других типах выборки, алгоритм сохраняет связанные элементы телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-152">But like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="3c90c-153">Например, при проверке телеметрии в поиске это позволит найти запрос, связанный с определенным исключением.</span><span class="sxs-lookup"><span data-stu-id="3c90c-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> 

<span data-ttu-id="3c90c-154">Счетчики метрик, например частота запросов и частота исключений, корректируются с учетом частоты выборки, так что в обозревателе метрик отображаются приблизительно точные значения.</span><span class="sxs-lookup"><span data-stu-id="3c90c-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="3c90c-155">**Обновите пакеты NuGet своего проекта** до последней *предварительной* версии Application Insights. В обозревателе решений щелкните проект правой кнопкой мыши, выберите "Управление пакетами NuGet", установите флажок **Включить предварительные версии** и выполните поиск Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="3c90c-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="3c90c-156">В файле [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) можно настроить несколько параметров узла `AdaptiveSamplingTelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="3c90c-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="3c90c-157">Ниже представлены значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3c90c-157">The figures shown are the default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="3c90c-158">Целевая частота, к которой стремится адаптивный алгоритм **на каждом узле сервера**.</span><span class="sxs-lookup"><span data-stu-id="3c90c-158">The target rate that the adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="3c90c-159">Если веб-приложение выполняется на множестве узлов, нужно уменьшить это значение, чтобы не превышать целевую скорость трафика на портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3c90c-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="3c90c-160">Интервал повторного вычисления текущей частоты телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-160">The interval at which the current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="3c90c-161">Вычисление выполняется на основе скользящего среднего.</span><span class="sxs-lookup"><span data-stu-id="3c90c-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="3c90c-162">Вы можете сократить этот интервал, если наблюдаете неожиданные скачки данных телеметрии в сторону увеличения.</span><span class="sxs-lookup"><span data-stu-id="3c90c-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="3c90c-163">Время, по истечении которого можно снова снизить процент выборки для сбора меньшего объема данных после изменения значения процента выборки.</span><span class="sxs-lookup"><span data-stu-id="3c90c-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="3c90c-164">Время, по истечении которого можно снова увеличить процент выборки для сбора большего объема данных после изменения значения процента выборки.</span><span class="sxs-lookup"><span data-stu-id="3c90c-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="3c90c-165">Минимальное допустимое значение с учетом изменения процента выборки.</span><span class="sxs-lookup"><span data-stu-id="3c90c-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="3c90c-166">Максимальное допустимое значение с учетом изменения процента выборки.</span><span class="sxs-lookup"><span data-stu-id="3c90c-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="3c90c-167">Взвешенное значение, присваиваемое последнему значению при вычислении скользящего среднего.</span><span class="sxs-lookup"><span data-stu-id="3c90c-167">In the calculation of the moving average, the weight assigned to the most recent value.</span></span> <span data-ttu-id="3c90c-168">Используйте значение не больше 1.</span><span class="sxs-lookup"><span data-stu-id="3c90c-168">Use a value equal to or less than 1.</span></span> <span data-ttu-id="3c90c-169">Использование значений ниже рекомендуемых приводит к тому, что скорость реагирования алгоритма на резкие изменения замедляется.</span><span class="sxs-lookup"><span data-stu-id="3c90c-169">Smaller values make the algorithm less reactive to sudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="3c90c-170">Значение, назначенное сразу после запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="3c90c-170">The value assigned when the app has just started.</span></span> <span data-ttu-id="3c90c-171">Не снижайте это значение во время отладки.</span><span class="sxs-lookup"><span data-stu-id="3c90c-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="3c90c-172">Разделенный точкой с запятой список типов, которые не должны включаться в выборку.</span><span class="sxs-lookup"><span data-stu-id="3c90c-172">A semi-colon delimited list of types that you do not want to be sampled.</span></span> <span data-ttu-id="3c90c-173">Распознаваемые типы: Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="3c90c-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="3c90c-174">Передаются все экземпляры указанных типов; типы, которые не указаны, включаются в выборку.</span><span class="sxs-lookup"><span data-stu-id="3c90c-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="3c90c-175">Разделенный точкой с запятой список типов, которые должны включаться в выборку.</span><span class="sxs-lookup"><span data-stu-id="3c90c-175">A semi-colon delimited list of types that you want to be sampled.</span></span> <span data-ttu-id="3c90c-176">Распознаваемые типы: Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="3c90c-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="3c90c-177">Указанные типы включаются в выборку; все экземпляры других типов будут всегда передаваться.</span><span class="sxs-lookup"><span data-stu-id="3c90c-177">The specified types are sampled; all instances of the other types will always be transmitted.</span></span>


<span data-ttu-id="3c90c-178">Чтобы **отключить** адаптивную выборку, удалите узел AdaptiveSamplingTelemetryProcessor в файле applicationinsights-config.</span><span class="sxs-lookup"><span data-stu-id="3c90c-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="3c90c-179">Альтернатива: настройка адаптивной выборки в коде</span><span class="sxs-lookup"><span data-stu-id="3c90c-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="3c90c-180">Вместо настройки выборки в CONFIG-файле вы можете использовать код.</span><span class="sxs-lookup"><span data-stu-id="3c90c-180">Instead of adjusting sampling in the .config file, you can use code.</span></span> <span data-ttu-id="3c90c-181">Это позволяет указать функцию обратного вызова, которая вызывается каждый раз, когда производится повторная оценка частоты выборки.</span><span class="sxs-lookup"><span data-stu-id="3c90c-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span></span> <span data-ttu-id="3c90c-182">Это можно использовать, например, чтобы узнать, какая частота выборки используется.</span><span class="sxs-lookup"><span data-stu-id="3c90c-182">You could use this, for example, to find out what sampling rate is being used.</span></span>

<span data-ttu-id="3c90c-183">Удалите узел `AdaptiveSamplingTelemetryProcessor` из CONFIG-файла.</span><span class="sxs-lookup"><span data-stu-id="3c90c-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span></span>

<span data-ttu-id="3c90c-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="3c90c-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust the settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report the sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="3c90c-185">([Сведения о процессорах телеметрии](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="3c90c-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="3c90c-186">Включение выборки для веб-страниц с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="3c90c-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="3c90c-187">Вы можете настроить выборку с фиксированной частотой для веб-страниц с любого сервера.</span><span class="sxs-lookup"><span data-stu-id="3c90c-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="3c90c-188">При [настройке веб-страниц для Application Insights](app-insights-javascript.md) измените фрагмент, скачанный с портала Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3c90c-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span></span> <span data-ttu-id="3c90c-189">(В приложениях ASP.NET фрагменты обычно содержатся в _Layout.cshtml.)  Вставьте строку, похожую на `samplingPercentage: 10,`, перед ключом инструментирования:</span><span class="sxs-lookup"><span data-stu-id="3c90c-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="3c90c-190">В качестве процента выборки выберите значение в процентах, близкое к 100/N, где N — это целое число.</span><span class="sxs-lookup"><span data-stu-id="3c90c-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="3c90c-191">В настоящее время выборка не поддерживает другие значения.</span><span class="sxs-lookup"><span data-stu-id="3c90c-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="3c90c-192">Если вы также включите выборку с фиксированной частотой на сервере, выборка будет синхронизироваться между клиентом и сервером. Благодаря этому вы сможете перемещаться между связанными представлениями страниц и запросами в службе поиска.</span><span class="sxs-lookup"><span data-stu-id="3c90c-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="3c90c-193">Выборка с фиксированной частотой для веб-сайтов ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3c90c-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="3c90c-194">Выборка с фиксированной частотой уменьшает объем трафика, отправляемого с веб-сервера и веб-браузеров.</span><span class="sxs-lookup"><span data-stu-id="3c90c-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="3c90c-195">В отличие от адаптивной выборки объем данных уменьшается в фиксированном, заданном вами размере.</span><span class="sxs-lookup"><span data-stu-id="3c90c-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="3c90c-196">Выборки клиента и сервера синхронизируются, а связанные элементы сохраняются: например, просматривая представление странице в поиске, вы всегда сможете найти соответствующий ему запрос.</span><span class="sxs-lookup"><span data-stu-id="3c90c-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="3c90c-197">Алгоритм выборки сохраняет связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="3c90c-197">The sampling algorithm retains related items.</span></span> <span data-ttu-id="3c90c-198">При каждом событии HTTP-запроса он и связанные с ним события игнорируются или передаются.</span><span class="sxs-lookup"><span data-stu-id="3c90c-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="3c90c-199">В обозревателе метрик такие параметры, как счетчики запросов и исключений, умножаются на коэффициент, компенсирующий частоту выборки, что позволяет получать примерно точные значения.</span><span class="sxs-lookup"><span data-stu-id="3c90c-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="3c90c-200">**Обновите пакеты NuGet проекта** до последней *предварительной* версии Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3c90c-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="3c90c-201">В обозревателе решений щелкните проект правой кнопкой мыши, выберите «Управление пакетами NuGet», установите флажок **Включить предварительный выпуск** и выполните поиск Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="3c90c-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="3c90c-202">**Отключите адаптивную выборку.** В файле [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) удалите или преобразуйте в комментарий узел `AdaptiveSamplingTelemetryProcessor`.</span><span class="sxs-lookup"><span data-stu-id="3c90c-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="3c90c-203">**Включите модуль выборки с фиксированной частотой.**</span><span class="sxs-lookup"><span data-stu-id="3c90c-203">**Enable the fixed-rate sampling module.**</span></span> <span data-ttu-id="3c90c-204">Добавьте этот фрагмент кода в файл [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="3c90c-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="3c90c-205">В качестве процента выборки выберите значение в процентах, близкое к 100/N, где N — это целое число.</span><span class="sxs-lookup"><span data-stu-id="3c90c-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="3c90c-206">В настоящее время выборка не поддерживает другие значения.</span><span class="sxs-lookup"><span data-stu-id="3c90c-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="3c90c-207">Альтернатива: включение выборки с фиксированной частотой в коде сервера</span><span class="sxs-lookup"><span data-stu-id="3c90c-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="3c90c-208">Вы можете использовать код и не задавать параметр выборки в CONFIG-файле.</span><span class="sxs-lookup"><span data-stu-id="3c90c-208">Instead of setting the sampling parameter in the .config file, you can use code.</span></span> 

<span data-ttu-id="3c90c-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="3c90c-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="3c90c-210">([Сведения о процессорах телеметрии](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="3c90c-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-to-use-sampling"></a><span data-ttu-id="3c90c-211">Когда следует использовать выборку?</span><span class="sxs-lookup"><span data-stu-id="3c90c-211">When to use sampling?</span></span>
<span data-ttu-id="3c90c-212">Адаптивная выборка включается автоматически, если используется пакет SDK для ASP.NET 2.0.0-beta3 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="3c90c-213">Выборку приема (на наших серверах) можно применять независимо от используемой версии SDK.</span><span class="sxs-lookup"><span data-stu-id="3c90c-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="3c90c-214">Выборка не требуется для большинства приложений малого и среднего размера.</span><span class="sxs-lookup"><span data-stu-id="3c90c-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="3c90c-215">Наиболее полезные диагностические сведения и наиболее точную статистику можно получить, собирая данные обо всех действиях пользователей.</span><span class="sxs-lookup"><span data-stu-id="3c90c-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="3c90c-216">Основные преимущества выборки:</span><span class="sxs-lookup"><span data-stu-id="3c90c-216">The main advantages of sampling are:</span></span>

* <span data-ttu-id="3c90c-217">Служба Application Insights удаляет («регулирует») точки данных, когда приложение слишком часто отправляет данные телеметрии за короткий интервал времени.</span><span class="sxs-lookup"><span data-stu-id="3c90c-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="3c90c-218">Вы остаетесь в пределах [квоты](app-insights-pricing.md) на точки данных для своей ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="3c90c-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="3c90c-219">Вам нужно сократить сетевой трафик, который тратится на сбор данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-219">To reduce network traffic from the collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="3c90c-220">Какой тип выборки следует использовать?</span><span class="sxs-lookup"><span data-stu-id="3c90c-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="3c90c-221">**Используйте выборку приема, если:**</span><span class="sxs-lookup"><span data-stu-id="3c90c-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="3c90c-222">Вы часто превышаете ежемесячную квоту телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="3c90c-223">Вы используете версию пакета SDK, которая не поддерживает выборки, например, более раннюю версию пакета SDK для Java или ASP.NET, чем версия 2.</span><span class="sxs-lookup"><span data-stu-id="3c90c-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="3c90c-224">Вы получаете много данных телеметрии с веб-браузеров пользователей.</span><span class="sxs-lookup"><span data-stu-id="3c90c-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="3c90c-225">**Используйте выборку с фиксированной частотой, если:**</span><span class="sxs-lookup"><span data-stu-id="3c90c-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="3c90c-226">Вы используете пакет SDK Application Insights для веб-служб ASP.NET 2.0.0 или более поздней версии; и</span><span class="sxs-lookup"><span data-stu-id="3c90c-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="3c90c-227">Вам нужна синхронизированная выборка между клиентом и сервером, которая позволяет перемещаться между связанными событиями на стороне клиента и сервера (такими, как просмотры страниц и HTTP-запросы) при использовании [службы поиска](app-insights-diagnostic-search.md)в ходе анализа событий.</span><span class="sxs-lookup"><span data-stu-id="3c90c-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="3c90c-228">Вам нужна уверенность в выборе соответствующего процента выборки для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="3c90c-228">You are confident of the appropriate sampling percentage for your app.</span></span> <span data-ttu-id="3c90c-229">Он должен быть достаточно высоким, чтобы получить точные метрики и при этом не превышать ценовую квоту и ограничения регулирования.</span><span class="sxs-lookup"><span data-stu-id="3c90c-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span></span> 

<span data-ttu-id="3c90c-230">**Используйте адаптивную выборку:**</span><span class="sxs-lookup"><span data-stu-id="3c90c-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="3c90c-231">В противном случае мы рекомендуем использовать адаптивную выборку.</span><span class="sxs-lookup"><span data-stu-id="3c90c-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="3c90c-232">В SDK сервера ASP.NET 2.0.0-beta3 или более поздней версии она включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3c90c-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="3c90c-233">Такая выборка не уменьшает трафик, не превышающий определенный минимальный объем, и не влияет на сайты, которые используются редко.</span><span class="sxs-lookup"><span data-stu-id="3c90c-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="3c90c-234">Как узнать, действует ли выборка</span><span class="sxs-lookup"><span data-stu-id="3c90c-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="3c90c-235">Чтобы узнать фактическую частоту выборки (где бы она ни применялась), выполните такой [запрос аналитики](app-insights-analytics.md) :</span><span class="sxs-lookup"><span data-stu-id="3c90c-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="3c90c-236">Для каждой сохранившейся записи `itemCount` обозначает число исходных записей, которые эта запись представляет (1 + число предыдущих удаленных записей).</span><span class="sxs-lookup"><span data-stu-id="3c90c-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="3c90c-237">Как работает функция выборки?</span><span class="sxs-lookup"><span data-stu-id="3c90c-237">How does sampling work?</span></span>
<span data-ttu-id="3c90c-238">Выборка с фиксированной частотой и адаптивная выборка — это компонент пакета SDK в ASP.NET 2.0.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="3c90c-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="3c90c-239">Выборка приема — это компонент службы Application Insights. Она может работать, даже если пакет SDK не выполняет выборку.</span><span class="sxs-lookup"><span data-stu-id="3c90c-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span></span> 

<span data-ttu-id="3c90c-240">Алгоритм выборки решает, какие элементы телеметрии необходимо удалить, а какие сохранить (как в пакете SDK, так и в службе Application Insights).</span><span class="sxs-lookup"><span data-stu-id="3c90c-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span></span> <span data-ttu-id="3c90c-241">Решение выборки основано на нескольких правилах, цель которых — сохранение всех точек взаимосвязанных данных без изменений, а также реализация функции диагностики в Application Insights даже с использованием сокращенного набора данных.</span><span class="sxs-lookup"><span data-stu-id="3c90c-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="3c90c-242">Например, если для неудачно завершенного запроса приложение отправляет дополнительные элементы телеметрии (например, исключение и трассировки, зарегистрированные этим запросом), выборка не будет разделять этот запрос и другие данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="3c90c-243">Она либо сохраняет, либо удаляет все элементы вместе.</span><span class="sxs-lookup"><span data-stu-id="3c90c-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="3c90c-244">Поэтому при просмотре сведений о запросе в Application Insights вы всегда будете видеть запрос вместе со связанными элементами телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span></span> 

<span data-ttu-id="3c90c-245">Для приложений, которые определяют пользователя (т. е. наиболее типичных веб-приложений), решение выборки основывается на хэше идентификатора пользователя. Это означает, что все данные телеметрии для конкретного пользователя либо сохраняются, либо удаляются.</span><span class="sxs-lookup"><span data-stu-id="3c90c-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="3c90c-246">Для типов приложений, которые не определяют пользователей (например, веб-службы), решение выборки основывается на идентификаторе операции запроса.</span><span class="sxs-lookup"><span data-stu-id="3c90c-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span></span> <span data-ttu-id="3c90c-247">Наконец, для элементов телеметрии, у которых нет ни идентификатора пользователя, ни идентификатора операции (например, элементы телеметрии, включенные в отчет по асинхронным потокам без контекста HTTP), выборка будет просто собирать определенный процент элементов телеметрии каждого типа.</span><span class="sxs-lookup"><span data-stu-id="3c90c-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="3c90c-248">Представляя вам данные телеметрии, служба Application Insights корректирует метрики в соответствии с процентом выборки, который использовался во время сбора. Это делается, чтобы компенсировать отсутствующие точки данных.</span><span class="sxs-lookup"><span data-stu-id="3c90c-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span></span> <span data-ttu-id="3c90c-249">Следовательно, при просмотре данных телеметрии в Application Insights пользователи видят статистически правильные приблизительные значения, очень близкие к реальным цифрам.</span><span class="sxs-lookup"><span data-stu-id="3c90c-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span></span>

<span data-ttu-id="3c90c-250">Точность приблизительного значения в значительной степени зависит от заданного процента выборки.</span><span class="sxs-lookup"><span data-stu-id="3c90c-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span></span> <span data-ttu-id="3c90c-251">Кроме того, точность возрастает для приложений, обрабатывающих большой объем сходных запросов от большого количества пользователей.</span><span class="sxs-lookup"><span data-stu-id="3c90c-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="3c90c-252">С другой стороны, для приложений, которые не работают с существенной нагрузкой, выборка не требуется, так как такие приложения обычно могут отправлять все данные телеметрии, не выходя за пределы квоты и не вызывая потерю данных в результате регулирования.</span><span class="sxs-lookup"><span data-stu-id="3c90c-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="3c90c-253">Обратите внимание, что служба Application Insights не выполняет выборку типов данных телеметрии, представленных метриками и сеансами, так как снижение точности для этих типов может быть весьма нежелательным.</span><span class="sxs-lookup"><span data-stu-id="3c90c-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="3c90c-254">Адаптивная выборка</span><span class="sxs-lookup"><span data-stu-id="3c90c-254">Adaptive sampling</span></span>
<span data-ttu-id="3c90c-255">Адаптивная выборка добавляет компонент, который отслеживает текущую скорость передачи данных из пакета SDK и корректирует процент выборки, чтобы оставаться в пределах целевой максимальной скорости.</span><span class="sxs-lookup"><span data-stu-id="3c90c-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span></span> <span data-ttu-id="3c90c-256">Корректировка пересчитывается через регулярные интервалы времени в зависимости от скользящего среднего для скорости исходящей передачи.</span><span class="sxs-lookup"><span data-stu-id="3c90c-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span></span>

## <a name="sampling-and-the-javascript-sdk"></a><span data-ttu-id="3c90c-257">Выборка и пакет SDK для JavaScript</span><span class="sxs-lookup"><span data-stu-id="3c90c-257">Sampling and the JavaScript SDK</span></span>
<span data-ttu-id="3c90c-258">Пакет SDK клиента (JavaScript) участвует в выборке с фиксированной частотой в сочетании с серверным пакетом SDK.</span><span class="sxs-lookup"><span data-stu-id="3c90c-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span></span> <span data-ttu-id="3c90c-259">Инструментированные страницы отправляют данные телеметрии клиента только от тех пользователей, которых сервер включил в выборку.</span><span class="sxs-lookup"><span data-stu-id="3c90c-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span></span> <span data-ttu-id="3c90c-260">Такая логика обеспечивает непрерывность сеанса пользователя как на клиенте, так и на сервере.</span><span class="sxs-lookup"><span data-stu-id="3c90c-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="3c90c-261">Благодаря этому с помощью любого элемента телеметрии в Application Insights можно найти все остальные элементы телеметрии для этого пользователя или сеанса.</span><span class="sxs-lookup"><span data-stu-id="3c90c-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="3c90c-262">*Данные телеметрии на клиенте и сервере не отображают скоординированные образцы, как описано выше.*</span><span class="sxs-lookup"><span data-stu-id="3c90c-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="3c90c-263">Убедитесь в том, что выборка с фиксированной частотой включена и на сервере, и в клиенте.</span><span class="sxs-lookup"><span data-stu-id="3c90c-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="3c90c-264">Убедитесь в том, что используется пакет SDK версии 2.0 или выше.</span><span class="sxs-lookup"><span data-stu-id="3c90c-264">Make sure that the SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="3c90c-265">Проверьте, указан ли процент выборки на клиенте и сервере.</span><span class="sxs-lookup"><span data-stu-id="3c90c-265">Check that you set the same sampling percentage in both the client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="3c90c-266">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="3c90c-266">Frequently Asked Questions</span></span>
<span data-ttu-id="3c90c-267">*Почему выборка — это не простой сбор X процентов данных телеметрии каждого типа?*</span><span class="sxs-lookup"><span data-stu-id="3c90c-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="3c90c-268">Хотя такой подход к выборке обеспечил бы очень высокую точность в приблизительных значениях метрик, он не позволит сопоставлять диагностические данные для каждого пользователя, сеанса и запроса, что является критически важным для диагностики.</span><span class="sxs-lookup"><span data-stu-id="3c90c-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="3c90c-269">Поэтому выборку лучше всего описать как «сбор всех элементов телеметрии для X процентов пользователей приложения» или «сбор всех данных телеметрии для X процентов запросов приложения».</span><span class="sxs-lookup"><span data-stu-id="3c90c-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="3c90c-270">Для элементов телеметрии, не связанных с запросами (включая асинхронную фоновую обработку), альтернативным вариантом является сбор X процентов всех элементов для данных телеметрии каждого типа.</span><span class="sxs-lookup"><span data-stu-id="3c90c-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="3c90c-271">*Может ли процент выборки меняться со временем?*</span><span class="sxs-lookup"><span data-stu-id="3c90c-271">*Can the sampling percentage change over time?*</span></span>

* <span data-ttu-id="3c90c-272">Да, адаптивная выборка постепенно меняет процент выборки в зависимости от текущего объема данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span></span>

<span data-ttu-id="3c90c-273">*Если я использую выборку с фиксированной частотой, как узнать, какой процент выборки будет оптимальным для моего приложения?*</span><span class="sxs-lookup"><span data-stu-id="3c90c-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span></span>

* <span data-ttu-id="3c90c-274">Один из способов — начать с адаптивной выборки, узнать подобранную частоту (см. вопрос выше) и переключиться на выборку с этой фиксированной частотой.</span><span class="sxs-lookup"><span data-stu-id="3c90c-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="3c90c-275">В противном случае придется только угадывать.</span><span class="sxs-lookup"><span data-stu-id="3c90c-275">Otherwise, you have to guess.</span></span> <span data-ttu-id="3c90c-276">Анализируйте текущее использование телеметрии в AI, наблюдайте осуществляемое регулирование и оценивайте объем собранных данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span></span> <span data-ttu-id="3c90c-277">Эти три фактора в сочетании с выбранной ценовой категорией позволяют оценить объем собранных данных телеметрии, который может потребоваться сократить.</span><span class="sxs-lookup"><span data-stu-id="3c90c-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span></span> <span data-ttu-id="3c90c-278">Однако увеличение числа пользователей или некоторые другие факторы, меняющие объем данных телеметрии, могут сделать оценку недействительной.</span><span class="sxs-lookup"><span data-stu-id="3c90c-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="3c90c-279">*Что произойдет, если настроить слишком низкий процент выборки?*</span><span class="sxs-lookup"><span data-stu-id="3c90c-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="3c90c-280">Слишком низкий процент выборки (излишне агрессивная выборка) снижает точность приблизительных значений, когда служба Application Insights пытается компенсировать отображение данных для сокращения объема данных.</span><span class="sxs-lookup"><span data-stu-id="3c90c-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span></span> <span data-ttu-id="3c90c-281">Кроме того, это может отрицательно повлиять на функцию диагностики, так как в выборку могут не попасть некоторые редкие сбои или медленные запросы.</span><span class="sxs-lookup"><span data-stu-id="3c90c-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="3c90c-282">*Что произойдет, если настроить слишком высокий процент выборки?*</span><span class="sxs-lookup"><span data-stu-id="3c90c-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="3c90c-283">Слишком высокий процент выборки (недостаточно агрессивная выборка) приводит к недостаточному снижению объема собранных данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3c90c-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span></span> <span data-ttu-id="3c90c-284">У вас по-прежнему может наблюдаться потеря данных телеметрии, связанная с регулированием, а затраты на использование Application Insights могут быть выше запланированных из-за избыточных расходов.</span><span class="sxs-lookup"><span data-stu-id="3c90c-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span></span>

<span data-ttu-id="3c90c-285">*На каких платформах можно использовать выборку?*</span><span class="sxs-lookup"><span data-stu-id="3c90c-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="3c90c-286">Выборка приема может выполняться автоматически, когда объем данных телеметрии превышает определенный порог, если пакет SDK не выполняет выборку.</span><span class="sxs-lookup"><span data-stu-id="3c90c-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span></span> <span data-ttu-id="3c90c-287">Она будет работать, например, если приложение использует сервер Java или если вы используете старую версию пакета SDK для ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3c90c-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span></span>
* <span data-ttu-id="3c90c-288">Если вы используете пакет SDK ASP.NET 2.0.0 и более поздних версий (размещенный в Azure или на собственном сервере), адаптивная выборка работает по умолчанию, однако вы можете перейти на выборку с фиксированной частотой, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="3c90c-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span></span> <span data-ttu-id="3c90c-289">При выборке с фиксированной частотой пакет SDK браузера выполняет автоматическую синхронизацию с событиями, связанными с выборкой.</span><span class="sxs-lookup"><span data-stu-id="3c90c-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span></span> 

<span data-ttu-id="3c90c-290">*Есть определенные редкие события, которые я всегда хочу просматривать. Как сделать так, чтобы модуль выборки не отфильтровывал их?*</span><span class="sxs-lookup"><span data-stu-id="3c90c-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span></span>

* <span data-ttu-id="3c90c-291">Инициализируете отдельный экземпляр TelemetryClient с новой конфигурацией TelemetryConfiguration (не активной по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="3c90c-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span></span> <span data-ttu-id="3c90c-292">Используйте его для отправки редких событий.</span><span class="sxs-lookup"><span data-stu-id="3c90c-292">Use that to send your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c90c-293">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c90c-293">Next steps</span></span>
* <span data-ttu-id="3c90c-294">[Фильтрация](app-insights-api-filtering-sampling.md) может обеспечивать более строгий контроль над данными, отправляемыми пакетом SDK.</span><span class="sxs-lookup"><span data-stu-id="3c90c-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

