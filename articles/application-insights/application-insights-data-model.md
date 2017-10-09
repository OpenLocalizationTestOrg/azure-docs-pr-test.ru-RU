---
title: "Модель данных телеметрии приложения аналитики aaaAzure | Документы Microsoft"
description: "Обзор модели данных Application Insights"
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
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Модель данных телеметрии Application Insights

[Azure Application Insights](app-insights-overview.md) отправляет данные телеметрии из вашего toohello приложения web портал Azure, таким образом, чтобы можно анализировать производительность hello и использование вашего приложения. модель телеметрии Hello Стандартизован так, чтобы его возможных toocreate платформы и мониторинга зависит от языка программирования. 

Данные, собранные Application Insights, моделируют типичный шаблон выполнения приложения:

![Модель приложений Application Insights](./media/application-insights-data-model/application-insights-data-model.png)

Hello телеметрию следующих типов, используемых toomonitor hello выполнения приложения. Hello следующие три типа обычно автоматически собранные hello пакет SDK Application Insights из hello платформа веб-приложений:

* [**Запрос** ](application-insights-data-model-request-telemetry.md) -созданный toolog запросы, полученные приложением. Например hello web Application Insights SDK автоматически создает запрос телеметрии элемент для каждого HTTP-запроса, получающего веб-приложения. 

    **Операции** — hello потоков выполнения, который обрабатывает запрос. Вы также можете [писать код](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor другие операции, такие как «пробуждение» на веб-задания или функцию, которая периодически выполняет обработку данных.  Каждая операция имеет идентификатор. Этот идентификатор, который можно использовать too[group]((application-insights-correlation.md) все данные телеметрии создан во время обработки запроса hello приложения. Каждая операция выполняется в течение определенного периода времени, после чего может завершиться успешно или сбоем.
* [**Исключение** ](application-insights-data-model-exception-telemetry.md) -обычно представляет исключение, которое вызывает toofail операции.
* [**Зависимости** ](application-insights-data-model-dependency-telemetry.md) -представляет вызов из внешней службы tooan приложения или хранилище, например API-интерфейса REST или SQL. В ASP.NET, определяются tooSQL вызовы зависимостей `System.Data`. Конечные точки tooHTTP вызовы определяются `System.Net`. 

Application Insights предоставляет три дополнительных типа данных пользовательской телеметрии:

* [Трассировки](application-insights-data-model-trace-telemetry.md) — используется либо непосредственно или через ведения журнала диагностики tooimplement адаптера с помощью платформу инструментирования, такие как знакомый tooyou `Log4Net` или `System.Diagnostics`.
* [Событие](application-insights-data-model-event-telemetry.md) -как правило, используется toocapture взаимодействие с пользователем в службе tooanalyze статистические характеристики интенсивности использования.
* [Метрика](application-insights-data-model-metric-telemetry.md) -использовать tooreport периодических скалярные значения.

Каждый элемент телеметрии можно определить hello [сведения о контексте](application-insights-data-model-context.md) как идентификатор сеанса версии или пользователя приложения. Контекст — это набор строго типизированных полей, который позволяет реализовывать определенные сценарии. Если версия приложения правильно инициализирована, Application Insights может обнаруживать новые закономерности в работе приложения, связанные с повторным развертыванием. Идентификатор сеанса может быть простой hello используется toocalculate или проблема оказывает влияние на пользователей. Отдельный подсчет числа идентификаторов сеансов, связанных с определенным сбоем зависимости, трассировкой ошибки или критическим исключением, позволяет получить ясное представление о последствиях.

Application Insights телеметрии модель определяет способ слишком[корреляции](application-insights-correlation.md) операции toohello телеметрии, частью которого он является. Например, запрос может выполнять вызовы базы данных SQL и записывать сведения о диагностике. Можно задать контекст hello корреляции для этих элементов телеметрии, связывающих его назад toohello телеметрии запроса.

## <a name="schema-improvements"></a>Усовершенствования схемы

Модель данных аналитики приложения является простой и основные и эффективный способ toomodel телеметрии приложения. Мы стремимся основных сценариев toosupport простых и упрощенной модели tookeep hello и разрешить tooextend hello схемы для расширенного использования.

проблемы tooreport данных модели или схемы и предложения использовать GitHub [ApplicationInsights домашней](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) репозитория.

## <a name="next-steps"></a>Дальнейшие действия

- [API Application Insights для пользовательских событий и метрик](app-insights-api-custom-events-metrics.md)
- Узнайте, каким образом слишком[расширения и фильтровать данные телеметрии](app-insights-api-filtering-sampling.md).
- Используйте [выборки](app-insights-sampling.md) toominimize объем телеметрии на основе модели данных.
- Ознакомление с [платформами](app-insights-platforms.md), поддерживаемыми Application Insights.
