---
title: "Фильтрация и предварительная обработка в пакете SDK для Azure Application Insights | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как создать обработчики и инициализаторы телеметрии для того, чтобы пакет SDK мог выполнять фильтрацию, и как добавлять свойства к данным перед отправкой данных телеметрии на портал Application Insights."
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
ms.openlocfilehash: 17e66775dd2cd1c858594102f1ddb32e2fbbccc8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="a9ae9-103">Фильтрация и предварительная обработка данных телеметрии в пакете SDK для Application Insights</span><span class="sxs-lookup"><span data-stu-id="a9ae9-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="a9ae9-104">Чтобы настроить способ сбора и обработки данных телеметрии перед их отправкой в службу Application Insights, можно написать и настроить подключаемые модули для пакета SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="a9ae9-105">[Выборка](app-insights-sampling.md) сокращает объем данных телеметрии, не искажая статистические данные.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="a9ae9-106">Благодаря выборке связанные точки данных хранятся вместе, что облегчает навигацию между ними во время диагностики проблемы.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="a9ae9-107">На портале общее количество умножается, чтобы компенсировать выборку.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="a9ae9-108">Фильтрация с использованием обработчиков данных телеметрии для [ASP.NET](#filtering) или [Java](app-insights-java-filter-telemetry.md) позволяет выбирать или изменять данные телеметрии в пакете SDK перед отправкой на сервер.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="a9ae9-109">Например, можно уменьшить объем данных телеметрии, исключив запросы от роботов.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="a9ae9-110">Но с помощью фильтрации сократить трафик проще, чем при помощи выборки.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="a9ae9-111">Хотя фильтрация обеспечивает более жесткий контроль над передаваемыми данными, следует не забывать и о влиянии на статистику (например, когда отфильтровываются все успешные запросы).</span><span class="sxs-lookup"><span data-stu-id="a9ae9-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="a9ae9-112">[Инициализаторы телеметрии добавляют свойства](#add-properties) к любым данным телеметрии, отправляемым из вашего приложения, включая данные телеметрии из стандартных модулей.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="a9ae9-113">Например, можно добавить вычисляемые значения или номера версий, по которым будут отфильтрованы данные на портале.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="a9ae9-114">[API пакета SDK](app-insights-api-custom-events-metrics.md) используется для отправки пользовательских событий и показателей.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="a9ae9-115">Перед началом работы:</span><span class="sxs-lookup"><span data-stu-id="a9ae9-115">Before you start:</span></span>

* <span data-ttu-id="a9ae9-116">Установите [пакет SDK Application Insights для ASP.NET](app-insights-asp-net.md) или [пакет SDK Application Insights для Java](app-insights-java-get-started.md) в свое приложение.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="a9ae9-117">Фильтрация: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="a9ae9-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="a9ae9-118">Такой подход позволяет более тщательно и непосредственно контролировать включение элементов в поток данных телеметрии и исключение из него.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="a9ae9-119">Этот метод можно использовать совместно с выборкой или по отдельности.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="a9ae9-120">Для фильтрации данных телеметрии нужно создать обработчик данных телеметрии и зарегистрировать его с помощью пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="a9ae9-121">Все данные телеметрии обрабатываются процессором, и можно исключить их из потока или добавить свойства.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="a9ae9-122">Сюда входят данные телеметрии из стандартных модулей, таких как сборщик запросов HTTP и сборщик зависимостей, а также данные телеметрии, созданные вами самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="a9ae9-123">Например, можно отфильтровать данные телеметрии о запросах из программ-роботов или успешных вызовах зависимости.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="a9ae9-124">Фильтрация данных телеметрии, отправленных из пакета SDK с помощью обработчиков, может исказить отображаемую на портале статистику и затруднить отслеживание связанных элементов.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="a9ae9-125">Вместо этого попробуйте использовать [выборку](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="a9ae9-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="a9ae9-126">Создание обработчика данных телеметрии (C#)</span><span class="sxs-lookup"><span data-stu-id="a9ae9-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="a9ae9-127">Убедитесь, что в проекте используется пакет SDK для Application Insights 2.0.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="a9ae9-128">Щелкните правой кнопкой мыши проект в обозревателе решений Visual Studio и выберите "Управление пакетами NuGet".</span><span class="sxs-lookup"><span data-stu-id="a9ae9-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="a9ae9-129">В диспетчере пакетов NuGet выберите Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="a9ae9-130">Чтобы создать фильтр, реализуйте обработчик ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="a9ae9-131">Это еще одна точка расширения, как и модуль телеметрии, инициализатор телеметрии или канал телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="a9ae9-132">Обратите внимание, что обработчики данных телеметрии создают цепь обработки.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="a9ae9-133">При создании экземпляра обработчика данных телеметрии ссылка передается в следующий обработчик в цепочке.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="a9ae9-134">Когда точка данных телеметрии передается в метод Process, он выполняет свою работу и затем вызывает следующий обработчик данных телеметрии в цепочке.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
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
1. <span data-ttu-id="a9ae9-135">В файл ApplicationInsights.config вставьте следующее:</span><span class="sxs-lookup"><span data-stu-id="a9ae9-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="a9ae9-136">(Это тот же раздел, где инициализируется фильтр выборки.)</span><span class="sxs-lookup"><span data-stu-id="a9ae9-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="a9ae9-137">Можно передавать строковые значения из файла конфигурации, указав открытые именованные свойства в классе.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="a9ae9-138">Будьте внимательны и задайте имя типа и имена свойств в файле конфигурации, совпадающие с именами классов и свойств в коде.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="a9ae9-139">Если файл конфигурации ссылается на несуществующий тип или свойство, пакет SDK может не суметь отправить данные телеметрии без уведомления.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="a9ae9-140">**Другой способ** — инициализировать фильтр в коде.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="a9ae9-141">Вставьте обработчик в цепочку в соответствующем классе инициализации, например AppStart в Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="a9ae9-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="a9ae9-142">Клиенты TelemetryClient, созданные после этой точки, будут использовать обработчики.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="a9ae9-143">Примеры фильтров</span><span class="sxs-lookup"><span data-stu-id="a9ae9-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="a9ae9-144">Искусственные запросы</span><span class="sxs-lookup"><span data-stu-id="a9ae9-144">Synthetic requests</span></span>
<span data-ttu-id="a9ae9-145">Вы можете отфильтровывать программы-роботы и веб-тесты.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-145">Filter out bots and web tests.</span></span> <span data-ttu-id="a9ae9-146">Хотя обозреватель метрик позволяет отфильтровывать искусственные источники, этот вариант сокращает трафик, фильтруя источники в пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="a9ae9-147">Сбой проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="a9ae9-147">Failed authentication</span></span>
<span data-ttu-id="a9ae9-148">Отфильтруйте запросы с ответом 401.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="a9ae9-149">Фильтрация быстрых удаленных вызовов зависимостей</span><span class="sxs-lookup"><span data-stu-id="a9ae9-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="a9ae9-150">Если требуется диагностировать только вызовы, которые выполняются медленно, можно отфильтровать быстрые вызовы.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="a9ae9-151">Это приведет к искажению статистических данных, отображаемых на портале.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="a9ae9-152">Диаграмма зависимостей будет выглядеть так, как будто все вызовы зависимостей завершились ошибкой.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="a9ae9-153">Неполадки диагностики зависимостей</span><span class="sxs-lookup"><span data-stu-id="a9ae9-153">Diagnose dependency issues</span></span>
<span data-ttu-id="a9ae9-154">[этом блоге](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) описан проект, в котором диагностика неполадок с зависимостями реализована в виде автоматического опрашивания зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="a9ae9-155">Добавление свойств: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="a9ae9-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="a9ae9-156">Используйте инициализаторы телеметрии, чтобы определить глобальные свойства, которые передаются со всеми данными телеметрии, и переопределить выбранное поведение стандартных модулей телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="a9ae9-157">Например, пакет Application Insights for Web собирает телеметрию о HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="a9ae9-158">По умолчанию любой запрос с кодом ответа > = 400 он помечает как неудавшийся.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="a9ae9-159">Если вам нужно, чтобы значение 400 считалось успешным, задайте инициализатор телеметрии, в котором можно настроить свойство Success.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="a9ae9-160">Если задан инициализатор телеметрии, он вызывается всякий раз, когда вызывается любой метод Track*().</span><span class="sxs-lookup"><span data-stu-id="a9ae9-160">If you provide a telemetry initializer, it is called whenever any of the Track*() methods is called.</span></span> <span data-ttu-id="a9ae9-161">Это относится также к модулям, вызываемым модулями стандартной телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="a9ae9-162">Обычно эти модули не задают свойство, которое уже задал инициализатор.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="a9ae9-163">**Определение инициализатора**</span><span class="sxs-lookup"><span data-stu-id="a9ae9-163">**Define your initializer**</span></span>

<span data-ttu-id="a9ae9-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="a9ae9-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
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
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="a9ae9-165">**Загрузка инициализатора**</span><span class="sxs-lookup"><span data-stu-id="a9ae9-165">**Load your initializer**</span></span>

<span data-ttu-id="a9ae9-166">В ApplicationInsights.config.:</span><span class="sxs-lookup"><span data-stu-id="a9ae9-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="a9ae9-167">*Другой способ* — создать экземпляр инициализатора в коде, например в Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="a9ae9-168">Дополнительную информацию см. здесь.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="a9ae9-169">Инициализаторы телеметрии JavaScript</span><span class="sxs-lookup"><span data-stu-id="a9ae9-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="a9ae9-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="a9ae9-170">*JavaScript*</span></span>

<span data-ttu-id="a9ae9-171">Вставьте инициализатор телеметрии сразу после кода инициализации, полученного на портале:</span><span class="sxs-lookup"><span data-stu-id="a9ae9-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

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

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="a9ae9-172">Краткое описание ненастраиваемых свойств, доступных в коллекции telemetryItem, см. в разделе [Экспорт модели данных Application Insights](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="a9ae9-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="a9ae9-173">Вы можете добавить любое количество инициализаторов по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="a9ae9-174">ITelemetryProcessor и ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="a9ae9-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="a9ae9-175">Различия между обработчиком и инициализатором данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="a9ae9-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="a9ae9-176">Обработчик и инициализатор данных телеметрии можно использовать для выполнения одинаковых заданий, например для добавления свойств в телеметрию.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="a9ae9-177">Свойство TelemetryInitializers всегда выполняется перед TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="a9ae9-178">Свойство TelemetryProcessors позволяет полностью заменить или удалить элемент телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="a9ae9-179">Свойство TelemetryProcessors не обрабатывает данные телеметрии счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="a9ae9-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="a9ae9-180">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="a9ae9-180">Reference docs</span></span>
* [<span data-ttu-id="a9ae9-181">Обзор API</span><span class="sxs-lookup"><span data-stu-id="a9ae9-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="a9ae9-182">Справочник по ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a9ae9-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="a9ae9-183">Код пакета SDK</span><span class="sxs-lookup"><span data-stu-id="a9ae9-183">SDK Code</span></span>
* [<span data-ttu-id="a9ae9-184">Базовый пакет SDK для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a9ae9-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="a9ae9-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="a9ae9-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="a9ae9-186">Пакет SDK для JavaScript</span><span class="sxs-lookup"><span data-stu-id="a9ae9-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="a9ae9-187"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a9ae9-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="a9ae9-188">Поиск в Application Insights</span><span class="sxs-lookup"><span data-stu-id="a9ae9-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="a9ae9-189">Выборка</span><span class="sxs-lookup"><span data-stu-id="a9ae9-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="a9ae9-190">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="a9ae9-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
