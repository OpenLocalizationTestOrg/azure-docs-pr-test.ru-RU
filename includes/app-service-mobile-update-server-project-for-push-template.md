<span data-ttu-id="b9d56-101">В этом разделе описывается обновление кода в существующем проекте серверной части мобильных приложений, которое позволит отправлять push-уведомления при каждом добавлении нового элемента.</span><span class="sxs-lookup"><span data-stu-id="b9d56-101">In this section, you update code in your existing Mobile Apps back-end project to send a push notification every time a new item is added.</span></span> <span data-ttu-id="b9d56-102">Это реализуется с помощью [шаблонов](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) Центров уведомлений, включая отправку push-уведомлений между разными платформами.</span><span class="sxs-lookup"><span data-stu-id="b9d56-102">This is powered by the [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="b9d56-103">Разные клиенты регистрируются для обмена push-уведомлениями с помощью шаблонов; одно такое универсальное push-уведомление можно получать на всех клиентских платформах.</span><span class="sxs-lookup"><span data-stu-id="b9d56-103">The various clients are registered for push notifications using templates, and a single universal push can get to all client platforms.</span></span>

<span data-ttu-id="b9d56-104">Выберите одну из процедур ниже, которая соответствует типу вашего серверного проекта: [серверный проект .NET](#dotnet) или [серверный проект Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="b9d56-104">Choose one of the following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="b9d56-105"><a name="dotnet"></a>Серверный проект .NET</span><span class="sxs-lookup"><span data-stu-id="b9d56-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="b9d56-106">В Visual Studio щелкните правой кнопкой мыши серверный проект и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b9d56-106">In Visual Studio, right-click the server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="b9d56-107">Найдите `Microsoft.Azure.NotificationHubs` и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="b9d56-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="b9d56-108">Это устанавливает библиотеку центров уведомлений для отправки уведомлений из серверной части.</span><span class="sxs-lookup"><span data-stu-id="b9d56-108">This installs the Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="b9d56-109">В серверном проекте откройте **Контроллеры** > **TodoItemController.cs** и добавьте следующие операторы using:</span><span class="sxs-lookup"><span data-stu-id="b9d56-109">In the server project, open **Controllers** > **TodoItemController.cs**, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="b9d56-110">В метод **PostTodoItem** добавьте следующий код после вызова **InsertAsync**.</span><span class="sxs-lookup"><span data-stu-id="b9d56-110">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>  

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending the message so that all template registrations that contain "messageParam"
        // will receive the notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added to the list.";

        try
        {
            // Send the push notification and log the results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="b9d56-111">При вставке нового элемента отправляется шаблонное уведомление, содержащее item.Text.</span><span class="sxs-lookup"><span data-stu-id="b9d56-111">This sends a template notification that contains the item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="b9d56-112">Повторная публикация серверного проекта</span><span class="sxs-lookup"><span data-stu-id="b9d56-112">Republish the server project.</span></span>

### <span data-ttu-id="b9d56-113"><a name="nodejs"></a>Серверный проект Node.js</span><span class="sxs-lookup"><span data-stu-id="b9d56-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="b9d56-114">При необходимости [скачайте серверный проект быстрого запуска](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) или воспользуйтесь [онлайн-редактором на портале Azure](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="b9d56-114">If you haven't already done so, [download the quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="b9d56-115">Замените существующий код в файле todoitem.js следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b9d56-115">Replace the existing code in todoitem.js with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="b9d56-116">При вставке нового элемента отправляется шаблонное уведомление, содержащее item.Text.</span><span class="sxs-lookup"><span data-stu-id="b9d56-116">This sends a template notification that contains the item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="b9d56-117">При редактировании этого файла на локальном компьютере повторно опубликуйте серверный проект.</span><span class="sxs-lookup"><span data-stu-id="b9d56-117">When editing the file on your local computer, republish the server project.</span></span>
