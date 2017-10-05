---
title: "Получение событий от концентраторов событий Azure с помощью платформы .NET Framework | Документация Майкрософт"
description: "Приведенные в этом руководстве инструкции помогут настроить получение событий от концентраторов событий Azure с помощью платформы .NET Framework."
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
ms.openlocfilehash: 581af52b3264b1a7c57315c65d5385a372308c27
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="58476-103">Получение событий от концентраторов событий Azure с помощью платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="58476-103">Receive events from Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="58476-104">Введение</span><span class="sxs-lookup"><span data-stu-id="58476-104">Introduction</span></span>

<span data-ttu-id="58476-105">Концентраторы событий — это служба, которая обрабатывает большие объемы данных телеметрии о событиях, поступающих от подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="58476-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="58476-106">После сбора дынных в концентраторах событий их можно сохранить с помощью кластера хранилища или преобразовать с помощью поставщика аналитики в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="58476-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="58476-107">Эта возможность сбора и обработки большого объема данных о событиях является ключевым компонентом в современных архитектурах приложений, включая "Интернет вещей".</span><span class="sxs-lookup"><span data-stu-id="58476-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="58476-108">В этом руководстве показано, как создать консольное приложение .NET Framework для получения сообщений из концентратора событий с помощью узла **[EventProcessorHost][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="58476-108">This tutorial shows how to write a .NET Framework console application that receives messages from an event hub using the **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="58476-109">Сведения об отправке событий с помощью платформы .NET Framework см. в статье [Отправка событий в концентраторы событий Azure с помощью платформы .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) или выберите соответствующий язык в содержании статьи слева.</span><span class="sxs-lookup"><span data-stu-id="58476-109">To send events using the .NET Framework, see the [Send events to Azure Event Hubs using the .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click the appropriate sending language in the left-hand table of contents.</span></span>

<span data-ttu-id="58476-110">[EventProcessorHost][EventProcessorHost] представляет собой класс .NET, который упрощает прием событий от концентраторов событий путем управления постоянными контрольными точками и одновременно принимает сообщения от этих концентраторов событий в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="58476-110">The [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="58476-111">С помощью класса [EventProcessorHost][Event Processor Host] можно разделить события между несколькими получателями даже в том случае, если они размещены в разных узлах.</span><span class="sxs-lookup"><span data-stu-id="58476-111">Using the [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="58476-112">В этом примере показано, как использовать [EventProcessorHost][EventProcessorHost] для одного получателя.</span><span class="sxs-lookup"><span data-stu-id="58476-112">This example shows how to use the [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="58476-113">В примере [развертывания обработки событий][Scale out Event Processing with Event Hubs] показано, как использовать [EventProcessorHost][EventProcessorHost] с несколькими получателями.</span><span class="sxs-lookup"><span data-stu-id="58476-113">The [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how to use the [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58476-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="58476-114">Prerequisites</span></span>

<span data-ttu-id="58476-115">Для работы с данным руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="58476-115">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="58476-116">[Microsoft Visual Studio 2015 или более поздней версии](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="58476-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="58476-117">На приведенных в этом руководстве снимках экрана используется Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="58476-117">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="58476-118">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="58476-118">An active Azure account.</span></span> <span data-ttu-id="58476-119">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="58476-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="58476-120">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="58476-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="58476-121">Создание пространства имен концентраторов событий и концентратора событий</span><span class="sxs-lookup"><span data-stu-id="58476-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="58476-122">Первым шагом является использование [портала Azure](https://portal.azure.com) для создания пространства имен типа концентраторов событий и получение учетных данных управления, необходимых приложению для взаимодействия с концентратором событий.</span><span class="sxs-lookup"><span data-stu-id="58476-122">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="58476-123">Чтобы создать пространство имен и концентратор событий, выполните процедуру, описанную в [этой статье](event-hubs-create.md), а затем перейдите к следующим действиям в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="58476-123">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="58476-124">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="58476-124">Create an Azure Storage account</span></span>

<span data-ttu-id="58476-125">Для использования класса [EventProcessorHost][EventProcessorHost] необходимо настроить [учетную запись хранения Azure][Azure Storage account].</span><span class="sxs-lookup"><span data-stu-id="58476-125">To use the [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="58476-126">Войдите на [портал Azure][Azure portal] и щелкните **Создать** в левой верхней части экрана.</span><span class="sxs-lookup"><span data-stu-id="58476-126">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
2. <span data-ttu-id="58476-127">Щелкните **Хранилище**, а затем — **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="58476-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="58476-128">В колонке **Создание учетной записи хранилища** введите имя учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="58476-128">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="58476-129">Выберите подписку Azure, группу ресурсов и расположение для создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="58476-129">Choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="58476-130">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="58476-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="58476-131">В списке учетных записей хранения выберите только что созданную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="58476-131">In the list of storage accounts, click the newly created storage account.</span></span>
5. <span data-ttu-id="58476-132">В колонке учетной записи хранения выберите **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="58476-132">In the storage account blade, click **Access keys**.</span></span> <span data-ttu-id="58476-133">Скопируйте значение **key1** , чтобы использовать позже в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="58476-133">Copy the value of **key1** to use later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="58476-134">Создание консольного приложения получателя</span><span class="sxs-lookup"><span data-stu-id="58476-134">Create a receiver console application</span></span>

1. <span data-ttu-id="58476-135">Создайте в Visual Studio новый проект Visual C# для классических приложений с помощью шаблона проекта **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="58476-135">In Visual Studio, create a new Visual C# Desktop App project using the **Console  Application** project template.</span></span> <span data-ttu-id="58476-136">Присвойте проекту имя **Получатель**.</span><span class="sxs-lookup"><span data-stu-id="58476-136">Name the project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="58476-137">В обозревателе решений щелкните правой кнопкой мыши проект **Получатель** и выберите пункт **Управление пакетами NuGet для решения**.</span><span class="sxs-lookup"><span data-stu-id="58476-137">In Solution Explorer, right-click the **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="58476-138">Щелкните вкладку **Обзор** и выполните поиск `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="58476-138">Click the **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="58476-139">Щелкните **Установить**и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="58476-139">Click **Install**, and accept the terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="58476-140">Visual Studio скачает, установит и добавит ссылку на [пакет концентратора событий служебной шины Azure EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost)со всеми его зависимостями.</span><span class="sxs-lookup"><span data-stu-id="58476-140">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="58476-141">Щелкните правой кнопкой мыши проект **Получатель**, а затем выберите пункты **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="58476-141">Right-click the **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="58476-142">Присвойте новому классу имя **SimpleEventProcessor**, а затем нажмите кнопку **Добавить**, чтобы создать класс.</span><span class="sxs-lookup"><span data-stu-id="58476-142">Name the new class **SimpleEventProcessor**, and then click **Add** to create the class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="58476-143">Добавьте в начало файла SimpleEventProcessor.cs следующие инструкции:</span><span class="sxs-lookup"><span data-stu-id="58476-143">Add the following statements at the top of the SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="58476-144">Затем замените следующий код текстом класса:</span><span class="sxs-lookup"><span data-stu-id="58476-144">Then, substitute the following code for the body of the class:</span></span>
    
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
    
  <span data-ttu-id="58476-145">Этот класс вызывается из **EventProcessorHost** для обработки событий, полученных от концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="58476-145">This class is called by the **EventProcessorHost** to process events received from the event hub.</span></span> <span data-ttu-id="58476-146">В классе `SimpleEventProcessor` используется контрольный таймер для периодического вызова метода контрольных точек в контексте **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="58476-146">The `SimpleEventProcessor` class uses a stopwatch to periodically call the checkpoint method on the **EventProcessorHost** context.</span></span> <span data-ttu-id="58476-147">Благодаря этому в случае перезагрузки получателя будет потеряно не более пяти минут обработки.</span><span class="sxs-lookup"><span data-stu-id="58476-147">This processing ensures that, if the receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="58476-148">Добавьте в класс **Program** в начале файла следующую инструкцию `using`.</span><span class="sxs-lookup"><span data-stu-id="58476-148">In the **Program** class, add the following `using` statement at the top of the file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="58476-149">Затем измените метод `Main` в классе `Program` следующим кодом. При этом укажите имя концентратора событий и сохраненную ранее строку подключения уровня пространства имен, а также учетную запись хранения и ключ, которые вы скопировали в предыдущих разделах.</span><span class="sxs-lookup"><span data-stu-id="58476-149">Then, replace the `Main` method in the `Program` class with the following code, substituting the event hub name and the namespace-level connection string that you saved previously, and the storage account and key that you copied in the previous sections.</span></span> 
    
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
    
    Console.WriteLine("Receiving. Press enter key to stop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. <span data-ttu-id="58476-150">Запустите программу и убедитесь в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="58476-150">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="58476-151">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="58476-151">Congratulations!</span></span> <span data-ttu-id="58476-152">Теперь вы можете получать сообщения из концентратора событий с помощью узла EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="58476-152">You have now received messages from an event hub using the Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="58476-153">В данном руководстве используется один экземпляр [EventProcessorHost][EventProcessorHost].</span><span class="sxs-lookup"><span data-stu-id="58476-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="58476-154">Чтобы увеличить пропускную способность, мы советуем запустить несколько экземпляров [EventProcessorHost][EventProcessorHost], как показано в примере [обработки масштабируемого события][обработка масштабируемого события].</span><span class="sxs-lookup"><span data-stu-id="58476-154">To increase throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in the [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="58476-155">В этом случае различные экземпляры автоматически координируются друг с другом для распределения нагрузки полученных событий.</span><span class="sxs-lookup"><span data-stu-id="58476-155">In those cases, the various instances automatically coordinate with each other to load balance the received events.</span></span> <span data-ttu-id="58476-156">Если каждый из нескольких получателей должен обрабатывать *все* события, то необходимо использовать понятие **ConsumerGroup** .</span><span class="sxs-lookup"><span data-stu-id="58476-156">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="58476-157">При получении события от разных компьютеров может оказаться полезным указать имена экземпляров [EventProcessorHost][EventProcessorHost] в компьютерах (или ролях), где они развернуты.</span><span class="sxs-lookup"><span data-stu-id="58476-157">When receiving events from different machines, it might be useful to specify names for [EventProcessorHost][EventProcessorHost] instances based on the machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="58476-158">См. дополнительные сведения о [концентраторах событий Azure][Event Hubs overview] и [программировании концентраторов событий][Event Hubs Programming Guide].</span><span class="sxs-lookup"><span data-stu-id="58476-158">For more information about these topics, see the [Event Hubs overview][Event Hubs overview] and the [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="58476-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58476-159">Next steps</span></span>

<span data-ttu-id="58476-160">Теперь у вас есть рабочее приложение, которое создает концентратор событий, а также отправляет и получает данные. Дополнительные сведения см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="58476-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting the following links:</span></span>

* <span data-ttu-id="58476-161">[Узел обработчика событий][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="58476-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="58476-162">[Обзор концентраторов событий Azure][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="58476-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="58476-163">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="58476-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

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
