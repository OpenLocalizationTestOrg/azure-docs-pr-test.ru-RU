---
title: "aaaSecure веб-API Azure Active Directory версии 2.0 с помощью Node.js | Документы Microsoft"
description: "Узнайте, как toobuild Node.js веб-API, который принимает токены из личную учетную запись Майкрософт и рабочих или учебных учетных записей."
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
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="740bd-103">Защита веб-API с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="740bd-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="740bd-104">Не все сценарии Azure Active Directory и возможности работы с конечной точкой v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="740bd-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="740bd-105">toodetermine необходимость использования hello v2.0 конечная точка либо hello v1.0, узнайте, как [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="740bd-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="740bd-106">При использовании endpoint v2.0 hello Azure Active Directory (Azure AD), можно использовать [OAuth 2.0](active-directory-v2-protocols.md) маркеры доступа tooprotect веб-API.</span><span class="sxs-lookup"><span data-stu-id="740bd-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="740bd-107">С помощью маркеров доступа OAuth 2.0 пользователи с личными учетными записями Майкрософт и рабочими или учебными учетными записями могут безопасно обращаться в вашему веб-API.</span><span class="sxs-lookup"><span data-stu-id="740bd-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="740bd-108">*Passport* — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="740bd-109">Он отличается гибкой модульной структурой, которая позволяет сравнительно незаметно размещать его в любом приложении на основе Express или веб-приложении Restify.</span><span class="sxs-lookup"><span data-stu-id="740bd-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="740bd-110">В Passport полный набор стратегий поддерживает процесс проверки подлинности с помощью имени пользователя и пароля, Facebook, Twitter и проч.</span><span class="sxs-lookup"><span data-stu-id="740bd-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="740bd-111">Мы разработали стратегию для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="740bd-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="740bd-112">В этой статье рассказывается как tooinstall hello модуля, а затем добавьте hello Azure AD `passport-azure-ad` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="740bd-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="740bd-113">Загрузить</span><span class="sxs-lookup"><span data-stu-id="740bd-113">Download</span></span>
<span data-ttu-id="740bd-114">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="740bd-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="740bd-115">toofollow hello учебник, вы можете [загрузить приложение hello основу как ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), или основу hello клона:</span><span class="sxs-lookup"><span data-stu-id="740bd-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="740bd-116">Можно также получить приложение hello завершено в конце hello этого учебника.</span><span class="sxs-lookup"><span data-stu-id="740bd-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="740bd-117">Шаг 1. Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="740bd-117">1: Register an app</span></span>
<span data-ttu-id="740bd-118">Создайте новое приложение на [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните [эти подробные шаги](active-directory-v2-app-registration.md) tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="740bd-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="740bd-119">Не забудьте выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="740bd-119">Make sure you:</span></span>

* <span data-ttu-id="740bd-120">Копировать hello **идентификатор приложения** назначенный tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="740bd-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="740bd-121">Он потребуется для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="740bd-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="740bd-122">Добавить hello **Mobile** платформы для приложения.</span><span class="sxs-lookup"><span data-stu-id="740bd-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="740bd-123">Копировать hello **URI перенаправления** из портала hello.</span><span class="sxs-lookup"><span data-stu-id="740bd-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="740bd-124">Необходимо использовать значение по умолчанию URI hello `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="740bd-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="740bd-125">Шаг 2. Установка Node.js</span><span class="sxs-lookup"><span data-stu-id="740bd-125">2: Install Node.js</span></span>
<span data-ttu-id="740bd-126">Образец hello toouse для этого учебника, необходимо [установки Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="740bd-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="740bd-127">Шаг 3. Установка MongoDB</span><span class="sxs-lookup"><span data-stu-id="740bd-127">3: Install MongoDB</span></span>
<span data-ttu-id="740bd-128">toosuccessfully использование этого образца, необходимо [установить MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="740bd-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="740bd-129">В этом образце используется MongoDB toomake постоянные REST API по экземплярам сервера.</span><span class="sxs-lookup"><span data-stu-id="740bd-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="740bd-130">В этой статье предполагается, что конечные точки установки и сервером по умолчанию hello используется для MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="740bd-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="740bd-131">4: install hello restify модулей в веб-API</span><span class="sxs-lookup"><span data-stu-id="740bd-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="740bd-132">Мы используем Resitfy toobuild нашем API REST.</span><span class="sxs-lookup"><span data-stu-id="740bd-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="740bd-133">Restify — это минималистичная и гибкая платформа для приложений Node.j, созданная на основе Express.</span><span class="sxs-lookup"><span data-stu-id="740bd-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="740bd-134">Restify имеет широкий набор функций, которые можно использовать API-интерфейс REST на основе Connect toobuild.</span><span class="sxs-lookup"><span data-stu-id="740bd-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="740bd-135">Установка Restify</span><span class="sxs-lookup"><span data-stu-id="740bd-135">Install restify</span></span>
1.  <span data-ttu-id="740bd-136">В командной строке измените каталог hello слишком**azuread**:</span><span class="sxs-lookup"><span data-stu-id="740bd-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="740bd-137">Если hello **azuread** каталог не существует, создайте его:</span><span class="sxs-lookup"><span data-stu-id="740bd-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="740bd-138">Установите Restify.</span><span class="sxs-lookup"><span data-stu-id="740bd-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="740bd-139">Hello выходные данные этой команды должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="740bd-139">hello output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="740bd-140">Вы получили сообщение об ошибке?</span><span class="sxs-lookup"><span data-stu-id="740bd-140">Did you get an error?</span></span>
<span data-ttu-id="740bd-141">В некоторых операционных системах при использовании hello `npm` команда, может появиться это сообщение: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="740bd-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="740bd-142">Ошибка Hello сопровождается запроса, попробуйте выполнить выполняющейся hello учетной записи с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="740bd-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="740bd-143">В этом случае команда hello `sudo` toorun `npm` на более высоком уровне привилегий.</span><span class="sxs-lookup"><span data-stu-id="740bd-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="740bd-144">Было возникнет ошибка, связанная tooDTrace?</span><span class="sxs-lookup"><span data-stu-id="740bd-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="740bd-145">При установке Restify может появиться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="740bd-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="740bd-146">Restify имеет tootrace мощный механизм, с помощью DTrace вызовы REST.</span><span class="sxs-lookup"><span data-stu-id="740bd-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="740bd-147">Однако во многих операционных системах DTrace отсутствует.</span><span class="sxs-lookup"><span data-stu-id="740bd-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="740bd-148">Это сообщение об ошибке можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="740bd-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="740bd-149">Шаг 5. Установка Passport.js для веб-интерфейса API</span><span class="sxs-lookup"><span data-stu-id="740bd-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="740bd-150">В командной строке hello изменить каталог hello слишком**azuread**.</span><span class="sxs-lookup"><span data-stu-id="740bd-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="740bd-151">Установите Passport.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="740bd-152">Hello выходные данные команды hello должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="740bd-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="740bd-153">6: Добавление веб-API tooyour passport azure ad</span><span class="sxs-lookup"><span data-stu-id="740bd-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="740bd-154">Добавьте hello OAuth стратегии, с помощью passport azuread.</span><span class="sxs-lookup"><span data-stu-id="740bd-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="740bd-155">`passport-azuread` — это набор стратегий, который устанавливает подключение Azure AD к Passport.</span><span class="sxs-lookup"><span data-stu-id="740bd-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="740bd-156">В этом примере REST API мы будем использовать эту стратегию для токенов носителя.</span><span class="sxs-lookup"><span data-stu-id="740bd-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="740bd-157">Платформа OAuth 2.0 позволяет выдавать маркеры любого известного типа, но в большинстве случаев используются маркеры только нескольких типов.</span><span class="sxs-lookup"><span data-stu-id="740bd-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="740bd-158">Токены носителя, часто используемые tooprotect конечных точек.</span><span class="sxs-lookup"><span data-stu-id="740bd-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="740bd-159">Токены носителя — тип hello наиболее широко выданного маркера в OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="740bd-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="740bd-160">Многие реализации OAuth 2.0 предполагают, что токены носителя являются единственным типом маркера, выданного hello.</span><span class="sxs-lookup"><span data-stu-id="740bd-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="740bd-161">В командной строке измените каталог hello слишком**azuread**.</span><span class="sxs-lookup"><span data-stu-id="740bd-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="740bd-162">Установка hello Passport.js `passport-azure-ad` модуля:</span><span class="sxs-lookup"><span data-stu-id="740bd-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="740bd-163">Hello выходные данные команды hello должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="740bd-163">hello output of hello command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="740bd-164">7: Добавление MongoDB модули tooyour веб-API</span><span class="sxs-lookup"><span data-stu-id="740bd-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="740bd-165">В этом примере мы используем MongoDB в качестве хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="740bd-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="740bd-166">Установить Mongoose, широко используемый подключаемый модуль, toomanage моделей и схем:</span><span class="sxs-lookup"><span data-stu-id="740bd-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="740bd-167">Установите hello драйвер базы данных MongoDB, которая также называется MongoDB.</span><span class="sxs-lookup"><span data-stu-id="740bd-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="740bd-168">Шаг 8. Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="740bd-168">8: Install additional modules</span></span>
<span data-ttu-id="740bd-169">Установите hello оставшихся необходимые модули.</span><span class="sxs-lookup"><span data-stu-id="740bd-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="740bd-170">В командной строке измените каталог hello слишком**azuread**:</span><span class="sxs-lookup"><span data-stu-id="740bd-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="740bd-171">Введите следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="740bd-171">Enter hello following commands.</span></span> <span data-ttu-id="740bd-172">Hello команды устанавливают следующие модули в папке node_modules hello:</span><span class="sxs-lookup"><span data-stu-id="740bd-172">hello commands install hello following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="740bd-173">Шаг 9. Создание файла Server.js для зависимостей</span><span class="sxs-lookup"><span data-stu-id="740bd-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="740bd-174">Файл Server.js содержит hello большую часть функций hello API веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="740bd-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="740bd-175">Добавьте большая часть файла с кодом toothis.</span><span class="sxs-lookup"><span data-stu-id="740bd-175">Add most of your code toothis file.</span></span> <span data-ttu-id="740bd-176">Для производственных целей рефакторинг функции hello разбиваются на меньшие файлы как для отдельных маршрутов и контроллеров.</span><span class="sxs-lookup"><span data-stu-id="740bd-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="740bd-177">В этой статье мы используем Server.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="740bd-178">В командной строке измените каталог hello слишком**azuread**:</span><span class="sxs-lookup"><span data-stu-id="740bd-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="740bd-179">С помощью редактора по своему усмотрению создайте файл server.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="740bd-180">Добавьте следующие сведения toohello файл hello:</span><span class="sxs-lookup"><span data-stu-id="740bd-180">Add hello following information toohello file:</span></span>

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

3.  <span data-ttu-id="740bd-181">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="740bd-181">Save hello file.</span></span> <span data-ttu-id="740bd-182">Скоро будет возвращать tooit.</span><span class="sxs-lookup"><span data-stu-id="740bd-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="740bd-183">10: создать файл конфигурации toostore параметры Azure AD</span><span class="sxs-lookup"><span data-stu-id="740bd-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="740bd-184">Этот файл код передает hello параметры конфигурации из вашего tooPassport.js портала Azure AD.</span><span class="sxs-lookup"><span data-stu-id="740bd-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="740bd-185">Эти значения конфигурации, созданный при добавлении API toohello hello веб-портала в начале статьи hello hello.</span><span class="sxs-lookup"><span data-stu-id="740bd-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="740bd-186">После копирования кода hello объясняется, какие tooput hello значениями этих параметров.</span><span class="sxs-lookup"><span data-stu-id="740bd-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="740bd-187">В командной строке измените каталог hello слишком**azuread**:</span><span class="sxs-lookup"><span data-stu-id="740bd-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="740bd-188">В редакторе создайте файл Config.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="740bd-189">Добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="740bd-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="740bd-190">Обязательные значения</span><span class="sxs-lookup"><span data-stu-id="740bd-190">Required values</span></span>

*   <span data-ttu-id="740bd-191">**IdentityMetadata**: это место, куда `passport-azure-ad` ищет данные конфигурации для hello поставщика удостоверений (IDP) и ключи toovalidate hello hello веб-маркеры JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="740bd-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="740bd-192">При использовании Azure AD, скорее всего, не следует toochange это.</span><span class="sxs-lookup"><span data-stu-id="740bd-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="740bd-193">**аудитория**: на URI перенаправления из портала hello.</span><span class="sxs-lookup"><span data-stu-id="740bd-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="740bd-194">Рекомендуется часто менять ключи.</span><span class="sxs-lookup"><span data-stu-id="740bd-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="740bd-195">Убедитесь, что всегда извлекаются из URL-адреса «openid_keys» hello, и приложение hello можно открыть hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="740bd-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="740bd-196">11: добавить файл Server.js tooyour конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="740bd-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="740bd-197">Приложению tooread hello значения из файла конфигурации hello, которую вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="740bd-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="740bd-198">Добавьте файл .config hello из требуемых ресурсов в приложении.</span><span class="sxs-lookup"><span data-stu-id="740bd-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="740bd-199">Задать toothose hello глобальные переменные, которые находятся в Config.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="740bd-200">В командной строке hello изменить каталог hello слишком**azuread**:</span><span class="sxs-lookup"><span data-stu-id="740bd-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="740bd-201">В редакторе откройте файл Server.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-201">In an editor, open Server.js.</span></span> <span data-ttu-id="740bd-202">Добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="740bd-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="740bd-203">Добавьте новый tooServer.js раздела:</span><span class="sxs-lookup"><span data-stu-id="740bd-203">Add a new section tooServer.js:</span></span>

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="740bd-204">12: Добавление hello MongoDB модели и данные схемы с помощью Mongoose</span><span class="sxs-lookup"><span data-stu-id="740bd-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="740bd-205">Затем подключите эти три файла в службе REST API.</span><span class="sxs-lookup"><span data-stu-id="740bd-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="740bd-206">В этой статье мы используем MongoDB toostore нашей задачи.</span><span class="sxs-lookup"><span data-stu-id="740bd-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="740bd-207">Этот вопрос обсуждается на *шаге 4*.</span><span class="sxs-lookup"><span data-stu-id="740bd-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="740bd-208">В файле Config.js hello, созданный на шаге 11, базы данных называется *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="740bd-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="740bd-209">Это было поместить в конце hello URL-адрес подключения mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="740bd-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="740bd-210">Не нужно toocreate базы данных, заранее в MongoDB.</span><span class="sxs-lookup"><span data-stu-id="740bd-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="740bd-211">Hello база данных создается на hello сначала выполнения приложения сервера (при условии, что hello базы данных еще не существует).</span><span class="sxs-lookup"><span data-stu-id="740bd-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="740bd-212">Hello server рассказали какие toouse базы данных MongoDB.</span><span class="sxs-lookup"><span data-stu-id="740bd-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="740bd-213">Далее необходимо toowrite некоторые модели hello toocreate дополнительного кода и схемы для вашего сервера задач.</span><span class="sxs-lookup"><span data-stu-id="740bd-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="740bd-214">модель Hello</span><span class="sxs-lookup"><span data-stu-id="740bd-214">hello model</span></span>
<span data-ttu-id="740bd-215">модель схемы Hello является очень простым.</span><span class="sxs-lookup"><span data-stu-id="740bd-215">hello schema model is very basic.</span></span> <span data-ttu-id="740bd-216">При необходимости ее можно расширить.</span><span class="sxs-lookup"><span data-stu-id="740bd-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="740bd-217">модель схемы Hello может принимать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="740bd-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="740bd-218">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="740bd-218">**NAME**.</span></span> <span data-ttu-id="740bd-219">Задача назначенного toohello Hello человека.</span><span class="sxs-lookup"><span data-stu-id="740bd-219">hello person assigned toohello task.</span></span> <span data-ttu-id="740bd-220">Это **строковое** значение.</span><span class="sxs-lookup"><span data-stu-id="740bd-220">This is a **string** value.</span></span>
*   <span data-ttu-id="740bd-221">**Задача**.</span><span class="sxs-lookup"><span data-stu-id="740bd-221">**TASK**.</span></span> <span data-ttu-id="740bd-222">Hello имя задачи «hello».</span><span class="sxs-lookup"><span data-stu-id="740bd-222">hello name of hello task.</span></span> <span data-ttu-id="740bd-223">Это **строковое** значение.</span><span class="sxs-lookup"><span data-stu-id="740bd-223">This is a **string** value.</span></span>
*   <span data-ttu-id="740bd-224">**Дата**.</span><span class="sxs-lookup"><span data-stu-id="740bd-224">**DATE**.</span></span> <span data-ttu-id="740bd-225">Hello Дата выполнения этой задачи hello.</span><span class="sxs-lookup"><span data-stu-id="740bd-225">hello date that hello task is due.</span></span> <span data-ttu-id="740bd-226">Это значение **datetime**.</span><span class="sxs-lookup"><span data-stu-id="740bd-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="740bd-227">**Завершено**.</span><span class="sxs-lookup"><span data-stu-id="740bd-227">**COMPLETED**.</span></span> <span data-ttu-id="740bd-228">Является ли hello задача завершена.</span><span class="sxs-lookup"><span data-stu-id="740bd-228">Whether hello task is completed.</span></span> <span data-ttu-id="740bd-229">Это **логическое** значение.</span><span class="sxs-lookup"><span data-stu-id="740bd-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="740bd-230">Создание схемы hello в коде hello</span><span class="sxs-lookup"><span data-stu-id="740bd-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="740bd-231">В командной строке измените каталог hello слишком**azuread**:</span><span class="sxs-lookup"><span data-stu-id="740bd-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="740bd-232">В редакторе откройте файл Server.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-232">In your editor, open Server.js.</span></span> <span data-ttu-id="740bd-233">Запись конфигурации hello добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="740bd-233">Below hello configuration entry, add hello following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="740bd-234">Он подключает toohello MongoDB сервера.</span><span class="sxs-lookup"><span data-stu-id="740bd-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="740bd-235">Он также возвращает объект схемы.</span><span class="sxs-lookup"><span data-stu-id="740bd-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="740bd-236">С помощью схемы hello, создайте модели в коде hello</span><span class="sxs-lookup"><span data-stu-id="740bd-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="740bd-237">Hello предшествующий код добавьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="740bd-237">Below hello preceding code, add hello following code:</span></span>

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="740bd-238">Как можно видеть из кода hello, сначала создать схему.</span><span class="sxs-lookup"><span data-stu-id="740bd-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="740bd-239">Затем создайте объект модели.</span><span class="sxs-lookup"><span data-stu-id="740bd-239">Next, you create a model object.</span></span> <span data-ttu-id="740bd-240">Используйте hello модели объекта toostore данных по всему hello кода при определении вашей **маршруты**.</span><span class="sxs-lookup"><span data-stu-id="740bd-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="740bd-241">Шаг 13. Добавление маршрутов для сервера REST API задачи</span><span class="sxs-lookup"><span data-stu-id="740bd-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="740bd-242">Теперь, когда toowork модели базы данных с добавьте hello маршруты, который будет использоваться для сервера API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="740bd-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="740bd-243">О маршрутах в Restify</span><span class="sxs-lookup"><span data-stu-id="740bd-243">About routes in restify</span></span>
<span data-ttu-id="740bd-244">Маршруты в restify рабочих точно hello так же, как при использовании hello стека, экспресс-выпуск.</span><span class="sxs-lookup"><span data-stu-id="740bd-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="740bd-245">Определения маршрутов с помощью hello URI, что предполагается toocall приложения hello клиента.</span><span class="sxs-lookup"><span data-stu-id="740bd-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="740bd-246">Как правило, свои маршруты вы определяете в отдельном файле.</span><span class="sxs-lookup"><span data-stu-id="740bd-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="740bd-247">В этом руководстве мы помещаем маршруты в файл Server.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="740bd-248">Для систем в рабочей среде мы рекомендуем вынести их в отдельный файл.</span><span class="sxs-lookup"><span data-stu-id="740bd-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="740bd-249">Типичный шаблон для маршрута Restify выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="740bd-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="740bd-250">Это шаблон hello на самом базовом уровне hello.</span><span class="sxs-lookup"><span data-stu-id="740bd-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="740bd-251">Restify (и Express) предоставляет гораздо более глубокую функциональные возможности, как типы приложений toodefine возможность hello и сложные маршрутизации между разными конечными точками.</span><span class="sxs-lookup"><span data-stu-id="740bd-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="740bd-252">Добавление сервера tooyour маршруты по умолчанию</span><span class="sxs-lookup"><span data-stu-id="740bd-252">Add default routes tooyour server</span></span>
<span data-ttu-id="740bd-253">Добавить базовый CRUD маршруты hello: **создания**, **получить**, **обновление**, и **удалить**.</span><span class="sxs-lookup"><span data-stu-id="740bd-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="740bd-254">В командной строке измените каталог hello слишком**azuread**:</span><span class="sxs-lookup"><span data-stu-id="740bd-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="740bd-255">В редакторе откройте файл Server.js.</span><span class="sxs-lookup"><span data-stu-id="740bd-255">In an editor, open Server.js.</span></span> <span data-ttu-id="740bd-256">Ниже записи в базе данных hello ранее сделанные, добавить hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="740bd-256">Below hello database entries you made earlier, add hello following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
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
    req.log.warn(err, 'createTask: unable toosave');
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
    'removeTask: unable toodelete %s',
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
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
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
    log.warn(err, "There are no tasks in hello database. Add one!");
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

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="740bd-257">Добавьте обработку ошибок для маршрутов hello</span><span class="sxs-lookup"><span data-stu-id="740bd-257">Add error handling for hello routes</span></span>
<span data-ttu-id="740bd-258">Добавьте некоторые обработку ошибок, могут взаимодействовать задней toohello клиента о проблеме hello, которыми вы столкнулись.</span><span class="sxs-lookup"><span data-stu-id="740bd-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="740bd-259">Добавьте следующий код ниже кода hello, который уже написаны hello:</span><span class="sxs-lookup"><span data-stu-id="740bd-259">Add hello following code below hello code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back toohello client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="740bd-260">Шаг 14. Создание сервера</span><span class="sxs-lookup"><span data-stu-id="740bd-260">14: Create your server</span></span>
<span data-ttu-id="740bd-261">Здравствуйте последнего самое toodo является tooadd свой экземпляр сервера.</span><span class="sxs-lookup"><span data-stu-id="740bd-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="740bd-262">экземпляр сервера Hello управляет вызовов.</span><span class="sxs-lookup"><span data-stu-id="740bd-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="740bd-263">Restify (и Express) предлагают эффективные возможности настройки, которые можно использовать на сервере REST API.</span><span class="sxs-lookup"><span data-stu-id="740bd-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="740bd-264">В этом учебнике мы используем hello наиболее базовой установки.</span><span class="sxs-lookup"><span data-stu-id="740bd-264">In this tutorial, we use hello most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst too10.
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
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="740bd-265">15: добавить маршруты hello (без проверки подлинности, сейчас)</span><span class="sxs-lookup"><span data-stu-id="740bd-265">15: Add hello routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
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
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a><span data-ttu-id="740bd-266">16: запускать сервер hello</span><span class="sxs-lookup"><span data-stu-id="740bd-266">16: Run hello server</span></span>
<span data-ttu-id="740bd-267">Это tootest рекомендуется перед добавлением проверки подлинности сервера.</span><span class="sxs-lookup"><span data-stu-id="740bd-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="740bd-268">Самый простой способ tootest Hello сервера — с помощью перелистывание в командной строке.</span><span class="sxs-lookup"><span data-stu-id="740bd-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="740bd-269">toodo, требуется простой программы, можно использовать tooparse результаты как JSON.</span><span class="sxs-lookup"><span data-stu-id="740bd-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="740bd-270">Установите средство JSON hello, мы используем hello следующие примеры:</span><span class="sxs-lookup"><span data-stu-id="740bd-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="740bd-271">При этом устанавливаются средства JSON hello глобально.</span><span class="sxs-lookup"><span data-stu-id="740bd-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="740bd-272">Убедитесь, что ваш экземпляр MongoDB работает.</span><span class="sxs-lookup"><span data-stu-id="740bd-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="740bd-273">Измените каталог hello слишком**azuread**, а затем запустите перелистывание:</span><span class="sxs-lookup"><span data-stu-id="740bd-273">Change hello directory too**azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="740bd-274">tooadd задачи:</span><span class="sxs-lookup"><span data-stu-id="740bd-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="740bd-275">Hello ответа должно быть:</span><span class="sxs-lookup"><span data-stu-id="740bd-275">hello response should be:</span></span>

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

5.  <span data-ttu-id="740bd-276">Перечисление задач для Brandon:</span><span class="sxs-lookup"><span data-stu-id="740bd-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="740bd-277">Если все эти команды выполняются без ошибок, не требуется сервер готов tooadd OAuth toohello REST API.</span><span class="sxs-lookup"><span data-stu-id="740bd-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="740bd-278">*Теперь у вас есть сервер REST API с MongoDB!*</span><span class="sxs-lookup"><span data-stu-id="740bd-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="740bd-279">17: Добавление сервера API-интерфейса REST tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="740bd-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="740bd-280">Теперь, когда выполнение API REST, он настраивается toouse его с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="740bd-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="740bd-281">В командной строке измените каталог hello слишком**azuread**:</span><span class="sxs-lookup"><span data-stu-id="740bd-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="740bd-282">Использовать oidcbearerstrategy hello, предоставляемую с passport azure ad</span><span class="sxs-lookup"><span data-stu-id="740bd-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="740bd-283">На данный момент вы создали стандартный сервер REST TODO без какой-либо авторизации.</span><span class="sxs-lookup"><span data-stu-id="740bd-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="740bd-284">Теперь добавьте проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="740bd-284">Now, add authentication.</span></span>

<span data-ttu-id="740bd-285">Во-первых требуется укажите toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="740bd-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="740bd-286">Сделайте это сразу после конфигурации сервера.</span><span class="sxs-lookup"><span data-stu-id="740bd-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="740bd-287">При написании API-интерфейсы, это toosomething данных отличается от маркера hello, hello пользователя подменить приветствия ссылку tooalways рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="740bd-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="740bd-288">Когда этот сервер сохраняет элементы TODO, она сохраняет их на основе идентификатора подписки пользователя hello в маркере hello (называемые через token.sub).</span><span class="sxs-lookup"><span data-stu-id="740bd-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="740bd-289">В поле «владелец» hello, поместите hello token.sub.</span><span class="sxs-lookup"><span data-stu-id="740bd-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="740bd-290">Это гарантирует доступность TODOs hello пользователя только данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="740bd-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="740bd-291">Никто не может получить доступ к TODOs hello, которые были введены.</span><span class="sxs-lookup"><span data-stu-id="740bd-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="740bd-292">Нет отсутствие проблем в hello API для «владелец».</span><span class="sxs-lookup"><span data-stu-id="740bd-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="740bd-293">Внешний пользователь может запросить элементы списка дел (TODO) других пользователей, даже если они прошли проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="740bd-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="740bd-294">Затем с помощью стратегии носителя подключения откройте Идентификатором hello, входящий в состав `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="740bd-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="740bd-295">Вставьте это после добавленного ранее:</span><span class="sxs-lookup"><span data-stu-id="740bd-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
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
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
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

<span data-ttu-id="740bd-296">Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.).</span><span class="sxs-lookup"><span data-stu-id="740bd-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="740bd-297">Все записи стратегии придерживаться toohello шаблон.</span><span class="sxs-lookup"><span data-stu-id="740bd-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="740bd-298">Передайте hello стратегии `function()` , использует токен и `done` в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="740bd-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="740bd-299">Стратегия Hello возвращается после его свою работу.</span><span class="sxs-lookup"><span data-stu-id="740bd-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="740bd-300">Пользователь hello хранилища и образа hello маркер tooask для него требуется еще раз.</span><span class="sxs-lookup"><span data-stu-id="740bd-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="740bd-301">Hello выше код принимает любой пользователь, который может проверить подлинность сервера tooyour.</span><span class="sxs-lookup"><span data-stu-id="740bd-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="740bd-302">Это называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="740bd-302">This is known as auto-registration.</span></span> <span data-ttu-id="740bd-303">На рабочем сервере не стоит toolet любой пользователь без необходимости их пройти процесс регистрации, выборе.</span><span class="sxs-lookup"><span data-stu-id="740bd-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="740bd-304">Обычно это является шаблон hello в потребительские приложения.</span><span class="sxs-lookup"><span data-stu-id="740bd-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="740bd-305">приложение Hello может разрешить tooregister с Facebook, но затем вас просят tooenter дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="740bd-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="740bd-306">Если с помощью программы командной строки не были в этом учебнике, можно извлечь из hello объекта маркера, который возвращается hello электронной почты.</span><span class="sxs-lookup"><span data-stu-id="740bd-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="740bd-307">Затем задайте себе вопрос: hello пользователя tooenter Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="740bd-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="740bd-308">Так как на тестовом сервере, можно добавить пользователя hello непосредственно toohello в памяти базы данных.</span><span class="sxs-lookup"><span data-stu-id="740bd-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="740bd-309">Защита конечных точек</span><span class="sxs-lookup"><span data-stu-id="740bd-309">Protect endpoints</span></span>
<span data-ttu-id="740bd-310">Защита конечных точек, указав hello **passport.authenticate()** вызов с протоколом hello, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="740bd-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="740bd-311">Вы можете изменить маршрут в коде сервера для более продвинутого использования:</span><span class="sxs-lookup"><span data-stu-id="740bd-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="740bd-312">Шаг 18. Повторный запуск серверного приложения</span><span class="sxs-lookup"><span data-stu-id="740bd-312">18: Run your server application again</span></span>
<span data-ttu-id="740bd-313">Используйте curl снова toosee при наличии защиты OAuth 2.0 для конечных точек.</span><span class="sxs-lookup"><span data-stu-id="740bd-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="740bd-314">Сделайте это до запуска любого клиентского пакета SDK для этой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="740bd-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="740bd-315">заголовки Hello вернул должен сообщить, правильно ли работает проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="740bd-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="740bd-316">Убедитесь, что ваш экземпляр MongoDB работает.</span><span class="sxs-lookup"><span data-stu-id="740bd-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="740bd-317">Изменить toohello **azuread** каталога, а затем используйте curl:</span><span class="sxs-lookup"><span data-stu-id="740bd-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="740bd-318">Попробуйте выполнить базовую команду POST:</span><span class="sxs-lookup"><span data-stu-id="740bd-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="740bd-319">Ответ 401 указывает уровень Passport hello пытается tooredirect toohello конечную точку авторизации, что именно вы хотите.</span><span class="sxs-lookup"><span data-stu-id="740bd-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="740bd-320">*Теперь у вас есть служба REST API, использующая OAuth 2.0!*</span><span class="sxs-lookup"><span data-stu-id="740bd-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="740bd-321">Вы уже сделали с этим сервером все, что можно реализовать без использования клиента, совместимого с OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="740bd-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="740bd-322">Для этого потребуется tooreview дополнительных учебника.</span><span class="sxs-lookup"><span data-stu-id="740bd-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="740bd-323">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="740bd-323">Next steps</span></span>
<span data-ttu-id="740bd-324">Справочник по образец hello завершена (без настройки) предоставляется как [ZIP-файл](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="740bd-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="740bd-325">Кроме того, его можно клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="740bd-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="740bd-326">Теперь можно переместить на toomore дополнительные разделы.</span><span class="sxs-lookup"><span data-stu-id="740bd-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="740bd-327">Может потребоваться tootry [защитить веб-приложение Node.js с помощью конечной точки v2.0 hello](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="740bd-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="740bd-328">Ниже приведены некоторые дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="740bd-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="740bd-329">Вход для пользователей учетных записей Майкрософт и Azure AD в одном приложении</span><span class="sxs-lookup"><span data-stu-id="740bd-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="740bd-330">Тег StackOverflow "azure-active-directory"</span><span class="sxs-lookup"><span data-stu-id="740bd-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="740bd-331">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="740bd-331">Get security updates for our products</span></span>
<span data-ttu-id="740bd-332">Мы рекомендуем toosign копирование toobe уведомлений при внесении угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="740bd-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="740bd-333">На hello [выпуске](https://technet.microsoft.com/security/dd252948) страницы, подписаться на оповещения tooSecurity рекомендации.</span><span class="sxs-lookup"><span data-stu-id="740bd-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

