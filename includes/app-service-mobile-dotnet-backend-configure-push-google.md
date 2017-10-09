<span data-ttu-id="dbc19-101">Используйте процедуру hello, соответствующую типу вашего проекта серверной части&mdash;либо [.NET серверной части](#dotnet) или [Node.js серверной части](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="dbc19-101">Use hello procedure that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="dbc19-102"><a name="dotnet"></a>Серверный проект .NET</span><span class="sxs-lookup"><span data-stu-id="dbc19-102"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="dbc19-103">В Visual Studio, щелкните правой кнопкой мыши проект сервера hello и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="dbc19-103">In Visual Studio, right-click hello server project, and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="dbc19-104">Найдите `Microsoft.Azure.NotificationHubs` и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="dbc19-104">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="dbc19-105">При этом устанавливаются hello концентраторы уведомлений клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="dbc19-105">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="dbc19-106">В папке Controllers hello откройте TodoItemController.cs и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="dbc19-106">In hello Controllers folder, open TodoItemController.cs and add hello following `using` statements:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. <span data-ttu-id="dbc19-107">Замените hello `PostTodoItem` метод с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="dbc19-107">Replace hello `PostTodoItem` method with hello following code:</span></span>  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
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

            // Android payload
            var androidNotificationPayload = "{ \"data\" : {\"message\":\"" + item.Text + "\"}}";

            try
            {
                // Send hello push notification and log hello results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write hello success result toohello logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write hello failure result toohello logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. <span data-ttu-id="dbc19-108">Повторная публикация проекта сервера hello.</span><span class="sxs-lookup"><span data-stu-id="dbc19-108">Republish hello server project.</span></span>

### <span data-ttu-id="dbc19-109"><a name="nodejs"></a>Серверный проект Node.js</span><span class="sxs-lookup"><span data-stu-id="dbc19-109"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="dbc19-110">Если вы еще не сделали этого, [загрузите проект краткое руководство hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), или в противном случае используйте hello [интерактивном редакторе в hello портал Azure](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="dbc19-110">If you haven't already done so, [download hello quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="dbc19-111">Замените существующий код hello в файле todoitem.js hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="dbc19-111">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a GCM native notification.
                    context.push.gcm.send(null, payload, function (error) {
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

    <span data-ttu-id="dbc19-112">Это отправляет уведомление GCM, содержащий hello item.text при вставке нового элемента todo.</span><span class="sxs-lookup"><span data-stu-id="dbc19-112">This sends a GCM notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="dbc19-113">При редактировании файла hello в локальном компьютере повторно опубликуйте проект сервера hello.</span><span class="sxs-lookup"><span data-stu-id="dbc19-113">When editing hello file in your local computer, republish hello server project.</span></span>
