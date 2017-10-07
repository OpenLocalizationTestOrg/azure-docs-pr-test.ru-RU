---
title: "события aaaReceive из концентраторов событий Azure с помощью Java | Документы Microsoft"
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
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="0211b-103">Получение событий от концентраторов событий Azure с помощью Java</span><span class="sxs-lookup"><span data-stu-id="0211b-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="0211b-104">Введение</span><span class="sxs-lookup"><span data-stu-id="0211b-104">Introduction</span></span>
<span data-ttu-id="0211b-105">Концентраторы событий — это система высокой степенью масштабирования приема, можно принять миллионов событий в секунду, включение tooprocess приложения и анализировать hello значительные объемы данных, создаваемых подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="0211b-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="0211b-106">После сбора данных в концентраторах событий их можно преобразовать и сохранить с помощью любого поставщика аналитики в реальном времени или в кластере хранилища.</span><span class="sxs-lookup"><span data-stu-id="0211b-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="0211b-107">Дополнительные сведения см. в разделе hello [Обзор концентраторов событий][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="0211b-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="0211b-108">В этом учебнике показано как tooreceive событий в концентратор событий с помощью консольного приложения, написанного на языке Java.</span><span class="sxs-lookup"><span data-stu-id="0211b-108">This tutorial shows how tooreceive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0211b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0211b-109">Prerequisites</span></span>

<span data-ttu-id="0211b-110">Порядок toocomplete этого учебника нужен hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="0211b-110">In order toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="0211b-111">Среда разработки Java.</span><span class="sxs-lookup"><span data-stu-id="0211b-111">A Java development environment.</span></span> <span data-ttu-id="0211b-112">Для этого руководства предполагается использование среды [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="0211b-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="0211b-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="0211b-113">An active Azure account.</span></span> <br/><span data-ttu-id="0211b-114">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0211b-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="0211b-115">Дополнительные сведения см. в разделе <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Бесплатная пробная версия Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="0211b-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="0211b-116">Прием сообщений через EventProcessorHost в Java</span><span class="sxs-lookup"><span data-stu-id="0211b-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="0211b-117">**EventProcessorHost** — это класс Java, который упрощает прием событий от концентраторов событий путем управления постоянными контрольными точками и параллельно принимает сообщения от этих концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="0211b-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="0211b-118">С помощью класса EventProcessorHost можно разделить события между несколькими получателями, даже если они размещены на разных узлах.</span><span class="sxs-lookup"><span data-stu-id="0211b-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="0211b-119">В этом примере показано, как toouse EventProcessorHost для одного получателя.</span><span class="sxs-lookup"><span data-stu-id="0211b-119">This example shows how toouse EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="0211b-120">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="0211b-120">Create a storage account</span></span>
<span data-ttu-id="0211b-121">необходим toouse EventProcessorHost [учетной записи хранилища Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="0211b-121">toouse EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="0211b-122">Войдите на toohello [портал Azure][Azure portal]и нажмите кнопку **+ создать** hello левой части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="0211b-122">Log on toohello [Azure portal][Azure portal], and click **+ New** on hello left-hand side of hello screen.</span></span>
2. <span data-ttu-id="0211b-123">Щелкните **Хранилище**, а затем — **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="0211b-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="0211b-124">В hello **создать учетную запись хранения** колонки, введите имя для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="0211b-124">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="0211b-125">Выполните оставшиеся hello hello поля, выберите нужный регион и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="0211b-125">Complete hello rest of hello fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="0211b-126">Выберите только что созданный hello учетной записи хранилища и нажмите кнопку **управление ключами доступа**:</span><span class="sxs-lookup"><span data-stu-id="0211b-126">Click hello newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="0211b-127">Скопируйте hello первичного ключа tooa временный путь для доступа, toouse далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0211b-127">Copy hello primary access key tooa temporary location, toouse later in this tutorial.</span></span>

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a><span data-ttu-id="0211b-128">Создание проекта Java с помощью hello EventProcessor узла</span><span class="sxs-lookup"><span data-stu-id="0211b-128">Create a Java project using hello EventProcessor Host</span></span>
<span data-ttu-id="0211b-129">Hello клиентской библиотеки Java для концентраторов событий доступна для использования в проектах Maven из hello [центральный репозиторий Maven][Maven Package]и можно указывать hello объявления зависимостей внутри вашей Файл проекта maven:</span><span class="sxs-lookup"><span data-stu-id="0211b-129">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository][Maven Package], and can be referenced using hello following dependency declaration inside your Maven project file:</span></span>    

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

<span data-ttu-id="0211b-130">Для различных типов среды сборки c, можно явно загрузить файлы JAR hello последнего выпуска из hello [центральный репозиторий Maven] [ Maven Package] или из [hello на точки распространения выпуска GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="0211b-130">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository][Maven Package] or from [hello release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="0211b-131">Для следующих образец hello сначала необходимо создайте новый проект Maven для приложений консоли или оболочки в избранные среда разработки Java.</span><span class="sxs-lookup"><span data-stu-id="0211b-131">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="0211b-132">Класс Hello называется `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="0211b-132">hello class is called `ErrorNotificationHandler`.</span></span>     
   
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
2. <span data-ttu-id="0211b-133">Используйте hello следующий код toocreate новый класс с именем `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="0211b-133">Use hello following code toocreate a new class called `EventProcessor`.</span></span>
   
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
3. <span data-ttu-id="0211b-134">Создайте один дополнительные класс с именем `EventProcessorSample`, с использованием hello следующий код.</span><span class="sxs-lookup"><span data-stu-id="0211b-134">Create one more class called `EventProcessorSample`, using hello following code.</span></span>
   
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
   
            System.out.println("Press enter toostop");
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
4. <span data-ttu-id="0211b-135">Замените следующие поля со значениями hello использовались при создании учетные записи хранилища и концентратора событий hello hello.</span><span class="sxs-lookup"><span data-stu-id="0211b-135">Replace hello following fields with hello values used when you created hello event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="0211b-136">В данном учебнике используется один экземпляр EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="0211b-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="0211b-137">tooincrease пропускной способности, рекомендуется запускать несколько экземпляров EventProcessorHost, предпочтительно на разных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="0211b-137">tooincrease throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="0211b-138">Это также обеспечивает избыточность.</span><span class="sxs-lookup"><span data-stu-id="0211b-138">This provides redundancy as well.</span></span> <span data-ttu-id="0211b-139">В таких случаях приветствия различные экземпляры автоматически координации друг с другом в порядке tooload баланс hello полученные события.</span><span class="sxs-lookup"><span data-stu-id="0211b-139">In those cases, hello various instances automatically coordinate with each other in order tooload balance hello received events.</span></span> <span data-ttu-id="0211b-140">Если требуется несколько получателей tooeach процесс *все* hello событий, необходимо использовать hello **ConsumerGroup** концепции.</span><span class="sxs-lookup"><span data-stu-id="0211b-140">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="0211b-141">При получении события из разных компьютерах, бывает полезно toospecify имена для EventProcessorHost экземпляров на основе машины hello (или ролей), в котором они развернуты.</span><span class="sxs-lookup"><span data-stu-id="0211b-141">When receiving events from different machines, it might be useful toospecify names for EventProcessorHost instances based on hello machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0211b-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0211b-142">Next steps</span></span>
<span data-ttu-id="0211b-143">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="0211b-143">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="0211b-144">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="0211b-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="0211b-145">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="0211b-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="0211b-146">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="0211b-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
