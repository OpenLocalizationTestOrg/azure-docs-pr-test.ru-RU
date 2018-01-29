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
ms.date: 10/10/2017
ms.author: sethm
ms.openlocfilehash: 5cf01580b53b551064a46282b9005ade6afe9604
ms.sourcegitcommit: 51ea178c8205726e8772f8c6f53637b0d43259c6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a>Приступая к отправке событий в концентраторы событий Azure на платформе .NET Standard

> [!NOTE]
> Этот пример можно найти на сайте [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).

В этом руководстве показано, как написать консольное приложение для .NET Core, которое отправляет набор событий в концентратор событий. Вы можете запустить решение [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) "как есть", заменив строки `EhConnectionString` и `EhEntityPath` своими значениями для концентратора событий. Или следуйте инструкциям этого руководства, чтобы создать собственное решение.

## <a name="prerequisites"></a>Предварительные требования

* [Microsoft Visual Studio 2015 или Microsoft Visual Studio 2017](http://www.visualstudio.com). В примерах в этом руководстве используется Visual Studio 2017, но также поддерживается Visual Studio 2015.
* [Инструментарий Visual Studio 2015 или Visual Studio 2017 для .NET Core](http://www.microsoft.com/net/core).
* Подписка Azure.
* Пространство имен концентратора событий.

Для отправки сообщений в концентратор событий мы напишем консольное приложение C# в Visual Studio.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Создание пространства имен концентраторов событий и концентратора событий

Первым шагом является использование [портала Azure](https://portal.azure.com) для создания пространства имен концентраторов событий и получение учетных данных управления, необходимых приложению для взаимодействия с концентратором событий. Чтобы создать пространство имен и концентратор событий, выполните процедуру, описанную в [этой статье](event-hubs-create.md), а затем перейдите к следующим действиям.

## <a name="create-a-console-application"></a>Создание консольного приложение

Запустите Visual Studio. В меню **Файл** выберите команду **Создать**, а затем — **Проект**. Создайте консольное приложение .NET Core.

![Новый проект][1]

## <a name="add-the-event-hubs-nuget-package"></a>Добавление пакета NuGet для концентраторов событий

Добавьте пакет NuGet библиотеки .NET Standard [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) в проект, сделав следующее: 

1. Щелкните созданный проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.
2. Откройте вкладку **Обзор**, а затем выполните поиск по фразе Microsoft.Azure.EventHubs и выберите пакет **Microsoft.Azure.EventHubs**. Щелкните **Установить** , чтобы выполнить установку, а затем закройте это диалоговое окно.

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a>Написание кода для отправки сообщений в концентратор событий

1. Добавьте следующие операторы `using` в начало файла program.cs.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. Добавьте в класс `Program` константы для строки подключения концентраторов событий и пути сущности (имя отдельного концентратора событий). Замените заполнители в скобках соответствующими значениями, которые были получены при создании концентратора событий. Убедитесь, что `{Event Hubs connection string}` — это строка подключения на уровне пространства имен, а не концентратора событий. 

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. Добавьте новый метод с именем `MainAsync` в класс `Program`, как показано далее:

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

4. Добавьте новый метод с именем `SendMessagesToEventHub` в класс `Program`, как показано далее:

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

5. В метод `Main` в классе `Program` добавьте следующий код.

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

6. Запустите программу и убедитесь в отсутствии ошибок.

Поздравляем! Теперь вы можете отправлять сообщения в концентратор событий.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о концентраторах событий см. в следующих источниках:

* [Основные сведения о получении сообщений с помощью узла EventProcessorHost в .NET Standard](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md)
* [Создание концентратора событий](event-hubs-create.md)
* [Часто задаваемые вопросы о концентраторах событий](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
