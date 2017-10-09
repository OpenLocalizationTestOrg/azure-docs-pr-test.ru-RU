



При отправке уведомления шаблона требуется tooprovide набор свойств, в нашем случае мы отправим hello набор свойств, содержащих hello локализованной версии hello текущих новостей, например:

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


В этом разделе показано, как toosend уведомления с помощью консольного приложения

Hello включены магазин Windows tooboth широковещательные пакеты кода и устройства iOS, так как внутренний hello выполнить рассылку tooany устройств hello поддерживается.

### <a name="toosend-notifications-using-a-c-console-app"></a>toosend уведомления с помощью консольного приложения C#
Изменение hello `SendTemplateNotificationAsync` метод в консольное приложение hello, созданный ранее с hello, следующий код. Обратите внимание, как в этом случае нет необходимости toosend несколько уведомлений для разных языков и платформ.

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


Обратите внимание на этот простой вызов будет доставлять слишком hello локализованные часть новостей**все** устройств, независимо от платформы hello как концентратор уведомлений сборки и доставляет hello правильные подписка устройств hello tooall собственного полезных данных tooa конкретного тега.

### <a name="sending-hello-notification-with-mobile-services"></a>Отправка уведомления hello с мобильными службами
В вашей мобильной службы планировщика можно использовать следующий скрипт hello:

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


