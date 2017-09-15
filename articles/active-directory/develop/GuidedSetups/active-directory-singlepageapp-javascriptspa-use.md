---
title: "Интерактивная настройка Azure AD версии 2 для приложений JS SPA | Документация Майкрософт"
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
ms.openlocfilehash: f52157df298ddfc1c1b29a18dc9a54aae59b52a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-sign-in-the-user"></a><span data-ttu-id="36275-103">Использование библиотеки проверки подлинности Майкрософт (MSAL) для входа пользователя</span><span class="sxs-lookup"><span data-stu-id="36275-103">Use the Microsoft Authentication Library (MSAL) to sign-in the user</span></span>

1.  <span data-ttu-id="36275-104">Создайте файл с именем `app.js`.</span><span class="sxs-lookup"><span data-stu-id="36275-104">Create a file named `app.js`.</span></span> <span data-ttu-id="36275-105">Если вы работаете с Visual Studio, выберите проект (корневую папку проекта), щелкните правой кнопкой мыши и выберите `Add` > `New Item` > `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="36275-105">If you are using Visual Studio, select the project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="36275-106">Добавьте в файл `app.js` следующий код:</span><span class="sxs-lookup"><span data-stu-id="36275-106">Add the following code to your `app.js` file:</span></span>

```javascript
// Graph API endpoint to show user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used to obtain the access token to read user profile
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
    // If page is refreshed, continue to display user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call the Microsoft Graph API and display the results on the page. Sign the user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user to sign in via loginRedirect.
        // This will redirect user to the Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // The call to loginRedirect above frontloads the consent to query Graph API during the sign-in.
        // If you want to use dynamic consent, just remove the graphAPIScopes from loginRedirect call.
        // As such, user will be prompted to give consent when requested access to a resource that 
        // he/she hasn't consented before. In the case of this application - 
        // the first time the Graph API call to obtain user's profile is executed.
    } else {
        // If user is already signed in, display the user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API to show the user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order to call the Graph API, an access token needs to be acquired.
        // Try to acquire the token used to query Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After the access token is acquired, call the Web API, sending the acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If the acquireTokenSilent() method fails, then acquire the token interactively via acquireTokenRedirect().
                // In this case, the browser will redirect user back to the Azure Active Directory v2 Endpoint so the user 
                // can reenter the current username/ password and/ or give consent to new permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get the token silently, the Graph API call results will be made and results will be displayed in the page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() to show results.
 * @param {string} errorDesc - If error occur, the error message
 * @param {object} token - The token received from login
 * @param {object} error - The error string
 * @param {string} tokenType - the token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in the page
 * @param {string} endpoint - the endpoint used for the error message
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
### <a name="more-information"></a><span data-ttu-id="36275-107">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="36275-107">More Information</span></span>

<span data-ttu-id="36275-108">Когда пользователь впервые нажимает кнопку *Call Microsoft Graph API* (Вызвать API Microsoft Graph), метод `callGraphApi` вызывает `loginRedirect` для входа пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="36275-108">After a user clicks the *‘Call Microsoft Graph API’* button for the first time, `callGraphApi` method calls `loginRedirect` to sign in the user.</span></span> <span data-ttu-id="36275-109">В результате выполнения этого метода пользователь перенаправляется на *конечную точку Microsoft Azure Active Directory версии 2* для запроса и проверки учетных данных.</span><span class="sxs-lookup"><span data-stu-id="36275-109">This method results in redirecting the user to the *Microsoft Azure Active Directory v2 endpoint* to prompt and validate the user's credentials.</span></span> <span data-ttu-id="36275-110">В результате успешного входа пользователь перенаправляется обратно на исходную страницу *index.html*, поступает маркер, обрабатываемый `msal.js`, после чего кэшируются сведения, содержащиеся в маркере.</span><span class="sxs-lookup"><span data-stu-id="36275-110">As a result of a successful sign-in, the user is redirected back to the original *index.html* page, and a token is received, processed by `msal.js` and the information contained in the token is cached.</span></span> <span data-ttu-id="36275-111">Этот маркер известен как *маркер идентификатора*. Он содержит основные сведения о пользователе, такие как отображаемое имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="36275-111">This token is known as the *ID token* and contains basic information about the user, such as the user display name.</span></span> <span data-ttu-id="36275-112">Если вы планируете использовать какие-либо данные, предоставляемые этим маркером, то необходимо убедиться, что маркер проверен внутренним сервером. Это позволит гарантировать, что маркер был выдан допустимому пользователю для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="36275-112">If you plan to use any data provided by this token for any purposes, you need to make sure this token is validated by your backend server to guarantee that the token was issued to a valid user for your application.</span></span>

<span data-ttu-id="36275-113">Одностраничное приложение, создаваемое в этом руководстве, не использует маркер идентификатора напрямую. Вместо этого оно вызывает `acquireTokenSilent` и (или) `acquireTokenRedirect` для получения *маркера доступа*, используемого для запроса API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="36275-113">The SPA generated by this guide does not make use directly of the ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` to acquire an *access token* used to query the Microsoft Graph API.</span></span> <span data-ttu-id="36275-114">Если вам нужен пример, проверяющий маркер идентификатора, ознакомьтесь с [этим](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Пример active-directory-javascript-singlepageapp-dotnet-webapi-v2 на портале GitHub") примером приложения на портале GitHub. В нем для проверки маркеров используется веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="36275-114">If you need a sample that validates the ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – the sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="36275-115">Интерактивное получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="36275-115">Getting a user token interactively</span></span>

<span data-ttu-id="36275-116">После первоначального входа вам не нужно требовать от пользователей повторно проходить проверку подлинности каждый раз, когда они запрашивают маркер для доступа к ресурсу, поэтому в большинстве случаев для получения маркеров следует использовать *acquireTokenSilent*.</span><span class="sxs-lookup"><span data-stu-id="36275-116">After the initial sign-in, you do not want the ask users to reauthenticate every time they need to request a token to access a resource – so *acquireTokenSilent* should be used most of the time to acquire tokens.</span></span> <span data-ttu-id="36275-117">Но существуют ситуации, когда пользователи должны взаимодействовать с конечной точкой Azure Active Directory версии 2. Далее приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="36275-117">There are situations however that you need to force users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="36275-118">Пользователям может потребоваться повторно ввести учетные данные, так как истек срок действия пароля</span><span class="sxs-lookup"><span data-stu-id="36275-118">Users may need to reenter their credentials because the password has expired</span></span>
-   <span data-ttu-id="36275-119">Ваше приложение запрашивает доступ к ресурсу, на обращение к которому пользователь должен дать согласие</span><span class="sxs-lookup"><span data-stu-id="36275-119">Your application is requesting access to a resource that the user needs to consent to</span></span>
-   <span data-ttu-id="36275-120">Требуется двухфакторная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="36275-120">Two factor authentication is required</span></span>

<span data-ttu-id="36275-121">Вызов *acquireTokenRedirect(scope)* приводит к перенаправлению пользователей на конечную точку Azure Active Directory версии 2 (или *acquireTokenPopup(scope)* приводит к отображению всплывающего окна), с которой пользователям нужно взаимодействовать либо подтвердив свои учетные данные, дав согласие на доступ к требуемому ресурсу, либо выполнив двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="36275-121">Calling the *acquireTokenRedirect(scope)* result in redirecting users to the Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need to interact with by either confirming their credentials, giving the consent to the required resource, or completing the two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="36275-122">Автоматическое получение маркера пользователя</span><span class="sxs-lookup"><span data-stu-id="36275-122">Getting a user token silently</span></span>
<span data-ttu-id="36275-123">Метод ` acquireTokenSilent` обрабатывает получение и обновление маркера без участия пользователя.</span><span class="sxs-lookup"><span data-stu-id="36275-123">The ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="36275-124">После первого выполнения метода `loginRedirect` (или `loginPopup`) обычно используется метод `acquireTokenSilent`, чтобы получить маркеры для доступа к защищенным ресурсам для последующих вызовов (например, автоматическое выполнение запросов или обновлений маркеров).</span><span class="sxs-lookup"><span data-stu-id="36275-124">After `loginRedirect` (or `loginPopup`) is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="36275-125">В некоторых случаях `acquireTokenSilent` может завершиться ошибкой, например если истек срок действия пароля пользователя.</span><span class="sxs-lookup"><span data-stu-id="36275-125">`acquireTokenSilent` may fail in some cases – for example, the user's password has expired.</span></span> <span data-ttu-id="36275-126">Приложение может обработать это исключение двумя способами:</span><span class="sxs-lookup"><span data-stu-id="36275-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="36275-127">Немедленно вызвать `acquireTokenRedirect`, в результате чего пользователю будет предложено выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="36275-127">Make a call to `acquireTokenRedirect` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="36275-128">Этот шаблон обычно используется в интерактивных приложениях, где пользователю недоступно не прошедшее проверку подлинности содержимое.</span><span class="sxs-lookup"><span data-stu-id="36275-128">This pattern is commonly used in online applications where there is no unauthenticated content in the application available to the user.</span></span> <span data-ttu-id="36275-129">Пример, созданный в ходе пошаговой настройки, использует этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="36275-129">The sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="36275-130">Приложения также могут визуально уведомить пользователя, что требуется интерактивный вход, чтобы пользователь мог выбрать подходящее время для входа или приложение могло повторить метод `acquireTokenSilent` ​​позднее.</span><span class="sxs-lookup"><span data-stu-id="36275-130">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="36275-131">Обычно это применимо для тех случаев, когда пользователь может использовать другие функции приложения, на которые это не влияет, например, когда в приложении есть не прошедшее проверку подлинности содержимое.</span><span class="sxs-lookup"><span data-stu-id="36275-131">This is commonly used when the user can use other functionality of the application without being disrupted - for example, there is unauthenticated content available in the application.</span></span> <span data-ttu-id="36275-132">В этом случае пользователь может решить, когда ему требуется вход для доступа к защищенному ресурсу, или обновить устаревшие данные.</span><span class="sxs-lookup"><span data-stu-id="36275-132">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="36275-133">Вызов API Microsoft Graph с помощью полученного маркера</span><span class="sxs-lookup"><span data-stu-id="36275-133">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="36275-134">Добавьте в файл `app.js` следующий код:</span><span class="sxs-lookup"><span data-stu-id="36275-134">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used to display the results
 * @param {object} showTokenElement = HTML element used to display the RAW access token
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
                        // Display response in the page
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
                        // Display response as error in the page
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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="36275-135">Дополнительные сведения о вызове REST через защищенный API</span><span class="sxs-lookup"><span data-stu-id="36275-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="36275-136">В примере приложения, созданном в этом руководстве, метод `callWebApiWithToken()` выполняет HTTP-запрос `GET` к защищенному ресурсу, требующему маркер, а затем возвращает содержимое вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="36275-136">In the sample application created by this guide, the `callWebApiWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="36275-137">Этот метод добавляет полученный маркер в *заголовок авторизации HTTP*.</span><span class="sxs-lookup"><span data-stu-id="36275-137">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="36275-138">Для примера приложения, созданного в этом руководстве, ресурс — это конечная точка *me* API Microsoft Graph, которая отображает сведения о профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="36275-138">For the sample application created by this guide, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="36275-139">Добавление метода для выхода пользователя</span><span class="sxs-lookup"><span data-stu-id="36275-139">Add a method to sign out the user</span></span>

<span data-ttu-id="36275-140">Добавьте в файл `app.js` следующий код:</span><span class="sxs-lookup"><span data-stu-id="36275-140">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Sign-out the user
 */
function signOut() {
    userAgentApplication.logout();
}
```
