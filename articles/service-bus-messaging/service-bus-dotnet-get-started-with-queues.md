---
title: "aaaGet к работе с очередями Azure Service Bus | Документы Microsoft"
description: "Написание консольного приложения C#, которое использует очереди обмена сообщениями служебной шины."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>Начало работы с очередями служебной шины
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>Что будет выполнено
В этом учебнике hello следующие шаги:

1. Создание пространства имен Service Bus, с помощью портала Azure hello.
2. Создание очереди Service Bus, с помощью портала Azure hello.
3. Записать сообщение toosend консольного приложения.
4. Запись сообщений, отправленных в предыдущем шаге hello hello tooreceive консольного приложения.

## <a name="prerequisites"></a>Предварительные требования
1. [Visual Studio 2015 или более поздней версии.](http://www.visualstudio.com) Hello примерах в этом учебнике используется Visual Studio 2017 г.
2. Подписка Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Создание пространства имен с помощью портала Azure hello
Если вы уже создавали пространство имен обмена сообщениями Service Bus, перехода toohello [создания очереди с помощью портала Azure hello](#2-create-a-queue-using-the-azure-portal) раздела.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2. Создание очереди с помощью портала Azure hello
Если вы уже создали очереди Service Bus, перейдите к toohello [отправки сообщений в очереди toohello](#3-send-messages-to-the-queue) раздела.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3. Отправка сообщений в очереди toohello
toosend сообщений в очереди toohello, мы написать консольное приложение C# с помощью Visual Studio.

### <a name="create-a-console-application"></a>Создание консольного приложение

Откройте Visual Studio и создайте проект **Консольное приложение (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Добавление пакета шины обслуживания NuGet hello
1. Щелкните правой кнопкой мыши только что созданный hello проекта и выберите **управление пакетами NuGet**.
2. Щелкните hello **Обзор** вкладке выполните поиск **Microsoft Azure Service Bus**и затем выберите hello **WindowsAzure.ServiceBus** элемента. Нажмите кнопку **установить** toocomplete hello установки, а затем закрыть диалоговое окно.
   
    ![Установка пакета NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>Запись некоторых toosend кода toohello очереди сообщений
1. Добавьте следующее hello `using` инструкции toohello верхней части файла Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Добавьте следующий код toohello hello `Main` метод. Набор hello `connectionString` строка соединения переменной toohello, полученный при создании имен hello, а также задать `queueName` toohello имя очереди, который использовался при создании очереди hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Вот как будет выглядеть файл Program.cs.
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Запустите программу hello и проверьте hello портала Azure: щелкните hello именем очереди в пространстве имен hello **Обзор** колонку. очередь Hello **Essentials** колонке отображается. Обратите внимание, что hello **число активных сообщение** теперь значение должно быть 1. Каждый раз при запуске приложения отправителя hello без получения сообщений hello. Это значение увеличивается на 1. Также Обратите внимание, что hello текущего размера очереди hello увеличивает каждое приложение hello время добавляет toohello очереди сообщений.
   
      ![Размер сообщения][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4. Получение сообщений из очереди hello

1. сообщения приветствия tooreceive, который вы отправили, создайте новое консольное приложение и добавить пакет шины обслуживания NuGet toohello ссылку, похожее приложение отправителя toohello предыдущего.
2. Добавьте следующее hello `using` инструкции toohello верхней части файла Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Добавьте следующий код toohello hello `Main` метод. Набор hello `connectionString` переменных toohello строку подключения, был получен при создании имен hello, и задайте `queueName` toohello имя очереди, который использовался при создании очереди hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Вот как будет выглядеть файл Program.cs.
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Запустите программу hello и снова проверьте hello портала. Обратите внимание, что hello **число активных сообщение** и **текущей** значения в данный момент 0.
   
    ![Длина очереди][queue-message-receive]

Поздравляем! Вы создали очередь, а также отправили и получили сообщение.

## <a name="next-steps"></a>Дальнейшие действия

Извлечение нашей [репозитории GitHub с примерами](https://github.com/Azure/azure-service-bus/tree/master/samples) , показаны некоторые дополнительные возможности обмена сообщениями Service Bus hello.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
