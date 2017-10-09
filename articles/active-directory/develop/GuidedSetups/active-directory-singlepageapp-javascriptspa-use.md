---
title: "aaaAzure AD v2 JS SPA Интерактивная установка - использование | Документы Microsoft"
description: "В этой статье описано, как приложения JavaScript SPA могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="dc3c2-103">Используйте user в toosign hello hello библиотеки проверки подлинности Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="dc3c2-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="dc3c2-104">Создайте файл с именем `app.js`.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-104">Create a file named `app.js`.</span></span> <span data-ttu-id="dc3c2-105">Если вы используете Visual Studio, выберите hello проектов (корневой папки проекта,), щелкните правой кнопкой мыши и выберите: `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="dc3c2-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="dc3c2-106">Добавьте следующий код tooyour hello `app.js` файла:</span><span class="sxs-lookup"><span data-stu-id="dc3c2-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="dc3c2-107">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="dc3c2-107">More Information</span></span>

<span data-ttu-id="dc3c2-108">После нажатия пользователем hello *«Вызвать Microsoft Graph API»* кнопки для hello первый раз `callGraphApi` вызовы метода `loginRedirect` toosign в hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="dc3c2-109">Этот метод приводит к перенаправление hello пользователя toohello *конечной точки Microsoft Azure Active Directory v2* tooprompt и проверки учетных данных пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="dc3c2-110">В результате успешного входа в систему пользователь hello является перенаправленный задней toohello исходного *index.html* страницы и токен поступает, обрабатываемых `msal.js` и кэшируется hello сведения, содержащиеся в маркере hello.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="dc3c2-111">Этот маркер называется hello *маркер идентификатора* и содержит основные сведения о пользователе hello, такие как отображаемое имя пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="dc3c2-112">Если планируется toouse данные предоставляемых по этот маркер для каких целей, необходимо убедиться, что этот маркер проверяется с вашей tooguarantee сервера базы данных, hello маркера toomake выдан tooa допустимого пользователя для приложения.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="dc3c2-113">Hello SPA, созданные в этом руководстве не смог использовать напрямую из маркер идентификатора hello-вместо этого он вызывает `acquireTokenSilent` и/или `acquireTokenRedirect` tooacquire *маркер доступа* используется tooquery hello Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="dc3c2-114">Если вам требуется образец, проверяет маркер идентификатора hello, взгляните на [это](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 пример") примера приложения в GitHub — образец hello использует веб-API ASP.NET для проверки токенов.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="dc3c2-115">Интерактивное получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="dc3c2-115">Getting a user token interactively</span></span>

<span data-ttu-id="dc3c2-116">После hello, начальный вход, вы не хотите hello Попросите пользователей tooreauthenticate каждый раз, они должны toorequest маркера tooaccess ресурсов — так *acquireTokenSilent* следует использовать большую часть токены tooacquire времени hello.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="dc3c2-117">Однако существуют ситуации, необходимо tooforce пользователи взаимодействуют с конечной точкой v2 Azure Active Directory — некоторые примеры:</span><span class="sxs-lookup"><span data-stu-id="dc3c2-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="dc3c2-118">Пользователям может потребоваться tooreenter свои учетные данные, так как истек срок действия пароля hello</span><span class="sxs-lookup"><span data-stu-id="dc3c2-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="dc3c2-119">Приложение запрашивает ресурс tooa доступ, hello tooconsent потребностей пользователя для</span><span class="sxs-lookup"><span data-stu-id="dc3c2-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="dc3c2-120">Требуется двухфакторная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="dc3c2-120">Two factor authentication is required</span></span>

<span data-ttu-id="dc3c2-121">Вызов hello *acquireTokenRedirect(scope)* привести перенаправления конечной точки toohello v2 Azure Active Directory пользователей (или *acquireTokenPopup(scope)* результат всплывающем окне) которых пользователям необходимо toointeract с подтверждая либо свои учетные данные, предоставляя toohello согласия hello необходимых ресурсов или завершение hello двухфакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="dc3c2-122">Автоматическое получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="dc3c2-122">Getting a user token silently</span></span>
<span data-ttu-id="dc3c2-123">Hello ` acquireTokenSilent` метод обрабатывает приобретения токена и обновления без вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="dc3c2-124">После `loginRedirect` (или `loginPopup`) выполняется для hello первый раз `acquireTokenSilent` tooobtain маркерами hello распространенным методом tooaccess защищенные ресурсы для последующих вызовов — как вызовы toorequest или обновить маркеры выполняются без вмешательства пользователя.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="dc3c2-125">`acquireTokenSilent`может ли сбой в некоторых случаях — например, пароль пользователя hello истек.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="dc3c2-126">Приложение может обработать это исключение двумя способами:</span><span class="sxs-lookup"><span data-stu-id="dc3c2-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="dc3c2-127">Вызвать слишком`acquireTokenRedirect` немедленно, что приводит запроса hello toosign пользователя в.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="dc3c2-128">Этот шаблон обычно используется в веб-приложений которого нет содержимого, не прошедшие проверку подлинности в пользователя доступны toohello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="dc3c2-129">Образец Hello, созданные этой интерактивной программы установки использует этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="dc3c2-130">Приложения также может сделать пользователь toohello визуальный индикатор, интерактивный вход не требуется, поэтому hello пользователь может выбрать toosign нужное время hello в или приложение hello перезапустит `acquireTokenSilent` позднее.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="dc3c2-131">Обычно это используется при hello пользователя можно использовать другие функциональные возможности приложения hello без была прервана - например, отсутствуют содержимого, не прошедшие проверку подлинности в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="dc3c2-132">В этом случае пользователь hello можно указать при хочет toosign в tooaccess hello защищенных ресурсов, или toorefresh hello устаревшие данные.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="dc3c2-133">Вызвать API Microsoft Graph hello hello токен, который был получен с помощью</span><span class="sxs-lookup"><span data-stu-id="dc3c2-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="dc3c2-134">Добавьте следующий код tooyour hello `app.js` файла:</span><span class="sxs-lookup"><span data-stu-id="dc3c2-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in hello page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in hello page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="dc3c2-135">Дополнительные сведения о вызове REST через защищенный API</span><span class="sxs-lookup"><span data-stu-id="dc3c2-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="dc3c2-136">В примере приложения hello, созданные в этом руководстве, hello `callWebApiWithToken()` в противном случае используется toomake HTTP `GET` запроса к защищенному ресурсу, требующий toohello содержимого токена и затем вернуться hello вызывающий объект.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="dc3c2-137">Этот метод добавляет маркер hello получена в hello *заголовок авторизации HTTP*.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="dc3c2-138">Для примера приложения hello, созданные в этом руководстве, hello ресурсов — hello Microsoft Graph API *мне* конечной точки — которого отображаются сведения о профиле пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="dc3c2-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="dc3c2-139">Добавьте метод toosign выход пользователя hello</span><span class="sxs-lookup"><span data-stu-id="dc3c2-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="dc3c2-140">Добавьте следующий код tooyour hello `app.js` файла:</span><span class="sxs-lookup"><span data-stu-id="dc3c2-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
