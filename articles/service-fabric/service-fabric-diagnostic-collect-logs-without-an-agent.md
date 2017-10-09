---
title: "журналы aaaCollect непосредственно из Azure Service Fabric с процессом службы | Microsoft Azure"
description: "Описание приложения могут отправлять журналы, напрямую tooa централизованно, например Azure Application Insights или Elasticsearch, не полагаясь на агент диагностики Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="6e466-103">Сбор журналов непосредственно из процесса службы Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e466-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="6e466-104">Внутрипроцессный сбор журналов</span><span class="sxs-lookup"><span data-stu-id="6e466-104">In-process log collection</span></span>
<span data-ttu-id="6e466-105">Сбор приложения журналов с помощью [расширения системы диагностики Azure](service-fabric-diagnostics-how-to-setup-wad.md) — это хороший вариант для **Azure Service Fabric** служб при небольших, набор hello журнала источники и назначения не изменяет часто и существует представляет собой простой сопоставление hello источников и их назначения.</span><span class="sxs-lookup"><span data-stu-id="6e466-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="6e466-106">Если нет, то альтернативой является toohave служб и отправлять свои журналы непосредственно tooa центрального расположения.</span><span class="sxs-lookup"><span data-stu-id="6e466-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="6e466-107">Этот процесс называется **внутрипроцессным сбором журналов** и имеет несколько потенциальных преимуществ.</span><span class="sxs-lookup"><span data-stu-id="6e466-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="6e466-108">*Простая настройка и развертывание.*</span><span class="sxs-lookup"><span data-stu-id="6e466-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="6e466-109">Конфигурация Hello сбора диагностических данных — просто частью конфигурации службы hello.</span><span class="sxs-lookup"><span data-stu-id="6e466-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="6e466-110">Это легко tooalways оставить его «синхронизировано» с hello остальной части приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6e466-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="6e466-111">Настройка каждого приложения или службы также является несложной задачей.</span><span class="sxs-lookup"><span data-stu-id="6e466-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="6e466-112">Сбор данных журнала на основе агентов обычно требуется отдельное развертывание и конфигурация диагностики агента hello, лишние административную задачу и потенциальный источник ошибок.</span><span class="sxs-lookup"><span data-stu-id="6e466-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="6e466-113">Часто имеется только один экземпляр агента hello допускается на каждую виртуальную машину (узел) и конфигурация агента hello является общим для всех приложений и служб, работающих на этом узле.</span><span class="sxs-lookup"><span data-stu-id="6e466-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="6e466-114">*Гибкость*</span><span class="sxs-lookup"><span data-stu-id="6e466-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="6e466-115">Hello приложение может отправлять данные hello везде, где он должен toogo, при условии, что имеется клиентская библиотека, которая поддерживает hello целевые системы хранения данных.</span><span class="sxs-lookup"><span data-stu-id="6e466-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="6e466-116">При необходимости можно добавлять новые расположения.</span><span class="sxs-lookup"><span data-stu-id="6e466-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="6e466-117">Можно реализовать сложные правила сбора, фильтрации и статистической обработки данных.</span><span class="sxs-lookup"><span data-stu-id="6e466-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="6e466-118">Сбор данных журнала на основе агентов часто ограничивается hello данных приемников, которые поддерживает агент hello.</span><span class="sxs-lookup"><span data-stu-id="6e466-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="6e466-119">Некоторые агенты являются расширяемыми.</span><span class="sxs-lookup"><span data-stu-id="6e466-119">Some agents are extensible.</span></span>

* <span data-ttu-id="6e466-120">*Доступ к данным приложения toointernal и контекстом*</span><span class="sxs-lookup"><span data-stu-id="6e466-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="6e466-121">Hello диагностики подсистемы, выполняющиеся внутри процесса hello приложения или службы можно легко дополнить hello трассировок с помощью контекстных сведений.</span><span class="sxs-lookup"><span data-stu-id="6e466-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="6e466-122">Сбор журналов на основе агентов, hello данные необходимо отправить агента tooan через механизм межпроцессного взаимодействия например трассировки событий Windows.</span><span class="sxs-lookup"><span data-stu-id="6e466-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="6e466-123">Однако при таком механизме могут возникнуть дополнительные ограничения.</span><span class="sxs-lookup"><span data-stu-id="6e466-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="6e466-124">Это возможно toocombine и выгода от обоих методов сбора.</span><span class="sxs-lookup"><span data-stu-id="6e466-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="6e466-125">На самом деле бывает hello наилучшим решением для многих приложений.</span><span class="sxs-lookup"><span data-stu-id="6e466-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="6e466-126">Коллекция на основе агента — это естественное решение для сбора журналов связанные toohello весь кластер и отдельных узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="6e466-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="6e466-127">Это намного более надежным способом, чем сбор журналов в процессе, toodiagnose проблемы при запуске службы и сбоев.</span><span class="sxs-lookup"><span data-stu-id="6e466-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="6e466-128">Кроме того многие службы, выполняющиеся внутри кластера Service Fabric, каждая служба, выполнив собственную коллекцию для внутрипроцессного журнала приведет многочисленные исходящие подключения из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="6e466-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="6e466-129">Большое количество исходящих подключений — сложная задача, для подсистемы сети hello и место назначения журналов hello.</span><span class="sxs-lookup"><span data-stu-id="6e466-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="6e466-130">Агент (например, агент [**системы диагностики Azure**](../cloud-services/cloud-services-dotnet-diagnostics.md)) может собирать данные от нескольких служб и отправлять все данные через небольшое число подключений, повышая производительность.</span><span class="sxs-lookup"><span data-stu-id="6e466-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="6e466-131">В этой статье показано, как tooset в процесс входа в коллекцию с помощью [ **EventFlow открытая библиотека**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="6e466-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="6e466-132">Другие библиотеки могут использоваться для hello же цели, но EventFlow имеет преимущество hello была разработана специально для внутрипроцессного журнала сбора и toosupport служб Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e466-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="6e466-133">Мы используем [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) как место назначения журналов hello.</span><span class="sxs-lookup"><span data-stu-id="6e466-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="6e466-134">Можно также использовать [**концентраторы событий**](https://azure.microsoft.com/services/event-hubs/) или [**Elasticsearch**](https://www.elastic.co/products/elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="6e466-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="6e466-135">Это просто вопрос установки соответствующего пакета NuGet и Настройка назначения «hello» в файле конфигурации EventFlow hello.</span><span class="sxs-lookup"><span data-stu-id="6e466-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="6e466-136">Дополнительные сведения о местах назначения журналов, отличных от Application Insights, см. в [документации по EventFlow](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="6e466-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="6e466-137">Добавление проекта служб Service Fabric tooa библиотеки EventFlow</span><span class="sxs-lookup"><span data-stu-id="6e466-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="6e466-138">Двоичные файлы EventFlow предоставляются как набор пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e466-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="6e466-139">tooadd EventFlow проект службы tooa Service Fabric, щелкните правой кнопкой мыши проект hello в hello обозреватель решений и выберите «Управление NuGet пакетов».</span><span class="sxs-lookup"><span data-stu-id="6e466-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="6e466-140">Перейдите на вкладку toohello «Просмотр» и выполните поиск «`Diagnostics.EventFlow`»:</span><span class="sxs-lookup"><span data-stu-id="6e466-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Пакеты NuGet EventFlow в диспетчере пакетов NuGet Visual Studio][1]

<span data-ttu-id="6e466-142">EventFlow, где размещается служба Hello должна включать соответствующие пакеты, в зависимости от hello источника и назначения для журналов приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6e466-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="6e466-143">Добавьте hello следующие пакеты:</span><span class="sxs-lookup"><span data-stu-id="6e466-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="6e466-144">(toocapture данных из класса EventSource hello службы и из стандартной EventSources, такие как *Майкрософт ServiceFabric* и *Microsoft ServiceFabric субъекты*)</span><span class="sxs-lookup"><span data-stu-id="6e466-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="6e466-145">(мы будем toosend hello журналы tooan Azure Application Insights ресурсов)</span><span class="sxs-lookup"><span data-stu-id="6e466-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="6e466-146">(включает инициализацию конвейера EventFlow hello из конфигурации службы Service Fabric и сообщает обо всех проблемах с Отправка диагностических данных в виде отчетов о работоспособности Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="6e466-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="6e466-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`пакет требует tootarget проекта hello службы .NET Framework 4.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6e466-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="6e466-148">Убедитесь, что значение hello соответствующие требуемой версии .NET framework в свойствах проекта перед установкой данного пакета.</span><span class="sxs-lookup"><span data-stu-id="6e466-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="6e466-149">После того как все hello пакеты установлены, hello следующим шагом является tooconfigure и включите EventFlow hello службы.</span><span class="sxs-lookup"><span data-stu-id="6e466-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="6e466-150">Настройка и включение сбора журналов</span><span class="sxs-lookup"><span data-stu-id="6e466-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="6e466-151">EventFlow конвейера, отвечающего за отправку журналов hello создается на основе спецификации, хранящейся в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6e466-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="6e466-152">Пакет `Microsoft.Diagnostics.EventFlow.ServiceFabric` устанавливает начальный файл конфигурации EventFlow в паку решения `PackageRoot\Config`.</span><span class="sxs-lookup"><span data-stu-id="6e466-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="6e466-153">Имя файла Hello `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="6e466-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="6e466-154">Этот файл конфигурации требует изменения toobe toocapture данные от служб по умолчанию hello `EventSource` класса и отправить службе аналитики tooApplication данных.</span><span class="sxs-lookup"><span data-stu-id="6e466-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="6e466-155">Мы предполагаем, что вы знакомы с **Azure Application Insights** службы, а также наличие ресурс Application Insights, планирование toouse toomonitor службе Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e466-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="6e466-156">Если вам требуются дополнительные сведения, ознакомьтесь с разделом [Создание ресурса Application Insights](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6e466-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="6e466-157">Привет открыть `eventFlowConfig.json` в редактор hello и измените его содержимое, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6e466-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="6e466-158">Убедитесь, что tooreplace hello ServiceEventSource имя и ключ инструментирования Application Insights в соответствии с toocomments.</span><span class="sxs-lookup"><span data-stu-id="6e466-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> <span data-ttu-id="6e466-159">Hello ServiceEventSource службы называется hello значение свойства Name hello hello `EventSourceAttribute` применения toohello ServiceEventSource класса.</span><span class="sxs-lookup"><span data-stu-id="6e466-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="6e466-160">Он будет указан в hello `ServiceEventSource.cs` файл, который является частью службы кода hello.</span><span class="sxs-lookup"><span data-stu-id="6e466-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="6e466-161">Например, в hello следующий код фрагмент кода hello hello ServiceEventSource имеет имя *MyCompany Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="6e466-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="6e466-162">Обратите внимание, что файл `eventFlowConfig.json` входит в пакет конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="6e466-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="6e466-163">Файл toothis изменения могут быть включены в full или конфигурации — только для обновления службы hello, тема tooService обновление проверки работоспособности и автоматического отката при наличии сбоя обновления.</span><span class="sxs-lookup"><span data-stu-id="6e466-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="6e466-164">Дополнительные сведения см. в разделе [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="6e466-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="6e466-165">Последний шаг Hello — tooinstantiate EventFlow конвейера в код запуска службы, расположенных в `Program.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="6e466-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="6e466-166">В hello помечены следующие дополнения связанных EventFlow пример с комментариями, начиная с `****`:</span><span class="sxs-lookup"><span data-stu-id="6e466-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    
                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

<span data-ttu-id="6e466-167">Имя Hello передается как параметр hello hello `CreatePipeline` метод hello `ServiceFabricDiagnosticsPipelineFactory` — имя hello hello *сущности работоспособности* представляющий hello EventFlow журнала коллекции конвейера.</span><span class="sxs-lookup"><span data-stu-id="6e466-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="6e466-168">Это имя используется в том случае, если обнаруживает EventFlow и ошибок и сообщает об этом через hello подсистемы работоспособности Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e466-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="6e466-169">Проверка</span><span class="sxs-lookup"><span data-stu-id="6e466-169">Verification</span></span>
<span data-ttu-id="6e466-170">Запустите службу и понаблюдайте за hello отладки окна вывода в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e466-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="6e466-171">После запуска службы hello должна появиться свидетельство, что служба отправляет записи «Телеметрию Application Insights».</span><span class="sxs-lookup"><span data-stu-id="6e466-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="6e466-172">Откройте веб-браузер и перейдите последовательно выберите tooyour ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6e466-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="6e466-173">Откройте вкладку «Поиск» (вверху hello колонка «Обзор» по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="6e466-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="6e466-174">После небольшой задержки должна появиться данные трассировок на портале Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="6e466-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![Журналы из Service Fabric на портале Application Insights][2]

## <a name="next-steps"></a><span data-ttu-id="6e466-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e466-176">Next steps</span></span>
* [<span data-ttu-id="6e466-177">Дополнительные сведения о диагностике и мониторинге службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e466-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="6e466-178">Документация по EventFlow</span><span class="sxs-lookup"><span data-stu-id="6e466-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
