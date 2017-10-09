---
title: "Статистическая обработка событий Service Fabric с EventFlow aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="23ee1-103">Агрегирование и сбор событий с помощью EventFlow</span><span class="sxs-lookup"><span data-stu-id="23ee1-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="23ee1-104">[EventFlow диагностики Microsoft](https://github.com/Azure/diagnostics-eventflow) может направлять события tooone узел или несколько назначений мониторинга.</span><span class="sxs-lookup"><span data-stu-id="23ee1-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="23ee1-105">Так как он включен в виде пакета NuGet в проекте службы, EventFlow код и конфигурация перемещаются вместе hello службы, что исключает проблемы с конфигурацией отдельным узлам hello сказано о службе диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="23ee1-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="23ee1-106">EventFlow выполняется внутри одного процесса службы и выходы настроены toohello подключается напрямую.</span><span class="sxs-lookup"><span data-stu-id="23ee1-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="23ee1-107">Из-за прямого подключения hello EventFlow работает в Azure, контейнер и развертывания службы в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="23ee1-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="23ee1-108">Соблюдайте осторожность при выполнении EventFlow в сценариях с высокой плотностью, например в контейнере, так как каждый конвейер EventFlow создает внешнее соединение.</span><span class="sxs-lookup"><span data-stu-id="23ee1-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="23ee1-109">Если вы разместите несколько процессов, то получите несколько исходящих подключений.</span><span class="sxs-lookup"><span data-stu-id="23ee1-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="23ee1-110">Это не столько значения для приложения Service Fabric, так как все реплики `ServiceType` запуска в hello же процесс, а это ограничивает hello число исходящих подключений.</span><span class="sxs-lookup"><span data-stu-id="23ee1-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="23ee1-111">EventFlow также предлагает фильтрацию событий, так что отправляются только события hello, которые соответствуют заданному фильтру hello.</span><span class="sxs-lookup"><span data-stu-id="23ee1-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="23ee1-112">Настройка EventFlow</span><span class="sxs-lookup"><span data-stu-id="23ee1-112">Setting up EventFlow</span></span>

<span data-ttu-id="23ee1-113">Двоичные файлы EventFlow предоставляются как набор пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="23ee1-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="23ee1-114">tooadd EventFlow проект службы tooa Service Fabric, щелкните правой кнопкой мыши проект hello в hello обозреватель решений и выберите «Управление NuGet пакетов».</span><span class="sxs-lookup"><span data-stu-id="23ee1-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="23ee1-115">Перейдите на вкладку toohello «Просмотр» и выполните поиск «`Diagnostics.EventFlow`»:</span><span class="sxs-lookup"><span data-stu-id="23ee1-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Пакеты NuGet EventFlow в диспетчере пакетов NuGet Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="23ee1-117">Появится список различных пакетов, которые помечены как "Входные данные" и "Выходные данные".</span><span class="sxs-lookup"><span data-stu-id="23ee1-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="23ee1-118">EventFlow поддерживает различные регистраторы и анализаторы журналов.</span><span class="sxs-lookup"><span data-stu-id="23ee1-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="23ee1-119">EventFlow, где размещается служба Hello должна включать соответствующие пакеты, в зависимости от hello источника и назначения для журналов приложения hello.</span><span class="sxs-lookup"><span data-stu-id="23ee1-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="23ee1-120">В дополнение к этому toohello ServiceFabric базовый пакет, также потребуется по крайней мере один вход и выход, которые настроены.</span><span class="sxs-lookup"><span data-stu-id="23ee1-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="23ee1-121">В примере можно добавить следующие пакеты toosent EventSource события tooApplication аналитики hello:</span><span class="sxs-lookup"><span data-stu-id="23ee1-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="23ee1-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture данных из класса EventSource hello службы и из стандартной EventSources, такие как *Майкрософт ServiceFabric* и *Microsoft ServiceFabric субъекты*)</span><span class="sxs-lookup"><span data-stu-id="23ee1-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="23ee1-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(мы будем toosend hello журналы tooan Azure Application Insights ресурсов)</span><span class="sxs-lookup"><span data-stu-id="23ee1-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="23ee1-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(включает инициализацию конвейера EventFlow hello из конфигурации службы Service Fabric и сообщает обо всех проблемах с Отправка диагностических данных в виде отчетов о работоспособности Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="23ee1-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="23ee1-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`пакет требует tootarget проекта hello службы .NET Framework 4.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="23ee1-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="23ee1-126">Убедитесь, что значение hello соответствующие требуемой версии .NET framework в свойствах проекта перед установкой данного пакета.</span><span class="sxs-lookup"><span data-stu-id="23ee1-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="23ee1-127">После того как все hello пакеты установлены, hello следующим шагом является tooconfigure и включите EventFlow hello службы.</span><span class="sxs-lookup"><span data-stu-id="23ee1-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="23ee1-128">Настройка и включение сбора журналов</span><span class="sxs-lookup"><span data-stu-id="23ee1-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="23ee1-129">конвейер EventFlow Hello, отвечающего за отправку журналов hello создается на основе спецификации, хранящейся в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="23ee1-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="23ee1-130">Hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` пакет устанавливает файл начальной конфигурации EventFlow под `PackageRoot\Config` папку решения, с именем `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="23ee1-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="23ee1-131">Этот файл конфигурации требует изменения toobe toocapture данные от служб по умолчанию hello `EventSource` класс и любые другие входные данные должны tooconfigure и отправки данных toohello соответствующее место.</span><span class="sxs-lookup"><span data-stu-id="23ee1-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="23ee1-132">Ниже приведен пример *eventFlowConfig.json* зависимости пакетов NuGet hello, упомянутых выше:</span><span class="sxs-lookup"><span data-stu-id="23ee1-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="23ee1-133">Hello ServiceEventSource службы называется hello значение свойства Name hello hello `EventSourceAttribute` применения toohello ServiceEventSource класса.</span><span class="sxs-lookup"><span data-stu-id="23ee1-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="23ee1-134">Он будет указан в hello `ServiceEventSource.cs` файл, который является частью службы кода hello.</span><span class="sxs-lookup"><span data-stu-id="23ee1-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="23ee1-135">Например, в hello следующий код фрагмент кода hello hello ServiceEventSource имеет имя *MyCompany Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="23ee1-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="23ee1-136">Обратите внимание, что файл `eventFlowConfig.json` входит в пакет конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="23ee1-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="23ee1-137">Файл toothis изменения могут быть включены в full или конфигурации — только для обновления службы hello, тема tooService обновление проверки работоспособности и автоматического отката при наличии сбоя обновления.</span><span class="sxs-lookup"><span data-stu-id="23ee1-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="23ee1-138">Дополнительные сведения см. в разделе [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="23ee1-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="23ee1-139">Hello *фильтры* раздел конфигурации hello позволяет toofurther собственные данные hello, toogo переход через hello EventFlow конвейера toohello выходов, позволяя toodrop включать определенные данные или изменить hello Структура данных о событиях hello.</span><span class="sxs-lookup"><span data-stu-id="23ee1-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="23ee1-140">Дополнительные сведения о фильтрации см. в разделе [Фильтры EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="23ee1-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="23ee1-141">Последний шаг Hello — tooinstantiate EventFlow конвейера в код запуска службы, расположенных в `Program.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="23ee1-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="23ee1-142">Имя Hello передается как параметр hello hello `CreatePipeline` метод hello `ServiceFabricDiagnosticsPipelineFactory` — имя hello hello *сущности работоспособности* представляющий hello EventFlow журнала коллекции конвейера.</span><span class="sxs-lookup"><span data-stu-id="23ee1-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="23ee1-143">Это имя используется в том случае, если обнаруживает EventFlow и ошибок и сообщает об этом через hello подсистемы работоспособности Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="23ee1-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="23ee1-144">С помощью настройки структуры службы и eventFlowConfig tooin параметров приложения</span><span class="sxs-lookup"><span data-stu-id="23ee1-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="23ee1-145">EventFlow поддерживает, с помощью Service Fabric и неверные параметры tooconfigure EventFlow параметры приложений.</span><span class="sxs-lookup"><span data-stu-id="23ee1-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="23ee1-146">Можно ссылаться с помощью этого синтаксиса для значений структуры параметров tooService:</span><span class="sxs-lookup"><span data-stu-id="23ee1-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="23ee1-147">`<section-name>`— Имя hello hello Service Fabric раздел конфигурации, и `<setting-name>` Установка конфигурации hello, предоставляя hello значение, которое будет использоваться tooconfigure EventFlow параметр.</span><span class="sxs-lookup"><span data-stu-id="23ee1-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="23ee1-148">Дополнительные сведения о том, как tooread toodo, перейдите слишком[поддержку настройки структуры службы и параметры приложения](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="23ee1-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="23ee1-149">Проверка</span><span class="sxs-lookup"><span data-stu-id="23ee1-149">Verification</span></span>

<span data-ttu-id="23ee1-150">Запустите службу и понаблюдайте за hello отладки окна вывода в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23ee1-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="23ee1-151">После запуска службы hello должна появиться свидетельство, которое отправляет службе записи toohello выходных данных, который вы настроили.</span><span class="sxs-lookup"><span data-stu-id="23ee1-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="23ee1-152">Перейдите событие tooyour анализа и визуализации платформы и убедитесь, что журналы запустили tooshow вверх (может потребоваться несколько минут).</span><span class="sxs-lookup"><span data-stu-id="23ee1-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="23ee1-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="23ee1-153">Next steps</span></span>

* [<span data-ttu-id="23ee1-154">Анализ событий и визуализация с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="23ee1-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="23ee1-155">Анализ событий и визуализация с помощью OMS</span><span class="sxs-lookup"><span data-stu-id="23ee1-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="23ee1-156">Документация по EventFlow</span><span class="sxs-lookup"><span data-stu-id="23ee1-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)