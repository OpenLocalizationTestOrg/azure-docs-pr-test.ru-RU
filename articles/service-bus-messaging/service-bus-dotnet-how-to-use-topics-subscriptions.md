---
title: "Начало работы с разделами и подписками служебной шины Azure | Документация Майкрософт"
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
ms.openlocfilehash: 9401ada519f600b0d2817f06a396e16607a24129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="a8852-103">Начало работы с разделами служебной шины</span><span class="sxs-lookup"><span data-stu-id="a8852-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="a8852-104">Что будет выполнено</span><span class="sxs-lookup"><span data-stu-id="a8852-104">What will be accomplished</span></span>

<span data-ttu-id="a8852-105">В этом руководстве рассматриваются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a8852-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="a8852-106">Создание пространства имен служебной шины с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a8852-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="a8852-107">Создание раздела служебной шины с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a8852-107">Create a Service Bus topic, using the Azure portal.</span></span>
3. <span data-ttu-id="a8852-108">Создание подписки на этот раздел служебной шины с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a8852-108">Create a Service Bus subscription to that topic, using the Azure portal.</span></span>
4. <span data-ttu-id="a8852-109">Создание консольного приложения для отправки сообщения в раздел.</span><span class="sxs-lookup"><span data-stu-id="a8852-109">Write a console application to send a message to the topic.</span></span>
5. <span data-ttu-id="a8852-110">Создание консольного приложения для получения этого сообщения из подписки.</span><span class="sxs-lookup"><span data-stu-id="a8852-110">Write a console application to receive that message from the subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8852-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a8852-111">Prerequisites</span></span>

1. <span data-ttu-id="a8852-112">[Visual Studio 2015 или более поздней версии.](http://www.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="a8852-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="a8852-113">В описанных в этом руководстве примерах используется Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a8852-113">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="a8852-114">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="a8852-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="a8852-115">1. Создание пространства имен с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="a8852-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="a8852-116">Если пространство имен для обмена сообщениями служебной шины уже создано, перейдите к разделу [Создание раздела с помощью портала Azure](#2-create-a-topic-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="a8852-116">If you have already created a Service Bus Messaging namespace, jump to the [Create a topic using the Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-the-azure-portal"></a><span data-ttu-id="a8852-117">2) Создание раздела с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="a8852-117">2. Create a topic using the Azure portal</span></span>

1. <span data-ttu-id="a8852-118">Войдите на [портал Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="a8852-118">Log on to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="a8852-119">В левой области навигации портала щелкните **Служебная шина**. Если элемент **Служебная шина** не отображается, щелкните **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="a8852-119">In the left navigation pane of the portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="a8852-120">Щелкните пространство имен, в котором хотите создать раздел.</span><span class="sxs-lookup"><span data-stu-id="a8852-120">Click the namespace in which you would like to create the topic.</span></span> <span data-ttu-id="a8852-121">Появится колонка обзора пространства имен:</span><span class="sxs-lookup"><span data-stu-id="a8852-121">The namespace overview blade appears:</span></span>
   
    ![Создание раздела][createtopic1]
4. <span data-ttu-id="a8852-123">В колонке **Пространство имен служебной шины** выберите **Разделы** и щелкните **Добавить раздел**.</span><span class="sxs-lookup"><span data-stu-id="a8852-123">In the **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Выбор разделов][createtopic2]
5. <span data-ttu-id="a8852-125">Введите имя темы и снимите флажок для параметра **Включить секционирование**.</span><span class="sxs-lookup"><span data-stu-id="a8852-125">Enter a name for the topic, and uncheck the **Enable partitioning** option.</span></span> <span data-ttu-id="a8852-126">Для других параметров оставьте значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a8852-126">Leave the other options with their default values.</span></span>
   
    ![Нажмите кнопку "Создать"][createtopic3]
6. <span data-ttu-id="a8852-128">Щелкните кнопку **Создать**в нижней части колонки.</span><span class="sxs-lookup"><span data-stu-id="a8852-128">At the bottom of the blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-to-the-topic"></a><span data-ttu-id="a8852-129">3. Создание подписки на раздел</span><span class="sxs-lookup"><span data-stu-id="a8852-129">3. Create a subscription to the topic</span></span>

1. <span data-ttu-id="a8852-130">В области ресурсов на портале выберите пространство имен, созданное на этапе 1, и щелкните имя раздела, созданное на этапе 2.</span><span class="sxs-lookup"><span data-stu-id="a8852-130">In the portal resources pane, click the namespace you created in step 1, then click name of the topic you created in step 2.</span></span>
2. <span data-ttu-id="a8852-131">На панели обзора вверху щелкните знак плюса рядом с надписью **Подписка**, чтобы добавить подписку на этот раздел.</span><span class="sxs-lookup"><span data-stu-id="a8852-131">A the top of the overview pane, click the plus sign next to **Subscription** to add a subscription to this topic.</span></span>

    ![Создание подписки][createtopic4]

3. <span data-ttu-id="a8852-133">Введите имя подписки.</span><span class="sxs-lookup"><span data-stu-id="a8852-133">Enter a name for the subscription.</span></span> <span data-ttu-id="a8852-134">Для других параметров оставьте значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a8852-134">Leave the other options with their default values.</span></span>

## <a name="4-send-messages-to-the-topic"></a><span data-ttu-id="a8852-135">4. Отправка сообщений в раздел</span><span class="sxs-lookup"><span data-stu-id="a8852-135">4. Send messages to the topic</span></span>

<span data-ttu-id="a8852-136">Для отправки сообщений в раздел мы создадим консольное приложение C# с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8852-136">To send messages to the topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="a8852-137">Создание консольного приложение</span><span class="sxs-lookup"><span data-stu-id="a8852-137">Create a console application</span></span>

<span data-ttu-id="a8852-138">Откройте Visual Studio и создайте проект **Консольное приложение (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="a8852-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="a8852-139">Получение пакета NuGet для служебной шины</span><span class="sxs-lookup"><span data-stu-id="a8852-139">Add the Service Bus NuGet package</span></span>

1. <span data-ttu-id="a8852-140">Щелкните созданный проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a8852-140">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="a8852-141">Откройте вкладку **Обзор**, выполните поиск по фразе **служебная шина Microsoft Azure** и выберите элемент **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="a8852-141">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="a8852-142">Щелкните **Установить** , чтобы выполнить установку, а затем закройте это диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a8852-142">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![Установка пакета NuGet][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-topic"></a><span data-ttu-id="a8852-144">Написание кода для отправки сообщения в раздел</span><span class="sxs-lookup"><span data-stu-id="a8852-144">Write some code to send a message to the topic</span></span>

1. <span data-ttu-id="a8852-145">Добавьте следующую инструкцию `using` в начало файла Program.cs.</span><span class="sxs-lookup"><span data-stu-id="a8852-145">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="a8852-146">Добавьте в метод `Main` следующий код.</span><span class="sxs-lookup"><span data-stu-id="a8852-146">Add the following code to the `Main` method.</span></span> <span data-ttu-id="a8852-147">Укажите для переменной `connectionString` строку подключения, полученную при создании пространства имен, и задайте для `topicName` имя раздела, которое использовалось при его создании.</span><span class="sxs-lookup"><span data-stu-id="a8852-147">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="a8852-148">Вот как будет выглядеть файл Program.cs.</span><span class="sxs-lookup"><span data-stu-id="a8852-148">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="a8852-149">Запустите программу и перейдите на портал Azure. В колонке **Обзор** щелкните имя раздела в пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="a8852-149">Run the program, and check the Azure portal: click the name of your topic in the namespace **Overview** blade.</span></span> <span data-ttu-id="a8852-150">Отобразится колонка раздела **Основные**.</span><span class="sxs-lookup"><span data-stu-id="a8852-150">The topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="a8852-151">Обратите внимание, что для каждой подписки внизу колонки параметр **Количество сообщений** должен иметь значение 1.</span><span class="sxs-lookup"><span data-stu-id="a8852-151">In the subscription(s) listed near the bottom of the blade, notice that the **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="a8852-152">Каждый раз при запуске приложения отправителя без получения сообщений (как указано в следующем разделе) это значение увеличивается на 1.</span><span class="sxs-lookup"><span data-stu-id="a8852-152">Each time you run the sender application without retrieving the messages (as described in the next section), this value increases by 1.</span></span> <span data-ttu-id="a8852-153">А при каждом добавлении сообщения в раздел или подписку текущий размер раздела увеличивается, как и значение параметра **Текущий** в колонке **Основные**.</span><span class="sxs-lookup"><span data-stu-id="a8852-153">Also note that the current size of the topic increments the **Current** value on the **Essentials** blade each time the app adds a message to the topic/subscription.</span></span>
   
      ![Размер сообщения][topic-message]

## <a name="5-receive-messages-from-the-subscription"></a><span data-ttu-id="a8852-155">5. Получение сообщений из подписки</span><span class="sxs-lookup"><span data-stu-id="a8852-155">5. Receive messages from the subscription</span></span>

1. <span data-ttu-id="a8852-156">Чтобы получить только что отправленные сообщения, создайте консольное приложение и добавьте ссылку на пакет NuGet служебной шины в соответствии с инструкциями для предыдущего приложения отправителя.</span><span class="sxs-lookup"><span data-stu-id="a8852-156">To receive the message or messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="a8852-157">Добавьте следующую инструкцию `using` в начало файла Program.cs.</span><span class="sxs-lookup"><span data-stu-id="a8852-157">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="a8852-158">Добавьте в метод `Main` следующий код.</span><span class="sxs-lookup"><span data-stu-id="a8852-158">Add the following code to the `Main` method.</span></span> <span data-ttu-id="a8852-159">Укажите для переменной `connectionString` строку подключения, полученную при создании пространства имен, и задайте для `topicName` имя раздела, которое использовалось при его создании.</span><span class="sxs-lookup"><span data-stu-id="a8852-159">Set the `connectionString` variable to the connection string you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="a8852-160">Вот как будет выглядеть файл Program.cs.</span><span class="sxs-lookup"><span data-stu-id="a8852-160">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="a8852-161">Запустите программу и перейдите на портал еще раз.</span><span class="sxs-lookup"><span data-stu-id="a8852-161">Run the program, and check the portal again.</span></span> <span data-ttu-id="a8852-162">Обратите внимание, что параметры **Количество сообщений** и **Текущий** имеют значение 0.</span><span class="sxs-lookup"><span data-stu-id="a8852-162">Notice that the **Message Count** and **Current** values are now 0.</span></span>
   
    ![Длина раздела][topic-message-receive]

<span data-ttu-id="a8852-164">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="a8852-164">Congratulations!</span></span> <span data-ttu-id="a8852-165">Вы создали раздел и подписку, а также отправили и получили сообщение.</span><span class="sxs-lookup"><span data-stu-id="a8852-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8852-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8852-166">Next steps</span></span>

<span data-ttu-id="a8852-167">Ознакомьтесь с [примерами в репозитории GitHub](https://github.com/Azure/azure-service-bus/tree/master/samples), демонстрирующими расширенные возможности обмена сообщениями служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a8852-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

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
