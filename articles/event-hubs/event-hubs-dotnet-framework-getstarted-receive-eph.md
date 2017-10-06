---
title: "Здравствуйте, aaaReceive события из концентраторов событий Azure с помощью .NET Framework | Документы Microsoft"
description: "Выполните этот учебник tooreceive события из концентраторов событий Azure с помощью hello .NET Framework."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a>Получать события из концентраторов событий Azure с помощью hello .NET Framework

## <a name="introduction"></a>Введение

Концентраторы событий — это служба, которая обрабатывает большие объемы данных телеметрии о событиях, поступающих от подключенных устройств и приложений. После сбора данных в концентраторы событий, можно хранить данные hello, с помощью кластера хранилища или преобразование с помощью поставщика аналитика в реальном времени. Эта возможность сбора и обработки крупномасштабных событий является ключевым компонентом архитектуры современных приложений, включая hello Интернета вещей (IoT).

В этом учебнике показано, как toowrite .NET Framework консольного приложения, которая получает сообщения из концентратора событий с помощью hello  **[узел обработчика событий][EventProcessorHost]**. toosend события, с помощью hello .NET Framework, см. hello [отправки событий с помощью .NET Framework hello концентраторов событий tooAzure](event-hubs-dotnet-framework-getstarted-send.md) статьи или щелкните соответствующий язык отправку hello в левой таблице hello содержимого.

Hello [узел обработчика событий] [ EventProcessorHost] представляет собой класс .NET, упрощающее получать события из концентраторов событий, поскольку управление постоянно конечными точками и параллельного получает от этих концентраторов событий. С помощью hello [узел обработчика событий][Event Processor Host], события можно распределить между несколькими получателями, даже в том случае, если размещенные в разных узлах. В этом примере показано, как toouse hello [узел обработчика событий] [ EventProcessorHost] для одного получателя. Hello [масштабирования обработки событий] [ Scale out Event Processing with Event Hubs] образце показано, как toouse hello [узел обработчика событий] [ EventProcessorHost] с несколькими получателями.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника требуется hello следующие предварительные требования:

* [Microsoft Visual Studio 2015 или более поздней версии](http://visualstudio.com). снимки экрана приветствия в этом учебнике с помощью Visual Studio 2017 г.
* Активная учетная запись Azure. Если ее нет, можно создать бесплатную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Создание пространства имен концентраторов событий и концентратора событий

Hello первым шагом является toouse hello [портал Azure](https://portal.azure.com) toocreate в пространство имен введите концентраторов событий и получить учетные данные управления, приложение должно toocommunicate с концентратором событий hello hello. toocreate пространство имен и концентратора событий, выполните процедуру hello в [в этой статье](event-hubs-create.md), продолжите hello, описанных в этом учебнике.

## <a name="create-an-azure-storage-account"></a>Создание учетной записи хранения Azure

toouse hello [узел обработчика событий][EventProcessorHost], необходимо иметь [учетной записи хранилища Azure][Azure Storage account]:

1. Войдите на toohello [портал Azure][Azure portal]и нажмите кнопку **New** на hello верхнего левого угла экрана приветствия.
2. Щелкните **Хранилище**, а затем — **Учетная запись хранения**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. В hello **создать учетную запись хранения** колонки, введите имя для учетной записи хранения hello. Выберите подписку Azure, группа ресурсов и расположение в какой ресурс toocreate hello. Затем щелкните **Создать**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. В списке учетных записей хранения hello выберите hello вновь созданные учетной записи хранилища.
5. В колонке hello учетной записи хранилища щелкните **ключи доступа**. Скопируйте значение hello **key1** toouse далее в этом учебнике.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a>Создание консольного приложения получателя

1. В Visual Studio создайте новый проект приложения рабочего стола Visual C# с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **получателя**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. В обозревателе решений щелкните правой кнопкой мыши hello **получателя** проекта, а затем нажмите кнопку **управление пакетами NuGet для решения**.
3. Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus Event Hub - EventProcessorHost`. Нажмите кнопку **установить**и примите условия использования hello.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    Visual Studio загрузит, устанавливает и добавляет toohello ссылки [Azure концентратора событий служебной шины - пакет EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), с его зависимости.
4. Щелкните правой кнопкой мыши hello **получателя** проекта, нажмите кнопку **добавить**и нажмите кнопку **класса**. Имя нового класса hello **SimpleEventProcessor**, а затем нажмите кнопку **добавить** toocreate hello класса.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. Добавьте следующие инструкции в начале hello файла SimpleEventProcessor.cs hello hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  Затем замените следующий код для основного текста hello класса hello hello:
    
  ```csharp
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
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  Этот класс вызывается hello **EventProcessorHost** tooprocess события, получаемые от концентратора событий hello. Hello `SimpleEventProcessor` класс использует метод контрольного таймера tooperiodically вызов hello контрольной точки на hello **EventProcessorHost** контекста. Такая обработка гарантирует, что при перезапуске приемника hello, теряет не более пяти минут обработки рабочих.
6. В hello **программы** класса, добавьте следующее hello `using` в начало файла hello hello инструкцию:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  Затем замените hello `Main` метод в hello `Program` класса hello, следующий код, подставив имя концентратора событий hello и подключение уровня пространства имен hello строки, которые ранее сохранена и hello учетной записи хранилища и ключ, который был скопирован в hello предыдущих разделов. 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
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
  ```

7. Запустите программу hello и убедитесь, что отсутствуют ошибки.
  
Поздравляем! Теперь вы получили сообщений из концентратора событий с помощью hello узел обработчика событий.


> [!NOTE]
> В данном руководстве используется один экземпляр [EventProcessorHost][EventProcessorHost]. tooincrease пропускной способности, рекомендуется запустить несколько экземпляров [EventProcessorHost][EventProcessorHost], как показано в hello [масштаб обработку события] [масштаб обработку события] образца. В таких случаях hello различные экземпляры автоматически координировать друг с другом tooload баланс hello полученных событий. Если требуется несколько получателей tooeach процесс *все* hello событий, необходимо использовать hello **ConsumerGroup** концепции. При получении события из разных компьютерах, бывает полезно toospecify имена для [EventProcessorHost] [ EventProcessorHost] экземпляров на основе машины hello (или ролей), в котором они развернуты. Дополнительные сведения об этих темах см. в разделе hello [Обзор концентраторов событий] [ Event Hubs overview] и hello [руководство по программированию концентраторов событий] [ Event Hubs Programming Guide] разделы.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы создали рабочее приложение, которое создает концентратора событий и отправляет и получает данные, Дополнительные сведения, перейдя по адресу hello ссылкам:

* [Узел обработчика событий][Event Processor Host]
* [Обзор концентраторов событий Azure][Event Hubs overview].
* [Часто задаваемые вопросы о концентраторах событий](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
