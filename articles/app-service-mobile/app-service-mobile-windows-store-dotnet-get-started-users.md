---
title: "приложения универсальной платформы Windows (UWP) tooyour authentication aaaAdd | Документы Microsoft"
description: "Узнайте, как пользователи tooauthenticate toouse мобильные приложения службы приложений Azure с помощью различных поставщиков удостоверений, включая приложения универсальной платформы Windows (UWP): AAD, Google, Facebook, Twitter и Майкрософт."
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
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="b6011-103">Добавление приложения Windows authentication tooyour</span><span class="sxs-lookup"><span data-stu-id="b6011-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="b6011-104">В этом разделе показано, как tooadd проверку подлинности на основе облака tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b6011-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="b6011-105">В этом учебнике добавлении проверки подлинности toohello универсальной платформы Windows (UWP) быстрый запуск проекта для мобильных приложений с помощью поставщика удостоверений, который поддерживается службой приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="b6011-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="b6011-106">После успешного проверку подлинности и авторизацию серверной части мобильного приложения, отображается значение идентификатора пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b6011-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="b6011-107">Этот учебник основывается на примеры использования мобильные приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b6011-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="b6011-108">Необходимо сначала пройти учебник hello [начало работы с мобильным приложениям](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6011-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="b6011-109"><a name="register"></a>Регистрация приложения для проверки подлинности и настройка hello службы приложений</span><span class="sxs-lookup"><span data-stu-id="b6011-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="b6011-110"><a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений</span><span class="sxs-lookup"><span data-stu-id="b6011-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="b6011-111">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="b6011-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="b6011-112">Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="b6011-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="b6011-113">В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении.</span><span class="sxs-lookup"><span data-stu-id="b6011-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="b6011-114">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="b6011-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="b6011-115">Он должен быть уникальным tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b6011-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="b6011-116">tooenable hello перенаправления на стороне сервера hello:</span><span class="sxs-lookup"><span data-stu-id="b6011-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="b6011-117">В hello [Azure портал] выберите приложение службы.</span><span class="sxs-lookup"><span data-stu-id="b6011-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="b6011-118">Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="b6011-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="b6011-119">В hello **допускается внешний URL-адреса перенаправления**, введите `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="b6011-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="b6011-120">Hello **url_scheme_of_your_app** в данной строке — hello схема URL-адресов для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b6011-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="b6011-121">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="b6011-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="b6011-122">Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.</span><span class="sxs-lookup"><span data-stu-id="b6011-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="b6011-123">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b6011-123">Click **OK**.</span></span>

5. <span data-ttu-id="b6011-124">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b6011-124">Click **Save**.</span></span>

## <span data-ttu-id="b6011-125"><a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="b6011-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="b6011-126">Теперь вы можете подтвердить этой серверной tooyour анонимный доступ отключен.</span><span class="sxs-lookup"><span data-stu-id="b6011-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="b6011-127">Задать в качестве запускаемого проекта hello hello проекта приложения UWP развертывание и запуск приложения hello; Убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b6011-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="b6011-128">Это происходит потому, что приложение hello пытается tooaccess код мобильного приложения без проверки подлинности пользователя, но hello *TodoItem* таблица теперь требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b6011-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="b6011-129">Затем пользователи tooauthenticate приложения hello обновляете перед запросом ресурсы из приложения службы.</span><span class="sxs-lookup"><span data-stu-id="b6011-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="b6011-130"><a name="add-authentication"></a>Добавить приложение toohello проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="b6011-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="b6011-131">В проекте приложения UWP hello файл MainPage.xaml.cs и добавьте следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="b6011-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
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
   
    <span data-ttu-id="b6011-132">Этот код проверяет подлинность пользователя hello с именем входа для Facebook.</span><span class="sxs-lookup"><span data-stu-id="b6011-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="b6011-133">При использовании поставщика удостоверений, отличные от Facebook, измените значение hello **MobileServiceAuthenticationProvider** выше значения toohello для поставщика.</span><span class="sxs-lookup"><span data-stu-id="b6011-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="b6011-134">Замените hello **OnNavigatedTo()** метод в файле MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="b6011-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="b6011-135">Далее вы добавите **вход** кнопку toohello приложение, запускающее проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b6011-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="b6011-136">Добавьте следующий фрагмент кода toohello MainPage.xaml.cs hello:</span><span class="sxs-lookup"><span data-stu-id="b6011-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="b6011-137">Откройте файл проекта MainPage.xaml hello, найдите элемент hello, определяющий hello **Сохранить** кнопку и заменить ее именем hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="b6011-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
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
5. <span data-ttu-id="b6011-138">Добавьте следующий фрагмент кода toohello App.xaml.cs hello:</span><span class="sxs-lookup"><span data-stu-id="b6011-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

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
6. <span data-ttu-id="b6011-139">Откройте файл Package.appxmanifest, перейдите в каталог слишком**объявления**в **доступные объявления** раскрывающегося списка выберите **протокола** и нажмите кнопку **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b6011-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="b6011-140">Теперь настройка hello **свойства** из hello **протокола** объявления.</span><span class="sxs-lookup"><span data-stu-id="b6011-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="b6011-141">В **отображаемое имя**, добавьте имя hello нужно toousers toodisplay приложения.</span><span class="sxs-lookup"><span data-stu-id="b6011-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="b6011-142">В поле **Имя** добавьте {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="b6011-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="b6011-143">Нажмите клавиши приложение hello ключа toorun hello F5, щелкните hello **вход** кнопки и вход в приложение hello с поставщиком удостоверений выбранной.</span><span class="sxs-lookup"><span data-stu-id="b6011-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="b6011-144">Вход в систему после успешного завершения, приложение hello выполняется без ошибок, и вы могли tooquery серверной части и производить toodata обновлений.</span><span class="sxs-lookup"><span data-stu-id="b6011-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="b6011-145"><a name="tokens"></a>Маркер проверки подлинности hello хранилища на приветствия клиента</span><span class="sxs-lookup"><span data-stu-id="b6011-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="b6011-146">Предыдущий пример Hello показал стандартный вход, требующий toocontact клиента hello оба поставщика удостоверений hello и hello службы приложений, каждый раз при запуске этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b6011-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="b6011-147">Не только неэффективен этот метод, можно запустить в использовании относится проблемы следует пробовать многие клиенты toostart приложения на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="b6011-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="b6011-148">Лучшим подходом является toocache hello авторизации токен, возвращенный вашей службы приложений и повторите toouse это перед использованием сначала вход на основе поставщика.</span><span class="sxs-lookup"><span data-stu-id="b6011-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="b6011-149">Можно кэшировать маркер hello, выдаваемые службой приложения независимо от того, используется ли-управляемый клиент или служба проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b6011-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="b6011-150">Этот учебник использует управляемую сервером проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b6011-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="b6011-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6011-151">Next steps</span></span>
<span data-ttu-id="b6011-152">Завершения этого учебника обычной проверки подлинности, рассмотрите возможность продолжить на tooone из hello следующие учебники:</span><span class="sxs-lookup"><span data-stu-id="b6011-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="b6011-153">Добавить приложение tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="b6011-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="b6011-154">Узнайте, как push-уведомления tooadd поддерживают tooyour приложения и настройки вашего мобильного приложения серверной toouse концентраторов уведомлений Azure toosend push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b6011-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="b6011-155">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="b6011-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="b6011-156">Узнайте, как автономные tooadd поддерживают приложения с помощью внутреннего сервера мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b6011-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="b6011-157">Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения.</span><span class="sxs-lookup"><span data-stu-id="b6011-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
