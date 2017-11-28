---
title: "aaaAzure модели данных телеметрии приложения аналитики - метрики телеметрии | Документы Microsoft"
description: "Модель данных Application Insights для телеметрии метрик"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="a26e5-103">Телеметрия метрик: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="a26e5-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="a26e5-104">[Application Insights](app-insights-overview.md) поддерживает два типа телеметрии метрик — отдельное измерение и предварительно вычисленная метрика.</span><span class="sxs-lookup"><span data-stu-id="a26e5-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="a26e5-105">Отдельное измерение содержит только имя и значение.</span><span class="sxs-lookup"><span data-stu-id="a26e5-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="a26e5-106">Предварительно агрегированные метрики указывает минимальное и максимальное значение метрики hello в интервал статистической обработки hello и стандартное отклонение его.</span><span class="sxs-lookup"><span data-stu-id="a26e5-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="a26e5-107">Телеметрия предварительно вычисленных метрик предполагает, что период статистической обработки составлял одну минуту.</span><span class="sxs-lookup"><span data-stu-id="a26e5-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="a26e5-108">Существует несколько известных имен метрик, поддерживаемых Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a26e5-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="a26e5-109">Метрика, представляющая счетчики системы и процессов:</span><span class="sxs-lookup"><span data-stu-id="a26e5-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="a26e5-110">**Имя .NET**</span><span class="sxs-lookup"><span data-stu-id="a26e5-110">**.NET name**</span></span>             | <span data-ttu-id="a26e5-111">**Платформонезависимое имя**</span><span class="sxs-lookup"><span data-stu-id="a26e5-111">**Platform agnostic name**</span></span> | <span data-ttu-id="a26e5-112">**Имя REST API**</span><span class="sxs-lookup"><span data-stu-id="a26e5-112">**REST API name**</span></span> | <span data-ttu-id="a26e5-113">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a26e5-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="a26e5-114">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="a26e5-114">Work in progress...</span></span> | [<span data-ttu-id="a26e5-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="a26e5-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="a26e5-116">Общее использование ЦП на компьютере</span><span class="sxs-lookup"><span data-stu-id="a26e5-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="a26e5-117">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="a26e5-117">Work in progress...</span></span> | [<span data-ttu-id="a26e5-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="a26e5-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="a26e5-119">Доступная память на диске</span><span class="sxs-lookup"><span data-stu-id="a26e5-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="a26e5-120">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="a26e5-120">Work in progress...</span></span> | [<span data-ttu-id="a26e5-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="a26e5-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="a26e5-122">ЦП процесса hello, где размещено приложение hello</span><span class="sxs-lookup"><span data-stu-id="a26e5-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="a26e5-123">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="a26e5-123">Work in progress...</span></span> | [<span data-ttu-id="a26e5-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="a26e5-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="a26e5-125">объем памяти, используемый процессом hello, где размещено приложение hello</span><span class="sxs-lookup"><span data-stu-id="a26e5-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="a26e5-126">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="a26e5-126">Work in progress...</span></span> | [<span data-ttu-id="a26e5-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="a26e5-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="a26e5-128">Частота выполнения операций ввода-вывода выполняется процессом, где размещено приложение hello</span><span class="sxs-lookup"><span data-stu-id="a26e5-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="a26e5-129">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="a26e5-129">Work in progress...</span></span> | [<span data-ttu-id="a26e5-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="a26e5-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="a26e5-131">Частота запросов, обрабатываемых приложением</span><span class="sxs-lookup"><span data-stu-id="a26e5-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="a26e5-132">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="a26e5-132">Work in progress...</span></span> | [<span data-ttu-id="a26e5-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="a26e5-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="a26e5-134">Частота исключений, выдаваемых приложением</span><span class="sxs-lookup"><span data-stu-id="a26e5-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="a26e5-135">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="a26e5-135">Work in progress...</span></span> | [<span data-ttu-id="a26e5-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="a26e5-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="a26e5-137">Среднее время выполнения запросов</span><span class="sxs-lookup"><span data-stu-id="a26e5-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="a26e5-138">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="a26e5-138">Work in progress...</span></span> | [<span data-ttu-id="a26e5-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="a26e5-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="a26e5-140">Количество запросов, ожидающих обработки в очереди hello</span><span class="sxs-lookup"><span data-stu-id="a26e5-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="a26e5-141">Имя</span><span class="sxs-lookup"><span data-stu-id="a26e5-141">Name</span></span>

<span data-ttu-id="a26e5-142">Имя метрики hello хотелось бы toosee портале Application Insights и пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a26e5-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="a26e5-143">Значение</span><span class="sxs-lookup"><span data-stu-id="a26e5-143">Value</span></span>

<span data-ttu-id="a26e5-144">Отдельное значение для измерения.</span><span class="sxs-lookup"><span data-stu-id="a26e5-144">Single value for measurement.</span></span> <span data-ttu-id="a26e5-145">Сумма отдельные измерения для агрегата hello.</span><span class="sxs-lookup"><span data-stu-id="a26e5-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="a26e5-146">Count</span><span class="sxs-lookup"><span data-stu-id="a26e5-146">Count</span></span>

<span data-ttu-id="a26e5-147">Вес метрики hello суммарный метрики.</span><span class="sxs-lookup"><span data-stu-id="a26e5-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="a26e5-148">Не следует задавать для измерения.</span><span class="sxs-lookup"><span data-stu-id="a26e5-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="a26e5-149">Min</span><span class="sxs-lookup"><span data-stu-id="a26e5-149">Min</span></span>

<span data-ttu-id="a26e5-150">Минимальное значение метрики hello статистическая обработка.</span><span class="sxs-lookup"><span data-stu-id="a26e5-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="a26e5-151">Не следует задавать для измерения.</span><span class="sxs-lookup"><span data-stu-id="a26e5-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="a26e5-152">Max</span><span class="sxs-lookup"><span data-stu-id="a26e5-152">Max</span></span>

<span data-ttu-id="a26e5-153">Максимальное значение метрики hello статистическая обработка.</span><span class="sxs-lookup"><span data-stu-id="a26e5-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="a26e5-154">Не следует задавать для измерения.</span><span class="sxs-lookup"><span data-stu-id="a26e5-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="a26e5-155">Стандартное отклонение</span><span class="sxs-lookup"><span data-stu-id="a26e5-155">Standard deviation</span></span>

<span data-ttu-id="a26e5-156">Стандартное отклонение hello суммарный метрику.</span><span class="sxs-lookup"><span data-stu-id="a26e5-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="a26e5-157">Не следует задавать для измерения.</span><span class="sxs-lookup"><span data-stu-id="a26e5-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="a26e5-158">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="a26e5-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="a26e5-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a26e5-159">Next steps</span></span>

- <span data-ttu-id="a26e5-160">Узнайте, как toouse [Application Insights API пользовательские события и метрики](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="a26e5-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="a26e5-161">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a26e5-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="a26e5-162">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a26e5-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
