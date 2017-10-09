<span data-ttu-id="3f8ba-101">В этом разделе будет обновить код в вашей существующей toosend серверной части проекта мобильным приложениям push-уведомлений, каждый раз при добавлении нового элемента.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="3f8ba-102">Это работает на основе hello [шаблона](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) функции концентраторов уведомлений Azure, включение кросс платформенных Push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="3f8ba-103">Hello различных клиентов регистрируются push-уведомления с помощью шаблонов, и отдельной принудительной универсальной можно получить tooall клиентских платформ.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="3f8ba-104">Выберите один из hello следующих процедур, соответствующую типу вашего проекта серверной части&mdash;либо [.NET серверной части](#dotnet) или [Node.js серверной части](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="3f8ba-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="3f8ba-105"><a name="dotnet"></a>Серверный проект .NET</span><span class="sxs-lookup"><span data-stu-id="3f8ba-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="3f8ba-106">В Visual Studio, щелкните правой кнопкой мыши проект сервера hello и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="3f8ba-107">Найдите `Microsoft.Azure.NotificationHubs` и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="3f8ba-108">При этом устанавливаются библиотеки hello концентраторы уведомлений для отправки уведомлений из вашей серверной части.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="3f8ba-109">В проекте сервера hello откройте **контроллеров** > **TodoItemController.cs**и добавьте следующее hello операторы using:</span><span class="sxs-lookup"><span data-stu-id="3f8ba-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="3f8ba-110">В hello **PostTodoItem** метод, добавьте следующий код после вызова hello слишком hello**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="3f8ba-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

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

    <span data-ttu-id="3f8ba-111">Это приведет к отправке уведомления шаблона, содержащей элемент hello. Текст при вставке нового элемента.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="3f8ba-112">Повторная публикация проекта сервера hello.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-112">Republish hello server project.</span></span>

### <span data-ttu-id="3f8ba-113"><a name="nodejs"></a>Серверный проект Node.js</span><span class="sxs-lookup"><span data-stu-id="3f8ba-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="3f8ba-114">Если вы еще не сделали этого, [загрузите проект серверной части краткого руководства hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), или в противном случае используйте hello [интерактивном редакторе в hello портал Azure](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="3f8ba-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="3f8ba-115">Замените существующий код hello в todoitem.js hello следующее:</span><span class="sxs-lookup"><span data-stu-id="3f8ba-115">Replace hello existing code in todoitem.js with hello following:</span></span>

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

    <span data-ttu-id="3f8ba-116">Это приведет к отправке уведомления шаблона, содержащий hello item.text при вставке нового элемента.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="3f8ba-117">При редактировании файла hello на локальном компьютере повторно опубликуйте проект сервера hello.</span><span class="sxs-lookup"><span data-stu-id="3f8ba-117">When editing hello file on your local computer, republish hello server project.</span></span>
