---
title: "Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET"
description: "Узнайте, как отправлять безопасные push-уведомления в Azure. Примеры кода написаны на C# с использованием API .NET."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: c0b963ef661612b1a176dd8e5f01d56e61eb5acb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="4c10f-104">Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET</span><span class="sxs-lookup"><span data-stu-id="4c10f-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="4c10f-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="4c10f-105">Overview</span></span>
<span data-ttu-id="4c10f-106">Поддержка push-уведомлений в Azure позволяет получить доступ к простой в использовании, многоплатформенной и масштабируемой инфраструктуре для отправки push-уведомлений, которая значительно упрощает реализацию push-уведомлений как для индивидуальных пользователей, так и для корпоративных приложений для мобильных платформ.</span><span class="sxs-lookup"><span data-stu-id="4c10f-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="4c10f-107">В этом учебнике показано, как использовать концентраторы уведомлений Azure для отправки push-уведомлений пользователю определенного приложения на конкретном устройстве.</span><span class="sxs-lookup"><span data-stu-id="4c10f-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="4c10f-108">Для проверки подлинности клиентов используется серверная часть веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4c10f-108">An ASP.NET WebAPI backend is used to authenticate clients.</span></span> <span data-ttu-id="4c10f-109">С помощью пользователя, прошедшего проверку подлинности клиента, тег будет добавляться автоматически на серверной части для регистрации уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4c10f-109">Using the authenticated client user, and tag will be automatically added by the backend to notification registration.</span></span> <span data-ttu-id="4c10f-110">Этот тег будет использоваться для отправки с серверной части для создания уведомлений конкретному пользователю.</span><span class="sxs-lookup"><span data-stu-id="4c10f-110">This tag will be used to send by the backend to generate notifications for a specific user.</span></span> <span data-ttu-id="4c10f-111">Дополнительные сведения о регистрации уведомлений с помощью серверной части приложения см. в разделе руководства [Регистрация из внутренней службы приложения](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c10f-111">For more information on registering for notifications using an app backend, see the guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="4c10f-112">В этом руководстве используется центр уведомлений и проект, созданные вами при работе с руководством [Начало работы с Центрами уведомлений для приложений универсальной платформы Windows].</span><span class="sxs-lookup"><span data-stu-id="4c10f-112">This tutorial builds on the notification hub and project that you created in the [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="4c10f-113">Этот учебник также необходимо изучить перед обращением к учебнику [Безопасные push-уведомления] .</span><span class="sxs-lookup"><span data-stu-id="4c10f-113">This tutorial is also the prerequisite to the [Secure Push] tutorial.</span></span> <span data-ttu-id="4c10f-114">После выполнения действий, о которых рассказывается в данном учебнике, вы можете приступать к работе с учебником [Безопасные push-уведомления] , в котором рассказывается, как изменить код, указанный в этом учебнике, для безопасной отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4c10f-114">After you have completed the steps in this tutorial, you can proceed to the [Secure Push] tutorial, which shows how to modify the code in this tutorial to send a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4c10f-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4c10f-115">Before you begin</span></span>
<span data-ttu-id="4c10f-116">Мы очень ценим ваши отзывы.</span><span class="sxs-lookup"><span data-stu-id="4c10f-116">We do take your feedback seriously.</span></span> <span data-ttu-id="4c10f-117">Если у вас возникли трудности с выполнением действий, описанных в этой статье, или у вас есть рекомендации по улучшению этого материала, пожалуйста, поделитесь с нами своими наблюдениями, воспользовавшись формой в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="4c10f-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span>

<span data-ttu-id="4c10f-118">Полный код для этого учебника можно найти на портале [GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="4c10f-118">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4c10f-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4c10f-119">Prerequisites</span></span>
<span data-ttu-id="4c10f-120">Перед началом работы с этим учебником необходимо изучить следующие учебники по мобильным службам.</span><span class="sxs-lookup"><span data-stu-id="4c10f-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="4c10f-121">[Начало работы с Центрами уведомлений для приложений универсальной платформы Windows]</span><span class="sxs-lookup"><span data-stu-id="4c10f-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="4c10f-122">С помощью этого учебника вы создадите центр уведомлений, зарезервируете имя приложения и зарегистрируетесь для получения уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4c10f-122">You create your notification hub and reserve the app name and register to receive notifications in this tutorial.</span></span> <span data-ttu-id="4c10f-123">В этом учебнике предполагается, что следующие действия уже были предприняты.</span><span class="sxs-lookup"><span data-stu-id="4c10f-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="4c10f-124">В противном случае выполните действия, описанные в статье [Начало работы с Центрами уведомлений для приложений универсальной платформы Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), в частности в разделах [Регистрация приложения для Магазина Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) и [Настройка концентратора уведомлений](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="4c10f-124">If not, please follow the steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, the sections [Register your app for the Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="4c10f-125">Обязательно проверьте, что вы ввели на портале значения полей **SID пакета** и **Секрет клиента**, на вкладке **Настройка** для концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4c10f-125">In particular, make sure that you have entered the **Package SID** and **Client Secret** values in the portal, in the **Configure** tab for your notification hub.</span></span> <span data-ttu-id="4c10f-126">Эта процедура настройки описывается в разделе [Настройка концентратора уведомлений](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="4c10f-126">This configuration procedure is described in the section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="4c10f-127">Этот шаг имеет большое значение: если учетные данные на портале не соответствуют учетным данным, указанным для выбранного имени приложения, push-уведомление не будет успешно выполнено.</span><span class="sxs-lookup"><span data-stu-id="4c10f-127">This is an important step: if the credentials on the portal do not match those specified for the app name you choose, the push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="4c10f-128">Если вы используете мобильные приложения в службе приложений Azure в качестве внутренней службы, то перейдите к [версии этого учебника для мобильных приложений](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="4c10f-128">If you are using Mobile Apps in Azure App Service as your backend service, see the [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-the-code-for-the-client-project"></a><span data-ttu-id="4c10f-129">Обновите код для клиентского проекта</span><span class="sxs-lookup"><span data-stu-id="4c10f-129">Update the code for the client project</span></span>
<span data-ttu-id="4c10f-130">В этом разделе вы обновите код в проекте, который вы завершили при работе с учебником [Начало работы с Центрами уведомлений для приложений универсальной платформы Windows] .</span><span class="sxs-lookup"><span data-stu-id="4c10f-130">In this section, you update the code in the project you completed for the [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="4c10f-131">Проект уже должен быть связан с хранилищем и настроен под концентратор уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4c10f-131">The should already be associated with the store and configured for your notification hub.</span></span> <span data-ttu-id="4c10f-132">В этом разделе вы добавите код для вызова нового внутреннего веб-API и используете его для регистрации и отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4c10f-132">In this section, you will add code to call the new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="4c10f-133">В Visual Studio откройте решение, созданное при работе с учебником [Начало работы с Центрами уведомлений для приложений универсальной платформы Windows] .</span><span class="sxs-lookup"><span data-stu-id="4c10f-133">In Visual Studio, open the the solution you created for the [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="4c10f-134">В обозревателе решений щелкните правой кнопкой мыши проект **(Windows 8.1)** и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-134">In Solution Explorer, right-click the **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="4c10f-135">В левой части окна выберите **В сети**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-135">On the left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="4c10f-136">В текстовом поле **Поиск** введите **Клиент HTTP**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-136">In the **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="4c10f-137">В списке результатов выберите **Клиентские библиотеки Microsoft HTTP** и нажмите **Установить**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-137">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="4c10f-138">Выполните установку.</span><span class="sxs-lookup"><span data-stu-id="4c10f-138">Complete the installation.</span></span>
6. <span data-ttu-id="4c10f-139">Вернитесь к полю NuGet **Поиск** и введите **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-139">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="4c10f-140">Установите пакет **Json.NET** и затем закройте окно диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c10f-140">Install the **Json.NET** package, and then close the NuGet Package Manager window.</span></span>
7. <span data-ttu-id="4c10f-141">Повторите предыдущие шаги для проекта **(Windows Phone 8.1)**, чтобы установить пакет NuGet **JSON.NET** для проекта Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="4c10f-141">Repeat the steps above for the **(Windows Phone 8.1)** project to install the **JSON.NET** NuGet package for the Windows Phone project.</span></span>
8. <span data-ttu-id="4c10f-142">В обозревателе решений в проекте **(Windows 8.1)** дважды щелкните файл **MainPage.xaml**, чтобы открыть его в редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c10f-142">In Solution Explorer, in the **(Windows 8.1)** project, double-click **MainPage.xaml** to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="4c10f-143">В XML-коде файла **MainPage.xaml** замените раздел `<Grid>` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="4c10f-143">In the **MainPage.xaml** XML code, replace the `<Grid>` section with the following code.</span></span> <span data-ttu-id="4c10f-144">Этот код добавляет текстовое поле имени пользователя и пароля, которые будут использоваться для проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="4c10f-144">This code adds a username and password textbox that the user will authenticate with.</span></span> <span data-ttu-id="4c10f-145">Он также добавляет текстовые поля для сообщения уведомления и тег имени пользователя, который должен получать уведомления:</span><span class="sxs-lookup"><span data-stu-id="4c10f-145">It also adds textboxes for the notification message and the username tag that should receive the notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag To Send To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="4c10f-146">В обозревателе решений в проекте **(Windows Phone 8.1)** откройте файл **MainPage.xaml** и замените раздел `<Grid>` Windows Phone 8.1 приведенным выше кодом.</span><span class="sxs-lookup"><span data-stu-id="4c10f-146">In Solution Explorer, in the **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace the Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="4c10f-147">Интерфейс должен выглядеть приблизительно так.</span><span class="sxs-lookup"><span data-stu-id="4c10f-147">The interface should look similar to whats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="4c10f-148">В обозревателе решений откройте файл **MainPage.xaml.cs** для проектов **(Windows 8.1)** и **(Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-148">In Solution Explorer, open the **MainPage.xaml.cs** file for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="4c10f-149">В верхнюю часть каждого из файлов добавьте такие `using` операторы:</span><span class="sxs-lookup"><span data-stu-id="4c10f-149">Add the following `using` statements at the top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="4c10f-150">В файле **MainPage.xaml.cs** для проектов **(Windows 8.1)** и **(Windows Phone 8.1)** добавьте в класс `MainPage` следующий элемент.</span><span class="sxs-lookup"><span data-stu-id="4c10f-150">In **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add the following member to the `MainPage` class.</span></span> <span data-ttu-id="4c10f-151">Обязательно замените `<Enter Your Backend Endpoint>` фактической конечной точкой серверной части, полученной ранее.</span><span class="sxs-lookup"><span data-stu-id="4c10f-151">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="4c10f-152">Например, `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="4c10f-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="4c10f-153">В файле **MainPage.xaml.cs** для проектов **(Windows 8.1)** и **(Windows Phone 8.1)** добавьте в класс MainPage приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="4c10f-153">Add the code below to the MainPage class in **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="4c10f-154">Метод `PushClick` является обработчиком нажатия для кнопки **Отправить push-уведомление** .</span><span class="sxs-lookup"><span data-stu-id="4c10f-154">The `PushClick` method is the click handler for the **Send Push** button.</span></span> <span data-ttu-id="4c10f-155">Он обеспечивает отправку серверной частью уведомлений на все устройства с тегом имени пользователя, который соответствует параметру `to_tag` .</span><span class="sxs-lookup"><span data-stu-id="4c10f-155">It calls the backend to trigger a notification to all devices with a username tag that matches the `to_tag` parameter.</span></span> <span data-ttu-id="4c10f-156">Сообщение уведомления отправляется в виде JSON-содержимого в теле запроса.</span><span class="sxs-lookup"><span data-stu-id="4c10f-156">The notification message is sent as JSON content in the request body.</span></span>
    
    <span data-ttu-id="4c10f-157">Метод `LoginAndRegisterClick` является обработчиком нажатия для кнопки **Вход и регистрация** .</span><span class="sxs-lookup"><span data-stu-id="4c10f-157">The `LoginAndRegisterClick` method is the click handler for the **Log in and register** button.</span></span> <span data-ttu-id="4c10f-158">Он сохраняет маркер проверки подлинности в локальном хранилище (обратите внимание, что это относится к любому маркеру, используемому в данной схеме проверки подлинности), а затем с помощью `RegisterClient` подписывается на получение уведомлений, используя серверную часть.</span><span class="sxs-lookup"><span data-stu-id="4c10f-158">It stores the basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` to register for notifications using the backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed to send " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // The "username:<user name>" tag gets automatically added by the message handler in the backend.
            // The tag passed here can be whatever other tags you may want to use.
            try
            {
                // The device handle used will be different depending on the device and PNS. 
                // Windows devices use the channel uri as the PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed to register with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="4c10f-159">В обозревателе решений в проекте **Shared** откройте файл **App.xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-159">In Solution Explorer, under the **Shared** project, open the **App.xaml.cs** file.</span></span> <span data-ttu-id="4c10f-160">В обработчике событий `OnLaunched()` найдите вызов `InitNotificationsAsync()`:</span><span class="sxs-lookup"><span data-stu-id="4c10f-160">Find the call to `InitNotificationsAsync()` in the `OnLaunched()` event handler.</span></span> <span data-ttu-id="4c10f-161">Закомментируйте или удалите вызов `InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="4c10f-161">Comment out or delete the call to `InitNotificationsAsync()`.</span></span> <span data-ttu-id="4c10f-162">Обработчик кнопки, добавленный выше, инициализирует регистрацию уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4c10f-162">The button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="4c10f-163">В обозревателе решений щелкните правой кнопкой мыши проект **Shared**, щелкните **Добавить**, а затем **Класс**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-163">In Solution Explorer, right-click the **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="4c10f-164">Присвойте классу имя **RegisterClient.cs**, затем нажмите кнопку **ОК**, чтобы создать класс.</span><span class="sxs-lookup"><span data-stu-id="4c10f-164">Name the class **RegisterClient.cs**, then click **OK** to generate the class.</span></span>
   
   <span data-ttu-id="4c10f-165">Этот класс будет реализовать вызовы REST, необходимые для связи с серверной частью приложения, с целью регистрации в службе push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4c10f-165">This class will wrap the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="4c10f-166">В данном случае также происходит локальное сохранение идентификаторов *registrationId* , созданных концентратором уведомлений в соответствии с описанием в разделе [Регистрация из серверной части приложения](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c10f-166">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="4c10f-167">Обратите внимание, что в данном случае используется маркер проверки подлинности, сохраненный в локальном хранилище при нажатии кнопки **Вход и регистрация** .</span><span class="sxs-lookup"><span data-stu-id="4c10f-167">Note that it uses an authorization token stored in local storage when you click the **Log in and register** button.</span></span>
2. <span data-ttu-id="4c10f-168">Добавьте в начало файла RegisterClient.cs следующие операторы `using` :</span><span class="sxs-lookup"><span data-stu-id="4c10f-168">Add the following `using` statements at the top of the RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="4c10f-169">Добавьте в определение класса `RegisterClient` следующий код:</span><span class="sxs-lookup"><span data-stu-id="4c10f-169">Add the following code inside the `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="4c10f-170">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="4c10f-170">Save all your changes.</span></span>

## <a name="testing-the-application"></a><span data-ttu-id="4c10f-171">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="4c10f-171">Testing the Application</span></span>
1. <span data-ttu-id="4c10f-172">Запустите приложение в Windows 8.1 и Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="4c10f-172">Launch the application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="4c10f-173">Для Windows Phone 8.1 запустить экземпляр можно в эмуляторе или в самом устройстве.</span><span class="sxs-lookup"><span data-stu-id="4c10f-173">For Windows Phone 8.1 you can run the instance in the emulator or an actual device.</span></span>
2. <span data-ttu-id="4c10f-174">В экземпляре приложения Windows 8.1 введите **имя пользователя** и **пароль**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4c10f-174">In the Windows 8.1 instance of the app, enter a **Username** and **Password** as shown in the screen below.</span></span> <span data-ttu-id="4c10f-175">Они должны отличаться от имени пользователя и пароля, вводимых в Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="4c10f-175">It should differ from the user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="4c10f-176">Щелкните **Вход и регистрация** и убедитесь, что в диалоговом окне отображается подтверждение выполнения входа.</span><span class="sxs-lookup"><span data-stu-id="4c10f-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="4c10f-177">Таким образом будет активирована кнопка **Отправить push-уведомление** .</span><span class="sxs-lookup"><span data-stu-id="4c10f-177">This will also enable the **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="4c10f-178">В экземпляре Windows Phone 8.1 введите строку с именем пользователя в поле **Имя пользователя** и в поле **Пароль**, затем щелкните **Вход и регистрация**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-178">On the Windows Phone 8.1 instance, enter a user name string in both the **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="4c10f-179">Затем в поле **Тег имени получателя** введите имя пользователя, зарегистрированное в Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="4c10f-179">Then in the **Recipient Username Tag** field, enter the user name registered on Windows 8.1.</span></span> <span data-ttu-id="4c10f-180">Введите сообщение уведомления и нажмите кнопку **Отправить push-уведомление**.</span><span class="sxs-lookup"><span data-stu-id="4c10f-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="4c10f-181">Сообщения уведомления могут получать только устройства с зарегистрированным соответствующим тегом имени получателя.</span><span class="sxs-lookup"><span data-stu-id="4c10f-181">Only the devices that have registered with the matching username tag receive the notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="4c10f-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c10f-182">Next Steps</span></span>
* <span data-ttu-id="4c10f-183">Если необходимо разделить пользователей по группам интересов, см. раздел [Использование концентраторов уведомлений для передачи экстренных новостей].</span><span class="sxs-lookup"><span data-stu-id="4c10f-183">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span>
* <span data-ttu-id="4c10f-184">Дополнительную информацию об использовании центров уведомлений можно найти в [руководстве по использованию центров уведомлений].</span><span class="sxs-lookup"><span data-stu-id="4c10f-184">To learn more about how to use Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
<span data-ttu-id="4c10f-185">[Начало работы с Центрами уведомлений для приложений универсальной платформы Windows]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="4c10f-185">[Get started with Notification Hubs]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="4c10f-186">[Безопасные push-уведомления]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="4c10f-186">[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span></span>
<span data-ttu-id="4c10f-187">[Использование концентраторов уведомлений для передачи экстренных новостей]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="4c10f-187">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
<span data-ttu-id="4c10f-188">[руководстве по использованию центров уведомлений]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="4c10f-188">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
