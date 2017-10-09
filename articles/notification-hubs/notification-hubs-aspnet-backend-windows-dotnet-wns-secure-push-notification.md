---
title: "aaaAzure Secure принудительной отправки уведомлений концентраторы"
description: "Узнайте, как безопасные toosend push-уведомления в Azure. Примеры кода на языке C# с использованием hello .NET API."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Безопасные push-уведомления посредством центров уведомлений Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Обзор
Поддержка уведомлений Push в Microsoft Azure позволяет tooaccess к использованию, несколькими платформами, масштабируемых push-инфраструктуру, которая значительно упрощает реализацию hello push-уведомлений для индивидуальных пользователей и корпоративных приложений для мобильных устройств платформы.

Иногда из-за ограничений tooregulatory или безопасности, приложение может возникнуть tooinclude что-нибудь в hello уведомление, которое не может передаваться через инфраструктуру hello Стандартная push-уведомлений. В данном учебнике как tooachieve hello такие же возможности, отправляя конфиденциальных данных через проверку подлинности безопасное соединение между hello клиентского устройства и внутреннего сервера приложения hello.

На высоком уровне hello поток выглядит следующим образом:

1. Hello приложения внутреннего интерфейса:
   * Сохраняет полезную нагрузку в базе данных серверной части.
   * Отправляет идентификатор hello toohello устройства создания уведомления (отправляются без защиты данных).
2. приложение Hello на устройстве hello, при получении уведомления hello:
   * устройство Hello обращается hello серверной части запроса hello безопасного полезных данных.
   * приложение Hello можно показать hello полезных данных в виде уведомлений на устройстве hello.

Очень важно, toonote, что предшествующий потока hello (и в этом учебнике) предполагается устройства hello склада маркер проверки подлинности в локальном хранилище после hello пользователь вошел в систему. Это гарантирует полностью эффективной работы, как hello устройства можно получить полезные данные безопасного hello уведомления, с помощью этого токена. Если приложение не хранить токены проверки подлинности на устройстве hello или может быть просрочен эти токены, hello приложения для устройств, при получении уведомления hello отображать универсального уведомление запроса приложение hello toolaunch hello пользователя. Затем приложение Hello проверяет подлинность пользователя hello и приводятся полезные данные уведомления hello.

В этом учебнике принудительной защиты как toosend push-уведомление безопасно. Hello учебник построен на hello [уведомить пользователей](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) учебник, поэтому hello шаги в этом учебнике должна выполнять первой.

> [!NOTE]
> В этом учебнике подразумевается, что вы создали и настроили центр уведомлений в соответствии с описанием в руководстве [Приступая к работе с центрами уведомлений (Магазин Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).
> Кроме того, обратите внимание, что для Windows Phone 8.1 требуются учетные данные Windows (не Windows Phone) и что фоновые задачи не работают на Windows Phone 8.0 и в Silverlight 8.1. Для приложений для магазина Windows, можно получать уведомления в фоновом режиме, только в том случае, если включить экран блокировки является приложение hello (щелкните флажок hello в hello Appmanifest).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>Изменение hello проекта Windows Phone
1. В hello **NotifyUserWindowsPhone** , добавьте следующий код tooApp.xaml.cs tooregister hello принудительной фоновой задачей hello. Добавьте следующие строки кода в конце hello hello hello `OnLaunched()` метод:
   
        RegisterBackgroundTask();
2. По-прежнему в App.xaml.cs, добавьте следующий код сразу после hello hello `OnLaunched()` метод:
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. Добавьте следующее hello `using` операторы в начале hello hello App.xaml.cs файла:
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. Из hello **файл** меню в Visual Studio щелкните **сохранить все**.

## <a name="create-hello-push-background-component"></a>Создать hello Push фона компонента
Hello следующим шагом является toocreate hello принудительной фона компонента.

1. В обозревателе решений щелкните правой кнопкой мыши узел верхнего уровня hello hello решения (**SecurePush решения** в данном случае), нажмите кнопку **добавить**, нажмите кнопку **новый проект**.
2. Разверните пункт **Приложения Магазина**, затем щелкните **Приложения Windows Phone** и выберите **Компонент среды выполнения Windows (Windows Phone)**. Имя проекта hello **PushBackgroundComponent**и нажмите кнопку **ОК** toocreate hello проекта.
   
    ![][12]
3. В обозревателе решений щелкните правой кнопкой мыши hello **PushBackgroundComponent (Windows Phone 8.1)** проекта, а затем нажмите кнопку **добавить**, нажмите кнопку **класса**. Имя нового класса hello **PushBackgroundTask.cs**. Нажмите кнопку **добавить** toogenerate hello класса.
4. Замените все содержимое hello hello **PushBackgroundComponent** определения пространства имен с hello после кода, заменив заполнитель hello `{back-end endpoint}` с конечной точкой hello серверной части, полученный при развертывании вашей Тыловой:
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. В обозревателе решений щелкните правой кнопкой мыши hello **PushBackgroundComponent (Windows Phone 8.1)** проект и выберите пункт **управление пакетами NuGet**.
6. В левой части окна hello, выберите **Online**.
7. В hello **поиска** введите **HTTP-клиент**.
8. В списке результатов hello, нажмите кнопку **клиентских библиотек HTTP Майкрософт**, а затем нажмите кнопку **установить**. Завершить установку hello.
9. Вернитесь в hello NuGet **поиска** введите **Json.net**. Установка hello **Json.NET** пакета, а затем hello закрыть окно диспетчера пакетов NuGet.
10. Добавьте следующее hello `using` инструкции вверху hello hello **PushBackgroundTask.cs** файла:
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. В обозревателе решений в hello **NotifyUserWindowsPhone (Windows Phone 8.1)** щелкните правой кнопкой мыши проект **ссылки**, нажмите кнопку **добавить ссылку...** . В диалоговом окне диспетчера ссылок hello, установите флажок "hello" рядом слишком**PushBackgroundComponent**, а затем нажмите кнопку **ОК**.
12. В обозревателе решений дважды щелкните **Package.appxmanifest** в hello **NotifyUserWindowsPhone (Windows Phone 8.1)** проекта. В разделе **уведомления**, задайте **поддержкой всплывающих** слишком**Да**.
    
    ![][3]
13. В по-прежнему **Package.appxmanifest**, нажмите кнопку hello **объявления** меню верхней hello. В hello **доступные объявления** раскрывающийся список, нажмите кнопку **фоновые задачи**, а затем нажмите кнопку **добавить**.
14. В **Package.appxmanifest** в разделе **Свойства** включите параметр **Push-уведомление**.
15. В **Package.appxmanifest**в разделе **параметры приложения**, тип **PushBackgroundComponent.PushBackgroundTask** в hello **точки входа** поле.
    
    ![][13]
16. Из hello **файл** меню, нажмите кнопку **сохранить все**.

## <a name="run-hello-application"></a>Запустите приложение hello
toorun Здравствуйте, приложения, hello следующие:

1. В Visual Studio, запустите hello **AppBackend** приложения веб-API. Отобразится веб-страница ASP.NET.
2. В Visual Studio, запустите hello **NotifyUserWindowsPhone (Windows Phone 8.1)** приложения Windows Phone. Эмулятор Windows Phone Hello запускается и автоматически загружает приложение hello.
3. В hello **NotifyUserWindowsPhone** приложения пользовательского интерфейса, введите имя пользователя и пароль. Это может быть любой строкой, но они должны быть hello одинаковое значение.
4. В hello **NotifyUserWindowsPhone** приложения пользовательского интерфейса, нажмите кнопку **входа и регистрации**. Затем нажмите **Отправить push-уведомление**.

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
