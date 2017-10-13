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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a>Телеметрия метрик: модель данных Application Insights

[Application Insights](app-insights-overview.md) поддерживает два типа телеметрии метрик — отдельное измерение и предварительно вычисленная метрика. Отдельное измерение содержит только имя и значение. Предварительно вычисленная метрика указывает минимальное и максимальное значение метрики в интервале статистической обработки, а также его стандартное отклонение.

Телеметрия предварительно вычисленных метрик предполагает, что период статистической обработки составлял одну минуту.

Существует несколько известных имен метрик, поддерживаемых Application Insights. 

Метрика, представляющая счетчики системы и процессов:

| **Имя .NET**             | **Платформонезависимое имя** | **Имя REST API** | **Описание**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | Ведется работа... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | Общее использование ЦП на компьютере
| `\Memory\Available Bytes`                 | Ведется работа... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | Доступная память на диске
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | Ведется работа... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | Использование ЦП для процесса, где размещается приложение
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | Ведется работа... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | Использование памяти для процесса, где размещается приложение
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | Ведется работа... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | Частота операций ввода-вывода, выполняемых процессом, где размещается приложение
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | Ведется работа... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | Частота запросов, обрабатываемых приложением 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | Ведется работа... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | Частота исключений, выдаваемых приложением
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | Ведется работа... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | Среднее время выполнения запросов
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | Ведется работа... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | Количество запросов в очереди, ожидающих обработки

## <a name="name"></a>Имя

Имя метрики, которое нужно отобразить на портале Application Insights и в пользовательском интерфейсе. 

## <a name="value"></a>Значение

Отдельное значение для измерения. Сумма отдельных измерений для агрегата.

## <a name="count"></a>Count

Вес вычисленной метрики. Не следует задавать для измерения.

## <a name="min"></a>Min

Минимальное значение вычисленной метрики. Не следует задавать для измерения.

## <a name="max"></a>Max

Максимальное значение вычисленной метрики. Не следует задавать для измерения.

## <a name="standard-deviation"></a>Стандартное отклонение

Стандартное отклонение вычисленной метрики. Не следует задавать для измерения.

## <a name="custom-properties"></a>Пользовательские свойства

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Дальнейшие действия

- Вы можете узнать, как использовать [API Application Insights для пользовательских событий и метрик](app-insights-api-custom-events-metrics.md#trackmetric).
- В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.
- Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.
