---
title: "Что такое Azure Application Insights AAA? | Документация Майкрософт"
description: "Управление производительностью и отслеживание использования работающего веб-приложения.  Обнаружение, рассмотрение и диагностика проблем. Сведения о том, как пользователи используют ваше приложение."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/14/2017
ms.author: bwren
ms.openlocfilehash: d2596f53a36991fcd08551e6395ece68a5801e39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-insights"></a>Что такое Azure Application Insights?
Application Insights — это расширяемая служба управления производительностью приложений (APM) для веб-разработчиков на нескольких платформах. Используйте его toomonitor динамической веб-приложения. Она автоматически обнаруживает аномалии производительности. Он включает toohelp средств гибкой аналитической диагностировать проблемы и toounderstand, какие пользователи фактически выполняют вместе с приложением.  Он разработан toohelp постоянно повысить производительность и удобство использования. Он работает для приложений на различных платформах, включая .NET, Node.js и J2EE, размещенные локально или в облаке hello. Интегрируется с процесс devOps и разными tooa точек подключения средств разработки.

![Составляйте диаграммы по действиям пользователей или детализируйте конкретные события.](./media/app-insights-overview/00-sample.png)

[Рассмотрим начальный анимации hello](https://www.youtube.com/watch?v=fX2NtGrh-Y0).

## <a name="how-does-application-insights-work"></a>Как работает Application Insights?
Установка пакета небольшое инструментирование в приложении и настроить ресурс Application Insights на портале Microsoft Azure hello. Инструментирование Hello отслеживает приложение и отправляет портал toohello данных телеметрии. (hello приложение может работать в любом месте — это не обязательно toobe, размещенных в Azure).

Инструментирование не только приложение hello веб-службы, но и все компоненты фона и hello JavaScript в веб-страницы приветствия сами. 

![Аналитики инструментирования приложений в приложении отправляет данные телеметрии tooyour ресурс Application Insights.](./media/app-insights-overview/01-scheme.png)


Кроме того можно извлечь данные телеметрии из среды узла hello, такие как счетчики производительности диагностики Azure и журналы Docker. Можно также настроить веб-тесты, которые периодически отправлять запросы на искусственных tooyour веб-службы.

Все эти потоки телеметрии интегрированы в hello портал Azure, где можно применить мощных аналитический и поиска средств toohello необработанных данных.


### <a name="whats-hello-overhead"></a>Что такое издержки hello
Hello влияние на производительность приложения, очень мал. Вызовы отслеживания не приводят к блокировке, выполняются в пакетном режиме и отправляется в отдельном потоке.

## <a name="what-does-application-insights-monitor"></a>Как работает монитор Application Insights?

Application Insights предназначен для команды разработчиков hello, toohelp понять, как работает приложение, и как он используется. Она отслеживает следующее:

* **Частота запросов, время отклика и частота сбоев.** Узнайте, какие страницы наиболее популярны, в какое время дня их посещают чаще всего, а также узнайте о расположении пользователей. Узнайте, какие страницы работают лучше всего. Если при увеличении количества запросов повышается время отклика и частота сбоев, возможно, возникла проблема с ресурсами. 
* **Частота зависимостей, время отклика и частота сбоев.** Узнайте, замедляют ли внешние службы вашу работу.
* **Исключения** — анализ статистики суммарный hello, или выбрать конкретные экземпляры и можно перейти к трассировке стека hello и связанные запросы. Исключения сервера и браузера регистрируются.
* **Просмотры страниц и производительность загрузки.** Эти сведения сообщаются через браузеры пользователей.
* **Вызовы AJAX** с веб-страницы. Скорость, время отклика и частота сбоев.
* **Количество пользователей и сеансов.**
* **Счетчики производительности** с компьютеров с сервером Windows или Linux, такие как ЦП, память и использование сети. 
* **Размещение диагностики** из Docker или Azure. 
* **Журналы диагностики трассировки** из вашего приложения. Предназначены для сопоставления событий трассировки с запросами.
* **Пользовательские события и метрики** создавать самостоятельно в hello клиента или сервера кода, tootrack бизнес-события, такие как элементы продаж или игр реализовано.

## <a name="where-do-i-see-my-telemetry"></a>Где отображаются мои данные телеметрии?

Существует множество способов tooexplore данных. Ознакомьтесь со следующими статьями:

|  |  |
| --- | --- |
| [**Интеллектуальное обнаружение в Application Insights**](app-insights-proactive-diagnostics.md)<br/>Автоматические оповещения адаптировать tooyour приложения обычных шаблонов, телеметрии и триггер когда что-нибудь за пределами hello стандартный подход. Также можно [настроить оповещения](app-insights-alerts.md) для определенных уровней пользовательских или стандартных метрик. |![Пример оповещения](./media/app-insights-overview/alerts-tn.png) |
| [**Схема сопоставления приложений в Application Insights**](app-insights-app-map.md)<br/>компоненты приложения, оповещения и ключевые показатели Hello. |![Схема сопоставления приложений](./media/app-insights-overview/appmap-tn.png)  |
| [**Профилирование динамических веб-приложений Azure с помощью Application Insights (предварительная версия)**](app-insights-profiler.md)<br/>Проверьте hello профили выполнения выборки запросов. |![Профилировщик](./media/app-insights-overview/profiler.png) |
| [**Usage analysis for web applications with Application Insights**](app-insights-usage-overview.md) (Аналитики использования для веб-приложений с Application Insights)<br/>Анализируйте сегментацию пользователей и хранение.|![Инструмент "Хранение"](./media/app-insights-overview/retention.png) |
| [**Работа с Application Insights в Visual Studio**](app-insights-diagnostic-search.md)<br/>Поиск и фильтрация событий, таких как запросы, исключения, вызовы зависимостей, журналы трассировки и просмотры страниц.  |![Поиск данных телеметрии](./media/app-insights-overview/search-tn.png) |
| [**Исследование метрик в Application Insights**](app-insights-metrics-explorer.md)<br/>Просмотр, фильтрация и сегментирование объединенных данных, таких как частоты запросов, ошибок и исключений, время отклика и время загрузки страницы. |![Метрики](./media/app-insights-overview/metrics-tn.png) |
| [**Панели мониторинга**](app-insights-dashboards.md#dashboards)<br/>Объединение разнородных данных из нескольких ресурсов и их совместное использование с другими пользователями. Идеальное решение для многокомпонентные приложений, а также для непрерывного отображения в комнату команды hello. |![Пример панели мониторинга](./media/app-insights-overview/dashboard-tn.png) |
| [**Динамический поток метрик: мгновенные метрики для подробного отслеживания**](app-insights-live-stream.md)<br/>При развертывании новой сборки, просмотрите эти toomake индикаторы производительности рядом реального времени, убедиться, что все работает правильно. |![Пример Live Metrics](./media/app-insights-overview/live-metrics-tn.png) |
| [**Аналитика в Application Insights**](app-insights-analytics.md)<br/>Получите ответы на сложные вопросы о производительности и использовании приложения с помощью этого мощного языка запросов. |![Пример аналитики](./media/app-insights-overview/analytics-tn.png) |
| [**Работа с Application Insights в Visual Studio**](app-insights-visual-studio.md)<br/>Просмотреть данные производительности в коде hello. Toocode перейти из трассировки стека.|![Visual studio](./media/app-insights-overview/visual-studio-tn.png) |
| [**Debug Snapshots on Exceptions in .NET Apps**](app-insights-snapshot-debugger.md) (Отладка моментальных снимков при исключениях в приложениях .NET)<br/>Отладка моментальных снимков, выбранных из активных операций со значениями параметров.|![Visual studio](./media/app-insights-overview/snapshot.png) |
| [**Использование данных Application Insights в Power BI**](app-insights-export-power-bi.md)<br/>Интегрируйте метрики использования с другими метриками бизнес-аналитики.| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [**Use the Application Insights REST API to build custom solutions**](https://dev.applicationinsights.io/) (Использование интерфейса REST API Application Insights для создания пользовательских решений)<br/>Напишите код, toorun запросы через метрики и необработанных данных.| ![Интерфейс REST API](./media/app-insights-overview/rest-tn.png) |
| [**Экспорт данных телеметрии из Application Insights**](app-insights-export-telemetry.md)<br/>Массовый экспорт toostorage необработанные данные по мере их поступления. |![экспорт.](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a>Как использовать Application Insights?

### <a name="monitor"></a>Монитор
Установите Application Insights в веб-приложении, настройте [доступность веб-тестов](app-insights-monitor-web-app-availability.md) и:

* Настройка [мониторинга](app-insights-dashboards.md) для вашей команды tookeep комнаты в глаза нагрузочных тестов, время отклика, и производительности hello зависимостей страницы загрузки и вызовов AJAX.
* Обнаружение, являющиеся медленных hello и большинство сбоев запросов.
* Контрольное значение [обновляющегося потока](app-insights-live-stream.md) при развертывании нового выпуска tooknow немедленно о потери.

### <a name="detect-diagnose"></a>Обнаружение и диагностика
При получении предупреждения или обнаружении проблемы:

* Оцените, сколько пользователей столкнулось с проблемами.
* сопоставляйте сбои с исключениями, вызовами зависимостей и трассировками;
* изучите профилировщик, моментальные снимки, дамп стека и журналы трассировки.

### <a name="build-measure-learn"></a>Создание, измерение и обучение
[Измерение эффективности hello](app-insights-usage-overview.md) каждой новой функции развертывания.

* Планирование toomeasure каким образом пользователи используют новый UX или бизнес-функций.
* записывайте пользовательскую телеметрию в свой код;
* Далее разработку базовый hello циклическое переключение жестких свидетельство из телеметрии.

## <a name="get-started"></a>Начало работы
Application Insights является одним из многих служб, размещенных в Microsoft Azure и телеметрии существует отправляется для анализа и представления hello. Поэтому перед выполнением других действий, вам понадобится подписка слишком[Microsoft Azure](http://azure.com). Он работает свободного toosign и при выборе hello основные [ценовой план](https://azure.microsoft.com/pricing/details/application-insights/) аналитики приложений является бесплатной пока приложение стал toohave значительных использования. Если у вашей организации уже есть подписка, они добавить ваш tooit учетной записи Майкрософт.

Существует несколько способов запуска tooget. Начните с того, который вам лучше подходит. Можно добавить позднее hello другим пользователям.

* **Во время выполнения: инструментирование веб-приложения на сервере hello.** Позволяет избежать toohello кода обновления. Необходимо, чтобы сервер tooyour доступа администратора.
  * [**Локальные или размещенные на виртуальной машине службы IIS**](app-insights-monitor-performance-live-website-now.md);
  * [**веб-приложения или виртуальные машины Azure**](app-insights-monitor-performance-live-website-now.md);
  * [**J2EE**](app-insights-java-live.md).
* **Во время разработки: добавьте код tooyour Application Insights.** Позволяет toowrite пользовательские телеметрии и tooinstrument серверной части и настольных приложений.
  * [Visual Studio](app-insights-asp-net.md) 2013 с обновлением 2 или более поздняя версия.
  * Java в [Eclipse](app-insights-java-eclipse.md) или [другие средства](app-insights-java-get-started.md);
  * [Node.js](app-insights-nodejs.md)
  * [другие платформы.](app-insights-platforms.md)
* **[Инструментирование веб-страниц](app-insights-javascript.md)** для получения сведений о просмотрах страниц, вызовах AJAX и других данных телеметрии на стороне клиента.
* **[Тесты доступности](app-insights-monitor-web-app-availability.md)** с наших серверов для регулярной проверки связи с вашим веб-сайтом.


## <a name="next-steps"></a>Дальнейшие действия
Приступите к работе во время выполнения с помощью:

* [сервера IIS;](app-insights-monitor-performance-live-website-now.md)
* [сервера J2EE.](app-insights-java-live.md)

Приступите к работе во время разработки с помощью:

* [ASP.NET](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [Node.js](app-insights-nodejs.md)

## <a name="support-and-feedback"></a>Поддержка и обратная связь
* Вопросы и проблемы
  * [Устранение неполадок][qna]
  * [Форум MSDN](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [Stackoverflow](http://stackoverflow.com/questions/tagged/ms-application-insights)
* Ваши предложения:
  * [UserVoice](https://visualstudio.uservoice.com/forums/357324)
* Блог:
  * [Блог Application Insights](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a>Видеоролики

[![Анимационное ознакомительное видео](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
