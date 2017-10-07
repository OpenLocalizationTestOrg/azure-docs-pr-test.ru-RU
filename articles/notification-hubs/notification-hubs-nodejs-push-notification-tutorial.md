---
title: "aaaSending push-уведомлений с концентраторами уведомлений Azure и Node.js"
description: "Узнайте, как toosend toouse концентраторы уведомлений push-уведомления из приложения Node.js."
keywords: "push-уведомление, push-уведомления, push-уведомления node.js, push-уведомления ios"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Отправка push-уведомлений с помощью Центров уведомлений Azure и Node.js
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Обзор
> [!IMPORTANT]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).
> 
> 

В этом руководстве будет показано, как toosend push-уведомления с помощью hello концентраторов уведомлений Azure непосредственно из приложения Node.js. 

Hello сценарии включают, отправка уведомлений tooapplications принудительной на следующих платформах hello:

* Android
* iOS
* Windows Phone
* Универсальные приложения Windows 

Дополнительные сведения о концентраторах уведомлений см. в разделе hello [дальнейшие действия](#next) раздела.

## <a name="what-are-notification-hubs"></a>Что такое концентраторы уведомлений
Концентраторы уведомлений Azure предоставляют простой в использовании мультиплатформенную, масштабируемую инфраструктуру для Отправка push-уведомления toomobile устройств. В инфраструктуре службы hello подробнее hello [концентраторов уведомлений Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) страницы.

## <a name="create-a-nodejs-application"></a>Создание приложения Node.js
Hello первым шагом в этом учебнике используется для создания нового пустого приложения Node.js. Инструкции по созданию приложений Node.js см. в разделе [создать и развернуть tooAzure приложений Node.js веб-сайт][nodejswebsite], [Node.js облачной службы] [ Node.js Cloud Service] с помощью Windows PowerShell или [веб-сайт в WebMatrix].

## <a name="configure-your-application-toouse-notification-hubs"></a>Настройка концентраторов уведомлений tooUse приложения
toouse концентраторов уведомлений Azure требуются toodownload и используйте hello Node.js [пакеты azure](https://www.npmjs.com/package/azure), включая встроенный набор вспомогательных библиотек, взаимодействующих со службами REST уведомлений push hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета
1. Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Linux) и перейдите в папку toohello, где создан пустого приложения .
2. Тип **npm установить azure sb** в командном окне приветствия.
3. Вы можете вручную запустить hello **ls** или **dir** tooverify команды, **узел\_модули** папка была создана. В этой папке найти hello **azure** пакет, который содержит необходимые tooaccess библиотеки hello hello концентратора уведомлений.

> [!NOTE]
> Дополнительные сведения об установке на официальные hello NPM [NPM блог](http://blog.npmjs.org/post/85484771375/how-to-install-npm). 
> 
> 

### <a name="import-hello-module"></a>Импорт модуля hello
В текстовом редакторе, добавьте следующие toohello вверху hello hello **server.js** файл приложения hello:

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Настройка подключения концентратора уведомлений Azure
Hello **NotificationHubService** объектов позволяет работать с концентраторами уведомлений. Hello следующий код создает **NotificationHubService** объект с именем концентратора nofication hello **hubname**. Добавьте его вверху hello hello **server.js** файла после tooimport hello azure hello инструкции модуля:

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Здравствуйте, подключение **connectionstring** значение можно получить из hello [портала Azure] , выполнив следующие шаги hello:

1. Hello панели навигации слева щелкните **Обзор**.
2. Выберите **концентраторы уведомлений**, затем найти hello-концентратор и вы хотите toouse для образца hello. Можно ссылаться toohello [Приступая к работе Windows Store учебника](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Если вам нужна помощь при создании нового концентратора уведомлений.
3. Выберите элемент **Параметры**.
4. Щелкните **Политики доступа**. Вы увидите строки подключения как для общего, так и для полного доступа.

![Портал Azure — центры уведомлений](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> Вы также можете получить hello строки соединения, использующей hello **Get-AzureSbNamespace** командлета, предоставляемые [Azure PowerShell](/powershell/azureps-cmdlets-docs) или hello **Показать пространства имен azure sb** с Hello [интерфейса командной строки Azure (Azure CLI)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Общая архитектура
Hello **NotificationHubService** объект предоставляет следующие экземпляры объекта для отправки push уведомления toospecific устройства и приложения hello:

* **Android** -использовать hello **GcmService** объекта, который доступен на **notificationHubService.gcm**
* **iOS** -использовать hello **ApnsService** объекта, который доступен по **notificationHubService.apns**
* **Windows Phone** -использовать hello **MpnsService** объекта, который доступен на **notificationHubService.mpns**
* **Универсальная платформа Windows** -использовать hello **WnsService** объекта, который доступен на **notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>Как: отправлять push уведомления tooAndroid приложения
Hello **GcmService** объект предоставляет **отправки** метод, который может быть используется toosend принудительной уведомления tooAndroid приложений. Hello **отправки** метод принимает hello следующие параметры:

* **Теги** -hello идентификатор тега. Если ни один тег, hello уведомления будут отправляться tooall клиентов.
* **Полезные данные** -hello JSON или необработанные строковые полезные данные сообщения.
* **Обратный вызов** -hello функции обратного вызова.

Дополнительные сведения о формате полезных данных hello см. в разделе hello **полезных данных** раздел hello [реализация сервера GCM](http://developer.android.com/google/gcm/server.html#payload) документа.

Hello следующий код использует hello **GcmService** экземпляра, предоставляемые hello **NotificationHubService** toosend tooall уведомления принудительной регистрации клиентов.

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>Как: отправлять push уведомления tooiOS приложения
Таким же как и для приложений Android, описанной выше, hello **ApnsService** объект предоставляет **отправки** метод, который может быть используется toosend принудительной уведомления tooiOS приложений. Hello **отправки** метод принимает hello следующие параметры:

* **Теги** -hello идентификатор тега. Если ни один тег, hello уведомления будут отправляться tooall клиентов.
* **Полезные данные** - hello сообщения JSON или строки полезных данных.
* **Обратный вызов** -hello функции обратного вызова.

Дополнительные сведения о формате hello полезных данных. в разделе hello **полезные данные уведомления** раздел hello [локальный и Push-уведомлений руководство по программированию на](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) документа.

Hello следующий код использует hello **ApnsService** экземпляра, предоставляемые hello **NotificationHubService** toosend оповещение сообщения tooall клиентов:

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>Как: отправлять push приложения телефона tooWindows уведомления
Hello **MpnsService** объект предоставляет **отправки** метод, который может быть tooWindows уведомлений используется toosend принудительной телефонных приложений. Hello **отправки** метод принимает hello следующие параметры:

* **Теги** -hello идентификатор тега. Если ни один тег, hello уведомления будут отправляться tooall клиентов.
* **Полезные данные** -hello полезные данные сообщения XML.
* **TargetName** - `toast` — уведомлений во всплывающем окне. `token` для уведомлений на плитке.
* **NotificationClass** -hello приоритет hello уведомления. . В разделе hello **элементов заголовка HTTP** раздел hello [Push-уведомления с сервера](http://msdn.microsoft.com/library/hh221551.aspx) документа для допустимых значений.
* **Options** — необязательные заголовки запроса.
* **Обратный вызов** -hello функции обратного вызова.

Список допустимых **TargetName**, **NotificationClass** параметры заголовка, извлечение и возврат hello [Push-уведомления с сервера](http://msdn.microsoft.com/library/hh221551.aspx) страницы.

Hello, следующий пример кода использует hello **MpnsService** экземпляра, предоставляемые hello **NotificationHubService** toosend принудительной всплывающее уведомление:

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>Как: отправлять push приложения платформы Windows (UWP), tooUniversal уведомления
Hello **WnsService** объект предоставляет **отправки** метода, могут быть используется toosend принудительной уведомления tooUniversal платформы Windows приложения.  Hello **отправки** метод принимает hello следующие параметры:

* **Теги** -hello идентификатор тега. Если ни один тег, hello уведомления будут отправляться tooall зарегистрированных клиентов.
* **Полезные данные** -полезные данные сообщения hello XML.
* **Тип** -hello тип уведомления.
* **Options** — необязательные заголовки запроса.
* **Обратный вызов** -hello функции обратного вызова.

Список допустимых типов и заголовков запроса см. в разделе [Заголовки запроса и ответа службы push-уведомлений (приложения среды выполнения Windows)](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Hello следующий код использует hello **WnsService** экземпляра, предоставляемые hello **NotificationHubService** toosend приложения UWP tooa всплывающих принудительной уведомления:

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Дальнейшие действия
фрагменты кода образца Hello выше позволяют вы tooeasily сборки службы инфраструктуры toodeliver принудительной уведомления tooa широкого спектра устройств. Теперь, когда вы узнали основы использования концентраторов уведомлений с node.js hello, выполните следующие дополнительные сведения о том, как можно расширить эти возможности дальнейшего toolearn ссылки.

* В разделе hello ссылка MSDN для [концентраторов уведомлений Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Посетите hello [Azure SDK для узла] репозитория в GitHub дополнительные образцы и сведения о реализации.

[Azure SDK для узла]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[веб-сайт в WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[портала Azure]: https://portal.azure.com
