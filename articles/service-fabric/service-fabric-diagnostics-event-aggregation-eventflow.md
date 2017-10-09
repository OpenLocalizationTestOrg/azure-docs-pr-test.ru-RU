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
# <a name="event-aggregation-and-collection-using-eventflow"></a>Агрегирование и сбор событий с помощью EventFlow

[EventFlow диагностики Microsoft](https://github.com/Azure/diagnostics-eventflow) может направлять события tooone узел или несколько назначений мониторинга. Так как он включен в виде пакета NuGet в проекте службы, EventFlow код и конфигурация перемещаются вместе hello службы, что исключает проблемы с конфигурацией отдельным узлам hello сказано о службе диагностики Azure. EventFlow выполняется внутри одного процесса службы и выходы настроены toohello подключается напрямую. Из-за прямого подключения hello EventFlow работает в Azure, контейнер и развертывания службы в локальной среде. Соблюдайте осторожность при выполнении EventFlow в сценариях с высокой плотностью, например в контейнере, так как каждый конвейер EventFlow создает внешнее соединение. Если вы разместите несколько процессов, то получите несколько исходящих подключений. Это не столько значения для приложения Service Fabric, так как все реплики `ServiceType` запуска в hello же процесс, а это ограничивает hello число исходящих подключений. EventFlow также предлагает фильтрацию событий, так что отправляются только события hello, которые соответствуют заданному фильтру hello.

## <a name="setting-up-eventflow"></a>Настройка EventFlow

Двоичные файлы EventFlow предоставляются как набор пакетов NuGet. tooadd EventFlow проект службы tooa Service Fabric, щелкните правой кнопкой мыши проект hello в hello обозреватель решений и выберите «Управление NuGet пакетов». Перейдите на вкладку toohello «Просмотр» и выполните поиск «`Diagnostics.EventFlow`»:

![Пакеты NuGet EventFlow в диспетчере пакетов NuGet Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

Появится список различных пакетов, которые помечены как "Входные данные" и "Выходные данные". EventFlow поддерживает различные регистраторы и анализаторы журналов. EventFlow, где размещается служба Hello должна включать соответствующие пакеты, в зависимости от hello источника и назначения для журналов приложения hello. В дополнение к этому toohello ServiceFabric базовый пакет, также потребуется по крайней мере один вход и выход, которые настроены. В примере можно добавить следующие пакеты toosent EventSource события tooApplication аналитики hello:

* `Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture данных из класса EventSource hello службы и из стандартной EventSources, такие как *Майкрософт ServiceFabric* и *Microsoft ServiceFabric субъекты*)
* `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(мы будем toosend hello журналы tooan Azure Application Insights ресурсов)
* `Microsoft.Diagnostics.EventFlow.ServiceFabric`(включает инициализацию конвейера EventFlow hello из конфигурации службы Service Fabric и сообщает обо всех проблемах с Отправка диагностических данных в виде отчетов о работоспособности Service Fabric)

>[!NOTE]
>`Microsoft.Diagnostics.EventFlow.Input.EventSource`пакет требует tootarget проекта hello службы .NET Framework 4.6 или более поздней версии. Убедитесь, что значение hello соответствующие требуемой версии .NET framework в свойствах проекта перед установкой данного пакета.

После того как все hello пакеты установлены, hello следующим шагом является tooconfigure и включите EventFlow hello службы.

## <a name="configuring-and-enabling-log-collection"></a>Настройка и включение сбора журналов
конвейер EventFlow Hello, отвечающего за отправку журналов hello создается на основе спецификации, хранящейся в файле конфигурации. Hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` пакет устанавливает файл начальной конфигурации EventFlow под `PackageRoot\Config` папку решения, с именем `eventFlowConfig.json`. Этот файл конфигурации требует изменения toobe toocapture данные от служб по умолчанию hello `EventSource` класс и любые другие входные данные должны tooconfigure и отправки данных toohello соответствующее место.

Ниже приведен пример *eventFlowConfig.json* зависимости пакетов NuGet hello, упомянутых выше:
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

Hello ServiceEventSource службы называется hello значение свойства Name hello hello `EventSourceAttribute` применения toohello ServiceEventSource класса. Он будет указан в hello `ServiceEventSource.cs` файл, который является частью службы кода hello. Например, в hello следующий код фрагмент кода hello hello ServiceEventSource имеет имя *MyCompany Application1-Stateless1*:

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

Обратите внимание, что файл `eventFlowConfig.json` входит в пакет конфигурации службы. Файл toothis изменения могут быть включены в full или конфигурации — только для обновления службы hello, тема tooService обновление проверки работоспособности и автоматического отката при наличии сбоя обновления. Дополнительные сведения см. в разделе [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).

Hello *фильтры* раздел конфигурации hello позволяет toofurther собственные данные hello, toogo переход через hello EventFlow конвейера toohello выходов, позволяя toodrop включать определенные данные или изменить hello Структура данных о событиях hello. Дополнительные сведения о фильтрации см. в разделе [Фильтры EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).

Последний шаг Hello — tooinstantiate EventFlow конвейера в код запуска службы, расположенных в `Program.cs` файла:

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

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a>С помощью настройки структуры службы и eventFlowConfig tooin параметров приложения

EventFlow поддерживает, с помощью Service Fabric и неверные параметры tooconfigure EventFlow параметры приложений. Можно ссылаться с помощью этого синтаксиса для значений структуры параметров tooService:

```json
servicefabric:/<section-name>/<setting-name>
``` 

`<section-name>`— Имя hello hello Service Fabric раздел конфигурации, и `<setting-name>` Установка конфигурации hello, предоставляя hello значение, которое будет использоваться tooconfigure EventFlow параметр. Дополнительные сведения о том, как tooread toodo, перейдите слишком[поддержку настройки структуры службы и параметры приложения](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).

## <a name="verification"></a>Проверка

Запустите службу и понаблюдайте за hello отладки окна вывода в Visual Studio. После запуска службы hello должна появиться свидетельство, которое отправляет службе записи toohello выходных данных, который вы настроили. Перейдите событие tooyour анализа и визуализации платформы и убедитесь, что журналы запустили tooshow вверх (может потребоваться несколько минут).

## <a name="next-steps"></a>Дальнейшие действия

* [Анализ событий и визуализация с помощью Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Анализ событий и визуализация с помощью OMS](service-fabric-diagnostics-event-analysis-oms.md)
* [Документация по EventFlow](https://github.com/Azure/diagnostics-eventflow)