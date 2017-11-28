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
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="f00e8-103">Начало работы с очередями служебной шины</span><span class="sxs-lookup"><span data-stu-id="f00e8-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="f00e8-104">Что будет выполнено</span><span class="sxs-lookup"><span data-stu-id="f00e8-104">What will be accomplished</span></span>
<span data-ttu-id="f00e8-105">В этом учебнике hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="f00e8-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="f00e8-106">Создание пространства имен Service Bus, с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f00e8-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="f00e8-107">Создание очереди Service Bus, с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f00e8-107">Create a Service Bus queue, using hello Azure portal.</span></span>
3. <span data-ttu-id="f00e8-108">Записать сообщение toosend консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="f00e8-108">Write a console application toosend a message.</span></span>
4. <span data-ttu-id="f00e8-109">Запись сообщений, отправленных в предыдущем шаге hello hello tooreceive консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="f00e8-109">Write a console application tooreceive hello messages sent in hello previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f00e8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f00e8-110">Prerequisites</span></span>
1. <span data-ttu-id="f00e8-111">[Visual Studio 2015 или более поздней версии.](http://www.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="f00e8-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="f00e8-112">Hello примерах в этом учебнике используется Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="f00e8-112">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="f00e8-113">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="f00e8-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="f00e8-114">1. Создание пространства имен с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="f00e8-114">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="f00e8-115">Если вы уже создавали пространство имен обмена сообщениями Service Bus, перехода toohello [создания очереди с помощью портала Azure hello](#2-create-a-queue-using-the-azure-portal) раздела.</span><span class="sxs-lookup"><span data-stu-id="f00e8-115">If you've already created a Service Bus Messaging namespace, jump toohello [Create a queue using hello Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a><span data-ttu-id="f00e8-116">2. Создание очереди с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="f00e8-116">2. Create a queue using hello Azure portal</span></span>
<span data-ttu-id="f00e8-117">Если вы уже создали очереди Service Bus, перейдите к toohello [отправки сообщений в очереди toohello](#3-send-messages-to-the-queue) раздела.</span><span class="sxs-lookup"><span data-stu-id="f00e8-117">If you have already created a Service Bus queue, jump toohello [Send messages toohello queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a><span data-ttu-id="f00e8-118">3. Отправка сообщений в очереди toohello</span><span class="sxs-lookup"><span data-stu-id="f00e8-118">3. Send messages toohello queue</span></span>
<span data-ttu-id="f00e8-119">toosend сообщений в очереди toohello, мы написать консольное приложение C# с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f00e8-119">toosend messages toohello queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="f00e8-120">Создание консольного приложение</span><span class="sxs-lookup"><span data-stu-id="f00e8-120">Create a console application</span></span>

<span data-ttu-id="f00e8-121">Откройте Visual Studio и создайте проект **Консольное приложение (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f00e8-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="f00e8-122">Добавление пакета шины обслуживания NuGet hello</span><span class="sxs-lookup"><span data-stu-id="f00e8-122">Add hello Service Bus NuGet package</span></span>
1. <span data-ttu-id="f00e8-123">Щелкните правой кнопкой мыши только что созданный hello проекта и выберите **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f00e8-123">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="f00e8-124">Щелкните hello **Обзор** вкладке выполните поиск **Microsoft Azure Service Bus**и затем выберите hello **WindowsAzure.ServiceBus** элемента.</span><span class="sxs-lookup"><span data-stu-id="f00e8-124">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="f00e8-125">Нажмите кнопку **установить** toocomplete hello установки, а затем закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="f00e8-125">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Установка пакета NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a><span data-ttu-id="f00e8-127">Запись некоторых toosend кода toohello очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="f00e8-127">Write some code toosend a message toohello queue</span></span>
1. <span data-ttu-id="f00e8-128">Добавьте следующее hello `using` инструкции toohello верхней части файла Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="f00e8-128">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="f00e8-129">Добавьте следующий код toohello hello `Main` метод.</span><span class="sxs-lookup"><span data-stu-id="f00e8-129">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="f00e8-130">Набор hello `connectionString` строка соединения переменной toohello, полученный при создании имен hello, а также задать `queueName` toohello имя очереди, который использовался при создании очереди hello.</span><span class="sxs-lookup"><span data-stu-id="f00e8-130">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="f00e8-131">Вот как будет выглядеть файл Program.cs.</span><span class="sxs-lookup"><span data-stu-id="f00e8-131">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="f00e8-132">Запустите программу hello и проверьте hello портала Azure: щелкните hello именем очереди в пространстве имен hello **Обзор** колонку.</span><span class="sxs-lookup"><span data-stu-id="f00e8-132">Run hello program, and check hello Azure portal: click hello name of your queue in hello namespace **Overview** blade.</span></span> <span data-ttu-id="f00e8-133">очередь Hello **Essentials** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="f00e8-133">hello queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="f00e8-134">Обратите внимание, что hello **число активных сообщение** теперь значение должно быть 1.</span><span class="sxs-lookup"><span data-stu-id="f00e8-134">Notice that hello **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="f00e8-135">Каждый раз при запуске приложения отправителя hello без получения сообщений hello. Это значение увеличивается на 1.</span><span class="sxs-lookup"><span data-stu-id="f00e8-135">Each time you run hello sender application without retrieving hello messages, this value increases by 1.</span></span> <span data-ttu-id="f00e8-136">Также Обратите внимание, что hello текущего размера очереди hello увеличивает каждое приложение hello время добавляет toohello очереди сообщений.</span><span class="sxs-lookup"><span data-stu-id="f00e8-136">Also note that hello current size of hello queue increments each time hello app adds a message toohello queue.</span></span>
   
      ![Размер сообщения][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a><span data-ttu-id="f00e8-138">4. Получение сообщений из очереди hello</span><span class="sxs-lookup"><span data-stu-id="f00e8-138">4. Receive messages from hello queue</span></span>

1. <span data-ttu-id="f00e8-139">сообщения приветствия tooreceive, который вы отправили, создайте новое консольное приложение и добавить пакет шины обслуживания NuGet toohello ссылку, похожее приложение отправителя toohello предыдущего.</span><span class="sxs-lookup"><span data-stu-id="f00e8-139">tooreceive hello messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="f00e8-140">Добавьте следующее hello `using` инструкции toohello верхней части файла Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="f00e8-140">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="f00e8-141">Добавьте следующий код toohello hello `Main` метод.</span><span class="sxs-lookup"><span data-stu-id="f00e8-141">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="f00e8-142">Набор hello `connectionString` переменных toohello строку подключения, был получен при создании имен hello, и задайте `queueName` toohello имя очереди, который использовался при создании очереди hello.</span><span class="sxs-lookup"><span data-stu-id="f00e8-142">Set hello `connectionString` variable toohello connection string that was obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="f00e8-143">Вот как будет выглядеть файл Program.cs.</span><span class="sxs-lookup"><span data-stu-id="f00e8-143">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="f00e8-144">Запустите программу hello и снова проверьте hello портала.</span><span class="sxs-lookup"><span data-stu-id="f00e8-144">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="f00e8-145">Обратите внимание, что hello **число активных сообщение** и **текущей** значения в данный момент 0.</span><span class="sxs-lookup"><span data-stu-id="f00e8-145">Notice that hello **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![Длина очереди][queue-message-receive]

<span data-ttu-id="f00e8-147">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="f00e8-147">Congratulations!</span></span> <span data-ttu-id="f00e8-148">Вы создали очередь, а также отправили и получили сообщение.</span><span class="sxs-lookup"><span data-stu-id="f00e8-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f00e8-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f00e8-149">Next steps</span></span>

<span data-ttu-id="f00e8-150">Извлечение нашей [репозитории GitHub с примерами](https://github.com/Azure/azure-service-bus/tree/master/samples) , показаны некоторые дополнительные возможности обмена сообщениями Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="f00e8-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
