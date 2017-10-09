---
title: "aaaSending push-уведомлений с концентраторами уведомлений Azure на Windows Phone | Документы Microsoft"
description: "В этом учебнике вы узнаете, как уведомления toopush концентраторов уведомлений Azure toouse tooa Windows Phone 8 или приложения Windows Phone 8.1 Silverlight."
services: notification-hubs
documentationcenter: windows
keywords: "push-уведомление, push-уведомление, push-уведомление windows phone"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Отправка push-уведомлений в приложения Windows Phone с помощью центров уведомлений Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Обзор
> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).
> 
> 

Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa: приложения Windows Phone 8 или Windows Phone 8.1 Silverlight. Если вы используете Windows Phone 8.1 (отличных от Silverlight), а затем ссылаться toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) версии.
В этом учебнике создается пустого приложения Windows Phone 8, получающий push-уведомления с помощью hello Microsoft Push Notification Service (MPNS). После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения.

> [!NOTE]
> пакет SDK для Windows Phone концентраторы уведомлений Hello не поддерживает использование hello Windows Push Notification Service (WNS) с приложениями Silverlight 8.1 Windows Phone. toouse WNS (вместо MPNS) с приложениями Silverlight 8.1 Windows Phone, выполните hello [концентраторы уведомлений — Windows Phone Silverlight учебника], которая использует API-интерфейс REST.
> 
> 

Hello учебник демонстрирует простой сценарий широковещательных hello в с использованием концентраторов уведомлений.

## <a name="prerequisites"></a>Предварительные требования
Этот учебник требует hello следующее:

* [Microsoft Visual Studio 2012 Express для Windows Phone]или более поздняя версия.

Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными Центрам уведомлений для приложений Windows Phone 8.

## <a name="create-your-notification-hub"></a>Создание центра уведомлений
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Щелкните hello <b>служб Notification Services</b> раздела (в пределах <i>параметры</i>), щелкните <b>Windows Phone (MPNS)</b> и нажмите кнопку hello <b>включить push без проверки подлинности </b> флажок.</p>
</li>
</ol>

&emsp;&emsp;![Azure Portal — включение push-уведомлений без проверки подлинности](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

Концентратор больше не была создана и настроена toosend не прошедшие проверку подлинности уведомления для Windows Phone.

> [!NOTE]
> В этом учебнике используется MPNS в режиме без проверки подлинности. Режим без проверки подлинности MPNS поставляется с ограничения на уведомления, можно отправить tooeach канала. Концентраторы уведомлений поддерживает [режиме с проверкой подлинности MPNS](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) , позволяя tooupload свой сертификат.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>Подключение приложения toohello концентратор уведомлений
1. В Visual Studio создайте новое консольное приложение Windows Phone 8.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    В Visual Studio 2013 с обновлением 2 вместо этого вы создаете приложение Windows Phone Silverlight.
   
    ![Visual Studio — новый проект — пустое приложение — Windows Phone Silverlight][11]
2. В Visual Studio, щелкните правой кнопкой мыши решение hello и нажмите кнопку **управление пакетами NuGet**.
   
    При этом отображаются hello **управление пакетами NuGet** диалоговое окно.
3. Поиск `WindowsAzure.Messaging.Managed` и нажмите кнопку **установить**, а затем примите условия использования hello.
   
    ![Visual Studio — диспетчер пакетов NuGet][20]
   
    Это загружает устанавливает и добавляет библиотеку обмена сообщениями Azure toohello ссылки для Windows с помощью hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">пакет WindowsAzure.Messaging.Managed NuGet</a>.
4. Откройте файл hello App.xaml.cs и добавьте следующее hello `using` инструкции:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. Добавьте следующий код в начало hello hello **Application_Launching** метод в App.xaml.cs:
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > Здравствуйте, значение **MyPushChannel** — это индекс, используемый toolookup существующего канала в hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) коллекции. Если канал отсутствует, создайте новую запись с таким именем.
   > 
   > 
   
    Убедитесь, что имя строки подключения концентратора и hello hello tooinsert вызывать **DefaultListenSharedAccessSignature** , полученный в предыдущем разделе hello.
    Этот код извлекает из MPNS hello URI канала для приложения hello и затем регистрирует URI канала в концентраторе уведомлений. Она также гарантирует зарегистрировано на концентраторе уведомлений, запускаемого каждое приложение hello времени URI канала hello.
   
   > [!NOTE]
   > Этот учебник отправляет устройства toohello всплывающие уведомления. При отправке уведомления плитки, вместо этого необходимо вызвать hello **BindToShellTile** метод на канале hello. toosupport плиток и всплывающих уведомлений, вызвать **BindToShellTile** и **BindToShellToast**.
   > 
   > 
6. В обозревателе решений откройте **свойства**откройте hello `WMAppManifest.xml` щелкните hello **возможности** вкладку и убедитесь, что hello **ID_CAP_PUSH_NOTIFICATION** проверяется возможность.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. Нажмите клавишу hello `F5` приложение hello toorun ключа.
   
    Отправляет сообщение отображается в приложение hello.
8. Приложение hello закрыть.  
   
   > [!NOTE]
   > tooreceive всплывающих push-уведомлений приложения hello не должна быть запущена на переднем плане hello.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>Отправка push-уведомлений из серверной части
Можно отправлять извещающие уведомления с помощью концентраторов уведомлений с любого сервера через hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">интерфейс REST</a>. В этом учебнике мы будем отправлять push-уведомления с помощью консольного приложения .NET. 

Пример как toosend push-уведомления из ASP.NET WebAPI серверную платформу, которая интегрируется с концентраторами уведомлений см. в разделе [уведомления концентраторы уведомления пользователей Azure с серверной части .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).  

Пример как hello toosend push-уведомления с помощью [API-интерфейс REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), извлечь [как toouse концентраторы уведомлений из Java](notification-hubs-java-push-notification-tutorial.md) и [как toouse концентраторы уведомлений из PHP](notification-hubs-php-push-notification-tutorial.md) .

1. Щелкните правой кнопкой мыши решение hello, выберите **добавить** и **новый проект...** , а затем в разделе **Visual C#**, нажмите кнопку **Windows** и **консольное приложение**и нажмите кнопку **ОК**.
   
       ![Visual Studio - New Project - Console Application][6]
   
    Используется для добавления нового Visual C# консольного приложения toohello решения. Это можно сделать также и в отдельном решении.
2. Щелкните **Сервис**, **Library Package Manager** (Диспетчер пакетов библиотеки), а затем — **Консоль диспетчера пакетов**.
   
    Откроется консоль диспетчера пакетов hello.
3. В hello **консоль диспетчера пакетов** окна, набор hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.
4. Откройте hello `Program.cs` файл и добавьте следующее hello `using` инструкции:
   
        using Microsoft.Azure.NotificationHubs;
5. В hello `Program` добавьте следующий метод hello:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    Убедитесь, что hello tooreplace `<hub name>` заполнитель с именем hello hello концентратор уведомлений, который отображается на портале hello. Кроме того, замените заполнитель строки подключения hello строкой подключения hello вызывается **DefaultFullSharedAccessSignature** , полученный в разделе "hello" «Настройка центра уведомлений».
   
   > [!NOTE]
   > Убедитесь, что используются hello строки подключения с **полного** доступ, не **прослушивания** доступа. Строка Hello прослушивания доступа не имеет разрешения toosend push-уведомлений.
   > 
   > 
6. Добавить hello, следующей строкой в вашей `Main` метод:
   
         SendNotificationAsync();
         Console.ReadLine();
7. С вашей Windows Phone эмулятор и вашего приложения hello закрытые, задайте консольное приложение как hello запускаемый проект по умолчанию и нажмите клавишу hello `F5` приложение hello toorun ключа.
   
    Вы получите всплывающее push-уведомление. Коснувшись баннер всплывающих hello загружает приложение hello.

Можно найти все возможные полезных данных hello hello [каталога всплывающих] и [плитки каталога] разделах в библиотеке MSDN.

## <a name="next-steps"></a>Дальнейшие действия
В этом простом примере вы широковещательной рассылки push уведомления tooall устройствами Windows Phone 8. 

В заказ tootarget определенным пользователям, см. toohello [toousers уведомления toopush использования концентраторов уведомлений] учебника. 

Следует ли toosegment пользователям по группы интересов, можно прочитать [toosend использования концентраторов уведомлений, новости]. 

Дополнительные сведения о toouse концентраторов уведомлений в [руководство концентраторы уведомлений].

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Microsoft Visual Studio 2012 Express для Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[руководство концентраторы уведомлений]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[toousers уведомления toopush использования концентраторов уведомлений]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend использования концентраторов уведомлений, новости]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[каталога всплывающих]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[плитки каталога]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[концентраторы уведомлений — Windows Phone Silverlight учебника]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

