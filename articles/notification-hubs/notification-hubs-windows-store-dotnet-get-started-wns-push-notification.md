---
title: "Начало работы с Центрами уведомлений Azure для приложений универсальной платформы Windows | Документация Майкрософт"
description: "При работе с этим руководством вы узнаете, как отправлять push-уведомления в приложение универсальной платформы Windows с помощью Центров уведомлений Azure."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9b50f1cca81348b69f7ff2d702c6c72871afe0a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Начало работы с Центрами уведомлений для приложений универсальной платформы Windows
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Обзор
В этом руководстве показано, как использовать Центры уведомлений Azure для отправки push-уведомлений в приложение универсальной платформы Windows (UWP).

В этом учебнике вам предстоит создать пустое приложение Магазина Windows, получающее push-уведомления с помощью службы push-уведомлений Windows (WNS). По завершении вы сможете рассылать push-уведомления на все устройства, где запущено ваше приложение, с помощью центра уведомлений.

## <a name="before-you-begin"></a>Перед началом работы
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Полный код для этого учебника можно найти на портале [GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).

## <a name="prerequisites"></a>Предварительные требования
Для работы с данным учебником требуется следующее:

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) или более поздняя версия.
* [Установленные средства разработки универсальных приложений Windows](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* Активная учетная запись Azure. <br/>Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).
* Активная учетная запись Магазина Windows.

Завершение изучения этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Центрам уведомлений для приложений универсальной платформы Windows.

## <a name="register-your-app-for-the-windows-store"></a>Регистрация приложения для Магазина Windows
Чтобы отправлять push-уведомления в приложения UWP, необходимо связать приложение с Магазином Windows. После этого необходимо настроить концентратор уведомлений на интеграцию с WNS.

1. Если вы еще не зарегистрировали свое приложение, перейдите в [Центр разработки для Windows](https://dev.windows.com/overview), войдите с помощью учетной записи Майкрософт, а затем щелкните **Создать приложение**.

2. Введите имя приложения и нажмите кнопку **Зарезервировать имя приложения**. При этом создается новая регистрация в Магазине Windows для вашего приложения.

3. В Visual Studio создайте проект приложения Visual C# для Магазина с помощью шаблона **Пустое приложение** универсального приложения Windows и щелкните **ОК**.

4. Примите значения по умолчанию для целевой и минимальной версий платформы.

5. В обозревателе решений щелкните правой кнопкой мыши проект приложения для Магазина Windows, щелкните **Магазин**, а затем — **Связать приложение с Магазином...**. Откроется мастер **Свяжите свое приложение с Магазином Windows** .

6. В мастере войдите с помощью учетной записи Майкрософт.

7. Выберите приложение, зарегистрированное на шаге 2, щелкните **Далее**, а затем — **Связать**. Это добавляет необходимые регистрационные данные Магазина Windows в манифест приложения.

8. На странице [Центр разработки для Windows](http://dev.windows.com/overview) вашего нового приложения щелкните **Службы**, а затем **Push-уведомления** и **WNS/MPNS**.

9. Щелкните **Новое уведомление**.

10. Щелкните шаблон **Blank (Toast)** (Пустое (всплывающее)) и нажмите кнопку **ОК**.

11. Введите **имя** уведомления и **контекстное** сообщение Visual. Затем щелкните **Save as draft** (Сохранить как черновик).

12. Перейдите на [портал регистрации приложений](http://apps.dev.microsoft.com) и войдите в систему.

13. Щелкните имя приложения. Запишите значение пароля в разделе **секретов приложения** и значение **идентификатора безопасности пакета (SID)**, указанное в параметрах платформы **Магазина Windows**.

     > [AZURE.WARNING]
    Секрет приложения и ИД безопасности пакета — это важные учетные данные для безопасного доступа. Не сообщайте никому эти значения и не распространяйте их вместе со своим приложением.

## <a name="configure-your-notification-hub"></a>Настройка концентратора уведомлений
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Выберите пункт <b>Службы уведомлений</b>, а затем — <b>Windows (WNS)</b>. После этого в поле <b>Секрет приложения</b> введите значение <b>секрета приложения</b>. Введите значение <b>идентификатора безопасности пакета</b>, полученное из WNS при работе с предыдущим разделом, и нажмите кнопку <b>Сохранить</b>.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

Концентратор уведомлений теперь настроен для работы с WNS, и у вас есть строки подключения, чтобы зарегистрировать приложение и отправлять уведомления.

## <a name="connect-your-app-to-the-notification-hub"></a>Подключение приложения к центру уведомлений
1. В Visual Studio щелкните решение правой кнопкой мыши, а затем выберите пункт **Управление пакетами NuGet**.
   
    Откроется диалоговое окно **Управление пакетами NuGet** .
2. Выполните поиск по запросу `WindowsAzure.Messaging.Managed` и нажмите кнопку **Установить**, после чего примите условия использования.
   
    ![][20]
   
    После этого будут выполнены скачивание, установка и добавление ссылки на библиотеку Azure Messaging для Windows с помощью <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">пакета NuGet WindowsAzure.Messaging.Managed</a>.
3. Откройте файл проекта App.xaml.cs и добавьте следующие операторы `using` . 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. Кроме того, в файле App.xaml.cs добавьте определение метода **InitNotificationsAsync** в класс **App**:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    Этот код получает универсальный идентификатор ресурса (URI) канала для приложения из WNS, а затем регистрирует этот идентификатор в вашем центре уведомлений.
   
   > [!NOTE]
   > Обязательно замените заполнитель your hub name именем центра уведомлений, которое отображается на портале Azure. Кроме того, замените заполнитель строки подключения на строку подключения **DefaultListenSharedAccessSignature**, полученную на странице **Access Polices** (Политики доступа) Центра уведомлений при работе с предыдущим разделом.
   > 
   > 
5. В верхней части обработчика событий **OnLaunched** в файле App.xaml.cs добавьте в новый метод **InitNotificationsAsync** следующий вызов:
   
        InitNotificationsAsync();
   
    Это обеспечит регистрацию URI канала в центре уведомлений при каждом запуске приложения.
6. Нажмите клавишу **F5**, чтобы запустить приложение. Отображается всплывающее диалоговое окно с ключом регистрации.

Теперь приложение готово к получению всплывающих уведомлений.

## <a name="send-notifications"></a>Отправка уведомлений
Вы можете быстро проверить получение уведомлений в приложении. Для этого отправьте уведомление на [портале Azure](https://portal.azure.com/), нажав кнопку **Тестовая отправка** в центре уведомлений, как показано на снимке экрана ниже.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

Push-уведомления обычно отправляются в серверной службе, например мобильными службами или ASP.NET, с помощью совместимой библиотеки. Также можно напрямую использовать REST API для отправки уведомлений, если для серверной части библиотека недоступна. 

В этом учебнике мы пойдем по простому пути и продемонстрируем тестирование клиентского приложения, отправляя уведомления с помощью пакета SDK для .NET для центров уведомлений не в серверную службу, а в консольное приложение. В качестве следующего шага по отправке уведомлений с сервера ASP.NET рекомендуем ознакомиться с руководством [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET] . Можно использовать следующие способы отправки уведомлений.

* **Интерфейс REST**. [Интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx) поддерживает уведомления на любой серверной платформе.
* **Пакет SDK .NET для Центров уведомлений Microsoft Azure**. В диспетчере пакетов NuGet для Visual Studio выполните команду [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**. [Использование центров уведомлений из Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Мобильные приложения Azure**. Пример отправки уведомлений из мобильного приложения Azure, интегрированного с Центрами уведомлений, см. в статье [Добавление push-уведомлений в приложение Windows](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java или PHP**. Примеры отправки уведомлений с использованием REST API см. в статьях "Использование концентраторов уведомлений из Java и "Использование концентраторов уведомлений из PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(Необязательно) Отправке уведомлений из консольного приложения в C#
Для отправки уведомлений с помощью консольного приложения .NET выполните указанные ниже действия. 

1. Щелкните решение правой кнопкой мыши, выберите пункты **Добавить** и **Создать проект...**. После этого в разделе **Visual C#** выберите **Windows** и **Консольное приложение**, а затем нажмите кнопку **ОК**.
   
    При этом в решение добавляется новое консольное приложение Visual C#. Это можно сделать также и в отдельном решении.

2. В Visual Studio последовательно выберите элементы **Сервис**, **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.
   
    В результате в Visual Studio откроется консоль диспетчера пакетов.
3. В окне консоли диспетчера пакетов задайте свойство **Проект по умолчанию** для нового проекта консольного приложения, а затем в окне консоли выполните следующую команду:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    После этого будет добавлена ссылка на пакет SDK для Центров уведомлений Azure с помощью <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакета NuGet Microsoft.Azure.Notification Hubs</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Откройте файл Program.cs и добавьте следующий оператор `using` :
   
        using Microsoft.Azure.NotificationHubs;
5. Добавьте в класс **Program** следующий метод:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure to replace the "hub name" placeholder with the name of the notification hub that as it appears in the Azure Portal. Also, replace the connection string placeholder with the **DefaultFullSharedAccessSignature** connection string that you obtained from the **Access Policies** page of your Notification Hub in the section called "Configure your notification hub."
   
   > [!NOTE]
   > Обязательно используйте строку подключения с **полным** доступом, а не c доступом к **прослушиванию**. У строки с доступом к прослушиванию отсутствуют разрешения для отправки уведомлений.
   > 
   > 
6. Добавьте следующие строки в метод **Main** :
   
         SendNotificationAsync();
         Console.ReadLine();
7. В Visual Studio щелкните проект консольного приложения правой кнопкой мыши и выберите пункт **Назначить запускаемым проектом** . Нажмите клавишу **F5**, чтобы запустить консольное приложение.
   
    На всех зарегистрированных устройствах будет получено всплывающее уведомление. Если щелкнуть заголовок уведомления или коснуться его, приложение будет загружено.

В таких разделах MSDN, как [каталог всплывающих уведомлений], [каталог плиток] и [обзор индикаторов событий], можно найти всю полезную информацию по данной теме.

## <a name="next-steps"></a>Дальнейшие действия
В этом простом примере осуществляется рассылка уведомлений на все устройства Windows через портал или консольное приложение. На следующем этапе мы рекомендуем ознакомиться с руководством [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET] . В нем описана процедура отправки уведомлений с сервера ASP.NET определенным пользователям с использованием тегов.

Если необходимо разделить пользователей по группам интересов, см. раздел [Использование концентраторов уведомлений для передачи экстренных новостей]. 

Дополнительные сведения о Центрах уведомлений см. в статье [Notification Hubs Guidance](notification-hubs-push-notification-overview.md) (Общие сведения о Центрах уведомлений).

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Использование концентраторов уведомлений для передачи экстренных новостей]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[каталог всплывающих уведомлений]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[каталог плиток]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[обзор индикаторов событий]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
