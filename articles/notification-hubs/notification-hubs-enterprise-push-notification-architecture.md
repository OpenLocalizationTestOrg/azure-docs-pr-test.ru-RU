---
title: "aaaNotification концентраторов - Корпоративная архитектура Push"
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
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="1b0ea-103">Руководство по архитектуре push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="1b0ea-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="1b0ea-104">Компании сегодня переходят постепенно по созданию мобильных приложений, либо для конечных пользователей (внешний) или для сотрудников hello (внутренний).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for hello employees (internal).</span></span> <span data-ttu-id="1b0ea-105">Они имеют существующие серверной системы на месте будь то мэйнфреймы или некоторые бизнес-приложений, которые должны быть интегрированы в hello архитектуру приложений для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into hello mobile application architecture.</span></span> <span data-ttu-id="1b0ea-106">В этом руководстве поговорим об оптимальном способе toodo такой интеграции, рекомендующее toocommon сценарии из возможных решений.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-106">This guide will talk about how best toodo this integration recommending possible solution toocommon scenarios.</span></span>

<span data-ttu-id="1b0ea-107">Часто требуется для Отправка push-уведомления toohello пользователей с помощью своих мобильных приложений, при возникновении события интерес в серверных системах hello.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-107">A frequent requirement is for sending push notification toohello users through their mobile application when an event of interest occurs in hello backend systems.</span></span> <span data-ttu-id="1b0ea-108">Например: </span><span class="sxs-lookup"><span data-stu-id="1b0ea-108">E.g.</span></span> <span data-ttu-id="1b0ea-109">Банк, имеющему приложения hello bank банковских операций для своего iPhone клиенту уведомление при дебета превышают определенный объем из своей учетной записи или интрасети, где сотрудник из финансового отдела с приложении утверждения бюджет на его Windows Phone хочет toobe toobe уведомление, когда он получает запрос на утверждение.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-109">a bank customer who has hello bank's banking app on her iPhone wants toobe notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants toobe notified when he gets an approval request.</span></span>

<span data-ttu-id="1b0ea-110">Hello банковского счета или утверждения обработки является toobe скорее всего, в некоторых серверной системе, в которой необходимо инициировать пользователь toohello push.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-110">hello bank account or approval processing is likely toobe done in some backend system which must initiate a push toohello user.</span></span> <span data-ttu-id="1b0ea-111">Может существовать несколько внутренних системах, которые должны все сборки hello разный принудительной tooimplement логики, при возникновении события уведомления.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-111">There may be multiple such backend systems which must all build hello same kind of logic tooimplement push when an event triggers a notification.</span></span> <span data-ttu-id="1b0ea-112">Hello сложность здесь заключается в интеграции несколько серверных системах вместе с отдельной принудительной системы, где hello конечные пользователи могут подписаны toodifferent уведомления и может существовать даже быть несколько мобильных приложений, например в случае, когда hello мобильные приложения интрасети где одного мобильного приложения может потребоваться уведомления tooreceive несколько таких систем баз.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-112">hello complexity here lies in integrating several backend systems together with a single push system where hello end users may have subscribed toodifferent notifications and there may even be multiple mobile applications e.g. in hello case of intranet mobile apps where one mobile application may want tooreceive notifications from multiple such backend systems.</span></span> <span data-ttu-id="1b0ea-113">Hello серверных системах не знать, и требуется tooknow принудительной семантику и технологии, поэтому распространенное решение традиционно была toointroduce компонентом опрашивает hello серверных системах на наличие событий, представляющие интерес и отвечает за отправку сообщений hello push Клиент toohello.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-113">hello backend systems do not know or need tooknow of push semantics/technology so a common solution here traditionally has been toointroduce a component which polls hello backend systems for any events of interest and is responsible for sending hello push messages toohello client.</span></span>
<span data-ttu-id="1b0ea-114">Здесь мы поговорим о решение еще лучше, с помощью шины обслуживания Azure — модель раздела или подписки, которая позволяет снизить сложность hello сделана масштабируемых решений hello.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce hello complexity while making hello solution scalable.</span></span>

<span data-ttu-id="1b0ea-115">Вот hello общая архитектура решения hello (общего для нескольких мобильных приложений, но одинаково применимы, если имеется только одно мобильное приложение)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-115">Here is hello general architecture of hello solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="1b0ea-116">Архитектура</span><span class="sxs-lookup"><span data-stu-id="1b0ea-116">Architecture</span></span>
![][1]

<span data-ttu-id="1b0ea-117">ключевыми являются Hello в этом Архитектурная схема является Azure Service Bus, который предоставляет модель программирования разделов и подписок (на его в параметре [программирование Service Bus Pub/Sub]).</span><span class="sxs-lookup"><span data-stu-id="1b0ea-117">hello key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="1b0ea-118">Hello получателем, что в данном случае является hello мобильного внутреннего сервера (обычно [мобильных служб Azure], которой будет инициировать принудительную toohello мобильных приложений) не принимать сообщения непосредственно из hello серверных системах, но вместо этого у нас есть Абстрактный промежуточный уровень [Azure Service Bus] позволяющее мобильной серверной части tooreceive сообщения из одного или нескольких серверных системах.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-118">hello receiver, which in this case, is hello Mobile backend (typically [Azure Mobile Service], which will initiate a push toohello mobile apps) does not receive messages directly from hello backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend tooreceive messages from one or more backend systems.</span></span> <span data-ttu-id="1b0ea-119">Раздел служебной шины должен toobe, созданные для каждого hello серверной систем, например, учетная запись, ч, процент, который по сути являются «разделы» интерес, в которой будет инициировать toobe сообщений, отправленных как push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-119">A Service Bus Topic needs toobe created for each of hello backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages toobe sent as push notification.</span></span> <span data-ttu-id="1b0ea-120">Hello серверных системах будет отправлять сообщения toothese разделы.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-120">hello backend systems will send messages toothese topics.</span></span> <span data-ttu-id="1b0ea-121">Серверной части мобильных устройств можно подписаться tooone или более такие темы, создавая подписку служебной шины.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-121">A Mobile Backend can subscribe tooone or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="1b0ea-122">Это будет оформлять tooreceive мобильной серверной части hello уведомления от соответствующей серверной системе hello.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-122">This will entitle hello mobile backend tooreceive a notification from hello corresponding backend system.</span></span> <span data-ttu-id="1b0ea-123">Мобильной серверной части продолжает toolisten для сообщений в своих подписках и сразу же при поступлении сообщения, он включает обратно и отправляет его в качестве концентратора уведомлений tooits уведомления.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-123">Mobile backend continues toolisten for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification tooits notification hub.</span></span> <span data-ttu-id="1b0ea-124">Затем концентраторы уведомлений со временем доставляет сообщение hello: toohello мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-124">Notification hubs then eventually delivers hello message toohello mobile app.</span></span> <span data-ttu-id="1b0ea-125">Поэтому toosummarize hello ключевые компоненты, у нас есть:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-125">So toosummarize hello key components, we have:</span></span>

1. <span data-ttu-id="1b0ea-126">Серверные системы (бизнес-системы или устаревшие системы)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="1b0ea-127">Создает раздел Service Bus</span><span class="sxs-lookup"><span data-stu-id="1b0ea-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="1b0ea-128">Отправляет сообщение</span><span class="sxs-lookup"><span data-stu-id="1b0ea-128">Sends Message</span></span>
2. <span data-ttu-id="1b0ea-129">Серверная часть мобильной службы</span><span class="sxs-lookup"><span data-stu-id="1b0ea-129">Mobile backend</span></span>
   * <span data-ttu-id="1b0ea-130">Создает подписку на службу</span><span class="sxs-lookup"><span data-stu-id="1b0ea-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="1b0ea-131">Получает сообщение (из серверной системы)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="1b0ea-132">Отправляет уведомление tooclients (через концентратор уведомлений Azure)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-132">Sends notification tooclients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="1b0ea-133">Мобильное приложение</span><span class="sxs-lookup"><span data-stu-id="1b0ea-133">Mobile Application</span></span>
   * <span data-ttu-id="1b0ea-134">Получает и отображает уведомление</span><span class="sxs-lookup"><span data-stu-id="1b0ea-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="1b0ea-135">Преимущества:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-135">Benefits:</span></span>
1. <span data-ttu-id="1b0ea-136">Hello разделения между отправителя (серверной части системы) и hello получателя (мобильное приложение или служба через концентратор уведомлений) позволяет дополнительных серверных системах интегрированы с минимальными изменениями.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-136">hello decoupling between hello receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="1b0ea-137">Эта возможность также упрощает сценарии hello несколько мобильных приложений, могут tooreceive события из одного или нескольких систем баз.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-137">This also makes hello scenario of multiple mobile apps being able tooreceive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="1b0ea-138">Пример:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="1b0ea-139">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1b0ea-139">Prerequisites</span></span>
<span data-ttu-id="1b0ea-140">Следует выполнить следующие учебники toofamiliarize hello концепции, а также общие шаги создания и настройки hello:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-140">You should complete hello following tutorials toofamiliarize with hello concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="1b0ea-141">[программирование Service Bus Pub/Sub] -это объясняет hello подробные сведения о работе с Service Bus разделов и подписок, как toocreate пространства имен toocontain разделов и подписок, как toosend & получения сообщений от них.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-141">[Service Bus Pub/Sub programming] - This explains hello details of working with Service Bus Topics/Subscriptions, how toocreate a namespace toocontain topics/subscriptions, how toosend & receive messages from them.</span></span>
2. <span data-ttu-id="1b0ea-142">[Концентраторы уведомлений - универсальное приложение для Windows учебника] -это объясняет, как tooset Настройка приложения для магазина Windows и использовать tooregister концентраторов уведомлений и затем получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-142">[Notification Hubs - Windows Universal tutorial] - This explains how tooset up a Windows Store app and use Notification Hubs tooregister and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="1b0ea-143">Пример кода</span><span class="sxs-lookup"><span data-stu-id="1b0ea-143">Sample code</span></span>
<span data-ttu-id="1b0ea-144">Полный образец кода Hello доступен на [образцов концентратора уведомлений о].</span><span class="sxs-lookup"><span data-stu-id="1b0ea-144">hello full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="1b0ea-145">Он состоит из трех компонентов:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-145">It is split into three components:</span></span>

1. <span data-ttu-id="1b0ea-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="1b0ea-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="1b0ea-147">а.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-147">a.</span></span> <span data-ttu-id="1b0ea-148">Этот проект использует hello *WindowsAzure.ServiceBus* пакета Nuget и основан на [программирование Service Bus Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="1b0ea-148">This project uses hello *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="1b0ea-149">b.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-149">b.</span></span> <span data-ttu-id="1b0ea-150">Это простой C# консольного приложения toosimulate бизнес-системе, которая инициирует toobe сообщение hello доставить toohello мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-150">This is a simple C# console app toosimulate an LoB system which initiates hello message toobe delivered toohello mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="1b0ea-151">c.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-151">c.</span></span> <span data-ttu-id="1b0ea-152">`CreateTopic`— раздел служебной шины используется toocreate hello, где будет отправлять сообщения.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-152">`CreateTopic` is used toocreate hello Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="1b0ea-153">d.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-153">d.</span></span> <span data-ttu-id="1b0ea-154">`SendMessage`— toothis сообщений hello используется toosend шины обслуживания.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-154">`SendMessage` is used toosend hello messages toothis Service Bus Topic.</span></span> <span data-ttu-id="1b0ea-155">Здесь мы просто отправляют набор сообщений произвольного toohello раздела периодически hello цель образца hello.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-155">Here we are simply sending a set of random messages toohello topic periodically for hello purpose of hello sample.</span></span> <span data-ttu-id="1b0ea-156">Как правило эту функцию будет выполнять серверная система, которая будет отправлять сообщения при наступлении события.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
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
2. <span data-ttu-id="1b0ea-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="1b0ea-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="1b0ea-158">а.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-158">a.</span></span> <span data-ttu-id="1b0ea-159">Этот проект использует hello *WindowsAzure.ServiceBus* и *Microsoft.Web.WebJobs.Publish* Nuget пакеты и на основе [программирование Service Bus Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="1b0ea-159">This project uses hello *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="1b0ea-160">b.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-160">b.</span></span> <span data-ttu-id="1b0ea-161">Это другой консольное приложение C#, который будет запущен как [веб-задания Azure] так как он содержит toorun постоянно toolisten для сообщений из hello LoB и серверных системах.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-161">This is another C# console app which we will run as an [Azure WebJob] since it has toorun continuously toolisten for messages from hello LoB/backend systems.</span></span> <span data-ttu-id="1b0ea-162">Оно будет входить в состав серверной части мобильной службы.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="1b0ea-163">c.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-163">c.</span></span> <span data-ttu-id="1b0ea-164">`CreateSubscription`— используется toocreate подписки служебной шины для раздела hello где hello серверной системе будет отправлять сообщения.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-164">`CreateSubscription` is used toocreate a Service Bus subscription for hello topic where hello backend system will send messages.</span></span> <span data-ttu-id="1b0ea-165">В зависимости от бизнес-сценария hello этот компонент будет создать одну или несколько подписок toocorresponding разделы (например, некоторые получают сообщения из системы отдела Кадров, некоторые из системы Финансы и т. д)</span><span class="sxs-lookup"><span data-stu-id="1b0ea-165">Depending on hello business scenario, this component will create one or more subscriptions toocorresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="1b0ea-166">d.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-166">d.</span></span> <span data-ttu-id="1b0ea-167">ReceiveMessageAndSendNotification сообщение hello используется tooread из раздела hello, с помощью своей подписки, при успешном выполнении hello чтения затем создать toohello toobe отправляются уведомления (в сценарии образец hello собственного всплывающего уведомления Windows) мобильных устройств приложение с использованием концентраторов уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-167">ReceiveMessageAndSendNotification is used tooread hello message from hello topic using its subscription and if hello read is successful then craft a notification (in hello sample scenario a Windows native toast notification) toobe sent toohello mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
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
   
    <span data-ttu-id="1b0ea-168">д.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-168">e.</span></span> <span data-ttu-id="1b0ea-169">Для публикации его в виде **веб-задания**, щелкните правой кнопкой мыши hello решения в Visual Studio и выберите **опубликовать как веб-задания**</span><span class="sxs-lookup"><span data-stu-id="1b0ea-169">For publishing this as a **WebJob**, right click on hello solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="1b0ea-170">f.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-170">f.</span></span> <span data-ttu-id="1b0ea-171">Выберите ваш профиль публикации и создания нового веб-сайта Azure, если он не существует, который будет размещаться этот веб-задания, и при наличии hello веб-сайт, затем **публикации**.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have hello WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="1b0ea-172">ж.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-172">g.</span></span> <span data-ttu-id="1b0ea-173">Настройка toobe задания hello «Запустите постоянно», чтобы при входе в toohello [классический портал Azure] вы увидите примерно hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-173">Configure hello job toobe "Run Continuously" so that when you log in toohello [Azure Classic Portal] you should see something like hello following:</span></span>
   
    ![][4]
3. <span data-ttu-id="1b0ea-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="1b0ea-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="1b0ea-175">а.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-175">a.</span></span> <span data-ttu-id="1b0ea-176">Это приложение магазина Windows, который будет получать всплывающие уведомления hello запуск веб-задания в рамках серверной части мобильных устройств и отобразить ее.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-176">This is a Windows Store application which will receive toast notifications from hello WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="1b0ea-177">Оно основано на материале [Концентраторы уведомлений - универсальное приложение для Windows учебника].</span><span class="sxs-lookup"><span data-stu-id="1b0ea-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="1b0ea-178">b.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-178">b.</span></span> <span data-ttu-id="1b0ea-179">Убедитесь, что приложение включен tooreceive всплывающие уведомления.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-179">Ensure that your application is enabled tooreceive toast notifications.</span></span>
   
    <span data-ttu-id="1b0ea-180">c.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-180">c.</span></span> <span data-ttu-id="1b0ea-181">Убедитесь, что hello, следующий код регистрации концентраторов уведомлений вызывается при запуске приложения hello (после замены hello *HubName* и *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-181">Ensure that hello following Notification Hubs registration code is being called at hello App start up (after replacing hello *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="1b0ea-182">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="1b0ea-182">Running sample:</span></span>
1. <span data-ttu-id="1b0ea-183">Убедитесь, что веб-задание выполняется успешно и запланированные слишком «запуск постоянно».</span><span class="sxs-lookup"><span data-stu-id="1b0ea-183">Ensure that your WebJob is running successfully and scheduled too"Run Continuously".</span></span>
2. <span data-ttu-id="1b0ea-184">Запустите hello **EnterprisePushMobileApp** , чтобы запустить приложение для магазина Windows hello.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-184">Run hello **EnterprisePushMobileApp** which will start hello Windows Store app.</span></span>
3. <span data-ttu-id="1b0ea-185">Запустите hello **EnterprisePushBackendSystem** консольного приложения, который имитирует серверной LoB hello и будет начать отправку сообщения, и вы увидите всплывающие уведомления отображаются hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-185">Run hello **EnterprisePushBackendSystem** console application which will simulate hello LoB backend and will start sending messages and you should see toast notifications appearing like hello following:</span></span>
   
    ![][5]
4. <span data-ttu-id="1b0ea-186">сообщения приветствия изначально были отправлены tooService разделы шины, которые было находится под наблюдением подписках Service Bus в веб-задания.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-186">hello messages were originally sent tooService Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="1b0ea-187">Если получено сообщение, уведомление был создан и отправлен toohello мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="1b0ea-187">Once a message was received, a notification was created and sent toohello mobile app.</span></span> <span data-ttu-id="1b0ea-188">Можно просмотреть журналы веб-задания tooconfirm hello обработку при переходе toohello журналы ссылку в hello [классический портал Azure] для веб-задания:</span><span class="sxs-lookup"><span data-stu-id="1b0ea-188">You can look through hello WebJob logs tooconfirm hello processing when you go toohello Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[образцов концентратора уведомлений о]: https://github.com/Azure/azure-notificationhubs-samples
[мобильных служб Azure]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[программирование Service Bus Pub/Sub]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[веб-задания Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[Концентраторы уведомлений - универсальное приложение для Windows учебника]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[классический портал Azure]: https://manage.windowsazure.com/
