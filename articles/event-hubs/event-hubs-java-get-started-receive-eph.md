---
title: "Получение событий от концентраторов событий Azure с помощью Java | Документация Майкрософт"
description: "Узнайте основные сведения о получении событий от концентраторов событий с помощью Java."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 3c1b455e6298367dc50f0943b58f6cf1e7f1c5fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="1ecee-103">Получение событий от концентраторов событий Azure с помощью Java</span><span class="sxs-lookup"><span data-stu-id="1ecee-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="1ecee-104">Введение</span><span class="sxs-lookup"><span data-stu-id="1ecee-104">Introduction</span></span>
<span data-ttu-id="1ecee-105">Концентраторы событий — это высокомасштабируемая система, способная принимать миллионы событий в секунду, благодаря которой приложения могут обрабатывать и анализировать большие объемы данных от подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="1ecee-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="1ecee-106">После сбора данных в концентраторах событий их можно преобразовать и сохранить с помощью любого поставщика аналитики в реальном времени или в кластере хранилища.</span><span class="sxs-lookup"><span data-stu-id="1ecee-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="1ecee-107">Дополнительные сведения см. в [обзоре концентраторов событий][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="1ecee-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="1ecee-108">В этом руководстве показано, как получать события из концентратора событий с помощью консольного приложения, написанного на языке Java.</span><span class="sxs-lookup"><span data-stu-id="1ecee-108">This tutorial shows how to receive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ecee-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1ecee-109">Prerequisites</span></span>

<span data-ttu-id="1ecee-110">Для работы с данным руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="1ecee-110">In order to complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="1ecee-111">Среда разработки Java.</span><span class="sxs-lookup"><span data-stu-id="1ecee-111">A Java development environment.</span></span> <span data-ttu-id="1ecee-112">Для этого руководства предполагается использование среды [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="1ecee-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="1ecee-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1ecee-113">An active Azure account.</span></span> <br/><span data-ttu-id="1ecee-114">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1ecee-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="1ecee-115">Дополнительные сведения см. в разделе <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Бесплатная пробная версия Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="1ecee-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="1ecee-116">Прием сообщений через EventProcessorHost в Java</span><span class="sxs-lookup"><span data-stu-id="1ecee-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="1ecee-117">**EventProcessorHost** — это класс Java, который упрощает прием событий от концентраторов событий путем управления постоянными контрольными точками и параллельно принимает сообщения от этих концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="1ecee-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="1ecee-118">С помощью класса EventProcessorHost можно разделить события между несколькими получателями, даже если они размещены на разных узлах.</span><span class="sxs-lookup"><span data-stu-id="1ecee-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="1ecee-119">В этом примере показано, как использовать EventProcessorHost для одного получателя.</span><span class="sxs-lookup"><span data-stu-id="1ecee-119">This example shows how to use EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="1ecee-120">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="1ecee-120">Create a storage account</span></span>
<span data-ttu-id="1ecee-121">Для использования класса EventProcessorHost необходимо настроить [учетную запись хранения Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="1ecee-121">To use EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="1ecee-122">Войдите на [портал Azure][Azure portal] и щелкните **+Создать** в левой части экрана.</span><span class="sxs-lookup"><span data-stu-id="1ecee-122">Log on to the [Azure portal][Azure portal], and click **+ New** on the left-hand side of the screen.</span></span>
2. <span data-ttu-id="1ecee-123">Щелкните **Хранилище**, а затем — **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="1ecee-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="1ecee-124">В колонке **Создание учетной записи хранилища** введите имя учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="1ecee-124">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="1ecee-125">Заполните остальные поля, выберите нужный регион и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1ecee-125">Complete the rest of the fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="1ecee-126">Выберите созданную учетную запись хранения и нажмите кнопку **Управление ключами доступа**.</span><span class="sxs-lookup"><span data-stu-id="1ecee-126">Click the newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="1ecee-127">Скопируйте первичный ключ доступа во временную папку, чтобы использовать позже в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="1ecee-127">Copy the primary access key to a temporary location, to use later in this tutorial.</span></span>

### <a name="create-a-java-project-using-the-eventprocessor-host"></a><span data-ttu-id="1ecee-128">Создание проекта Java с помощью EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="1ecee-128">Create a Java project using the EventProcessor Host</span></span>
<span data-ttu-id="1ecee-129">Клиентская библиотека Java для концентраторов событий доступна для использования в проектах из [центрального репозитория Maven][Maven Package]. Ссылаться на нее можно, используя следующее объявление зависимости в файле проекта Maven:</span><span class="sxs-lookup"><span data-stu-id="1ecee-129">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository][Maven Package], and can be referenced using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

<span data-ttu-id="1ecee-130">Для различных типов сред сборки можно явно получить последние выпущенные JAR-файлы из [центрального репозитория Maven][Maven Package] или из [точки распространения выпусков на GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="1ecee-130">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository][Maven Package] or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="1ecee-131">Следующий пример сначала создает новый проект Maven для приложения консоли или оболочки в избранной среде разработки Java.</span><span class="sxs-lookup"><span data-stu-id="1ecee-131">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="1ecee-132">Класс называется `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="1ecee-132">The class is called `ErrorNotificationHandler`.</span></span>     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="1ecee-133">Создайте новый класс с именем `EventProcessor`с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="1ecee-133">Use the following code to create a new class called `EventProcessor`.</span></span>
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="1ecee-134">Создайте еще один класс с именем `EventProcessorSample` с помощью следующего кода.</span><span class="sxs-lookup"><span data-stu-id="1ecee-134">Create one more class called `EventProcessorSample`, using the following code.</span></span>
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter to stop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="1ecee-135">Замените значения в следующих полях значениями, которые использовались при создании концентратора событий и учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="1ecee-135">Replace the following fields with the values used when you created the event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="1ecee-136">В данном учебнике используется один экземпляр EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="1ecee-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="1ecee-137">Чтобы увеличить пропускную способность, рекомендуется запустить несколько экземпляров EventProcessorHost (желательно на отдельных компьютерах).</span><span class="sxs-lookup"><span data-stu-id="1ecee-137">To increase throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="1ecee-138">Это также обеспечивает избыточность.</span><span class="sxs-lookup"><span data-stu-id="1ecee-138">This provides redundancy as well.</span></span> <span data-ttu-id="1ecee-139">В этом случае различные экземпляры автоматически координируются друг с другом для распределения нагрузки полученных событий.</span><span class="sxs-lookup"><span data-stu-id="1ecee-139">In those cases, the various instances automatically coordinate with each other in order to load balance the received events.</span></span> <span data-ttu-id="1ecee-140">Если каждый из нескольких получателей должен обрабатывать *все* события, то необходимо использовать понятие **ConsumerGroup** .</span><span class="sxs-lookup"><span data-stu-id="1ecee-140">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="1ecee-141">При получении события от разных компьютеров может оказаться полезным указать имена экземпляров EventProcessorHost в компьютерах (или ролях), где они развернуты.</span><span class="sxs-lookup"><span data-stu-id="1ecee-141">When receiving events from different machines, it might be useful to specify names for EventProcessorHost instances based on the machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1ecee-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ecee-142">Next steps</span></span>
<span data-ttu-id="1ecee-143">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="1ecee-143">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="1ecee-144">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="1ecee-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="1ecee-145">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="1ecee-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="1ecee-146">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="1ecee-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
