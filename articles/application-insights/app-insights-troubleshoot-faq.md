---
title: "aaaAzure аналитики приложений часто задаваемые вопросы о | Документы Microsoft"
description: "Вопросы и ответы об Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Application Insights: вопросы и ответы

## <a name="configuration-problems"></a>Проблемы с конфигурацией
*У меня не получается настроить компоненты, о которых идет речь в таких статьях:*

* [Troubleshooting no data - Application Insights for .NET](app-insights-asp-net-troubleshoot-no-data.md)
* [раздел "Устранение неполадок"](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Настройка системы диагностики Azure для входа в Application Insights](app-insights-azure-diagnostics.md)
* [Устранение неполадок, а также вопросы и ответы по Application Insights для Java](app-insights-java-troubleshoot.md)

*Я не получаю данные с моего сервера*

* [Настройка исключений брандмауэра](app-insights-ip-addresses.md)
* [Настройка сервера ASP.NET](app-insights-monitor-performance-live-website-now.md)
* [Настройка сервера Java](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>Можно ли использовать Application Insights с...?

* [Веб-приложения на сервере IIS — локальном или в виртуальной машине](app-insights-asp-net.md)
* [Веб-приложения Java](app-insights-java-get-started.md)
* [Приложения Node.js](app-insights-nodejs.md)
* [Веб-приложения в Azure](app-insights-azure-web-apps.md)
* [Облачные службы в Azure](app-insights-cloudservices.md)
* [Серверы приложений, работающие в Docker](app-insights-docker.md)
* [Одностраничные веб-приложения](app-insights-javascript.md)
* [SharePoint](app-insights-sharepoint.md)
* [Классические приложения Windows](app-insights-windows-desktop.md)
* [другие платформы.](app-insights-platforms.md)

## <a name="is-it-free"></a>Предоставляется ли бесплатно?

Да, для экспериментальных целей. В ценовой план basic hello приложение может отправлять определенных скидку данных каждого месяца бесплатно. лимит свободного Hello — достаточно большой toocover разработки и публикации приложения для небольшого числа пользователей. Можно задать tooprevent крепления больше, чем указанный объем данных из процесса обработки.

Больших объемов данных телеметрии взимается по hello ГБ. Некоторые советы о том, как мы предоставляем слишком[ограничить стоимость](app-insights-pricing.md).

план корпоративного Hello влечет за собой плата за каждый день, отправляющий данные телеметрии каждый узел веб-сервера. Он подходит в том случае, если требуется, чтобы toouse непрерывного экспорта в широком масштабе.

[Чтение hello ценовой план](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="how-much-is-it-costing"></a>Сколько это стоит?

* Откройте hello **компоненты и цены** страницы в ресурс Application Insights. На ней приводится диаграмма недавнего использования. При желании можно задать ограничение на объем данных.
* Откройте hello [выставления счетов Azure колонке](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview) toosee счета на всех ресурсах.

## <a name="q14"></a>Что Application Insights изменяет в моем проекте?
Hello сведения зависят от типа hello проекта. Для веб-приложения:

* Добавляет tooyour эти файлы проекта:

  * ApplicationInsights.config.
  * ai.js
* Устанавливает следующие пакеты NuGet:

  * *Application Insights API* - hello основные API
  * *Application Insights API для веб-приложений* -использовать toosend телеметрии с сервера hello
  * *Application Insights API для приложений JavaScript* -используется toosend телеметрии от приветствия клиента

    в пакетах Hello эти сборки:
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* Вставляет элементы в:

  * Web.config
  * packages.config
* (Новые проекты только - если вы [Добавление существующего проекта Application Insights tooan][start], у вас есть toodo это вручную.) Вставка фрагментов кода в hello tooinitialize код клиента и сервера с идентификатором hello Application Insights ресурса. Например в приложении MVC код вставляется в главной страницы приветствия Views/Shared/_Layout.cshtml

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>Как обновить предыдущие версии пакета SDK?
В разделе hello [заметки о выпуске](app-insights-release-notes.md) для hello SDK соответствующие tooyour типа приложения.

## <a name="update"></a>Как изменить ресурс Azure, в который проект отправляет данные?
В обозревателе решений щелкните правой кнопкой мыши `ApplicationInsights.config` и выберите **Обновить Application Insights**. Вы можете отправить hello tooan существующего или нового ресурса данных в Azure. Мастер изменения Hello hello ключа инструментирования в файле ApplicationInsights.config определяет, где SDK сервера hello отправляет данные. Если не снят «Обновить все», повлечет за собой изменение ключа hello, где он отображается в веб-страниц.

## <a name="what-is-status-monitor"></a>Что такое монитор состояния?

Классического приложения, можно использовать в вашей IIS web server toohelp настроить Application Insights в веб-приложениях. Оно не собирает телеметрию: его можно остановить, когда вы не настраиваете приложение. 

[Подробнее](app-insights-monitor-performance-live-website-now.md#questions).

## <a name="what-telemetry-is-collected-by-application-insights"></a>Какую телеметрию собирает Application Insights?

Из серверных веб-приложений:

* HTTP-запросы;
* [зависимости](app-insights-asp-net-dependencies.md); Вызовы: баз данных SQL. HTTP вызывает tooexternal службы; Azure Cosmos DB, таблиц, хранилище больших двоичных объектов и очередей. 
* [исключения](app-insights-asp-net-exceptions.md) и трассировки стека;
* [Счетчики производительности](app-insights-performance-counters.md) — Если вы используете [монитор состояния](app-insights-monitor-performance-live-website-now.md), Azure monitoring(app-insights-azure-web-apps.md) или hello [collectd записи Application Insights](app-insights-java-collectd.md).
* [пользовательские события и метрики](app-insights-api-custom-events-metrics.md), которые вы создаете в коде;
* [Журналы трассировки](app-insights-asp-net-trace-logs.md) при настройке соответствующих сборщика hello.

С [клиентских веб-страниц](app-insights-javascript.md):

* [число просмотров страниц](app-insights-web-track-usage.md);
* [вызовы AJAX](app-insights-asp-net-dependencies.md) — запросы, выполняемые из запущенного скрипта;
* загрузка данных при просмотре страниц;
* количество пользователей и сеансов;
* [идентификаторы пользователей, прошедших проверку подлинности](app-insights-api-custom-events-metrics.md#authenticated-users).

Из других источников, если они настроены:

* [Настройка системы диагностики Azure для входа в Application Insights](app-insights-azure-diagnostics.md)
* [контейнеры Docker](app-insights-docker.md);
* [Импорт таблиц tooAnalytics](app-insights-analytics-import.md)
* [OMS (Log Analytics)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/);
* [Logstash](app-insights-analytics-import.md).

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>Можно ли отфильтровать или изменить некоторые данные телеметрии?

Да, в hello server можно написать:

* Процессор toofilter телеметрии или добавить свойства tooselected телеметрии элементов перед их отправкой в приложении.
* Данные телеметрии tooadd свойства tooall элементы инициализатора телеметрии.

Дополнительные сведения об [ASP.NET](app-insights-api-filtering-sampling.md) или [Java](app-insights-java-filter-telemetry.md).

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>Как определяются данные по городу, стране и другие данные по географическому расположению?

Мы найти hello IP-адрес (IPv4 или IPv6) hello веб-клиента с помощью [GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/).

* Браузер телеметрии: мы собираем IP-адрес отправителя hello.
* Сервер телеметрии: модуль Application Insights hello собирает hello клиентского IP-адреса. Эти сведения не собираются, если задан заголовок `X-Forwarded-For`.

Можно настроить hello `ClientIpHeaderTelemetryInitializer` tootake hello IP-адрес из другой заголовок. В некоторых системах, например, он перемещается по учетной записи-посредника, загружать балансировки или CDN слишком`X-Originating-IP`. [Подробнее](http://apmtips.com/blog/2016/07/05/client-ip-address/).

Вы можете [использовать Power BI](app-insights-export-power-bi.md) toodisplay телеметрии вашего запроса на карте.


## <a name="data"></a>Как долго хранятся данные на портале hello Защищены ли они?
Ознакомьтесь с разделом [Хранение данных и конфиденциальность][data].

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>Личные сведения (PII) можно отправлять в hello телеметрии?

Это возможно, если ваш код отправляет такие данные. Это также может происходить, если переменные в трассировках стека содержат персональные данные. Группа разработчиков выполнить tooensure оценки риска, правильно обрабатывается персональных данных. [Дополнительные сведения о хранении и конфиденциальности данных](app-insights-data-retention-privacy.md).

последний октет Hello hello клиента веб-адрес всегда имеет too0 после приема порталом hello.

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>Мой ключ iKey доступен в исходном коде веб-страницы. 

* Это обычная ситуация в решениях для мониторинга.
* Он не может быть toosteal используемых данных.
* Он может быть используется tooskew оповещениями данных или триггера.
* Мы не получали сообщений от клиентов о возникновении таких проблем.

Вы можете:

* использовать два отдельных ключа iKey (отдельных ресурса Application Insights) для данных клиента и сервера; Или
* Запись прокси-сервера, который выполняется на сервере и иметь hello веб-клиента передачи данных через прокси-сервера.

## <a name="post"></a>Как просмотреть данные POST в колонке «Поиск по журналу диагностики»?
Мы не заносить в журнал данные POST автоматически, но можно использовать вызов TrackTrace: поместить данные hello в параметре сообщение hello. Это имеет больше максимального размера превышает ограничения hello по строковым свойствам на то, что не удается применить фильтр на нем.

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>Следует ли использовать один или несколько ресурсов Application Insights?

Использование одного ресурса для всех компонентов hello или ролей одной бизнес-системы. Используйте отдельные ресурсы для стадий разработки, тестирования и выпуска, а также для независимых приложений.

* [Здесь описании hello](app-insights-separate-resources.md)
* [Пример: облачная служба с рабочей ролью и веб-ролью](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>Как динамически изменить ключ инструментирования hello?

* [Ознакомьтесь с этим обсуждением](app-insights-separate-resources.md)
* [Пример: облачная служба с рабочей ролью и веб-ролью](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>Что такое hello пользователей и сеансов подсчитывает?

* пакет JavaScript SDK для Hello задает файл cookie пользователя на hello веб-клиента, tooidentify пользователей и действия toogroup файла cookie сеанса.
* Если отсутствует клиентский скрипт, вы можете [устанавливать файлы cookie на сервере hello](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/).
* Если один реальный пользователь работает с вашим сайтом в разных браузерах, на разных компьютерах либо использует конфиденциальный режим просмотра или режим инкогнито, то он будет учитываться несколько раз.
* tooidentify вошедшего в систему пользователя по машинам и браузеры, добавьте вызов слишком[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users).

## <a name="q17"></a> Все ли активировано в Application Insights?
| Что вы должны видеть | Как tooget его | Для чего это нужно |
| --- | --- | --- |
| Диаграммы доступности |[Веб-тесты](app-insights-monitor-web-app-availability.md) |Узнать, что ваше веб-приложение работает |
| Производительность приложения на сервере: время отклика и т.д. |[Добавление проекта Application Insights tooyour](app-insights-asp-net.md) или [установить монитор состояния аналитики Активов на сервере](app-insights-monitor-performance-live-website-now.md) (или написать собственный код слишком[отслеживания зависимостей](app-insights-api-custom-events-metrics.md#trackdependency)) |Выявить проблемы производительности |
| Телеметрия зависимостей |[Установить монитор состояний Application Insights на сервере](app-insights-monitor-performance-live-website-now.md) |Выявить проблемы с базами данных или другими внешними компонентами |
| Получение данных трассировки стека из исключений |[Вставить вызовы TrackException в код](app-insights-asp-net-exceptions.md) (некоторые выводятся автоматически) |Обнаружить и диагностировать исключения |
| Поиск по трассировкам журнала |[Добавить адаптер ведения журнала](app-insights-asp-net-trace-logs.md) |Выявить исключения, проблемы производительности |
| Основная информация об использовании клиента: просмотр страниц, сеансы и т. д. |[Инициализатор JavaScript на веб-страницах](app-insights-javascript.md) |Аналитика использования |
| Настраиваемые метрики клиента |[Трассировка вызовов на веб-страницах](app-insights-api-custom-events-metrics.md) |Расширить возможности для пользователя |
| Настраиваемые метрики сервера |[Отслеживание вызовов на сервере](app-insights-api-custom-events-metrics.md) |Бизнес-аналитика |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>Почему являются hello подсчитывает в диаграммах поиска и метрики равны?

[Выборка](app-insights-sampling.md) уменьшает количество hello телеметрии элементов (запросы, пользовательские события и т. д.), которые фактически отправлен через портал toohello приложения. В поле поиска появляются hello фактически полученных элементов. В диаграммах метрик, отображающие количество событий появляются hello исходного произошедших событий. 

Каждый передаваемый элемент имеет свойство `itemCount`, которое показывает, сколько исходных событий представляет этот элемент. tooobserve выборки в операции можно выполнить этот запрос в аналитике:

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>Служба автоматизации

### <a name="configuring-application-insights"></a>Настройка Application Insights

С помощью монитора ресурсов Azure можно [создавать скрипты PowerShell](app-insights-powershell.md) для выполнения следующих задач:

* создание и обновление ресурсов Application Insights;
* Набор hello ценовой план.
* Получите ключ инструментирования hello.
* добавление оповещения метрики;
* добавление теста доступности.

Вы не можете настроить отчет обозревателя метрик или непрерывный экспорт.

### <a name="querying-hello-telemetry"></a>Запрос телеметрии hello

Используйте hello [API-интерфейса REST](https://dev.applicationinsights.io/) toorun [Analytics](app-insights-analytics.md) запросов.

## <a name="how-can-i-set-an-alert-on-an-event"></a>Как можно настроить оповещение о событии?

Оповещения Azure настраиваются только для метрик. Создайте пользовательскую метрику, пороговое значение которой будет нарушаться при наступлении события. Затем задайте предупреждения для метрики hello. Обратите внимание, что: вы получите уведомление всякий раз, когда метрика hello пересекает hello пороговое значение в любом направлении; Вы не сможете получить уведомления до hello первый пересечения, независимо от того, является ли начальное значение hello большими или очень маленькими; всегда является задержку в несколько минут.

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>Взимается ли плата за передачу данных между веб-приложением Azure и Application Insights?

* Если ваше веб-приложение Azure размещается в центре данных с конечной точкой сбора Application Insights, плата не взимается. 
* Если в центре данных размещения нет конечной точки сбора, то за передачу данных телеметрии приложения будет взиматься [плата за передачу исходящих данных Azure](https://azure.microsoft.com/pricing/details/bandwidth/).

Это не зависит от того, где размещается ресурс Application Insights. Он просто зависит от распространения hello нашей конечных точек.

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>Можно отправить портале Application Insights toohello телеметрии?

Мы рекомендуем использовать наши пакеты SDK и использовать hello API пакета SDK (app-insights-api-custom-events-metrics.md). Имеются hello пакета SDK для различных вариантов [платформы](app-insights-platforms.md). Эти пакеты SDK управляют буферизацией, сжатием, регулированием, повторными попытками и другими операциями. Здравствуйте, однако [схемы приема](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema) и [протокол конечной точки](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md) являются открытыми.

## <a name="can-i-monitor-an-intranet-web-server"></a>Можно ли отслеживать веб-сервер в интрасети?

Есть два способа.

### <a name="firewall-door"></a>Разрешение в брандмауэре

Разрешить ваши конечные точки web server toosend телеметрии tooour https://dc.services.visualstudio.com:443 и https://rt.services.visualstudio.com:443. 

### <a name="proxy"></a>Прокси-сервер

Маршрутизировать трафик от шлюза tooa сервер в интрасети, установив это в файле ApplicationInsights.config:

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

Шлюз должен отправить toohttps://dc.services.visualstudio.com:443 трафика hello/v2/отслеживания

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>Можно ли выполнять веб-тесты доступности на сервере в интрасети?

Наш [веб-тестов](app-insights-monitor-web-app-availability.md) проведение точки присутствия, распространяемые земного шара hello. Есть два решения.

* Брандмауэра дверца — Разрешить запросы сервера tooyour из [hello long и возможность изменения списка веб-агенты тестирования](app-insights-ip-addresses.md).
* Напишите собственный код toosend периодические запросы tooyour сервер из внутри вашей сети. Для этой цели можно выполнять веб-тесты Visual Studio. Инженер-испытатель Hello может послать результаты hello tooApplication аналитику, используя TrackAvailability() API hello.

## <a name="more-answers"></a>Другие ответы
* [Форум Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md
