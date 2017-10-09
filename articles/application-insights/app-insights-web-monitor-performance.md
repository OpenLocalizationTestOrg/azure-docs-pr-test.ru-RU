---
title: "aaaMonitor состояния приложения и использования с помощью Application Insights"
description: "Приступая к работе с Application Insights. Анализ использования, доступности и производительности локальных приложений или веб-приложений Microsoft Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>Отслеживание производительности в веб-приложениях


Она позволяет удостовериться, что приложение работает с хорошей производительностью, и быстро выяснить, были ли сбои. [Application Insights] [ start] сообщения о всех проблем производительности и исключений, а справки вы найдете и диагностировать hello основные причины.

Application Insights можно отслеживать веб-приложения и службы Java и ASP.NET, а также службы WCF. Они могут размещаться локально, на виртуальных машинах, а также как веб-сайты Microsoft Azure. 

На стороне клиента hello Application Insights может занять телеметрии из веб-страниц и других устройств, включая iOS, Android и магазина Windows.

>[!Note]
> Мы добавили новые возможности для поиска медленно выполняющихся страниц в веб-приложении. Если у вас нет доступа к tooit, ее включить, настройку параметров предварительного просмотра с hello [предварительной версии](app-insights-previews.md). Узнайте, как эти новые возможности в [поиска и устранения проблем производительности с hello интерактивного исследования производительности](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Настройка мониторинга производительности
Если вы еще не добавили Application Insights tooyour проекта (то есть, если он не имеет ApplicationInsights.config), выберите один из следующих способов работы tooget:

* [Веб-приложения ASP.NET](app-insights-asp-net.md)
  * [Добавление мониторинга исключений](app-insights-asp-net-exceptions.md)
  * [Добавление мониторинга зависимостей](app-insights-monitor-performance-live-website-now.md)
* [Веб-приложения J2EE](app-insights-java-get-started.md)
  * [Добавление мониторинга зависимостей](app-insights-java-agent.md)

## <a name="view"></a>Просмотр метрик производительности
В [hello портал Azure](https://portal.azure.com), найдите ресурс Application Insights toohello, который настроен для вашего приложения. Обзор колонке Hello отображаются основные данные:

Щелкните любой toosee диаграммы более подробные сведения и toosee результаты на более длительный период. Например, щелкните плитку hello запросов, а затем выберите диапазон времени:

![Перемещаться по данным toomore и выберите диапазон времени](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Щелкните toochoose диаграммы какие метрики, он отображается, или добавить новую диаграмму и выберите его метрики:

![Выберите метрики toochoose графа](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Снимите все показатели hello** полное выделение hello toosee, которая доступна. метрики Hello делятся на группы; При выборе любого члена группы только hello других членов этой группы отображаются.

## <a name="metrics"></a>Что все это означает? Плитки и отчеты о производительности
Имеются различные метрики производительности, которые можно получить. Давайте начнем с тех, которые отображаются по умолчанию в колонке приложения hello.

### <a name="requests"></a>Запросы
Hello количество HTTP-запросов, полученных в течение указанного периода. Сравните это с результатами hello на другие отчеты toosee, как приложение ведет себя как загрузка hello меняется.

HTTP-запросы включают в себя все запросы GET и POST для страниц, данных и изображений.

Щелкните на подсчете tooget плитки приветствия для конкретного URL-адресов.

### <a name="average-response-time"></a>Среднее время ответа
Меры hello время между ввода, возвращаемых приложения и hello ответа веб-запроса.

Hello точек Показать скользящее среднее. Если имеется много запросов, может возникнуть некоторые, может отличаться от среднего hello без очевидным пиковых нагрузок или оказываются в hello graph.

Обращайте внимание на необычные пики. Средняя toorise времени ответа с уделять запросов. В случае неограниченного уделять hello приложения может попадание ограничение ресурсов, таких как мощность Процессора и hello службы, используемые в нем.

Щелкните раз tooget hello плитки для конкретного URL-адресов.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>Slowest requests (Самые медленные запросы)
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Показывает, какие запросы могут потребовать оптимизации производительности.

### <a name="failed-requests"></a>Failed requests (Неудачные запросы)
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

Это счетчик запросов, которые вызвали не перехваченные исключения.

Щелкните hello плитки toosee hello подробные сведения о конкретных ошибок и выберите его подробности toosee отдельный запрос. 

Для детального изучения доступна только репрезентативная выборка сбоев.

### <a name="other-metrics"></a>Другие метрики
toosee других метриках отображения, щелкните график и затем отмените выбор всех hello метрики toosee hello все доступные набора. Нажмите кнопку (i) toosee определения каждой метрики.

![Отмените выбор всех показателей toosee hello всего набора](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

Здравствуйте, при выборе любой hello метрики отключает другим пользователям, которые не могут присутствовать на одной диаграмме.

## <a name="set-alerts"></a>Задание предупреждений
уведомления по электронной почте о необычных значениях метрик, toobe добавить оповещение. Вы можете Администраторы учетных записей электронной почты toohello для toosend hello или toospecific адреса электронной почты.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Задайте другие свойства ресурса hello перед hello. Не следует выбирать ресурсы webtest hello Если tooset оповещения на производительность или метрики использования.

Быть тщательно toonote hello единиц, в которых в ответ на вопрос tooenter hello пороговое значение.

*Я не вижу hello кнопки "добавить оповещение".* -Это toowhich учетной записи группы, у вас есть доступ только для чтения? Обратитесь к администратору учетной записи hello.

## <a name="diagnosis"></a>Диагностические проблемы
Вот некоторые советы по выявлению и диагностике проблем с производительностью:

* Настройка [веб-тестов] [ availability] toobe оповещение, если веб-узел выходит из строя или отвечает неправильно или медленно. 
* Сравнение hello количество запросов с toosee других метрик на предмет ошибок или медленный ответ связанные tooload.
* [Вставка и поиск операторов трассировки] [ diagnostic] в ваш код toohelp выявить проблемы.
* Отслеживайте работу веб-приложения с помощью [Live Metrics Stream][livestream].
* Записать состояние hello приложения .net с [отладчик моментального снимка][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Поиск и устранение узких мест производительности с помощью интерактивного исследования производительности

Можно использовать hello новый Application Insights производительности интерактивного исследования toolocate областей веб-приложения с замедление работы общую производительность. Можно быстро найти конкретные страницы замедляют работу и использовать hello [средство профилирования](app-insights-profiler.md) toosee при наличии корреляцию между ними.

### <a name="create-a-list-of-slow-performing-pages"></a>Создание списка медленно выполняющихся страниц 

Первый шаг Hello для поиска проблем с производительностью — tooget список hello медленно отвечать на запросы страниц. Привет, показанную ниже демонстрируется использование hello производительности колонке tooget список потенциальных tooinvestigate страниц дальнейшей. Быстро видно на этой странице, было slow-down hello время ответа приложения hello в приблизительно 6:00, а затем в приблизительно 22: 00. Также вы увидите, что операции сведения о клиенте GET hello имеет некоторые длительные операции с Медиана: время отклика 507.05 время в миллисекундах. 

![Интерактивная производительность Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Просмотр определенных страниц

Получив моментальный снимок производительности приложения, можно получить дополнительные сведения о медленно выполняющихся операциях. Щелкните любой операции в toosee hello список hello сведения, как показано ниже. Hello диаграммы можно увидеть, если производительность hello был основан на зависимость. Также видно сколько hello опытным пользователям различные времени ответа. 

![Колонка "Операции" в Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Просмотр данных для определенного периода времени

После идентификации определенного момента времени tooinvestigate детализации и даже дальнейших toolook на hello определенных операций, которые могли привести slow-down производительности hello. При нажатии кнопки на определенный момент времени можно получить сведения о hello страницы приветствия, как показано ниже. В hello пример ниже, вы увидите hello операции, перечисленные для определенного периода времени вместе с кодами ответа сервера hello и продолжительность операции hello. Также имеется hello URL-адрес для открытия рабочего элемента TFS, если вам требуется toosend этой команды разработки сведения tooyour.

![Временной срез Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Просмотр подробных сведений об определенной операции

После идентификации определенного момента времени tooinvestigate детализации и даже дальнейших toolook на hello определенных операций, которые могли привести slow-down производительности hello. Щелкните операцию на основе сведений hello toosee списка hello hello операции, как показано ниже. В этом примере видно, что не удалось выполнить операцию hello и Application Insights предоставленные hello подробные сведения о hello приложение hello исключение вызвало. Опять же, вы можете легко создать рабочий элемент TFS из этой колонки.

![Колонка "Операции" в Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Дальнейшие действия
[Веб-тестов] [ availability] -веб-запросов отправки tooyour приложения с регулярными интервалами из вокруг Здравствуй, мир.

[Записать и искать трассировки диагностики] [ diagnostic] — Вставка трассировки вызовов и анализировать проблемы toopinpoint результаты hello.

[Отслеживание использования][usage] — получайте информацию о том, как люди используют ваше приложение.

[Устранение неполадок][qna] — вопросы и ответы



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



