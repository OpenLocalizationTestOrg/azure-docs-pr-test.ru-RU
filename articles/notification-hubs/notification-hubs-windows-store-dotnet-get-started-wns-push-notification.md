---
title: "aaaGet работы с Azure уведомления концентраторов для универсальной платформы приложений для Windows | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toouse концентраторов уведомлений Azure toopush уведомления tooa приложения универсальной платформы Windows."
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
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Начало работы с Центрами уведомлений для приложений универсальной платформы Windows
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Обзор
Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa универсальной платформы Windows (UWP) приложения.

В этом учебнике создается пустое приложение магазина Windows, получающий push-уведомления с помощью hello Windows Push Notification Service (WNS). После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения.

## <a name="before-you-begin"></a>Перед началом работы
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

код завершения Hello в этом учебнике можно найти на GitHub [здесь](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).

## <a name="prerequisites"></a>Предварительные требования
Этот учебник требует hello следующее:

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) или более поздняя версия.
* [Установленные средства разработки универсальных приложений Windows](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* Активная учетная запись Azure. <br/>Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).
* Активная учетная запись Магазина Windows.

Завершение изучения этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Центрам уведомлений для приложений универсальной платформы Windows.

## <a name="register-your-app-for-hello-windows-store"></a>Регистрация приложения для магазина Windows hello
toosend принудительной уведомления tooUWP приложений, необходимо связать toohello вашего приложения магазина Windows. Затем необходимо настроить на toointegrate концентратора уведомлений с WNS.

1. Если приложение еще не зарегистрирован, перейдите в папку toohello [центра разработчиков Windows](https://dev.windows.com/overview), войти в учетную запись Майкрософт и нажмите кнопку **создайте новое приложение**.

2. Введите имя приложения и нажмите кнопку **Зарезервировать имя приложения**. При этом создается новая регистрация в Магазине Windows для вашего приложения.

3. В Visual Studio, создайте новый проект Visual C# магазина с помощью универсальных Windows hello **пустое приложение** шаблона и нажмите кнопку **ОК**.

4. Примите значения по умолчанию hello для hello целевую и минимальную версии платформы.

5. В обозревателе решений щелкните правой кнопкой мыши проект приложения для магазина Windows hello, нажмите кнопку **хранилища**, а затем нажмите кнопку **связать приложение с hello хранилища...** . hello **связывать приложения с магазина Windows hello** откроется окно мастера.

6. В мастере hello войти в учетную запись Майкрософт.

7. Выберите приложение hello, зарегистрированный на шаге 2, щелкните **Далее**, а затем нажмите кнопку **связать**. Это добавляет манифест приложения toohello сведения о регистрации требуется hello магазина Windows.

8. Включите hello [центра разработчиков Windows](http://dev.windows.com/overview) для нового приложения и щелкните **службы**, нажмите кнопку **Push-уведомления**и нажмите кнопку **WNS или MPNS**.

9. Щелкните **Новое уведомление**.

10. Щелкните шаблон **Blank (Toast)** (Пустое (всплывающее)) и нажмите кнопку **ОК**.

11. Введите **имя** уведомления и **контекстное** сообщение Visual. Затем щелкните **Save as draft** (Сохранить как черновик).

12. Перейдите toohello [портала регистрации приложения](http://apps.dev.microsoft.com) и войдите в систему.

13. Щелкните имя приложения. Запишите hello **секрет приложения** пароль и hello **пакета идентификатор безопасности (SID)** в hello **магазина Windows** параметры платформы.

     > [AZURE.WARNING]
    секрет приложения Hello и ИД безопасности пакета являются важными элементами обеспечения безопасности. Не сообщайте никому эти значения и не распространяйте их вместе со своим приложением.

## <a name="configure-your-notification-hub"></a>Настройка концентратора уведомлений
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Выберите hello <b>служб Notification Services</b> параметр и hello <b>Windows (WNS)</b> параметр. Затем введите hello <b>секрет приложения</b> пароль в hello <b>ключ безопасности</b> поля. Введите ваш <b>ИД безопасности пакета</b> значения, полученные из WNS в предыдущем разделе hello и нажмите кнопку <b>Сохранить</b>.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

Концентратор уведомлений будет настроенных toowork с WNS, и иметь tooregister строки подключения hello приложения и отправку уведомлений.

## <a name="connect-your-app-toohello-notification-hub"></a>Подключение приложения toohello концентратор уведомлений
1. В Visual Studio, щелкните правой кнопкой мыши решение hello и нажмите кнопку **управление пакетами NuGet**.
   
    При этом отображаются hello **управление пакетами NuGet** диалоговое окно.
2. Поиск `WindowsAzure.Messaging.Managed` и нажмите кнопку **установить**и примите условия использования hello.
   
    ![][20]
   
    Это загружает устанавливает и добавляет библиотеку обмена сообщениями Azure toohello ссылки для Windows с помощью hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">пакет WindowsAzure.Messaging.Managed NuGet</a>.
3. Откройте файл проекта App.xaml.cs hello и добавьте следующее hello `using` инструкции. 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. Также в App.xaml.cs, добавьте следующее hello **InitNotificationsAsync** toohello определение метода **приложения** класса:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    Этот код извлекает из WNS hello URI канала для приложения hello и затем регистрирует URI канала в концентраторе уведомлений.
   
   > [!NOTE]
   > Убедитесь, что tooreplace hello заполнитель «имя концентратора» hello имя концентратора уведомлений hello в hello портала Azure. Также замените заполнитель строки подключения hello hello **DefaultListenSharedAccessSignature** строку подключения, который получен из hello **политики доступа** страницы центра уведомлений в предыдущего раздела.
   > 
   > 
5. Вверху hello hello **OnLaunched** обработчик событий в App.xaml.cs, добавьте после вызова toohello новый hello **InitNotificationsAsync** метод:
   
        InitNotificationsAsync();
   
    Это гарантирует зарегистрировано на концентраторе уведомлений, запускаемого каждое приложение hello времени URI канала hello.
6. Нажмите клавишу hello **F5** приложение hello toorun ключа. Отображается всплывающее диалоговое окно, содержащее ключ регистрации hello.

Приложение больше не готов tooreceive всплывающие уведомления.

## <a name="send-notifications"></a>Отправка уведомлений
Можно быстро проверить получение уведомлений в приложение путем отправки уведомления в hello [портала Azure](https://portal.azure.com/) с помощью hello **Тестовая отправка** кнопку на концентраторе уведомлений hello, как показано ниже экрана приветствия.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

Push-уведомления обычно отправляются в серверной службе, например мобильными службами или ASP.NET, с помощью совместимой библиотеки. Также можно использовать hello REST API напрямую toosend уведомления сообщений, если библиотека недоступна для серверной части. 

В этом учебнике мы должен быть простым и просто демонстрации тестирование приложения клиента путем отправки уведомлений с использованием hello .NET SDK для концентраторов уведомлений в консольном приложении, а не серверной службы. Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений] учебника hello на следующем шаге для отправки уведомлений из серверной части ASP.NET. Тем не менее можно использовать следующие подходы hello для отправки уведомлений:

* **Интерфейс REST**: может поддерживать уведомления на любой платформе серверной части, с помощью hello [интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Пакета SDK .NET концентраторы уведомлений Microsoft Azure**: В hello диспетчера пакетов Nuget для Visual Studio, запустите [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [как концентраторы уведомлений из Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).
* **Мобильные приложения Azure**: пример того, как toosend уведомления от мобильного приложения Azure, интегрируется с концентраторами уведомлений в разделе [Добавление push-уведомлений для мобильных приложений](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: пример как toosend уведомления с помощью hello API-интерфейс REST, в разделе «как toouse концентраторы уведомлений из Java и PHP» ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(Необязательно) Отправке уведомлений из консольного приложения в C#
toosend уведомления с помощью консольного приложения .NET выполните следующие действия. 

1. Щелкните правой кнопкой мыши решение hello, выберите **добавить** и **новый проект...** , а затем в разделе **Visual C#**, нажмите кнопку **Windows** и **консольное приложение**и нажмите кнопку **ОК**.
   
    Используется для добавления нового Visual C# консольного приложения toohello решения. Это можно сделать также и в отдельном решении.

2. В Visual Studio последовательно выберите элементы **Сервис**, **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.
   
    Откроется консоль диспетчера пакетов hello в Visual Studio.
3. В hello в окне консоли диспетчера пакетов, задайте hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Откройте файл Program.cs hello и добавьте следующее hello `using` инструкции:
   
        using Microsoft.Azure.NotificationHubs;
5. В hello **программы** добавьте следующий метод hello:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > Убедитесь, что используются hello строки подключения, которая содержит **полного** доступ, не **прослушивания** доступа. Строка Hello прослушивания доступа не имеет разрешения toosend уведомления.
   > 
   > 
6. Добавьте следующие строки в hello hello **Main** метод:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Щелкните правой кнопкой мыши проект консольного приложения hello в Visual Studio, а затем нажмите кнопку **Назначить запускаемым проектом** tooset его hello запускаемым проектом. Нажмите клавишу hello **F5** ключа toorun приложения hello.
   
    На всех зарегистрированных устройствах будет получено всплывающее уведомление. Нажав кнопку баннер всплывающих hello загружает приложение hello.

Можно найти все полезные данные hello поддерживается hello [каталога всплывающих], [плитки каталога], и [значок Обзор] разделах в библиотеке MSDN.

## <a name="next-steps"></a>Дальнейшие действия
В этом простом примере вы отправили tooall широковещательной рассылки уведомлений устройства Windows с помощью портала hello или консольное приложение. Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений] учебника в качестве следующего шага hello. Также будет показано, как уведомления о toosend из серверной части ASP.NET с помощью тегов tootarget конкретных пользователей.

Если toosegment пользователям по группы интересов, см. [toosend использования концентраторов уведомлений, новости]. 

toolearn. в разделе Общие сведения о концентраторах уведомлений [руководство концентраторы уведомлений](notification-hubs-push-notification-overview.md).

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[toousers уведомления toopush использования концентраторов уведомлений]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend использования концентраторов уведомлений, новости]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[каталога всплывающих]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[плитки каталога]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[значок Обзор]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
