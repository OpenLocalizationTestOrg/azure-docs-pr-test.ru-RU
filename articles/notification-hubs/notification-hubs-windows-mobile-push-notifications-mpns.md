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
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="6c661-104">Отправка push-уведомлений в приложения Windows Phone с помощью центров уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="6c661-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="6c661-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="6c661-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="6c661-106">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6c661-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6c661-107">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6c661-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6c661-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="6c661-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="6c661-109">Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa: приложения Windows Phone 8 или Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="6c661-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="6c661-110">Если вы используете Windows Phone 8.1 (отличных от Silverlight), а затем ссылаться toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) версии.</span><span class="sxs-lookup"><span data-stu-id="6c661-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="6c661-111">В этом учебнике создается пустого приложения Windows Phone 8, получающий push-уведомления с помощью hello Microsoft Push Notification Service (MPNS).</span><span class="sxs-lookup"><span data-stu-id="6c661-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using hello Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="6c661-112">После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения.</span><span class="sxs-lookup"><span data-stu-id="6c661-112">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="6c661-113">пакет SDK для Windows Phone концентраторы уведомлений Hello не поддерживает использование hello Windows Push Notification Service (WNS) с приложениями Silverlight 8.1 Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="6c661-113">hello Notification Hubs Windows Phone SDK does not support using hello Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="6c661-114">toouse WNS (вместо MPNS) с приложениями Silverlight 8.1 Windows Phone, выполните hello [концентраторы уведомлений — Windows Phone Silverlight учебника], которая использует API-интерфейс REST.</span><span class="sxs-lookup"><span data-stu-id="6c661-114">toouse WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow hello [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="6c661-115">Hello учебник демонстрирует простой сценарий широковещательных hello в с использованием концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6c661-115">hello tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c661-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6c661-116">Prerequisites</span></span>
<span data-ttu-id="6c661-117">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="6c661-117">This tutorial requires hello following:</span></span>

* <span data-ttu-id="6c661-118">[Microsoft Visual Studio 2012 Express для Windows Phone]или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="6c661-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="6c661-119">Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными Центрам уведомлений для приложений Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="6c661-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="6c661-120">Создание центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="6c661-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="6c661-121">Щелкните hello <b>служб Notification Services</b> раздела (в пределах <i>параметры</i>), щелкните <b>Windows Phone (MPNS)</b> и нажмите кнопку hello <b>включить push без проверки подлинности </b> флажок.</span><span class="sxs-lookup"><span data-stu-id="6c661-121">Click hello <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click hello <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Azure Portal — включение push-уведомлений без проверки подлинности](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="6c661-123">Концентратор больше не была создана и настроена toosend не прошедшие проверку подлинности уведомления для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="6c661-123">Your hub is now created and configured toosend unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="6c661-124">В этом учебнике используется MPNS в режиме без проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6c661-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="6c661-125">Режим без проверки подлинности MPNS поставляется с ограничения на уведомления, можно отправить tooeach канала.</span><span class="sxs-lookup"><span data-stu-id="6c661-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send tooeach channel.</span></span> <span data-ttu-id="6c661-126">Концентраторы уведомлений поддерживает [режиме с проверкой подлинности MPNS](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) , позволяя tooupload свой сертификат.</span><span class="sxs-lookup"><span data-stu-id="6c661-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you tooupload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a><span data-ttu-id="6c661-127">Подключение приложения toohello концентратор уведомлений</span><span class="sxs-lookup"><span data-stu-id="6c661-127">Connecting your app toohello notification hub</span></span>
1. <span data-ttu-id="6c661-128">В Visual Studio создайте новое консольное приложение Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="6c661-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="6c661-129">В Visual Studio 2013 с обновлением 2 вместо этого вы создаете приложение Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="6c661-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio — новый проект — пустое приложение — Windows Phone Silverlight][11]
2. <span data-ttu-id="6c661-131">В Visual Studio, щелкните правой кнопкой мыши решение hello и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6c661-131">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="6c661-132">При этом отображаются hello **управление пакетами NuGet** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6c661-132">This displays hello **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="6c661-133">Поиск `WindowsAzure.Messaging.Managed` и нажмите кнопку **установить**, а затем примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="6c661-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept hello terms of use.</span></span>
   
    ![Visual Studio — диспетчер пакетов NuGet][20]
   
    <span data-ttu-id="6c661-135">Это загружает устанавливает и добавляет библиотеку обмена сообщениями Azure toohello ссылки для Windows с помощью hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">пакет WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="6c661-135">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="6c661-136">Откройте файл hello App.xaml.cs и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="6c661-136">Open hello file App.xaml.cs and add hello following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="6c661-137">Добавьте следующий код в начало hello hello **Application_Launching** метод в App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="6c661-137">Add hello following code at hello top of **Application_Launching** method in App.xaml.cs:</span></span>
   
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
   > <span data-ttu-id="6c661-138">Здравствуйте, значение **MyPushChannel** — это индекс, используемый toolookup существующего канала в hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) коллекции.</span><span class="sxs-lookup"><span data-stu-id="6c661-138">hello value **MyPushChannel** is an index that is used toolookup an existing channel in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="6c661-139">Если канал отсутствует, создайте новую запись с таким именем.</span><span class="sxs-lookup"><span data-stu-id="6c661-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="6c661-140">Убедитесь, что имя строки подключения концентратора и hello hello tooinsert вызывать **DefaultListenSharedAccessSignature** , полученный в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="6c661-140">Make sure tooinsert hello name of your hub and hello connection string called **DefaultListenSharedAccessSignature** that you obtained in hello previous section.</span></span>
    <span data-ttu-id="6c661-141">Этот код извлекает из MPNS hello URI канала для приложения hello и затем регистрирует URI канала в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6c661-141">This code retrieves hello channel URI for hello app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="6c661-142">Она также гарантирует зарегистрировано на концентраторе уведомлений, запускаемого каждое приложение hello времени URI канала hello.</span><span class="sxs-lookup"><span data-stu-id="6c661-142">It also guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c661-143">Этот учебник отправляет устройства toohello всплывающие уведомления.</span><span class="sxs-lookup"><span data-stu-id="6c661-143">This tutorial sends a toast notification toohello device.</span></span> <span data-ttu-id="6c661-144">При отправке уведомления плитки, вместо этого необходимо вызвать hello **BindToShellTile** метод на канале hello.</span><span class="sxs-lookup"><span data-stu-id="6c661-144">When you send a tile notification, you must instead call hello **BindToShellTile** method on hello channel.</span></span> <span data-ttu-id="6c661-145">toosupport плиток и всплывающих уведомлений, вызвать **BindToShellTile** и **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="6c661-145">toosupport both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="6c661-146">В обозревателе решений откройте **свойства**откройте hello `WMAppManifest.xml` щелкните hello **возможности** вкладку и убедитесь, что hello **ID_CAP_PUSH_NOTIFICATION** проверяется возможность.</span><span class="sxs-lookup"><span data-stu-id="6c661-146">In Solution Explorer, expand **Properties**, open hello `WMAppManifest.xml` file, click hello **Capabilities** tab, and make sure that hello **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. <span data-ttu-id="6c661-147">Нажмите клавишу hello `F5` приложение hello toorun ключа.</span><span class="sxs-lookup"><span data-stu-id="6c661-147">Press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="6c661-148">Отправляет сообщение отображается в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="6c661-148">A registration message is displayed in hello app.</span></span>
8. <span data-ttu-id="6c661-149">Приложение hello закрыть.</span><span class="sxs-lookup"><span data-stu-id="6c661-149">Close hello app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="6c661-150">tooreceive всплывающих push-уведомлений приложения hello не должна быть запущена на переднем плане hello.</span><span class="sxs-lookup"><span data-stu-id="6c661-150">tooreceive a toast push notification, hello application must not be running in hello foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="6c661-151">Отправка push-уведомлений из серверной части</span><span class="sxs-lookup"><span data-stu-id="6c661-151">Send push notifications from your backend</span></span>
<span data-ttu-id="6c661-152">Можно отправлять извещающие уведомления с помощью концентраторов уведомлений с любого сервера через hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">интерфейс REST</a>.</span><span class="sxs-lookup"><span data-stu-id="6c661-152">You can send push notifications by using Notification Hubs from any backend via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="6c661-153">В этом учебнике мы будем отправлять push-уведомления с помощью консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="6c661-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="6c661-154">Пример как toosend push-уведомления из ASP.NET WebAPI серверную платформу, которая интегрируется с концентраторами уведомлений см. в разделе [уведомления концентраторы уведомления пользователей Azure с серверной части .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="6c661-154">For an example of how toosend push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="6c661-155">Пример как hello toosend push-уведомления с помощью [API-интерфейс REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), извлечь [как toouse концентраторы уведомлений из Java](notification-hubs-java-push-notification-tutorial.md) и [как toouse концентраторы уведомлений из PHP](notification-hubs-php-push-notification-tutorial.md) .</span><span class="sxs-lookup"><span data-stu-id="6c661-155">For an example of how toosend push notifications by using hello [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="6c661-156">Щелкните правой кнопкой мыши решение hello, выберите **добавить** и **новый проект...** , а затем в разделе **Visual C#**, нажмите кнопку **Windows** и **консольное приложение**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6c661-156">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="6c661-157">Используется для добавления нового Visual C# консольного приложения toohello решения.</span><span class="sxs-lookup"><span data-stu-id="6c661-157">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="6c661-158">Это можно сделать также и в отдельном решении.</span><span class="sxs-lookup"><span data-stu-id="6c661-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="6c661-159">Щелкните **Сервис**, **Library Package Manager** (Диспетчер пакетов библиотеки), а затем — **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="6c661-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="6c661-160">Откроется консоль диспетчера пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="6c661-160">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="6c661-161">В hello **консоль диспетчера пакетов** окна, набор hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6c661-161">In hello **Package Manager Console** window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="6c661-162">При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="6c661-162">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="6c661-163">Откройте hello `Program.cs` файл и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="6c661-163">Open hello `Program.cs` file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="6c661-164">В hello `Program` добавьте следующий метод hello:</span><span class="sxs-lookup"><span data-stu-id="6c661-164">In hello `Program` class, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="6c661-165">Убедитесь, что hello tooreplace `<hub name>` заполнитель с именем hello hello концентратор уведомлений, который отображается на портале hello.</span><span class="sxs-lookup"><span data-stu-id="6c661-165">Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello portal.</span></span> <span data-ttu-id="6c661-166">Кроме того, замените заполнитель строки подключения hello строкой подключения hello вызывается **DefaultFullSharedAccessSignature** , полученный в разделе "hello" «Настройка центра уведомлений».</span><span class="sxs-lookup"><span data-stu-id="6c661-166">Also, replace hello connection string placeholder with hello connection string called **DefaultFullSharedAccessSignature** that you obtained in hello section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c661-167">Убедитесь, что используются hello строки подключения с **полного** доступ, не **прослушивания** доступа.</span><span class="sxs-lookup"><span data-stu-id="6c661-167">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="6c661-168">Строка Hello прослушивания доступа не имеет разрешения toosend push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6c661-168">hello listen-access string does not have permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="6c661-169">Добавить hello, следующей строкой в вашей `Main` метод:</span><span class="sxs-lookup"><span data-stu-id="6c661-169">Add hello following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="6c661-170">С вашей Windows Phone эмулятор и вашего приложения hello закрытые, задайте консольное приложение как hello запускаемый проект по умолчанию и нажмите клавишу hello `F5` приложение hello toorun ключа.</span><span class="sxs-lookup"><span data-stu-id="6c661-170">With your Windows Phone emulator running and your app closed, set hello console application project as hello default startup project, and then press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="6c661-171">Вы получите всплывающее push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="6c661-171">You will receive a toast push notification.</span></span> <span data-ttu-id="6c661-172">Коснувшись баннер всплывающих hello загружает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="6c661-172">Tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="6c661-173">Можно найти все возможные полезных данных hello hello [каталога всплывающих] и [плитки каталога] разделах в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="6c661-173">You can find all hello possible payloads in hello [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c661-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c661-174">Next steps</span></span>
<span data-ttu-id="6c661-175">В этом простом примере вы широковещательной рассылки push уведомления tooall устройствами Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="6c661-175">In this simple example, you broadcasted push notifications tooall your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="6c661-176">В заказ tootarget определенным пользователям, см. toohello [toousers уведомления toopush использования концентраторов уведомлений] учебника.</span><span class="sxs-lookup"><span data-stu-id="6c661-176">In order tootarget specific users, refer toohello [Use Notification Hubs toopush notifications toousers] tutorial.</span></span> 

<span data-ttu-id="6c661-177">Следует ли toosegment пользователям по группы интересов, можно прочитать [toosend использования концентраторов уведомлений, новости].</span><span class="sxs-lookup"><span data-stu-id="6c661-177">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="6c661-178">Дополнительные сведения о toouse концентраторов уведомлений в [руководство концентраторы уведомлений].</span><span class="sxs-lookup"><span data-stu-id="6c661-178">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance].</span></span>

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

