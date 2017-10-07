---
title: "tooAzure aaaSend событий с помощью .NET Standard концентраторов событий | Документы Microsoft"
description: "Начало работы отправки tooEvent концентраторов событий в .NET Standard"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="ea306-103">Начало работы отправки сообщений tooAzure концентраторов событий в .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ea306-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="ea306-104">Этот пример можно найти на сайте [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="ea306-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="ea306-105">В этом учебнике показано, как toowrite .NET Core консольное приложение, которое отправляет набор сообщений tooan концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="ea306-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="ea306-106">Можно запустить hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) решения,-заменив hello `EhConnectionString` и `EhEntityPath` строки собственными значениями концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="ea306-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="ea306-107">Или же можно воспользоваться hello шагов в этот учебник toocreate свои собственные.</span><span class="sxs-lookup"><span data-stu-id="ea306-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea306-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea306-108">Prerequisites</span></span>

* <span data-ttu-id="ea306-109">[Microsoft Visual Studio 2015 или Microsoft Visual Studio 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ea306-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="ea306-110">также поддерживается Hello примерах данного учебника используйте Visual Studio 2017 г., но Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ea306-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="ea306-111">[Инструментарий Visual Studio 2015 или Visual Studio 2017 для .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="ea306-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="ea306-112">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="ea306-112">An Azure subscription.</span></span>
* <span data-ttu-id="ea306-113">Пространство имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="ea306-113">An event hub namespace.</span></span>

<span data-ttu-id="ea306-114">концентратор событий tooan toosend сообщения, мы будем использовать Visual Studio toowrite консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="ea306-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="ea306-115">Создание пространства имен концентраторов событий и концентратора событий</span><span class="sxs-lookup"><span data-stu-id="ea306-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="ea306-116">Hello первым шагом является toouse hello [портал Azure](https://portal.azure.com) toocreate пространство имен для типа концентратора событий hello и получить учетные данные управления, необходимые приложению toocommunicate с концентратором событий hello hello.</span><span class="sxs-lookup"><span data-stu-id="ea306-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="ea306-117">toocreate пространства имен и концентратора событий, выполните процедуру hello в [в этой статье](event-hubs-create.md)и продолжите hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="ea306-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="ea306-118">Создание консольного приложение</span><span class="sxs-lookup"><span data-stu-id="ea306-118">Create a console application</span></span>

<span data-ttu-id="ea306-119">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea306-119">Start Visual Studio.</span></span> <span data-ttu-id="ea306-120">Из hello **файл** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="ea306-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="ea306-121">Создайте консольное приложение .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ea306-121">Create a .NET Core console application.</span></span>

![Новый проект][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="ea306-123">Добавьте пакет NuGet концентраторов событий hello</span><span class="sxs-lookup"><span data-stu-id="ea306-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="ea306-124">Добавить hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard библиотеки NuGet пакета tooyour проекта, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ea306-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="ea306-125">Щелкните правой кнопкой мыши только что созданный hello проекта и выберите **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ea306-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="ea306-126">Нажмите кнопку hello **Обзор** , а затем поиск «Microsoft.Azure.EventHubs» и выберите hello **Microsoft.Azure.EventHubs** пакета.</span><span class="sxs-lookup"><span data-stu-id="ea306-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="ea306-127">Нажмите кнопку **установить** toocomplete hello установки, а затем закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="ea306-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="ea306-128">Запись некоторых концентратора событий toosend сообщения код toohello</span><span class="sxs-lookup"><span data-stu-id="ea306-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="ea306-129">Добавьте следующее hello `using` инструкций toohello верхней части файла Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="ea306-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="ea306-130">Добавить toohello константы `Program` класс для hello концентраторов событий строку и сущности путь подключения (имя концентратора события).</span><span class="sxs-lookup"><span data-stu-id="ea306-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="ea306-131">Замените заполнители hello в квадратных скобках hello соответствующих значений, которые были получены при создании концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="ea306-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="ea306-132">Добавьте новый метод с именем `MainAsync` toohello `Program` класса, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="ea306-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="ea306-133">Добавьте новый метод с именем `SendMessagesToEventHub` toohello `Program` класса, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="ea306-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
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

5. <span data-ttu-id="ea306-134">Добавьте следующий код toohello hello `Main` метод в hello `Program` класса.</span><span class="sxs-lookup"><span data-stu-id="ea306-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="ea306-135">Вот как будет выглядеть файл Program.cs.</span><span class="sxs-lookup"><span data-stu-id="ea306-135">Here is what your Program.cs should look like.</span></span>

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
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
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

6. <span data-ttu-id="ea306-136">Запустите программу hello и убедитесь, что отсутствуют ошибки.</span><span class="sxs-lookup"><span data-stu-id="ea306-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="ea306-137">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="ea306-137">Congratulations!</span></span> <span data-ttu-id="ea306-138">Теперь было отправлено концентратора событий tooan сообщений.</span><span class="sxs-lookup"><span data-stu-id="ea306-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea306-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ea306-139">Next steps</span></span>
<span data-ttu-id="ea306-140">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="ea306-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="ea306-141">Основные сведения о получении сообщений с помощью узла EventProcessorHost в .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ea306-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="ea306-142">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="ea306-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ea306-143">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="ea306-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ea306-144">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="ea306-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
