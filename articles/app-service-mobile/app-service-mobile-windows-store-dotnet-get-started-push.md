---
title: "принудительные уведомления aaaAdd tooyour-приложения универсальной платформы Windows (UWP) | Документы Microsoft"
description: "Узнайте, как toouse мобильные приложения службы приложений Azure и концентраторов уведомлений Azure toosend push-уведомления tooyour универсальной платформы Windows (UWP) приложения."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a>Добавление приложения Windows tooyour уведомлений push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Обзор
В этом учебнике добавить push уведомления toohello [краткое руководство по Windows](app-service-mobile-windows-store-dotnet-get-started.md) проекта, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.

Если вы не используете hello загружен проект быстрый запуск сервера, будет необходимо hello пакета расширения уведомлений push. В разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) для получения дополнительной информации.

## <a name="configure-hub"></a>Настройка концентратора уведомлений
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>Регистрация приложения для работы с push-уведомлениями
Требуется toosubmit toohello вашего приложения магазина Windows, а затем настроить toointegrate проекта на сервере с принудительной отправкой toosend Windows Notification Service (WNS).

1. В обозревателе решений Visual Studio, щелкните правой кнопкой мыши проект приложения hello UWP, щелкните **хранилища** > **связать приложение с hello хранилища...** .

    ![Связь приложения с Магазином Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. В мастере приветствия щелкните **Далее**, войти в учетную запись Майкрософт, введите имя приложения в **зарезервировать новое имя приложения**, нажмите кнопку **резерва**.
3. После регистрации приложения hello hello успешно создан, выберите новое имя приложения, нажмите кнопку **Далее**, а затем нажмите кнопку **связать**. Это добавляет манифест приложения toohello сведения о регистрации требуется hello магазина Windows.  
4. Перейдите toohello [центра разработчиков Windows](https://dev.windows.com/en-us/overview)вход с учетной записью Майкрософт, нажмите кнопку Регистрация нового приложения hello в **Мои приложения**, затем разверните **службы**  >  **Push-уведомления**.
5. В hello **Push-уведомления** щелкните **узла службы Live** под **мобильных служб Microsoft Azure**.
6. На странице регистрации hello, запишите значение hello в **секреты приложения** и hello **ИД безопасности пакета**, который затем используется tooconfigure серверной части мобильных приложений.

    ![Связь приложения с Магазином Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > Hello секрета клиента и ИД безопасности пакета являются важными элементами обеспечения безопасности. Не сообщайте никому эти значения и не распространяйте их вместе со своим приложением. Hello **идентификатор приложения** с проверки подлинности учетной записи Майкрософт секретный tooconfigure hello.
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>Настройка внутреннего toosend hello push-уведомлений
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>Обновление сервера toosend hello push-уведомлений
Процедура hello ниже, соответствующую типу вашего внутреннего проекта&mdash;либо [серверное приложение .NET](#dotnet) или [Node.js серверной](#nodejs).

### <a name="dotnet"></a>Серверный проект .NET
1. В Visual Studio, щелкните правой кнопкой мыши проект сервера hello и нажмите кнопку **управление пакетами NuGet**, поиск Microsoft.Azure.NotificationHubs, а затем нажмите кнопку **установить**. При этом устанавливаются hello концентраторы уведомлений клиентской библиотеки.
2. Разверните **контроллеров**откройте TodoItemController.cs и добавьте следующее hello операторы using:

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

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Этот код показывает toosend концентратора уведомлений hello push-уведомление после вставки нового элемента.
4. Повторная публикация проекта сервера hello.

### <a name="nodejs"></a>Серверный проект Node.js
1. Если вы еще не сделали этого, [загрузите проект краткое руководство hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) или в противном случае используйте hello [интерактивном редакторе в hello портал Azure](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Замените существующий код hello в файле todoitem.js hello hello следующее:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
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

    Это отправляет всплывающее уведомление WNS, содержащий hello item.text при вставке нового элемента todo.
3. При редактировании файла hello на локальном компьютере повторно опубликуйте проект сервера hello.

## <a id="update-app"></a>Добавить приложение tooyour уведомлений push
Затем приложение необходимо зарегистрировать для получения push-уведомлений при запуске. Уже включена аутентификация, убедитесь в том, что hello пользователь выполняет вход перед попыткой tooregister push-уведомления.

1. Откройте hello **App.xaml.cs** файл проекта и добавьте следующее hello `using` инструкции:

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. В hello того же файла, добавьте следующее hello **InitNotificationsAsync** toohello определение метода **приложения** класса:

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    Этот код извлекает из WNS hello ChannelURI для приложения hello и затем выполняется регистрация, ChannelURI приложение мобильного приложения службы.
3. Вверху hello hello **OnLaunched** обработчик событий в **App.xaml.cs**, добавить hello **async** определение метода toohello модификатор и добавьте hello следующий вызов toohello новый  **InitNotificationsAsync** методом, как следующий пример hello:

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    Это гарантирует, что приветствия кратковременных ChannelURI регистрируется при каждом запуске приложения hello.
4. Перестройте проект приложения UWP. Приложение больше не готов tooreceive всплывающие уведомления.

## <a id="test"></a>Тестирование push-уведомлений в приложении
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>Дальнейшие действия
Дополнительные сведения о push-уведомлениях:

* [Управление toouse hello клиента для мобильных приложений Azure](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  Шаблоны обеспечивают гибкость toosend кросс платформенных Push-уведомлений, а также локализованные Push-уведомлений. Узнайте, как шаблоны tooregister.
* [Диагностика неполадок, связанных с push-уведомлениями](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Существуют различные причины, по которым уведомления могут теряться или не доходить до устройств. В этом разделе показано, как tooanalyze и выясните, hello корневой причиной сбоев уведомлений push.

Рассмотрим, продолжая tooone из hello следующие учебники:

* [Добавить приложение tooyour проверки подлинности](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Узнайте, как пользователи tooauthenticate приложения с поставщиком удостоверений.
* [Включение автономной синхронизации для приложения](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Узнайте, как автономные tooadd поддерживают приложения с помощью внутреннего сервера мобильного приложения. Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения.

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
