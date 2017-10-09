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
# <a name="enterprise-push-architectural-guidance"></a>Руководство по архитектуре push-уведомлений
Компании сегодня переходят постепенно по созданию мобильных приложений, либо для конечных пользователей (внешний) или для сотрудников hello (внутренний). Они имеют существующие серверной системы на месте будь то мэйнфреймы или некоторые бизнес-приложений, которые должны быть интегрированы в hello архитектуру приложений для мобильных устройств. В этом руководстве поговорим об оптимальном способе toodo такой интеграции, рекомендующее toocommon сценарии из возможных решений.

Часто требуется для Отправка push-уведомления toohello пользователей с помощью своих мобильных приложений, при возникновении события интерес в серверных системах hello. Например:  Банк, имеющему приложения hello bank банковских операций для своего iPhone клиенту уведомление при дебета превышают определенный объем из своей учетной записи или интрасети, где сотрудник из финансового отдела с приложении утверждения бюджет на его Windows Phone хочет toobe toobe уведомление, когда он получает запрос на утверждение.

Hello банковского счета или утверждения обработки является toobe скорее всего, в некоторых серверной системе, в которой необходимо инициировать пользователь toohello push. Может существовать несколько внутренних системах, которые должны все сборки hello разный принудительной tooimplement логики, при возникновении события уведомления. Hello сложность здесь заключается в интеграции несколько серверных системах вместе с отдельной принудительной системы, где hello конечные пользователи могут подписаны toodifferent уведомления и может существовать даже быть несколько мобильных приложений, например в случае, когда hello мобильные приложения интрасети где одного мобильного приложения может потребоваться уведомления tooreceive несколько таких систем баз. Hello серверных системах не знать, и требуется tooknow принудительной семантику и технологии, поэтому распространенное решение традиционно была toointroduce компонентом опрашивает hello серверных системах на наличие событий, представляющие интерес и отвечает за отправку сообщений hello push Клиент toohello.
Здесь мы поговорим о решение еще лучше, с помощью шины обслуживания Azure — модель раздела или подписки, которая позволяет снизить сложность hello сделана масштабируемых решений hello.

Вот hello общая архитектура решения hello (общего для нескольких мобильных приложений, но одинаково применимы, если имеется только одно мобильное приложение)

## <a name="architecture"></a>Архитектура
![][1]

ключевыми являются Hello в этом Архитектурная схема является Azure Service Bus, который предоставляет модель программирования разделов и подписок (на его в параметре [программирование Service Bus Pub/Sub]). Hello получателем, что в данном случае является hello мобильного внутреннего сервера (обычно [мобильных служб Azure], которой будет инициировать принудительную toohello мобильных приложений) не принимать сообщения непосредственно из hello серверных системах, но вместо этого у нас есть Абстрактный промежуточный уровень [Azure Service Bus] позволяющее мобильной серверной части tooreceive сообщения из одного или нескольких серверных системах. Раздел служебной шины должен toobe, созданные для каждого hello серверной систем, например, учетная запись, ч, процент, который по сути являются «разделы» интерес, в которой будет инициировать toobe сообщений, отправленных как push-уведомлений. Hello серверных системах будет отправлять сообщения toothese разделы. Серверной части мобильных устройств можно подписаться tooone или более такие темы, создавая подписку служебной шины. Это будет оформлять tooreceive мобильной серверной части hello уведомления от соответствующей серверной системе hello. Мобильной серверной части продолжает toolisten для сообщений в своих подписках и сразу же при поступлении сообщения, он включает обратно и отправляет его в качестве концентратора уведомлений tooits уведомления. Затем концентраторы уведомлений со временем доставляет сообщение hello: toohello мобильного приложения. Поэтому toosummarize hello ключевые компоненты, у нас есть:

1. Серверные системы (бизнес-системы или устаревшие системы)
   * Создает раздел Service Bus
   * Отправляет сообщение
2. Серверная часть мобильной службы
   * Создает подписку на службу
   * Получает сообщение (из серверной системы)
   * Отправляет уведомление tooclients (через концентратор уведомлений Azure)
3. Мобильное приложение
   * Получает и отображает уведомление

### <a name="benefits"></a>Преимущества:
1. Hello разделения между отправителя (серверной части системы) и hello получателя (мобильное приложение или служба через концентратор уведомлений) позволяет дополнительных серверных системах интегрированы с минимальными изменениями.
2. Эта возможность также упрощает сценарии hello несколько мобильных приложений, могут tooreceive события из одного или нескольких систем баз.  

## <a name="sample"></a>Пример:
### <a name="prerequisites"></a>Предварительные требования
Следует выполнить следующие учебники toofamiliarize hello концепции, а также общие шаги создания и настройки hello:

1. [программирование Service Bus Pub/Sub] -это объясняет hello подробные сведения о работе с Service Bus разделов и подписок, как toocreate пространства имен toocontain разделов и подписок, как toosend & получения сообщений от них.
2. [Концентраторы уведомлений - универсальное приложение для Windows учебника] -это объясняет, как tooset Настройка приложения для магазина Windows и использовать tooregister концентраторов уведомлений и затем получать уведомления.

### <a name="sample-code"></a>Пример кода
Полный образец кода Hello доступен на [образцов концентратора уведомлений о]. Он состоит из трех компонентов:

1. **EnterprisePushBackendSystem**
   
    а. Этот проект использует hello *WindowsAzure.ServiceBus* пакета Nuget и основан на [программирование Service Bus Pub/Sub].
   
    b. Это простой C# консольного приложения toosimulate бизнес-системе, которая инициирует toobe сообщение hello доставить toohello мобильного приложения.
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`— раздел служебной шины используется toocreate hello, где будет отправлять сообщения.
   
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
   
    d. `SendMessage`— toothis сообщений hello используется toosend шины обслуживания. Здесь мы просто отправляют набор сообщений произвольного toohello раздела периодически hello цель образца hello. Как правило эту функцию будет выполнять серверная система, которая будет отправлять сообщения при наступлении события.
   
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
2. **ReceiveAndSendNotification**
   
    а. Этот проект использует hello *WindowsAzure.ServiceBus* и *Microsoft.Web.WebJobs.Publish* Nuget пакеты и на основе [программирование Service Bus Pub/Sub].
   
    b. Это другой консольное приложение C#, который будет запущен как [веб-задания Azure] так как он содержит toorun постоянно toolisten для сообщений из hello LoB и серверных системах. Оно будет входить в состав серверной части мобильной службы.
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`— используется toocreate подписки служебной шины для раздела hello где hello серверной системе будет отправлять сообщения. В зависимости от бизнес-сценария hello этот компонент будет создать одну или несколько подписок toocorresponding разделы (например, некоторые получают сообщения из системы отдела Кадров, некоторые из системы Финансы и т. д)
   
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
   
    d. ReceiveMessageAndSendNotification сообщение hello используется tooread из раздела hello, с помощью своей подписки, при успешном выполнении hello чтения затем создать toohello toobe отправляются уведомления (в сценарии образец hello собственного всплывающего уведомления Windows) мобильных устройств приложение с использованием концентраторов уведомлений Azure.
   
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
   
    д. Для публикации его в виде **веб-задания**, щелкните правой кнопкой мыши hello решения в Visual Studio и выберите **опубликовать как веб-задания**
   
    ![][2]
   
    f. Выберите ваш профиль публикации и создания нового веб-сайта Azure, если он не существует, который будет размещаться этот веб-задания, и при наличии hello веб-сайт, затем **публикации**.
   
    ![][3]
   
    ж. Настройка toobe задания hello «Запустите постоянно», чтобы при входе в toohello [классический портал Azure] вы увидите примерно hello следующим образом:
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    а. Это приложение магазина Windows, который будет получать всплывающие уведомления hello запуск веб-задания в рамках серверной части мобильных устройств и отобразить ее. Оно основано на материале [Концентраторы уведомлений - универсальное приложение для Windows учебника].  
   
    b. Убедитесь, что приложение включен tooreceive всплывающие уведомления.
   
    c. Убедитесь, что hello, следующий код регистрации концентраторов уведомлений вызывается при запуске приложения hello (после замены hello *HubName* и *DefaultListenSharedAccessSignature*:
   
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

### <a name="running-sample"></a>Запуск примера
1. Убедитесь, что веб-задание выполняется успешно и запланированные слишком «запуск постоянно».
2. Запустите hello **EnterprisePushMobileApp** , чтобы запустить приложение для магазина Windows hello.
3. Запустите hello **EnterprisePushBackendSystem** консольного приложения, который имитирует серверной LoB hello и будет начать отправку сообщения, и вы увидите всплывающие уведомления отображаются hello следующим образом:
   
    ![][5]
4. сообщения приветствия изначально были отправлены tooService разделы шины, которые было находится под наблюдением подписках Service Bus в веб-задания. Если получено сообщение, уведомление был создан и отправлен toohello мобильного приложения. Можно просмотреть журналы веб-задания tooconfirm hello обработку при переходе toohello журналы ссылку в hello [классический портал Azure] для веб-задания:
   
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
