В этом разделе будет обновить код в вашей существующей toosend серверной части проекта мобильным приложениям push-уведомлений, каждый раз при добавлении нового элемента. Это работает на основе hello [шаблона](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) функции концентраторов уведомлений Azure, включение кросс платформенных Push-уведомлений. Hello различных клиентов регистрируются push-уведомления с помощью шаблонов, и отдельной принудительной универсальной можно получить tooall клиентских платформ.

Выберите один из hello следующих процедур, соответствующую типу вашего проекта серверной части&mdash;либо [.NET серверной части](#dotnet) или [Node.js серверной части](#nodejs).

### <a name="dotnet"></a>Серверный проект .NET
1. В Visual Studio, щелкните правой кнопкой мыши проект сервера hello и нажмите кнопку **управление пакетами NuGet**. Найдите `Microsoft.Azure.NotificationHubs` и нажмите кнопку **Установить**. При этом устанавливаются библиотеки hello концентраторы уведомлений для отправки уведомлений из вашей серверной части.
2. В проекте сервера hello откройте **контроллеров** > **TodoItemController.cs**и добавьте следующее hello операторы using:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. В hello **PostTodoItem** метод, добавьте следующий код после вызова hello слишком hello**InsertAsync**:  

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Это приведет к отправке уведомления шаблона, содержащей элемент hello. Текст при вставке нового элемента.
4. Повторная публикация проекта сервера hello.

### <a name="nodejs"></a>Серверный проект Node.js
1. Если вы еще не сделали этого, [загрузите проект серверной части краткого руководства hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), или в противном случае используйте hello [интерактивном редакторе в hello портал Azure](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Замените существующий код hello в todoitem.js hello следующее:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    Это приведет к отправке уведомления шаблона, содержащий hello item.text при вставке нового элемента.
3. При редактировании файла hello на локальном компьютере повторно опубликуйте проект сервера hello.
