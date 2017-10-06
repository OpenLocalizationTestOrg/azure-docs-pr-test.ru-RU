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
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="79627-103">Получать события из концентраторов событий Azure с помощью hello .NET Framework</span><span class="sxs-lookup"><span data-stu-id="79627-103">Receive events from Azure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="79627-104">Введение</span><span class="sxs-lookup"><span data-stu-id="79627-104">Introduction</span></span>

<span data-ttu-id="79627-105">Концентраторы событий — это служба, которая обрабатывает большие объемы данных телеметрии о событиях, поступающих от подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="79627-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="79627-106">После сбора данных в концентраторы событий, можно хранить данные hello, с помощью кластера хранилища или преобразование с помощью поставщика аналитика в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="79627-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="79627-107">Эта возможность сбора и обработки крупномасштабных событий является ключевым компонентом архитектуры современных приложений, включая hello Интернета вещей (IoT).</span><span class="sxs-lookup"><span data-stu-id="79627-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="79627-108">В этом учебнике показано, как toowrite .NET Framework консольного приложения, которая получает сообщения из концентратора событий с помощью hello  **[узел обработчика событий][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="79627-108">This tutorial shows how toowrite a .NET Framework console application that receives messages from an event hub using hello **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="79627-109">toosend события, с помощью hello .NET Framework, см. hello [отправки событий с помощью .NET Framework hello концентраторов событий tooAzure](event-hubs-dotnet-framework-getstarted-send.md) статьи или щелкните соответствующий язык отправку hello в левой таблице hello содержимого.</span><span class="sxs-lookup"><span data-stu-id="79627-109">toosend events using hello .NET Framework, see hello [Send events tooAzure Event Hubs using hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click hello appropriate sending language in hello left-hand table of contents.</span></span>

<span data-ttu-id="79627-110">Hello [узел обработчика событий] [ EventProcessorHost] представляет собой класс .NET, упрощающее получать события из концентраторов событий, поскольку управление постоянно конечными точками и параллельного получает от этих концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="79627-110">hello [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="79627-111">С помощью hello [узел обработчика событий][Event Processor Host], события можно распределить между несколькими получателями, даже в том случае, если размещенные в разных узлах.</span><span class="sxs-lookup"><span data-stu-id="79627-111">Using hello [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="79627-112">В этом примере показано, как toouse hello [узел обработчика событий] [ EventProcessorHost] для одного получателя.</span><span class="sxs-lookup"><span data-stu-id="79627-112">This example shows how toouse hello [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="79627-113">Hello [масштабирования обработки событий] [ Scale out Event Processing with Event Hubs] образце показано, как toouse hello [узел обработчика событий] [ EventProcessorHost] с несколькими получателями.</span><span class="sxs-lookup"><span data-stu-id="79627-113">hello [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how toouse hello [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79627-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="79627-114">Prerequisites</span></span>

<span data-ttu-id="79627-115">toocomplete этого учебника требуется hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="79627-115">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="79627-116">[Microsoft Visual Studio 2015 или более поздней версии](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="79627-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="79627-117">снимки экрана приветствия в этом учебнике с помощью Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="79627-117">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="79627-118">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="79627-118">An active Azure account.</span></span> <span data-ttu-id="79627-119">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="79627-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="79627-120">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="79627-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="79627-121">Создание пространства имен концентраторов событий и концентратора событий</span><span class="sxs-lookup"><span data-stu-id="79627-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="79627-122">Hello первым шагом является toouse hello [портал Azure](https://portal.azure.com) toocreate в пространство имен введите концентраторов событий и получить учетные данные управления, приложение должно toocommunicate с концентратором событий hello hello.</span><span class="sxs-lookup"><span data-stu-id="79627-122">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="79627-123">toocreate пространство имен и концентратора событий, выполните процедуру hello в [в этой статье](event-hubs-create.md), продолжите hello, описанных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="79627-123">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="79627-124">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="79627-124">Create an Azure Storage account</span></span>

<span data-ttu-id="79627-125">toouse hello [узел обработчика событий][EventProcessorHost], необходимо иметь [учетной записи хранилища Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="79627-125">toouse hello [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="79627-126">Войдите на toohello [портал Azure][Azure portal]и нажмите кнопку **New** на hello верхнего левого угла экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="79627-126">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
2. <span data-ttu-id="79627-127">Щелкните **Хранилище**, а затем — **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="79627-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="79627-128">В hello **создать учетную запись хранения** колонки, введите имя для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="79627-128">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="79627-129">Выберите подписку Azure, группа ресурсов и расположение в какой ресурс toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="79627-129">Choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="79627-130">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="79627-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="79627-131">В списке учетных записей хранения hello выберите hello вновь созданные учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="79627-131">In hello list of storage accounts, click hello newly created storage account.</span></span>
5. <span data-ttu-id="79627-132">В колонке hello учетной записи хранилища щелкните **ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="79627-132">In hello storage account blade, click **Access keys**.</span></span> <span data-ttu-id="79627-133">Скопируйте значение hello **key1** toouse далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="79627-133">Copy hello value of **key1** toouse later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="79627-134">Создание консольного приложения получателя</span><span class="sxs-lookup"><span data-stu-id="79627-134">Create a receiver console application</span></span>

1. <span data-ttu-id="79627-135">В Visual Studio создайте новый проект приложения рабочего стола Visual C# с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="79627-135">In Visual Studio, create a new Visual C# Desktop App project using hello **Console  Application** project template.</span></span> <span data-ttu-id="79627-136">Имя проекта hello **получателя**.</span><span class="sxs-lookup"><span data-stu-id="79627-136">Name hello project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="79627-137">В обозревателе решений щелкните правой кнопкой мыши hello **получателя** проекта, а затем нажмите кнопку **управление пакетами NuGet для решения**.</span><span class="sxs-lookup"><span data-stu-id="79627-137">In Solution Explorer, right-click hello **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="79627-138">Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="79627-138">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="79627-139">Нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="79627-139">Click **Install**, and accept hello terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="79627-140">Visual Studio загрузит, устанавливает и добавляет toohello ссылки [Azure концентратора событий служебной шины - пакет EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), с его зависимости.</span><span class="sxs-lookup"><span data-stu-id="79627-140">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="79627-141">Щелкните правой кнопкой мыши hello **получателя** проекта, нажмите кнопку **добавить**и нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="79627-141">Right-click hello **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="79627-142">Имя нового класса hello **SimpleEventProcessor**, а затем нажмите кнопку **добавить** toocreate hello класса.</span><span class="sxs-lookup"><span data-stu-id="79627-142">Name hello new class **SimpleEventProcessor**, and then click **Add** toocreate hello class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="79627-143">Добавьте следующие инструкции в начале hello файла SimpleEventProcessor.cs hello hello:</span><span class="sxs-lookup"><span data-stu-id="79627-143">Add hello following statements at hello top of hello SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="79627-144">Затем замените следующий код для основного текста hello класса hello hello:</span><span class="sxs-lookup"><span data-stu-id="79627-144">Then, substitute hello following code for hello body of hello class:</span></span>
    
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
    
  <span data-ttu-id="79627-145">Этот класс вызывается hello **EventProcessorHost** tooprocess события, получаемые от концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="79627-145">This class is called by hello **EventProcessorHost** tooprocess events received from hello event hub.</span></span> <span data-ttu-id="79627-146">Hello `SimpleEventProcessor` класс использует метод контрольного таймера tooperiodically вызов hello контрольной точки на hello **EventProcessorHost** контекста.</span><span class="sxs-lookup"><span data-stu-id="79627-146">hello `SimpleEventProcessor` class uses a stopwatch tooperiodically call hello checkpoint method on hello **EventProcessorHost** context.</span></span> <span data-ttu-id="79627-147">Такая обработка гарантирует, что при перезапуске приемника hello, теряет не более пяти минут обработки рабочих.</span><span class="sxs-lookup"><span data-stu-id="79627-147">This processing ensures that, if hello receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="79627-148">В hello **программы** класса, добавьте следующее hello `using` в начало файла hello hello инструкцию:</span><span class="sxs-lookup"><span data-stu-id="79627-148">In hello **Program** class, add hello following `using` statement at hello top of hello file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="79627-149">Затем замените hello `Main` метод в hello `Program` класса hello, следующий код, подставив имя концентратора событий hello и подключение уровня пространства имен hello строки, которые ранее сохранена и hello учетной записи хранилища и ключ, который был скопирован в hello предыдущих разделов.</span><span class="sxs-lookup"><span data-stu-id="79627-149">Then, replace hello `Main` method in hello `Program` class with hello following code, substituting hello event hub name and hello namespace-level connection string that you saved previously, and hello storage account and key that you copied in hello previous sections.</span></span> 
    
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

7. <span data-ttu-id="79627-150">Запустите программу hello и убедитесь, что отсутствуют ошибки.</span><span class="sxs-lookup"><span data-stu-id="79627-150">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="79627-151">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="79627-151">Congratulations!</span></span> <span data-ttu-id="79627-152">Теперь вы получили сообщений из концентратора событий с помощью hello узел обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="79627-152">You have now received messages from an event hub using hello Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="79627-153">В данном руководстве используется один экземпляр [EventProcessorHost][EventProcessorHost].</span><span class="sxs-lookup"><span data-stu-id="79627-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="79627-154">tooincrease пропускной способности, рекомендуется запустить несколько экземпляров [EventProcessorHost][EventProcessorHost], как показано в hello [масштаб обработку события] [масштаб обработку события] образца.</span><span class="sxs-lookup"><span data-stu-id="79627-154">tooincrease throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in hello [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="79627-155">В таких случаях hello различные экземпляры автоматически координировать друг с другом tooload баланс hello полученных событий.</span><span class="sxs-lookup"><span data-stu-id="79627-155">In those cases, hello various instances automatically coordinate with each other tooload balance hello received events.</span></span> <span data-ttu-id="79627-156">Если требуется несколько получателей tooeach процесс *все* hello событий, необходимо использовать hello **ConsumerGroup** концепции.</span><span class="sxs-lookup"><span data-stu-id="79627-156">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="79627-157">При получении события из разных компьютерах, бывает полезно toospecify имена для [EventProcessorHost] [ EventProcessorHost] экземпляров на основе машины hello (или ролей), в котором они развернуты.</span><span class="sxs-lookup"><span data-stu-id="79627-157">When receiving events from different machines, it might be useful toospecify names for [EventProcessorHost][EventProcessorHost] instances based on hello machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="79627-158">Дополнительные сведения об этих темах см. в разделе hello [Обзор концентраторов событий] [ Event Hubs overview] и hello [руководство по программированию концентраторов событий] [ Event Hubs Programming Guide] разделы.</span><span class="sxs-lookup"><span data-stu-id="79627-158">For more information about these topics, see hello [Event Hubs overview][Event Hubs overview] and hello [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="79627-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79627-159">Next steps</span></span>

<span data-ttu-id="79627-160">Теперь, когда вы создали рабочее приложение, которое создает концентратора событий и отправляет и получает данные, Дополнительные сведения, перейдя по адресу hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="79627-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting hello following links:</span></span>

* <span data-ttu-id="79627-161">[Узел обработчика событий][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="79627-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="79627-162">[Обзор концентраторов событий Azure][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="79627-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="79627-163">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="79627-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

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
