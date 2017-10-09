### <span data-ttu-id="6908c-101"><a name="server-auth"></a>Практическое руководство. Проверка подлинности с помощью поставщика (серверный поток)</span><span class="sxs-lookup"><span data-stu-id="6908c-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="6908c-102">Мобильные приложения toohave управления процессом проверки подлинности hello в приложении, необходимо зарегистрировать приложение с помощью поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6908c-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="6908c-103">Затем в службе приложений Azure требуется идентификатор приложения hello tooconfigure и секрет, полученные от поставщика.</span><span class="sxs-lookup"><span data-stu-id="6908c-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="6908c-104">Дополнительные сведения см. в разделе учебника hello [приложение tooyour authentication добавить](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="6908c-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="6908c-105">После регистрации поставщика удостоверений, вызовите hello `.login()` метод с именем hello поставщика.</span><span class="sxs-lookup"><span data-stu-id="6908c-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="6908c-106">Например toologin с Facebook использовать hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="6908c-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="6908c-107">Hello допустимые значения для hello поставщика: «aad», «facebook», «google», «microsoftaccount» и «twitter».</span><span class="sxs-lookup"><span data-stu-id="6908c-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="6908c-108">Сейчас проверка подлинности Google не выполняется через серверный поток.</span><span class="sxs-lookup"><span data-stu-id="6908c-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="6908c-109">tooauthenticate с Google, необходимо использовать [потока клиента метод](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="6908c-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="6908c-110">В этом случае служба приложений Azure управляет поток проверки подлинности hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="6908c-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="6908c-111">Он отображает страницу входа hello hello выбранного поставщика и создает маркер проверки подлинности службы приложений после успешного входа в систему с поставщиком удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="6908c-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="6908c-112">функция входа Hello, после завершения возвращает объект JSON, который предоставляет идентификатор пользователя hello и службы приложений токена проверки подлинности в полях userId и authenticationToken hello, соответственно.</span><span class="sxs-lookup"><span data-stu-id="6908c-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="6908c-113">Этот маркер можно поместить в кэш и повторно использовать, пока не истечет срок его действия.</span><span class="sxs-lookup"><span data-stu-id="6908c-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="6908c-114"><a name="client-auth"></a>Практическое руководство. Проверка подлинности с помощью поставщика (клиентский поток)</span><span class="sxs-lookup"><span data-stu-id="6908c-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="6908c-115">Приложение может также независимо друг от друга обратитесь к поставщику удостоверений hello, а затем введите hello вернул токен tooyour службы приложений для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6908c-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="6908c-116">Этот порядок клиента позволяет tooprovide единого входа в систему для пользователей или tooretrieve дополнительные пользовательские данные от поставщика удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="6908c-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="6908c-117">Простой пример проверки подлинности на основе учетной записи социальной сети</span><span class="sxs-lookup"><span data-stu-id="6908c-117">Social Authentication basic example</span></span>

<span data-ttu-id="6908c-118">В этом примере используется пакет SDK для клиента Facebook для проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="6908c-118">This example uses Facebook client SDK for authentication:</span></span>

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
<span data-ttu-id="6908c-119">Предоставленный поставщиком соответствующих hello SDK хранится в переменной маркера hello, предполагается этот токен hello.</span><span class="sxs-lookup"><span data-stu-id="6908c-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="6908c-120">Пример учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="6908c-120">Microsoft Account example</span></span>

<span data-ttu-id="6908c-121">в этом примере используется следующая Hello hello пакета SDK Live, который поддерживает один вход для приложений магазина Windows с помощью учетной записи Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="6908c-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

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

<span data-ttu-id="6908c-122">В этом примере получает от Live Connect, являющийся предоставленного tooyour службы приложений путем вызова функции hello имени входа.</span><span class="sxs-lookup"><span data-stu-id="6908c-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="6908c-123"><a name="auth-getinfo"></a>Как: получение сведений о hello с проверкой подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="6908c-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="6908c-124">сведения о проверке подлинности Hello можно получить из hello `/.auth/me` конечную точку HTTP с помощью вызова с любой библиотекой AJAX.</span><span class="sxs-lookup"><span data-stu-id="6908c-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="6908c-125">Обеспечить настройку hello `X-ZUMO-AUTH` токена проверки подлинности tooyour заголовок.</span><span class="sxs-lookup"><span data-stu-id="6908c-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="6908c-126">Hello токена проверки подлинности хранится в `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="6908c-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="6908c-127">Например toouse API fetch hello:</span><span class="sxs-lookup"><span data-stu-id="6908c-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="6908c-128">Компонент выборки предоставляется в виде [пакета NPM](https://www.npmjs.com/package/whatwg-fetch) или для скачивания браузером из [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="6908c-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="6908c-129">Можно также использовать jQuery или другой данных hello toofetch AJAX API.</span><span class="sxs-lookup"><span data-stu-id="6908c-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="6908c-130">Данные получаются в виде объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="6908c-130">Data is received as a JSON object.</span></span>
