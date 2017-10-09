---
title: "aaaTelemetry выборки в Azure Application Insights | Документы Microsoft"
description: "Как tookeep hello объем телеметрии в группе управления."
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
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="b715e-103">Выборка в Application Insights</span><span class="sxs-lookup"><span data-stu-id="b715e-103">Sampling in Application Insights</span></span>


<span data-ttu-id="b715e-104">Выборка — это функция [Azure Application Insights](app-insights-overview.md),</span><span class="sxs-lookup"><span data-stu-id="b715e-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b715e-105">Он является hello рекомендуется способом tooreduce телеметрии трафика и хранения данных, сохраняя статистически правильный анализ данных приложений.</span><span class="sxs-lookup"><span data-stu-id="b715e-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="b715e-106">Фильтр Hello выбирает элементы, которые связаны с другими, чтобы переходить между элементами, при выполнении диагностики исследования.</span><span class="sxs-lookup"><span data-stu-id="b715e-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="b715e-107">Если метрики счетчиков должны быть представлены tooyou в портал hello, они являются повторно нормализованный tootake учетную запись выборки toominimize любой влияет на статистику hello hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="b715e-108">Выборка сокращает расходы, связанные с использованием трафика и данных, помогая избежать регулирования.</span><span class="sxs-lookup"><span data-stu-id="b715e-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="b715e-109">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="b715e-109">In brief:</span></span>
* <span data-ttu-id="b715e-110">Выборка сохраняет 1 в  *n*  записывает и отменяет hello rest.</span><span class="sxs-lookup"><span data-stu-id="b715e-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="b715e-111">Например, при частоте выборки 20 % сохраняется 1 из 5 событий.</span><span class="sxs-lookup"><span data-stu-id="b715e-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="b715e-112">Если приложение отправляет большие объемы данных телеметрии, выборка происходит автоматически (в приложениях веб-сервера ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="b715e-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="b715e-113">Можно также задать выборки вручную, либо в hello портала на странице; цен hello или в hello пакета SDK для ASP.NET в файл .config hello tooalso сократить сетевой трафик hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="b715e-114">Если журнала пользовательских событий, и вы хотите toomake набор событий, либо сохранить, иначе удаляются вместе, убедитесь, что они имеют hello одинаковое значение идентификатором операции.</span><span class="sxs-lookup"><span data-stu-id="b715e-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="b715e-115">делитель выборки Hello  *n*  сообщается в каждой записи в свойстве hello `itemCount`, которой поиска отображается в узле hello понятное имя «количество запросов» или «счетчик событий».</span><span class="sxs-lookup"><span data-stu-id="b715e-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="b715e-116">Если выборка не выполняется, `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="b715e-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="b715e-117">При написании запросов аналитики необходимо [учитывать выборку](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="b715e-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="b715e-118">В частности, вместо простого подсчета записей следует использовать функцию `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="b715e-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="b715e-119">Типы выборки</span><span class="sxs-lookup"><span data-stu-id="b715e-119">Types of sampling</span></span>
<span data-ttu-id="b715e-120">Существует три альтернативных метода выборки.</span><span class="sxs-lookup"><span data-stu-id="b715e-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="b715e-121">**Адаптивная выборки** автоматически корректирует hello объем телеметрии, отправленные hello SDK в приложении ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b715e-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="b715e-122">По умолчанию используется SDK версии 2.0.0-beta3.</span><span class="sxs-lookup"><span data-stu-id="b715e-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="b715e-123">Сейчас этот модуль доступен только в рамках серверной телеметрии ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b715e-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="b715e-124">**Выборка-rate** уменьшает hello объем телеметрии, отправленные с сервер ASP.NET из браузеров пользователей.</span><span class="sxs-lookup"><span data-stu-id="b715e-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="b715e-125">Можно задать скорость hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-125">You set hello rate.</span></span> <span data-ttu-id="b715e-126">Hello клиента и сервера будет синхронизировать их выборки, что, в поиск, можно перемещаться между связанной страницы представлений и запросов.</span><span class="sxs-lookup"><span data-stu-id="b715e-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="b715e-127">**Выборка приема** работает в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b715e-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="b715e-128">Он сбрасывает некоторые данные телеметрии hello, поступившего от приложения, с частотой, устанавливаемое.</span><span class="sxs-lookup"><span data-stu-id="b715e-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="b715e-129">Она не уменьшает трафик телеметрии, но помогает оставаться в пределах месячной квоты.</span><span class="sxs-lookup"><span data-stu-id="b715e-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="b715e-130">большим преимуществом Hello приема выборки — может быть задана без повторного развертывания приложения, что он работает одинаково для всех серверов и клиентов.</span><span class="sxs-lookup"><span data-stu-id="b715e-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="b715e-131">Если выполняется адаптивная или фиксированная выборка, выборка приема отключена.</span><span class="sxs-lookup"><span data-stu-id="b715e-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="b715e-132">Выборка приема</span><span class="sxs-lookup"><span data-stu-id="b715e-132">Ingestion sampling</span></span>
<span data-ttu-id="b715e-133">Эта форма выборки работает в hello точке, где hello телеметрии из вашего веб-сервера, браузерах и устройствах достигает конечной точки службы Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="b715e-134">Несмотря на то, что он не уменьшить трафик телеметрии hello, отправляемых из приложения, он приводит к уменьшению объема hello обработки и хранения (и оплачивать) с Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b715e-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="b715e-135">Используйте этот тип выборки, если приложение часто проходит над его месячной квоты и у вас нет hello возможность использовать один из типов на основе пакета SDK для hello выборки.</span><span class="sxs-lookup"><span data-stu-id="b715e-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="b715e-136">Задать частоту выборки hello в hello квоты и колонки цены:</span><span class="sxs-lookup"><span data-stu-id="b715e-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![Из колонки Обзор приложения hello нажмите кнопку Параметры, квоты, образцы, выберите частоту выборки и нажмите кнопку обновления.](./media/app-insights-sampling/04.png)

<span data-ttu-id="b715e-138">Как и другие виды выборки hello алгоритм сохраняет телеметрии связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="b715e-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="b715e-139">Например, если анализ телеметрии hello в поиск, можно будет toofind hello запроса связанных tooa конкретного исключения.</span><span class="sxs-lookup"><span data-stu-id="b715e-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="b715e-140">Правильно сохраняются счетчики метрик, например частота запросов и частота исключений.</span><span class="sxs-lookup"><span data-stu-id="b715e-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="b715e-141">Точки данных, отклоненные выборкой, доступны не во всех функциях Application Insights, например [Непрерывный экспорт](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="b715e-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="b715e-142">Выборка приема не работает во время действия адаптивной или фиксированной выборки на основе пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="b715e-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="b715e-143">Если частота выборки hello hello SDK менее 100%, то hello приема частоту выборки, устанавливаемое игнорируется.</span><span class="sxs-lookup"><span data-stu-id="b715e-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="b715e-144">значение Hello, отображаются на плитке hello указывает значение hello, настроенной для приема выборки.</span><span class="sxs-lookup"><span data-stu-id="b715e-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="b715e-145">Если пакет SDK для выборки в операции, он не представляет hello фактическое дискретизации.</span><span class="sxs-lookup"><span data-stu-id="b715e-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="b715e-146">Адаптивная выборка на веб-сервере</span><span class="sxs-lookup"><span data-stu-id="b715e-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="b715e-147">Адаптивная выборки доступен для hello пакет SDK Application Insights для ASP.NET v 2.0.0-beta3 и более поздних версий и включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b715e-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="b715e-148">Адаптивная выборки влияет hello объем телеметрии, отправленные вашей toohello приложения web server служба Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b715e-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="b715e-149">Hello тома регулируется автоматически tookeep в пределах указанной максимальной скорости трафика.</span><span class="sxs-lookup"><span data-stu-id="b715e-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="b715e-150">Он не работает с небольшими объемами данных телеметрии и не затрагивается при отладке приложения или веб-узла с низкой нагрузкой.</span><span class="sxs-lookup"><span data-stu-id="b715e-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="b715e-151">tooachieve hello целевой том, некоторые из созданных телеметрии hello отбрасывается.</span><span class="sxs-lookup"><span data-stu-id="b715e-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="b715e-152">Но как другие типы выборки, алгоритм hello сохраняет телеметрии связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="b715e-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="b715e-153">Например, если анализ телеметрии hello в поиск, можно будет toofind hello запроса связанных tooa конкретного исключения.</span><span class="sxs-lookup"><span data-stu-id="b715e-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="b715e-154">Метрика подсчитывает, таких как частота запросов и частоты исключений скорректированное toocompensate для hello, частоту выборки, чтобы они отображали приблизительно правильные значения в обозревателе метрику.</span><span class="sxs-lookup"><span data-stu-id="b715e-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="b715e-155">**Обновление проекта NuGet** последние пакеты toohello *предварительного выпуска* версии Application Insights: щелкните правой кнопкой мыши проект hello в обозревателе решений, выберите Управление пакетами NuGet проверьте **Include Предварительная** и выполните поиск Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="b715e-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="b715e-156">В [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), можно настроить несколько параметров в hello `AdaptiveSamplingTelemetryProcessor` узла.</span><span class="sxs-lookup"><span data-stu-id="b715e-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="b715e-157">фигуры Hello показано являются значениями по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="b715e-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="b715e-158">Hello целевой скорость, с которой hello адаптивный алгоритм стремится к тому, **на каждом узле сервера**.</span><span class="sxs-lookup"><span data-stu-id="b715e-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="b715e-159">Если веб-приложение работает на множестве узлов, так, чтобы tooremain внутри вашей целевой интенсивность трафика на портале Application Insights hello Уменьшите это значение.</span><span class="sxs-lookup"><span data-stu-id="b715e-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="b715e-160">Интервал приветствия, на какие hello текущая скорость телеметрии повторного вычисления.</span><span class="sxs-lookup"><span data-stu-id="b715e-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="b715e-161">Вычисление выполняется на основе скользящего среднего.</span><span class="sxs-lookup"><span data-stu-id="b715e-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="b715e-162">Может потребоваться tooshorten этот интервал в случае ответственность toosudden пакетами телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b715e-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="b715e-163">При изменении значения выборки в процентах, как скоро после мы допускается toolower выборки в процентах снова toocapture меньше данных.</span><span class="sxs-lookup"><span data-stu-id="b715e-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="b715e-164">При изменении значения выборки в процентах, как скоро после мы допускается tooincrease выборки в процентах снова toocapture больше данных.</span><span class="sxs-lookup"><span data-stu-id="b715e-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="b715e-165">Как меняется выборки в процентах, какова минимальное значение hello мы разрешены tooset.</span><span class="sxs-lookup"><span data-stu-id="b715e-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="b715e-166">Как меняется выборки в процентах, Каково максимальное значение hello мы разрешены tooset.</span><span class="sxs-lookup"><span data-stu-id="b715e-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="b715e-167">При расчете hello hello скользящее среднее вес hello назначить toohello самое последнее значение.</span><span class="sxs-lookup"><span data-stu-id="b715e-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="b715e-168">Используйте tooor равно значение меньше 1.</span><span class="sxs-lookup"><span data-stu-id="b715e-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="b715e-169">Меньшие значения изменять алгоритм hello менее toosudden.</span><span class="sxs-lookup"><span data-stu-id="b715e-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="b715e-170">Hello значение, заданное при запуске приложение hello просто.</span><span class="sxs-lookup"><span data-stu-id="b715e-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="b715e-171">Не снижайте это значение во время отладки.</span><span class="sxs-lookup"><span data-stu-id="b715e-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="b715e-172">Список типов, которые не нужно toobe выборки, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="b715e-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="b715e-173">Распознаваемые типы: Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="b715e-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="b715e-174">Все экземпляры hello указало при передаче типов; проверит Hello типов, которые не указаны.</span><span class="sxs-lookup"><span data-stu-id="b715e-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="b715e-175">Список типов, которые вы хотите toobe выборки, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="b715e-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="b715e-176">Распознаваемые типы: Dependency, Event, Exception, PageView, Request, Trace.</span><span class="sxs-lookup"><span data-stu-id="b715e-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="b715e-177">Hello задан, проверяются типы; все экземпляры служб hello других типов всегда будет передаваться.</span><span class="sxs-lookup"><span data-stu-id="b715e-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="b715e-178">**tooswitch отключение** адаптивной выборки, удалить hello AdaptiveSamplingTelemetryProcessor узел из конфигурации applicationinsights.</span><span class="sxs-lookup"><span data-stu-id="b715e-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="b715e-179">Альтернатива: настройка адаптивной выборки в коде</span><span class="sxs-lookup"><span data-stu-id="b715e-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="b715e-180">Вместо настройки выборки в config-файле hello, можно использовать код.</span><span class="sxs-lookup"><span data-stu-id="b715e-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="b715e-181">Это позволяет toospecify функцию обратного вызова, который вызывается каждый раз, когда производится повторная оценка частоты выборки hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="b715e-182">Это можно использовать, например, используется toofind out какие частоту выборки.</span><span class="sxs-lookup"><span data-stu-id="b715e-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="b715e-183">Удалите hello `AdaptiveSamplingTelemetryProcessor` узел из hello config-файла.</span><span class="sxs-lookup"><span data-stu-id="b715e-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="b715e-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="b715e-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

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
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="b715e-185">([Сведения о процессорах телеметрии](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="b715e-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="b715e-186">Включение выборки для веб-страниц с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="b715e-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="b715e-187">Вы можете настроить выборку с фиксированной частотой для веб-страниц с любого сервера.</span><span class="sxs-lookup"><span data-stu-id="b715e-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="b715e-188">Когда вы [Настройка hello веб-страниц для Application Insights](app-insights-javascript.md), изменить фрагмент кода hello, получаемые из портала hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b715e-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="b715e-189">(В приложениях ASP.NET, фрагмент кода hello обычно попадают в _Layout.cshtml.)  Вставка строки как `samplingPercentage: 10,` перед hello ключ инструментирования:</span><span class="sxs-lookup"><span data-stu-id="b715e-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

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

<span data-ttu-id="b715e-190">Процент выборки hello выберите значение в процентах, является закрыть too100/N, где N — целое число.</span><span class="sxs-lookup"><span data-stu-id="b715e-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="b715e-191">В настоящее время выборка не поддерживает другие значения.</span><span class="sxs-lookup"><span data-stu-id="b715e-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="b715e-192">При включении фиксированной частота выборки на сервере hello, hello клиентами и сервером синхронизируются, что, в поиск, можно перемещаться между связанной страницы представлений и запросов.</span><span class="sxs-lookup"><span data-stu-id="b715e-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="b715e-193">Выборка с фиксированной частотой для веб-сайтов ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b715e-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="b715e-194">Выборка фиксированной ставке уменьшает hello трафик веб-сервера и веб-браузеры.</span><span class="sxs-lookup"><span data-stu-id="b715e-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="b715e-195">В отличие от адаптивной выборки объем данных уменьшается в фиксированном, заданном вами размере.</span><span class="sxs-lookup"><span data-stu-id="b715e-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="b715e-196">Он также синхронизирует hello клиента и сервера выборки и сохранения связанных элементов — например, так что при просмотре представления страницы поиска можно найти его на запросы.</span><span class="sxs-lookup"><span data-stu-id="b715e-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="b715e-197">Алгоритм выборки Hello сохраняет связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="b715e-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="b715e-198">При каждом событии HTTP-запроса он и связанные с ним события игнорируются или передаются.</span><span class="sxs-lookup"><span data-stu-id="b715e-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="b715e-199">В обозревателе метрик ставки, такие как счетчики запроса и исключение умножаются toocompensate фактором для дискретизации hello, чтобы они приблизительно верны.</span><span class="sxs-lookup"><span data-stu-id="b715e-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="b715e-200">**Обновить пакеты NuGet для проекта** toohello последние *предварительного выпуска* версии Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b715e-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="b715e-201">Щелкните правой кнопкой мыши проект hello в обозревателе решений, выберите Управление пакетами NuGet проверьте **включить предварительный выпуск** и выполните поиск Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="b715e-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="b715e-202">**Отключение адаптивной выборки**: В [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), удалите или закомментируйте hello `AdaptiveSamplingTelemetryProcessor` узла.</span><span class="sxs-lookup"><span data-stu-id="b715e-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="b715e-203">**Включите модуль hello-rate выборки.**</span><span class="sxs-lookup"><span data-stu-id="b715e-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="b715e-204">Добавьте следующий фрагмент слишком[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="b715e-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="b715e-205">Процент выборки hello выберите значение в процентах, является закрыть too100/N, где N — целое число.</span><span class="sxs-lookup"><span data-stu-id="b715e-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="b715e-206">В настоящее время выборка не поддерживает другие значения.</span><span class="sxs-lookup"><span data-stu-id="b715e-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="b715e-207">Альтернатива: включение выборки с фиксированной частотой в коде сервера</span><span class="sxs-lookup"><span data-stu-id="b715e-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="b715e-208">Вместо параметра выборки hello в config-файле hello, можно использовать код.</span><span class="sxs-lookup"><span data-stu-id="b715e-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="b715e-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="b715e-209">*C#*</span></span>

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

<span data-ttu-id="b715e-210">([Сведения о процессорах телеметрии](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="b715e-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="b715e-211">Когда toouse выборки?</span><span class="sxs-lookup"><span data-stu-id="b715e-211">When toouse sampling?</span></span>
<span data-ttu-id="b715e-212">Адаптивная выборки включается автоматически при использовании hello 2.0.0-beta3 версии пакета SDK для ASP.NET или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b715e-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="b715e-213">Выборку приема (на наших серверах) можно применять независимо от используемой версии SDK.</span><span class="sxs-lookup"><span data-stu-id="b715e-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="b715e-214">Выборка не требуется для большинства приложений малого и среднего размера.</span><span class="sxs-lookup"><span data-stu-id="b715e-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="b715e-215">наиболее полезные сведения диагностики Hello и наиболее точную статистику получаются путем сбора данных для всех действий пользователей.</span><span class="sxs-lookup"><span data-stu-id="b715e-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="b715e-216">Основные преимущества Hello выборки являются:</span><span class="sxs-lookup"><span data-stu-id="b715e-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="b715e-217">Служба Application Insights удаляет («регулирует») точки данных, когда приложение слишком часто отправляет данные телеметрии за короткий интервал времени.</span><span class="sxs-lookup"><span data-stu-id="b715e-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="b715e-218">tookeep внутри hello [квоты](app-insights-pricing.md) точек данных для используемого ценового уровня.</span><span class="sxs-lookup"><span data-stu-id="b715e-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="b715e-219">tooreduce сетевой трафик от hello коллекцию телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b715e-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="b715e-220">Какой тип выборки следует использовать?</span><span class="sxs-lookup"><span data-stu-id="b715e-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="b715e-221">**Используйте выборку приема, если:**</span><span class="sxs-lookup"><span data-stu-id="b715e-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="b715e-222">Вы часто превышаете ежемесячную квоту телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b715e-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="b715e-223">Вы используете более ранних, чем 2 версии hello SDK, который не поддерживает дискретизацию - например, hello Java SDK или версии ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b715e-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="b715e-224">Вы получаете много данных телеметрии с веб-браузеров пользователей.</span><span class="sxs-lookup"><span data-stu-id="b715e-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="b715e-225">**Используйте выборку с фиксированной частотой, если:**</span><span class="sxs-lookup"><span data-stu-id="b715e-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="b715e-226">Вы используете hello пакет SDK Application Insights для ASP.NET web services версии 2.0.0 и более поздних версиях и</span><span class="sxs-lookup"><span data-stu-id="b715e-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="b715e-227">Требуется синхронизированные выборки между клиентом и сервером, таким образом, если выполняется анализ событий в [поиска](app-insights-diagnostic-search.md), можно переходить между связанных событий на приветствия клиента и сервера, например представления страниц и HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="b715e-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="b715e-228">Вы уверены, hello в процентном отношении соответствующие выборки для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b715e-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="b715e-229">Ее нужно находится достаточно высоко tooget точные показатели, но ниже hello скорость, с которой превышает ценообразования и hello регулирование пределы.</span><span class="sxs-lookup"><span data-stu-id="b715e-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="b715e-230">**Используйте адаптивную выборку:**</span><span class="sxs-lookup"><span data-stu-id="b715e-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="b715e-231">В противном случае мы рекомендуем использовать адаптивную выборку.</span><span class="sxs-lookup"><span data-stu-id="b715e-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="b715e-232">Оно включено по умолчанию на сервере ASP.NET hello SDK, версии 2.0.0-beta3 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b715e-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="b715e-233">Такая выборка не уменьшает трафик, не превышающий определенный минимальный объем, и не влияет на сайты, которые используются редко.</span><span class="sxs-lookup"><span data-stu-id="b715e-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="b715e-234">Как узнать, действует ли выборка</span><span class="sxs-lookup"><span data-stu-id="b715e-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="b715e-235">выборки скорость независимо от того, где он был применен, используйте фактические hello toodiscover [аналитический запрос](app-insights-analytics.md) подобные:</span><span class="sxs-lookup"><span data-stu-id="b715e-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="b715e-236">В каждом сохраняются записи, `itemCount` указывает номер исходной записи, которые он представляет равно too1 + hello число предыдущих записей отклоненных hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="b715e-237">Как работает функция выборки?</span><span class="sxs-lookup"><span data-stu-id="b715e-237">How does sampling work?</span></span>
<span data-ttu-id="b715e-238">-Rate и адаптивной выборки являются возможностью hello SDK в версиях ASP.NET из версии 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="b715e-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="b715e-239">Выборка приема — это функция hello служба Application Insights и может быть в операции, если hello SDK не выполняет выборку.</span><span class="sxs-lookup"><span data-stu-id="b715e-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="b715e-240">Алгоритм выборки Hello решает, какие toodrop элементов телеметрии и какие другие tookeep (если он является hello SDK или служба Application Insights hello).</span><span class="sxs-lookup"><span data-stu-id="b715e-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="b715e-241">Hello выборки решение основано на несколько правил, которые стремятся toopreserve все точки взаимосвязанных данных без изменений, обслуживание диагностики опыт в Application Insights, пригодных к использованию и надежное даже с сокращенный набор данных.</span><span class="sxs-lookup"><span data-stu-id="b715e-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="b715e-242">Например, если для неудачно завершенного запроса приложение отправляет дополнительные элементы телеметрии (например, исключение и трассировки, зарегистрированные этим запросом), выборка не будет разделять этот запрос и другие данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b715e-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="b715e-243">Она либо сохраняет, либо удаляет все элементы вместе.</span><span class="sxs-lookup"><span data-stu-id="b715e-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="b715e-244">В результате при просмотре сведений о запросе hello в Application Insights всегда видеть запрос hello вместе с его телеметрии связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="b715e-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="b715e-245">Для приложений, которые определяют «user» (то есть наиболее типичных веб-приложений), hello выборки решение зависит от хэш hello идентификатора пользователя hello, это означает, что все данные телеметрии для любого конкретного пользователя сохраняется либо удалены.</span><span class="sxs-lookup"><span data-stu-id="b715e-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="b715e-246">Для типов приложений, которые не определяют пользователей (например, веб-службы) hello hello выборки решение зависит от hello идентификатор операции запроса hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="b715e-247">Наконец для элементов hello телеметрии, которые не имеют идентификатор пользователя, ни операции (для примера телеметрии элементов отчета из асинхронных потоков без контекста http) выборки просто захватывает процент телеметрии элементов каждого типа.</span><span class="sxs-lookup"><span data-stu-id="b715e-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="b715e-248">При представлении задней tooyou телеметрии, Application Insights hello, служба настраивает hello показатели по hello такой же Процент выборки, которые использовались во время hello сбора, toocompensate для hello отсутствующие точки данных.</span><span class="sxs-lookup"><span data-stu-id="b715e-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="b715e-249">Таким образом при просмотре hello телеметрии в Application Insights, hello работе пользователей статистически правильный приближений, являются очень близкие toohello вещественных чисел.</span><span class="sxs-lookup"><span data-stu-id="b715e-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="b715e-250">Точность Hello приближения hello во многом зависит от процента выборки hello настроен.</span><span class="sxs-lookup"><span data-stu-id="b715e-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="b715e-251">Кроме того для приложений, обрабатывающих большой объем обычно сходных запросов из большого количества пользователей роста точности hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="b715e-252">На Здравствуйте другой стороны, для приложений, которые не работают с существенную нагрузку, как эти приложения обычно могут отправлять свои данные телеметрии должны оставаться в пределах квоты hello без риска потери данных после регулирования выборки не требуется.</span><span class="sxs-lookup"><span data-stu-id="b715e-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="b715e-253">Обратите внимание, что Application Insights не пример типов телеметрии метрики и сеансов с момента для этих типов могут быть нежелательному Снижение точности hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="b715e-254">Адаптивная выборка</span><span class="sxs-lookup"><span data-stu-id="b715e-254">Adaptive sampling</span></span>
<span data-ttu-id="b715e-255">Адаптивная выборки добавляет компонент, мониторы hello текущая скорость передачи данных из пакета SDK для hello и корректирует toostay tootry Процент выборки hello в hello целевой максимальной скорости.</span><span class="sxs-lookup"><span data-stu-id="b715e-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="b715e-256">корректировки Hello пересчитывается через регулярные интервалы, а основан на скользящее среднее для hello исходящих скорости передачи данных.</span><span class="sxs-lookup"><span data-stu-id="b715e-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="b715e-257">Выборка и hello JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="b715e-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="b715e-258">Hello клиентского (JavaScript) SDK участвует в фиксированной скорость выборки в сочетании с серверными hello SDK.</span><span class="sxs-lookup"><span data-stu-id="b715e-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="b715e-259">Hello инструментированы страниц будет отправлять телеметрии на стороне клиента из hello и те же пользователи, для какой hello серверные решил его слишком «sample в.»</span><span class="sxs-lookup"><span data-stu-id="b715e-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="b715e-260">Эта логика является целостность спроектированный toomaintain сеанс пользователя через клиент сервер стороны и.</span><span class="sxs-lookup"><span data-stu-id="b715e-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="b715e-261">Благодаря этому с помощью любого элемента телеметрии в Application Insights можно найти все остальные элементы телеметрии для этого пользователя или сеанса.</span><span class="sxs-lookup"><span data-stu-id="b715e-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="b715e-262">*Данные телеметрии на клиенте и сервере не отображают скоординированные образцы, как описано выше.*</span><span class="sxs-lookup"><span data-stu-id="b715e-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="b715e-263">Убедитесь в том, что выборка с фиксированной частотой включена и на сервере, и в клиенте.</span><span class="sxs-lookup"><span data-stu-id="b715e-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="b715e-264">Убедитесь, что этой hello SDK версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b715e-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="b715e-265">Убедитесь, что выбран hello же выборки процент в hello клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="b715e-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="b715e-266">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="b715e-266">Frequently Asked Questions</span></span>
<span data-ttu-id="b715e-267">*Почему выборка — это не простой сбор X процентов данных телеметрии каждого типа?*</span><span class="sxs-lookup"><span data-stu-id="b715e-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="b715e-268">Хотя такой подход выборки обеспечит с очень высокой точностью в метрики приближений, он будет нарушена возможность toocorrelate диагностических данных для каждого пользователя, сеанса и запрос, которая необходима для диагностики.</span><span class="sxs-lookup"><span data-stu-id="b715e-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="b715e-269">Поэтому выборку лучше всего описать как «сбор всех элементов телеметрии для X процентов пользователей приложения» или «сбор всех данных телеметрии для X процентов запросов приложения».</span><span class="sxs-lookup"><span data-stu-id="b715e-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="b715e-270">Для hello телеметрии элементы, не связанные с запросами hello (например, фон асинхронная обработка) попадающие hello обратно слишком «сбор X процентов всех элементов для каждого типа телеметрии.»</span><span class="sxs-lookup"><span data-stu-id="b715e-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="b715e-271">*Процент выборки hello меняться со временем?*</span><span class="sxs-lookup"><span data-stu-id="b715e-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="b715e-272">Да, постепенно адаптивной выборки изменяется hello выборки процент, основанный на hello в настоящее время наблюдается объем телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="b715e-273">*Если я использую фиксированной частоты выборки, как определить, какие выборки в процентах будет работать наилучшим образом подходит для приложения hello?*</span><span class="sxs-lookup"><span data-stu-id="b715e-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="b715e-274">Один из способов — toostart с адаптивной выборки, узнайте, как оценить сопоставляет на (см. hello выше вопрос), и затем коммутатора toofixed частота выборки с использованием этого курса.</span><span class="sxs-lookup"><span data-stu-id="b715e-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="b715e-275">В противном случае у вас tooguess.</span><span class="sxs-lookup"><span data-stu-id="b715e-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="b715e-276">Анализ текущего использования телеметрии в AI, наблюдать за любой регулирования, появление и оценка hello объема hello сбора данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b715e-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="b715e-277">Эти три набора входных данных вместе с выбранной ценовой категории, предложить, сколько стоит tooreduce hello объем собранных hello телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b715e-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="b715e-278">Однако увеличение hello количество пользователей или некоторые другие shift hello объем телеметрии, может сделать недействительным свою оценку.</span><span class="sxs-lookup"><span data-stu-id="b715e-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="b715e-279">*Что произойдет, если настроить слишком низкий процент выборки?*</span><span class="sxs-lookup"><span data-stu-id="b715e-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="b715e-280">Слишком мало выборки в процентах (over-aggressive выборки) снижает точность hello приближений hello, если Application Insights пытается toocompensate hello визуализации данных hello для сокращения тома данных hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="b715e-281">Кроме того возможности диагностики может снизиться, так, как часть hello редко сбои или медленных запросов могут быть использованы в выборке.</span><span class="sxs-lookup"><span data-stu-id="b715e-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="b715e-282">*Что произойдет, если настроить слишком высокий процент выборки?*</span><span class="sxs-lookup"><span data-stu-id="b715e-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="b715e-283">Настройка слишком высокой выборки в процентах (не агрессивно достаточно) приведет к недостаточно снижению объема hello hello сбор телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b715e-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="b715e-284">По-прежнему могут возникнуть телеметрии, потери данных, относящегося к toothrottling и hello стоимость использования Application Insights может быть выше, чем вы запланированный из-за накладных расходов toooverage.</span><span class="sxs-lookup"><span data-stu-id="b715e-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="b715e-285">*На каких платформах можно использовать выборку?*</span><span class="sxs-lookup"><span data-stu-id="b715e-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="b715e-286">Приема выборки может произойти автоматически для любого телеметрии определенной громкости, если hello SDK не выполняет выборки.</span><span class="sxs-lookup"><span data-stu-id="b715e-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="b715e-287">Например, это будет работать, если ваше приложение использует сервер Java или если вы используете старую версию пакета SDK для ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="b715e-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="b715e-288">Если вы используете пакет SDK для ASP.NET версии 2.0.0 и более поздних версий (размещенный в Azure или на собственном сервере), вы получаете адаптивной выборки по умолчанию, но можно переключить toofixed скорость, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="b715e-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="b715e-289">С фиксированной частоты выборки, браузер hello SDK автоматически синхронизирует toosample связанных событий.</span><span class="sxs-lookup"><span data-stu-id="b715e-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="b715e-290">*Существуют определенные редкие события, требуется, чтобы toosee. Как получить их за пределами модуля hello выборки?*</span><span class="sxs-lookup"><span data-stu-id="b715e-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="b715e-291">Инициализируйте отдельный экземпляр TelemetryClient с новой TelemetryConfiguration (hello по умолчанию не активным).</span><span class="sxs-lookup"><span data-stu-id="b715e-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="b715e-292">Используйте этот toosend редких событий.</span><span class="sxs-lookup"><span data-stu-id="b715e-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b715e-293">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b715e-293">Next steps</span></span>
* <span data-ttu-id="b715e-294">[Фильтрация](app-insights-api-filtering-sampling.md) может обеспечивать более строгий контроль над данными, отправляемыми пакетом SDK.</span><span class="sxs-lookup"><span data-stu-id="b715e-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

