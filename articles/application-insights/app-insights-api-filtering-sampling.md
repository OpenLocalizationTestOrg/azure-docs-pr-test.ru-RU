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
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a><span data-ttu-id="f83b5-103">Фильтрация и предварительной обработки данных телеметрии из hello пакет SDK Application Insights</span><span class="sxs-lookup"><span data-stu-id="f83b5-103">Filtering and preprocessing telemetry in hello Application Insights SDK</span></span>


<span data-ttu-id="f83b5-104">Можно записывать и настраивать подключаемые модули для hello пакет SDK Application Insights toocustomize как телеметрии отслеживаются и обработаны перед отправкой toohello служба Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f83b5-104">You can write and configure plug-ins for hello Application Insights SDK toocustomize how telemetry is captured and processed before it is sent toohello Application Insights service.</span></span>

* <span data-ttu-id="f83b5-105">[Выборка](app-insights-sampling.md) уменьшает объем hello телеметрии без влияния на статистике.</span><span class="sxs-lookup"><span data-stu-id="f83b5-105">[Sampling](app-insights-sampling.md) reduces hello volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="f83b5-106">Благодаря выборке связанные точки данных хранятся вместе, что облегчает навигацию между ними во время диагностики проблемы.</span><span class="sxs-lookup"><span data-stu-id="f83b5-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="f83b5-107">На портале hello hello общего числа, умноженному toocompensate для выборки hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-107">In hello portal, hello total counts are multiplied toocompensate for hello sampling.</span></span>
* <span data-ttu-id="f83b5-108">Фильтрация с помощью телеметрии процессоров [для ASP.NET](#filtering) или [Java](app-insights-java-filter-telemetry.md) позволяет выбрать или изменить данные телеметрии из пакета SDK для hello перед отправкой toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="f83b5-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in hello SDK before it is sent toohello server.</span></span> <span data-ttu-id="f83b5-109">Например можно сократить объем hello телеметрии, исключив из программы-роботы запросов.</span><span class="sxs-lookup"><span data-stu-id="f83b5-109">For example, you could reduce hello volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="f83b5-110">Однако фильтрации более общее трафик tooreducing подход, чем при выборке.</span><span class="sxs-lookup"><span data-stu-id="f83b5-110">But filtering is a more basic approach tooreducing traffic than sampling.</span></span> <span data-ttu-id="f83b5-111">Позволяет контролировать то, что передается, но у вас есть toobe виду, что оно влияет на статистике - например, если нужно отфильтровать всех успешных запросов.</span><span class="sxs-lookup"><span data-stu-id="f83b5-111">It allows you more control over what is transmitted, but you have toobe aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="f83b5-112">[Инициализаторы телеметрии добавлять свойства](#add-properties) tooany телеметрии, отправленных из приложений, включая данные телеметрии из стандартных модулях hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-112">[Telemetry Initializers add properties](#add-properties) tooany telemetry sent from your app, including telemetry from hello standard modules.</span></span> <span data-ttu-id="f83b5-113">Например можно добавить вычисляемые значения; или номера версий, какие данные hello toofilter hello портала.</span><span class="sxs-lookup"><span data-stu-id="f83b5-113">For example, you could add calculated values; or version numbers by which toofilter hello data in hello portal.</span></span>
* <span data-ttu-id="f83b5-114">[Hello API пакета SDK](app-insights-api-custom-events-metrics.md) используется toosend пользовательские события и метрики.</span><span class="sxs-lookup"><span data-stu-id="f83b5-114">[hello SDK API](app-insights-api-custom-events-metrics.md) is used toosend custom events and metrics.</span></span>

<span data-ttu-id="f83b5-115">Перед началом работы:</span><span class="sxs-lookup"><span data-stu-id="f83b5-115">Before you start:</span></span>

* <span data-ttu-id="f83b5-116">Установите hello Application Insights [пакет SDK для ASP.NET](app-insights-asp-net.md) или [пакета SDK для Java](app-insights-java-get-started.md) в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="f83b5-116">Install hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="f83b5-117">Фильтрация: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="f83b5-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="f83b5-118">Такой подход позволяет непосредственно контролировать то, что включаются или исключаются из потока данных телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-118">This technique gives you more direct control over what is included or excluded from hello telemetry stream.</span></span> <span data-ttu-id="f83b5-119">Этот метод можно использовать совместно с выборкой или по отдельности.</span><span class="sxs-lookup"><span data-stu-id="f83b5-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="f83b5-120">телеметрии toofilter процессора телеметрии и затем зарегистрируйте его в пакет SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-120">toofilter telemetry, you write a telemetry processor and register it with hello SDK.</span></span> <span data-ttu-id="f83b5-121">Все данные телеметрии проходит через процессора, и вы можете toodrop его из hello потока или добавить свойства.</span><span class="sxs-lookup"><span data-stu-id="f83b5-121">All telemetry goes through your processor, and you can choose toodrop it from hello stream, or add properties.</span></span> <span data-ttu-id="f83b5-122">Сюда входят стандартные модули hello как сборщик запрос HTTP hello и hello зависимостей сборщика данных телеметрии, а также данные телеметрии, созданный самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="f83b5-122">This includes telemetry from hello standard modules such as hello HTTP request collector and hello dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="f83b5-123">Например, можно отфильтровать данные телеметрии о запросах из программ-роботов или успешных вызовах зависимости.</span><span class="sxs-lookup"><span data-stu-id="f83b5-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="f83b5-124">Фильтрация hello телеметрии, отправленные hello SDK с помощью процессоров могут исказить статистику hello портале hello и сделать его сложно toofollow связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="f83b5-124">Filtering hello telemetry sent from hello SDK using processors can skew hello statistics that you see in hello portal, and make it difficult toofollow related items.</span></span>
>
> <span data-ttu-id="f83b5-125">Вместо этого попробуйте использовать [выборку](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="f83b5-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="f83b5-126">Создание обработчика данных телеметрии (C#)</span><span class="sxs-lookup"><span data-stu-id="f83b5-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="f83b5-127">Убедитесь, что hello пакет SDK Application Insights в проект версии 2.0.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f83b5-127">Verify that hello Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="f83b5-128">Щелкните правой кнопкой мыши проект в обозревателе решений Visual Studio и выберите "Управление пакетами NuGet".</span><span class="sxs-lookup"><span data-stu-id="f83b5-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="f83b5-129">В диспетчере пакетов NuGet выберите Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="f83b5-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="f83b5-130">Фильтр, toocreate реализовать ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="f83b5-130">toocreate a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="f83b5-131">Это еще одна точка расширения, как и модуль телеметрии, инициализатор телеметрии или канал телеметрии.</span><span class="sxs-lookup"><span data-stu-id="f83b5-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="f83b5-132">Обратите внимание, что обработчики данных телеметрии создают цепь обработки.</span><span class="sxs-lookup"><span data-stu-id="f83b5-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="f83b5-133">При создании экземпляра процессора телеметрии, передаваемому процессоров следующего toohello ссылку в цепочке hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-133">When you instantiate a telemetry processor, you pass a link toohello next processor in hello chain.</span></span> <span data-ttu-id="f83b5-134">Когда точки данных телеметрии передается методу toohello, он выполняет свой код и затем вызывает hello процессоров следующего телеметрии в цепочке hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-134">When a telemetry data point is passed toohello Process method, it does its work and then calls hello next Telemetry Processor in hello chain.</span></span>

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
1. <span data-ttu-id="f83b5-135">В файл ApplicationInsights.config вставьте следующее:</span><span class="sxs-lookup"><span data-stu-id="f83b5-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="f83b5-136">(Это hello один раздел, где инициализировать фильтр выборки.)</span><span class="sxs-lookup"><span data-stu-id="f83b5-136">(This is hello same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="f83b5-137">Строковые значения можно передать в файле .config hello, предоставляя открытые именованные свойства в классе.</span><span class="sxs-lookup"><span data-stu-id="f83b5-137">You can pass string values from hello .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="f83b5-138">Будьте внимательны, имя типа toomatch hello и любые имена свойств в классе toohello файл .config hello и имена свойств в коде hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-138">Take care toomatch hello type name and any property names in hello .config file toohello class and property names in hello code.</span></span> <span data-ttu-id="f83b5-139">Если файл .config hello ссылается на несуществующий тип или свойство, hello SDK может выполняться не toosend любой телеметрии.</span><span class="sxs-lookup"><span data-stu-id="f83b5-139">If hello .config file references a non-existent type or property, hello SDK may silently fail toosend any telemetry.</span></span>
>
>

<span data-ttu-id="f83b5-140">**Кроме того** можно инициализировать фильтр hello в коде.</span><span class="sxs-lookup"><span data-stu-id="f83b5-140">**Alternatively,** you can initialize hello filter in code.</span></span> <span data-ttu-id="f83b5-141">В классе подходящий инициализации — например AppStart Global.asax.cs - вставьте процессор в цепочку hello:</span><span class="sxs-lookup"><span data-stu-id="f83b5-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into hello chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="f83b5-142">Клиенты TelemetryClient, созданные после этой точки, будут использовать обработчики.</span><span class="sxs-lookup"><span data-stu-id="f83b5-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="f83b5-143">Примеры фильтров</span><span class="sxs-lookup"><span data-stu-id="f83b5-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="f83b5-144">Искусственные запросы</span><span class="sxs-lookup"><span data-stu-id="f83b5-144">Synthetic requests</span></span>
<span data-ttu-id="f83b5-145">Вы можете отфильтровывать программы-роботы и веб-тесты.</span><span class="sxs-lookup"><span data-stu-id="f83b5-145">Filter out bots and web tests.</span></span> <span data-ttu-id="f83b5-146">Несмотря на то, что дает обозревателя метрик hello toofilter параметр искусственных источники, этот параметр уменьшает трафик с помощью фильтрации их в пакет SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-146">Although Metrics Explorer gives you hello option toofilter out synthetic sources, this option reduces traffic by filtering them at hello SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="f83b5-147">Сбой проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f83b5-147">Failed authentication</span></span>
<span data-ttu-id="f83b5-148">Отфильтруйте запросы с ответом 401.</span><span class="sxs-lookup"><span data-stu-id="f83b5-148">Filter out requests with a "401" response.</span></span>

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

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="f83b5-149">Фильтрация быстрых удаленных вызовов зависимостей</span><span class="sxs-lookup"><span data-stu-id="f83b5-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="f83b5-150">Если требуется только toodiagnose вызовов, которые выполняются медленно, отфильтровывайте те fast hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-150">If you only want toodiagnose calls that are slow, filter out hello fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="f83b5-151">Это приведет к искажению hello статистические данные, отображаемые на портале hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-151">This will skew hello statistics you see on hello portal.</span></span> <span data-ttu-id="f83b5-152">Диаграмма зависимостей Hello будет выглядеть как hello зависимостей, вызываются все ошибки.</span><span class="sxs-lookup"><span data-stu-id="f83b5-152">hello dependency chart will look as if hello dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="f83b5-153">Неполадки диагностики зависимостей</span><span class="sxs-lookup"><span data-stu-id="f83b5-153">Diagnose dependency issues</span></span>
<span data-ttu-id="f83b5-154">[Этот блог](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) описаны проблемы зависимостей проекта toodiagnose отправляя toodependencies регулярных проверок связи автоматически.</span><span class="sxs-lookup"><span data-stu-id="f83b5-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project toodiagnose dependency issues by automatically sending regular pings toodependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="f83b5-155">Добавление свойств: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="f83b5-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="f83b5-156">Использование данных телеметрии инициализаторы toodefine глобальные свойства, которые отправляются с все данные телеметрии; и toooverride поведения модулей стандартной телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-156">Use telemetry initializers toodefine global properties that are sent with all telemetry; and toooverride selected behavior of hello standard telemetry modules.</span></span>

<span data-ttu-id="f83b5-157">Например hello Application Insights для веб-пакет собирает данные телеметрии, о HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="f83b5-157">For example, hello Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="f83b5-158">По умолчанию любой запрос с кодом ответа > = 400 он помечает как неудавшийся.</span><span class="sxs-lookup"><span data-stu-id="f83b5-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="f83b5-159">Однако если вы хотите tootreat 400 как успех, можно указать инициализатор телеметрии, который задает свойство Success hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-159">But if you want tootreat 400 as a success, you can provide a telemetry initializer that sets hello Success property.</span></span>

<span data-ttu-id="f83b5-160">Если указан инициализатор телеметрии, он вызывается всякий раз, когда любой из hello Track*() вызывать методы.</span><span class="sxs-lookup"><span data-stu-id="f83b5-160">If you provide a telemetry initializer, it is called whenever any of hello Track*() methods is called.</span></span> <span data-ttu-id="f83b5-161">Сюда входят методы, называемые модулями стандартной телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="f83b5-161">This includes methods called by hello standard telemetry modules.</span></span> <span data-ttu-id="f83b5-162">Обычно эти модули не задают свойство, которое уже задал инициализатор.</span><span class="sxs-lookup"><span data-stu-id="f83b5-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="f83b5-163">**Определение инициализатора**</span><span class="sxs-lookup"><span data-stu-id="f83b5-163">**Define your initializer**</span></span>

<span data-ttu-id="f83b5-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="f83b5-164">*C#*</span></span>

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

<span data-ttu-id="f83b5-165">**Загрузка инициализатора**</span><span class="sxs-lookup"><span data-stu-id="f83b5-165">**Load your initializer**</span></span>

<span data-ttu-id="f83b5-166">В ApplicationInsights.config.:</span><span class="sxs-lookup"><span data-stu-id="f83b5-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="f83b5-167">*Кроме того* можно создать экземпляр инициализатора hello в коде, например в Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="f83b5-167">*Alternatively,* you can instantiate hello initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="f83b5-168">Дополнительную информацию см. здесь.</span><span class="sxs-lookup"><span data-stu-id="f83b5-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="f83b5-169">Инициализаторы телеметрии JavaScript</span><span class="sxs-lookup"><span data-stu-id="f83b5-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="f83b5-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="f83b5-170">*JavaScript*</span></span>

<span data-ttu-id="f83b5-171">Вставьте инициализатор телеметрии сразу после кода инициализации hello, полученный на портале hello:</span><span class="sxs-lookup"><span data-stu-id="f83b5-171">Insert a telemetry initializer immediately after hello initialization code that you got from hello portal:</span></span>

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

<span data-ttu-id="f83b5-172">Сводка hello не настраиваемые свойства, предоставляемые hello telemetryItem. в разделе [Экспорт модели данных приложения аналитики](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="f83b5-172">For a summary of hello non-custom properties available on hello telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="f83b5-173">Вы можете добавить любое количество инициализаторов по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="f83b5-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="f83b5-174">ITelemetryProcessor и ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="f83b5-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="f83b5-175">Что такое hello различие между процессорами телеметрии и телеметрии инициализаторы</span><span class="sxs-lookup"><span data-stu-id="f83b5-175">What's hello difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="f83b5-176">Существуют некоторые перекрытия в работе с ними: оба могут иметь tootelemetry используется tooadd свойства.</span><span class="sxs-lookup"><span data-stu-id="f83b5-176">There are some overlaps in what you can do with them: both can be used tooadd properties tootelemetry.</span></span>
* <span data-ttu-id="f83b5-177">Свойство TelemetryInitializers всегда выполняется перед TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="f83b5-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="f83b5-178">TelemetryProcessors позволяют toocompletely заменить или удалить элемент телеметрии.</span><span class="sxs-lookup"><span data-stu-id="f83b5-178">TelemetryProcessors allow you toocompletely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="f83b5-179">Свойство TelemetryProcessors не обрабатывает данные телеметрии счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="f83b5-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="f83b5-180">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="f83b5-180">Reference docs</span></span>
* [<span data-ttu-id="f83b5-181">Обзор API</span><span class="sxs-lookup"><span data-stu-id="f83b5-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="f83b5-182">Справочник по ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f83b5-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="f83b5-183">Код пакета SDK</span><span class="sxs-lookup"><span data-stu-id="f83b5-183">SDK Code</span></span>
* [<span data-ttu-id="f83b5-184">Базовый пакет SDK для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f83b5-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="f83b5-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="f83b5-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="f83b5-186">Пакет SDK для JavaScript</span><span class="sxs-lookup"><span data-stu-id="f83b5-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="f83b5-187"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f83b5-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="f83b5-188">Поиск в Application Insights</span><span class="sxs-lookup"><span data-stu-id="f83b5-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="f83b5-189">Выборка</span><span class="sxs-lookup"><span data-stu-id="f83b5-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="f83b5-190">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f83b5-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
