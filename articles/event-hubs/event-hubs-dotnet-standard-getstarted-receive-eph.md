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
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>Начать получение сообщений с использованием hello узел обработчика событий в .NET Standard

> [!NOTE]
> Этот пример можно найти на сайте [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).

В этом учебнике показано, как toowrite .NET Core консольного приложения, которая получает сообщения из концентратора событий с помощью **EventProcessorHost**. Можно запустить hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) решения,-замена строк hello собственными значениями события концентратора и хранения данных учетной записи. Или же можно воспользоваться hello шагов в этот учебник toocreate свои собственные.

## <a name="prerequisites"></a>Предварительные требования

* [Microsoft Visual Studio 2015 или Microsoft Visual Studio 2017](http://www.visualstudio.com). также поддерживается Hello примерах данного учебника используйте Visual Studio 2017 г., но Visual Studio 2015.
* [Инструментарий Visual Studio 2015 или Visual Studio 2017 для .NET Core](http://www.microsoft.com/net/core).
* Подписка Azure.
* Пространство имен концентраторов событий Azure.
* Учетная запись хранения Azure.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Создание пространства имен концентраторов событий и концентратора событий  

Hello первым шагом является toouse hello [портал Azure](https://portal.azure.com) toocreate пространство имен для hello концентраторов событий введите и получить учетные данные управления, необходимые приложению toocommunicate с концентратором событий hello hello. toocreate пространство имен и концентратора событий, выполните процедуру hello в [в этой статье](event-hubs-create.md)и продолжите hello следующие шаги.  

## <a name="create-an-azure-storage-account"></a>Создание учетной записи хранения Azure  

1. Войдите в toohello [портал Azure](https://portal.azure.com).  
2. В области навигации слева hello hello портала щелкните **New**, нажмите кнопку **хранилища**и нажмите кнопку **учетной записи хранилища**.  
3. Заполните поля hello в колонке учетной записи хранилища hello и нажмите кнопку **создать**.

    ![Создать учетную запись хранения][1]

4. После появления hello **развертывания успешно** сообщение, щелкните имя hello hello новой учетной записи хранения. В hello **Essentials** колонка, щелкните **большие двоичные объекты**. Здравствуйте, когда **службе BLOB-объектов** открывается колонка, щелкните **+ контейнер** вверху hello. Присвойте имя контейнера hello, а затем закройте hello **службе BLOB-объектов** колонку.  
5. Нажмите кнопку **ключи доступа** в hello левой колонке и скопируйте hello имя контейнера хранилища hello, hello учетной записи хранилища и значение hello **key1**. Сохраните эти значения tooNotepad или других временное расположение.  

## <a name="create-a-console-application"></a>Создание консольного приложение

Запустите Visual Studio. Из hello **файл** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**. Создайте консольное приложение .NET Core.

![Новый проект][2]

## <a name="add-hello-event-hubs-nuget-package"></a>Добавьте пакет NuGet концентраторов событий hello

Добавить hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) и [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard проекта библиотеки NuGet пакеты tooyour, выполните следующие действия: 

1. Щелкните правой кнопкой мыши только что созданный hello проекта и выберите **управление пакетами NuGet**.
2. Нажмите кнопку hello **Обзор** , а затем поиск «Microsoft.Azure.EventHubs» и выберите hello **Microsoft.Azure.EventHubs** пакета. Нажмите кнопку **установить** toocomplete hello установки, а затем закрыть диалоговое окно.
3. Повторите шаги 1 и 2, а также установить hello **Microsoft.Azure.EventHubs.Processor** пакета.

## <a name="implement-hello-ieventprocessor-interface"></a>Реализуйте интерфейс IEventProcessor hello

1. В обозревателе решений щелкните правой кнопкой мыши проект hello, нажмите кнопку **добавить**, а затем нажмите кнопку **класса**. Имя нового класса hello **SimpleEventProcessor**.

2. Откройте файл SimpleEventProcessor.cs hello и добавьте следующее hello `using` инструкций toohello вверху файла hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. Реализуйте hello `IEventProcessor` интерфейса. Замените все содержимое hello hello `SimpleEventProcessor` класса hello, следующий код:

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>Метод главной консоли, который использует класс tooreceive hello SimpleEventProcessor сообщения

1. Добавьте следующее hello `using` инструкций toohello верхней части файла Program.cs hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. Добавить toohello константы `Program` класс для строки подключения концентратора событий hello, имя концентратора событий, имя контейнера в учетной записи хранения, имя учетной записи хранения и ключ учетной записи хранения. Добавьте hello после кода, заменив заполнители hello и соответствующие им значения.

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. Добавьте новый метод с именем `MainAsync` toohello `Program` класса, как показано ниже:

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

3. Добавьте следующие строки кода toohello hello `Main` метод:

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    Вот как будет выглядеть файл Program.cs.

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

4. Запустите программу hello и убедитесь, что отсутствуют ошибки.

Поздравляем! Теперь Получено сообщений из концентратора событий с помощью hello узел обработчика событий.

## <a name="next-steps"></a>Дальнейшие действия
На сайте ссылкам hello, изучите более подробную концентраторов событий:

* [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md)
* [Создание концентратора событий](event-hubs-create.md)
* [Часто задаваемые вопросы о концентраторах событий](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
