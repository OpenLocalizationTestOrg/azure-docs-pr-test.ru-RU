---
title: "журналы трассировки aaaExplore .NET в Application Insights"
description: "Поиск журналов, созданных с помощью Trace, Log4Net или NLog."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>Просмотр журналов трассировки .NET в Application Insights
При использовании NLog, log4Net или System.Diagnostic.Trace для диагностической трассировки в приложении ASP.NET, что журналы отправлено слишком[Azure Application Insights][start], где вы можете анализировать и поиска их. Журналы будут объединены с другими hello телеметрии, поступающих из своего приложения, чтобы вы могли определить hello трассировки, связанные с обслуживанием каждого пользовательского запроса и сопоставлять их с другими событиями и отчеты об исключениях.

> [!NOTE]
> Требуется модуля записи журнала hello? Это полезный адаптер для сторонних средств ведения журнала, но если вы еще не используете NLog, log4Net или System.Diagnostics.Trace, рассмотрите возможность вызова [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) напрямую.
>
>

## <a name="install-logging-on-your-app"></a>Установка ведения журнала в приложении
Установите выбранную платформу ведения журналов в своем проекте. При этом должна появиться запись в файлах app.config или web.config.

Если вы используете System.Diagnostics.Trace, необходимо tooadd tooweb.config входа.

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>Настройка журналов toocollect Application Insights
**[Добавление проекта Application Insights tooyour](app-insights-asp-net.md)**  Если вы еще не сделали, еще. Вы увидите параметр tooinclude hello сборщика данных журнала.

Или выберите **Настроить Application Insights** , щелкнув правой кнопкой мыши на своем проекте в обозревателе решений. Выберите параметр hello слишком**настройки сбора данных трассировки**.

*Вы не видите меню Application Insights или параметр для включения сборщика журналов?* Попробуйте выполнить [Устранение неполадок](#troubleshooting).

## <a name="manual-installation"></a>Ручная установка
Используйте этот метод, если ваш тип проекта не поддерживается программой установки Application Insights hello (например Windows рабочего стола проект).

1. Если планируется toouse log4Net или NLog, установите его в своем проекте.
2. В обозревателе решений щелкните правой кнопкой мыши ваш проект и выберите **Управление пакетами NuGet**.
3. Поиск Application Insights
4. Выберите соответствующий пакет hello - один из:

   * Microsoft.ApplicationInsights.TraceListener (вызовы методов System.Diagnostics.Trace toocapture)
   * Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource события)
   * Microsoft.ApplicationInsights.EtwListener (toocapture события трассировки событий Windows)
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

пакет NuGet Hello устанавливает необходимые сборки hello, а также изменяет web.config или app.config.

## <a name="insert-diagnostic-log-calls"></a>Вставка вызовов журнала диагностики
При использовании System.Diagnostics.Trace типичный вызов будет выглядеть следующим образом:

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

если вы предпочитаете log4net или NLog:

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>Использование событий EventSource
Можно настроить [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) tooApplication toobe отправки событий аналитики как трассировок. Сначала установите hello `Microsoft.ApplicationInsights.EventSourceListener` пакет NuGet. Затем измените `TelemetryModules` раздел hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) файла.

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

Для каждого источника можно задать следующие параметры hello.
 * `Name`Указывает имя hello hello EventSource toocollect.
 * `Level`Указывает hello toocollect уровня ведения журнала. Возможные значения: `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(Необязательно) задает целочисленное значение hello toouse сочетания ключевых слов.

## <a name="using-diagnosticsource-events"></a>Использование событий DiagnosticSource
Можно настроить [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) tooApplication toobe отправки событий аналитики как трассировок. Сначала установите hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) пакет NuGet. Затем измените hello `TelemetryModules` раздел hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) файла.

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

Для каждого DiagnosticSource требуется tootrace, добавьте запись с hello `Name` toohello имя вашей DiagnosticSource набора атрибутов.

## <a name="using-etw-events"></a>Использование событий трассировки событий Windows
Вы можете настроить отправлен tooApplication аналитики как трассировки toobe события трассировки событий Windows. Сначала установите hello `Microsoft.ApplicationInsights.EtwCollector` пакет NuGet. Затем измените `TelemetryModules` раздел hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) файла.

> [!NOTE] 
> События трассировки событий Windows могут собираться только в том случае, если hello процесс размещения hello SDK выполняется под идентификатором, который является членом группы «Пользователи журналов производительности» или Администраторы.

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

Для каждого источника можно задать следующие параметры hello.
 * `ProviderName`— Имя hello toocollect поставщика трассировки событий Windows hello.
 * `ProviderGuid`Указывает hello GUID toocollect поставщика трассировки событий Windows hello, можно использовать вместо `ProviderName`.
 * `Level`Задает hello toocollect уровня ведения журнала. Возможные значения: `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(Необязательно) задает hello целочисленное значение toouse сочетания ключевое слово.

## <a name="using-hello-trace-api-directly"></a>Непосредственное использование hello трассировки API
API трассировки Application Insights hello можно вызывать напрямую. Этот API использовать адаптеры ведения журналов Hello.

Например:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

Преимуществом TrackTrace является относительно большие объемы данных можно поместить в сообщение hello. например данных POST.

Кроме того можно добавить сообщение tooyour уровня серьезности. И, как и другие данные телеметрии, можно добавить значения свойств, которые используются toohelp фильтрации или поиска для разных наборов трассировок. Например:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

Это позволит вам, в [поиска][diagnostic], tooeasily отфильтровать все сообщения hello уровня серьезности конкретного связанные tooa определенной базы данных.

## <a name="explore-your-logs"></a>Просмотр журналов
Запустите приложение в режиме отладки или разверните его.

В колонке Общие сведения о приложении в [hello портале Application Insights][portal], выберите [поиска][diagnostic].

![В Application Insights выберите элемент «Поиск»](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![поиска](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

Можно, например:

* фильтровать трассировки журнала или элементы с определенными свойствами;
* просматривать подробные сведения конкретного элемента;
* Найти другие телеметрии связанные toohello того же запроса пользователя (то есть с hello таким же идентификатором операции)
* Сохранить конфигурацию hello этой страницы в список избранного

> [!NOTE]
> **Выборка.** Если приложение отправляет большой объем данных, и вы используете hello пакет SDK Application Insights для ASP.NET версии 2.0.0-beta3 или более поздней версии, функция адаптивной выборки hello может работать и отправьте доля телеметрии. [Дополнительная информация о выборке.](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>Дальнейшие действия
[Диагностика ошибок и исключений в ASP.NET][exceptions]

[Дополнительная информация о службе поиска][diagnostic].

## <a name="troubleshooting"></a>Устранение неполадок
### <a name="how-do-i-do-this-for-java"></a>Как это сделать в Java?
Используйте hello [адаптеров журнала Java](app-insights-java-trace-logs.md).

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>В контекстном меню проекта hello, нет возможности Application Insights
* Проверьте, установлены ли на этом компьютере средства Application Insights. В меню "Сервис, расширения и обновления" Visual Studio найдите "Средства Application Insights". Если он отсутствует в вкладку "установлено" hello, откройте вкладку hello в интерактивном режиме и установите его.
* Возможно, этот тип проекта не поддерживается средствами Application Insights. Используйте [установку вручную](#manual-installation).

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Параметр адаптера не журнала в средстве настройки hello
* Вы должны платформы ведения журналов tooinstall hello.
* Если вы используете System.Diagnostics.Trace, убедитесь, что это средство [настроено в `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).
* У вас есть hello последнюю версию Application Insights В Visual Studio **средства** меню, выберите **расширения и обновления**и откройте hello **обновления** вкладки. Если есть средства аналитические средства разработчика, щелкните tooupdate его.

### <a name="emptykey"></a>Появляется сообщение об ошибке «ключ инструментирования не может быть пустым»
Похоже, вы установили hello, ведение журнала пакета Nuget адаптера без установки Application Insights.

В обозревателе решений щелкните правой кнопкой мыши `ApplicationInsights.config` и выберите **Обновить Application Insights**. Появится диалоговое окно, которое предлагает toosign в tooAzure и либо создать ресурс Application Insights или повторно использовать уже существующий. Это должно исправить проблему.

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>Я отображаются трассировки диагностики поиска, но не hello других событий
Иногда может потребоваться время для всех hello события и запросы tooget через конвейер hello.

### <a name="limits"></a>Какой объем данных сохраняется?
Несколько факторов влияют на объем данных, хранящихся в hello. В разделе hello [ограничения](app-insights-api-custom-events-metrics.md#limits) раздел страницы метрики hello клиента событий для получения дополнительной информации. 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>Я не вижу некоторые из записей журнала hello ожидаемых
Если приложение отправляет большой объем данных, и вы используете hello пакет SDK Application Insights для ASP.NET версии 2.0.0-beta3 или более поздней версии, функция адаптивной выборки hello может работать и отправьте доля телеметрии. [Дополнительная информация о выборке.](app-insights-sampling.md)

## <a name="add"></a>Дальнейшие действия
* [Наблюдение за доступностью и скоростью реагирования веб-сайта][availability]
* [Устранение неполадок][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
