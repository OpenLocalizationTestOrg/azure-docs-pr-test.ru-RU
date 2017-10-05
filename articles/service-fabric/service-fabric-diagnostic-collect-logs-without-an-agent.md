---
title: "Сбор журналов непосредственно из процесса службы Azure Service Fabric | Microsoft Azure"
description: "Описывает, как приложения Service Fabric могут отправлять журналы непосредственно в центральное расположение, например Azure Application Insights или Elasticsearch, не полагаясь на агент системы диагностики Azure."
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
ms.openlocfilehash: b7d2541928f4248750417a77d99033c8b4354dcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="8a045-103">Сбор журналов непосредственно из процесса службы Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8a045-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="8a045-104">Внутрипроцессный сбор журналов</span><span class="sxs-lookup"><span data-stu-id="8a045-104">In-process log collection</span></span>
<span data-ttu-id="8a045-105">Сбор журналов приложений с помощью [расширения системы диагностики Azure](service-fabric-diagnostics-how-to-setup-wad.md) — хороший вариант для служб **Azure Service Fabric**, если набор источников и мест назначения журналов невелик и редко меняется, а источники и места назначения легко сопоставимы.</span><span class="sxs-lookup"><span data-stu-id="8a045-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if the set of log sources and destinations is small, does not change often, and there is a straightforward mapping between the sources and their destinations.</span></span> <span data-ttu-id="8a045-106">В противном случае можно настроить службы для отправки своих журналов в центральное расположение.</span><span class="sxs-lookup"><span data-stu-id="8a045-106">If not, an alternative is to have services send their logs directly to a central location.</span></span> <span data-ttu-id="8a045-107">Этот процесс называется **внутрипроцессным сбором журналов** и имеет несколько потенциальных преимуществ.</span><span class="sxs-lookup"><span data-stu-id="8a045-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="8a045-108">*Простая настройка и развертывание.*</span><span class="sxs-lookup"><span data-stu-id="8a045-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="8a045-109">Конфигурация сбора диагностических данных является лишь частью конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="8a045-109">The configuration of diagnostic data collection is just part of the service configuration.</span></span> <span data-ttu-id="8a045-110">Ее легко сохранять "синхронизированной" с остальной частью приложения.</span><span class="sxs-lookup"><span data-stu-id="8a045-110">It is easy to always keep it "in sync" with the rest of the application.</span></span>
    * <span data-ttu-id="8a045-111">Настройка каждого приложения или службы также является несложной задачей.</span><span class="sxs-lookup"><span data-stu-id="8a045-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="8a045-112">Сбор журналов на основе агента обычно требует отдельного развертывания и настройки агента диагностики. Как правило, это прибавляет работы администратору и может являться источником ошибок.</span><span class="sxs-lookup"><span data-stu-id="8a045-112">Agent-based log collection usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="8a045-113">Часто на виртуальной машине (узле) существует только один экземпляр агента, и конфигурация агента совместно используется всеми приложениями и службами, запущенными на этом узле.</span><span class="sxs-lookup"><span data-stu-id="8a045-113">Often there is only one instance of the agent allowed per virtual machine (node) and the agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="8a045-114">*Гибкость*</span><span class="sxs-lookup"><span data-stu-id="8a045-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="8a045-115">Приложение может отправлять данные куда угодно при наличии клиентской библиотеки, поддерживающей систему хранения целевых данных.</span><span class="sxs-lookup"><span data-stu-id="8a045-115">The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system.</span></span> <span data-ttu-id="8a045-116">При необходимости можно добавлять новые расположения.</span><span class="sxs-lookup"><span data-stu-id="8a045-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="8a045-117">Можно реализовать сложные правила сбора, фильтрации и статистической обработки данных.</span><span class="sxs-lookup"><span data-stu-id="8a045-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="8a045-118">Сбор журналов на основе агента часто ограничивается приемниками данных, которые поддерживает агент.</span><span class="sxs-lookup"><span data-stu-id="8a045-118">Agent-based log collection is often limited by the data sinks that the agent supports.</span></span> <span data-ttu-id="8a045-119">Некоторые агенты являются расширяемыми.</span><span class="sxs-lookup"><span data-stu-id="8a045-119">Some agents are extensible.</span></span>

* <span data-ttu-id="8a045-120">*Доступ к внутренним данным приложения и контексту*</span><span class="sxs-lookup"><span data-stu-id="8a045-120">*Access to internal application data and context*</span></span>
   
    * <span data-ttu-id="8a045-121">В подсистему диагностики, которая работает внутри процесса приложения или службы, можно легко добавить трассировку с помощью контекстной информации.</span><span class="sxs-lookup"><span data-stu-id="8a045-121">The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.</span></span>
    * <span data-ttu-id="8a045-122">В случае сбора журналов на основе агента данные должны отправляться в агент с помощью механизма межпроцессного взаимодействия, например трассировки событий Windows.</span><span class="sxs-lookup"><span data-stu-id="8a045-122">With agent-based log collection, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="8a045-123">Однако при таком механизме могут возникнуть дополнительные ограничения.</span><span class="sxs-lookup"><span data-stu-id="8a045-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="8a045-124">Преимущества обоих методов сбора можно объединить.</span><span class="sxs-lookup"><span data-stu-id="8a045-124">It is possible to combine and benefit from both collection methods.</span></span> <span data-ttu-id="8a045-125">Это действительно может оказаться наилучшим решением для многих приложений.</span><span class="sxs-lookup"><span data-stu-id="8a045-125">Indeed, it might be the best solution for many applications.</span></span> <span data-ttu-id="8a045-126">Сбор на основе агента — логичное решение для сбора журналов, связанных со всем кластером и отдельными его узлами.</span><span class="sxs-lookup"><span data-stu-id="8a045-126">Agent-based collection is a natural solution for collecting logs related to the whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="8a045-127">Он гораздо надежнее, чем внутрипроцессный сбор журналов, и лучше подходит для диагностики проблем и сбоев при запуске службы.</span><span class="sxs-lookup"><span data-stu-id="8a045-127">It is much more reliable way, than in-process log collection, to diagnose service startup problems and crashes.</span></span> <span data-ttu-id="8a045-128">Кроме того, если в кластере Service Fabric запущено много служб, каждая из них выполняет собственный внутрипроцессный сбор журналов, что приведет к многочисленным исходящим подключениям из кластера.</span><span class="sxs-lookup"><span data-stu-id="8a045-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from the cluster.</span></span> <span data-ttu-id="8a045-129">Большое количество исходящих подключений нагружает как подсистему сети, так и место назначения журналов, что увеличивает затраты.</span><span class="sxs-lookup"><span data-stu-id="8a045-129">Large number of outgoing connections is taxing both for the network subsystem and for the log destination.</span></span> <span data-ttu-id="8a045-130">Агент (например, агент [**системы диагностики Azure**](../cloud-services/cloud-services-dotnet-diagnostics.md)) может собирать данные от нескольких служб и отправлять все данные через небольшое число подключений, повышая производительность.</span><span class="sxs-lookup"><span data-stu-id="8a045-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="8a045-131">В этой статье показано, как настроить внутрипроцессный сбор журналов с помощью [**библиотеки с открытым кодом EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="8a045-131">In this article, we show how to set up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="8a045-132">Для этой цели можно использовать и другие библиотеки, но EventFlow имеет преимущество, так как она была разработана специально для внутрипроцессного сбора журналов и поддержки служб Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8a045-132">Other libraries might be used for the same purpose, but EventFlow has the benefit of having been designed specifically for in-process log collection and to support Service Fabric services.</span></span> <span data-ttu-id="8a045-133">Мы используем [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) в качестве места назначения журналов.</span><span class="sxs-lookup"><span data-stu-id="8a045-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as the log destination.</span></span> <span data-ttu-id="8a045-134">Можно также использовать [**концентраторы событий**](https://azure.microsoft.com/services/event-hubs/) или [**Elasticsearch**](https://www.elastic.co/products/elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="8a045-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="8a045-135">Это лишь вопрос установки соответствующего пакета NuGet и настройки назначения в файле конфигурации EventFlow.</span><span class="sxs-lookup"><span data-stu-id="8a045-135">It is just a question of installing appropriate NuGet package and configuring the destination in the EventFlow configuration file.</span></span> <span data-ttu-id="8a045-136">Дополнительные сведения о местах назначения журналов, отличных от Application Insights, см. в [документации по EventFlow](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="8a045-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-to-a-service-fabric-service-project"></a><span data-ttu-id="8a045-137">Добавление библиотеки EventFlow в проект службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8a045-137">Adding EventFlow library to a Service Fabric service project</span></span>
<span data-ttu-id="8a045-138">Двоичные файлы EventFlow предоставляются как набор пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="8a045-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="8a045-139">Чтобы добавить библиотеку EventFlow в проект службы Service Fabric, щелкните его правой кнопкой мыши в обозревателе решений и выберите "Управление пакетами NuGet".</span><span class="sxs-lookup"><span data-stu-id="8a045-139">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="8a045-140">Перейдите на вкладку "Обзор" и найдите `Diagnostics.EventFlow`.</span><span class="sxs-lookup"><span data-stu-id="8a045-140">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Пакеты NuGet EventFlow в диспетчере пакетов NuGet Visual Studio][1]

<span data-ttu-id="8a045-142">Служба, в которой размещается EventFlow, должна содержать соответствующие пакеты в зависимости от источника и назначения журналов приложений.</span><span class="sxs-lookup"><span data-stu-id="8a045-142">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="8a045-143">Добавьте приведенные ниже пакеты.</span><span class="sxs-lookup"><span data-stu-id="8a045-143">Add the following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="8a045-144">(Для сбора данных из класса EventSource службы и стандартных классов EventSource, например *Microsoft-ServiceFabric-Services* и *Microsoft-ServiceFabric-Actors*.)</span><span class="sxs-lookup"><span data-stu-id="8a045-144">(to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="8a045-145">(Мы собираемся отправлять журналы в ресурс Azure Application Insights.)</span><span class="sxs-lookup"><span data-stu-id="8a045-145">(we are going to send the logs to an Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="8a045-146">(Позволяет инициализировать конвейер EventFlow из конфигурации службы Service Fabric и сообщать о всех проблемах отправки диагностических данных в виде отчетов о работоспособности Service Fabric.)</span><span class="sxs-lookup"><span data-stu-id="8a045-146">(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="8a045-147">Для пакета `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` требуется, чтобы в проекте службы использовалась платформа .NET Framework 4.6 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="8a045-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="8a045-148">Обязательно задайте соответствующую целевую платформу в свойствах проекта, прежде чем устанавливать этот пакет.</span><span class="sxs-lookup"><span data-stu-id="8a045-148">Make sure you set the appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="8a045-149">После установки всех пакетов следующим шагом является настройка и включение EventFlow в службе.</span><span class="sxs-lookup"><span data-stu-id="8a045-149">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="8a045-150">Настройка и включение сбора журналов</span><span class="sxs-lookup"><span data-stu-id="8a045-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="8a045-151">Конвейер EventFlow, отвечающий за отправку журналов, создается на основе спецификации, хранящейся в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8a045-151">EventFlow pipeline, responsible for sending the logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="8a045-152">Пакет `Microsoft.Diagnostics.EventFlow.ServiceFabric` устанавливает начальный файл конфигурации EventFlow в паку решения `PackageRoot\Config`.</span><span class="sxs-lookup"><span data-stu-id="8a045-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="8a045-153">Это файл `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="8a045-153">The file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="8a045-154">Данный файл конфигурации нужно изменить, чтобы собирать данные из класса службы по умолчанию `EventSource` и отправлять их в службу Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8a045-154">This configuration file needs to be modified to capture data from the default service `EventSource` class and send data to Application Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="8a045-155">Мы предполагаем, что вы уже работали со службой **Azure Application Insights** и у вас есть ресурс Application Insights, который планируется использовать для мониторинга службы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8a045-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan to use to monitor your Service Fabric service.</span></span> <span data-ttu-id="8a045-156">Если вам требуются дополнительные сведения, ознакомьтесь с разделом [Создание ресурса Application Insights](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="8a045-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="8a045-157">Откройте файл `eventFlowConfig.json` в редакторе и измените его содержимое, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8a045-157">Open the `eventFlowConfig.json` file in the editor and change its content as shown below.</span></span> <span data-ttu-id="8a045-158">Обязательно замените имя ServiceEventSource и ключ инструментирования Application Insights в соответствии с комментариями.</span><span class="sxs-lookup"><span data-stu-id="8a045-158">Make sure to replace the ServiceEventSource name and Application Insights instrumentation key according to comments.</span></span> 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
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
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> <span data-ttu-id="8a045-159">Имя ServiceEventSource службы — это значение свойства Name в `EventSourceAttribute`, которое применяется к классу ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="8a045-159">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="8a045-160">Все это указывается в файле `ServiceEventSource.cs`, который является частью кода службы.</span><span class="sxs-lookup"><span data-stu-id="8a045-160">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="8a045-161">Например, в приведенном ниже фрагменте кода именем ServiceEventSource является *MyCompany Application1-Stateless1*.</span><span class="sxs-lookup"><span data-stu-id="8a045-161">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="8a045-162">Обратите внимание, что файл `eventFlowConfig.json` входит в пакет конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="8a045-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="8a045-163">Изменения в этот файл могут вноситься только полными обновлениями или обновлениями конфигурации службы, которые проходят проверку работоспособности обновлений Service Fabric и автоматически откатываются в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="8a045-163">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="8a045-164">Дополнительные сведения см. в разделе [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="8a045-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="8a045-165">Завершающим шагом является создание экземпляра конвейера EventFlow в коде запуска службы, расположенном в файле `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="8a045-165">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="8a045-166">В следующем примере изменения, связанные с EventFlow, помечены комментариями, которые начинаются с `****`.</span><span class="sxs-lookup"><span data-stu-id="8a045-166">In the following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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
        /// This is the entry point of the service host process.
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

<span data-ttu-id="8a045-167">Имя, переданное в качестве параметра в метод `CreatePipeline` класса `ServiceFabricDiagnosticsPipelineFactory`, — это имя *сущности работоспособности*, представляющей конвейер EventFlow для сбора журналов.</span><span class="sxs-lookup"><span data-stu-id="8a045-167">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="8a045-168">Это имя используется в том случае, если EventFlow обнаруживает ошибку и сообщает о ней через подсистему работоспособности Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8a045-168">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="8a045-169">Проверка</span><span class="sxs-lookup"><span data-stu-id="8a045-169">Verification</span></span>
<span data-ttu-id="8a045-170">Запустите службу и просмотрите окно выходных данных отладки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a045-170">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="8a045-171">После запуска службы вы должны увидеть подтверждения того, что она отправляет записи телеметрии Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8a045-171">After the service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="8a045-172">Откройте веб-браузер и перейдите к своему ресурсу Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8a045-172">Open a web browser and navigate go to your Application Insights resource.</span></span> <span data-ttu-id="8a045-173">Откройте вкладку "Поиск" (в верхней части колонки "Обзор", используемой по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="8a045-173">Open "Search" tab (at the top of the default "Overview" blade).</span></span> <span data-ttu-id="8a045-174">После небольшой задержки ваши трассировки должны начать появляться на портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8a045-174">After a short delay you should start seeing your traces in the Application Insights portal:</span></span>

![Журналы из Service Fabric на портале Application Insights][2]

## <a name="next-steps"></a><span data-ttu-id="8a045-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a045-176">Next steps</span></span>
* [<span data-ttu-id="8a045-177">Дополнительные сведения о диагностике и мониторинге службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8a045-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="8a045-178">Документация по EventFlow</span><span class="sxs-lookup"><span data-stu-id="8a045-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
