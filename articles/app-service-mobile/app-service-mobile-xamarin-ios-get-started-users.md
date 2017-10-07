---
title: "aaaGet запущена с использованием проверки подлинности для мобильных приложений в Xamarin iOS"
description: "Узнайте, каким образом пользователи tooauthenticate toouse мобильные приложения Xamarin приложения iOS с помощью различных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="11d3a-103">Добавление приложения Xamarin.iOS tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="11d3a-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="11d3a-104">В этом разделе показано, как пользователи tooauthenticate приложение службы мобильных приложений из клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="11d3a-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="11d3a-105">В этом учебнике добавления проверки подлинности toohello Xamarin.iOS быстрый запуск проекта с помощью поставщика удостоверений, который поддерживается службой приложений.</span><span class="sxs-lookup"><span data-stu-id="11d3a-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="11d3a-106">После успешного проверку подлинности или авторизации мобильного приложения, отображается значение идентификатора пользователя hello и будет может tooaccess только табличные данные.</span><span class="sxs-lookup"><span data-stu-id="11d3a-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="11d3a-107">Необходимо сначала пройти учебник hello [Создание приложения Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="11d3a-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="11d3a-108">Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакета расширения проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="11d3a-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="11d3a-109">Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="11d3a-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="11d3a-110">Регистрация приложения для проверки подлинности и настройка служб приложений</span><span class="sxs-lookup"><span data-stu-id="11d3a-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="11d3a-111">Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений</span><span class="sxs-lookup"><span data-stu-id="11d3a-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="11d3a-112">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="11d3a-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="11d3a-113">Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="11d3a-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="11d3a-114">В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении.</span><span class="sxs-lookup"><span data-stu-id="11d3a-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="11d3a-115">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="11d3a-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="11d3a-116">Он должен быть уникальным tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="11d3a-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="11d3a-117">tooenable hello перенаправления на стороне сервера hello:</span><span class="sxs-lookup"><span data-stu-id="11d3a-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="11d3a-118">В hello [Azure портал] выберите приложение службы.</span><span class="sxs-lookup"><span data-stu-id="11d3a-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="11d3a-119">Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="11d3a-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="11d3a-120">В hello **допускается внешний URL-адреса перенаправления**, введите `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="11d3a-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="11d3a-121">Hello **url_scheme_of_your_app** в данной строке — hello схема URL-адресов для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="11d3a-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="11d3a-122">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="11d3a-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="11d3a-123">Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.</span><span class="sxs-lookup"><span data-stu-id="11d3a-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="11d3a-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="11d3a-124">Click **OK**.</span></span>

5. <span data-ttu-id="11d3a-125">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="11d3a-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="11d3a-126">Ограничить разрешения пользователей tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="11d3a-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="11d3a-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="11d3a-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="11d3a-128">В Visual Studio или Xamarin Studio Запустите клиентский проект hello на устройстве или эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="11d3a-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="11d3a-129">Убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello.</span><span class="sxs-lookup"><span data-stu-id="11d3a-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="11d3a-130">Сбой Hello — журнал toohello консоль hello отладчика.</span><span class="sxs-lookup"><span data-stu-id="11d3a-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="11d3a-131">Поэтому в Visual Studio, вы увидите сбоя hello в окне вывода hello.</span><span class="sxs-lookup"><span data-stu-id="11d3a-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="11d3a-132">&nbsp;&nbsp;Эта ошибка несанкционированного происходит потому, что приложение hello пытается tooaccess серверной части мобильное приложение от имени пользователя без проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="11d3a-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="11d3a-133">Hello *TodoItem* таблица теперь требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="11d3a-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="11d3a-134">Далее можно обновить ресурсов toorequest hello клиентского приложения из внутреннего сервера мобильного приложения hello с прошедшим проверку пользователем.</span><span class="sxs-lookup"><span data-stu-id="11d3a-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="11d3a-135">Добавить приложение toohello проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="11d3a-135">Add authentication toohello app</span></span>
<span data-ttu-id="11d3a-136">В этом разделе предстоит изменить приложение hello toodisplay экран входа перед отображением данных.</span><span class="sxs-lookup"><span data-stu-id="11d3a-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="11d3a-137">При запуске приложение hello, он будет не подключиться tooyour службы приложений и не отображаются все данные.</span><span class="sxs-lookup"><span data-stu-id="11d3a-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="11d3a-138">После hello первый раз hello, выполняемых этим пользователем жестов обновления hello, отобразится экран входа hello. После успешного входа hello список элементов todo отображается.</span><span class="sxs-lookup"><span data-stu-id="11d3a-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="11d3a-139">В клиентском проекте hello, откройте файл hello **QSTodoService.cs** и добавьте следующее hello с помощью инструкции и `MobileServiceUser` с toohello доступа QSTodoService класса:</span><span class="sxs-lookup"><span data-stu-id="11d3a-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="11d3a-140">Добавьте новый метод с именем **Authenticate** слишком**QSTodoService** с hello следующие определения:</span><span class="sxs-lookup"><span data-stu-id="11d3a-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] <span data-ttu-id="11d3a-141">При использовании поставщика удостоверений, отличные от Facebook, измените значение hello, переданный слишком**LoginAsync** выше tooone hello следующее: _MicrosoftAccount_, _Twitter_, _Google_, или _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="11d3a-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="11d3a-142">Откройте файл **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="11d3a-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="11d3a-143">Изменить определение метода hello **ViewDidLoad** Удаление вызова hello слишком**RefreshAsync()** скоро истекает hello:</span><span class="sxs-lookup"><span data-stu-id="11d3a-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="11d3a-144">Измените метод hello **RefreshAsync** tooauthenticate Если hello **пользователя** свойство имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="11d3a-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="11d3a-145">Добавьте после кода hello верхней части определения метода hello hello:</span><span class="sxs-lookup"><span data-stu-id="11d3a-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="11d3a-146">Откройте **AppDelegate.cs**, добавьте следующий метод hello:</span><span class="sxs-lookup"><span data-stu-id="11d3a-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="11d3a-147">Откройте **Info.plist** файл, перейдите в слишком**типы URL-адрес** в hello **Дополнительно** раздела.</span><span class="sxs-lookup"><span data-stu-id="11d3a-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="11d3a-148">Теперь настройка hello **идентификатор** и hello **URL-схем** тип URL-адрес и нажмите кнопку **добавить тип URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="11d3a-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="11d3a-149">**URL-схем** должно быть таким же hello как {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="11d3a-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="11d3a-150">В Visual Studio или Xamarin Studio подключен tooyour узла сборки Xamarin на компьютере Mac Запустите клиентский проект hello, предназначенных для устройства или эмулятора.</span><span class="sxs-lookup"><span data-stu-id="11d3a-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="11d3a-151">Убедитесь, что данные не отображаются, приложение hello.</span><span class="sxs-lookup"><span data-stu-id="11d3a-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="11d3a-152">Для выполнения обновления жестов hello перетащите вниз hello список элементов, которые вызовут tooappear экрана входа hello.</span><span class="sxs-lookup"><span data-stu-id="11d3a-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="11d3a-153">После успешного ввода действительных учетных данных, приложение hello будет отображать список элементов todo hello и внесении toohello обновляет данные.</span><span class="sxs-lookup"><span data-stu-id="11d3a-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Создание приложения Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md