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
# <a name="metric-telemetry-application-insights-data-model"></a>Телеметрия метрик: модель данных Application Insights

[Application Insights](app-insights-overview.md) поддерживает два типа телеметрии метрик — отдельное измерение и предварительно вычисленная метрика. Отдельное измерение содержит только имя и значение. Предварительно агрегированные метрики указывает минимальное и максимальное значение метрики hello в интервал статистической обработки hello и стандартное отклонение его.

Телеметрия предварительно вычисленных метрик предполагает, что период статистической обработки составлял одну минуту.

Существует несколько известных имен метрик, поддерживаемых Application Insights. 

Метрика, представляющая счетчики системы и процессов:

| **Имя .NET**             | **Платформонезависимое имя** | **Имя REST API** | **Описание**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | Ведется работа... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | Общее использование ЦП на компьютере
| `\Memory\Available Bytes`                 | Ведется работа... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | Доступная память на диске
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | Ведется работа... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | ЦП процесса hello, где размещено приложение hello
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | Ведется работа... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | объем памяти, используемый процессом hello, где размещено приложение hello
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | Ведется работа... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | Частота выполнения операций ввода-вывода выполняется процессом, где размещено приложение hello
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | Ведется работа... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | Частота запросов, обрабатываемых приложением 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | Ведется работа... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | Частота исключений, выдаваемых приложением
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | Ведется работа... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | Среднее время выполнения запросов
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | Ведется работа... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | Количество запросов, ожидающих обработки в очереди hello

## <a name="name"></a>Имя

Имя метрики hello хотелось бы toosee портале Application Insights и пользовательского интерфейса. 

## <a name="value"></a>Значение

Отдельное значение для измерения. Сумма отдельные измерения для агрегата hello.

## <a name="count"></a>Count

Вес метрики hello суммарный метрики. Не следует задавать для измерения.

## <a name="min"></a>Min

Минимальное значение метрики hello статистическая обработка. Не следует задавать для измерения.

## <a name="max"></a>Max

Максимальное значение метрики hello статистическая обработка. Не следует задавать для измерения.

## <a name="standard-deviation"></a>Стандартное отклонение

Стандартное отклонение hello суммарный метрику. Не следует задавать для измерения.

## <a name="custom-properties"></a>Пользовательские свойства

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, как toouse [Application Insights API пользовательские события и метрики](app-insights-api-custom-events-metrics.md#trackmetric).
- В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.
- Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.
