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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Использование библиотеки проверки подлинности Microsoft (MSAL) hello tooget маркер для hello Microsoft Graph API

В этом разделе показано, как tooget MSAL toouse маркер hello Microsoft Graph API.

1.  В `MainWindow.xaml.cs`, добавьте ссылку hello для класса toohello MSAL библиотеки:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Замените код класса <code>MainWindow</code>:
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
### <a name="more-information"></a>Дополнительные сведения
#### <a name="getting-a-user-token-interactive"></a>Интерактивное получение маркера пользователя
Вызов hello `AcquireTokenAsync` toosign пользователя в hello результаты метода в окне запроса. Приложения обычно требуют toosign пользователя в интерактивном режиме hello первый раз, они должны tooaccess защищенному ресурсу или при tooacquire операции в фоновом режиме, может произойти сбой маркера (например hello пользователя срок действия пароля истек).

#### <a name="getting-a-user-token-silently"></a>Автоматическое получение маркера пользователя
`AcquireTokenSilentAsync` обрабатывает получение и обновление маркера без участия пользователя. После `AcquireTokenAsync` выполняется для hello первый раз `AcquireTokenSilentAsync` tooobtain маркерами hello используется обычный метод tooaccess защищенные ресурсы для последующих вызовов — как вызовы toorequest или обновить маркеры выполняются без вмешательства пользователя.
Со временем `AcquireTokenSilentAsync` завершится ошибкой, — например hello пользователя выполнен выход или изменил свой пароль на другом устройстве. Когда MSAL обнаруживает, что hello проблему можно устранить путем интерактивного вмешательства, в `MsalUiRequiredException`. Приложение может обработать это исключение двумя способами:

1.  Звонок от `AcquireTokenAsync` немедленно, в результате запроса пользователя hello в toosign. Этот шаблон обычно используется в веб-приложений там, где отсутствует не автономного содержимого в приложение hello для пользователя hello. Hello образец созданные эта интерактивная программа установки использует этот шаблон: его можно просматривать в действие hello первый раз, когда выполняется образец hello: так как пользователь не использовали приложения hello `PublicClientApp.Users.FirstOrDefault()` будет содержать значение null и `MsalUiRequiredException` будет создано исключение. Здравствуйте код в образце hello, а затем обрабатывает hello исключения путем вызова `AcquireTokenAsync` приведет к подтверждения пользователя hello в toosign.

2.  Приложения также может сделать пользователь toohello визуальный индикатор, интерактивный вход не требуется, поэтому hello пользователь может выбрать toosign нужное время hello в или приложение hello перезапустит `AcquireTokenSilentAsync` позднее. Это обычно используется при hello пользователя можно использовать другие функциональные возможности приложения hello без была прервана - например, отсутствуют автономного содержимого в приложение hello. В этом случае hello пользователь мог решать при хочет toosign в tooaccess hello защищенных ресурсов, toorefresh hello устаревшую информацию или приложения может решить tooretry `AcquireTokenSilentAsync` при восстановлении сети после станет временно недоступной.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Вызвать API Microsoft Graph hello hello токен, который был получен с помощью

1. Добавьте новый метод hello ниже tooyour `MainWindow.xaml.cs`. Hello в противном случае используется toomake `GET` запрос к API Graph, используя заголовок авторизации:

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Дополнительные сведения о вызове REST через защищенный API

В этом образце приложения hello `GetHttpContentWithToken` в противном случае используется toomake HTTP `GET` запроса к защищенному ресурсу, требующий toohello содержимого токена и затем вернуться hello вызывающий объект. Этот метод добавляет маркер hello получена в hello *заголовок авторизации HTTP*. Для этого образца hello ресурсов — hello Microsoft Graph API *мне* конечной точки — которого отображаются сведения о профиле пользователя hello.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Добавьте метод toosign выход пользователя hello

1. Добавьте следующий метод tooyour hello `MainWindow.xaml.cs` toosign выход пользователя hello:

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
### <a name="more-info-on-sign-out"></a>Дополнительные сведения о выходе

`SignOutButton_Click`Здравствуйте, удаляет пользователя из кэша MSAL пользователя — эффективно сведения MSAL tooforget hello текущего пользователя, tooacquire будущих запроса маркера будет успешным, только если он станет toobe интерактивный.
Несмотря на то, что приложение hello в этом образце поддерживает один пользователь, MSAL поддерживает сценарии, где может быть несколько учетных записей, выполнившего вход в hello одновременно — пример — приложение электронной почты которых у пользователя есть несколько учетных записей.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>Отображение основных сведений о маркере

1. Добавьте следующий метод tootooyour hello `MainWindow.xaml.cs` toodisplay основные сведения о токене hello:

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
### <a name="more-information"></a>Дополнительные сведения

Токены получена через *OpenID Connect* также содержать небольшое подмножество пользователей toohello нужные сведения. `DisplayBasicTokenInfo`содержит базовые сведения, содержащиеся в маркере hello: например, пользователь hello отображаемое имя и идентификатор, а также hello срока действия маркера даты и hello строка, представляющая маркер доступа hello сам. Эти сведения отображаются для вас toosee. Можно нажать hello *вызова API Graph Microsoft* кнопку несколько раз и посмотрите, что hello тот же токен был использован повторно для последующих запросов. Также вы увидите Дата окончания срока действия hello расширяемого при MSAL решает, что это время toorenew hello маркер.
<!--end-collapse-->

