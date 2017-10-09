---
title: "aaaLive поток метрики настраиваемых метрик и диагностики в Azure Application Insights | Документы Microsoft"
description: "Мониторинг веб-приложения в реальном времени с помощью пользовательских метрик и диагностика проблем с помощью динамического веб-канала сбоев, трассировок и событий."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>Live Metrics Stream: мониторинг и диагностика с задержкой в 1 секунду 

Проверки подавать сигналы hello динамической, в рабочей среде веб-приложения с помощью динамический поток метрики из [Application Insights](app-insights-overview.md). Выбор и фильтрация toowatch счетчики метрики и производительности в режиме реального времени, без tooyour любой телевизионными службы. Проверяйте трассировки стека на основе образцов неудавшихся запросов и исключений. Вместе с [Profiler](app-insights-profiler.md), [отладчиком моментальных снимков](app-insights-snapshot-debugger.md) и [тестированием производительности](app-insights-monitor-web-app-availability.md#performance-tests) Live Metrics Stream предоставляет эффективное средство диагностики веб-сайта, не вмешивающееся в его работу.

С помощью Live Metrics Stream можно выполнять следующие действия:

* Проверять выпущенное исправление, наблюдая за производительностью и числом сбоев.
* Посмотрите hello влияние тестирования нагрузки и диагностики проблем с live. 
* Сосредоточиться на конкретный тест сеансов или отфильтровать известные проблемы, при выборе и фильтрации требуется toowatch метрики hello.
* Получать трассировки исключений по мере того, как они возникают.
* Поэкспериментируйте с фильтрами toofind hello наиболее релевантных ключевых показателей эффективности.
* Отслеживать любые счетчики производительности Windows в режиме реального времени.
* Легко идентификации сервера, который испытывает проблемы и отфильтровать все hello/динамическая ключевого индикатора Производительности веб-канала toojust этого сервера.

[![Видео, посвященное Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

Динамический поток метрики в настоящее время доступен для приложений ASP.NET, выполняющихся в локальной среде или в облаке hello. 

## <a name="get-started"></a>Начало работы

1. Если вы еще не [установили Application Insights](app-insights-asp-net.md) в своем веб-приложении ASP.NET или [приложении Windows Server](app-insights-windows-services.md), сделайте это сейчас. 
2. **Последнюю версию обновления toohello** пакета Application Insights hello. В Visual Studio щелкните проект правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**. Откройте hello **обновления** установите флажок **включить предварительный выпуск**и выбрать все пакеты Microsoft.ApplicationInsights.* hello.

    Разверните приложение заново.

3. В hello [портал Azure](https://portal.azure.com), откройте hello ресурс Application Insights для своего приложения, а затем обновляющегося потока.

4. [Канал управления безопасного hello](#secure-the-control-channel) Если конфиденциальные данные, например имена клиентов можно использовать в фильтры.


![В колонке Обзор hello щелкните обновляющегося потока](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>Данные отсутствуют? Проверьте брандмауэр сервера

Проверьте hello [исходящие порты для потоковой трансляции метрики](app-insights-ip-addresses.md#outgoing-ports) открыты в брандмауэре hello серверов. 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>Чем Live Metrics Stream отличается от обозревателя метрик и службы аналитики?

| |Live Stream | Обозреватель метрик и служба аналитики |
|---|---|---|
|Задержка|Данные отображаются в течение одной секунды|Агрегирование выполняется в течение нескольких минут|
|Нет сохранения|Данные хранятся на диаграмме hello, и затем удаляется|[Данные сохраняются 90 дней](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|По запросу|Данные передаются, пока открыта служба Live Metrics|Данные отправляются в том случае, когда hello SDK установлен и включен|
|Free|Плата за данные Live Stream не взимается|Тема слишком[цены](app-insights-pricing.md)
|Выборка|Передаются все выбранные метрики и счетчики. Производится выборка сбоев и трассировок стека. TelemetryProcessors не применяются.|Может производиться [выборка](app-insights-api-filtering-sampling.md) событий.|
|Канал управления|Сигналы управления фильтра, отправляются toohello SDK. Рекомендуется [защитить этот канал](#secure-channel).|Связь является односторонней, toohello портала|


## <a name="select-and-filter-your-metrics"></a>Выбор и фильтрация метрик

(На классическом приложений ASP.NET с помощью hello новейшую версию пакета SDK.)

Вы можете отслеживать пользовательские ключевого индикатора Производительности динамической путем применения фильтров произвольный на любой телеметрии Application Insights с портала hello. Щелкните элемент управления фильтром hello, показывающий, когда вы указатель любой hello диаграмм. Следующая диаграмма Hello отображения на диаграмме пользовательского запроса счетчик ключевого показателя Эффективности с фильтры для атрибутов URL-адрес и длительность. Проверьте фильтры с hello Предварительный просмотр потока раздел, описывающий динамического канала телеметрии, которая соответствует критериям hello, заданные в любой момент времени. 

![Пользовательский КПЭ запросов](./media/app-insights-live-stream/live-stream-filteredMetric.png)

Вы можете отслеживать не только количество. Hello параметры зависят от типа hello потока, который может быть любой телеметрии Application Insights: запросы, зависимости, исключения, трассировок, события или метрик. Поток может передавать и ваше [пользовательское измерение](app-insights-api-custom-events-metrics.md#properties).

![Параметры значения](./media/app-insights-live-stream/live-stream-valueoptions.png)

В дополнение к этому tooApplication телеметрии аналитики также можно отслеживать любого счетчика производительности Windows, выбрав, параметры потока hello и указав имя hello счетчика производительности "hello".

Динамические метрики объединяются дважды: локально на каждом сервере, а затем на всех серверах. По умолчанию hello в одном, используя другие параметры hello соответствующих раскрывающихся списков можно изменить.

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>Пример данных телеметрии: пользовательские события динамической диагностики
По умолчанию hello динамического канала событий показаны примеры запросов с ошибками и вызовы зависимостей, исключения, события и трассировки. Щелкните hello значок toosee hello применения отбора в любой момент времени. 

![Динамический веб-канал по умолчанию](./media/app-insights-live-stream/live-stream-eventsdefault.png)

Как с метриками, можно указать любой произвольный критерии tooany типов телеметрии Application Insights hello. В этом примере мы выбираем конкретные сбои запросов, трассировки и события. Мы также выбираем все исключения и сбои зависимостей.

![Пользовательский динамический веб-канал](./media/app-insights-live-stream/live-stream-events.png)

Примечание: В настоящее время в критериях исключения на уровне сообщений, используйте сообщение hello внешней исключения. В предыдущих примере hello toofilter out hello критической исключение с сообщением внутреннее исключение (следующим hello «<--» разделитель) «hello client отключен». использовался критерий "Message not-contains "Error reading request content"" (Сообщение не содержит "Ошибка при чтении содержимого запроса").

В разделе hello сведения об элементе в hello live веб-канала, щелкнув его. Вы можете приостановить hello веб-канала либо нажав **приостановить** просто прокрутку вниз или при выборе пункта меню. Динамического канала будет возобновлена после прокрутки начало обратной toohello или щелкнув hello счетчик элементов, собранные во время оно было приостановлено.

![Выборка динамических ошибок](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>Фильтрация по экземпляру сервера

Если вы хотите toomonitor экземпляр роли сервера, можно отфильтровать сервером.

![Выборка динамических ошибок](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>Требования к пакетам SDK
Пользовательские метрики и события Live Metrics Stream доступны при использовании версии 2.4.0-beta2 или более новой версии [пакета SDK для Application Insights для веб-приложений](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Помните, параметр «Включить предварительный выпуск» tooselect из диспетчера пакетов NuGet.

## <a name="secure-hello-control-channel"></a>Безопасный канал управления hello
Hello настраиваемые фильтры заданных критериев отправляются назад toohello компонент Live метрики hello пакет SDK Application Insights. Hello фильтры могут содержать конфиденциальные сведения, например кодов клиента. Можно сделать канала hello secure секретным ключом API Кроме toohello ключ инструментирования.
### <a name="create-an-api-key"></a>Создание ключа API

![Создание ключа API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>Добавление ключа tooConfiguration API
Добавьте в файл applicationinsights.config hello, hello AuthenticationApiKey toohello QuickPulseTelemetryModule.
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
Или в коде, задайте его в hello QuickPulseTelemetryModule:

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

Однако если распознавать и доверять всем hello подключенных серверов, можно попробовать hello настраиваемые фильтры без канала с проверкой подлинности hello. Эта возможность доступна в течение шести месяцев. Это переопределение требуется после каждого создания сеанса или подключения нового сервера.

![Параметры аутентификации Live Metrics](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>Настоятельно рекомендуется установить канал с проверкой подлинности hello перед вводом потенциально конфиденциальных данных, например CustomerID в критериях фильтра hello.
>

## <a name="generating-a-performance-test-load"></a>Создание нагрузки для тестирования производительности

Влияние hello toowatch загрузки увеличить, используйте hello теста производительности колонку. В ней имитируются одновременные запросы от нескольких пользователей. Его можно запустить либо «ручные тесты» (ping тесты) одного URL-адреса, или он может выполнять [многоэтапной веб-теста производительности](app-insights-monitor-web-app-availability.md#multi-step-web-tests) отправлять (в hello таким же способом, как доступности тестирования).

> [!TIP]
> После создания теста производительности hello, откройте тест hello и hello колонке обновляющегося потока в отдельных окнах. Можно увидеть при запуске теста производительности и контрольных значений обновляющегося потока в hello hello из очереди одновременно.
>


## <a name="troubleshooting"></a>Устранение неполадок

Данные отсутствуют? Если приложение находится в защищенной сети: Live Metrics Stream использует IP-адреса, отличающиеся IP-адресов другой телеметрии Application Insights. Убедитесь, что [эти IP-адреса](app-insights-ip-addresses.md) открыты в брандмауэре.



## <a name="next-steps"></a>Дальнейшие действия
* [Отслеживание использования Application Insights.](app-insights-web-track-usage.md)
* [Использование диагностического поиска](app-insights-diagnostic-search.md)
* [Профилировщик](app-insights-profiler.md)
* [Отладчик моментальных снимков](app-insights-snapshot-debugger.md)
