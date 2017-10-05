---
title: "Модель данных телеметрии Azure Application Insights — телеметрия метрик | Документы Майкрософт"
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
ms.openlocfilehash: 42e55db4f932de85ee1a71c408b889e0ff9fe3e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="54cd3-103">Телеметрия метрик: модель данных Application Insights</span><span class="sxs-lookup"><span data-stu-id="54cd3-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="54cd3-104">[Application Insights](app-insights-overview.md) поддерживает два типа телеметрии метрик — отдельное измерение и предварительно вычисленная метрика.</span><span class="sxs-lookup"><span data-stu-id="54cd3-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="54cd3-105">Отдельное измерение содержит только имя и значение.</span><span class="sxs-lookup"><span data-stu-id="54cd3-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="54cd3-106">Предварительно вычисленная метрика указывает минимальное и максимальное значение метрики в интервале статистической обработки, а также его стандартное отклонение.</span><span class="sxs-lookup"><span data-stu-id="54cd3-106">Pre-aggregated metric specifies minimum and maximum value of the metric in the aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="54cd3-107">Телеметрия предварительно вычисленных метрик предполагает, что период статистической обработки составлял одну минуту.</span><span class="sxs-lookup"><span data-stu-id="54cd3-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="54cd3-108">Существует несколько известных имен метрик, поддерживаемых Application Insights.</span><span class="sxs-lookup"><span data-stu-id="54cd3-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="54cd3-109">Метрика, представляющая счетчики системы и процессов:</span><span class="sxs-lookup"><span data-stu-id="54cd3-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="54cd3-110">**Имя .NET**</span><span class="sxs-lookup"><span data-stu-id="54cd3-110">**.NET name**</span></span>             | <span data-ttu-id="54cd3-111">**Платформонезависимое имя**</span><span class="sxs-lookup"><span data-stu-id="54cd3-111">**Platform agnostic name**</span></span> | <span data-ttu-id="54cd3-112">**Имя REST API**</span><span class="sxs-lookup"><span data-stu-id="54cd3-112">**REST API name**</span></span> | <span data-ttu-id="54cd3-113">**Описание**</span><span class="sxs-lookup"><span data-stu-id="54cd3-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="54cd3-114">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="54cd3-114">Work in progress...</span></span> | [<span data-ttu-id="54cd3-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="54cd3-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="54cd3-116">Общее использование ЦП на компьютере</span><span class="sxs-lookup"><span data-stu-id="54cd3-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="54cd3-117">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="54cd3-117">Work in progress...</span></span> | [<span data-ttu-id="54cd3-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="54cd3-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="54cd3-119">Доступная память на диске</span><span class="sxs-lookup"><span data-stu-id="54cd3-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="54cd3-120">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="54cd3-120">Work in progress...</span></span> | [<span data-ttu-id="54cd3-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="54cd3-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="54cd3-122">Использование ЦП для процесса, где размещается приложение</span><span class="sxs-lookup"><span data-stu-id="54cd3-122">CPU of the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="54cd3-123">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="54cd3-123">Work in progress...</span></span> | [<span data-ttu-id="54cd3-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="54cd3-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="54cd3-125">Использование памяти для процесса, где размещается приложение</span><span class="sxs-lookup"><span data-stu-id="54cd3-125">memory used by the process hosting the application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="54cd3-126">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="54cd3-126">Work in progress...</span></span> | [<span data-ttu-id="54cd3-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="54cd3-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="54cd3-128">Частота операций ввода-вывода, выполняемых процессом, где размещается приложение</span><span class="sxs-lookup"><span data-stu-id="54cd3-128">rate of I/O operations runs by process hosting the application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="54cd3-129">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="54cd3-129">Work in progress...</span></span> | [<span data-ttu-id="54cd3-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="54cd3-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="54cd3-131">Частота запросов, обрабатываемых приложением</span><span class="sxs-lookup"><span data-stu-id="54cd3-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="54cd3-132">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="54cd3-132">Work in progress...</span></span> | [<span data-ttu-id="54cd3-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="54cd3-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="54cd3-134">Частота исключений, выдаваемых приложением</span><span class="sxs-lookup"><span data-stu-id="54cd3-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="54cd3-135">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="54cd3-135">Work in progress...</span></span> | [<span data-ttu-id="54cd3-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="54cd3-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="54cd3-137">Среднее время выполнения запросов</span><span class="sxs-lookup"><span data-stu-id="54cd3-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="54cd3-138">Ведется работа...</span><span class="sxs-lookup"><span data-stu-id="54cd3-138">Work in progress...</span></span> | [<span data-ttu-id="54cd3-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="54cd3-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="54cd3-140">Количество запросов в очереди, ожидающих обработки</span><span class="sxs-lookup"><span data-stu-id="54cd3-140">number of requests waiting for the processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="54cd3-141">Имя</span><span class="sxs-lookup"><span data-stu-id="54cd3-141">Name</span></span>

<span data-ttu-id="54cd3-142">Имя метрики, которое нужно отобразить на портале Application Insights и в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="54cd3-142">Name of the metric you'd like to see in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="54cd3-143">Значение</span><span class="sxs-lookup"><span data-stu-id="54cd3-143">Value</span></span>

<span data-ttu-id="54cd3-144">Отдельное значение для измерения.</span><span class="sxs-lookup"><span data-stu-id="54cd3-144">Single value for measurement.</span></span> <span data-ttu-id="54cd3-145">Сумма отдельных измерений для агрегата.</span><span class="sxs-lookup"><span data-stu-id="54cd3-145">Sum of individual measurements for the aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="54cd3-146">Count</span><span class="sxs-lookup"><span data-stu-id="54cd3-146">Count</span></span>

<span data-ttu-id="54cd3-147">Вес вычисленной метрики.</span><span class="sxs-lookup"><span data-stu-id="54cd3-147">Metric weight of the aggregated metric.</span></span> <span data-ttu-id="54cd3-148">Не следует задавать для измерения.</span><span class="sxs-lookup"><span data-stu-id="54cd3-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="54cd3-149">Min</span><span class="sxs-lookup"><span data-stu-id="54cd3-149">Min</span></span>

<span data-ttu-id="54cd3-150">Минимальное значение вычисленной метрики.</span><span class="sxs-lookup"><span data-stu-id="54cd3-150">Minimum value of the aggregated metric.</span></span> <span data-ttu-id="54cd3-151">Не следует задавать для измерения.</span><span class="sxs-lookup"><span data-stu-id="54cd3-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="54cd3-152">Max</span><span class="sxs-lookup"><span data-stu-id="54cd3-152">Max</span></span>

<span data-ttu-id="54cd3-153">Максимальное значение вычисленной метрики.</span><span class="sxs-lookup"><span data-stu-id="54cd3-153">Maximum value of the aggregated metric.</span></span> <span data-ttu-id="54cd3-154">Не следует задавать для измерения.</span><span class="sxs-lookup"><span data-stu-id="54cd3-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="54cd3-155">Стандартное отклонение</span><span class="sxs-lookup"><span data-stu-id="54cd3-155">Standard deviation</span></span>

<span data-ttu-id="54cd3-156">Стандартное отклонение вычисленной метрики.</span><span class="sxs-lookup"><span data-stu-id="54cd3-156">Standard deviation of the aggregated metric.</span></span> <span data-ttu-id="54cd3-157">Не следует задавать для измерения.</span><span class="sxs-lookup"><span data-stu-id="54cd3-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="54cd3-158">Пользовательские свойства</span><span class="sxs-lookup"><span data-stu-id="54cd3-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="54cd3-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="54cd3-159">Next steps</span></span>

- <span data-ttu-id="54cd3-160">Вы можете узнать, как использовать [API Application Insights для пользовательских событий и метрик](app-insights-api-custom-events-metrics.md#trackmetric).</span><span class="sxs-lookup"><span data-stu-id="54cd3-160">Learn how to use [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="54cd3-161">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="54cd3-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="54cd3-162">Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.</span><span class="sxs-lookup"><span data-stu-id="54cd3-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
