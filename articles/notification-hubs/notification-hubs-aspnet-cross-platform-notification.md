---
title: "toousers aaaSend кросс платформенных уведомлений с концентраторами уведомлений (ASP.NET)"
description: "Узнайте, как toosend шаблоны концентраторы уведомлений toouse в одном запросе уведомления зависящий от платформы, предназначенный для всех платформ."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>Отправлять уведомления кросс платформенных toousers с концентраторами уведомлений
В предыдущем учебнике hello [уведомить пользователей с концентраторами уведомлений], вы узнали, как toopush уведомления tooall устройства, зарегистрированные с конкретного прошедшего проверку пользователя. В этом учебнике нескольких запросов были необходимые toosend уведомления tooeach поддерживается клиентской платформе. Уведомления концентраторов поддерживает шаблоны, которые позволяют указать, как конкретного устройства хочет tooreceive уведомления. Это упрощает отправку кроссплатформенных уведомлений. В этом разделе показано, как tootake преимуществами toosend шаблоны, в один запрос, зависящий от платформы уведомление, предназначенный для всех платформ. Дополнительные сведения о шаблонах см. в статье [Общие сведения о концентраторах уведомлений][Templates].
> [!IMPORTANT]
> Проекты Windows Phone 8.1 и более ранней версии не поддерживаются в Visual Studio 2017. Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Концентраторы уведомлений позволяет tooregister устройства несколько шаблонов с hello таким же тегом. В этом случае входящего сообщения, предназначенные для тега приведет несколько уведомлений доставляться toohello устройства, один для каждого шаблона. Это позволяет вам toodisplay hello одного сообщения в несколько уведомлений visual, такие как оба значка, а всплывающее уведомление в приложении для магазина Windows.
> 
> 

Выполните следующие шаги toosend кросс платформенных уведомления с помощью шаблонов hello.

1. В hello обозревателя решений в Visual Studio разверните hello **контроллеров** папки, а затем откройте hello RegisterController.cs файла.
2. Найдите hello блок кода в hello **поместить** метод, который создает новую регистрацию замените hello `switch` содержимого с hello, следующий код:
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    Этот код вызывает метод платформой toocreate hello регистрацию шаблона вместо собственную регистрацию. Уже имеющиеся регистрации изменять не нужно, поскольку регистрация шаблонов является производной от собственной регистрации.
3. В hello **уведомления** контроллер, замените hello **sendNotification** метод с hello, следующий код:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Этот код отправляет уведомление tooall платформы на hello же время и без необходимости toospecify собственного полезных данных. Строит концентраторов уведомлений и доставляет hello устройства tooevery правильный полезных данных с помощью предоставленных hello *тега* значение, как указано в шаблонах hello зарегистрирован.
4. Повторно опубликуйте серверный проект WebApi.
5. Снова запустите клиентское приложение hello и убедитесь, что регистрация выполняется успешно.
6. (Необязательно) Развернуть hello клиентского приложения tooa второго устройства, а затем выполните приложение hello.
   
    Обратите внимание, что на каждом из устройств отображается уведомление.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы завершили работу с данным учебником, вы можете узнать больше о центрах уведомлений и шаблонах в следующих разделах:

* **[Использование концентраторов уведомлений toosend новости]** <br/>Демонстрация другого сценария для использования шаблонов.
* **[Общие сведения о концентраторах уведомлений][Templates]**<br/>содержится более подробная информация о шаблонах.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Использование концентраторов уведомлений toosend новости]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[уведомить пользователей с концентраторами уведомлений]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
