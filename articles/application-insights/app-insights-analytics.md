---
title: "aaaAnalytics - hello мощное средство аналитики приложений Azure | Документы Microsoft"
description: "Обзор аналитики hello мощное средство диагностики поиска средство аналитики приложений. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a>Аналитика в Application Insights
[Аналитика](app-insights-analytics.md) — мощное средство поиска функция hello [Application Insights](app-insights-overview.md). На этих страницах описан язык запросов Log Analytics. 

* **[Вводное видео hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Испытайте аналитика на нашем смоделированные данные](https://analytics.applicationinsights.io/demo)**  Если ваше приложение еще не отправляет данные tooApplication аналитики.
* **[SQL-пользователей Памятка](https://aka.ms/sql-analytics)**  преобразует наиболее общих идиом hello.
* **[Справочник по языку](app-insights-analytics-reference.md)**  узнать, как все toouse hello мощные функции hello язык запросов для анализа журналов.


## <a name="queries-in-analytics"></a>Запросы в аналитике
Типичный запрос содержит *исходную* таблицу и ряд *операторов*, разделенных `|`. 

Например давайте выясним какое время дня гражданами hello Hyderabad повторите наш веб-приложения. А пока что мы посмотрим, какие коды результатов возвращаются tootheir HTTP-запросов. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

Мы количество IP-адресов для различных клиентов, сгруппировать их по часам hello hello дня по hello за последние 7 дней. 

> [!NOTE]
> результаты tooget за пределами hello предыдущие 24 часа, либо явным образом включить «timestamp» в запросе либо используйте hello время диапазона раскрывающееся меню.
>

Позволяет отобразить результаты hello с hello линейчатой диаграммы презентации, выбрав toostack результаты hello коды ответа:

![Выберите линейчатую диаграмму, оси x и y, а затем сегментацию.](./media/app-insights-analytics/020.png)

Похоже, в Хайдерабаде наше приложение наиболее популярно в обеденное время и время отхода ко сну. (И нам следует изучить эти 500 кодов.)

Кроме того, существуют сложные статистические операции.

![Результаты статистического запроса](./media/app-insights-analytics/025.png)

язык Hello имеет множество функций привлекательным:


* [Фильтрация](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) необработанных данных телеметрии приложения по любым полям, включая пользовательские свойства и метрики.
* [Соединение](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) нескольких таблиц — соотношение запросов с просмотрами страниц, вызовами зависимостей, исключениями и трассировками журнала.
* Сложные статистические [агрегаты](https://docs.loganalytics.io/learn/tutorials/aggregations.html).
* Столь же мощных, как SQL, но гораздо проще для сложных запросов: вместо вложенных инструкций передать hello данные из одного toohello простые операции рядом.
* Мгновенные яркие визуализации.
* [ПИН-код диаграммы панели мониторинга tooAzure](app-insights-analytics-using.md#pin-to-dashboard).
* [Экспорт tooPower запросов BI](app-insights-analytics-using.md#export-to-power-bi).
* Отсутствует [API-интерфейса REST](https://dev.applicationinsights.io/) можно использовать запросы toorun программными средствами, например из Powershell.


## <a name="connect-tooyour-application-insights-data"></a>Подключение к данным tooyour Application Insights
Откройте аналитику в [колонке "Обзор"](app-insights-dashboards.md) приложения в Application Insights. 

![На сайте portal.azure.com откройте ресурс Application Insights и щелкните "Аналитика".](./media/app-insights-analytics/001.png)


## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>Примеры запросов

Повторите эти пошаговые руководства tooillustrate hello степень аналитика с помощью:

 *  [Автоматическая диагностика пиков и пропуска шагов в контексте длительности запросов.](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [Анализ снижения производительности путем анализа временных рядов.](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [Анализ сбоев приложения с помощью функций autocluster и diffpatterns.](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [Расширенное определение формы путем анализа временных рядов.](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [С помощью скользящего окна операций tooanalyze приложения об использовании (скользящий MAU/DAU и т. д)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [Обнаружение нарушений в работе службы на основе анализа журналов отладки](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) и соответствующая запись блога [здесь](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).
 *  [Профилирование производительности приложений с помощью простых журналов отладки](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) и соответствующая запись блога [здесь](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/).
 *  [Измерение длительности hello для каждого шага в потоке кода с помощью простого отладочный журналы](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) и соответствующие записи блога [здесь](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [Анализ параллелизма с помощью простых журналов отладки](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) и соответствующая запись блога [здесь](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/).



## <a name="next-steps"></a>Дальнейшие действия
* Мы рекомендуем начать с hello [обзор языка](app-insights-analytics-tour.md). 
* Дополнительные сведения об [использовании аналитики](app-insights-analytics-using.md). 
* [Справочник по языку](app-insights-analytics-reference.md). 
