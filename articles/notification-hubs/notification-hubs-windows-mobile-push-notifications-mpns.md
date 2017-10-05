---
title: "Отправка push-уведомлений в приложения Windows Phone с помощью центров уведомлений Azure | Документация Майкрософт"
description: "Из этого учебника вы узнаете, как использовать центры уведомлений Azure для отправки push-уведомлений в приложение Silverlight для Windows Phone 8 или Windows Phone 8.1."
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
ms.openlocfilehash: f0bfe81f849813d146d644b32490af657b1071b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="fd889-104">Отправка push-уведомлений в приложения Windows Phone с помощью центров уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="fd889-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="fd889-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="fd889-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="fd889-106">Для работы с этим учебником необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="fd889-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="fd889-107">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="fd889-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fd889-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="fd889-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="fd889-109">В этом учебнике показано, как использовать центры уведомлений Azure для отправки push-уведомлений в приложение Silverlight для Windows Phone 8 или Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="fd889-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="fd889-110">Если вы ориентируетесь на Windows Phone 8.1 (не Silverlight), см. версию [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="fd889-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer to the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="fd889-111">В этом учебнике вам предстоит создать пустое приложение Windows Phone 8, получающее push-уведомления с помощью службы push-уведомлений Майкрософт (MPNS).</span><span class="sxs-lookup"><span data-stu-id="fd889-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using the Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="fd889-112">По завершении вы сможете рассылать push-уведомления на все устройства, где запущено ваше приложение, с помощью центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="fd889-112">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="fd889-113">Центры уведомлений Windows Phone SDK не поддерживают использование службы push-уведомлений Windows (WNS) с приложениями Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="fd889-113">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="fd889-114">Использование WNS (вместо MPNS) с приложениями Windows Phone 8.1 Silverlight описано в статье [Центр уведомлений: учебник для Windows Phone Silverlight], в котором используются API REST.</span><span class="sxs-lookup"><span data-stu-id="fd889-114">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="fd889-115">В этом учебнике описывается простой сценарий вещания с использованием Центров уведомлений.</span><span class="sxs-lookup"><span data-stu-id="fd889-115">The tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd889-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fd889-116">Prerequisites</span></span>
<span data-ttu-id="fd889-117">Для работы с данным учебником требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="fd889-117">This tutorial requires the following:</span></span>

* <span data-ttu-id="fd889-118">[Microsoft Visual Studio 2012 Express для Windows Phone]или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="fd889-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="fd889-119">Завершение изучения этого учебника является необходимым условием для работы со всеми другими учебниками, посвященными Центрам уведомлений для приложений Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="fd889-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="fd889-120">Создание центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="fd889-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="fd889-121">Щелкните раздел <b>Службы уведомлений</b> (в колонке <i>Параметры</i>), выберите пункт <b>Windows Phone (MPNS)</b> и установите флажок <b>Включить push-уведомления без проверки подлинности</b>.</span><span class="sxs-lookup"><span data-stu-id="fd889-121">Click the <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click the <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Azure Portal — включение push-уведомлений без проверки подлинности](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="fd889-123">Концентратор будет создан и настроен для отправки уведомлений без проверки подлинности для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="fd889-123">Your hub is now created and configured to send unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="fd889-124">В этом учебнике используется MPNS в режиме без проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="fd889-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="fd889-125">Режим MPNS без проверки подлинности налагает ограничения на использование уведомлений, отправляемых для каждого канала.</span><span class="sxs-lookup"><span data-stu-id="fd889-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send to each channel.</span></span> <span data-ttu-id="fd889-126">Центры уведомлений поддерживают [Режим работы MPNS с проверкой подлинности](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) , позволяя отправить ваш сертификат.</span><span class="sxs-lookup"><span data-stu-id="fd889-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you to upload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-to-the-notification-hub"></a><span data-ttu-id="fd889-127">Подключение приложения к центру уведомлений</span><span class="sxs-lookup"><span data-stu-id="fd889-127">Connecting your app to the notification hub</span></span>
1. <span data-ttu-id="fd889-128">В Visual Studio создайте новое консольное приложение Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="fd889-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="fd889-129">В Visual Studio 2013 с обновлением 2 вместо этого вы создаете приложение Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="fd889-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio — новый проект — пустое приложение — Windows Phone Silverlight][11]
2. <span data-ttu-id="fd889-131">В Visual Studio щелкните решение правой кнопкой мыши, а затем выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fd889-131">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="fd889-132">Откроется диалоговое окно **Управление пакетами NuGet** .</span><span class="sxs-lookup"><span data-stu-id="fd889-132">This displays the **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="fd889-133">Выполните поиск по запросу `WindowsAzure.Messaging.Managed` , щелкните **Установить**, а затем примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="fd889-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept the terms of use.</span></span>
   
    ![Visual Studio — диспетчер пакетов NuGet][20]
   
    <span data-ttu-id="fd889-135">После этого будут выполнены скачивание, установка и добавление ссылки на библиотеку Azure Messaging для Windows с помощью <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">пакета NuGet WindowsAzure.Messaging.Managed</a>.</span><span class="sxs-lookup"><span data-stu-id="fd889-135">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="fd889-136">Откройте файл App.xaml.cs и добавьте следующие инструкции `using` :</span><span class="sxs-lookup"><span data-stu-id="fd889-136">Open the file App.xaml.cs and add the following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="fd889-137">Добавьте следующий код в верхнюю часть метода **Application_Launching** в файле App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="fd889-137">Add the following code at the top of **Application_Launching** method in App.xaml.cs:</span></span>
   
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
   > <span data-ttu-id="fd889-138">Значение **MyPushChannel** — это индекс, который используется для поиска существующего канала в коллекции [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd889-138">The value **MyPushChannel** is an index that is used to lookup an existing channel in the [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="fd889-139">Если канал отсутствует, создайте новую запись с таким именем.</span><span class="sxs-lookup"><span data-stu-id="fd889-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="fd889-140">Обязательно вставьте имя концентратора и строку подключения с именем **DefaultListenSharedAccessSignature** , полученные в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="fd889-140">Make sure to insert the name of your hub and the connection string called **DefaultListenSharedAccessSignature** that you obtained in the previous section.</span></span>
    <span data-ttu-id="fd889-141">Этот код получает универсальный код ресурса (URI) канала (ChannelURI) для приложения из MPNS, а затем регистрирует ChannelURI в вашем центре уведомлений.</span><span class="sxs-lookup"><span data-stu-id="fd889-141">This code retrieves the channel URI for the app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="fd889-142">Он также гарантирует регистрацию ChannelURI в центре уведомлений при каждом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="fd889-142">It also guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fd889-143">В этом учебнике на устройство отправляется всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="fd889-143">This tutorial sends a toast notification to the device.</span></span> <span data-ttu-id="fd889-144">Когда вы отправляете всплывающее уведомление, необходимо вместо этого вызвать метод **BindToShellTile** в канале.</span><span class="sxs-lookup"><span data-stu-id="fd889-144">When you send a tile notification, you must instead call the **BindToShellTile** method on the channel.</span></span> <span data-ttu-id="fd889-145">Чтобы поддерживать одновременно и всплывающие уведомления, и уведомления на плитке, следует вызвать оба метода: **BindToShellTile** и **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="fd889-145">To support both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="fd889-146">В обозревателе решений разверните меню **Свойства**, откройте файл `WMAppManifest.xml`, перейдите на вкладку **Capabilities** (Возможности) и убедитесь, что установлен флажок **ID_CAP_PUSH_NOTIFICATION**.</span><span class="sxs-lookup"><span data-stu-id="fd889-146">In Solution Explorer, expand **Properties**, open the `WMAppManifest.xml` file, click the **Capabilities** tab, and make sure that the **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt to send a push notification to the app will fail.
7. <span data-ttu-id="fd889-147">Нажмите клавишу `F5` , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="fd889-147">Press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="fd889-148">В приложении отобразится сообщение о регистрации.</span><span class="sxs-lookup"><span data-stu-id="fd889-148">A registration message is displayed in the app.</span></span>
8. <span data-ttu-id="fd889-149">Закройте приложение.</span><span class="sxs-lookup"><span data-stu-id="fd889-149">Close the app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="fd889-150">Для получения всплывающего push-уведомления приложение не должно выполняться в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="fd889-150">To receive a toast push notification, the application must not be running in the foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="fd889-151">Отправка push-уведомлений из серверной части</span><span class="sxs-lookup"><span data-stu-id="fd889-151">Send push notifications from your backend</span></span>
<span data-ttu-id="fd889-152">Push-уведомления можно отправлять с помощью центров уведомлений с любого сервера через общедоступный <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">интерфейс REST</a>.</span><span class="sxs-lookup"><span data-stu-id="fd889-152">You can send push notifications by using Notification Hubs from any backend via the public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="fd889-153">В этом учебнике мы будем отправлять push-уведомления с помощью консольного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="fd889-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="fd889-154">Пример отправки push-уведомлений из серверной части веб-API ASP.NET, интегрированной с центрами уведомлений, см. в статье [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="fd889-154">For an example of how to send push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="fd889-155">Примеры отправки push-уведомлений с использованием [REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx) см. в статье [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) (Использование центров уведомлений из Java) и [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md) (Использование центров уведомлений из PHP).</span><span class="sxs-lookup"><span data-stu-id="fd889-155">For an example of how to send push notifications by using the [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="fd889-156">Щелкните решение правой кнопкой мыши, выберите пункты **Добавить** и **Создать проект...**. После этого в разделе **Visual C#** выберите **Windows** и **Консольное приложение**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fd889-156">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="fd889-157">При этом в решение добавляется новое консольное приложение Visual C#.</span><span class="sxs-lookup"><span data-stu-id="fd889-157">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="fd889-158">Это можно сделать также и в отдельном решении.</span><span class="sxs-lookup"><span data-stu-id="fd889-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="fd889-159">Щелкните **Сервис**, **Library Package Manager** (Диспетчер пакетов библиотеки), а затем — **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="fd889-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="fd889-160">Отобразится консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="fd889-160">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="fd889-161">В окне **консоли диспетчера пакетов** задайте свойство **Default project** (Проект по умолчанию) для нового проекта консольного приложения, а затем в окне консоли выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fd889-161">In the **Package Manager Console** window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="fd889-162">После этого будет добавлена ссылка на пакет SDK для Центров уведомлений Azure с помощью <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакета NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="fd889-162">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="fd889-163">Откройте файл `Program.cs` и добавьте следующую инструкцию `using`:</span><span class="sxs-lookup"><span data-stu-id="fd889-163">Open the `Program.cs` file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="fd889-164">Добавьте в класс `Program` следующий метод:</span><span class="sxs-lookup"><span data-stu-id="fd889-164">In the `Program` class, add the following method:</span></span>
   
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
   
    <span data-ttu-id="fd889-165">Обязательно замените заполнитель `<hub name>` именем центра уведомлений, которое отображается на портале.</span><span class="sxs-lookup"><span data-stu-id="fd889-165">Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the portal.</span></span> <span data-ttu-id="fd889-166">Кроме того, замените заполнитель строки подключения строкой подключения с именем **DefaultFullSharedAccessSignature** , полученной в разделе «Настройка концентратора уведомлений».</span><span class="sxs-lookup"><span data-stu-id="fd889-166">Also, replace the connection string placeholder with the connection string called **DefaultFullSharedAccessSignature** that you obtained in the section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fd889-167">Обязательно используйте строку подключения с **полным** доступом, а не доступом к **прослушиванию**.</span><span class="sxs-lookup"><span data-stu-id="fd889-167">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="fd889-168">У строки с доступом к прослушиванию отсутствуют разрешения для отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="fd889-168">The listen-access string does not have permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="fd889-169">Добавьте следующую строку в метод `Main` :</span><span class="sxs-lookup"><span data-stu-id="fd889-169">Add the following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="fd889-170">Когда эмулятор Windows Phone будет запущен, а приложение будет закрыто, установите проект приложения консоли в качестве начального проекта по умолчанию, после чего нажмите клавишу `F5` , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="fd889-170">With your Windows Phone emulator running and your app closed, set the console application project as the default startup project, and then press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="fd889-171">Вы получите всплывающее push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="fd889-171">You will receive a toast push notification.</span></span> <span data-ttu-id="fd889-172">Приложение загружается при касании этого всплывающего баннера.</span><span class="sxs-lookup"><span data-stu-id="fd889-172">Tapping the toast banner loads the app.</span></span>

<span data-ttu-id="fd889-173">В [каталоге всплывающих уведомлений] и [каталоге уведомлений на плитке] на сайте MSDN можно найти самые разнообразные полезные данные.</span><span class="sxs-lookup"><span data-stu-id="fd889-173">You can find all the possible payloads in the [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd889-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd889-174">Next steps</span></span>
<span data-ttu-id="fd889-175">В этом простом примере осуществляется широковещательная рассылка push-уведомлений на все устройства Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="fd889-175">In this simple example, you broadcasted push notifications to all your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="fd889-176">Сведения о том, как рассылать уведомления определенным пользователям, см. в руководстве [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET].</span><span class="sxs-lookup"><span data-stu-id="fd889-176">In order to target specific users, refer to the [Use Notification Hubs to push notifications to users] tutorial.</span></span> 

<span data-ttu-id="fd889-177">Если необходимо разделить пользователей по группам интересов, см. раздел [Использование концентраторов уведомлений для передачи экстренных новостей].</span><span class="sxs-lookup"><span data-stu-id="fd889-177">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="fd889-178">Дополнительные сведения об использовании концентраторов уведомлений см. в [руководстве по использованию концентраторов уведомлений].</span><span class="sxs-lookup"><span data-stu-id="fd889-178">Learn more about how to use Notification Hubs in [Notification Hubs Guidance].</span></span>

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
<span data-ttu-id="fd889-179">[Microsoft Visual Studio 2012 Express для Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span><span class="sxs-lookup"><span data-stu-id="fd889-179">[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span></span>
<span data-ttu-id="fd889-180">[руководстве по использованию концентраторов уведомлений]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="fd889-180">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
<span data-ttu-id="fd889-181">[Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="fd889-181">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="fd889-182">[Использование концентраторов уведомлений для передачи экстренных новостей]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span><span class="sxs-lookup"><span data-stu-id="fd889-182">[Use Notification Hubs to send breaking news]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span></span>
<span data-ttu-id="fd889-183">[каталоге всплывающих уведомлений]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="fd889-183">[toast catalog]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span></span>
<span data-ttu-id="fd889-184">[каталоге уведомлений на плитке]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="fd889-184">[tile catalog]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span></span>
<span data-ttu-id="fd889-185">[Центр уведомлений: учебник для Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span><span class="sxs-lookup"><span data-stu-id="fd889-185">[Notification Hubs - Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span></span>

