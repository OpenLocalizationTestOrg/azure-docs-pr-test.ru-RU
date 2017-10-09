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
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a>Сбор журналов непосредственно из процесса службы Azure Service Fabric
## <a name="in-process-log-collection"></a>Внутрипроцессный сбор журналов
Сбор приложения журналов с помощью [расширения системы диагностики Azure](service-fabric-diagnostics-how-to-setup-wad.md) — это хороший вариант для **Azure Service Fabric** служб при небольших, набор hello журнала источники и назначения не изменяет часто и существует представляет собой простой сопоставление hello источников и их назначения. Если нет, то альтернативой является toohave служб и отправлять свои журналы непосредственно tooa центрального расположения. Этот процесс называется **внутрипроцессным сбором журналов** и имеет несколько потенциальных преимуществ.

* *Простая настройка и развертывание.*

    * Конфигурация Hello сбора диагностических данных — просто частью конфигурации службы hello. Это легко tooalways оставить его «синхронизировано» с hello остальной части приложения hello.
    * Настройка каждого приложения или службы также является несложной задачей.
        * Сбор данных журнала на основе агентов обычно требуется отдельное развертывание и конфигурация диагностики агента hello, лишние административную задачу и потенциальный источник ошибок. Часто имеется только один экземпляр агента hello допускается на каждую виртуальную машину (узел) и конфигурация агента hello является общим для всех приложений и служб, работающих на этом узле. 

* *Гибкость*
   
    * Hello приложение может отправлять данные hello везде, где он должен toogo, при условии, что имеется клиентская библиотека, которая поддерживает hello целевые системы хранения данных. При необходимости можно добавлять новые расположения.
    * Можно реализовать сложные правила сбора, фильтрации и статистической обработки данных.
    * Сбор данных журнала на основе агентов часто ограничивается hello данных приемников, которые поддерживает агент hello. Некоторые агенты являются расширяемыми.

* *Доступ к данным приложения toointernal и контекстом*
   
    * Hello диагностики подсистемы, выполняющиеся внутри процесса hello приложения или службы можно легко дополнить hello трассировок с помощью контекстных сведений.
    * Сбор журналов на основе агентов, hello данные необходимо отправить агента tooan через механизм межпроцессного взаимодействия например трассировки событий Windows. Однако при таком механизме могут возникнуть дополнительные ограничения.

Это возможно toocombine и выгода от обоих методов сбора. На самом деле бывает hello наилучшим решением для многих приложений. Коллекция на основе агента — это естественное решение для сбора журналов связанные toohello весь кластер и отдельных узлах кластера. Это намного более надежным способом, чем сбор журналов в процессе, toodiagnose проблемы при запуске службы и сбоев. Кроме того многие службы, выполняющиеся внутри кластера Service Fabric, каждая служба, выполнив собственную коллекцию для внутрипроцессного журнала приведет многочисленные исходящие подключения из кластера hello. Большое количество исходящих подключений — сложная задача, для подсистемы сети hello и место назначения журналов hello. Агент (например, агент [**системы диагностики Azure**](../cloud-services/cloud-services-dotnet-diagnostics.md)) может собирать данные от нескольких служб и отправлять все данные через небольшое число подключений, повышая производительность. 

В этой статье показано, как tooset в процесс входа в коллекцию с помощью [ **EventFlow открытая библиотека**](https://github.com/Azure/diagnostics-eventflow). Другие библиотеки могут использоваться для hello же цели, но EventFlow имеет преимущество hello была разработана специально для внутрипроцессного журнала сбора и toosupport служб Service Fabric. Мы используем [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) как место назначения журналов hello. Можно также использовать [**концентраторы событий**](https://azure.microsoft.com/services/event-hubs/) или [**Elasticsearch**](https://www.elastic.co/products/elasticsearch). Это просто вопрос установки соответствующего пакета NuGet и Настройка назначения «hello» в файле конфигурации EventFlow hello. Дополнительные сведения о местах назначения журналов, отличных от Application Insights, см. в [документации по EventFlow](https://github.com/Azure/diagnostics-eventflow).

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a>Добавление проекта служб Service Fabric tooa библиотеки EventFlow
Двоичные файлы EventFlow предоставляются как набор пакетов NuGet. tooadd EventFlow проект службы tooa Service Fabric, щелкните правой кнопкой мыши проект hello в hello обозреватель решений и выберите «Управление NuGet пакетов». Перейдите на вкладку toohello «Просмотр» и выполните поиск «`Diagnostics.EventFlow`»:

![Пакеты NuGet EventFlow в диспетчере пакетов NuGet Visual Studio][1]

EventFlow, где размещается служба Hello должна включать соответствующие пакеты, в зависимости от hello источника и назначения для журналов приложения hello. Добавьте hello следующие пакеты: 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * (toocapture данных из класса EventSource hello службы и из стандартной EventSources, такие как *Майкрософт ServiceFabric* и *Microsoft ServiceFabric субъекты*)
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * (мы будем toosend hello журналы tooan Azure Application Insights ресурсов)  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * (включает инициализацию конвейера EventFlow hello из конфигурации службы Service Fabric и сообщает обо всех проблемах с Отправка диагностических данных в виде отчетов о работоспособности Service Fabric)

> [!NOTE]
> `Microsoft.Diagnostics.EventFlow.Inputs.EventSource`пакет требует tootarget проекта hello службы .NET Framework 4.6 или более поздней версии. Убедитесь, что значение hello соответствующие требуемой версии .NET framework в свойствах проекта перед установкой данного пакета. 

После того как все hello пакеты установлены, hello следующим шагом является tooconfigure и включите EventFlow hello службы.

## <a name="configuring-and-enabling-log-collection"></a>Настройка и включение сбора журналов
EventFlow конвейера, отвечающего за отправку журналов hello создается на основе спецификации, хранящейся в файле конфигурации. Пакет `Microsoft.Diagnostics.EventFlow.ServiceFabric` устанавливает начальный файл конфигурации EventFlow в паку решения `PackageRoot\Config`. Имя файла Hello `eventFlowConfig.json`. Этот файл конфигурации требует изменения toobe toocapture данные от служб по умолчанию hello `EventSource` класса и отправить службе аналитики tooApplication данных.

> [!NOTE]
> Мы предполагаем, что вы знакомы с **Azure Application Insights** службы, а также наличие ресурс Application Insights, планирование toouse toomonitor службе Service Fabric. Если вам требуются дополнительные сведения, ознакомьтесь с разделом [Создание ресурса Application Insights](../application-insights/app-insights-create-new-resource.md).

Привет открыть `eventFlowConfig.json` в редактор hello и измените его содержимое, как показано ниже. Убедитесь, что tooreplace hello ServiceEventSource имя и ключ инструментирования Application Insights в соответствии с toocomments. 

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
> Hello ServiceEventSource службы называется hello значение свойства Name hello hello `EventSourceAttribute` применения toohello ServiceEventSource класса. Он будет указан в hello `ServiceEventSource.cs` файл, который является частью службы кода hello. Например, в hello следующий код фрагмент кода hello hello ServiceEventSource имеет имя *MyCompany Application1-Stateless1*:
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

Обратите внимание, что файл `eventFlowConfig.json` входит в пакет конфигурации службы. Файл toothis изменения могут быть включены в full или конфигурации — только для обновления службы hello, тема tooService обновление проверки работоспособности и автоматического отката при наличии сбоя обновления. Дополнительные сведения см. в разделе [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).

Последний шаг Hello — tooinstantiate EventFlow конвейера в код запуска службы, расположенных в `Program.cs` файла. В hello помечены следующие дополнения связанных EventFlow пример с комментариями, начиная с `****`:

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

Имя Hello передается как параметр hello hello `CreatePipeline` метод hello `ServiceFabricDiagnosticsPipelineFactory` — имя hello hello *сущности работоспособности* представляющий hello EventFlow журнала коллекции конвейера. Это имя используется в том случае, если обнаруживает EventFlow и ошибок и сообщает об этом через hello подсистемы работоспособности Service Fabric.

## <a name="verification"></a>Проверка
Запустите службу и понаблюдайте за hello отладки окна вывода в Visual Studio. После запуска службы hello должна появиться свидетельство, что служба отправляет записи «Телеметрию Application Insights». Откройте веб-браузер и перейдите последовательно выберите tooyour ресурс Application Insights. Откройте вкладку «Поиск» (вверху hello колонка «Обзор» по умолчанию hello). После небольшой задержки должна появиться данные трассировок на портале Application Insights hello:

![Журналы из Service Fabric на портале Application Insights][2]

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о диагностике и мониторинге службы Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [Документация по EventFlow](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
