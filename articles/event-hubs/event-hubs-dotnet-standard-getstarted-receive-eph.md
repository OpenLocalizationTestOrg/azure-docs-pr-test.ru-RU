---
title: "события aaaReceive из концентраторов событий Azure с помощью .NET Standard | Документы Microsoft"
description: "Начать получение сообщений с использованием hello EventProcessorHost в .NET Standard"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="725d3-103">Начать получение сообщений с использованием hello узел обработчика событий в .NET Standard</span><span class="sxs-lookup"><span data-stu-id="725d3-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="725d3-104">Этот пример можно найти на сайте [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="725d3-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="725d3-105">В этом учебнике показано, как toowrite .NET Core консольного приложения, которая получает сообщения из концентратора событий с помощью **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="725d3-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="725d3-106">Можно запустить hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) решения,-замена строк hello собственными значениями события концентратора и хранения данных учетной записи.</span><span class="sxs-lookup"><span data-stu-id="725d3-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="725d3-107">Или же можно воспользоваться hello шагов в этот учебник toocreate свои собственные.</span><span class="sxs-lookup"><span data-stu-id="725d3-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="725d3-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="725d3-108">Prerequisites</span></span>

* <span data-ttu-id="725d3-109">[Microsoft Visual Studio 2015 или Microsoft Visual Studio 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="725d3-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="725d3-110">также поддерживается Hello примерах данного учебника используйте Visual Studio 2017 г., но Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="725d3-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="725d3-111">[Инструментарий Visual Studio 2015 или Visual Studio 2017 для .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="725d3-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="725d3-112">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="725d3-112">An Azure subscription.</span></span>
* <span data-ttu-id="725d3-113">Пространство имен концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="725d3-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="725d3-114">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="725d3-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="725d3-115">Создание пространства имен концентраторов событий и концентратора событий</span><span class="sxs-lookup"><span data-stu-id="725d3-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="725d3-116">Hello первым шагом является toouse hello [портал Azure](https://portal.azure.com) toocreate пространство имен для hello концентраторов событий введите и получить учетные данные управления, необходимые приложению toocommunicate с концентратором событий hello hello.</span><span class="sxs-lookup"><span data-stu-id="725d3-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="725d3-117">toocreate пространство имен и концентратора событий, выполните процедуру hello в [в этой статье](event-hubs-create.md)и продолжите hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="725d3-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="725d3-118">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="725d3-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="725d3-119">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="725d3-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="725d3-120">В области навигации слева hello hello портала щелкните **New**, нажмите кнопку **хранилища**и нажмите кнопку **учетной записи хранилища**.</span><span class="sxs-lookup"><span data-stu-id="725d3-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="725d3-121">Заполните поля hello в колонке учетной записи хранилища hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="725d3-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![Создать учетную запись хранения][1]

4. <span data-ttu-id="725d3-123">После появления hello **развертывания успешно** сообщение, щелкните имя hello hello новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="725d3-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="725d3-124">В hello **Essentials** колонка, щелкните **большие двоичные объекты**.</span><span class="sxs-lookup"><span data-stu-id="725d3-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="725d3-125">Здравствуйте, когда **службе BLOB-объектов** открывается колонка, щелкните **+ контейнер** вверху hello.</span><span class="sxs-lookup"><span data-stu-id="725d3-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="725d3-126">Присвойте имя контейнера hello, а затем закройте hello **службе BLOB-объектов** колонку.</span><span class="sxs-lookup"><span data-stu-id="725d3-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="725d3-127">Нажмите кнопку **ключи доступа** в hello левой колонке и скопируйте hello имя контейнера хранилища hello, hello учетной записи хранилища и значение hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="725d3-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="725d3-128">Сохраните эти значения tooNotepad или других временное расположение.</span><span class="sxs-lookup"><span data-stu-id="725d3-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="725d3-129">Создание консольного приложение</span><span class="sxs-lookup"><span data-stu-id="725d3-129">Create a console application</span></span>

<span data-ttu-id="725d3-130">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="725d3-130">Start Visual Studio.</span></span> <span data-ttu-id="725d3-131">Из hello **файл** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="725d3-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="725d3-132">Создайте консольное приложение .NET Core.</span><span class="sxs-lookup"><span data-stu-id="725d3-132">Create a .NET Core console application.</span></span>

![Новый проект][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="725d3-134">Добавьте пакет NuGet концентраторов событий hello</span><span class="sxs-lookup"><span data-stu-id="725d3-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="725d3-135">Добавить hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) и [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard проекта библиотеки NuGet пакеты tooyour, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="725d3-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="725d3-136">Щелкните правой кнопкой мыши только что созданный hello проекта и выберите **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="725d3-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="725d3-137">Нажмите кнопку hello **Обзор** , а затем поиск «Microsoft.Azure.EventHubs» и выберите hello **Microsoft.Azure.EventHubs** пакета.</span><span class="sxs-lookup"><span data-stu-id="725d3-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="725d3-138">Нажмите кнопку **установить** toocomplete hello установки, а затем закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="725d3-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="725d3-139">Повторите шаги 1 и 2, а также установить hello **Microsoft.Azure.EventHubs.Processor** пакета.</span><span class="sxs-lookup"><span data-stu-id="725d3-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="725d3-140">Реализуйте интерфейс IEventProcessor hello</span><span class="sxs-lookup"><span data-stu-id="725d3-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="725d3-141">В обозревателе решений щелкните правой кнопкой мыши проект hello, нажмите кнопку **добавить**, а затем нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="725d3-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="725d3-142">Имя нового класса hello **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="725d3-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="725d3-143">Откройте файл SimpleEventProcessor.cs hello и добавьте следующее hello `using` инструкций toohello вверху файла hello.</span><span class="sxs-lookup"><span data-stu-id="725d3-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="725d3-144">Реализуйте hello `IEventProcessor` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="725d3-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="725d3-145">Замените все содержимое hello hello `SimpleEventProcessor` класса hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="725d3-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="725d3-146">Метод главной консоли, который использует класс tooreceive hello SimpleEventProcessor сообщения</span><span class="sxs-lookup"><span data-stu-id="725d3-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="725d3-147">Добавьте следующее hello `using` инструкций toohello верхней части файла Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="725d3-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="725d3-148">Добавить toohello константы `Program` класс для строки подключения концентратора событий hello, имя концентратора событий, имя контейнера в учетной записи хранения, имя учетной записи хранения и ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="725d3-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="725d3-149">Добавьте hello после кода, заменив заполнители hello и соответствующие им значения.</span><span class="sxs-lookup"><span data-stu-id="725d3-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="725d3-150">Добавьте новый метод с именем `MainAsync` toohello `Program` класса, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="725d3-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="725d3-151">Добавьте следующие строки кода toohello hello `Main` метод:</span><span class="sxs-lookup"><span data-stu-id="725d3-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="725d3-152">Вот как будет выглядеть файл Program.cs.</span><span class="sxs-lookup"><span data-stu-id="725d3-152">Here is what your Program.cs file should look like:</span></span>

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="725d3-153">Запустите программу hello и убедитесь, что отсутствуют ошибки.</span><span class="sxs-lookup"><span data-stu-id="725d3-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="725d3-154">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="725d3-154">Congratulations!</span></span> <span data-ttu-id="725d3-155">Теперь Получено сообщений из концентратора событий с помощью hello узел обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="725d3-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="725d3-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="725d3-156">Next steps</span></span>
<span data-ttu-id="725d3-157">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="725d3-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="725d3-158">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="725d3-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="725d3-159">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="725d3-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="725d3-160">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="725d3-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
