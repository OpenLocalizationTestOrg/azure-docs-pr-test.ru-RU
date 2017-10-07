---
title: "aaaGet запущена с использованием проверки подлинности для мобильных приложений в Xamarin Forms приложения | Документы Microsoft"
description: "Узнайте, каким образом пользователи tooauthenticate toouse мобильные приложения Xamarin Forms приложения с помощью различных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="44148-103">Добавить приложение Xamarin Forms tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="44148-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="44148-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="44148-104">Overview</span></span>
<span data-ttu-id="44148-105">В этом разделе показано, как пользователи tooauthenticate приложение службы мобильных приложений из клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="44148-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="44148-106">В этом учебнике hello Xamarin Forms быстрый запуск проекта с помощью поставщика удостоверений, который поддерживается службой приложений добавить проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="44148-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="44148-107">После успешного проверку подлинности или авторизации мобильного приложения, отображается значение идентификатора пользователя hello и будет может tooaccess только табличные данные.</span><span class="sxs-lookup"><span data-stu-id="44148-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44148-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44148-108">Prerequisites</span></span>
<span data-ttu-id="44148-109">Для получения оптимальных результатов hello к этому учебнику, рекомендуется сначала выполнить hello [Создание приложения Xamarin Forms] [ 1] учебника.</span><span class="sxs-lookup"><span data-stu-id="44148-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="44148-110">Завершив работу, вы получите проект Xamarin Forms — кроссплатформенное приложение TodoList.</span><span class="sxs-lookup"><span data-stu-id="44148-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="44148-111">Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакета расширения проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="44148-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="44148-112">Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure][2].</span><span class="sxs-lookup"><span data-stu-id="44148-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="44148-113">Регистрация приложения для проверки подлинности и настройка служб приложений</span><span class="sxs-lookup"><span data-stu-id="44148-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="44148-114"><a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений</span><span class="sxs-lookup"><span data-stu-id="44148-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="44148-115">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="44148-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="44148-116">Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="44148-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="44148-117">В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении.</span><span class="sxs-lookup"><span data-stu-id="44148-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="44148-118">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="44148-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="44148-119">Он должен быть уникальным tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="44148-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="44148-120">tooenable hello перенаправления на стороне сервера hello:</span><span class="sxs-lookup"><span data-stu-id="44148-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="44148-121">В hello [Azure портал] выберите приложение службы.</span><span class="sxs-lookup"><span data-stu-id="44148-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="44148-122">Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="44148-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="44148-123">В hello **допускается внешний URL-адреса перенаправления**, введите `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="44148-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="44148-124">Hello **url_scheme_of_your_app** в данной строке — hello схема URL-адресов для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="44148-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="44148-125">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="44148-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="44148-126">Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.</span><span class="sxs-lookup"><span data-stu-id="44148-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="44148-127">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="44148-127">Click **OK**.</span></span>

5. <span data-ttu-id="44148-128">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="44148-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="44148-129">Ограничить разрешения пользователей tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="44148-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="44148-130">Добавление проверки подлинности toohello переносимой библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="44148-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="44148-131">Мобильные приложения использует hello [LoginAsync] [ 3] метод расширения в hello [MobileServiceClient] [ 4] toosign в пользователя службы приложения Проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="44148-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="44148-132">Этот пример использует поток управляемого сервером проверки подлинности, который отображает интерфейс поставщика hello вход в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="44148-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="44148-133">Дополнительные сведения см. в статье [Управляемая сервером проверка подлинности][5].</span><span class="sxs-lookup"><span data-stu-id="44148-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="44148-134">Чтобы пользователям было удобнее работать с вашим рабочим приложением, попробуйте использовать [управляемую клиентом аутентификацию][6].</span><span class="sxs-lookup"><span data-stu-id="44148-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="44148-135">Определение tooauthenticate в проекте Xamarin Forms **IAuthenticate** интерфейса в hello переносимой библиотеки классов для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="44148-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="44148-136">Затем добавьте **входа** кнопку toohello интерфейса, определенные на hello переносимой библиотеки классов, которую можно щелкнуть toostart проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="44148-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="44148-137">Данные загружаются из внутреннего сервера мобильного приложения hello после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="44148-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="44148-138">Реализуйте hello **IAuthenticate** интерфейс для каждой платформы, поддерживаемые в приложении.</span><span class="sxs-lookup"><span data-stu-id="44148-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="44148-139">В Visual Studio и Xamarin Studio, откройте App.cs из проекта hello с **переносимой** в hello имя, являющееся проекта переносимой библиотеки классов, затем добавьте следующие hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="44148-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="44148-140">В App.cs, добавьте следующее hello `IAuthenticate` определением непосредственно перед hello интерфейса `App` определения класса.</span><span class="sxs-lookup"><span data-stu-id="44148-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="44148-141">интерфейс hello tooinitialize с помощью реализации платформой добавлять hello следующие статические члены toohello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="44148-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="44148-142">Откройте TodoList.xaml из проекта переносимой библиотеки классов hello, добавьте следующее hello **кнопку** элемент в hello *buttonsPanel* макет элемента, после существующего кнопки hello:</span><span class="sxs-lookup"><span data-stu-id="44148-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="44148-143">Эта кнопка запускает управляемую сервером проверку подлинности с помощью серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="44148-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="44148-144">Откройте TodoList.xaml.cs из проекта переносимой библиотеки классов hello, а затем добавьте следующие поля toohello hello `TodoList` класса:</span><span class="sxs-lookup"><span data-stu-id="44148-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="44148-145">Замените hello **OnAppearing** метод с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="44148-145">Replace hello **OnAppearing** method with hello following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="44148-146">Этот код гарантирует, что только обновления данных из службы hello после вы прошли проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="44148-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="44148-147">Добавьте следующий обработчик для hello hello **щелчок** toohello событий **TodoList** класса:</span><span class="sxs-lookup"><span data-stu-id="44148-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="44148-148">Сохраните изменения и перестройте проект переносимой библиотеки классов hello проверка без ошибок.</span><span class="sxs-lookup"><span data-stu-id="44148-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="44148-149">Добавить приложение Android toohello проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="44148-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="44148-150">В этом разделе показано, как tooimplement hello **IAuthenticate** интерфейс в проекте Android приложения hello.</span><span class="sxs-lookup"><span data-stu-id="44148-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="44148-151">Пропустите этот раздел, если вы не пользуетесь устройствами Android.</span><span class="sxs-lookup"><span data-stu-id="44148-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="44148-152">В Visual Studio и Xamarin Studio, щелкните правой кнопкой мыши hello **droid** проекта, затем **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="44148-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="44148-153">Нажмите клавишу F5 toostart hello проекта в отладчике hello, а затем убедитесь, что необработанное исключение с кодом состояния 401 (не санкционировано) возникает после запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="44148-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="44148-154">код 401 Hello создается, так как доступ к серверной части hello только для пользователей ограниченными tooauthorized.</span><span class="sxs-lookup"><span data-stu-id="44148-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="44148-155">Откройте MainActivity.cs в проект Android hello и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="44148-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="44148-156">Обновление hello **MainActivity** hello класс tooimplement **IAuthenticate** интерфейс следующим образом:</span><span class="sxs-lookup"><span data-stu-id="44148-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="44148-157">Обновление hello **MainActivity** класс, добавив **MobileServiceUser** поля и **Authenticate** метод, который требуется для hello **IAuthenticate**  интерфейс следующим образом:</span><span class="sxs-lookup"><span data-stu-id="44148-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="44148-158">Если используется поставщик удостоверений, отличающийся от Facebook, выберите другое значение [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="44148-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="44148-159">Добавьте следующий код внутри hello <application> узел AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="44148-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. <span data-ttu-id="44148-160">Добавьте следующий код toohello hello **OnCreate** метод hello **MainActivity** класса перед вызовом hello слишком`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="44148-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="44148-161">Этот код гарантирует, что средство проверки подлинности hello инициализируется перед загрузкой приложения hello.</span><span class="sxs-lookup"><span data-stu-id="44148-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="44148-162">Перестройте приложение hello, запустите его, а затем войдите с помощью поставщика проверки подлинности hello выбранным и убедитесь, что заданы может tooaccess данные в виде прошедшего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="44148-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="44148-163">Добавление приложения iOS toohello проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="44148-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="44148-164">В этом разделе показано, как tooimplement hello **IAuthenticate** интерфейса в проект приложения hello iOS.</span><span class="sxs-lookup"><span data-stu-id="44148-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="44148-165">Пропустите этот раздел, если вы не пользуетесь устройствами iOS.</span><span class="sxs-lookup"><span data-stu-id="44148-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="44148-166">В Visual Studio и Xamarin Studio, щелкните правой кнопкой мыши hello **iOS** проекта, затем **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="44148-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="44148-167">Нажмите клавишу F5 toostart hello проекта в отладчике hello, а затем убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello.</span><span class="sxs-lookup"><span data-stu-id="44148-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="44148-168">ответ 401 Hello создается, так как доступ к серверной части hello только для пользователей ограниченными tooauthorized.</span><span class="sxs-lookup"><span data-stu-id="44148-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="44148-169">Откройте AppDelegate.cs в проекте iOS hello и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="44148-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="44148-170">Обновление hello **AppDelegate** hello класс tooimplement **IAuthenticate** интерфейс следующим образом:</span><span class="sxs-lookup"><span data-stu-id="44148-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="44148-171">Обновление hello **AppDelegate** класс, добавив **MobileServiceUser** поля и **Authenticate** метод, который требуется для hello **IAuthenticate**  интерфейс следующим образом:</span><span class="sxs-lookup"><span data-stu-id="44148-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="44148-172">Если используется поставщик удостоверений, отличающийся от Facebook, выберите другое значение [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="44148-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="44148-173">Обновить класс AppDelegate hello, добавив перегруженный метод OpenUrl (параметры NSDictionary UIApplication NSUrl URL-адрес приложения)</span><span class="sxs-lookup"><span data-stu-id="44148-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="44148-174">Добавьте следующие строки кода toohello hello **FinishedLaunching** слишком вызов метода перед hello`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="44148-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="44148-175">Этот код гарантирует, что средство проверки подлинности hello инициализируется перед загрузкой приложение hello.</span><span class="sxs-lookup"><span data-stu-id="44148-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="44148-176">Добавить **{url_scheme_of_your_app}** tooURL схемы в файле Info.plist.</span><span class="sxs-lookup"><span data-stu-id="44148-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="44148-177">Перестройте приложение hello, запустите его, а затем войдите с помощью поставщика проверки подлинности hello выбранным и убедитесь, что заданы может tooaccess данные в виде прошедшего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="44148-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="44148-178">Добавление проверки подлинности tooWindows 10 (включая телефон) проекты приложений</span><span class="sxs-lookup"><span data-stu-id="44148-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="44148-179">В этом разделе показано, как tooimplement hello **IAuthenticate** интерфейса в проектах приложений Windows 10 hello.</span><span class="sxs-lookup"><span data-stu-id="44148-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="44148-180">используется проекты универсальной платформы Windows (UWP), но с использованием hello Hello **UWP** проекта (с помощью указанных изменений).</span><span class="sxs-lookup"><span data-stu-id="44148-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="44148-181">Пропустите этот раздел, если вы не пользуетесь устройствами Windows.</span><span class="sxs-lookup"><span data-stu-id="44148-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="44148-182">«В Visual Studio щелкните правой кнопкой мыши либо hello **UWP** проекта, затем **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="44148-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="44148-183">Нажмите клавишу F5 toostart hello проекта в отладчике hello, а затем убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello.</span><span class="sxs-lookup"><span data-stu-id="44148-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="44148-184">ответ 401 Hello происходит потому, что доступ к серверной части hello — только для пользователей ограниченными tooauthorized.</span><span class="sxs-lookup"><span data-stu-id="44148-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="44148-185">Откройте файл MainPage.xaml.cs для проекта приложения Windows hello и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="44148-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="44148-186">Замените `<your_Portable_Class_Library_namespace>` с пространством имен hello вашей переносимой библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="44148-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="44148-187">Обновление hello **MainPage** hello класс tooimplement **IAuthenticate** интерфейс следующим образом:</span><span class="sxs-lookup"><span data-stu-id="44148-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="44148-188">Обновление hello **MainPage** класс, добавив **MobileServiceUser** поля и **Authenticate** метод, который требуется для hello **IAuthenticate** интерфейс следующим образом:</span><span class="sxs-lookup"><span data-stu-id="44148-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="44148-189">Если используется поставщик удостоверений, отличающийся от Facebook, выберите другое значение [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="44148-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="44148-190">Добавьте следующие строки кода в конструкторе hello для hello hello **MainPage** класса перед вызовом hello слишком`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="44148-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="44148-191">Замените `<your_Portable_Class_Library_namespace>` с пространством имен hello вашей переносимой библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="44148-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="44148-192">Если вы используете **UWP**, добавьте следующее hello **OnActivated** toohello переопределение метода **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="44148-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="44148-193">Переопределение метода hello уже существует, добавьте условного кода hello из предшествующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="44148-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="44148-194">Этот код не требуется для универсальных проектов Windows.</span><span class="sxs-lookup"><span data-stu-id="44148-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="44148-195">Добавьте **{схема_URL-адреса_вашего_приложения}** в файл Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="44148-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="44148-196">Перестройте приложение hello, запустите его, а затем войдите с помощью поставщика проверки подлинности hello выбранным и убедитесь, что заданы может tooaccess данные в виде прошедшего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="44148-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44148-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44148-197">Next steps</span></span>
<span data-ttu-id="44148-198">Завершения этого учебника обычной проверки подлинности, рассмотрите возможность продолжить на tooone из hello следующие учебники:</span><span class="sxs-lookup"><span data-stu-id="44148-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="44148-199">Добавить приложение tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="44148-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="44148-200">Узнайте, как push-уведомления tooadd поддерживают tooyour приложения и настройки вашего мобильного приложения серверной toouse концентраторов уведомлений Azure toosend push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="44148-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="44148-201">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="44148-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="44148-202">Узнайте, как автономные tooadd поддерживают приложения с помощью мобильного приложения серверной части.</span><span class="sxs-lookup"><span data-stu-id="44148-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="44148-203">Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением — Просмотр, добавление или изменение данных — даже в том случае, если нет сетевого соединения.</span><span class="sxs-lookup"><span data-stu-id="44148-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
