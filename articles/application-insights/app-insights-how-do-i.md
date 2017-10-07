---
title: "aaaHow по выполнению в Azure Application Insights | Документы Microsoft"
description: "Вопросы и ответы об Application Insights"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a>Как работать с Application Insights
## <a name="get-an-email-when-"></a>Получать уведомление по электронной почте, если...
### <a name="email-if-my-site-goes-down"></a>Уведомлять меня по электронной почте, если сайт выходит из строя
Настройте [веб-тест доступности](app-insights-monitor-web-app-availability.md).

### <a name="email-if-my-site-is-overloaded"></a>Уведомлять меня по электронной почте, если сайт перегружен
Настройте [оповещение](app-insights-alerts.md) для **времени ответа от сервера**. Пороговое значение может быть в пределах от 1 до 2 секунд.

![](./media/app-insights-how-do-i/030-server.png)

Приложение может также демонстрировать признаки нагрузки, выдавая коды ошибок. Настройте оповещение при **неудачных запросах**.

Если вы хотите tooset оповещение на **исключения сервера**, может потребоваться toodo [дополнительной настройки](app-insights-asp-net-exceptions.md) в toosee данные о заказах.

### <a name="email-on-exceptions"></a>Получить уведомление по электронной почте при исключении
1. [Настройте мониторинг исключений](app-insights-asp-net-exceptions.md)
2. [Создать оповещение](app-insights-alerts.md) на hello исключение подсчета метрики

### <a name="email-on-an-event-in-my-app"></a>Уведомлять меня по электронной почте о событиях в приложении
Предположим, что вам нравится tooget сообщение электронной почты при возникновении определенного события. Application Insights не предоставляет эту функцию напрямую, но позволяет [отправлять оповещение, если метрика превысит пороговое значение](app-insights-alerts.md).

Оповещения можно настроить для [пользовательских метрик](app-insights-api-custom-events-metrics.md#trackmetric), но не для пользовательских событий. Запись некоторых tooincrease кода метрики при возникновении события hello:

    telemetry.TrackMetric("Alarm", 10);

или:

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

Так как предупреждения имеют два состояния, вы можете toosend низкое значение рассмотрим hello предупреждение toohave завершен:

    telemetry.TrackMetric("Alarm", 0.5);

Создать диаграмму в [метрики обозреватель](app-insights-metrics-explorer.md) toosee вашей звуковых сигналов:

![](./media/app-insights-how-do-i/010-alarm.png)

Теперь можно задайте предупреждения toofire при hello метрика выходит за пределы mid значение на короткий промежуток времени:

![](./media/app-insights-how-do-i/020-threshold.png)

Задайте усреднение минимальный период toohello hello.

Вы сможете получить сообщения электронной почты при hello метрика выходит за пределы и ниже порогового значения hello.

Некоторые точки tooconsider:

* Оповещение может находиться в двух состояниях: «оповещение» и «исправен». состояние Hello вычисляется только в том случае, когда поступает метрики.
* Сообщение электронной почты отправляется только в том случае, когда изменяется состояние hello. Именно поэтому у вас есть toosend высокой и низкой стоимости метрики.
* Предупреждение tooevaluate hello, среднее hello берется hello полученных значений через hello предшествующего периода. Это происходит каждый раз при получении метрики, поэтому чаще, чем период hello задать могут отправляться сообщения электронной почты.
* Так как сообщения электронной почты, отправленных на «предупреждение» и «Исправен», может потребоваться tooconsider повторно говорить одноразовой события как условие с двумя состояниями. Например вместо события «завершена» имеют условие «задание выполняется», где получить сообщения электронной почты в hello начало и конец задания.

### <a name="set-up-alerts-automatically"></a>Настройте автоматические оповещения
[Используйте PowerShell toocreate новые предупреждения](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>Используйте PowerShell tooManage Application Insights
* [Создание новых ресурсов](app-insights-powershell-script-create-resource.md)
* [Создание новых оповещений](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>Разделение телеметрии разных версий

* Несколько ролей в приложении. Используйте единый ресурс Application Insights и выполните фильтрацию по cloud_Rolename. [Подробнее](app-insights-monitor-multi-role-apps.md)
* Отдельные стадии разработки, тестирования и выпуска версий. Используйте различные ресурсы Application Insights. Получают ключи hello инструментирования из файла web.config. [Дополнительные сведения](app-insights-separate-resources.md)
* Отчеты о версиях сборки. Добавьте свойство с помощью инициализатора телеметрии. [Подробнее](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>Мониторинг внутренних серверов и классических приложений
[Модуль SDK для Windows Server используйте hello](app-insights-windows-desktop.md).

## <a name="visualize-data"></a>Визуализируйте данные
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>Панель мониторинга с метрикой для нескольких приложений
* В [обозревателе метрик](app-insights-metrics-explorer.md)настройте диаграмму и сохраните ее в списке избранного. Закрепите панель мониторинга Azure toohello.

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>Панель мониторинга с данными из других источников и Application Insights
* [Экспортировать данные телеметрии tooPower BI](app-insights-export-power-bi.md).

Или

* Используйте SharePoint как панель мониторинга для отображения данных веб-компонентов SharePoint. [Использовать непрерывный Экспорт и Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).  Использование базы данных hello tooexamine PowerView и создайте веб-части SharePoint для PowerView.

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>Отфильтровывание анонимных или прошедших проверку подлинности пользователей
Если вход пользователей, можно задать hello [идентификатор пользователя с проверкой подлинности](app-insights-api-custom-events-metrics.md#authenticated-users). (Это не происходит автоматически.)

Затем можно:

* выполнить поиск по определенным идентификаторам пользователей;

![](./media/app-insights-how-do-i/110-search.png)

* Фильтрация метрики tooeither анонимного или прошедшего проверку подлинности пользователей

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>Изменение имен и значений свойств
Создайте [фильтр](app-insights-api-filtering-sampling.md#filtering). Это дает возможность изменять или фильтровать данные телеметрии, перед отправкой из вашего приложения tooApplication аналитики.

## <a name="list-specific-users-and-their-usage"></a>Вывод списка определенных пользователей и информации об их использовании
Если необходимо просто слишком[поиска для конкретных пользователей](#search-specific-users), можно задать hello [идентификатор пользователя с проверкой подлинности](app-insights-api-custom-events-metrics.md#authenticated-users).

Если вы хотите получить список пользователей с данными — например, на какие страницы заходят пользователи или как часто они входят в систему, — существует два варианта действий:

* [Идентификатор прошедшего проверку подлинности пользователя набор](app-insights-api-custom-events-metrics.md#authenticated-users), [Экспорт базы данных tooa](app-insights-code-sample-export-sql-stream-analytics.md) и используйте подходящий средств tooanalyze существует данные пользователей.
* Если имеется небольшое количество пользователей, отправьте пользовательские события или метрики, с данными hello интерес как hello значение метрики или имя события и ИД пользователя параметр hello как свойство. tooanalyze просмотров страниц, замените hello стандартный вызов trackPageView JavaScript. tooanalyze телеметрию на стороне сервера, используйте телеметрии инициализатора tooadd hello идентификатор tooall сервера телеметрия пользователя. После этого можно отфильтровывать и разделять метрики и поиск по идентификатору пользователя hello.

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>Уменьшить трафик с моей tooApplication app Insights
* В [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), отключите модули не требуется такой сборщик счетчика производительности hello.
* Используйте [выборки и фильтрации](app-insights-api-filtering-sampling.md) на hello SDK.
* На веб-страницах максимальное число hello вызовов Ajax для представления каждой страницы. В hello фрагмент скрипта после `instrumentationKey:...` , вставьте: `,maxAjaxCallsPerView:3` (или подходящий номер).
* Если вы используете [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), вычисления статистической функции hello пакетов значения метрики перед отправкой hello результат. Это можно сделать с помощью перегруженного метода TrackMetric().

Подробнее о [расценках и квотах](app-insights-pricing.md).

## <a name="disable-telemetry"></a>Отключение данных телеметрии
слишком**динамически остановить и запустить** hello сбор и передача данных телеметрии с сервера hello:

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



слишком**отключить выбранный Стандартная сборщики** - счетчики производительности, например, HTTP-запросы или зависимостей - удалить или закомментировать строку hello соответствующих строк в [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Удалось это делается, например, если требуется toosend TrackRequest данных.

## <a name="view-system-performance-counters"></a>Просмотр счетчиков производительности системы
Среди hello метрик, которые можно отобразить в обозревателе метрик представляют собой набор счетчиков производительности системы. В готовой колонке **Серверы** отображается несколько таких счетчиков.

![Откройте ресурс Application Insights и щелкните "Серверы".](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>Если данные счетчика производительности не отображаются
* **Сервер IIS** на собственном компьютере или на виртуальной машине. [Установите монитор состояния](app-insights-monitor-performance-live-website-now.md).
* **Веб-сайт Azure** — мы еще не поддерживаем счетчики производительности. Существует несколько методик, которые можно получить в составе Стандартная панель управления веб-сайте Azure hello.
* **Сервер Unix** - [установите collectd](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay дополнительных счетчиков производительности
* Во-первых, [добавить новую диаграмму](app-insights-metrics-explorer.md) и увидеть, если счетчик hello в hello basic устанавливается мы предлагаем.
* В противном случае [добавить набор toohello счетчика hello, собранные модуль счетчика производительности hello](app-insights-performance-counters.md).
