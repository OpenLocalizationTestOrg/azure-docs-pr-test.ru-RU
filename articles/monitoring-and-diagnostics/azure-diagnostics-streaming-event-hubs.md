---
title: "данные диагностики Azure в hello Горячий путь с помощью концентраторов событий aaaStreaming | Документы Microsoft"
description: "Настройку диагностики Azure с концентраторами событий последний tooend, включая руководство для распространенных сценариев."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a>Потоковая передача данных диагностики Azure в hello Горячий путь с помощью концентраторов событий
Диагностика Azure предоставляет гибкие возможности toocollect метрики и журналов из облачных служб виртуальных машин (ВМ) и передачи результатов tooAzure хранилища. Начиная с версии hello марта 2016 г. (SDK 2.9) временные рамки, можно отправить toocustom диагностики источники данных и передачи данных Горячий путь в секундах с помощью [концентраторов событий Azure](https://azure.microsoft.com/services/event-hubs/).

Поддерживаемые типы данных включают:

* Трассировка событий Windows (ETW)
* Счетчики производительности
* Журналы событий Windows
* Журналы приложений
* Журналы инфраструктуры системы диагностики Azure

В этой статье рассказывается о том, tooconfigure диагностики Azure с концентраторами событий из конечного tooend. Также описаны следующие распространенные сценарии hello:

* Каким образом ведет журнал toocustomize hello и метрики, которые отправляются tooEvent концентраторы
* Как toochange конфигураций в каждой среде
* Как концентраторы событий tooview поток данных
* Как tootroubleshoot hello подключения  

## <a name="prerequisites"></a>Предварительные требования
Данные receieving концентраторов событий из системы диагностики Azure поддерживаются в облачных служб, виртуальных машин, наборы масштабирования виртуальных машин и Service Fabric, начиная с Azure SDK 2.9 hello и hello соответствующий средства Azure для Visual Studio.

* Расширение системы диагностики Azure версии 1.6 (в[пакете SDK для Azure для .NET 2.9 или более поздней версии](https://azure.microsoft.com/downloads/) оно используется по умолчанию).
* [Visual Studio 2013 или более поздней версии](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* Существующие конфигурации диагностики Azure в приложении с помощью *.wadcfgx* файл и один из следующих методов hello:
  * Visual Studio: [настройка системы диагностики для облачных служб и виртуальных машин Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Windows PowerShell: [включение диагностики в облачных службах Azure с помощью PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)
* Пространство имен концентраторов событий подготовлены для статьи hello [приступить к работе с концентраторами событий](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a>Подключение приемника концентраторов tooEvent диагностики Azure
По умолчанию диагностики Azure всегда отправляет журналы и показатели tooan учетной записи хранилища Azure. Приложения также могут отправлять данные tooEvent концентраторов путем добавления нового **приемники** "раздела" hello **PublicConfig** / **WadCfg** элемент hello *.wadcfgx* файла. В Visual Studio hello *.wadcfgx* файл хранится в пути hello: **проекта облачной службы** > **ролей** > **() RoleName)** > **diagnostics.wadcfgx** файла.

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

В этом примере URL-адрес имеет значение toohello полностью концентратора событий hello полное пространство имен концентратора событий hello: пространство имен концентраторов событий + «/» + имя концентратора событий.  

URL-адрес отображается в hello концентратора событий Hello [портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885) на панели мониторинга hello концентраторов событий.  

Hello **приемника** имя можно задать допустимую строку tooany при условии, что hello одинаковое значение согласованно используется в файле конфигурации hello.

> [!NOTE]
> В этом разделе могут быть настроены дополнительные приемники, например *applicationInsights* . Система диагностики Azure позволяет одному или более приемники определено, если каждый приемник также объявляется в hello toobe **PrivateConfig** раздела.  
>
>

Hello концентраторов событий приемник должен также быть объявляются и определяются в hello **PrivateConfig** раздел hello *.wadcfgx* файла конфигурации.

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

Hello `SharedAccessKeyName` значение должно соответствовать ключ подписи общего доступа (SAS) и политики, который был определен в hello **концентраторов событий** пространства имен. Обзор панели мониторинга концентраторов событий toohello в hello [портал Azure](https://manage.windowsazure.com), щелкните hello **Настройка** вкладку и настроить именованной политики (например, «SendRule»), который имеет *отправки* разрешения. Hello **StorageAccount** также объявляется в **PrivateConfig**. Нет необходимости toochange значения, если они работают. В этом примере мы оставьте hello значения пустой, это знак, подчиненных активов будет устанавливать значения hello. Например, hello *ServiceConfiguration.Cloud.cscfg* файла конфигурации среды задает имена неподходящей среде hello и ключи.  

> [!WARNING]
> ключ SAS концентраторов событий Hello хранится в виде обычного текста в hello *.wadcfgx* файла. Часто этот ключ возврата системы управления версиями toosource или доступна как ресурс в ваш сервер сборки, поэтому его следует защитить соответствующим образом. Рекомендуется использовать ключ SAS с *только отправку* разрешения таким образом, пользователь-злоумышленник может записи toohello концентратора событий, но не прослушивания tooit или управлять им.
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a>Настройка системы диагностики Azure toosend журналы и показатели tooEvent концентраторы
Как отмечалось ранее, все по умолчанию и пользовательские диагностические данные, то есть метрики и журналов, автоматически отправляется tooAzure хранилища в интервалах hello настроен. С концентраторами событий и любой дополнительный приемник можно указать любой корневой или конечный узел в toobe иерархии hello отправлено toohello концентратора событий. К этим данным относятся события трассировки Windows, счетчики производительности, журналы событий Windows и журналы приложений.   

Очень важно, передача концентраторов tooEvent tooconsider следует количества точек данных. Обычно разработчики передают по критическому пути с низкой задержкой данные, которые должны быть быстро использованы и интерпретированы. Примерами являются системы, отслеживающие предупреждения, или правила автомасштабирования. Разработчик также может настроить альтернативное хранилище данных анализа или поиска, например, Stream Analytics, ElasticSearch, пользовательской системы мониторинга или сторонней системы мониторинга, которую вы предпочитаете.

Hello ниже приведены некоторые примеры конфигурации.

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

В приведенном выше примере hello, hello приемник является родительским примененных toohello **PerformanceCounters** узла в иерархии hello, что означает все дочерние **PerformanceCounters** будут отправляться tooEvent концентраторов.  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

В предыдущем примере hello hello приемник является три счетчика примененных tooonly: **запросов в очереди**, **отклонение запросов**, и **% загруженности процессора**.  

Hello следующем примере показано, как разработчик может ограничить hello объем отправляемых данных toobe hello важные метрики, используемые для этой службы работоспособности.  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

В этом примере hello приемник примененных toologs который отфильтрованный только tooerror уровня трассировки.

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>Развертывание и обновление приложения облачной службы и конфигурации системы диагностики
Visual Studio предоставляет hello самый простой путь toodeploy hello приложения и конфигурации приемника концентраторов событий. hello tooview и измените файл, открыть hello *.wadcfgx* файла в Visual Studio, измените его и сохранить его. путь Hello **проекта облачной службы** > **ролей** > **(RoleName)** > **diagnostics.wadcfgx**.  

На этом этапе все и развертывания обновление действий в Visual Studio, Visual Studio Team System и всех команд или сценариев, которые основаны на MSBuild и использовать hello **/t: публикация** целевой включают hello *.wadcfgx*  в процессе обработки пакетов hello. Кроме того развертывания и обновления развертывание hello tooAzure файла с помощью hello соответствующее расширение агента диагностики Azure на виртуальные машины.

После развертывания приложения hello и конфигурации системы диагностики Azure будет сразу же видеть действия на панели мониторинга hello hello концентратора событий. Это означает, что вы будете готовы toomove на tooviewing hello-path данных hello прослушивателя клиента или анализа средство по вашему выбору.  

Следующий рисунок hello hello концентраторов событий мониторинга представлен работоспособное отправку диагностики данных toohello события концентратора запуск через некоторое время после 23: 00. Это время hello приложение было развернуто с обновленной *.wadcfgx* файла и hello приемника был настроен должным образом.

![][0]  

> [!NOTE]
> При внесении toohello обновлений для файла конфигурации диагностики Azure (.wadcfgx), рекомендуется push hello обновления toohello всего приложения, а также hello конфигурации с помощью публикации Visual Studio или сценарий Windows PowerShell.  
>
>

## <a name="view-hot-path-data"></a>Просмотр данных, передаваемых по критическому пути
Как отмечалось ранее, существует множество вариантов использования для прослушивания tooand обработки данных для концентраторов событий.

Один простой подход — toocreate небольшую тестовую консольного приложения toolisten toohello концентратора событий и Здравствуй, мир выходной поток. Можно поместить следующий код, который является более подробно в hello [приступить к работе с концентраторами событий](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), в консольном приложении.  

Обратите внимание, что консольное приложение hello должен включать hello [пакет NuGet узел обработчика событий](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).  

Запомнить tooreplace значения hello в угловые скобки в hello **Main** функция со значениями для ресурсов.   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a>Устранение неполадок приемников концентраторов событий
* концентратор событий Hello не показывает активность входящих или исходящих событий должным образом.

    Убедитесь в том, что концентратор событий успешно подготовлен. Все сведения о соединении в hello **PrivateConfig** раздел *.wadcfgx* должна соответствовать значениям hello ресурса, как показано на портале hello. Убедитесь, что SAS политики определен («SendRule» в примере hello) в hello портала и что *отправки* разрешение.  
* После обновления концентратора событий hello перестал активности входящих или исходящих событий.

    Во-первых, убедитесь, что этот концентратор событий hello и сведения о конфигурации указано правильно, как описано выше. Здравствуйте, иногда **PrivateConfig** сбрасывается в обновлении развертывания. Hello рекомендуется исправить, все изменения слишком toomake*.wadcfgx* в hello проект и затем отправить обновления завершения приложения. Если это невозможно, убедитесь, что это обновление диагностики hello помещает полный **PrivateConfig** , включающего hello ключ SAS.  
* Я попытался предложения hello и hello концентратора событий по-прежнему не работает.

    Попробуйте найти в таблице хранилища Azure hello, содержащий и журналы ошибок для самой системе диагностики Azure: **WADDiagnosticInfrastructureLogsTable**. Один из вариантов — toouse средства, как [обозреватель хранилищ Azure](http://www.storageexplorer.com) учетной записи хранилища toothis tooconnect просмотра этой таблицы и добавить запрос для меток времени в hello последние 24 часа. Можно использовать средство hello tooexport в CSV-файл и откройте его в приложении, таком как Microsoft Excel. Excel позволяет легко toosearch карточки строк, таких как **EventHubs**, toosee, что возникла ошибка.  

## <a name="next-steps"></a>Дальнейшие действия
•    [Дополнительные сведения о концентраторах событий](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>Приложение. Полный пример файла конфигурации системы диагностики Azure (WADCFGX-файл)
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

Hello взаимодополняющие *ServiceConfiguration.Cloud.cscfg* для выглядит в этом примере hello следующим образом.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

Эквивалентные параметры на основе JSON для виртуальных машин выглядят следующим образом:
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия
На сайте ссылкам hello, изучите более подробную концентраторов событий:

* [Обзор концентраторов событий](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Создание концентратора событий](../event-hubs/event-hubs-create.md)
* [Часто задаваемые вопросы о концентраторах событий](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
