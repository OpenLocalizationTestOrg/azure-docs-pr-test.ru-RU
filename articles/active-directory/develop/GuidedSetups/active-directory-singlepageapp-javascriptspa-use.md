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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Используйте user в toosign hello hello библиотеки проверки подлинности Microsoft (MSAL)

1.  Создайте файл с именем `app.js`. Если вы используете Visual Studio, выберите hello проектов (корневой папки проекта,), щелкните правой кнопкой мыши и выберите: `Add`  >  `New Item`  >  `JavaScript File`:
2.  Добавьте следующий код tooyour hello `app.js` файла:

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
### <a name="more-information"></a>Дополнительные сведения

После нажатия пользователем hello *«Вызвать Microsoft Graph API»* кнопки для hello первый раз `callGraphApi` вызовы метода `loginRedirect` toosign в hello пользователя. Этот метод приводит к перенаправление hello пользователя toohello *конечной точки Microsoft Azure Active Directory v2* tooprompt и проверки учетных данных пользователя hello. В результате успешного входа в систему пользователь hello является перенаправленный задней toohello исходного *index.html* страницы и токен поступает, обрабатываемых `msal.js` и кэшируется hello сведения, содержащиеся в маркере hello. Этот маркер называется hello *маркер идентификатора* и содержит основные сведения о пользователе hello, такие как отображаемое имя пользователя hello. Если планируется toouse данные предоставляемых по этот маркер для каких целей, необходимо убедиться, что этот маркер проверяется с вашей tooguarantee сервера базы данных, hello маркера toomake выдан tooa допустимого пользователя для приложения.

Hello SPA, созданные в этом руководстве не смог использовать напрямую из маркер идентификатора hello-вместо этого он вызывает `acquireTokenSilent` и/или `acquireTokenRedirect` tooacquire *маркер доступа* используется tooquery hello Microsoft Graph API. Если вам требуется образец, проверяет маркер идентификатора hello, взгляните на [это](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 пример") примера приложения в GitHub — образец hello использует веб-API ASP.NET для проверки токенов.

#### <a name="getting-a-user-token-interactively"></a>Интерактивное получение маркера пользователя

После hello, начальный вход, вы не хотите hello Попросите пользователей tooreauthenticate каждый раз, они должны toorequest маркера tooaccess ресурсов — так *acquireTokenSilent* следует использовать большую часть токены tooacquire времени hello. Однако существуют ситуации, необходимо tooforce пользователи взаимодействуют с конечной точкой v2 Azure Active Directory — некоторые примеры:
-   Пользователям может потребоваться tooreenter свои учетные данные, так как истек срок действия пароля hello
-   Приложение запрашивает ресурс tooa доступ, hello tooconsent потребностей пользователя для
-   Требуется двухфакторная проверка подлинности

Вызов hello *acquireTokenRedirect(scope)* привести перенаправления конечной точки toohello v2 Azure Active Directory пользователей (или *acquireTokenPopup(scope)* результат всплывающем окне) которых пользователям необходимо toointeract с подтверждая либо свои учетные данные, предоставляя toohello согласия hello необходимых ресурсов или завершение hello двухфакторной проверки подлинности.

#### <a name="getting-a-user-token-silently"></a>Автоматическое получение маркера пользователя
Hello ` acquireTokenSilent` метод обрабатывает приобретения токена и обновления без вмешательства пользователя. После `loginRedirect` (или `loginPopup`) выполняется для hello первый раз `acquireTokenSilent` tooobtain маркерами hello распространенным методом tooaccess защищенные ресурсы для последующих вызовов — как вызовы toorequest или обновить маркеры выполняются без вмешательства пользователя.
`acquireTokenSilent`может ли сбой в некоторых случаях — например, пароль пользователя hello истек. Приложение может обработать это исключение двумя способами:

1.  Вызвать слишком`acquireTokenRedirect` немедленно, что приводит запроса hello toosign пользователя в. Этот шаблон обычно используется в веб-приложений которого нет содержимого, не прошедшие проверку подлинности в пользователя доступны toohello приложения hello. Образец Hello, созданные этой интерактивной программы установки использует этот шаблон.

2. Приложения также может сделать пользователь toohello визуальный индикатор, интерактивный вход не требуется, поэтому hello пользователь может выбрать toosign нужное время hello в или приложение hello перезапустит `acquireTokenSilent` позднее. Обычно это используется при hello пользователя можно использовать другие функциональные возможности приложения hello без была прервана - например, отсутствуют содержимого, не прошедшие проверку подлинности в приложение hello. В этом случае пользователь hello можно указать при хочет toosign в tooaccess hello защищенных ресурсов, или toorefresh hello устаревшие данные.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Вызвать API Microsoft Graph hello hello токен, который был получен с помощью

Добавьте следующий код tooyour hello `app.js` файла:

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Дополнительные сведения о вызове REST через защищенный API

В примере приложения hello, созданные в этом руководстве, hello `callWebApiWithToken()` в противном случае используется toomake HTTP `GET` запроса к защищенному ресурсу, требующий toohello содержимого токена и затем вернуться hello вызывающий объект. Этот метод добавляет маркер hello получена в hello *заголовок авторизации HTTP*. Для примера приложения hello, созданные в этом руководстве, hello ресурсов — hello Microsoft Graph API *мне* конечной точки — которого отображаются сведения о профиле пользователя hello.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Добавьте метод toosign выход пользователя hello

Добавьте следующий код tooyour hello `app.js` файла:

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
