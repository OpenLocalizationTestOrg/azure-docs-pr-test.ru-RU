



<span data-ttu-id="5542d-101">При отправке уведомления шаблона требуется tooprovide набор свойств, в нашем случае мы отправим hello набор свойств, содержащих hello локализованной версии hello текущих новостей, например:</span><span class="sxs-lookup"><span data-stu-id="5542d-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="5542d-102">В этом разделе показано, как toosend уведомления с помощью консольного приложения</span><span class="sxs-lookup"><span data-stu-id="5542d-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="5542d-103">Hello включены магазин Windows tooboth широковещательные пакеты кода и устройства iOS, так как внутренний hello выполнить рассылку tooany устройств hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5542d-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="5542d-104">toosend уведомления с помощью консольного приложения C#</span><span class="sxs-lookup"><span data-stu-id="5542d-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="5542d-105">Изменение hello `SendTemplateNotificationAsync` метод в консольное приложение hello, созданный ранее с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="5542d-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="5542d-106">Обратите внимание, как в этом случае нет необходимости toosend несколько уведомлений для разных языков и платформ.</span><span class="sxs-lookup"><span data-stu-id="5542d-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


<span data-ttu-id="5542d-107">Обратите внимание на этот простой вызов будет доставлять слишком hello локализованные часть новостей**все** устройств, независимо от платформы hello как концентратор уведомлений сборки и доставляет hello правильные подписка устройств hello tooall собственного полезных данных tooa конкретного тега.</span><span class="sxs-lookup"><span data-stu-id="5542d-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="5542d-108">Отправка уведомления hello с мобильными службами</span><span class="sxs-lookup"><span data-stu-id="5542d-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="5542d-109">В вашей мобильной службы планировщика можно использовать следующий скрипт hello:</span><span class="sxs-lookup"><span data-stu-id="5542d-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


