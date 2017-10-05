---
title: "Получение событий от концентраторов событий Azure с помощью .NET Standard | Документация Майкрософт"
description: "Основные сведения о получении сообщений с помощью узла EventProcessorHost в .NET Standard"
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
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="7ded5-103">Основные сведения о получении сообщений с помощью узла EventProcessorHost в .NET Standard</span><span class="sxs-lookup"><span data-stu-id="7ded5-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="7ded5-104">Этот пример можно найти на сайте [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="7ded5-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="7ded5-105">В этом руководстве показано, как создать консольное приложение .NET Core для получения сообщений из концентратора событий с помощью узла **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="7ded5-106">Вы можете запустить решение [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) "как есть", заменив соответствующие строки своими значениями для концентратора событий и учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7ded5-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="7ded5-107">Или следуйте инструкциям этого руководства, чтобы создать собственное решение.</span><span class="sxs-lookup"><span data-stu-id="7ded5-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ded5-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7ded5-108">Prerequisites</span></span>

* <span data-ttu-id="7ded5-109">[Microsoft Visual Studio 2015 или Microsoft Visual Studio 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="7ded5-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="7ded5-110">В примерах в этом руководстве используется Visual Studio 2017, но также поддерживается Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7ded5-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="7ded5-111">[Инструментарий Visual Studio 2015 или Visual Studio 2017 для .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="7ded5-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="7ded5-112">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="7ded5-112">An Azure subscription.</span></span>
* <span data-ttu-id="7ded5-113">Пространство имен концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="7ded5-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="7ded5-114">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="7ded5-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="7ded5-115">Создание пространства имен концентраторов событий и концентратора событий</span><span class="sxs-lookup"><span data-stu-id="7ded5-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="7ded5-116">Первым шагом является использование [портала Azure](https://portal.azure.com) для создания пространства имен концентраторов событий и получение учетных данных управления, необходимых приложению для взаимодействия с концентратором событий.</span><span class="sxs-lookup"><span data-stu-id="7ded5-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="7ded5-117">Чтобы создать пространство имен и концентратор событий, выполните процедуру, описанную в [этой статье](event-hubs-create.md), а затем перейдите к следующим действиям.</span><span class="sxs-lookup"><span data-stu-id="7ded5-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="7ded5-118">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="7ded5-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="7ded5-119">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ded5-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="7ded5-120">В области навигации слева на странице портала щелкните **Создать** > **Хранилище** > **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="7ded5-121">Заполните поля в колонке учетной записи хранения и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![Создать учетную запись хранения][1]

4. <span data-ttu-id="7ded5-123">Получив сообщение об **успешном выполнении развертывания**, щелкните имя новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7ded5-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="7ded5-124">В колонке **Основные компоненты** щелкните **BLOB-объекты**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="7ded5-125">В верхней части открывшейся колонки **Служба BLOB-объектов** щелкните **+ Container** (+ Контейнер).</span><span class="sxs-lookup"><span data-stu-id="7ded5-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="7ded5-126">Присвойте контейнеру имя, а затем закройте колонку **Служба BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="7ded5-127">Щелкните элемент **Ключи доступа** в колонке слева и скопируйте имя контейнера хранения, а также значение **key1**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="7ded5-128">Сохраните на время эти значения в Блокноте или любом другом месте.</span><span class="sxs-lookup"><span data-stu-id="7ded5-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="7ded5-129">Создание консольного приложение</span><span class="sxs-lookup"><span data-stu-id="7ded5-129">Create a console application</span></span>

<span data-ttu-id="7ded5-130">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ded5-130">Start Visual Studio.</span></span> <span data-ttu-id="7ded5-131">В меню **Файл** выберите команду **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="7ded5-132">Создайте консольное приложение .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7ded5-132">Create a .NET Core console application.</span></span>

![Новый проект][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="7ded5-134">Добавление пакета NuGet для концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="7ded5-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="7ded5-135">Добавьте пакеты NuGet библиотеки .NET Standard [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) и [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) в проект, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="7ded5-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="7ded5-136">Щелкните созданный проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="7ded5-137">Откройте вкладку **Обзор**, а затем выполните поиск по фразе Microsoft.Azure.EventHubs и выберите пакет **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="7ded5-138">Щелкните **Установить** , чтобы выполнить установку, а затем закройте это диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="7ded5-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="7ded5-139">Повторите шаги 1 и 2 и установите пакет **Microsoft.Azure.EventHubs.Processor**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="7ded5-140">Реализация интерфейса IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="7ded5-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="7ded5-141">В обозревателе решений щелкните правой кнопкой мыши проект, выберите **Добавить**, а затем щелкните **Класс**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="7ded5-142">Назовите новый класс **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="7ded5-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="7ded5-143">Откройте файл SimpleEventProcessor.cs и добавьте в его начало следующие операторы `using`.</span><span class="sxs-lookup"><span data-stu-id="7ded5-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="7ded5-144">Реализуйте интерфейс `IEventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="7ded5-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="7ded5-145">Замените все содержимое класса `SimpleEventProcessor` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="7ded5-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="7ded5-146">Написание метода главной консоли, использующего класс SimpleEventProcessor для получения сообщений</span><span class="sxs-lookup"><span data-stu-id="7ded5-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="7ded5-147">Добавьте следующие операторы `using` в начало файла program.cs.</span><span class="sxs-lookup"><span data-stu-id="7ded5-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="7ded5-148">Добавьте в класс `Program` константы для строки подключения концентраторов событий, имени концентратора событий, имени контейнера учетной записи хранения, имени учетной записи хранения и ключа учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7ded5-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="7ded5-149">Добавьте следующий код, заменив заполнители соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="7ded5-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="7ded5-150">Добавьте новый метод с именем `MainAsync` в класс `Program`, как показано далее:</span><span class="sxs-lookup"><span data-stu-id="7ded5-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

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

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="7ded5-151">Добавьте в метод `Main` следующую строку кода:</span><span class="sxs-lookup"><span data-stu-id="7ded5-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="7ded5-152">Вот как будет выглядеть файл Program.cs.</span><span class="sxs-lookup"><span data-stu-id="7ded5-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="7ded5-153">Запустите программу и убедитесь в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="7ded5-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="7ded5-154">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="7ded5-154">Congratulations!</span></span> <span data-ttu-id="7ded5-155">Теперь вы можете получать сообщения из концентратора событий с помощью узла EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="7ded5-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ded5-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ded5-156">Next steps</span></span>
<span data-ttu-id="7ded5-157">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="7ded5-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="7ded5-158">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="7ded5-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="7ded5-159">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="7ded5-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="7ded5-160">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="7ded5-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
