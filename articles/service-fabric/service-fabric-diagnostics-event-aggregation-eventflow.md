---
title: "Агрегирование событий Azure Service Fabric c помощью EventFlow | Документы Майкрософт"
description: "Ознакомьтесь со сведениями об агрегировании и сборе событий с использованием EventFlow для мониторинга и диагностики кластеров Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 90d26a77b749e70de3a7d910f15820653e2ef39b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="0155d-103">Агрегирование и сбор событий с помощью EventFlow</span><span class="sxs-lookup"><span data-stu-id="0155d-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="0155d-104">[EventFlow службы диагностики Microsoft](https://github.com/Azure/diagnostics-eventflow) позволяет направлять события от узла к одному или нескольким целевым объектам для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0155d-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node to one or more monitoring destinations.</span></span> <span data-ttu-id="0155d-105">Так как это решение включается в проект службы как пакет NuGet, код и конфигурация EventFlow перемещаются вместе со службой, устраняя необходимость отдельной настройки каждого узла для системы диагностики Azure, которую мы обсуждали выше.</span><span class="sxs-lookup"><span data-stu-id="0155d-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with the service, eliminating the per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="0155d-106">EventFlow выполняется внутри процесса службы и напрямую подключается к настроенным потокам вывода.</span><span class="sxs-lookup"><span data-stu-id="0155d-106">EventFlow runs within your service process, and connects directly to the configured outputs.</span></span> <span data-ttu-id="0155d-107">Прямое подключение позволяет использовать EventFlow для служб, развернутых в Azure, с помощью контейнера или в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="0155d-107">Because of the direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="0155d-108">Соблюдайте осторожность при выполнении EventFlow в сценариях с высокой плотностью, например в контейнере, так как каждый конвейер EventFlow создает внешнее соединение.</span><span class="sxs-lookup"><span data-stu-id="0155d-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="0155d-109">Если вы разместите несколько процессов, то получите несколько исходящих подключений.</span><span class="sxs-lookup"><span data-stu-id="0155d-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="0155d-110">Об этом можно не беспокоиться при использовании приложений Service Fabric, так как все реплики `ServiceType` выполняются в одном процессе, что ограничивает число исходящих подключений.</span><span class="sxs-lookup"><span data-stu-id="0155d-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in the same process, and this limits the number of outbound connections.</span></span> <span data-ttu-id="0155d-111">EventFlow также поддерживает фильтрацию событий, то есть позволяет отправлять только события, соответствующие указанному фильтру.</span><span class="sxs-lookup"><span data-stu-id="0155d-111">EventFlow also offers event filtering, so that only the events that match the specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="0155d-112">Настройка EventFlow</span><span class="sxs-lookup"><span data-stu-id="0155d-112">Setting up EventFlow</span></span>

<span data-ttu-id="0155d-113">Двоичные файлы EventFlow предоставляются как набор пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="0155d-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="0155d-114">Чтобы добавить библиотеку EventFlow в проект службы Service Fabric, щелкните его правой кнопкой мыши в обозревателе решений и выберите "Управление пакетами NuGet".</span><span class="sxs-lookup"><span data-stu-id="0155d-114">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="0155d-115">Перейдите на вкладку "Обзор" и найдите `Diagnostics.EventFlow`.</span><span class="sxs-lookup"><span data-stu-id="0155d-115">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Пакеты NuGet EventFlow в диспетчере пакетов NuGet Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="0155d-117">Появится список различных пакетов, которые помечены как "Входные данные" и "Выходные данные".</span><span class="sxs-lookup"><span data-stu-id="0155d-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="0155d-118">EventFlow поддерживает различные регистраторы и анализаторы журналов.</span><span class="sxs-lookup"><span data-stu-id="0155d-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="0155d-119">Служба, в которой размещается EventFlow, должна содержать соответствующие пакеты в зависимости от источника и назначения журналов приложений.</span><span class="sxs-lookup"><span data-stu-id="0155d-119">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="0155d-120">Помимо основного пакета ServiceFabric, также требуется настроить по крайней мере один ввод и один вывод.</span><span class="sxs-lookup"><span data-stu-id="0155d-120">In addition to the core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="0155d-121">Например, можно добавить следующие пакеты для отправки событий EventSource в Application Insights:</span><span class="sxs-lookup"><span data-stu-id="0155d-121">For exmaple, you can add the following packages to sent EventSource events to Application Insights:</span></span>

* <span data-ttu-id="0155d-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` для сбора данных из класса EventSource службы и стандартных классов EventSource, например *Microsoft-ServiceFabric-Services* и *Microsoft-ServiceFabric-Actors*</span><span class="sxs-lookup"><span data-stu-id="0155d-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="0155d-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (мы собираемся отправлять журналы в ресурс Azure Application Insights)</span><span class="sxs-lookup"><span data-stu-id="0155d-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going to send the logs to an Azure Application Insights resource)</span></span>
* <span data-ttu-id="0155d-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric` (позволяет инициализировать конвейер EventFlow из конфигурации службы Service Fabric и сообщать о всех проблемах отправки диагностических данных в виде отчетов о работоспособности Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="0155d-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="0155d-125">Для пакета `Microsoft.Diagnostics.EventFlow.Input.EventSource` требуется, чтобы в проекте службы использовалась платформа .NET Framework 4.6 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="0155d-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="0155d-126">Обязательно задайте соответствующую целевую платформу в свойствах проекта, прежде чем устанавливать этот пакет.</span><span class="sxs-lookup"><span data-stu-id="0155d-126">Make sure you set the appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="0155d-127">После установки всех пакетов следующим шагом является настройка и включение EventFlow в службе.</span><span class="sxs-lookup"><span data-stu-id="0155d-127">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="0155d-128">Настройка и включение сбора журналов</span><span class="sxs-lookup"><span data-stu-id="0155d-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="0155d-129">Конвейер EventFlow, отвечающий за отправку журналов, создается на основе спецификации, хранящейся в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0155d-129">The EventFlow pipeline responsible for sending the logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="0155d-130">Пакет `Microsoft.Diagnostics.EventFlow.ServiceFabric` устанавливает начальный файл конфигурации EventFlow в паку решения `PackageRoot\Config` с именем `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="0155d-130">The `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="0155d-131">Этот файл конфигурации нужно изменить, чтобы собирать данные из класса `EventSource` службы по умолчанию, а также другие входные данные, которые вы хотите настроить, и отправлять их в соответствующее место.</span><span class="sxs-lookup"><span data-stu-id="0155d-131">This configuration file needs to be modified to capture data from the default service `EventSource` class, and any other inputs you want to configure, and send data to the appropriate place.</span></span>

<span data-ttu-id="0155d-132">Вот пример файла *eventFlowConfig.json* на основе упомянутых выше пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="0155d-132">Here is a sample *eventFlowConfig.json* based on the NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="0155d-133">Имя ServiceEventSource службы — это значение свойства Name в `EventSourceAttribute`, которое применяется к классу ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="0155d-133">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="0155d-134">Все это указывается в файле `ServiceEventSource.cs`, который является частью кода службы.</span><span class="sxs-lookup"><span data-stu-id="0155d-134">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="0155d-135">Например, в приведенном ниже фрагменте кода именем ServiceEventSource является *MyCompany Application1-Stateless1*.</span><span class="sxs-lookup"><span data-stu-id="0155d-135">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="0155d-136">Обратите внимание, что файл `eventFlowConfig.json` входит в пакет конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="0155d-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="0155d-137">Изменения в этот файл могут вноситься только полными обновлениями или обновлениями конфигурации службы, которые проходят проверку работоспособности обновлений Service Fabric и автоматически откатываются в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="0155d-137">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="0155d-138">Дополнительные сведения см. в разделе [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="0155d-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="0155d-139">Раздел *filters* конфигурации позволяет произвести дополнительную настройку данных, которые будут передаваться по конвейеру EventFlow на вывод, включив или исключив определенную информацию либо изменив структуру данных событий.</span><span class="sxs-lookup"><span data-stu-id="0155d-139">The *filters* section of the config allows you to further customize the information that is going to go through the EventFlow pipeline to the outputs, allowing you to drop or include certain information, or change the structure of the event data.</span></span> <span data-ttu-id="0155d-140">Дополнительные сведения о фильтрации см. в разделе [Фильтры EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="0155d-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="0155d-141">Завершающим шагом является создание экземпляра конвейера EventFlow в коде запуска службы, расположенном в файле `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="0155d-141">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="0155d-142">Имя, переданное в качестве параметра в метод `CreatePipeline` класса `ServiceFabricDiagnosticsPipelineFactory`, — это имя *сущности работоспособности*, представляющей конвейер EventFlow для сбора журналов.</span><span class="sxs-lookup"><span data-stu-id="0155d-142">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="0155d-143">Это имя используется в том случае, если EventFlow обнаруживает ошибку и сообщает о ней через подсистему работоспособности Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0155d-143">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-to-in-eventflowconfig"></a><span data-ttu-id="0155d-144">Использование параметров Service Fabric и параметров приложений в eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="0155d-144">Using Service Fabric settings and application parameters to in eventFlowConfig</span></span>

<span data-ttu-id="0155d-145">EventFlow поддерживает использование параметров Service Fabric и параметров приложений для настройки параметров EventFlow.</span><span class="sxs-lookup"><span data-stu-id="0155d-145">EventFlow supports using Service Fabric settings and application paremeters to configure EventFlow settings.</span></span> <span data-ttu-id="0155d-146">На параметры Service Fabric можно ссылаться с помощью специального синтаксиса для значений:</span><span class="sxs-lookup"><span data-stu-id="0155d-146">You can refer to Service Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="0155d-147">`<section-name>` — это имя раздела конфигурации Service Fabric, а `<setting-name>` — это параметр конфигурации, предоставляющий значение, которое будет использоваться для настройки параметра EventFlow.</span><span class="sxs-lookup"><span data-stu-id="0155d-147">`<section-name>` is the name of the Service Fabric configuration section, and `<setting-name>` is the configuration setting providing the value that will be used to configure an EventFlow setting.</span></span> <span data-ttu-id="0155d-148">Дополнительные сведения см. в статье [Поддержка параметров Service Fabric и параметров приложений](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="0155d-148">To read more about how to do this, go to [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="0155d-149">Проверка</span><span class="sxs-lookup"><span data-stu-id="0155d-149">Verification</span></span>

<span data-ttu-id="0155d-150">Запустите службу и просмотрите окно выходных данных отладки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0155d-150">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="0155d-151">После запуска службы вы должны увидеть подтверждение того, что она отправляет записи в настроенное расположение вывода.</span><span class="sxs-lookup"><span data-stu-id="0155d-151">After the service is started, you should start seeing evidence that your service is sending records to the output that you have configured.</span></span> <span data-ttu-id="0155d-152">Перейдите в платформу анализа и визуализации событий и убедитесь в том, что журналы начали отображаться (это может занять несколько минут).</span><span class="sxs-lookup"><span data-stu-id="0155d-152">Navigate to your event analysis and visualization platform and confirm that logs have started to show up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0155d-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0155d-153">Next steps</span></span>

* [<span data-ttu-id="0155d-154">Анализ событий и визуализация с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="0155d-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="0155d-155">Анализ событий и визуализация с помощью OMS</span><span class="sxs-lookup"><span data-stu-id="0155d-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="0155d-156">Документация по EventFlow</span><span class="sxs-lookup"><span data-stu-id="0155d-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)