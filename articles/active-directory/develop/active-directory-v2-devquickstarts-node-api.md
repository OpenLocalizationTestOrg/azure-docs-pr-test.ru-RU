---
title: "Защита веб-API Azure Active Directory v2.0 с помощью Node.js | Документы Майкрософт"
description: "Узнайте, как создать веб-API .NET Node.js, принимающий маркеры доступа личных учетных записей Майкрософт, а также рабочих и учебных учетных записей."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="d438d-103">Защита веб-API с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="d438d-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="d438d-104">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="d438d-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="d438d-105">Чтобы определить, стоит ли вам использовать конечную точку версии 2.0 или 1.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d438d-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="d438d-106">При использовании конечной точки Azure Active Directory (Azure AD) версии 2.0 можно использовать маркеры доступа [OAuth 2.0](active-directory-v2-protocols.md) для защиты веб-API.</span><span class="sxs-lookup"><span data-stu-id="d438d-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="d438d-107">С помощью маркеров доступа OAuth 2.0 пользователи с личными учетными записями Майкрософт и рабочими или учебными учетными записями могут безопасно обращаться в вашему веб-API.</span><span class="sxs-lookup"><span data-stu-id="d438d-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="d438d-108">*Passport* — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="d438d-109">Он отличается гибкой модульной структурой, которая позволяет сравнительно незаметно размещать его в любом приложении на основе Express или веб-приложении Restify.</span><span class="sxs-lookup"><span data-stu-id="d438d-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="d438d-110">В Passport полный набор стратегий поддерживает процесс проверки подлинности с помощью имени пользователя и пароля, Facebook, Twitter и проч.</span><span class="sxs-lookup"><span data-stu-id="d438d-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="d438d-111">Мы разработали стратегию для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d438d-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="d438d-112">В этой статье описывается установка модуля и последующее добавление подключаемого модуля `passport-azure-ad` Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d438d-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="d438d-113">Загрузить</span><span class="sxs-lookup"><span data-stu-id="d438d-113">Download</span></span>
<span data-ttu-id="d438d-114">Код в этом учебнике размещен на портале [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="d438d-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="d438d-115">Для выполнения действий в этом руководстве вы можете [скачать заготовку приложения как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip) или клонировать структуру:</span><span class="sxs-lookup"><span data-stu-id="d438d-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="d438d-116">Можно также воспользоваться готовым приложением в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="d438d-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="d438d-117">Шаг 1. Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="d438d-117">1: Register an app</span></span>
<span data-ttu-id="d438d-118">Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md), чтобы зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="d438d-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="d438d-119">Не забудьте выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d438d-119">Make sure you:</span></span>

* <span data-ttu-id="d438d-120">Скопируйте **идентификатор приложения**, назначенный приложению.</span><span class="sxs-lookup"><span data-stu-id="d438d-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="d438d-121">Он потребуется для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="d438d-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="d438d-122">Добавьте для приложения **мобильную** платформу.</span><span class="sxs-lookup"><span data-stu-id="d438d-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="d438d-123">Скопируйте значение **URI перенаправления** с портала.</span><span class="sxs-lookup"><span data-stu-id="d438d-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="d438d-124">Необходимо использовать значение URI по умолчанию — `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="d438d-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="d438d-125">Шаг 2. Установка Node.js</span><span class="sxs-lookup"><span data-stu-id="d438d-125">2: Install Node.js</span></span>
<span data-ttu-id="d438d-126">Чтобы использовать пример для этого руководства, необходимо [установить Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="d438d-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="d438d-127">Шаг 3. Установка MongoDB</span><span class="sxs-lookup"><span data-stu-id="d438d-127">3: Install MongoDB</span></span>
<span data-ttu-id="d438d-128">Чтобы успешно использовать этот пример, необходимо [установить MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="d438d-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="d438d-129">В этом примере MongoDB используется, чтобы интерфейс REST API устойчиво работал с несколькими экземплярами сервера.</span><span class="sxs-lookup"><span data-stu-id="d438d-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="d438d-130">В этой статье предполагается, что вы используете установку по умолчанию и конечные точки сервера для MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="d438d-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="d438d-131">Шаг 4. Установка модулей Restify для веб-API</span><span class="sxs-lookup"><span data-stu-id="d438d-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="d438d-132">Мы используем Resitfy для построения интерфейса REST API.</span><span class="sxs-lookup"><span data-stu-id="d438d-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="d438d-133">Restify — это минималистичная и гибкая платформа для приложений Node.j, созданная на основе Express.</span><span class="sxs-lookup"><span data-stu-id="d438d-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="d438d-134">Restify имеет широкий набор функций, которые можно использовать для создания интерфейсов REST API поверх Connect.</span><span class="sxs-lookup"><span data-stu-id="d438d-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="d438d-135">Установка Restify</span><span class="sxs-lookup"><span data-stu-id="d438d-135">Install restify</span></span>
1.  <span data-ttu-id="d438d-136">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="d438d-137">Если каталог **azuread** не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="d438d-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="d438d-138">Установите Restify.</span><span class="sxs-lookup"><span data-stu-id="d438d-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="d438d-139">Выходные данные этой команды должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d438d-139">The output of this command should look like this:</span></span>

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a><span data-ttu-id="d438d-140">Вы получили сообщение об ошибке?</span><span class="sxs-lookup"><span data-stu-id="d438d-140">Did you get an error?</span></span>
<span data-ttu-id="d438d-141">В некоторых операционных системах при использовании команды `npm` может появиться сообщение: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="d438d-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="d438d-142">Оно сопровождается запросом на использование учетной записи с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="d438d-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="d438d-143">В этом случае необходимо с помощью команды `sudo` запустить `npm` с более высоким уровнем привилегий.</span><span class="sxs-lookup"><span data-stu-id="d438d-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="d438d-144">Вы получили сообщение об ошибке, которая относится к DTrace?</span><span class="sxs-lookup"><span data-stu-id="d438d-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="d438d-145">При установке Restify может появиться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="d438d-145">When you install restify, you might see this message:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="d438d-146">Restify предоставляет мощный механизм для трассировки вызовов REST с помощью DTrace.</span><span class="sxs-lookup"><span data-stu-id="d438d-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="d438d-147">Однако во многих операционных системах DTrace отсутствует.</span><span class="sxs-lookup"><span data-stu-id="d438d-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="d438d-148">Это сообщение об ошибке можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="d438d-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="d438d-149">Шаг 5. Установка Passport.js для веб-интерфейса API</span><span class="sxs-lookup"><span data-stu-id="d438d-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="d438d-150">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="d438d-151">Установите Passport.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="d438d-152">Выходные данные этой команды должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d438d-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="d438d-153">Шаг 6. Добавление Passport-Azure-AD в веб-API</span><span class="sxs-lookup"><span data-stu-id="d438d-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="d438d-154">Затем добавьте стратегию OAuth с помощью passport-azuread.</span><span class="sxs-lookup"><span data-stu-id="d438d-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="d438d-155">`passport-azuread` — это набор стратегий, который устанавливает подключение Azure AD к Passport.</span><span class="sxs-lookup"><span data-stu-id="d438d-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="d438d-156">В этом примере REST API мы будем использовать эту стратегию для токенов носителя.</span><span class="sxs-lookup"><span data-stu-id="d438d-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="d438d-157">Платформа OAuth 2.0 позволяет выдавать маркеры любого известного типа, но в большинстве случаев используются маркеры только нескольких типов.</span><span class="sxs-lookup"><span data-stu-id="d438d-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="d438d-158">Маркер-носитель обычно используется для защиты конечных точек.</span><span class="sxs-lookup"><span data-stu-id="d438d-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="d438d-159">Это самый распространенный тип выдаваемых маркеров в OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d438d-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="d438d-160">Во многих реализациях OAuth 2.0 предполагается, что маркер-носитель — это единственный тип выданного токена.</span><span class="sxs-lookup"><span data-stu-id="d438d-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="d438d-161">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="d438d-162">Установите модуль Passport.js `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="d438d-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="d438d-163">Выходные данные этой команды должны выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d438d-163">The output of the command should look like this:</span></span>

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="d438d-164">Шаг 7. Добавление модулей MongoDB в веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="d438d-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="d438d-165">В этом примере мы используем MongoDB в качестве хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="d438d-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="d438d-166">Установите Mongoose, широко используемый подключаемый модуль для управления моделями и схемами.</span><span class="sxs-lookup"><span data-stu-id="d438d-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="d438d-167">Установите драйвер базы данных для MongoDB (который также называется MongoDB).</span><span class="sxs-lookup"><span data-stu-id="d438d-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="d438d-168">Шаг 8. Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="d438d-168">8: Install additional modules</span></span>
<span data-ttu-id="d438d-169">Установите остальные необходимые модули.</span><span class="sxs-lookup"><span data-stu-id="d438d-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="d438d-170">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="d438d-171">Введите следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d438d-171">Enter the following commands.</span></span> <span data-ttu-id="d438d-172">Они используются для установки следующих модулей в каталоге node_modules:</span><span class="sxs-lookup"><span data-stu-id="d438d-172">The commands install the following modules in your node_modules directory:</span></span>

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="d438d-173">Шаг 9. Создание файла Server.js для зависимостей</span><span class="sxs-lookup"><span data-stu-id="d438d-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="d438d-174">Основная часть функций для сервера веб-API реализована в файле Server.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="d438d-175">Добавьте в этот файл основную часть своего кода.</span><span class="sxs-lookup"><span data-stu-id="d438d-175">Add most of your code to this file.</span></span> <span data-ttu-id="d438d-176">В производственных целях можно разделить функционал на небольшие файлы, такие как отдельные маршруты и контроллеры.</span><span class="sxs-lookup"><span data-stu-id="d438d-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="d438d-177">В этой статье мы используем Server.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="d438d-178">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="d438d-179">С помощью редактора по своему усмотрению создайте файл server.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="d438d-180">Добавьте в файл следующие данные:</span><span class="sxs-lookup"><span data-stu-id="d438d-180">Add the following information to the file:</span></span>

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  <span data-ttu-id="d438d-181">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="d438d-181">Save the file.</span></span> <span data-ttu-id="d438d-182">Вы вернетесь к нему позже.</span><span class="sxs-lookup"><span data-stu-id="d438d-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="d438d-183">Шаг 10. Создание файла конфигурации для сохранения параметров Azure AD</span><span class="sxs-lookup"><span data-stu-id="d438d-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="d438d-184">Данный фрагмент кода передает параметры конфигурации с вашего портала Azure AD в файл Passport.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="d438d-185">Эти значения конфигурации были созданы, когда вы добавляли веб-API на портал, выполняя первую часть этого руководства.</span><span class="sxs-lookup"><span data-stu-id="d438d-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="d438d-186">Мы объясним, какие значения нужно указать для этих параметров в скопированном фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="d438d-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="d438d-187">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="d438d-188">В редакторе создайте файл Config.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="d438d-189">Добавьте следующие данные:</span><span class="sxs-lookup"><span data-stu-id="d438d-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="d438d-190">Обязательные значения</span><span class="sxs-lookup"><span data-stu-id="d438d-190">Required values</span></span>

*   <span data-ttu-id="d438d-191">**IdentityMetadata**. Здесь модуль `passport-azure-ad` будет искать данные конфигурации для поставщика удостоверений (IDP), а также ключи для проверки маркеров JWT.</span><span class="sxs-lookup"><span data-stu-id="d438d-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="d438d-192">Если вы используете Azure AD, возможно, эти данные изменять не нужно.</span><span class="sxs-lookup"><span data-stu-id="d438d-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="d438d-193">**audience**— это универсальный код ресурса (URI) перенаправления с портала.</span><span class="sxs-lookup"><span data-stu-id="d438d-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d438d-194">Рекомендуется часто менять ключи.</span><span class="sxs-lookup"><span data-stu-id="d438d-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="d438d-195">Убедитесь, что вы всегда извлекаете данные из URL-адреса openid_keys и что приложение имеет доступ к Интернету.</span><span class="sxs-lookup"><span data-stu-id="d438d-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="d438d-196">Шаг 11. Добавление конфигурации в файл Server.js</span><span class="sxs-lookup"><span data-stu-id="d438d-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="d438d-197">Приложение должно считывать значения из только что созданного файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d438d-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="d438d-198">Добавьте в приложение файл с расширением .config в качестве требуемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="d438d-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="d438d-199">Задайте глобальным переменным значения из файла Config.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="d438d-200">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="d438d-201">В редакторе откройте файл Server.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-201">In an editor, open Server.js.</span></span> <span data-ttu-id="d438d-202">Добавьте следующие данные:</span><span class="sxs-lookup"><span data-stu-id="d438d-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="d438d-203">Добавьте новый раздел в Server.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="d438d-204">Шаг 12. Добавление сведений о модели и схеме MongoDB с помощью Mongoose</span><span class="sxs-lookup"><span data-stu-id="d438d-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="d438d-205">Затем подключите эти три файла в службе REST API.</span><span class="sxs-lookup"><span data-stu-id="d438d-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="d438d-206">В этой статье мы используем MongoDB для хранения наших задач.</span><span class="sxs-lookup"><span data-stu-id="d438d-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="d438d-207">Этот вопрос обсуждается на *шаге 4*.</span><span class="sxs-lookup"><span data-stu-id="d438d-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="d438d-208">В файле Config.js, созданном на шаге 11, база данных называется *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="d438d-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="d438d-209">Это вы указали в конце URL-адреса подключения mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="d438d-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="d438d-210">Не нужно заранее создавать эту базу данных в MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d438d-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="d438d-211">База данных создается при первом запуске серверного приложения (при условии, что база данных еще не существует).</span><span class="sxs-lookup"><span data-stu-id="d438d-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="d438d-212">Вы указали серверу, какую базу данных MongoDB следует использовать.</span><span class="sxs-lookup"><span data-stu-id="d438d-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="d438d-213">Далее необходимо написать дополнительный код для создания модели и схемы для задач сервера.</span><span class="sxs-lookup"><span data-stu-id="d438d-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="d438d-214">Модель</span><span class="sxs-lookup"><span data-stu-id="d438d-214">The model</span></span>
<span data-ttu-id="d438d-215">Модель схемы очень проста.</span><span class="sxs-lookup"><span data-stu-id="d438d-215">The schema model is very basic.</span></span> <span data-ttu-id="d438d-216">При необходимости ее можно расширить.</span><span class="sxs-lookup"><span data-stu-id="d438d-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="d438d-217">Модель схемы имеет следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d438d-217">The schema model has these values:</span></span>

*   <span data-ttu-id="d438d-218">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="d438d-218">**NAME**.</span></span> <span data-ttu-id="d438d-219">Кому назначено это задание.</span><span class="sxs-lookup"><span data-stu-id="d438d-219">The person assigned to the task.</span></span> <span data-ttu-id="d438d-220">Это **строковое** значение.</span><span class="sxs-lookup"><span data-stu-id="d438d-220">This is a **string** value.</span></span>
*   <span data-ttu-id="d438d-221">**Задача**.</span><span class="sxs-lookup"><span data-stu-id="d438d-221">**TASK**.</span></span> <span data-ttu-id="d438d-222">Имя задачи.</span><span class="sxs-lookup"><span data-stu-id="d438d-222">The name of the task.</span></span> <span data-ttu-id="d438d-223">Это **строковое** значение.</span><span class="sxs-lookup"><span data-stu-id="d438d-223">This is a **string** value.</span></span>
*   <span data-ttu-id="d438d-224">**Дата**.</span><span class="sxs-lookup"><span data-stu-id="d438d-224">**DATE**.</span></span> <span data-ttu-id="d438d-225">Дата ожидаемого выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="d438d-225">The date that the task is due.</span></span> <span data-ttu-id="d438d-226">Это значение **datetime**.</span><span class="sxs-lookup"><span data-stu-id="d438d-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="d438d-227">**Завершено**.</span><span class="sxs-lookup"><span data-stu-id="d438d-227">**COMPLETED**.</span></span> <span data-ttu-id="d438d-228">Статус завершения задачи.</span><span class="sxs-lookup"><span data-stu-id="d438d-228">Whether the task is completed.</span></span> <span data-ttu-id="d438d-229">Это **логическое** значение.</span><span class="sxs-lookup"><span data-stu-id="d438d-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="d438d-230">Создание схемы в коде</span><span class="sxs-lookup"><span data-stu-id="d438d-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="d438d-231">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="d438d-232">В редакторе откройте файл Server.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-232">In your editor, open Server.js.</span></span> <span data-ttu-id="d438d-233">Под записью конфигурации добавьте следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="d438d-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="d438d-234">Этот код подключается к серверу MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d438d-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="d438d-235">Он также возвращает объект схемы.</span><span class="sxs-lookup"><span data-stu-id="d438d-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="d438d-236">С помощью схемы создайте модель в коде</span><span class="sxs-lookup"><span data-stu-id="d438d-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="d438d-237">После предыдущего кода добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="d438d-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="d438d-238">Как видно из кода, сначала вы создаете схему данных.</span><span class="sxs-lookup"><span data-stu-id="d438d-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="d438d-239">Затем создайте объект модели.</span><span class="sxs-lookup"><span data-stu-id="d438d-239">Next, you create a model object.</span></span> <span data-ttu-id="d438d-240">Используйте объект модели для хранения данных в коде при определении **маршрутов**.</span><span class="sxs-lookup"><span data-stu-id="d438d-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="d438d-241">Шаг 13. Добавление маршрутов для сервера REST API задачи</span><span class="sxs-lookup"><span data-stu-id="d438d-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="d438d-242">Теперь модель базы данных готова к использованию. Добавьте маршруты, которые будут использоваться для сервера REST API.</span><span class="sxs-lookup"><span data-stu-id="d438d-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="d438d-243">О маршрутах в Restify</span><span class="sxs-lookup"><span data-stu-id="d438d-243">About routes in restify</span></span>
<span data-ttu-id="d438d-244">Маршруты в Restify действуют точно так же, как и при использовании стека Express.</span><span class="sxs-lookup"><span data-stu-id="d438d-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="d438d-245">Вы определяете маршруты с помощью идентификатора URI, который, как предполагается, будут вызывать клиентские приложения.</span><span class="sxs-lookup"><span data-stu-id="d438d-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="d438d-246">Как правило, свои маршруты вы определяете в отдельном файле.</span><span class="sxs-lookup"><span data-stu-id="d438d-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="d438d-247">В этом руководстве мы помещаем маршруты в файл Server.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="d438d-248">Для систем в рабочей среде мы рекомендуем вынести их в отдельный файл.</span><span class="sxs-lookup"><span data-stu-id="d438d-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="d438d-249">Типичный шаблон для маршрута Restify выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d438d-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="d438d-250">Это шаблон на самом базовом уровне.</span><span class="sxs-lookup"><span data-stu-id="d438d-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="d438d-251">В Restify (как и в Express) доступны очень мощные функциональные возможности, например для определения типов приложений и выполнения сложной маршрутизации между несколькими конечными точками.</span><span class="sxs-lookup"><span data-stu-id="d438d-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="d438d-252">Добавление на сервер маршрутов по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d438d-252">Add default routes to your server</span></span>
<span data-ttu-id="d438d-253">Добавьте маршруты для базовых операций CRUD (**создание**, **извлечение**, **обновление** и **удаление** данных).</span><span class="sxs-lookup"><span data-stu-id="d438d-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="d438d-254">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="d438d-255">В редакторе откройте файл Server.js.</span><span class="sxs-lookup"><span data-stu-id="d438d-255">In an editor, open Server.js.</span></span> <span data-ttu-id="d438d-256">Добавьте следующие сведения под записями о базе данных, которые вы добавили ранее:</span><span class="sxs-lookup"><span data-stu-id="d438d-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable to save');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable to delete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in the database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="d438d-257">Добавление обработки ошибок для маршрутов</span><span class="sxs-lookup"><span data-stu-id="d438d-257">Add error handling for the routes</span></span>
<span data-ttu-id="d438d-258">Добавьте процедуру для обработки ошибок, чтобы сообщать клиенту о возникающих проблемах.</span><span class="sxs-lookup"><span data-stu-id="d438d-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="d438d-259">Добавьте следующий код после кода, который вы уже написали:</span><span class="sxs-lookup"><span data-stu-id="d438d-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a><span data-ttu-id="d438d-260">Шаг 14. Создание сервера</span><span class="sxs-lookup"><span data-stu-id="d438d-260">14: Create your server</span></span>
<span data-ttu-id="d438d-261">Осталось только добавить экземпляр сервера.</span><span class="sxs-lookup"><span data-stu-id="d438d-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="d438d-262">Экземпляр сервера управляет вызовами.</span><span class="sxs-lookup"><span data-stu-id="d438d-262">The server instance manages your calls.</span></span>

<span data-ttu-id="d438d-263">Restify (и Express) предлагают эффективные возможности настройки, которые можно использовать на сервере REST API.</span><span class="sxs-lookup"><span data-stu-id="d438d-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="d438d-264">В этом руководстве используется базовая процедура настройки.</span><span class="sxs-lookup"><span data-stu-id="d438d-264">In this tutorial, we use the most basic setup.</span></span>

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst to 10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="d438d-265">Шаг 15. Добавление маршрутов (в настоящее время без аутентификации)</span><span class="sxs-lookup"><span data-stu-id="d438d-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="d438d-266">Шаг 16. Запуск сервера</span><span class="sxs-lookup"><span data-stu-id="d438d-266">16: Run the server</span></span>
<span data-ttu-id="d438d-267">Перед добавлением функции проверки подлинности рекомендуется проверить сервер.</span><span class="sxs-lookup"><span data-stu-id="d438d-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="d438d-268">Проще всего это сделать с помощью curl из командной строки.</span><span class="sxs-lookup"><span data-stu-id="d438d-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="d438d-269">Для этого требуется простая служебная программа, которую можно использовать для анализа выходных данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="d438d-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="d438d-270">Установите средство JSON, которое используется в следующих примерах:</span><span class="sxs-lookup"><span data-stu-id="d438d-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="d438d-271">Это обеспечивает глобальную установку средства JSON.</span><span class="sxs-lookup"><span data-stu-id="d438d-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="d438d-272">Убедитесь, что ваш экземпляр MongoDB работает.</span><span class="sxs-lookup"><span data-stu-id="d438d-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="d438d-273">Измените каталог на **azuread** и запустите curl:</span><span class="sxs-lookup"><span data-stu-id="d438d-273">Change the directory to **azuread**, and then run curl:</span></span>

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  <span data-ttu-id="d438d-274">Добавьте задачу:</span><span class="sxs-lookup"><span data-stu-id="d438d-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="d438d-275">Ответ должен быть следующим:</span><span class="sxs-lookup"><span data-stu-id="d438d-275">The response should be:</span></span>

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  <span data-ttu-id="d438d-276">Перечисление задач для Brandon:</span><span class="sxs-lookup"><span data-stu-id="d438d-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="d438d-277">Если все эти команды выполняются без ошибок, можно приступать к добавлению OAuth на сервер REST API.</span><span class="sxs-lookup"><span data-stu-id="d438d-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="d438d-278">*Теперь у вас есть сервер REST API с MongoDB!*</span><span class="sxs-lookup"><span data-stu-id="d438d-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="d438d-279">Шаг 17. Добавление функции проверки подлинности на сервер REST API</span><span class="sxs-lookup"><span data-stu-id="d438d-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="d438d-280">Теперь, когда у вас есть работающий REST API, настройте его для использования с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d438d-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="d438d-281">В командной строке смените каталог на **azuread**.</span><span class="sxs-lookup"><span data-stu-id="d438d-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="d438d-282">Использование стратегии OIDCBearerStrategy, включенной в passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="d438d-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="d438d-283">На данный момент вы создали стандартный сервер REST TODO без какой-либо авторизации.</span><span class="sxs-lookup"><span data-stu-id="d438d-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="d438d-284">Теперь добавьте проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="d438d-284">Now, add authentication.</span></span>

<span data-ttu-id="d438d-285">Сначала укажите, что вы хотите использовать Passport.</span><span class="sxs-lookup"><span data-stu-id="d438d-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="d438d-286">Сделайте это сразу после конфигурации сервера.</span><span class="sxs-lookup"><span data-stu-id="d438d-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="d438d-287">При написании интерфейсов API рекомендуется всегда связывать данные с уникальными параметрами маркера, которые пользователь не сможет подделать.</span><span class="sxs-lookup"><span data-stu-id="d438d-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="d438d-288">Когда сервер сохраняет элементы списка дел (TODO), он делает это на основании идентификатора подписки пользователя в маркере (вызываемого с помощью token.sub).</span><span class="sxs-lookup"><span data-stu-id="d438d-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="d438d-289">token.sub указывается в поле owner (владелец).</span><span class="sxs-lookup"><span data-stu-id="d438d-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="d438d-290">Благодаря этому только владелец сможет получить доступ к своим элементам списка дел (TODO).</span><span class="sxs-lookup"><span data-stu-id="d438d-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="d438d-291">Никто другой не может получить доступ к элементам списка дел (TODO), которые были введены.</span><span class="sxs-lookup"><span data-stu-id="d438d-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="d438d-292">В API владелец не раскрывается.</span><span class="sxs-lookup"><span data-stu-id="d438d-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="d438d-293">Внешний пользователь может запросить элементы списка дел (TODO) других пользователей, даже если они прошли проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="d438d-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="d438d-294">Теперь используйте стратегию Open ID Connect Bearer, включенную в состав `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="d438d-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="d438d-295">Вставьте это после добавленного ранее:</span><span class="sxs-lookup"><span data-stu-id="d438d-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying the user');
log.info(token, 'was the token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="d438d-296">Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.).</span><span class="sxs-lookup"><span data-stu-id="d438d-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="d438d-297">Все авторы стратегии придерживаются этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="d438d-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="d438d-298">Передайте стратегию `function()`, которая использует маркер и значение `done` в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="d438d-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="d438d-299">Стратегия возвращается после того, как выполнит всю свою работу.</span><span class="sxs-lookup"><span data-stu-id="d438d-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="d438d-300">Сохраните данные пользователя и маркер, чтобы не задавать их в следующий раз повторно.</span><span class="sxs-lookup"><span data-stu-id="d438d-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d438d-301">Приведенный выше код принимает любого пользователя, который может пройти проверку подлинности на сервере.</span><span class="sxs-lookup"><span data-stu-id="d438d-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="d438d-302">Это называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="d438d-302">This is known as auto-registration.</span></span> <span data-ttu-id="d438d-303">На рабочих серверах не нужно разрешать другим пользователям входить без выбранной вами регистрации.</span><span class="sxs-lookup"><span data-stu-id="d438d-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="d438d-304">Это обычное поведение в приложениях для потребителей.</span><span class="sxs-lookup"><span data-stu-id="d438d-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="d438d-305">Приложение можно зарегистрировать в Facebook, но потребуется ввести дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="d438d-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="d438d-306">Если в этом руководстве вы не использовали программу командной строки, сообщение электронной почты можно извлечь из возвращаемого объекта маркера.</span><span class="sxs-lookup"><span data-stu-id="d438d-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="d438d-307">Затем вы можете попросить пользователя ввести дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="d438d-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="d438d-308">Так как это всего лишь тестовый сервер, просто добавьте пользователей в базу данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="d438d-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="d438d-309">Защита конечных точек</span><span class="sxs-lookup"><span data-stu-id="d438d-309">Protect endpoints</span></span>
<span data-ttu-id="d438d-310">Для защиты конечных точек необходимо указать вызов **passport.authenticate()** с протоколом, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="d438d-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="d438d-311">Вы можете изменить маршрут в коде сервера для более продвинутого использования:</span><span class="sxs-lookup"><span data-stu-id="d438d-311">You can edit your route in your server code for a more advanced option:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="d438d-312">Шаг 18. Повторный запуск серверного приложения</span><span class="sxs-lookup"><span data-stu-id="d438d-312">18: Run your server application again</span></span>
<span data-ttu-id="d438d-313">Снова воспользуйтесь curl, чтобы определить, активирована ли защита OAuth 2.0 применительно к конечным точкам.</span><span class="sxs-lookup"><span data-stu-id="d438d-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="d438d-314">Сделайте это до запуска любого клиентского пакета SDK для этой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d438d-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="d438d-315">Возвращаемые заголовки должны содержать сведения о правильной работе функции проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d438d-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="d438d-316">Убедитесь, что ваш экземпляр MongoDB работает.</span><span class="sxs-lookup"><span data-stu-id="d438d-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="d438d-317">Измените каталог на **azuread**, а затем используйте curl:</span><span class="sxs-lookup"><span data-stu-id="d438d-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="d438d-318">Попробуйте выполнить базовую команду POST:</span><span class="sxs-lookup"><span data-stu-id="d438d-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="d438d-319">Ответ 401 указывает, что уровень Passport пытается перенаправить нас к конечной точке авторизации. Это именно то, что нам нужно.</span><span class="sxs-lookup"><span data-stu-id="d438d-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="d438d-320">*Теперь у вас есть служба REST API, использующая OAuth 2.0!*</span><span class="sxs-lookup"><span data-stu-id="d438d-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="d438d-321">Вы уже сделали с этим сервером все, что можно реализовать без использования клиента, совместимого с OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d438d-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="d438d-322">Для работы с клиентом необходимо изучить дополнительное руководство.</span><span class="sxs-lookup"><span data-stu-id="d438d-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d438d-323">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d438d-323">Next steps</span></span>
<span data-ttu-id="d438d-324">Полный пример (без ваших значений конфигурации) можно загрузить в виде [ZIP-архива](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d438d-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="d438d-325">Кроме того, его можно клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="d438d-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="d438d-326">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="d438d-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="d438d-327">Вы можете попытаться [защитить веб-приложение Node.js с помощью конечной точки версии 2.0](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="d438d-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="d438d-328">Ниже приведены некоторые дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d438d-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="d438d-329">Вход для пользователей учетных записей Майкрософт и Azure AD в одном приложении</span><span class="sxs-lookup"><span data-stu-id="d438d-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="d438d-330">Тег StackOverflow "azure-active-directory"</span><span class="sxs-lookup"><span data-stu-id="d438d-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="d438d-331">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="d438d-331">Get security updates for our products</span></span>
<span data-ttu-id="d438d-332">Мы рекомендуем вам зарегистрироваться для получения уведомлений о нарушениях безопасности.</span><span class="sxs-lookup"><span data-stu-id="d438d-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="d438d-333">Это можно сделать, подписавшись на уведомления безопасности консультационных служб на странице [технического центра безопасности](https://technet.microsoft.com/security/dd252948).</span><span class="sxs-lookup"><span data-stu-id="d438d-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

