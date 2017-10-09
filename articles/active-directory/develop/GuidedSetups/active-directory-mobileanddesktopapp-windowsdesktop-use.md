---
title: "aaaAzure AD v2 Windows Desktop Приступая к работе - Используйте | Документы Microsoft"
description: "Здесь описывается, как классические приложения для Windows .NET (XAML) могут вызвать API, требующий маркеры доступа от конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="861d4-103">Использование библиотеки проверки подлинности Microsoft (MSAL) hello tooget маркер для hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="861d4-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="861d4-104">В этом разделе показано, как tooget MSAL toouse маркер hello Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="861d4-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="861d4-105">В `MainWindow.xaml.cs`, добавьте ссылку hello для класса toohello MSAL библиотеки:</span><span class="sxs-lookup"><span data-stu-id="861d4-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="861d4-106">Замените код класса <code>MainWindow</code>:</span><span class="sxs-lookup"><span data-stu-id="861d4-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="861d4-107">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="861d4-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="861d4-108">Интерактивное получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="861d4-108">Getting a user token interactive</span></span>
<span data-ttu-id="861d4-109">Вызов hello `AcquireTokenAsync` toosign пользователя в hello результаты метода в окне запроса.</span><span class="sxs-lookup"><span data-stu-id="861d4-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="861d4-110">Приложения обычно требуют toosign пользователя в интерактивном режиме hello первый раз, они должны tooaccess защищенному ресурсу или при tooacquire операции в фоновом режиме, может произойти сбой маркера (например hello пользователя срок действия пароля истек).</span><span class="sxs-lookup"><span data-stu-id="861d4-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="861d4-111">Автоматическое получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="861d4-111">Getting a user token silently</span></span>
<span data-ttu-id="861d4-112">`AcquireTokenSilentAsync` обрабатывает получение и обновление маркера без участия пользователя.</span><span class="sxs-lookup"><span data-stu-id="861d4-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="861d4-113">После `AcquireTokenAsync` выполняется для hello первый раз `AcquireTokenSilentAsync` tooobtain маркерами hello используется обычный метод tooaccess защищенные ресурсы для последующих вызовов — как вызовы toorequest или обновить маркеры выполняются без вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="861d4-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="861d4-114">Со временем `AcquireTokenSilentAsync` завершится ошибкой, — например hello пользователя выполнен выход или изменил свой пароль на другом устройстве.</span><span class="sxs-lookup"><span data-stu-id="861d4-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="861d4-115">Когда MSAL обнаруживает, что hello проблему можно устранить путем интерактивного вмешательства, в `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="861d4-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="861d4-116">Приложение может обработать это исключение двумя способами:</span><span class="sxs-lookup"><span data-stu-id="861d4-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="861d4-117">Звонок от `AcquireTokenAsync` немедленно, в результате запроса пользователя hello в toosign.</span><span class="sxs-lookup"><span data-stu-id="861d4-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="861d4-118">Этот шаблон обычно используется в веб-приложений там, где отсутствует не автономного содержимого в приложение hello для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="861d4-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="861d4-119">Hello образец созданные эта интерактивная программа установки использует этот шаблон: его можно просматривать в действие hello первый раз, когда выполняется образец hello: так как пользователь не использовали приложения hello `PublicClientApp.Users.FirstOrDefault()` будет содержать значение null и `MsalUiRequiredException` будет создано исключение.</span><span class="sxs-lookup"><span data-stu-id="861d4-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="861d4-120">Здравствуйте код в образце hello, а затем обрабатывает hello исключения путем вызова `AcquireTokenAsync` приведет к подтверждения пользователя hello в toosign.</span><span class="sxs-lookup"><span data-stu-id="861d4-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="861d4-121">Приложения также может сделать пользователь toohello визуальный индикатор, интерактивный вход не требуется, поэтому hello пользователь может выбрать toosign нужное время hello в или приложение hello перезапустит `AcquireTokenSilentAsync` позднее.</span><span class="sxs-lookup"><span data-stu-id="861d4-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="861d4-122">Это обычно используется при hello пользователя можно использовать другие функциональные возможности приложения hello без была прервана - например, отсутствуют автономного содержимого в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="861d4-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="861d4-123">В этом случае hello пользователь мог решать при хочет toosign в tooaccess hello защищенных ресурсов, toorefresh hello устаревшую информацию или приложения может решить tooretry `AcquireTokenSilentAsync` при восстановлении сети после станет временно недоступной.</span><span class="sxs-lookup"><span data-stu-id="861d4-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="861d4-124">Вызвать API Microsoft Graph hello hello токен, который был получен с помощью</span><span class="sxs-lookup"><span data-stu-id="861d4-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="861d4-125">Добавьте новый метод hello ниже tooyour `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="861d4-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="861d4-126">Hello в противном случае используется toomake `GET` запрос к API Graph, используя заголовок авторизации:</span><span class="sxs-lookup"><span data-stu-id="861d4-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="861d4-127">Дополнительные сведения о вызове REST через защищенный API</span><span class="sxs-lookup"><span data-stu-id="861d4-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="861d4-128">В этом образце приложения hello `GetHttpContentWithToken` в противном случае используется toomake HTTP `GET` запроса к защищенному ресурсу, требующий toohello содержимого токена и затем вернуться hello вызывающий объект.</span><span class="sxs-lookup"><span data-stu-id="861d4-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="861d4-129">Этот метод добавляет маркер hello получена в hello *заголовок авторизации HTTP*.</span><span class="sxs-lookup"><span data-stu-id="861d4-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="861d4-130">Для этого образца hello ресурсов — hello Microsoft Graph API *мне* конечной точки — которого отображаются сведения о профиле пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="861d4-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="861d4-131">Добавьте метод toosign выход пользователя hello</span><span class="sxs-lookup"><span data-stu-id="861d4-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="861d4-132">Добавьте следующий метод tooyour hello `MainWindow.xaml.cs` toosign выход пользователя hello:</span><span class="sxs-lookup"><span data-stu-id="861d4-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

```csharp
/// <summary>
/// Sign out hello current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="861d4-133">Дополнительные сведения о выходе</span><span class="sxs-lookup"><span data-stu-id="861d4-133">More info on Sign-Out</span></span>

<span data-ttu-id="861d4-134">`SignOutButton_Click`Здравствуйте, удаляет пользователя из кэша MSAL пользователя — эффективно сведения MSAL tooforget hello текущего пользователя, tooacquire будущих запроса маркера будет успешным, только если он станет toobe интерактивный.</span><span class="sxs-lookup"><span data-stu-id="861d4-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="861d4-135">Несмотря на то, что приложение hello в этом образце поддерживает один пользователь, MSAL поддерживает сценарии, где может быть несколько учетных записей, выполнившего вход в hello одновременно — пример — приложение электронной почты которых у пользователя есть несколько учетных записей.</span><span class="sxs-lookup"><span data-stu-id="861d4-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="861d4-136">Отображение основных сведений о маркере</span><span class="sxs-lookup"><span data-stu-id="861d4-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="861d4-137">Добавьте следующий метод tootooyour hello `MainWindow.xaml.cs` toodisplay основные сведения о токене hello:</span><span class="sxs-lookup"><span data-stu-id="861d4-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in hello token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="861d4-138">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="861d4-138">More Information</span></span>

<span data-ttu-id="861d4-139">Токены получена через *OpenID Connect* также содержать небольшое подмножество пользователей toohello нужные сведения.</span><span class="sxs-lookup"><span data-stu-id="861d4-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="861d4-140">`DisplayBasicTokenInfo`содержит базовые сведения, содержащиеся в маркере hello: например, пользователь hello отображаемое имя и идентификатор, а также hello срока действия маркера даты и hello строка, представляющая маркер доступа hello сам.</span><span class="sxs-lookup"><span data-stu-id="861d4-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="861d4-141">Эти сведения отображаются для вас toosee.</span><span class="sxs-lookup"><span data-stu-id="861d4-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="861d4-142">Можно нажать hello *вызова API Graph Microsoft* кнопку несколько раз и посмотрите, что hello тот же токен был использован повторно для последующих запросов.</span><span class="sxs-lookup"><span data-stu-id="861d4-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="861d4-143">Также вы увидите Дата окончания срока действия hello расширяемого при MSAL решает, что это время toorenew hello маркер.</span><span class="sxs-lookup"><span data-stu-id="861d4-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

