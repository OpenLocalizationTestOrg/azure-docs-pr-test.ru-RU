---
title: "aaaGet работы с Azure Service Bus разделы и подписки | Документы Microsoft"
description: "Написание консольного приложения C#, которое использует обмен сообщениями служебной шины для разделов и подписок"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>Начало работы с разделами служебной шины

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>Что будет выполнено

В этом учебнике hello следующие шаги:

1. Создание пространства имен Service Bus, с помощью портала Azure hello.
2. Создайте раздел служебной шины, с помощью портала Azure hello.
3. Создайте раздел toothat подписки Service Bus, с помощью hello портал Azure.
4. Написания приложения консоли toosend раздела toohello сообщения.
5. Запись tooreceive консольного приложения это сообщение от подписки hello.

## <a name="prerequisites"></a>Предварительные требования

1. [Visual Studio 2015 или более поздней версии.](http://www.visualstudio.com) Hello примерах в этом учебнике используется Visual Studio 2017 г.
2. Подписка Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Создание пространства имен с помощью портала Azure hello

Если вы уже создали пространство имен обмена сообщениями Service Bus, перехода toohello [создайте раздел с помощью портала Azure hello](#2-create-a-topic-using-the-azure-portal) раздела.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2. Создайте раздел с помощью портала Azure hello

1. Войдите на toohello [портал Azure][azure-portal].
2. В области навигации слева hello hello портала щелкните **Service Bus** (Если вы не видите **Service Bus**, нажмите кнопку **дополнительные службы**).
3. Щелкните hello пространство имен, в котором вы хотите toocreate hello раздела. Откроется колонка Обзор Hello пространство имен:
   
    ![Создание раздела][createtopic1]
4. В hello **пространства имен Service Bus** колонка, щелкните **разделы**, нажмите кнопку **добавить раздел**.
   
    ![Выбор разделов][createtopic2]
5. Введите имя для раздела hello и снимите флажок hello **включить секционирование** параметр. Hello других параметров оставьте их значения по умолчанию.
   
    ![Нажмите кнопку "Создать"][createtopic3]
6. Hello нижней части колонки hello, нажмите кнопку **создать**.

## <a name="3-create-a-subscription-toohello-topic"></a>3. Создание раздела toohello подписки

1. В области портала ресурсы hello щелкните hello пространства имен, созданный на шаге 1, а затем щелкните имя раздела hello, созданный на шаге 2.
2. Hello вверху области "Обзор" hello, щелкните hello плюс рядом входа слишком**подписки** tooadd toothis подписки раздела.

    ![Создание подписки][createtopic4]

3. Введите имя для подписки hello. Hello других параметров оставьте их значения по умолчанию.

## <a name="4-send-messages-toohello-topic"></a>4. Отправить toohello темы о сообщениях

раздел toohello toosend сообщения, мы написать консольное приложение C# с помощью Visual Studio.

### <a name="create-a-console-application"></a>Создание консольного приложение

Откройте Visual Studio и создайте проект **Консольное приложение (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Добавление пакета шины обслуживания NuGet hello

1. Щелкните правой кнопкой мыши только что созданный hello проекта и выберите **управление пакетами NuGet**.
2. Щелкните hello **Обзор** вкладке выполните поиск **Microsoft Azure Service Bus**и затем выберите hello **WindowsAzure.ServiceBus** элемента. Нажмите кнопку **установить** toocomplete hello установки, а затем закрыть диалоговое окно.
   
    ![Установка пакета NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>Написания некоторые toosend код раздела toohello сообщения

1. Добавьте следующее hello `using` инструкции toohello верхней части файла Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Добавьте следующий код toohello hello `Main` метод. Набор hello `connectionString` строка соединения переменной toohello, полученный при создании имен hello, а также задать `topicName` toohello имя, которое использовалось при создании раздела hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
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

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Запустите программу hello и проверьте hello портала Azure: щелкните имя раздела в пространстве имен hello hello **Обзор** колонку. раздел Hello **Essentials** колонке отображается. Hello подписок в списке hello нижней части колонки hello, обратите внимание, что hello **число сообщений** значение для каждой подписки теперь должен быть равен 1. Каждый раз, в случае запуска приложения отправителя hello без получения сообщений hello (как описано в следующем разделе hello), это значение увеличивается на 1. Также Обратите внимание, текущий размер hello hello разделе шагом hello **текущей** значение hello **Essentials** колонке каждый раз, приложение hello добавляет toohello сообщения раздела или подписки.
   
      ![Размер сообщения][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5. Получение сообщений из подписки hello

1. tooreceive приветственных сообщений или сообщений, который вы отправили, создайте новое консольное приложение и добавить пакет шины обслуживания NuGet toohello ссылку, аналогичные приложения отправителя toohello предыдущего.
2. Добавьте следующее hello `using` инструкции toohello верхней части файла Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Добавьте следующий код toohello hello `Main` метод. Набор hello `connectionString` строка соединения переменной toohello, можно получить при создании имен hello и задайте `topicName` toohello имя, которое использовалось при создании раздела hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
4. Запустите программу hello и снова проверьте hello портала. Обратите внимание, что hello **число сообщений** и **текущей** значения в данный момент 0.
   
    ![Длина раздела][topic-message-receive]

Поздравляем! Вы создали раздел и подписку, а также отправили и получили сообщение.

## <a name="next-steps"></a>Дальнейшие действия

Извлечение нашей [репозитории GitHub с примерами](https://github.com/Azure/azure-service-bus/tree/master/samples) , показаны некоторые дополнительные возможности обмена сообщениями Service Bus hello.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
