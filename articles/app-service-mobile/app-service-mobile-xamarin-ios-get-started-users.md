---
title: "Начало работы с проверкой подлинности для мобильных приложений в Xamarin iOS"
description: "Использование мобильных приложений для проверки подлинности пользователей приложения Xamarin iOS с помощью разных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Майкрософт."
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
ms.openlocfilehash: 454b2df5a9bf8cfba93befea54370957ab044d95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="51f29-103">Добавление проверки подлинности в приложение Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="51f29-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="51f29-104">В этом разделе показано, как выполнить проверку подлинности пользователей мобильного приложения службы приложений из клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="51f29-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="51f29-105">В этом учебнике приведены инструкции, позволяющие добавить проверку подлинности в ознакомительный проект Xamarin.Forms, используя поставщик удостоверений, поддерживаемый службой приложений.</span><span class="sxs-lookup"><span data-stu-id="51f29-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="51f29-106">После успешной проверки подлинности и авторизации мобильным приложением отображается значение идентификатора пользователя, и вы сможете получить доступ к закрытым табличным данным.</span><span class="sxs-lookup"><span data-stu-id="51f29-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="51f29-107">Сначала необходимо выполнить инструкции из руководства [Создание приложения Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="51f29-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="51f29-108">Если вы не используете скачанный проект быстрого запуска сервера, в проект необходимо добавить пакет расширений для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="51f29-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="51f29-109">в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="51f29-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="51f29-110">Регистрация приложения для проверки подлинности и настройка служб приложений</span><span class="sxs-lookup"><span data-stu-id="51f29-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-to-the-allowed-external-redirect-urls"></a><span data-ttu-id="51f29-111">Добавление приложения в список разрешенных URL-адресов внешнего перенаправления</span><span class="sxs-lookup"><span data-stu-id="51f29-111">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="51f29-112">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="51f29-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="51f29-113">Это позволяет системе аутентификации выполнять перенаправление обратно в приложение после завершения процесса аутентификации.</span><span class="sxs-lookup"><span data-stu-id="51f29-113">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="51f29-114">В этом руководстве мы повсеместно используем схему URL-адресов _appname_.</span><span class="sxs-lookup"><span data-stu-id="51f29-114">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="51f29-115">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="51f29-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="51f29-116">Она должна быть уникальной для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="51f29-116">It should be unique to your mobile application.</span></span> <span data-ttu-id="51f29-117">Вот как можно включить перенаправление на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="51f29-117">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="51f29-118">На портале Azure выберите свою службу приложений.</span><span class="sxs-lookup"><span data-stu-id="51f29-118">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="51f29-119">Выберите пункт меню **Аутентификация или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="51f29-119">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="51f29-120">В поле **Разрешенные URL-адреса внешнего перенаправления** введите `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="51f29-120">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="51f29-121">**url_scheme_of_your_app** в этой строке — это схема URL-адресов для вашего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="51f29-121">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="51f29-122">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="51f29-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="51f29-123">Необходимо записать выбранную строку, так как потребуется в нескольких местах настроить код мобильного приложения с использованием схемы URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="51f29-123">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="51f29-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="51f29-124">Click **OK**.</span></span>

5. <span data-ttu-id="51f29-125">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="51f29-125">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="51f29-126">Ограничение разрешений для пользователей, прошедших проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="51f29-126">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="51f29-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="51f29-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="51f29-128">В Visual Studio или Xamarin Studio запустите клиентский проект на устройстве или в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="51f29-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="51f29-129">Убедитесь, что после запуска приложения возникает необработанное исключение с кодом состояния 401 (неавторизованный).</span><span class="sxs-lookup"><span data-stu-id="51f29-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="51f29-130">Ошибка записывается в консоль отладчика.</span><span class="sxs-lookup"><span data-stu-id="51f29-130">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="51f29-131">Поэтому в Visual Studio вы увидите ошибку в окне вывода.</span><span class="sxs-lookup"><span data-stu-id="51f29-131">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="51f29-132">&nbsp;&nbsp;Эта нештатная ошибка происходит потому, что приложение пытается получить доступ к серверной части мобильного приложения от имени не прошедшего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="51f29-132">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="51f29-133">Теперь для таблицы *TodoItem* требуется аутентификация.</span><span class="sxs-lookup"><span data-stu-id="51f29-133">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="51f29-134">Далее вы обновите клиентское приложение для запроса ресурсов из серверной части мобильного приложения прошедшим аутентификацию пользователем.</span><span class="sxs-lookup"><span data-stu-id="51f29-134">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="51f29-135">Добавление проверки подлинности в приложение</span><span class="sxs-lookup"><span data-stu-id="51f29-135">Add authentication to the app</span></span>
<span data-ttu-id="51f29-136">В этом разделе предстоит изменить приложение для отображения экрана входа до отображения данных.</span><span class="sxs-lookup"><span data-stu-id="51f29-136">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="51f29-137">При запуске приложение не подключится к службе приложений и не отобразит никаких данных.</span><span class="sxs-lookup"><span data-stu-id="51f29-137">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="51f29-138">После первого обновления пользователем появится экран входа; список задач появится после успешного входа.</span><span class="sxs-lookup"><span data-stu-id="51f29-138">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="51f29-139">В проекте клиента откройте файл **QSTodoService.cs** и добавьте следующий оператор using и объект `MobileServiceUser` с методом доступа к классу QSTodoService:</span><span class="sxs-lookup"><span data-stu-id="51f29-139">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="51f29-140">Добавьте новый метод **Authenticate** в **QSTodoService** со следующим определением:</span><span class="sxs-lookup"><span data-stu-id="51f29-140">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="51f29-141">Если у вас поставщик удостоверений, отличный от Facebook, замените значение, передаваемое в метод **LoginAsync** выше, одним из следующих: _MicrosoftAccount_, _Twitter_, _Google_ или _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="51f29-141">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="51f29-142">Откройте файл **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="51f29-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="51f29-143">Измените определение метода **ViewDidLoad**, удалив вызов **RefreshAsync()** в конце:</span><span class="sxs-lookup"><span data-stu-id="51f29-143">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="51f29-144">Измените метод **RefreshAsync** для проверки подлинности, если для свойства **User** задано значение null.</span><span class="sxs-lookup"><span data-stu-id="51f29-144">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="51f29-145">Добавьте следующий код в верхнюю часть определения метода:</span><span class="sxs-lookup"><span data-stu-id="51f29-145">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="51f29-146">Откройте файл **AppDelegate.cs** и добавьте следующий метод:</span><span class="sxs-lookup"><span data-stu-id="51f29-146">Open **AppDelegate.cs**, add the following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="51f29-147">Откройте файл **Info.plist** и перейдите к записи **Типы URL-адресов** в разделе **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="51f29-147">Open **Info.plist** file, navigate to **URL Types** in the **Advanced** section.</span></span> <span data-ttu-id="51f29-148">Теперь настройте **идентификатор** и **схемы URL-адресов** для типов URL-адресов, а затем щелкните **Добавить тип URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="51f29-148">Now configure the **Identifier** and the **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="51f29-149">**Схемы URL-адресов** должны совпадать с {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="51f29-149">**URL Schemes** should be the same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="51f29-150">В среде Visual Studio или Xamarin Studio, подключенной к узлу сборки Xamarin на компьютере Macintosh, запустите клиентский проект, указав устройство или эмулятор.</span><span class="sxs-lookup"><span data-stu-id="51f29-150">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="51f29-151">Убедитесь, что в приложении не отображаются данные.</span><span class="sxs-lookup"><span data-stu-id="51f29-151">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="51f29-152">Обновите, потянув вниз список элементов, чтобы появился экран входа.</span><span class="sxs-lookup"><span data-stu-id="51f29-152">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="51f29-153">После успешного ввода допустимых учетных данных в приложении отобразится список элементов задач и вы сможете внести изменения в данные.</span><span class="sxs-lookup"><span data-stu-id="51f29-153">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
<span data-ttu-id="51f29-154">[Создание приложения Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="51f29-154">[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>