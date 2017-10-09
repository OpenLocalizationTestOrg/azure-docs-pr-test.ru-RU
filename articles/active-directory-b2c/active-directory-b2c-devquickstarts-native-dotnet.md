---
title: "aaaAzure Active Directory B2C | Документы Microsoft"
description: "Как toobuild настольных приложений Windows, содержит вход, регистрации и профиль управления с помощью Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>Azure AD B2C: создание классического приложения Windows
С помощью B2C Azure Active Directory (Azure AD), можно добавить классического приложения функции управления tooyour мощные самообслуживания идентификаторов в несколько простых шагов. В этой статье будет показано, как toocreate приложение .NET Windows Presentation Foundation (WPF) «список дел», которое включает в себя пользователя регистрации, вход и управление профилями пользователей. приложение Hello будет включать поддержку для регистрации и входа с помощью электронной почты или имя пользователя. Приложение будет поддерживать регистрацию и вход в систему по имени пользователя или адресу электронной почты, а также по учетной записи в социальной сети, такой как Facebook или Google.

## <a name="get-an-azure-ad-b2c-directory"></a>Создание каталога Azure AD B2C
Перед использованием Azure AD B2C необходимо создать каталог или клиент.  Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д. Прежде чем продолжать работу с руководством, [создайте каталог B2C](active-directory-b2c-get-started.md), если вы его еще не создали.

## <a name="create-an-application"></a>Создание приложения
Далее необходимо toocreate приложения в каталоге B2C. Это дает сведения о Azure AD, что его нуждается toosecurely взаимодействовать с приложением. toocreate приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md).  Не забудьте сделать следующее.

* Включить **собственного клиента** в приложение hello.
* Копировать hello **URI перенаправления** `urn:ietf:wg:oauth:2.0:oob`. Это URL-адрес по умолчанию hello для этого примера кода.
* Копировать hello **идентификатор приложения** , назначенный tooyour приложения. Оно понадобится вам позднее.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Создание политик
В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md). Этот пример кода включает три способа идентификации: регистрацию, вход в систему и изменение профиля. Необходимо toocreate политики для каждого типа, как описано в [статье политики](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). При создании hello три политики, нужно убедиться, что:

* Выберите либо **регистрации идентификатора пользователя** или **электронной почты регистрации** в колонке Поставщики удостоверений hello.
* В политике регистрации укажите **отображаемое имя** и другие атрибуты регистрации.
* В каждой политике в качестве утверждения приложения выберите утверждения **Отображаемое имя** и **Идентификатор объекта**. Можно также выбрать другие утверждения.
* Копировать hello **имя** каждой политики, после его создания. Он должен иметь префикс hello `b2c_1_`.  Эти имена политик понадобятся вам через некоторое время.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

После успешного создания hello три политики, вы будете готовы toobuild приложения.

## <a name="download-hello-code"></a>Загрузка кода hello
Здравствуйте, код для этого учебника [сохраняется на сайте GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet). Образец hello toobuild как можно перейти, вы можете [загрузить каркас проект как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip). Также можно клонировать основу hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

также является приложение Hello завершения [доступны как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) или на hello `complete` ветви hello одного репозитория.

После загрузки кода образца hello запущен tooget файл .sln Visual Studio откройте hello. Hello `TaskClient` проект является hello классическое приложение WPF, hello пользователь взаимодействует с. Для целей этого учебника hello он вызывает задачу серверной части веб-API, размещенных в Azure, который хранит список дел каждого пользователя.  Нет необходимости toobuild hello веб-API, у нас уже есть она запущена.

toolearn как веб-API безопасно проверка подлинности запросов с помощью Azure AD B2C извлечь [веб-API Приступая к работе статьи](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="execute-policies"></a>Выполнение политик
Приложение взаимодействует с Azure AD B2C, отправляя сообщения проверки подлинности, укажите политику hello требуемый tooexecute hello HTTP-запроса. Для классических приложений .NET, можно использовать hello Предварительный просмотр сообщения проверки подлинности OAuth 2.0 toosend библиотеки проверки подлинности Microsoft (MSAL), выполнение политик и получения маркеров, которые вызывают веб-API-интерфейсы.

### <a name="install-msal"></a>Установка MSAL
Добавить MSAL toohello `TaskClient` проекта с помощью консоли диспетчера пакетов Visual Studio hello.

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>Ввод данных B2C
Привет открыть файл `Globals.cs` и замените все значения свойств hello свои собственные. Этот класс используется во всех `TaskClient` tooreference часто используемых значений.

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a>Создать hello PublicClientApplication
основной класс Hello MSAL: `PublicClientApplication`. Этот класс представляет приложение в системе hello Azure AD B2C. Когда hello Инициализирует приложение, создайте экземпляр класса `PublicClientApplication` в `MainWindow.xaml.cs`. Это можно использовать в окне приветствия.

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a>Запуск потока регистрации
Когда пользователь соглашается toosigns вверх, нужно tooinitiate регистрации потока, в котором применяется созданной вами политикой регистрации hello. Для этого требуется только вызов метода `pca.AcquireTokenAsync(...)`с помощью MSAL. Здравствуйте, параметры, можно передать слишком`AcquireTokenAsync(...)` определить, какой токен появляется, hello политику, используемую в запрос проверки подлинности hello и многое другое.

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }

            MessageBox.Show(message);
        }

        return;
    }
}
```

### <a name="initiate-a-sign-in-flow"></a>Инициация потока входа
Можно выполнить вход в потоке hello так же, как запустить регистрации потока. При входе в систему пользователя сделать hello же вызвать tooMSAL, с использованием политики входа:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a>Инициирование потока изменения профиля
Еще раз, можно выполнить политику изменения профиля в hello аналогичным способом:

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

Во всех этих случаях MSAL либо возвращает маркер в `AuthenticationResult` , либо выдает исключение. Каждый раз, получить маркер из MSAL, можно использовать hello `AuthenticationResult.User` объекта tooupdate hello пользовательских данных в приложение hello, например hello пользовательского интерфейса. ADAL также кэшей hello маркер для использования в других частях приложения hello.

### <a name="check-for-tokens-on-app-start"></a>Проверка наличия маркеров при запуске приложения
Также можно отслеживать состояние входа пользователя hello tookeep MSAL.  В этом приложении мы хотим tooremain пользователя hello, даже после их закрыть приложение hello и повторно открыть его в системе.  Назад внутри hello `OnInitialized` переопределить, используйте его MSAL `AcquireTokenSilent` toocheck метод для кэшированных маркеров:

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
    return;
}
```

## <a name="call-hello-task-api"></a>Вызвать API задачи hello
Использовали MSAL tooexecute политик и получения токенов.  При необходимости toouse один эти токены toocall hello задач API вы снова сможете использовать его MSAL `AcquireTokenSilent` toocheck метод для кэшированных маркеров:

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
        }
        else
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }
            MessageBox.Show(message);
        }

        return;
    }
    ...
```

При слишком hello вызовов`AcquireTokenSilentAsync(...)` завершается успешно и будет найден маркер в кэш hello, можно добавить hello маркера toohello `Authorization` заголовок hello HTTP-запроса. Список дел заголовок tooauthenticate hello запроса tooread hello в учетной записи пользователя будет использоваться веб-задачи Hello API:

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>Пользователь hello Sign out
Наконец, можно использовать MSAL tooend сеанс пользователя с приложение hello при выборе пользователем hello **Выход**.  При использовании MSAL, эти действия выполняются, сняв все маркеры hello из кэша маркеров hello.

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a>Запуск образца приложения hello
Наконец построение и запуск образца hello.  После регистрации приложения hello с помощью электронной почты адрес или имя пользователя. Выйдите из системы и войти снова как hello же пользователя. Измените профиль пользователя. Выйдите и зарегистрируйтесь от имени другого пользователя.

## <a name="add-social-idps"></a>Добавление поставщиков удостоверений социальных сетей
В настоящее время приложение hello поддерживает только регистрации пользователя и войти, использовать **локальные учетные записи**. Учетные записи хранятся в каталоге B2C, где применяется имя пользователя и пароль. С помощью Azure AD B2C можно добавить поддержку для других поставщиков удостоверений (IDP), не изменяя код.

tooadd социальных IDPs tooyour приложение, начните с выполнения следующего hello подробные инструкции в следующих статьях. Для каждого поставщика Удостоверений требуется toosupport, нужно tooregister приложения в этой системе и получение идентификатора клиента.

* [Настройка Facebook как поставщика удостоверений](active-directory-b2c-setup-fb-app.md)
* [Настройка Google как поставщика удостоверений](active-directory-b2c-setup-goog-app.md)
* [Настройка Amazon как поставщика удостоверений](active-directory-b2c-setup-amzn-app.md)
* [Настройка LinkedIn как поставщика удостоверений](active-directory-b2c-setup-li-app.md)

После добавления каталог tooyour B2C Поставщики удостоверений hello, необходимо каждый из трех политик tooinclude hello новый IDPs как описано в hello tooedit [статье политики](active-directory-b2c-reference-policies.md). После сохранения политик, снова запустите приложение hello. Вы увидите hello, добавления новых IDPs входа и регистрации в качестве параметров каждой своими впечатлениями удостоверения.

Можно поэкспериментировать с политиками и наблюдать за hello влияние на примере приложения. например: добавлять или удалять поставщиков удостоверений, управлять утверждениями приложений или изменять атрибуты регистрации, а также наблюдать эффект в примере приложения. Эксперименты помогают увидеть связь между политиками, запросами на проверку подлинности и библиотекой MSAL.

Справочник по hello выполнить образец [предоставляется как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip). Кроме того, его можно клонировать из GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
