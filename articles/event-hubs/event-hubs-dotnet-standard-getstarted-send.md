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
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>Начало работы отправки сообщений tooAzure концентраторов событий в .NET Standard

> [!NOTE]
> Этот пример можно найти на сайте [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).

В этом учебнике показано, как toowrite .NET Core консольное приложение, которое отправляет набор сообщений tooan концентратора событий. Можно запустить hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) решения,-заменив hello `EhConnectionString` и `EhEntityPath` строки собственными значениями концентратора событий. Или же можно воспользоваться hello шагов в этот учебник toocreate свои собственные.

## <a name="prerequisites"></a>Предварительные требования

* [Microsoft Visual Studio 2015 или Microsoft Visual Studio 2017](http://www.visualstudio.com). также поддерживается Hello примерах данного учебника используйте Visual Studio 2017 г., но Visual Studio 2015.
* [Инструментарий Visual Studio 2015 или Visual Studio 2017 для .NET Core](http://www.microsoft.com/net/core).
* Подписка Azure.
* Пространство имен концентратора событий.

концентратор событий tooan toosend сообщения, мы будем использовать Visual Studio toowrite консольное приложение C#.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Создание пространства имен концентраторов событий и концентратора событий

Hello первым шагом является toouse hello [портал Azure](https://portal.azure.com) toocreate пространство имен для типа концентратора событий hello и получить учетные данные управления, необходимые приложению toocommunicate с концентратором событий hello hello. toocreate пространства имен и концентратора событий, выполните процедуру hello в [в этой статье](event-hubs-create.md)и продолжите hello следующие шаги.

## <a name="create-a-console-application"></a>Создание консольного приложение

Запустите Visual Studio. Из hello **файл** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**. Создайте консольное приложение .NET Core.

![Новый проект][1]

## <a name="add-hello-event-hubs-nuget-package"></a>Добавьте пакет NuGet концентраторов событий hello

Добавить hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard библиотеки NuGet пакета tooyour проекта, выполните следующие действия: 

1. Щелкните правой кнопкой мыши только что созданный hello проекта и выберите **управление пакетами NuGet**.
2. Нажмите кнопку hello **Обзор** , а затем поиск «Microsoft.Azure.EventHubs» и выберите hello **Microsoft.Azure.EventHubs** пакета. Нажмите кнопку **установить** toocomplete hello установки, а затем закрыть диалоговое окно.

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>Запись некоторых концентратора событий toosend сообщения код toohello

1. Добавьте следующее hello `using` инструкций toohello верхней части файла Program.cs hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. Добавить toohello константы `Program` класс для hello концентраторов событий строку и сущности путь подключения (имя концентратора события). Замените заполнители hello в квадратных скобках hello соответствующих значений, которые были получены при создании концентратора событий hello.

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. Добавьте новый метод с именем `MainAsync` toohello `Program` класса, как показано ниже:

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

4. Добавьте новый метод с именем `SendMessagesToEventHub` toohello `Program` класса, как показано ниже:

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

5. Добавьте следующий код toohello hello `Main` метод в hello `Program` класса.

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Вот как будет выглядеть файл Program.cs.

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

6. Запустите программу hello и убедитесь, что отсутствуют ошибки.

Поздравляем! Теперь было отправлено концентратора событий tooan сообщений.

## <a name="next-steps"></a>Дальнейшие действия
На сайте ссылкам hello, изучите более подробную концентраторов событий:

* [Основные сведения о получении сообщений с помощью узла EventProcessorHost в .NET Standard](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md)
* [Создание концентратора событий](event-hubs-create.md)
* [Часто задаваемые вопросы о концентраторах событий](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
