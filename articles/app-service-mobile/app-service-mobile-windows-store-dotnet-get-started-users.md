---
title: "Добавление проверки подлинности в приложение универсальной платформы Windows (UWP) | Документация Майкрософт"
description: "Узнайте, как использовать мобильные приложения службы приложений Azure, чтобы выполнять аутентификацию пользователей приложения универсальной платформы Windows (UWP) с помощью разных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Майкрософт."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 47da343d4ec956ec2e669757f56e853675f887a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="83a72-103">Добавление проверки подлинности в приложение Windows</span><span class="sxs-lookup"><span data-stu-id="83a72-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="83a72-104">В этом разделе показано, как добавить проверку подлинности на основе облака в мобильное приложение.</span><span class="sxs-lookup"><span data-stu-id="83a72-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="83a72-105">В этом учебнике вы добавите проверку подлинности в проект быстрого запуска универсальной платформы Windows (UWP) для мобильных приложений, используя поставщик удостоверений, поддерживаемый службой приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="83a72-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="83a72-106">После успешной проверки подлинности и авторизации сервером мобильных приложений отображается значение идентификатора пользователя.</span><span class="sxs-lookup"><span data-stu-id="83a72-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="83a72-107">Этот учебник создан на основе краткого руководства по мобильным приложениям.</span><span class="sxs-lookup"><span data-stu-id="83a72-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="83a72-108">Вам необходимо сначала изучить учебник [Начало работы с мобильными приложениями](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83a72-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="83a72-109"><a name="register"></a>Регистрация приложения для проверки подлинности и настройка службы приложений</span><span class="sxs-lookup"><span data-stu-id="83a72-109"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="83a72-110"><a name="redirecturl"></a>Добавление приложения в список разрешенных URL-адресов внешнего перенаправления</span><span class="sxs-lookup"><span data-stu-id="83a72-110"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="83a72-111">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="83a72-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="83a72-112">Это позволяет системе аутентификации выполнять перенаправление обратно в приложение после завершения процесса аутентификации.</span><span class="sxs-lookup"><span data-stu-id="83a72-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="83a72-113">В этом руководстве мы повсеместно используем схему URL-адресов _appname_.</span><span class="sxs-lookup"><span data-stu-id="83a72-113">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="83a72-114">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="83a72-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="83a72-115">Она должна быть уникальной для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="83a72-115">It should be unique to your mobile application.</span></span> <span data-ttu-id="83a72-116">Вот как можно включить перенаправление на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="83a72-116">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="83a72-117">На портале Azure выберите свою службу приложений.</span><span class="sxs-lookup"><span data-stu-id="83a72-117">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="83a72-118">Выберите пункт меню **Аутентификация или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="83a72-118">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="83a72-119">В поле **Разрешенные URL-адреса внешнего перенаправления** введите `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="83a72-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="83a72-120">**url_scheme_of_your_app** в этой строке — это схема URL-адресов для вашего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="83a72-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="83a72-121">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="83a72-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="83a72-122">Необходимо записать выбранную строку, так как потребуется в нескольких местах настроить код мобильного приложения с использованием схемы URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="83a72-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="83a72-123">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="83a72-123">Click **OK**.</span></span>

5. <span data-ttu-id="83a72-124">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="83a72-124">Click **Save**.</span></span>

## <span data-ttu-id="83a72-125"><a name="permissions"></a>Предоставление разрешений только пользователям, прошедшим проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="83a72-125"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="83a72-126">Теперь можно убедиться, что анонимный доступ к серверной части был отключен.</span><span class="sxs-lookup"><span data-stu-id="83a72-126">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="83a72-127">Назначив проект приложения UWP запускаемым проектом, разверните и запустите приложение. Убедитесь в том, что после его запуска порождается необработанное исключение с кодом состояния 401 (не авторизован).</span><span class="sxs-lookup"><span data-stu-id="83a72-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="83a72-128">Это происходит потому, что приложение пытается получить доступ к коду мобильного приложения от имени пользователя, не прошедшего проверку подлинности, но таблице *TodoItem* теперь требуется проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="83a72-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="83a72-129">Далее вы обновите приложение, чтобы оно выполняло проверку подлинности пользователей перед запросом ресурсов из службы приложений.</span><span class="sxs-lookup"><span data-stu-id="83a72-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="83a72-130"><a name="add-authentication"></a>Добавление проверки подлинности в приложение</span><span class="sxs-lookup"><span data-stu-id="83a72-130"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="83a72-131">В файле MainPage.xaml.cs проекта приложения UWP добавьте следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="83a72-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="83a72-132">Этот код выполняет проверку подлинности пользователя с помощью имени входа в Facebook.</span><span class="sxs-lookup"><span data-stu-id="83a72-132">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="83a72-133">Если используется поставщик удостоверений, отличный от Facebook, измените значение **MobileServiceAuthenticationProvider** выше на значение для вашего поставщика.</span><span class="sxs-lookup"><span data-stu-id="83a72-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="83a72-134">Замените метод **OnNavigatedTo()** в файле MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="83a72-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="83a72-135">Затем добавьте кнопку **Вход** в приложение, которое запускает проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="83a72-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="83a72-136">Добавьте в файл MainPage.xaml.cs следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="83a72-136">Add the following code snippet to the MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Switch the buttons and load items from the mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="83a72-137">Откройте файл проекта MainPage.xaml, найдите элемент, который определяет кнопку **Сохранить** и замените его следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="83a72-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. <span data-ttu-id="83a72-138">Добавьте в файл App.xaml.cs следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="83a72-138">Add the following code snippet to the App.xaml.cs:</span></span>

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. <span data-ttu-id="83a72-139">Откройте файл Package.appxmanifest, перейдите к разделу **Объявления**, в раскрывающемся списке **Доступные объявления** выберите пункт **Протокол** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83a72-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="83a72-140">Далее настройте **свойства** объявления **протокола**.</span><span class="sxs-lookup"><span data-stu-id="83a72-140">Now configure the **Properties** of the **Protocol** declaration.</span></span> <span data-ttu-id="83a72-141">В поле **Отображаемое имя** добавьте имя, которое должно отображаться для пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="83a72-141">In **Display name**, add the name you wish to display to users of your application.</span></span> <span data-ttu-id="83a72-142">В поле **Имя** добавьте {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="83a72-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="83a72-143">Нажмите клавишу F5, чтобы запустить приложение, нажмите кнопку **Вход** и войдите в приложение с помощью выбранного поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="83a72-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="83a72-144">После успешного входа приложение работает без ошибок, а вы должны быть в состоянии выполнять запросы к серверной части и обновлять данные.</span><span class="sxs-lookup"><span data-stu-id="83a72-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <span data-ttu-id="83a72-145"><a name="tokens"></a>Сохранение токена проверки подлинности в клиенте</span><span class="sxs-lookup"><span data-stu-id="83a72-145"><a name="tokens"></a>Store the authentication token on the client</span></span>
<span data-ttu-id="83a72-146">В предыдущем примере был показан стандартный вход, при котором клиенту нужно подключаться к поставщику удостоверений и службе приложений каждый раз, когда приложение запускается.</span><span class="sxs-lookup"><span data-stu-id="83a72-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="83a72-147">Мало того что этот метод неэффективен, вы можете столкнуться с проблемами, связанными с использованием приложения, если большое количество клиентов попытаются запустить приложение одновременно.</span><span class="sxs-lookup"><span data-stu-id="83a72-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="83a72-148">Лучше кэшировать токен авторизации, который возвратила служба приложений, причем делать это до входа через поставщика.</span><span class="sxs-lookup"><span data-stu-id="83a72-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="83a72-149">Токен, выданный службами приложений, можно кэшировать независимо от используемой аутентификации (управляемая службой либо клиентом).</span><span class="sxs-lookup"><span data-stu-id="83a72-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="83a72-150">Этот учебник использует управляемую сервером проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="83a72-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="83a72-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83a72-151">Next steps</span></span>
<span data-ttu-id="83a72-152">Вы прошли этот учебник по обычной проверке подлинности и теперь можете перейти к одному из следующих учебников:</span><span class="sxs-lookup"><span data-stu-id="83a72-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="83a72-153">Добавление push-уведомлений в приложение</span><span class="sxs-lookup"><span data-stu-id="83a72-153">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="83a72-154">Узнайте, как добавить поддержку push-уведомлений в мобильное приложение и настроить в его серверной части использование концентраторов уведомлений Azure для отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="83a72-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="83a72-155">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="83a72-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="83a72-156">Узнайте, как добавить в приложение поддержку автономной работы с помощью серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="83a72-156">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="83a72-157">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением &mdash; просматривать, добавлять или изменять данные &mdash; даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="83a72-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
