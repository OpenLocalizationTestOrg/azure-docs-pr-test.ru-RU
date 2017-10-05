---
title: "Отправка событий в концентраторы событий Azure с помощью .NET Standard | Документация Майкрософт"
description: "Узнайте, как начать работу с отправкой событий в концентраторы событий на платформе .NET Standard."
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
ms.openlocfilehash: 8af9d70965c1c9ad8c49b7d2bb04244fc207058d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a><span data-ttu-id="9a653-103">Приступая к отправке событий в концентраторы событий Azure на платформе .NET Standard</span><span class="sxs-lookup"><span data-stu-id="9a653-103">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="9a653-104">Этот пример можно найти на сайте [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="9a653-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="9a653-105">В этом руководстве показано, как написать консольное приложение для .NET Core, которое отправляет набор событий в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="9a653-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span></span> <span data-ttu-id="9a653-106">Вы можете запустить решение [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) "как есть", заменив строки `EhConnectionString` и `EhEntityPath` своими значениями для концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="9a653-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="9a653-107">Или следуйте инструкциям этого руководства, чтобы создать собственное решение.</span><span class="sxs-lookup"><span data-stu-id="9a653-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a653-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9a653-108">Prerequisites</span></span>

* <span data-ttu-id="9a653-109">[Microsoft Visual Studio 2015 или Microsoft Visual Studio 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="9a653-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="9a653-110">В примерах в этом руководстве используется Visual Studio 2017, но также поддерживается Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9a653-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="9a653-111">[Инструментарий Visual Studio 2015 или Visual Studio 2017 для .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="9a653-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="9a653-112">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="9a653-112">An Azure subscription.</span></span>
* <span data-ttu-id="9a653-113">Пространство имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="9a653-113">An event hub namespace.</span></span>

<span data-ttu-id="9a653-114">Для отправки сообщений в концентратор событий мы напишем консольное приложение C# в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9a653-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="9a653-115">Создание пространства имен концентраторов событий и концентратора событий</span><span class="sxs-lookup"><span data-stu-id="9a653-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="9a653-116">Первым шагом является использование [портала Azure](https://portal.azure.com) для создания пространства имен концентраторов событий и получение учетных данных управления, необходимых приложению для взаимодействия с концентратором событий.</span><span class="sxs-lookup"><span data-stu-id="9a653-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="9a653-117">Чтобы создать пространство имен и концентратор событий, выполните процедуру, описанную в [этой статье](event-hubs-create.md), а затем перейдите к следующим действиям.</span><span class="sxs-lookup"><span data-stu-id="9a653-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="9a653-118">Создание консольного приложение</span><span class="sxs-lookup"><span data-stu-id="9a653-118">Create a console application</span></span>

<span data-ttu-id="9a653-119">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9a653-119">Start Visual Studio.</span></span> <span data-ttu-id="9a653-120">В меню **Файл** выберите команду **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="9a653-120">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="9a653-121">Создайте консольное приложение .NET Core.</span><span class="sxs-lookup"><span data-stu-id="9a653-121">Create a .NET Core console application.</span></span>

![Новый проект][1]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="9a653-123">Добавление пакета NuGet для концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="9a653-123">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="9a653-124">Добавьте пакет NuGet библиотеки .NET Standard [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) в проект, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="9a653-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package to your project by following these steps:</span></span> 

1. <span data-ttu-id="9a653-125">Щелкните созданный проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9a653-125">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="9a653-126">Откройте вкладку **Обзор**, а затем выполните поиск по фразе Microsoft.Azure.EventHubs и выберите пакет **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="9a653-126">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="9a653-127">Щелкните **Установить** , чтобы выполнить установку, а затем закройте это диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="9a653-127">Click **Install** to complete the installation, then close this dialog box.</span></span>

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a><span data-ttu-id="9a653-128">Написание кода для отправки сообщений в концентратор событий</span><span class="sxs-lookup"><span data-stu-id="9a653-128">Write some code to send messages to the event hub</span></span>

1. <span data-ttu-id="9a653-129">Добавьте следующие операторы `using` в начало файла program.cs.</span><span class="sxs-lookup"><span data-stu-id="9a653-129">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="9a653-130">Добавьте в класс `Program` константы для строки подключения концентраторов событий и пути сущности (имя отдельного концентратора событий).</span><span class="sxs-lookup"><span data-stu-id="9a653-130">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="9a653-131">Замените заполнители в скобках соответствующими значениями, которые были получены при создании концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="9a653-131">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="9a653-132">Добавьте новый метод с именем `MainAsync` в класс `Program`, как показано далее:</span><span class="sxs-lookup"><span data-stu-id="9a653-132">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
        // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
        // we are using the connection string from the namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="9a653-133">Добавьте новый метод с именем `SendMessagesToEventHub` в класс `Program`, как показано далее:</span><span class="sxs-lookup"><span data-stu-id="9a653-133">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages to the event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. <span data-ttu-id="9a653-134">В метод `Main` в классе `Program` добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="9a653-134">Add the following code to the `Main` method in the `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="9a653-135">Вот как будет выглядеть файл Program.cs.</span><span class="sxs-lookup"><span data-stu-id="9a653-135">Here is what your Program.cs should look like.</span></span>

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
                // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
                // we are using the connection string from the namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER to exit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages to the event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. <span data-ttu-id="9a653-136">Запустите программу и убедитесь в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="9a653-136">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="9a653-137">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="9a653-137">Congratulations!</span></span> <span data-ttu-id="9a653-138">Теперь вы можете отправлять сообщения в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="9a653-138">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a653-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a653-139">Next steps</span></span>
<span data-ttu-id="9a653-140">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="9a653-140">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="9a653-141">Основные сведения о получении сообщений с помощью узла EventProcessorHost в .NET Standard</span><span class="sxs-lookup"><span data-stu-id="9a653-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="9a653-142">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="9a653-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="9a653-143">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="9a653-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="9a653-144">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="9a653-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
