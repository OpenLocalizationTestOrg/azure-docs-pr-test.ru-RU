---
title: "Центры уведомлений — корпоративная архитектура системы push-уведомлений"
description: "Руководство по использованию центров уведомлений Azure в корпоративной среде"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: ae7c1c9644ecfe7fe4ad6e332cc0683a3b5df22f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="594db-103">Руководство по архитектуре push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="594db-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="594db-104">Сегодня предприятия постепенно переходят к созданию мобильных приложений для конечных пользователей (внешних) или сотрудников (внутренних).</span><span class="sxs-lookup"><span data-stu-id="594db-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="594db-105">У них есть серверные системы, размещенные на мэйнфреймах, или бизнес-приложения, которые нужно интегрировать в архитектуру приложений для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="594db-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="594db-106">В этом руководстве рассказывается об оптимальном подходе к такой интеграции и излагаются рекомендации относительно возможных решений для распространенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="594db-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="594db-107">Одно из наиболее распространенных требований — возможность отправки push-уведомлений пользователям с помощью мобильных приложений при определенных событиях в серверной системе.</span><span class="sxs-lookup"><span data-stu-id="594db-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="594db-108">Например: </span><span class="sxs-lookup"><span data-stu-id="594db-108">E.g.</span></span> <span data-ttu-id="594db-109">клиент банка, у которого есть банковское приложение на iPhone, хочет получать уведомления при списании со счета сумм, превышающих определенное значение, а сотрудник из финансового отдела, у которого есть приложение для утверждения бюджета на устройстве Windows Phone, хочет получать по интрасети уведомления при получении запроса на утверждение.</span><span class="sxs-lookup"><span data-stu-id="594db-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="594db-110">Обслуживание банковского счета и обработка утверждений, как правило, осуществляются в серверной системе, которая должна инициировать отправку push-уведомлений пользователю.</span><span class="sxs-lookup"><span data-stu-id="594db-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="594db-111">Таких серверных систем может быть несколько, а для реализации push-уведомлений, отправка которых инициируется наступлением определенных событий, все они должны быть созданы на основе одной и той же логики.</span><span class="sxs-lookup"><span data-stu-id="594db-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="594db-112">Сложность в том, как интегрировать несколько серверных систем с одной системой push-уведомлений, где конечные пользователи могут подписываться на различные уведомления и даже использовать различные мобильные приложения, например, в случае интрасети, где одно мобильное приложение может получать уведомления из нескольких таких серверных систем.</span><span class="sxs-lookup"><span data-stu-id="594db-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="594db-113">Серверным системам неизвестна или не должна быть известна семантика или технология системы отправки push-уведомлений, поэтому в таких случаях традиционным решением было внедрение компонента, который опрашивает серверные системы, чтобы определить, не произошло ли то или иное событие, и отвечает за отправку push-уведомлений клиенту.</span><span class="sxs-lookup"><span data-stu-id="594db-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="594db-114">Здесь мы поговорим о еще лучшем решении с использованием служебной шины Azure — модели разделов и подписок, которая обеспечивает простоту и масштабируемость.</span><span class="sxs-lookup"><span data-stu-id="594db-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="594db-115">Ниже описана общая архитектура решения. Изложенная здесь информация касается общего случая нескольких мобильных приложений, однако она в равной мере применима в случае, если такое приложение только одно.</span><span class="sxs-lookup"><span data-stu-id="594db-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="594db-116">Архитектура</span><span class="sxs-lookup"><span data-stu-id="594db-116">Architecture</span></span>
![][1]

<span data-ttu-id="594db-117">Основной элемент на этой схеме архитектуры — это служебная шина Azure, которая предоставляет модель программирования разделов и подписок (подробнее об этом см. в статье [Как использовать разделы и подписки служебной шины]).</span><span class="sxs-lookup"><span data-stu-id="594db-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="594db-118">Получатель (в данном случае это серверная часть мобильной службы, обычно — [мобильная служба Azure], которая будет инициировать отправку push-уведомлений для мобильных приложений) не получает сообщения напрямую от серверных систем. Эти уведомления поступают к нему с промежуточного уровня абстракции, предоставляемого [служебной шиной Azure], что позволяет серверной части мобильной службы получать сообщения из одной или нескольких серверных систем.</span><span class="sxs-lookup"><span data-stu-id="594db-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="594db-119">Раздел "Служебная шина" необходимо создать для каждой из серверных систем, например "Бухгалтерия", "Отдел кадров" и "Финансы", по сути являющиеся "разделами", которые будут инициировать отправку сообщений в виде push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="594db-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="594db-120">Серверные системы будут отправлять сообщения в эти разделы.</span><span class="sxs-lookup"><span data-stu-id="594db-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="594db-121">Мобильный внутренний сервер может подписаться на один или несколько таких разделов, создав подписку на служебную шину.</span><span class="sxs-lookup"><span data-stu-id="594db-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="594db-122">Это даст серверной части мобильной службы возможность получать уведомления от соответствующей серверной системы.</span><span class="sxs-lookup"><span data-stu-id="594db-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="594db-123">Этот сервер продолжает прослушивать сообщения по своим подпискам, и как только сообщение поступает, он отправляет его в виде уведомления в свой центр уведомлений.</span><span class="sxs-lookup"><span data-stu-id="594db-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="594db-124">В конечном итоге центры уведомлений доставляют сообщение в мобильное приложение.</span><span class="sxs-lookup"><span data-stu-id="594db-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="594db-125">Итак, у нас есть следующие ключевые компоненты:</span><span class="sxs-lookup"><span data-stu-id="594db-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="594db-126">Серверные системы (бизнес-системы или устаревшие системы)</span><span class="sxs-lookup"><span data-stu-id="594db-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="594db-127">Создает раздел Service Bus</span><span class="sxs-lookup"><span data-stu-id="594db-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="594db-128">Отправляет сообщение</span><span class="sxs-lookup"><span data-stu-id="594db-128">Sends Message</span></span>
2. <span data-ttu-id="594db-129">Серверная часть мобильной службы</span><span class="sxs-lookup"><span data-stu-id="594db-129">Mobile backend</span></span>
   * <span data-ttu-id="594db-130">Создает подписку на службу</span><span class="sxs-lookup"><span data-stu-id="594db-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="594db-131">Получает сообщение (из серверной системы)</span><span class="sxs-lookup"><span data-stu-id="594db-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="594db-132">Отправляет уведомление клиентам (через центр уведомлений Azure)</span><span class="sxs-lookup"><span data-stu-id="594db-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="594db-133">Мобильное приложение</span><span class="sxs-lookup"><span data-stu-id="594db-133">Mobile Application</span></span>
   * <span data-ttu-id="594db-134">Получает и отображает уведомление</span><span class="sxs-lookup"><span data-stu-id="594db-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="594db-135">Преимущества:</span><span class="sxs-lookup"><span data-stu-id="594db-135">Benefits:</span></span>
1. <span data-ttu-id="594db-136">Разделение на получателя (мобильное приложение или служба через центр уведомлений) и отправителя (серверные системы) позволяет интегрировать дополнительные серверные системы с минимальными изменениями.</span><span class="sxs-lookup"><span data-stu-id="594db-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="594db-137">Упрощается ситуация, когда необходимо, чтобы уведомления о событиях в одной или нескольких серверных системах получали несколько мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="594db-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="594db-138">Пример:</span><span class="sxs-lookup"><span data-stu-id="594db-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="594db-139">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="594db-139">Prerequisites</span></span>
<span data-ttu-id="594db-140">Чтобы ознакомиться с основными понятиями и общими процедурами создания и настройки, необходимо пройти следующие учебники:</span><span class="sxs-lookup"><span data-stu-id="594db-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="594db-141">[Как использовать разделы и подписки служебной шины] — здесь подробно описывается работа с разделами и подписками служебной шины, создание пространства имен для хранения разделов и подписок, отправка им сообщений и получение сообщений от них.</span><span class="sxs-lookup"><span data-stu-id="594db-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="594db-142">[учебника по центрам уведомлений для Windows Universal] — в этом учебнике рассказывается о том, как настроить приложение Магазина Windows и использовать центры уведомлений для регистрации и последующего получения уведомлений.</span><span class="sxs-lookup"><span data-stu-id="594db-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="594db-143">Пример кода</span><span class="sxs-lookup"><span data-stu-id="594db-143">Sample code</span></span>
<span data-ttu-id="594db-144">Полный пример кода доступен в [коллекции примеров центра уведомлений].</span><span class="sxs-lookup"><span data-stu-id="594db-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="594db-145">Он состоит из трех компонентов:</span><span class="sxs-lookup"><span data-stu-id="594db-145">It is split into three components:</span></span>

1. <span data-ttu-id="594db-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="594db-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="594db-147">а.</span><span class="sxs-lookup"><span data-stu-id="594db-147">a.</span></span> <span data-ttu-id="594db-148">Этот проект использует пакет NuGet *WindowsAzure.ServiceBus* и основан на материале, изложенном в статье [Как использовать разделы и подписки служебной шины].</span><span class="sxs-lookup"><span data-stu-id="594db-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="594db-149">b.</span><span class="sxs-lookup"><span data-stu-id="594db-149">b.</span></span> <span data-ttu-id="594db-150">Это простое консольное приложение на C# для моделирования бизнес-систем, которое инициирует доставку сообщений мобильному приложению.</span><span class="sxs-lookup"><span data-stu-id="594db-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="594db-151">c.</span><span class="sxs-lookup"><span data-stu-id="594db-151">c.</span></span> <span data-ttu-id="594db-152">`CreateTopic` используется для создания раздела служебной шины, в который будут отправляться сообщения.</span><span class="sxs-lookup"><span data-stu-id="594db-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="594db-153">d.</span><span class="sxs-lookup"><span data-stu-id="594db-153">d.</span></span> <span data-ttu-id="594db-154">`SendMessage` используется для отправки сообщений в этот раздел служебной шины.</span><span class="sxs-lookup"><span data-stu-id="594db-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="594db-155">В данном примере мы будем периодически отправлять набор случайных сообщений в этот раздел.</span><span class="sxs-lookup"><span data-stu-id="594db-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="594db-156">Как правило эту функцию будет выполнять серверная система, которая будет отправлять сообщения при наступлении события.</span><span class="sxs-lookup"><span data-stu-id="594db-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. <span data-ttu-id="594db-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="594db-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="594db-158">а.</span><span class="sxs-lookup"><span data-stu-id="594db-158">a.</span></span> <span data-ttu-id="594db-159">Этот проект использует пакеты NuGet *WindowsAzure.ServiceBus* и *Microsoft.Web.WebJobs.Publish* и основан на материале, изложенном в статье [Как использовать разделы и подписки служебной шины].</span><span class="sxs-lookup"><span data-stu-id="594db-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="594db-160">b.</span><span class="sxs-lookup"><span data-stu-id="594db-160">b.</span></span> <span data-ttu-id="594db-161">Это еще одно консольное приложение на C#, которое мы будем запускать в качестве [веб-задания Azure] , так как оно должно выполняться непрерывно для прослушивания сообщений из бизнес-систем и серверных систем.</span><span class="sxs-lookup"><span data-stu-id="594db-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="594db-162">Оно будет входить в состав серверной части мобильной службы.</span><span class="sxs-lookup"><span data-stu-id="594db-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="594db-163">c.</span><span class="sxs-lookup"><span data-stu-id="594db-163">c.</span></span> <span data-ttu-id="594db-164">`CreateSubscription` используется для создания подписки служебной шины для раздела, в который серверная система будет отправлять сообщения.</span><span class="sxs-lookup"><span data-stu-id="594db-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="594db-165">В зависимости от бизнес-сценария этот компонент создаст одну или несколько подписок на соответствующие разделы (например, одни будут получать сообщения из системы "Отдел кадров", другие — из системы "Финансы" и т. д.)</span><span class="sxs-lookup"><span data-stu-id="594db-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="594db-166">d.</span><span class="sxs-lookup"><span data-stu-id="594db-166">d.</span></span> <span data-ttu-id="594db-167">ReceiveMessageAndSendNotification используется для чтения сообщения из раздела с использованием подписки. Если операция считывания выполнена успешно, создается уведомление (в этом примере сценария — собственное всплывающее уведомление Windows), которое необходимо отправить в мобильное приложение с помощью Центров уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="594db-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    <span data-ttu-id="594db-168">д.</span><span class="sxs-lookup"><span data-stu-id="594db-168">e.</span></span> <span data-ttu-id="594db-169">Чтобы опубликовать этот процесс в виде **веб-задания**, щелкните правой кнопкой мыши решение в Visual Studio и выберите **Publish as WebJob** (Опубликовать как веб-задание).</span><span class="sxs-lookup"><span data-stu-id="594db-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="594db-170">Е.</span><span class="sxs-lookup"><span data-stu-id="594db-170">f.</span></span> <span data-ttu-id="594db-171">Выберите профиль публикации и создайте новый веб-сайт Azure для размещения веб-задания (если он еще не существует), а когда веб-сайт будет создан, щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="594db-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="594db-172">ж.</span><span class="sxs-lookup"><span data-stu-id="594db-172">g.</span></span> <span data-ttu-id="594db-173">Настройте "непрерывное выполнение" задания, чтобы при входе на [классическом портале Azure] отображалось примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="594db-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="594db-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="594db-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="594db-175">а.</span><span class="sxs-lookup"><span data-stu-id="594db-175">a.</span></span> <span data-ttu-id="594db-176">Это приложение Магазина Windows, которое будет получать всплывающие уведомления из задания WebJob, выполняющегося в составе серверной части мобильной службы, и отображать это уведомление.</span><span class="sxs-lookup"><span data-stu-id="594db-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="594db-177">Оно основано на материале [учебника по центрам уведомлений для Windows Universal].</span><span class="sxs-lookup"><span data-stu-id="594db-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="594db-178">b.</span><span class="sxs-lookup"><span data-stu-id="594db-178">b.</span></span> <span data-ttu-id="594db-179">Убедитесь, что в приложении включено получение всплывающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="594db-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="594db-180">c.</span><span class="sxs-lookup"><span data-stu-id="594db-180">c.</span></span> <span data-ttu-id="594db-181">Убедитесь, что при запуске приложения вызывается следующий код регистрации Центров уведомлений (после замены *HubName* и *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="594db-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="594db-182">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="594db-182">Running sample:</span></span>
1. <span data-ttu-id="594db-183">Убедитесь, что задание WebJob успешно запущено и для него запланировано «непрерывное выполнение».</span><span class="sxs-lookup"><span data-stu-id="594db-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="594db-184">Запустите **EnterprisePushMobileApp** , чтобы запустить приложение Магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="594db-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="594db-185">Запустите консольное приложение **EnterprisePushBackendSystem**, которое будет имитировать серверную часть бизнес-системы и начнет отправлять сообщения. Вы должны увидеть примерно такие всплывающие уведомления:</span><span class="sxs-lookup"><span data-stu-id="594db-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="594db-186">Первоначально сообщения были отправлены в разделы Service Bus, которые отслеживаются по подпискам Service Bus в задании WebJob.</span><span class="sxs-lookup"><span data-stu-id="594db-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="594db-187">При получении сообщения было создано уведомление, которое затем было отправлено в мобильное приложение.</span><span class="sxs-lookup"><span data-stu-id="594db-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="594db-188">Чтобы убедиться в правильности выполнения обработки, можно просмотреть журналы задания WebJob, перейдя по ссылке "Журналы" на [классическом портале Azure] для соответствующего задания WebJob:</span><span class="sxs-lookup"><span data-stu-id="594db-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
<span data-ttu-id="594db-189">[коллекции примеров центра уведомлений]: https://github.com/Azure/azure-notificationhubs-samples</span><span class="sxs-lookup"><span data-stu-id="594db-189">[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples</span></span>
<span data-ttu-id="594db-190">[мобильная служба Azure]: http://azure.microsoft.com/documentation/services/mobile-services/</span><span class="sxs-lookup"><span data-stu-id="594db-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span></span>
<span data-ttu-id="594db-191">[служебной шиной Azure]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span><span class="sxs-lookup"><span data-stu-id="594db-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span></span>
<span data-ttu-id="594db-192">[Как использовать разделы и подписки служебной шины]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span><span class="sxs-lookup"><span data-stu-id="594db-192">[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span></span>
<span data-ttu-id="594db-193">[веб-задания Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span><span class="sxs-lookup"><span data-stu-id="594db-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span></span>
<span data-ttu-id="594db-194">[учебника по центрам уведомлений для Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="594db-194">[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="594db-195">[классическом портале Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="594db-195">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
