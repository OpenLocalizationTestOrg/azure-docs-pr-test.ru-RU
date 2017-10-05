---
title: "Начало работы с проверкой подлинности для мобильных приложений Xamarin для Android"
description: "Узнайте, как использовать мобильные приложения для проверки подлинности пользователей приложения Xamarin для Android с помощью разных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Майкрософт."
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
ms.openlocfilehash: 8f9a1109018c708d52cdcb7b8bce43861cecd31c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinandroid-app"></a><span data-ttu-id="b6d67-103">Добавление проверки подлинности в приложение Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="b6d67-103">Add authentication to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="b6d67-104">В этом разделе показано, как аутентифицировать пользователей мобильного приложения из клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="b6d67-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="b6d67-105">В этом учебнике вы добавите аутентификацию в проект быстрого запуска, используя поставщик удостоверений, поддерживаемый мобильными приложениями Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d67-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="b6d67-106">После успешной аутентификации и авторизации в мобильном приложении отображается значение идентификатора пользователя.</span><span class="sxs-lookup"><span data-stu-id="b6d67-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span></span>

<span data-ttu-id="b6d67-107">Этот учебник создан на основе краткого руководства по мобильным приложениям.</span><span class="sxs-lookup"><span data-stu-id="b6d67-107">This tutorial is based on the Mobile App quickstart.</span></span> <span data-ttu-id="b6d67-108">Необходимо также сначала пройти руководство [Создание приложения Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="b6d67-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="b6d67-109">Если вы не используете скачанный проект быстрого запуска сервера, в проект необходимо добавить пакет расширений для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="b6d67-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="b6d67-110">в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b6d67-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="b6d67-111"><a name="register"></a>Регистрация приложения для проверки подлинности и настройка служб приложений</span><span class="sxs-lookup"><span data-stu-id="b6d67-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="b6d67-112"><a name="redirecturl"></a>Добавление приложения в список разрешенных URL-адресов внешнего перенаправления</span><span class="sxs-lookup"><span data-stu-id="b6d67-112"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="b6d67-113">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="b6d67-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="b6d67-114">Это позволяет системе аутентификации выполнять перенаправление обратно в приложение после завершения процесса аутентификации.</span><span class="sxs-lookup"><span data-stu-id="b6d67-114">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="b6d67-115">В этом руководстве мы повсеместно используем схему URL-адресов _appname_.</span><span class="sxs-lookup"><span data-stu-id="b6d67-115">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="b6d67-116">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="b6d67-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="b6d67-117">Она должна быть уникальной для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b6d67-117">It should be unique to your mobile application.</span></span> <span data-ttu-id="b6d67-118">Вот как можно включить перенаправление на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="b6d67-118">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="b6d67-119">На портале Azure выберите свою службу приложений.</span><span class="sxs-lookup"><span data-stu-id="b6d67-119">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="b6d67-120">Выберите пункт меню **Аутентификация или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="b6d67-120">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="b6d67-121">В поле **Разрешенные URL-адреса внешнего перенаправления** введите `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="b6d67-121">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="b6d67-122">**url_scheme_of_your_app** в этой строке — это схема URL-адресов для вашего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b6d67-122">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="b6d67-123">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="b6d67-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="b6d67-124">Необходимо записать выбранную строку, так как потребуется в нескольких местах настроить код мобильного приложения с использованием схемы URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="b6d67-124">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="b6d67-125">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b6d67-125">Click **OK**.</span></span>

5. <span data-ttu-id="b6d67-126">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b6d67-126">Click **Save**.</span></span>

## <span data-ttu-id="b6d67-127"><a name="permissions"></a>Предоставление разрешений только пользователям, прошедшим проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="b6d67-127"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="b6d67-128">В Visual Studio или Xamarin Studio запустите клиентский проект на устройстве или в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="b6d67-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="b6d67-129">Убедитесь, что после запуска приложения возникает необработанное исключение с кодом состояния 401 (неавторизованный).</span><span class="sxs-lookup"><span data-stu-id="b6d67-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="b6d67-130">Это вызвано тем, что приложение пытается получить доступ к серверной части мобильного приложения от имени неаутентифицированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b6d67-130">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="b6d67-131">Теперь для таблицы *TodoItem* требуется аутентификация.</span><span class="sxs-lookup"><span data-stu-id="b6d67-131">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="b6d67-132">Далее вы обновите клиентское приложение для запроса ресурсов из серверной части мобильного приложения прошедшим аутентификацию пользователем.</span><span class="sxs-lookup"><span data-stu-id="b6d67-132">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="b6d67-133"><a name="add-authentication"></a>Добавление проверки подлинности в приложение</span><span class="sxs-lookup"><span data-stu-id="b6d67-133"><a name="add-authentication"></a>Add authentication to the app</span></span>
<span data-ttu-id="b6d67-134">Для отображения данных в обновленном приложении пользователи должны будут коснуться кнопки **Вход** и пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b6d67-134">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="b6d67-135">Добавьте в класс **TodoActivity** следующий код:</span><span class="sxs-lookup"><span data-stu-id="b6d67-135">Add the following code to the **TodoActivity** class:</span></span>
   
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
                //Hide the button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load the data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="b6d67-136">При этом создается новый метод для проверки подлинности пользователя и метод обработчика для новой кнопки **Вход** .</span><span class="sxs-lookup"><span data-stu-id="b6d67-136">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="b6d67-137">Пользователь в примере кода выше аутентифицируется с помощью имени для входа Facebook.</span><span class="sxs-lookup"><span data-stu-id="b6d67-137">The user in the example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="b6d67-138">Диалоговое окно используется для отображения идентификатора пользователя после аутентификации.</span><span class="sxs-lookup"><span data-stu-id="b6d67-138">A dialog is used to display the user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b6d67-139">Если вы используете поставщик удостоверений, отличный от Facebook, замените значение, передаваемое в метод **LoginAsync** выше, одним из следующих: *MicrosoftAccount*, *Twitter*, *Google* или *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="b6d67-139">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="b6d67-140">В методе **OnCreate** удалите или закомментируйте следующую строку кода:</span><span class="sxs-lookup"><span data-stu-id="b6d67-140">In the **OnCreate** method, delete or comment-out the following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="b6d67-141">В файле Activity_To_Do.axml вставьте определение кнопки *LoginUser* перед уже имеющейся кнопкой *AddItem*:</span><span class="sxs-lookup"><span data-stu-id="b6d67-141">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="b6d67-142">Добавьте следующий элемент в файл ресурсов Strings.xml:</span><span class="sxs-lookup"><span data-stu-id="b6d67-142">Add the following element to the Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="b6d67-143">Откройте файл AndroidManifest.xml и добавьте следующий код в XML-элемент `<application>`:</span><span class="sxs-lookup"><span data-stu-id="b6d67-143">Open the AndroidManifest.xml file, add the following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="b6d67-144">В Visual Studio или Xamarin Studio запустите клиентский проект на устройстве или в эмуляторе либо выполните вход с помощью выбранного поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b6d67-144">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="b6d67-145">После успешного выполнения входа в приложении отобразится ваш идентификатор для входа и список элементов задач, и вы сможете внести изменения в данные.</span><span class="sxs-lookup"><span data-stu-id="b6d67-145">When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
<span data-ttu-id="b6d67-146">[Создание приложения Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b6d67-146">[Create a Xamarin.Android app]: app-service-mobile-xamarin-android-get-started.md</span></span>