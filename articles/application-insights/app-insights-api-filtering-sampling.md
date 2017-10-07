---
title: "aaaFiltering и предварительной обработки в hello Azure пакет SDK Application Insights | Документы Microsoft"
description: "Написания процессоров телеметрии и телеметрии инициализаторы для hello SDK toofilter или добавить свойства toohello данных перед отправкой портале Application Insights toohello телеметрии hello."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>Фильтрация и предварительной обработки данных телеметрии из hello пакет SDK Application Insights


Можно записывать и настраивать подключаемые модули для hello пакет SDK Application Insights toocustomize как телеметрии отслеживаются и обработаны перед отправкой toohello служба Application Insights.

* [Выборка](app-insights-sampling.md) уменьшает объем hello телеметрии без влияния на статистике. Благодаря выборке связанные точки данных хранятся вместе, что облегчает навигацию между ними во время диагностики проблемы. На портале hello hello общего числа, умноженному toocompensate для выборки hello.
* Фильтрация с помощью телеметрии процессоров [для ASP.NET](#filtering) или [Java](app-insights-java-filter-telemetry.md) позволяет выбрать или изменить данные телеметрии из пакета SDK для hello перед отправкой toohello сервера. Например можно сократить объем hello телеметрии, исключив из программы-роботы запросов. Однако фильтрации более общее трафик tooreducing подход, чем при выборке. Позволяет контролировать то, что передается, но у вас есть toobe виду, что оно влияет на статистике - например, если нужно отфильтровать всех успешных запросов.
* [Инициализаторы телеметрии добавлять свойства](#add-properties) tooany телеметрии, отправленных из приложений, включая данные телеметрии из стандартных модулях hello. Например можно добавить вычисляемые значения; или номера версий, какие данные hello toofilter hello портала.
* [Hello API пакета SDK](app-insights-api-custom-events-metrics.md) используется toosend пользовательские события и метрики.

Перед началом работы:

* Установите hello Application Insights [пакет SDK для ASP.NET](app-insights-asp-net.md) или [пакета SDK для Java](app-insights-java-get-started.md) в вашем приложении.

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>Фильтрация: ITelemetryProcessor
Такой подход позволяет непосредственно контролировать то, что включаются или исключаются из потока данных телеметрии hello. Этот метод можно использовать совместно с выборкой или по отдельности.

телеметрии toofilter процессора телеметрии и затем зарегистрируйте его в пакет SDK для hello. Все данные телеметрии проходит через процессора, и вы можете toodrop его из hello потока или добавить свойства. Сюда входят стандартные модули hello как сборщик запрос HTTP hello и hello зависимостей сборщика данных телеметрии, а также данные телеметрии, созданный самостоятельно. Например, можно отфильтровать данные телеметрии о запросах из программ-роботов или успешных вызовах зависимости.

> [!WARNING]
> Фильтрация hello телеметрии, отправленные hello SDK с помощью процессоров могут исказить статистику hello портале hello и сделать его сложно toofollow связанные элементы.
>
> Вместо этого попробуйте использовать [выборку](app-insights-sampling.md).
>
>

### <a name="create-a-telemetry-processor-c"></a>Создание обработчика данных телеметрии (C#)
1. Убедитесь, что hello пакет SDK Application Insights в проект версии 2.0.0 или более поздней версии. Щелкните правой кнопкой мыши проект в обозревателе решений Visual Studio и выберите "Управление пакетами NuGet". В диспетчере пакетов NuGet выберите Microsoft.ApplicationInsights.Web.
2. Фильтр, toocreate реализовать ITelemetryProcessor. Это еще одна точка расширения, как и модуль телеметрии, инициализатор телеметрии или канал телеметрии.

    Обратите внимание, что обработчики данных телеметрии создают цепь обработки. При создании экземпляра процессора телеметрии, передаваемому процессоров следующего toohello ссылку в цепочке hello. Когда точки данных телеметрии передается методу toohello, он выполняет свой код и затем вызывает hello процессоров следующего телеметрии в цепочке hello.

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. В файл ApplicationInsights.config вставьте следующее:

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(Это hello один раздел, где инициализировать фильтр выборки.)

Строковые значения можно передать в файле .config hello, предоставляя открытые именованные свойства в классе.

> [!WARNING]
> Будьте внимательны, имя типа toomatch hello и любые имена свойств в классе toohello файл .config hello и имена свойств в коде hello. Если файл .config hello ссылается на несуществующий тип или свойство, hello SDK может выполняться не toosend любой телеметрии.
>
>

**Кроме того** можно инициализировать фильтр hello в коде. В классе подходящий инициализации — например AppStart Global.asax.cs - вставьте процессор в цепочку hello:

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

Клиенты TelemetryClient, созданные после этой точки, будут использовать обработчики.

### <a name="example-filters"></a>Примеры фильтров
#### <a name="synthetic-requests"></a>Искусственные запросы
Вы можете отфильтровывать программы-роботы и веб-тесты. Несмотря на то, что дает обозревателя метрик hello toofilter параметр искусственных источники, этот параметр уменьшает трафик с помощью фильтрации их в пакет SDK для hello.

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>Сбой проверки подлинности
Отфильтруйте запросы с ответом 401.

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>Фильтрация быстрых удаленных вызовов зависимостей
Если требуется только toodiagnose вызовов, которые выполняются медленно, отфильтровывайте те fast hello.

> [!NOTE]
> Это приведет к искажению hello статистические данные, отображаемые на портале hello. Диаграмма зависимостей Hello будет выглядеть как hello зависимостей, вызываются все ошибки.
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a>Неполадки диагностики зависимостей
[Этот блог](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) описаны проблемы зависимостей проекта toodiagnose отправляя toodependencies регулярных проверок связи автоматически.


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>Добавление свойств: ITelemetryInitializer
Использование данных телеметрии инициализаторы toodefine глобальные свойства, которые отправляются с все данные телеметрии; и toooverride поведения модулей стандартной телеметрии hello.

Например hello Application Insights для веб-пакет собирает данные телеметрии, о HTTP-запросов. По умолчанию любой запрос с кодом ответа > = 400 он помечает как неудавшийся. Однако если вы хотите tootreat 400 как успех, можно указать инициализатор телеметрии, который задает свойство Success hello.

Если указан инициализатор телеметрии, он вызывается всякий раз, когда любой из hello Track*() вызывать методы. Сюда входят методы, называемые модулями стандартной телеметрии hello. Обычно эти модули не задают свойство, которое уже задал инициализатор.

**Определение инициализатора**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**Загрузка инициализатора**

В ApplicationInsights.config.:

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*Кроме того* можно создать экземпляр инициализатора hello в коде, например в Global.aspx.cs:

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[Дополнительную информацию см. здесь.](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>Инициализаторы телеметрии JavaScript
*JavaScript*

Вставьте инициализатор телеметрии сразу после кода инициализации hello, полученный на портале hello:

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

Сводка hello не настраиваемые свойства, предоставляемые hello telemetryItem. в разделе [Экспорт модели данных приложения аналитики](app-insights-export-data-model.md).

Вы можете добавить любое количество инициализаторов по своему усмотрению.

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor и ITelemetryInitializer
Что такое hello различие между процессорами телеметрии и телеметрии инициализаторы

* Существуют некоторые перекрытия в работе с ними: оба могут иметь tootelemetry используется tooadd свойства.
* Свойство TelemetryInitializers всегда выполняется перед TelemetryProcessors.
* TelemetryProcessors позволяют toocompletely заменить или удалить элемент телеметрии.
* Свойство TelemetryProcessors не обрабатывает данные телеметрии счетчика производительности.


## <a name="reference-docs"></a>Справочная документация
* [Обзор API](app-insights-api-custom-events-metrics.md)
* [Справочник по ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>Код пакета SDK
* [Базовый пакет SDK для ASP.NET](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Пакет SDK для JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>Дальнейшие действия
* [Поиск в Application Insights](app-insights-diagnostic-search.md)
* [Выборка](app-insights-sampling.md)
* [Устранение неполадок](app-insights-troubleshoot-faq.md)
