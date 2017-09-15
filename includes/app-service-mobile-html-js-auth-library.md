### <span data-ttu-id="3e17a-101"><a name="server-auth"></a>Практическое руководство. Проверка подлинности с помощью поставщика (серверный поток)</span><span class="sxs-lookup"><span data-stu-id="3e17a-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="3e17a-102">Чтобы мобильные приложения могли выполнять процесс проверки подлинности в вашем приложении, необходимо зарегистрировать приложение у поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="3e17a-102">To have Mobile Apps manage the authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="3e17a-103">Затем в службе приложений Azure необходимо настроить код приложения и секретный код, предоставленный поставщиком.</span><span class="sxs-lookup"><span data-stu-id="3e17a-103">Then in your Azure App Service, you need to configure the application ID and secret provided by your provider.</span></span>
<span data-ttu-id="3e17a-104">Дополнительные сведения см. в учебнике [Добавление проверки подлинности в приложение](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="3e17a-104">For more information, see the tutorial [Add authentication to your app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="3e17a-105">После регистрации у поставщика удостоверений вызовите метод `.login()` с указанием имени вашего поставщика.</span><span class="sxs-lookup"><span data-stu-id="3e17a-105">Once you have registered your identity provider, call the `.login()` method with the name of your provider.</span></span> <span data-ttu-id="3e17a-106">Например, для входа в систему через Facebook используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="3e17a-106">For example, to login with Facebook use the following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="3e17a-107">Допустимые для поставщика значения: aad, facebook, google, microsoftaccount и twitter.</span><span class="sxs-lookup"><span data-stu-id="3e17a-107">The valid values for the provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="3e17a-108">Сейчас проверка подлинности Google не выполняется через серверный поток.</span><span class="sxs-lookup"><span data-stu-id="3e17a-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="3e17a-109">Для проверки подлинности с помощью Google необходимо использовать [метод клиентского потока](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="3e17a-109">To authenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="3e17a-110">В этом случае служба приложений Azure управляет потоком проверки подлинности согласно протоколу OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3e17a-110">In this case, Azure App Service manages the OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="3e17a-111">Она отображает страницу входа выбранного поставщика и создает маркер проверки подлинности службы приложений после успешного входа с помощью поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="3e17a-111">It displays the login page of the selected provider and generates an App Service authentication token after successful login with the identity provider.</span></span> <span data-ttu-id="3e17a-112">Функция login после завершения работы возвращает объект JSON, который содержит и идентификатор пользователя, и маркер проверки подлинности службы приложений в полях userId и authenticationToken соответственно.</span><span class="sxs-lookup"><span data-stu-id="3e17a-112">The login function, when complete, returns a JSON object that exposes both the user ID and App Service authentication token in the userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="3e17a-113">Этот маркер можно поместить в кэш и повторно использовать, пока не истечет срок его действия.</span><span class="sxs-lookup"><span data-stu-id="3e17a-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="3e17a-114"><a name="client-auth"></a>Практическое руководство. Проверка подлинности с помощью поставщика (клиентский поток)</span><span class="sxs-lookup"><span data-stu-id="3e17a-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="3e17a-115">Приложение может также независимо связаться с поставщиком удостоверений и сообщить возвращаемый маркер вашей службе приложений для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3e17a-115">Your app can also independently contact the identity provider and then provide the returned token to your App Service for authentication.</span></span> <span data-ttu-id="3e17a-116">Этот клиентский поток позволяет пользователям выполнять единый вход или получать дополнительные данные о пользователе от поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="3e17a-116">This client flow enables you to provide a single sign-in experience for users or to retrieve additional user data from the identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="3e17a-117">Простой пример проверки подлинности на основе учетной записи социальной сети</span><span class="sxs-lookup"><span data-stu-id="3e17a-117">Social Authentication basic example</span></span>

<span data-ttu-id="3e17a-118">В этом примере используется пакет SDK для клиента Facebook для проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="3e17a-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="3e17a-119">В этом примере предполагается, что маркер, предоставленный соответствующим поставщиком SDK, сохраняется в переменной token.</span><span class="sxs-lookup"><span data-stu-id="3e17a-119">This example assumes that the token provided by the respective provider SDK is stored in the token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="3e17a-120">Пример учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="3e17a-120">Microsoft Account example</span></span>

<span data-ttu-id="3e17a-121">В следующем примере используется пакет SDK Live, поддерживающий единый вход в приложения Магазина Windows с использованием учетной записи Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="3e17a-121">The following example uses the Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="3e17a-122">Этот пример получает маркер из Live Connect, который предоставляется вашей службе приложений путем вызова функции login.</span><span class="sxs-lookup"><span data-stu-id="3e17a-122">This example gets a token from Live Connect, which is supplied to your App Service by calling the login function.</span></span>

###<span data-ttu-id="3e17a-123"><a name="auth-getinfo"></a>Практическое руководство. Получение сведений о пользователе, прошедшем аутентификацию</span><span class="sxs-lookup"><span data-stu-id="3e17a-123"><a name="auth-getinfo"></a>How to: Obtain information about the authenticated user</span></span>

<span data-ttu-id="3e17a-124">Сведения о проверке подлинности можно получить из конечной точки `/.auth/me`, выполнив вызов HTTP с помощью любой библиотеки AJAX.</span><span class="sxs-lookup"><span data-stu-id="3e17a-124">The authentication information can be retrieved from the `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="3e17a-125">Обязательно настройте заголовок `X-ZUMO-AUTH` для маркера аутентификации.</span><span class="sxs-lookup"><span data-stu-id="3e17a-125">Ensure you set the `X-ZUMO-AUTH` header to your authentication token.</span></span>  <span data-ttu-id="3e17a-126">Маркер аутентификации хранится в `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="3e17a-126">The authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="3e17a-127">Например, чтобы использовать API выборки:</span><span class="sxs-lookup"><span data-stu-id="3e17a-127">For example, to use the fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // The user object contains the claims for the authenticated user
    });
```

<span data-ttu-id="3e17a-128">Компонент выборки предоставляется в виде [пакета NPM](https://www.npmjs.com/package/whatwg-fetch) или для скачивания браузером из [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="3e17a-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="3e17a-129">Для получения информации можно также использовать jQuery или другой API AJAX.</span><span class="sxs-lookup"><span data-stu-id="3e17a-129">You could also use jQuery or another AJAX API to fetch the information.</span></span>  <span data-ttu-id="3e17a-130">Данные получаются в виде объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="3e17a-130">Data is received as a JSON object.</span></span>
