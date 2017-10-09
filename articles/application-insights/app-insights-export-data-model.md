---
title: "aaaAzure модели данных аналитики приложений | Документы Microsoft"
description: "Описание свойств, экспортируемых с помощью непрерывного экспорта в формате JSON и используемых в качестве фильтров."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a>Экспорт модели данных Application Insights
В этой таблице перечислены свойства hello телеметрии, отправленные hello [Application Insights](app-insights-overview.md) портала toohello пакеты SDK.
Вы увидите эти свойства в выходных данных [непрерывного экспорта](app-insights-export-telemetry.md).
Они также отображаются в фильтрах свойств в [обозревателе метрик](app-insights-metrics-explorer.md) и при [диагностическом поиске](app-insights-diagnostic-search.md).

Toonote точек:

* `[0]`в этих таблицах обозначает точку пути hello, когда имеется tooinsert индекса; но не всегда 0.
* Продолжительность времени указана в десятых долях микросекунды, поэтому 10 000 000 = 1 с.
* Значения даты и времени UTC и указываются в формате ISO hello`yyyy-MM-DDThh:mm:ss.sssZ`


## <a name="example"></a>Пример
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  }

## <a name="context"></a>Context
Для каждого типа данных телеметрии приведен пример с разделом контекста. Не все эти поля передаются со всеми точками данных.

| Путь | Тип | Примечания |
| --- | --- | --- |
| context.custom.dimensions [0] |объект [ ] |Набор пар "ключ — значение", заданный параметром пользовательских свойств. Максимальная длина ключа — 100, максимальная длина значения —1024. Более 100 уникальные значения, свойство hello может выполняться поиск, но не может использоваться для сегментации. Максимальное количество — 200 ключей на ключ ikey. |
| context.custom.metrics [0] |объект [ ] |Набор пар "ключ — значение", заданный параметром пользовательских измерений и метриками TrackMetric. Максимальная длина ключа — 100. Значения могут быть числовыми. |
| context.data.eventTime |строка |Формат UTC. |
| context.data.isSynthetic |Логическое |Запрос отображается toocome нижняя или веб-теста. |
| context.data.samplingRate |number |Процент создаваемых hello SDK, который отправляется tooportal телеметрии. Диапазон 0,0–100,0. |
| context.device |object |Устройство клиента |
| context.device.browser |строка |IE, Chrome… |
| context.device.browserVersion |строка |Chrome 48.0… |
| context.device.deviceModel |строка | |
| context.device.deviceName |строка | |
| context.device.id |строка | |
| context.device.locale |строка |en-GB, de-DE… |
| context.device.network |строка | |
| context.device.oemName |строка | |
| context.device.osVersion |строка |ОС узла |
| context.device.roleInstance |строка |Идентификатор узла сервера |
| context.device.roleName |строка | |
| context.device.type |строка |ПК, браузер… |
| context.location |object |На основе значения clientip. |
| context.location.city |строка |На основе значения clientip (если известно) |
| context.location.clientip |string |Последний восьмиугольник — анонимные too0. |
| context.location.continent |строка | |
| context.location.country |строка | |
| context.location.province |строка |Страна или область |
| context.operation.id |string |Элементы, имеющие hello таким же идентификатором операции отображаются в виде связанных элементов портала hello. Обычно идентификатор запроса hello. |
| context.operation.name |строка |URL-адрес или имя запроса |
| context.operation.parentId |строка |Разрешает использование вложенных связанных элементов. |
| context.session.id |string |Идентификатор группы операций из hello одного источника. Период, в течение 30 минут без операции сигналы hello завершение сеанса. |
| context.session.isFirst |Логическое | |
| context.user.accountAcquisitionDate |строка | |
| context.user.anonAcquisitionDate |строка | |
| context.user.anonId |строка | |
| context.user.authAcquisitionDate |строка |[Прошедший проверку пользователь.](app-insights-api-custom-events-metrics.md#authenticated-users) |
| context.user.isAuthenticated |Логическое | |
| internal.data.documentVersion |строка | |
| internal.data.id |строка | |

## <a name="events"></a>События
Пользовательские события, создаваемые элементом [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).

| Путь | Тип | Примечания |
| --- | --- | --- |
| event [0] count |целое число |100/(частота[выборки](app-insights-sampling.md) ). Например, 4 = &gt; 25 %. |
| event [0] name |строка |Имя события.  Максимальная длина: 250 |
| event [0] url |строка | |
| event [0] urlData.base |строка | |
| event [0] urlData.host |строка | |

## <a name="exceptions"></a>Исключения
Отчеты [исключения](app-insights-asp-net-exceptions.md) в hello server и hello браузера.

| Путь | Тип | Примечания |
| --- | --- | --- |
| basicException [0] assembly |строка | |
| basicException [0] count |целое число |100/(частота[выборки](app-insights-sampling.md) ). Например, 4 = &gt; 25 %. |
| basicException [0] exceptionGroup |строка | |
| basicException [0] exceptionType |string | |
| basicException [0] failedUserCodeMethod |строка | |
| basicException [0] failedUserCodeAssembly |строка | |
| basicException [0] handledAt |строка | |
| basicException [0] hasFullStack |Логическое | |
| basicException [0] id |строка | |
| basicException [0] method |строка | |
| basicException [0] message |строка |Сообщение об исключении. Максимальная длина: 10 000 |
| basicException [0] outerExceptionMessage |строка | |
| basicException [0] outerExceptionThrownAtAssembly |строка | |
| basicException [0] outerExceptionThrownAtMethod |строка | |
| basicException [0] outerExceptionType |строка | |
| basicException [0] outerId |строка | |
| basicException [0] parsedStack [0] assembly |строка | |
| basicException [0] parsedStack [0] fileName |строка | |
| basicException [0] parsedStack [0] level |целое число | |
| basicException [0] parsedStack [0] line |целое число | |
| basicException [0] parsedStack [0] method |строка | |
| basicException [0] stack |строка |Максимальная длина: 10 000 |
| basicException [0] typeName |строка | |

## <a name="trace-messages"></a>Сообщения трассировки
Отправленные [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), а по hello [адаптеры ведения журналов](app-insights-asp-net-trace-logs.md).

| Путь | Тип | Примечания |
| --- | --- | --- |
| message [0] loggerName |строка | |
| message [0] parameters |строка | |
| message [0] raw |string |сообщение журнала Hello, максимальной длиной 10 КБ. |
| message [0] severityLevel |строка | |

## <a name="remote-dependency"></a>Удаленная зависимость
Отправитель: TrackDependency. Использовать tooreport производительности и использовании [вызывает toodependencies](app-insights-asp-net-dependencies.md) сервера hello и вызовы AJAX в браузере hello.

| Путь | Тип | Примечания |
| --- | --- | --- |
| remoteDependency [0] async |Логическое | |
| remoteDependency [0] baseName |строка | |
| remoteDependency [0] commandName |строка |Например, home/index |
| remoteDependency [0] count |целое число |100/(частота[выборки](app-insights-sampling.md) ). Например, 4 = &gt; 25 %. |
| remoteDependency [0] dependencyTypeName |строка |HTTP, SQL, … |
| remoteDependency [0] durationMetric.value |number |Время от вызова toocompletion ответа зависимостей |
| remoteDependency [0] id |строка | |
| remoteDependency [0] name |строка |URL-адрес. Максимальная длина: 250 |
| remoteDependency [0] resultCode |строка |Из зависимости HTTP. |
| remoteDependency [0] success |Логическое | |
| remoteDependency [0] type |строка |HTTP, SQL, … |
| remoteDependency [0] url |строка |Максимальная длина: 2000 |
| remoteDependency [0] urlData.base |строка |Максимальная длина: 2000 |
| remoteDependency [0] urlData.hashTag |строка | |
| remoteDependency [0] urlData.host |строка |Максимальная длина: 200 |

## <a name="requests"></a>Requests (Запросы)
Отправитель: [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest). Стандартные модули Hello использовать этот tooreports время ответа сервера, на сервере hello.

| Путь | Тип | Примечания |
| --- | --- | --- |
| request [0] count |целое число |100/(частота[выборки](app-insights-sampling.md) ). Например: 4 =&gt; 25 %. |
| request [0] durationMetric.value |number |Время от tooresponse поступающих запросов. 1e7 = 1 с. |
| request [0] id |строка |Идентификатор операции |
| request [0] name |строка |GET или POST + базовый URL-адрес.  Максимальная длина: 250 |
| request [0] responseCode |целое число |Отправлено ответов tooclient HTTP |
| request [0] success |Логическое |Значение по умолчанию == (responseCode &lt; 400) |
| request [0] url |строка |Не включая узел. |
| request [0] urlData.base |строка | |
| request [0] urlData.hashTag |строка | |
| request [0] urlData.host |строка | |

## <a name="page-view-performance"></a>Производительность просмотра страницы
Отправленные hello браузера. Меры hello tooprocess время страницы, от пользователя вызывающей стороны hello запроса toodisplay завершения (за исключением асинхронные вызовы AJAX).

Контекстные значения показывают версию клиентской ОС и версию браузера.

| Путь | Тип | Примечания |
| --- | --- | --- |
| clientPerformance [0] clientProcess.value |целое число |Время в конце получение toodisplaying hello hello HTML-страницы. |
| clientPerformance [0] name |строка | |
| clientPerformance [0] networkConnection.value |целое число |Время, затраченное tooestablish сетевое подключение. |
| clientPerformance [0] receiveRequest.value |целое число |Время в конце отправки hello запроса tooreceiving hello HTML в ответе. |
| clientPerformance [0] sendRequest.value |целое число |Время от запроса сделанной toosend hello HTTP. |
| clientPerformance [0] total.value |целое число |Время от начала страницы toosend hello запроса toodisplaying hello. |
| clientPerformance [0] url |строка |URL-адрес запроса. |
| clientPerformance [0] urlData.base |строка | |
| clientPerformance [0] urlData.hashTag |строка | |
| clientPerformance [0] urlData.host |строка | |
| clientPerformance [0] urlData.protocol |строка | |

## <a name="page-views"></a>Просмотры страницы
Отправитель: trackPageView() или [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)

| Путь | Тип | Примечания |
| --- | --- | --- |
| view [0] count |целое число |100/(частота[выборки](app-insights-sampling.md) ). Например, 4 = &gt; 25 %. |
| view [0] durationMetric.value |целое число |При необходимости значение можно указать в методе trackPageView() или с помощью метода start/stopTrackPage(). Не Здравствуйте таким же, как clientPerformance значения. |
| view [0] name |строка |Заголовок страницы.  Максимальная длина: 250 |
| view [0] url |строка | |
| view [0] urlData.base |строка | |
| view [0] urlData.hashTag |строка | |
| view [0] urlData.host |строка | |

## <a name="availability"></a>Доступность
Это свойство создает отчеты о [веб-тестах на доступность](app-insights-monitor-web-app-availability.md).

| Путь | Тип | Примечания |
| --- | --- | --- |
| availability [0] availabilityMetric.name |строка |Доступность |
| availability [0] availabilityMetric.value |number |1,0 или 0,0. |
| availability [0] count |целое число |100/(частота[выборки](app-insights-sampling.md) ). Например, 4 = &gt; 25 %. |
| availability [0] dataSizeMetric.name |строка | |
| availability [0] dataSizeMetric.value |целое число | |
| availability [0] durationMetric.name |строка | |
| availability [0] durationMetric.value |number |Продолжительность теста. 1e7 = 1 с. |
| availability [0] message |строка |Диагностика сбоя. |
| availability [0] result |строка |Успех или сбой. |
| availability [0] runLocation |строка |Географический объект-источник HTTP-запроса. |
| availability [0] testName |строка | |
| availability [0] testRunId |строка | |
| availability [0] testTimestamp |строка | |

## <a name="metrics"></a>Метрики
Создатель: TrackMetric().

найдено значение метрики Hello в context.custom.metrics[0]

Например:

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a>О значениях метрик
Значения метрик (как в отчетах, так и в других элементах) сообщаются в рамках стандартной структуры объекта. Например:

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

В настоящее время - то, что это может изменить в будущих - сообщили hello стандартные модули SDK, все значения hello `count==1` и только hello `name` и `value` поля могут быть полезны. Hello единственный случай, где они будут отличаться бы при написании TrackMetric вызовы в которых hello другие параметры.

Здравствуйте, назначение hello остальные поля — toobe tooallow метрики, статистически hello SDK tooreduce трафика toohello портала. Например, перед отправкой каждого отчета с метриками вы можете получить среднее значение для нескольких последовательных показаний. Затем будет расчета hello min, max, стандартное отклонение и статистическое значение (сумма или среднее) и задайте заданное число toohello показания, представленный hello отчета.

В таблицах hello выше мы опущен hello редко используемые поля count, min, max, stdDev и sampledValue.

Вместо предварительной статистической обработке метрик, можно использовать [выборки](app-insights-sampling.md) при необходимости tooreduce hello объем телеметрии.

### <a name="durations"></a>Длительность
За исключением оговоренных случаев, показатели длительности представлены в десятых долях микросекунды, то есть 10 000 000,0 — это 1 с.

## <a name="see-also"></a>Дополнительные материалы
* [Application Insights](app-insights-overview.md)
* [Непрерывный экспорт](app-insights-export-telemetry.md)
* [Примеры кода](app-insights-export-telemetry.md#code-samples)
