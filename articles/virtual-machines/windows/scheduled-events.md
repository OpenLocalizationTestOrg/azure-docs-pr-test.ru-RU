---
title: "aaaScheduled событий для виртуальных машин Windows в Azure | Документы Microsoft"
description: "Запланированные события использования hello Azure метаданные службы для виртуальных машинах Windows."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a>Служба метаданных Azure. Запланированные события (предварительная версия) для виртуальных машин Windows

> [!NOTE] 
> Предварительный просмотр вносятся доступных tooyou, вы принимаете условия использования toohello условие hello. Дополнительные сведения см. в статье [Дополнительные условия использования предварительных выпусков Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Запланированные события является одним из subservices hello под hello Azure метаданных службы. Она предоставляет сведения о предстоящих событиях (например, перезагрузках), что позволяет приложениям подготовиться к ним и уменьшить влияние на работу. Эти сведения доступны для всех типов виртуальных машин Azure, включая PaaS и IaaS. Запланированные события предоставляет виртуальную машину времени задачи профилактического tooperform эффект hello toominimize события. 

Запланированные события доступны для виртуальных машин Windows и Linux. Сведения о запланированных событиях в Linux см. в статье [Служба метаданных Azure. Запланированные события (предварительная версия) для виртуальных машин Linux](../windows/scheduled-events.md).

## <a name="why-scheduled-events"></a>Зачем нужны запланированные события

С запланированные события можно предпринять шаги hello влияние toolimit intiated платформы обслуживания или действия, инициируемые пользователем в службе. 

Несколькими экземплярами рабочих нагрузок, которые используют состояние toomaintain методы репликации, могут быть уязвимыми toooutages происходит между несколькими экземплярами. Такие простои могут потребовать дорогостоящих действий (например, перестроения индексов) или привести к потере реплики. 

Во многих других случаях hello общую доступность службы может быть повышена путем выполнения последовательность отключения, таких как завершение (или отменяемое) транзакции на лету, переназначение задачи tooother виртуальных машин в кластере hello (отработка отказа вручную) или удаление hello Виртуальную машину из пула подсистемы балансировки нагрузки сети. 

Существуют случаи, где обращения к администратору о предстоящих событий или ведение журнала такого события помочь повышение hello удобство обслуживания приложений, размещенных в облаке hello.

Варианты использования Azure служба метаданных поверхности запланированные события в hello ниже:
-   Инициируемое платформой обслуживание (например, развертывание ОС узла).
-   Инициируемые пользователем вызовы (например, пользователь перезапускает или повторно развертывает виртуальную машину).


## <a name="hello-basics"></a>Основы Hello  

Azure служба метаданных предоставляет сведения о запуске виртуальных машин с помощью конечной точки REST, доступный из hello виртуальной Машины. сведения о Hello доступна через немаршрутизируемый IP, чтобы она не предоставляется вне hello виртуальной Машины.

### <a name="scope"></a>Область
Запланированные события, отображается tooall виртуальных машин в облачной службе или tooall виртуальных машин в группе доступности. Поэтому следует проверить hello `Resources` в tooidentify событий hello, в которой виртуальные машины будут затронуты toobe. 

### <a name="discovering-hello-endpoint"></a>Обнаружение конечной точки hello
В случае hello, где создается виртуальной машины в виртуальной сети (VNet), служба метаданных hello доступна из статический немаршрутизируемый IP- `169.254.169.254`.
Если hello виртуальной машины в виртуальной сети вариантов по умолчанию hello для облачных служб и классические ВМ не создается дополнительная логика является toouse конечной точки требуется toodiscover hello. См. Образец toolearn toothis как слишком[обнаружение конечной точки узлов hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Управление версиями 
Hello метаданных экземпляра службы с версиями. Версии являются обязательными, и текущая версия hello `2017-03-01`.

> [!NOTE] 
> Предыдущие выпуски Предварительный просмотр поддерживается {последние} в качестве hello api-version запланированные события. Этот формат не поддерживается и будет считаться устаревшей в будущем hello.

### <a name="using-headers"></a>Использование заголовков
При запросе hello метаданных службы, необходимо указать заголовок hello `Metadata: true` tooensure hello запрос не был перенаправлен непреднамеренно.

### <a name="enabling-scheduled-events"></a>Включение запланированных событий
Hello при первом запуске запроса для запланированных событий Azure неявно включает hello функцию на виртуальной машине. Поэтому следует ожидать задержки ответа в первом вызове из копии tootwo минут.

### <a name="user-initiated-maintenance"></a>Обслуживание, инициированное пользователем
Пользователь запустил обслуживание виртуальных машин через hello портал Azure API, CLI, или PowerShell приводит запланированное событие. Это позволяет tootest hello обслуживания подготовки логики в приложении а tooprepare вашего приложения для обслуживания инициированной пользователем.

При перезапуске виртуальной машины планируется событие с типом `Reboot`. При развертывании виртуальной машины планируется событие с типом `Redeploy`.

> [!NOTE] 
> Сейчас можно одновременно запланировать более десяти операций обслуживания, инициированных пользователем. Это ограничение будет снято еще до выпуска общедоступной версии запланированных событий.

> [!NOTE] 
> Сейчас обслуживание, инициированное пользователем, которое влияет на запланированные события, не настраивается. Возможность настройки запланирована к следующему выпуску.

## <a name="using-hello-api"></a>С помощью hello API

### <a name="query-for-events"></a>Запрос сведений о событиях
Вы можете запрашивать запланированные события, просто выполнив hello следующий вызов:

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

Ответ содержит массив запланированных событий. Если это будет пустой массив, значит сейчас запланированных событий нет.
В случае hello которых запланированные события, hello ответ содержит массив событий: 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>Свойства события
|Свойство  |  Описание |
| - | - |
| EventId | Глобальный уникальный идентификатор этого события. <br><br> Пример: <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| EventType | Влияние, которое оказывает это событие. <br><br> Значения: <br><ul><li> `Freeze`: hello виртуальной машины — запланированных toopause несколько секунд. Hello ЦП приостанавливается, но не влияет на открытые файлы, сетевые подключения или оперативной памяти. <li>`Reboot`: hello запланирована перезагрузка виртуальной машины (непостоянные памяти теряются). <li>`Redeploy`: hello виртуальной машины является узлом tooanother запланированных toomove (временных дисков теряются). |
| ResourceType | Тип ресурса, на который влияет это событие. <br><br> Значения: <ul><li>`VirtualMachine`|
| Ресурсы| Список ресурсов, на которые влияет это событие. Это гарантируется машины toocontain из не более одного [домен обновления](manage-availability.md), но не может содержать все машины в hello UD. <br><br> Пример: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Event Status | Состояние этого события. <br><br> Значения: <ul><li>`Scheduled`: Это событие является запланированных toostart после hello времени, указанного в hello `NotBefore` свойство.<li>`Started`. Это событие запущено.</ul> Не `Completed` или когда-либо предоставляется как состояние; hello событие больше не возвращаются при завершении события hello.
| NotBefore| Время, после которого может быть запущено это событие. <br><br> Пример: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Планирование события
Каждое событие запланирована минимальное количество времени в будущем hello в зависимости от типа события. Это время отражается в свойстве события `NotBefore`. 

|EventType  | Минимальное время уведомления |
| - | - |
| Freeze| 15 минут |
| Reboot | 15 минут |
| Повторное развертывание | 10 минут |

### <a name="starting-an-event"></a>Запуск события 

Как только вы узнали о предстоящих событий и завершили свою логику для нормальное завершение работы, вы можете утвердить необработанных событий hello, делая `POST` вызова toohello метаданные службы с hello `EventId`. Указывает tooAzure, он может сократить минимальное уведомления hello время (если возможно). 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> Подтверждение события позволяет hello tooproceed событий для всех `Resources` в событии hello не только hello виртуальную машину, которая подтверждает hello событий. Таким образом можно tooelect подтверждение hello руководитель toocoordinate, которое может быть простым как первой машине hello в hello `Resources` поля.


## <a name="powershell-sample"></a>Пример для PowerShell 

Hello следующие примеры запросов hello метаданные службы для запланированных событий и утверждает каждого необработанные события.

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a>Пример на языке C\# 

Hello следующий пример является простой клиента, которая взаимодействует со службой метаданных hello.

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

Запланированные события может быть представлен с помощью hello следующие структуры данных.

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

Hello следующие примеры запросов hello метаданные службы для запланированных событий и утверждает каждого необработанные события.

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a>Пример на языке Python 

Hello следующие примеры запросов hello метаданные службы для запланированных событий и утверждает каждого необработанные события.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Дальнейшие действия 

- Дополнительные сведения о hello API-интерфейса в hello [метаданные экземпляра службы](instance-metadata-service.md).
- Подробнее о [плановом обслуживании виртуальных машин Windows в Azure](planned-maintenance.md).

