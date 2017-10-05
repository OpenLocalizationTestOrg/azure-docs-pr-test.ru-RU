---
title: "Типы приложений для конечной точки Azure Active Directory версии 2.0 | Документация Майкрософт"
description: "Типы приложений и сценарии, поддерживаемые конечной точкой Azure Active Directory версии 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 9d59e7f0e8f326c40be86e199d7712f6c565cc13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="app-types-for-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="7946d-103">Типы приложений для конечной точки Azure Active Directory версии 2.0</span><span class="sxs-lookup"><span data-stu-id="7946d-103">App types for the Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="7946d-104">Конечная точка Azure Active Directory версии 2.0 поддерживает аутентификацию для различных современных архитектур приложений, которые основаны на стандартном отраслевом протоколе [OAuth 2.0 или OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="7946d-105">В этой статье описываются типы приложений, которые можно создавать с помощью Azure AD версии 2.0 вне зависимости от выбранного языка и платформы.</span><span class="sxs-lookup"><span data-stu-id="7946d-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="7946d-106">Сведения в этой статье помогут вам получить общее представление о возможных сценариях, прежде вы [приступите к работе с кодом](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="7946d-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="7946d-107">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="7946d-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="7946d-108">Чтобы определить, стоит ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="the-basics"></a><span data-ttu-id="7946d-109">Основные сведения</span><span class="sxs-lookup"><span data-stu-id="7946d-109">The basics</span></span>
<span data-ttu-id="7946d-110">Каждое приложение, использующее конечную точку версии 2.0, нужно зарегистрировать на [портале регистрации приложений Майкрософт](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7946d-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="7946d-111">В процессе регистрации приложения будет задано несколько параметров приложения:</span><span class="sxs-lookup"><span data-stu-id="7946d-111">The app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="7946d-112">**идентификатор приложения**, который определяет конкретное приложение;</span><span class="sxs-lookup"><span data-stu-id="7946d-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="7946d-113">**универсальный код ресурса (URI) перенаправления**, который можно использовать для направления ответов к приложению;</span><span class="sxs-lookup"><span data-stu-id="7946d-113">A **Redirect URI** that you can use to direct responses back to your app</span></span>
* <span data-ttu-id="7946d-114">несколько других зависящих от сценария значений.</span><span class="sxs-lookup"><span data-stu-id="7946d-114">A few other scenario-specific values</span></span>

<span data-ttu-id="7946d-115">Дополнительные сведения см. в статье о [регистрации приложения](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-115">For details, learn how to [register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="7946d-116">После регистрации приложение взаимодействует со службой Azure AD, отправляя запросы к конечной точке Azure AD версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="7946d-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="7946d-117">Мы предоставляем платформы и библиотеки с открытым кодом, которые отвечают обрабатывают данные этих запросов.</span><span class="sxs-lookup"><span data-stu-id="7946d-117">We provide open-source frameworks and libraries that handle the details of these requests.</span></span> <span data-ttu-id="7946d-118">Также имеется возможность самостоятельно реализовать логику аутентификации, создавая запросы к этим конечным точкам.</span><span class="sxs-lookup"><span data-stu-id="7946d-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries to link to -->

## <a name="web-apps"></a><span data-ttu-id="7946d-119">веб-приложений:</span><span class="sxs-lookup"><span data-stu-id="7946d-119">Web apps</span></span>
<span data-ttu-id="7946d-120">Для веб-приложений (.NET, PHP, Java, Ruby, Python, Node), доступных пользователю через браузер, для входа пользователей можно использовать [OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="7946d-121">В OpenID Connect веб-приложение получает маркер идентификации.</span><span class="sxs-lookup"><span data-stu-id="7946d-121">In OpenID Connect, the web app receives an ID token.</span></span> <span data-ttu-id="7946d-122">Это маркер безопасности, который проверяет удостоверение пользователя и предоставляет сведения о пользователе в форме утверждений.</span><span class="sxs-lookup"><span data-stu-id="7946d-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span></span>

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

<span data-ttu-id="7946d-123">Все типы маркеров и утверждений, доступных для приложения, описаны в [справочнике по маркерам версии 2.0](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="7946d-124">В приложениях веб-сервера поток аутентификации для входа состоит из следующих базовых этапов.</span><span class="sxs-lookup"><span data-stu-id="7946d-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span></span>

![Поток аутентификации веб-приложения](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="7946d-126">Личность пользователя можно подтвердить, проверив маркер идентификации с открытым ключом подписывания, полученный от конечной точки версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="7946d-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span></span> <span data-ttu-id="7946d-127">Для этого задается файл cookie сеанса, с помощью которого можно идентифицировать пользователя при последующих запросах страницы.</span><span class="sxs-lookup"><span data-stu-id="7946d-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="7946d-128">Чтобы увидеть этот сценарий в действии, изучите один из примеров кода входа в веб-приложение в разделе [Приступая к работе](active-directory-appmodel-v2-overview.md#getting-started) для версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="7946d-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="7946d-129">Помимо простого входа в систему, приложению веб-сервера может потребоваться доступ к некоторым другим веб-службам, например интерфейсу REST API.</span><span class="sxs-lookup"><span data-stu-id="7946d-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span></span> <span data-ttu-id="7946d-130">В этом случае приложение веб-сервера участвует в объединенном потоке OpenID Connect и OAuth 2.0 с использованием [потока кода авторизации OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="7946d-131">Чтобы больше узнать об этом сценарии, ознакомьтесь с тем, как [приступить к работе с веб-приложениями и интерфейсами веб-API](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="7946d-132">Веб-API</span><span class="sxs-lookup"><span data-stu-id="7946d-132">Web APIs</span></span>
<span data-ttu-id="7946d-133">Конечную точку версии 2.0 можно использовать для защиты веб-служб, таких как веб-API REST.</span><span class="sxs-lookup"><span data-stu-id="7946d-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="7946d-134">Веб-API вместо маркеров идентификации и файлов cookie сеанса использует маркер доступа OAuth 2.0 для защиты данных и аутентификации входящих запросов.</span><span class="sxs-lookup"><span data-stu-id="7946d-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span></span> <span data-ttu-id="7946d-135">Объект, вызывающий веб-API, добавляет маркер доступа в начале заголовка авторизации HTTP-запроса, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7946d-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="7946d-136">Веб-API использует маркер доступа для проверки удостоверения объекта, вызывающего API, и получения сведений о нем из утверждений, которые закодированы в маркере доступа.</span><span class="sxs-lookup"><span data-stu-id="7946d-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span></span> <span data-ttu-id="7946d-137">Чтобы изучить все типы маркеров и утверждений, доступных для приложения, ознакомьтесь со [справочником по маркерам версии 2.0](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="7946d-138">Веб-API может дать пользователям возможность применять определенные функции и данные или отказаться от них, предоставляя разрешения, которые также называют [областями](active-directory-v2-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="7946d-139">Чтобы вызывающее приложение получило разрешение для области, пользователь должен дать согласие на это.</span><span class="sxs-lookup"><span data-stu-id="7946d-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span></span> <span data-ttu-id="7946d-140">Конечная точка версии 2.0 запрашивает разрешения у пользователя и записывает их во все маркеры доступа, получаемые веб-API.</span><span class="sxs-lookup"><span data-stu-id="7946d-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span></span> <span data-ttu-id="7946d-141">Веб-API проверяет маркеры доступа, получаемые при каждом вызове, и выполняет проверки авторизации.</span><span class="sxs-lookup"><span data-stu-id="7946d-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="7946d-142">Веб-API может получать маркеры доступа от всех типов приложений, включая приложения веб-сервера, классические и мобильные приложения, одностраничные приложения, серверные управляющие программы и даже другие веб-API.</span><span class="sxs-lookup"><span data-stu-id="7946d-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="7946d-143">Общий поток для веб-API выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="7946d-143">The high-level flow for a Web API looks like this:</span></span>

![Поток аутентификации веб-API](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="7946d-145">Чтобы узнать, как защитить веб-API с помощью маркеров доступа OAuth 2.0, изучите примеры кода веб-API в разделе [Приступая к работе](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="7946d-145">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="7946d-146">Во многих случаях веб-интерфейсам API также требуется выполнять исходящие запросы к другим нижестоящим веб-API, защищенным Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7946d-146">In many cases, web APIs also need to make outbound requests to other downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="7946d-147">Для этого веб-API могут воспользоваться преимуществами потока **От имени** Azure AD. Это позволяет им обменять входящий маркер доступа на другой маркер доступа, который будет использоваться в исходящих запросах.</span><span class="sxs-lookup"><span data-stu-id="7946d-147">To do so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows the web API to exchange an incoming access token for another access token to be used in outbound requests.</span></span>  <span data-ttu-id="7946d-148">Дополнительные сведения о потоке "От имени" конечной точки версии 2.0 см. [здесь](active-directory-v2-protocols-oauth-on-behalf-of.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-148">The v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="7946d-149">Мобильные и собственные приложения</span><span class="sxs-lookup"><span data-stu-id="7946d-149">Mobile and native apps</span></span>
<span data-ttu-id="7946d-150">Приложениям, установленным на устройстве, например мобильным и классическим приложениям, часто требуется доступ к внутренним службам или интерфейсам веб-API, которые хранят данные и выполняют различные функции от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="7946d-150">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="7946d-151">В этих приложениях можно реализовать процесс входа и авторизации во внутренних службах с помощью [потока кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-151">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="7946d-152">В этом потоке приложение получает код авторизации от конечной точки версии 2.0 при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="7946d-152">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span></span> <span data-ttu-id="7946d-153">Код авторизации представляет собой разрешение, полученное от приложения, на вызов внутренних служб от имени пользователя, выполнившего вход.</span><span class="sxs-lookup"><span data-stu-id="7946d-153">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span></span> <span data-ttu-id="7946d-154">Приложение может передать код авторизации в фоновом режиме, чтобы получить маркер доступа OAuth 2.0 и маркер обновления.</span><span class="sxs-lookup"><span data-stu-id="7946d-154">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="7946d-155">Приложение может использовать маркер доступа для аутентификации в интерфейсах веб-API в HTTP-запросах и использовать маркер обновления, чтобы получать новые маркеры доступа после истечения срока действия старых маркеров.</span><span class="sxs-lookup"><span data-stu-id="7946d-155">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span></span>

![Поток аутентификации собственного приложения](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="7946d-157">Одностраничные приложения (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="7946d-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="7946d-158">Многие современные приложения содержат интерфейсное одностраничное приложение, созданное преимущественно на языке JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7946d-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="7946d-159">Часто они создаются с помощью таких платформ, как AngularJS, Ember.js или Durandal.js.</span><span class="sxs-lookup"><span data-stu-id="7946d-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="7946d-160">Конечная точка Azure AD версии 2.0 поддерживает эти приложения с помощью [неявного потока OAuth 2.0](active-directory-v2-protocols-implicit.md).</span><span class="sxs-lookup"><span data-stu-id="7946d-160">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="7946d-161">В этом потоке приложение получает маркеры из конечной точки авторизации версии 2.0 напрямую, без какого-либо обмена данными между серверами.</span><span class="sxs-lookup"><span data-stu-id="7946d-161">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="7946d-162">Вся логика аутентификации и обработки сеансов размещается в клиенте JavaScript без перенаправления на дополнительные страницы.</span><span class="sxs-lookup"><span data-stu-id="7946d-162">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span></span>

![Неявный поток аутентификации](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="7946d-164">Чтобы увидеть этот сценарий в действии, изучите один из примеров кода одностраничного приложения из раздела [Приступая к работе](active-directory-appmodel-v2-overview.md#getting-started) .</span><span class="sxs-lookup"><span data-stu-id="7946d-164">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="7946d-165">Управляющие программы и серверные приложения</span><span class="sxs-lookup"><span data-stu-id="7946d-165">Daemons and server-side apps</span></span>
<span data-ttu-id="7946d-166">Приложениям, использующим долговременные процессы или работающим без взаимодействия с пользователем, тоже нужна возможность доступа к защищенным ресурсам, таким как интерфейсы веб-API.</span><span class="sxs-lookup"><span data-stu-id="7946d-166">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span></span> <span data-ttu-id="7946d-167">Такие приложения могут выполнять аутентификацию и получать маркеры, используя удостоверение приложения (а не делегированное удостоверение пользователя) с помощью потока учетных данных клиента OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="7946d-167">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="7946d-168">В этом потоке приложение взаимодействует непосредственно с конечной точкой `/token`, чтобы получить конечные точки.</span><span class="sxs-lookup"><span data-stu-id="7946d-168">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span></span>

![Поток аутентификации управляющей программы](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="7946d-170">Чтобы создать управляющую программу, изучите документацию по учетным данным клиентов в нашем разделе [Приступая к работе](active-directory-appmodel-v2-overview.md#getting-started) или ознакомьтесь с [примером приложения .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span><span class="sxs-lookup"><span data-stu-id="7946d-170">To build a daemon app, see the client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>
