---
title: "aaaGet запущена с использованием проверки подлинности для мобильных приложений в Xamarin Android"
description: "Узнайте, как toouse мобильные приложения tooauthenticate пользователей приложения Xamarin Android с помощью различных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Майкрософт."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a><span data-ttu-id="f145b-103">Добавить приложение Xamarin.Android tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f145b-103">Add authentication tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="f145b-104">В этом разделе показано, как пользователи tooauthenticate мобильного приложения из клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="f145b-104">This topic shows you how tooauthenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="f145b-105">В этом учебнике добавьте проект краткое руководство toohello проверки подлинности, с помощью поставщика удостоверений, который поддерживается модулем мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="f145b-105">In this tutorial, you add authentication toohello quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="f145b-106">После успешного проверку подлинности и авторизации в мобильное приложение hello, отображается значение идентификатора пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="f145b-106">After being successfully authenticated and authorized in hello Mobile App, hello user ID value is displayed.</span></span>

<span data-ttu-id="f145b-107">Этот учебник основывается на примеры использования мобильного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f145b-107">This tutorial is based on hello Mobile App quickstart.</span></span> <span data-ttu-id="f145b-108">Также в первую очередь необходимо пройти учебник hello [Создание приложения Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="f145b-108">You must also first complete hello tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="f145b-109">Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакета расширения проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="f145b-109">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="f145b-110">Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f145b-110">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="f145b-111"><a name="register"></a>Регистрация приложения для проверки подлинности и настройка служб приложений</span><span class="sxs-lookup"><span data-stu-id="f145b-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="f145b-112"><a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений</span><span class="sxs-lookup"><span data-stu-id="f145b-112"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="f145b-113">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="f145b-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="f145b-114">Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="f145b-114">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="f145b-115">В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении.</span><span class="sxs-lookup"><span data-stu-id="f145b-115">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="f145b-116">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="f145b-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="f145b-117">Он должен быть уникальным tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="f145b-117">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="f145b-118">tooenable hello перенаправления на стороне сервера hello:</span><span class="sxs-lookup"><span data-stu-id="f145b-118">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="f145b-119">В hello [Azure портал] выберите приложение службы.</span><span class="sxs-lookup"><span data-stu-id="f145b-119">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="f145b-120">Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="f145b-120">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="f145b-121">В hello **допускается внешний URL-адреса перенаправления**, введите `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="f145b-121">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="f145b-122">Hello **url_scheme_of_your_app** в данной строке — hello схема URL-адресов для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="f145b-122">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="f145b-123">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="f145b-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="f145b-124">Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.</span><span class="sxs-lookup"><span data-stu-id="f145b-124">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="f145b-125">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f145b-125">Click **OK**.</span></span>

5. <span data-ttu-id="f145b-126">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f145b-126">Click **Save**.</span></span>

## <span data-ttu-id="f145b-127"><a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="f145b-127"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="f145b-128">В Visual Studio или Xamarin Studio Запустите клиентский проект hello на устройстве или эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="f145b-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="f145b-129">Убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello.</span><span class="sxs-lookup"><span data-stu-id="f145b-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="f145b-130">Это происходит потому, что приложение hello пытается tooaccess серверной части мобильное приложение как локальный пользователь.</span><span class="sxs-lookup"><span data-stu-id="f145b-130">This happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="f145b-131">Hello *TodoItem* таблица теперь требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f145b-131">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="f145b-132">Далее можно обновить ресурсов toorequest hello клиентского приложения из внутреннего сервера мобильного приложения hello с прошедшим проверку пользователем.</span><span class="sxs-lookup"><span data-stu-id="f145b-132">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="f145b-133"><a name="add-authentication"></a>Добавить приложение toohello проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f145b-133"><a name="add-authentication"></a>Add authentication toohello app</span></span>
<span data-ttu-id="f145b-134">приложение Hello — hello tootap пользователей обновленные toorequire **входа** кнопку и пройти проверку подлинности перед отображением данных.</span><span class="sxs-lookup"><span data-stu-id="f145b-134">hello app is updated toorequire users tootap hello **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="f145b-135">Добавьте следующий код toohello hello **TodoActivity** класса:</span><span class="sxs-lookup"><span data-stu-id="f145b-135">Add hello following code toohello **TodoActivity** class:</span></span>
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="f145b-136">Это создает новый tooauthenticate метод пользователя и метод обработчика нового **входа** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f145b-136">This creates a new method tooauthenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="f145b-137">Hello в приведенном выше примере кода hello происходит проверка подлинности с помощью имени входа для Facebook.</span><span class="sxs-lookup"><span data-stu-id="f145b-137">hello user in hello example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="f145b-138">Диалоговое окно является используется toodisplay hello ИД пользователя после проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f145b-138">A dialog is used toodisplay hello user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f145b-139">При использовании поставщика удостоверений, отличные от Facebook, измените значение hello передано слишком**LoginAsync** выше tooone hello следующее: *MicrosoftAccount*, *Twitter*, *Google*, или *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="f145b-139">If you are using an identity provider other than Facebook, change hello value passed too**LoginAsync** above tooone of hello following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="f145b-140">В hello **OnCreate** метода, delete или hello вне комментария, следующей строкой кода:</span><span class="sxs-lookup"><span data-stu-id="f145b-140">In hello **OnCreate** method, delete or comment-out hello following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="f145b-141">В файле Activity_To_Do.axml hello, добавьте следующее hello *LoginUser* кнопку определение перед hello существующих *AddItem* кнопки:</span><span class="sxs-lookup"><span data-stu-id="f145b-141">In hello Activity_To_Do.axml file, add hello following *LoginUser* button definition before hello existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="f145b-142">Добавьте следующие файл ресурсов Strings.xml toohello элемент hello:</span><span class="sxs-lookup"><span data-stu-id="f145b-142">Add hello following element toohello Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="f145b-143">Откройте файл AndroidManifest.xml hello, добавьте следующий код внутри hello `<application>` XML-элемента:</span><span class="sxs-lookup"><span data-stu-id="f145b-143">Open hello AndroidManifest.xml file, add hello following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="f145b-144">В Visual Studio и Xamarin Studio Запустите клиентский проект hello на устройстве или эмуляторе и войдите с помощью поставщика удостоверений для выбранного.</span><span class="sxs-lookup"><span data-stu-id="f145b-144">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="f145b-145">После успешного входа в систему, приложение hello будет отображен идентификатор входа в систему, а hello список элементов todo и делает данные toohello обновлений.</span><span class="sxs-lookup"><span data-stu-id="f145b-145">When you are successfully logged-in, hello app will display your login ID and hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Создание приложения Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md