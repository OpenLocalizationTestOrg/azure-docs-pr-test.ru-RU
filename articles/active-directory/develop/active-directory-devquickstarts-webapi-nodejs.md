---
title: "Приступая к работе AD Node.js aaaAzure | Документы Microsoft"
description: "Как toobuild веб-API Node.js REST, интегрируется с Azure AD для проверки подлинности."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="ad42a-103">Начало работы с веб-API для Node.js</span><span class="sxs-lookup"><span data-stu-id="ad42a-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ad42a-104">*Passport* — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="ad42a-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="ad42a-105">Гибкая и модульной Passport плавно могут удаляться в tooany срочные или Restify веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ad42a-105">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="ad42a-106">Он также позволяет использовать разные стратегии с поддержкой аутентификации на основе имени пользователя и пароля, учетных записей Facebook, Twitter и пр.</span><span class="sxs-lookup"><span data-stu-id="ad42a-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="ad42a-107">Мы разработали стратегию для Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad42a-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ad42a-108">Мы установить этот модуль, а затем добавьте hello Microsoft Azure Active Directory `passport-azure-ad` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="ad42a-108">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="ad42a-109">toodo это, необходимо:</span><span class="sxs-lookup"><span data-stu-id="ad42a-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="ad42a-110">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ad42a-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="ad42a-111">Настройка вашего приложения toouse Passport `passport-azure-ad` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="ad42a-111">Set up your app toouse Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="ad42a-112">Настройка клиентского приложения toocall hello tooDo список веб-API.</span><span class="sxs-lookup"><span data-stu-id="ad42a-112">Configure a client application toocall hello tooDo List web API.</span></span>

<span data-ttu-id="ad42a-113">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="ad42a-113">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="ad42a-114">Данная статья не охватывает как tooimplement вход, регистрация, или профиль управления с помощью Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ad42a-114">This article doesn't cover how tooimplement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="ad42a-115">Этот раздел посвящен вызовах веб-API после hello пользователь уже прошел проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="ad42a-115">It focuses on calling web APIs after hello user is already authenticated.</span></span>  <span data-ttu-id="ad42a-116">Мы рекомендуем начать с [как toointegrate с Azure Active Directory документа](active-directory-how-to-integrate.md) toolearn об основах hello из Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad42a-116">We recommend that you start with [How toointegrate with Azure Active Directory document](active-directory-how-to-integrate.md) toolearn about hello basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="ad42a-117">Мы выпустили все hello исходного кода в этом примере выполнение в GitHub в рамках лицензии MIT, и вы можете бесплатно tooclone (или даже лучше вилки) и предоставления отзывов и запросов по запросу.</span><span class="sxs-lookup"><span data-stu-id="ad42a-117">We've released all hello source code for this running example in GitHub under an MIT license, so feel free tooclone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="ad42a-118">Информация о модулях Node.js</span><span class="sxs-lookup"><span data-stu-id="ad42a-118">About Node.js modules</span></span>
<span data-ttu-id="ad42a-119">В этом пошаговом руководстве мы используем модули Node.js.</span><span class="sxs-lookup"><span data-stu-id="ad42a-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="ad42a-120">Модули — это загружаемые пакеты JavaScript, предоставляющие вашему приложению определенные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="ad42a-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="ad42a-121">Обычно установите модули, используя hello Node.js NPM средство командной строки в каталоге установки NPM hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-121">You usually install modules by using hello Node.js an NPM command-line tool in hello NPM installation directory.</span></span> <span data-ttu-id="ad42a-122">Тем не менее некоторые модули, такие как HTTP-модуль hello, будут включены в пакет Node.js core hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-122">However, some modules, such as hello HTTP module, are included in hello core Node.js package.</span></span>

<span data-ttu-id="ad42a-123">Установленные модули сохраняются в hello **node_modules** каталог в корневой каталог установки Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-123">Installed modules are saved in hello **node_modules** directory at hello root of your Node.js installation directory.</span></span> <span data-ttu-id="ad42a-124">В каждом модуле hello **node_modules** directory поддерживает собственный **node_modules** каталог, содержащий каких-либо модулей, от которых он зависит.</span><span class="sxs-lookup"><span data-stu-id="ad42a-124">Each module in hello **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="ad42a-125">Кроме того, отдельный каталог **node_modules** создается для каждого требуемого модуля.</span><span class="sxs-lookup"><span data-stu-id="ad42a-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="ad42a-126">Эта структура каталогов рекурсивные представляет цепочку зависимостей hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-126">This recursive directory structure represents hello dependency chain.</span></span>

<span data-ttu-id="ad42a-127">Эта структура цепочки зависимостей занимает много дискового пространства.</span><span class="sxs-lookup"><span data-stu-id="ad42a-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="ad42a-128">Однако она также гарантирует, что соблюдены все зависимости, и этой версии hello hello модули, используемые в разработке также используется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ad42a-128">But it also guarantees that all dependencies are met and that hello version of hello modules that's used in development is also used in production.</span></span> <span data-ttu-id="ad42a-129">Это делает более предсказуемое поведение приложения hello производства и предотвращает проблемы управления версиями, которые могут повлиять на пользователей.</span><span class="sxs-lookup"><span data-stu-id="ad42a-129">This makes hello production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="ad42a-130">Шаг 1. Регистрация клиента Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad42a-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="ad42a-131">toouse это образец, необходимо, чтобы клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad42a-131">toouse this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="ad42a-132">Если вы точно не знаете, какой клиент — или tooget, в статье [как tooget в Azure AD для клиента](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ad42a-132">If you're not sure what a tenant is or how tooget one, see [How tooget an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="ad42a-133">Этап 2. Создание приложения</span><span class="sxs-lookup"><span data-stu-id="ad42a-133">Step 2: Create an application</span></span>
<span data-ttu-id="ad42a-134">Далее нужно создать приложение в каталоге, что Azure AD предоставляет сведения, необходимые toosecurely взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="ad42a-134">Next you create an app in your directory that gives Azure AD information that it needs toosecurely communicate with your app.</span></span>  <span data-ttu-id="ad42a-135">Hello клиентского приложения и веб-API представлены одним **идентификатор приложения** таким образом, так как они включают в себя один логический приложения.</span><span class="sxs-lookup"><span data-stu-id="ad42a-135">Both hello client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="ad42a-136">toocreate приложения, выполните [эти инструкции](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="ad42a-136">toocreate an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="ad42a-137">Если вы создаете бизнес-приложение, возможно, [вам будут полезны эти дополнительные инструкции](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="ad42a-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="ad42a-138">toocreate приложения:</span><span class="sxs-lookup"><span data-stu-id="ad42a-138">toocreate an application:</span></span>

1. <span data-ttu-id="ad42a-139">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad42a-139">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ad42a-140">Hello в верхнем меню выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ad42a-140">On hello top menu, select your account.</span></span> <span data-ttu-id="ad42a-141">После этого в разделе hello **каталога** выберите hello клиента Active Directory, где требуется tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="ad42a-141">Then, under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="ad42a-142">Выберите в меню hello слева hello, **более служб**, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad42a-142">In hello menu on hello left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="ad42a-143">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ad42a-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="ad42a-144">Выполните запросы toocreate hello **веб-приложение или WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="ad42a-144">Follow hello prompts toocreate a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="ad42a-145">Hello **имя** из hello приложения описывает tooend пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="ad42a-145">hello **name** of hello application describes your application tooend users.</span></span>

      * <span data-ttu-id="ad42a-146">Hello **URL-адрес входа** hello базовый URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="ad42a-146">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="ad42a-147">Здравствуйте, по умолчанию используется URL-адрес образца кода hello `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="ad42a-147">hello default URL of hello sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="ad42a-148">Когда вы закончите регистрацию, Azure AD назначит приложению уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ad42a-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="ad42a-149">Это значение требуется в следующих разделах hello, поэтому скопируйте его со страницы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-149">You need this value in hello next sections, so copy it from hello application page.</span></span>

7. <span data-ttu-id="ad42a-150">Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-150">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="ad42a-151">Hello **URI идентификатора приложения** — это уникальный идентификатор для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ad42a-151">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="ad42a-152">соглашение о Hello — toouse `https://<tenant-domain>/<app-name>`, например: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="ad42a-152">hello convention is toouse `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="ad42a-153">Создание **ключ** для вашего приложения hello **параметры** страницы и скопируйте его в любом месте.</span><span class="sxs-lookup"><span data-stu-id="ad42a-153">Create a **Key** for your application from hello **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="ad42a-154">Скоро он вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="ad42a-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="ad42a-155">Шаг 3. Скачивание Node.js для своей платформы</span><span class="sxs-lookup"><span data-stu-id="ad42a-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="ad42a-156">toosuccessfully использование этого образца, необходимо иметь состоящая из Node.js.</span><span class="sxs-lookup"><span data-stu-id="ad42a-156">toosuccessfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="ad42a-157">Установите Node.js с сайта [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="ad42a-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="ad42a-158">Шаг 4. Установка MongoDB на вашей платформе</span><span class="sxs-lookup"><span data-stu-id="ad42a-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="ad42a-159">toosuccessfully использование этого образца, необходимо иметь состоящая из MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad42a-159">toosuccessfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="ad42a-160">Используйте hello toomake MongoDB постоянные API-интерфейса REST по экземплярам сервера.</span><span class="sxs-lookup"><span data-stu-id="ad42a-160">You use MongoDB toomake hello REST API persistent across server instances.</span></span>

<span data-ttu-id="ad42a-161">Установите MongoDB с сайта [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="ad42a-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="ad42a-162">В этом пошаговом руководстве предполагается использовать конечные точки установки и сервером по умолчанию hello для MongoDB, что на момент написания этой статьи hello является mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="ad42a-162">This walkthrough assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="ad42a-163">Шаг 5: Установка модулей Restify hello в веб-API</span><span class="sxs-lookup"><span data-stu-id="ad42a-163">Step 5: Install hello Restify modules in your web API</span></span>
<span data-ttu-id="ad42a-164">Мы используем Restify toobuild нашем API REST.</span><span class="sxs-lookup"><span data-stu-id="ad42a-164">We are using Restify toobuild our REST API.</span></span> <span data-ttu-id="ad42a-165">Restify — это минималистичная и гибкая платформа для приложений Node.j, созданная на основе Express.</span><span class="sxs-lookup"><span data-stu-id="ad42a-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="ad42a-166">Она располагает широким набором функций, позволяющих реализовать интерфейсы REST API поверх Connect.</span><span class="sxs-lookup"><span data-stu-id="ad42a-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="ad42a-167">Установка Restify</span><span class="sxs-lookup"><span data-stu-id="ad42a-167">Install Restify</span></span>
1. <span data-ttu-id="ad42a-168">Из командной строки hello, измените каталоги toohello **azuread** каталога.</span><span class="sxs-lookup"><span data-stu-id="ad42a-168">From hello command line, change directories toohello **azuread** directory.</span></span> <span data-ttu-id="ad42a-169">Если hello **azuread** каталог не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="ad42a-169">If hello **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="ad42a-170">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="ad42a-170">Type hello following command:</span></span>

    `npm install restify`

    <span data-ttu-id="ad42a-171">Эта команда устанавливает Restify.</span><span class="sxs-lookup"><span data-stu-id="ad42a-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="ad42a-172">Вы получили сообщение об ошибке?</span><span class="sxs-lookup"><span data-stu-id="ad42a-172">Did you get an error?</span></span>
<span data-ttu-id="ad42a-173">В некоторых операционных системах при использовании параметра NPM может появиться такое сообщение об ошибке (**Error: EPERM, chmod '/usr/local/bin/..'**).</span><span class="sxs-lookup"><span data-stu-id="ad42a-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="ad42a-174">и предложения, попробуйте выполнить выполняющейся hello учетной записи с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ad42a-174">and a suggestion that you try running hello account as an administrator.</span></span> <span data-ttu-id="ad42a-175">В этом случае используйте toorun команда hello sudo NPM с более высоким уровнем привилегий.</span><span class="sxs-lookup"><span data-stu-id="ad42a-175">If this occurs, use hello sudo command toorun NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="ad42a-176">Вы получили сообщение об ошибке, которая относится к DTRACE?</span><span class="sxs-lookup"><span data-stu-id="ad42a-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="ad42a-177">При установке Restify может появиться примерно следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="ad42a-177">You might see an error like this when installing Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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
<span data-ttu-id="ad42a-178">Restify предоставляет мощный механизм для трассировки вызовов REST с помощью DTrace.</span><span class="sxs-lookup"><span data-stu-id="ad42a-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="ad42a-179">Но во многих операционных системах DTrace отсутствует.</span><span class="sxs-lookup"><span data-stu-id="ad42a-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="ad42a-180">Эти ошибки можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="ad42a-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="ad42a-181">Hello выходные данные этой команды должен выглядеть примерно toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ad42a-181">hello output of this command should look similar toohello following output:</span></span>

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
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="ad42a-182">Шаг 6. Установка Passport.js для веб-интерфейса API</span><span class="sxs-lookup"><span data-stu-id="ad42a-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="ad42a-183">[Passport](http://passportjs.org/) — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="ad42a-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="ad42a-184">Гибкая и модульной Passport плавно могут удаляться в tooany срочные или Restify веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ad42a-184">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="ad42a-185">Он также позволяет использовать разные стратегии с поддержкой аутентификации на основе имени пользователя и пароля, учетных записей Facebook, Twitter и пр.</span><span class="sxs-lookup"><span data-stu-id="ad42a-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="ad42a-186">Мы разработали стратегию для Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad42a-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="ad42a-187">Мы установить этот модуль, а затем добавьте подключаемого модуля стратегии hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad42a-187">We install this module and then add hello Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="ad42a-188">Из командной строки hello, измените каталоги toohello **azuread** каталога.</span><span class="sxs-lookup"><span data-stu-id="ad42a-188">From hello command line, change directories toohello **azuread** directory.</span></span>

2. <span data-ttu-id="ad42a-189">tooinstall passport.js введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ad42a-189">tooinstall passport.js, enter hello following command :</span></span>

    `npm install passport`

    <span data-ttu-id="ad42a-190">Hello выходные данные команды hello должен выглядеть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="ad42a-190">hello output of hello command should look similar toohello following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="ad42a-191">Шаг 7: Добавление веб-API tooyour Passport Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad42a-191">Step 7: Add Passport-Azure-AD tooyour web API</span></span>
<span data-ttu-id="ad42a-192">Далее добавим стратегии hello OAuth с помощью `passport-azure-ad`, набор стратегии, которые подключаются tooPassport Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad42a-192">Next we add hello OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory tooPassport.</span></span> <span data-ttu-id="ad42a-193">В этом примере REST API мы будем использовать эту стратегию для токенов носителя.</span><span class="sxs-lookup"><span data-stu-id="ad42a-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="ad42a-194">Платформа OAuth2 позволяет выдавать маркеры любого известного типа, но в большинстве случаев используются маркеры только нескольких типов.</span><span class="sxs-lookup"><span data-stu-id="ad42a-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="ad42a-195">Токены носителя являются маркерами hello чаще всего используется для защиты конечных точек.</span><span class="sxs-lookup"><span data-stu-id="ad42a-195">Bearer tokens are hello most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="ad42a-196">Они имеют тип hello наиболее широко выданного маркера в OAuth2.</span><span class="sxs-lookup"><span data-stu-id="ad42a-196">They are hello most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="ad42a-197">Многие предполагают, что токены носителя являются единственным типом токены, выданные hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-197">Many implementations assume that bearer tokens are hello only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="ad42a-198">Из командной строки hello, измените каталоги toohello **azuread** каталога.</span><span class="sxs-lookup"><span data-stu-id="ad42a-198">From hello command line, change directories toohello **azuread** directory.</span></span>

<span data-ttu-id="ad42a-199">Тип hello следующая команда tooinstall hello Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="ad42a-199">Type hello following command tooinstall hello Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="ad42a-200">Hello выходные данные команды hello должен выглядеть примерно toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ad42a-200">hello output of hello command should look similar toohello following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="ad42a-201">Шаг 8: Добавление MongoDB модули tooyour веб-API</span><span class="sxs-lookup"><span data-stu-id="ad42a-201">Step 8: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="ad42a-202">Мы используем MongoDB в качестве хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="ad42a-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="ad42a-203">По этой причине мы должны tooinstall hello широко используется подключаемый модуль вызываемой модели toomanage Mongoose и схемы.</span><span class="sxs-lookup"><span data-stu-id="ad42a-203">For that reason, we need tooinstall hello widely used plug-in called Mongoose toomanage models and schemas.</span></span> <span data-ttu-id="ad42a-204">Также нужно tooinstall hello базы данных драйверов для MongoDB (который также называется MongoDB).</span><span class="sxs-lookup"><span data-stu-id="ad42a-204">We also need tooinstall hello database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="ad42a-205">Шаг 9. Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="ad42a-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="ad42a-206">Далее приведены инструкции по установке hello оставшихся необходимые модули.</span><span class="sxs-lookup"><span data-stu-id="ad42a-206">Next we install hello remaining required modules.</span></span>

1. <span data-ttu-id="ad42a-207">Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.</span><span class="sxs-lookup"><span data-stu-id="ad42a-207">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad42a-208">Введите следующие команды tooinstall hello эти модули в вашей **node_modules** каталога:</span><span class="sxs-lookup"><span data-stu-id="ad42a-208">Enter hello following commands tooinstall these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="ad42a-209">Шаг 10. Создание server.js с зависимостями</span><span class="sxs-lookup"><span data-stu-id="ad42a-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="ad42a-210">Hello server.js обеспечивает большую часть функций hello API веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="ad42a-210">hello server.js file provides most of hello functionality for our web API server.</span></span> <span data-ttu-id="ad42a-211">Мы добавляем большая часть наших toothis файл кода.</span><span class="sxs-lookup"><span data-stu-id="ad42a-211">We add most of our code toothis file.</span></span> <span data-ttu-id="ad42a-212">В рабочей среде рекомендуется выполнить рефакторинг функции hello на меньшие файлы, такие как отдельные маршруты и контроллеров.</span><span class="sxs-lookup"><span data-stu-id="ad42a-212">For production purposes, we recommend that you refactor hello functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="ad42a-213">В этом демонстрационном примере мы включим все эти механизмы в файл server.js.</span><span class="sxs-lookup"><span data-stu-id="ad42a-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="ad42a-214">Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.</span><span class="sxs-lookup"><span data-stu-id="ad42a-214">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad42a-215">Создание `server.js` файл в любом редакторе, а затем добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="ad42a-215">Create a `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="ad42a-216">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-216">Save hello file.</span></span> <span data-ttu-id="ad42a-217">Мы вернемся вскоре tooit.</span><span class="sxs-lookup"><span data-stu-id="ad42a-217">We'll return tooit shortly.</span></span>

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="ad42a-218">Шаг 11: Создание файла конфигурации toostore настройки Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad42a-218">Step 11: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="ad42a-219">Этот файл код передает hello параметры конфигурации из вашего tooPassport.js портала Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad42a-219">This code file passes hello configuration parameters from your Azure Active Directory portal tooPassport.js.</span></span> <span data-ttu-id="ad42a-220">Эти значения конфигурации, созданный при добавлении API toohello hello веб-портала в первой части пошагового руководства hello hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-220">You created these configuration values when you added hello web API toohello portal in hello first part of hello walkthrough.</span></span> <span data-ttu-id="ad42a-221">После копирования кода hello рассказывается какие tooput hello значениями этих параметров.</span><span class="sxs-lookup"><span data-stu-id="ad42a-221">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

1. <span data-ttu-id="ad42a-222">Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.</span><span class="sxs-lookup"><span data-stu-id="ad42a-222">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad42a-223">Создание `config.js` файл в любом редакторе, а затем добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="ad42a-223">Create a `config.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. <span data-ttu-id="ad42a-224">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-224">Save hello file.</span></span>

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a><span data-ttu-id="ad42a-225">Шаг 12: Добавление значений tooyour server.js файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="ad42a-225">Step 12: Add configuration values tooyour server.js file</span></span>
<span data-ttu-id="ad42a-226">Мы должны tooread эти значения из hello config-файл, созданный для нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ad42a-226">We need tooread these values from hello .config file that you created across our application.</span></span> <span data-ttu-id="ad42a-227">toodo это, мы добавляем hello config-файл как необходимый ресурс в приложении.</span><span class="sxs-lookup"><span data-stu-id="ad42a-227">toodo this, we add hello .config file as a required resource in our application.</span></span> <span data-ttu-id="ad42a-228">Мы Установка hello глобальные переменные toomatch hello переменных в документе config.js hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-228">Then we set hello global variables toomatch hello variables in hello config.js document.</span></span>

1. <span data-ttu-id="ad42a-229">Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.</span><span class="sxs-lookup"><span data-stu-id="ad42a-229">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad42a-230">Откройте ваш `server.js` файл в любом редакторе, а затем добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="ad42a-230">Open your `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="ad42a-231">Затем добавьте новый раздел слишком`server.js` с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="ad42a-231">Then add a new section too`server.js` with hello following code:</span></span>

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="ad42a-232">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-232">Save hello file.</span></span>

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="ad42a-233">Шаг 13: Добавление hello MongoDB модели и данные схемы с помощью Mongoose</span><span class="sxs-lookup"><span data-stu-id="ad42a-233">Step 13: Add hello MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="ad42a-234">Теперь эта Подготовка будет toostart оплата, как мы объединять эти три файла в службу REST API.</span><span class="sxs-lookup"><span data-stu-id="ad42a-234">Now all this preparation is going toostart paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="ad42a-235">В данном пошаговом руководстве мы используем MongoDB toostore нашей задачи, как описано в шаге 4.</span><span class="sxs-lookup"><span data-stu-id="ad42a-235">For this walkthrough, we use MongoDB toostore our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="ad42a-236">В hello `config.js` файла, созданного на шаге 11, мы позвонили базе данных `tasklist`, так как это было поместить в конце hello нашей **mogoose_auth_local** URL-адрес подключения.</span><span class="sxs-lookup"><span data-stu-id="ad42a-236">In hello `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at hello end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="ad42a-237">Не нужно toocreate базы данных, заранее в MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ad42a-237">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="ad42a-238">Вместо этого MongoDB это за нас на hello сначала создает выполнения приложения сервера (при условии, что hello базы данных еще не существует).</span><span class="sxs-lookup"><span data-stu-id="ad42a-238">Instead, MongoDB creates this for us on hello first run of our server application (assuming that hello database doesn't already exist).</span></span>

<span data-ttu-id="ad42a-239">Теперь, когда мы рассказали hello сервера базы данных MongoDB, который мы хотели бы toouse, то необходимо toowrite некоторые модели hello toocreate дополнительного кода и схемы для наших сервера задач.</span><span class="sxs-lookup"><span data-stu-id="ad42a-239">Now that we've told hello server which MongoDB database we'd like toouse, we need toowrite some additional code toocreate hello model and schema for our server's tasks.</span></span>

### <a name="discussion-of-hello-model"></a><span data-ttu-id="ad42a-240">Обсуждение модели hello</span><span class="sxs-lookup"><span data-stu-id="ad42a-240">Discussion of hello model</span></span>
<span data-ttu-id="ad42a-241">Мы используем очень простую модель схемы.</span><span class="sxs-lookup"><span data-stu-id="ad42a-241">Our schema model is simple.</span></span> <span data-ttu-id="ad42a-242">Вы можете дополнить ее в соответствии с потребностями.</span><span class="sxs-lookup"><span data-stu-id="ad42a-242">You expand it as required.</span></span>

<span data-ttu-id="ad42a-243">Имя: имя hello hello, кто назначается toohello задачи.</span><span class="sxs-lookup"><span data-stu-id="ad42a-243">NAME: hello name of hello person who is assigned toohello task.</span></span> <span data-ttu-id="ad42a-244">Тип **Строка**.</span><span class="sxs-lookup"><span data-stu-id="ad42a-244">A **String**.</span></span>

<span data-ttu-id="ad42a-245">ЗАДАЧИ: hello саму задачу.</span><span class="sxs-lookup"><span data-stu-id="ad42a-245">TASK: hello task itself.</span></span> <span data-ttu-id="ad42a-246">Тип **Строка**.</span><span class="sxs-lookup"><span data-stu-id="ad42a-246">A **String**.</span></span>

<span data-ttu-id="ad42a-247">Дата: hello Дата задачи hello оплаты.</span><span class="sxs-lookup"><span data-stu-id="ad42a-247">DATE: hello date that hello task is due.</span></span> <span data-ttu-id="ad42a-248">Тип **Дата и время**.</span><span class="sxs-lookup"><span data-stu-id="ad42a-248">A **DATETIME**.</span></span>

<span data-ttu-id="ad42a-249">ЗАВЕРШЕНО: Если задачу «hello» была завершена или нет.</span><span class="sxs-lookup"><span data-stu-id="ad42a-249">COMPLETED: If hello task has been completed or not.</span></span> <span data-ttu-id="ad42a-250">Тип **Логическое значение**.</span><span class="sxs-lookup"><span data-stu-id="ad42a-250">A **BOOLEAN**.</span></span>

### <a name="creating-hello-schema-in-hello-code"></a><span data-ttu-id="ad42a-251">Создание схемы hello в коде hello</span><span class="sxs-lookup"><span data-stu-id="ad42a-251">Creating hello schema in hello code</span></span>
1. <span data-ttu-id="ad42a-252">Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.</span><span class="sxs-lookup"><span data-stu-id="ad42a-252">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="ad42a-253">Откройте ваш `server.js` файл в любом редакторе, а затем добавьте следующую информацию ниже запись конфигурации hello hello:</span><span class="sxs-lookup"><span data-stu-id="ad42a-253">Open your `server.js` file in your favorite editor, and then add hello following information below hello configuration entry:</span></span>

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="ad42a-254">Как видно из кода hello нашей схемы сначала создается.</span><span class="sxs-lookup"><span data-stu-id="ad42a-254">As you can tell from hello code, we create our schema first.</span></span> <span data-ttu-id="ad42a-255">Затем мы создадим объекта модели, мы используем наши данные во всей hello кода при определении toostore наших **маршруты**.</span><span class="sxs-lookup"><span data-stu-id="ad42a-255">Then we create a model object that we use toostore our data throughout hello code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="ad42a-256">Шаг 14. Добавление маршрутов для сервера задач REST API</span><span class="sxs-lookup"><span data-stu-id="ad42a-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="ad42a-257">Теперь, когда у нас есть toowork модели базы данных с, добавим hello маршруты, мы применяемые постоянной серверов REST API.</span><span class="sxs-lookup"><span data-stu-id="ad42a-257">Now that we have a database model toowork with, let's add hello routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="ad42a-258">О маршрутах в Restify</span><span class="sxs-lookup"><span data-stu-id="ad42a-258">About routes in Restify</span></span>
<span data-ttu-id="ad42a-259">Маршруты незавершенное Restify hello таким же образом, они в hello Express стека.</span><span class="sxs-lookup"><span data-stu-id="ad42a-259">Routes work in Restify hello same way they do in hello Express stack.</span></span> <span data-ttu-id="ad42a-260">Определения маршрутов с помощью hello URI, что предполагается toocall приложения hello клиента.</span><span class="sxs-lookup"><span data-stu-id="ad42a-260">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="ad42a-261">Как правило, свои маршруты вы определяете в отдельном файле.</span><span class="sxs-lookup"><span data-stu-id="ad42a-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="ad42a-262">Для наших целей мы поместили нашей маршруты в файле server.js hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-262">For our purposes, we put our routes in hello server.js file.</span></span> <span data-ttu-id="ad42a-263">Для систем в рабочей среде мы рекомендуем вынести их в отдельный файл.</span><span class="sxs-lookup"><span data-stu-id="ad42a-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="ad42a-264">Типичный шаблон Restify для маршрута выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ad42a-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="ad42a-265">Это шаблон hello на самом базовом уровне.</span><span class="sxs-lookup"><span data-stu-id="ad42a-265">This is hello pattern at its most basic level.</span></span> <span data-ttu-id="ad42a-266">В Restify (как и в Express) доступны очень мощные функциональные возможности, например для определения типов приложений и выполнения сложной маршрутизации между несколькими конечными точками.</span><span class="sxs-lookup"><span data-stu-id="ad42a-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="ad42a-267">В нашем примере мы используем самые простые маршруты.</span><span class="sxs-lookup"><span data-stu-id="ad42a-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-tooour-server"></a><span data-ttu-id="ad42a-268">Добавление сервера tooour маршруты по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ad42a-268">Add default routes tooour server</span></span>
<span data-ttu-id="ad42a-269">Теперь мы добавить hello основные маршруты CRUD для создания, извлечения, обновления и удаления.</span><span class="sxs-lookup"><span data-stu-id="ad42a-269">We now add hello basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="ad42a-270">Из командной строки hello, измените каталоги toohello **azuread** папку, если вы еще не существует:</span><span class="sxs-lookup"><span data-stu-id="ad42a-270">From hello command line, change directories toohello **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="ad42a-271">Откройте hello `server.js` файл в любом редакторе, а затем добавьте следующую информацию ниже hello предыдущей базы данных записи, сделанные hello:</span><span class="sxs-lookup"><span data-stu-id="ad42a-271">Open hello `server.js` file in your favorite editor, and then add hello following information below hello previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="ad42a-272">Добавление обработки ошибок в интерфейсы API</span><span class="sxs-lookup"><span data-stu-id="ad42a-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="ad42a-273">Шаг 15. Создание сервера</span><span class="sxs-lookup"><span data-stu-id="ad42a-273">Step 15: Create your server</span></span>
<span data-ttu-id="ad42a-274">Мы уже определили базу данных и создали все маршруты.</span><span class="sxs-lookup"><span data-stu-id="ad42a-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="ad42a-275">последний самое toodo Hello добавить hello экземпляр сервера, который управляет наши вызовы.</span><span class="sxs-lookup"><span data-stu-id="ad42a-275">hello last thing toodo is add hello server instance that manages our calls.</span></span>

<span data-ttu-id="ad42a-276">В Restify (и Express) можно выполнять множество настройки для сервера REST API, а снова будет самый простой установки hello toouse для наших целей.</span><span class="sxs-lookup"><span data-stu-id="ad42a-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going toouse hello most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a><span data-ttu-id="ad42a-277">Шаг 16: Добавьте сервер toohello маршруты hello (без проверки подлинности, сейчас)</span><span class="sxs-lookup"><span data-stu-id="ad42a-277">Step 16: Add hello routes toohello server (without authentication for now)</span></span>
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a><span data-ttu-id="ad42a-278">Шаг 17: Запуск сервера hello (перед добавлением поддержка OAuth)</span><span class="sxs-lookup"><span data-stu-id="ad42a-278">Step 17: Run hello server (before adding OAuth support)</span></span>
<span data-ttu-id="ad42a-279">Прежде чем добавить аутентификацию, давайте протестируем сервер.</span><span class="sxs-lookup"><span data-stu-id="ad42a-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="ad42a-280">наиболее простым способом tootest Hello сервера — с помощью перелистывание в командной строке.</span><span class="sxs-lookup"><span data-stu-id="ad42a-280">hello easiest way tootest your server is by using curl in a command line.</span></span> <span data-ttu-id="ad42a-281">Перед этим мы должны служебную программу, которая позволяет нам tooparse выходные данные в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="ad42a-281">Before we do that, we need a utility that allows us tooparse output as JSON.</span></span>

1. <span data-ttu-id="ad42a-282">Установите hello следующие средства JSON (это средство используется всех hello следующие примеры):</span><span class="sxs-lookup"><span data-stu-id="ad42a-282">Install hello following JSON tool (all hello following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="ad42a-283">При этом устанавливаются средства JSON hello глобально.</span><span class="sxs-lookup"><span data-stu-id="ad42a-283">This installs hello JSON tool globally.</span></span> <span data-ttu-id="ad42a-284">Теперь, когда мы выполнена, давайте воспроизведения с сервером hello:</span><span class="sxs-lookup"><span data-stu-id="ad42a-284">Now that we’ve accomplished that, let’s play with hello server:</span></span>

2. <span data-ttu-id="ad42a-285">Сначала убедитесь, что запущен экземпляр MongoDB:</span><span class="sxs-lookup"><span data-stu-id="ad42a-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="ad42a-286">Затем измените toohello каталог и запустите изгиб:</span><span class="sxs-lookup"><span data-stu-id="ad42a-286">Then, change toohello directory and start curling:</span></span>

    <span data-ttu-id="ad42a-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="ad42a-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. <span data-ttu-id="ad42a-288">Затем можно добавить задачу следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ad42a-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="ad42a-289">Hello ответа должно быть:</span><span class="sxs-lookup"><span data-stu-id="ad42a-289">hello response should be:</span></span>

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
    <span data-ttu-id="ad42a-290">Для перечисления задач для Brandon можно использовать следующий способ:</span><span class="sxs-lookup"><span data-stu-id="ad42a-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="ad42a-291">Если все это работает, мы готовы tooadd OAuth toohello REST API сервера.</span><span class="sxs-lookup"><span data-stu-id="ad42a-291">If all this works, we're ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="ad42a-292">У вас уже есть сервер REST API с MongoDB!</span><span class="sxs-lookup"><span data-stu-id="ad42a-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-tooour-rest-api-server"></a><span data-ttu-id="ad42a-293">Шаг 18: Добавление сервера API-интерфейса REST tooour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="ad42a-293">Step 18: Add authentication tooour REST API server</span></span>
<span data-ttu-id="ad42a-294">Теперь, когда у нас запущен сервер REST API, мы можем использовать его для работы с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad42a-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="ad42a-295">Из командной строки hello, измените каталоги toohello **azuread** папку, если вы не являетесь уже существует.</span><span class="sxs-lookup"><span data-stu-id="ad42a-295">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="ad42a-296">Использовать hello OIDCBearerStrategy, который входит в состав passport azure ad</span><span class="sxs-lookup"><span data-stu-id="ad42a-296">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="ad42a-297">Мы создали стандартный сервер REST TODO без какой-либо авторизации.</span><span class="sxs-lookup"><span data-stu-id="ad42a-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="ad42a-298">Самое время добавить такую функцию.</span><span class="sxs-lookup"><span data-stu-id="ad42a-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="ad42a-299">Во-первых мы должны tooindicate, что мы хотим toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="ad42a-299">First, we need tooindicate that we want toouse Passport.</span></span> <span data-ttu-id="ad42a-300">Сделайте это сразу после конфигурации другого сервера:</span><span class="sxs-lookup"><span data-stu-id="ad42a-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="ad42a-301">При написании API, рекомендуется связывать уникальный из токена hello, hello пользователя toosomething данных hello подменить.</span><span class="sxs-lookup"><span data-stu-id="ad42a-301">When you write APIs, we recommend that you always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="ad42a-302">Когда этот сервер сохраняет элементы TODO, она сохраняет их на основе кода hello объекта пользователя hello в маркере hello (называемые через token.oid), который мы поместили в поле «владелец» hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-302">When this server stores TODO items, it stores them based on hello object ID of hello user in hello token (called through token.oid), which we put in hello “owner” field.</span></span> <span data-ttu-id="ad42a-303">Благодаря этому только владелец сможет получить доступ к своим элементам списка дел.</span><span class="sxs-lookup"><span data-stu-id="ad42a-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="ad42a-304">Нет отсутствие проблем в hello API «владелец», поэтому внешний пользователь может запросить hello TODOs других пользователей, даже если они проходят проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="ad42a-304">There is no exposure in hello API of “owner,” so an external user can request hello TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="ad42a-305">Далее используем стратегии носителя hello, входящий в состав `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="ad42a-305">Next let’s use hello bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="ad42a-306">Посмотрите на код hello сейчас и hello rest будут описаны чуть ниже.</span><span class="sxs-lookup"><span data-stu-id="ad42a-306">Look at hello code for now and we'll explain hello rest shortly.</span></span> <span data-ttu-id="ad42a-307">Вставьте этот текст после добавленного ранее:</span><span class="sxs-lookup"><span data-stu-id="ad42a-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="ad42a-308">Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.); это поведение учитывают все разработчики модулей стратегий.</span><span class="sxs-lookup"><span data-stu-id="ad42a-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="ad42a-309">Просматривая стратегии hello, видно, что мы передаем функции, которая содержит маркер и выполняются как параметры hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-309">Looking at hello strategy, you see we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="ad42a-310">Стратегия Hello поставляется обратно toous после он выполняет свою работу.</span><span class="sxs-lookup"><span data-stu-id="ad42a-310">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="ad42a-311">Да, мы храните hello пользователя и маркер hello образа, нам не нужно tooask его еще раз.</span><span class="sxs-lookup"><span data-stu-id="ad42a-311">After it does, we store hello user and stash hello token so we won’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad42a-312">Предыдущий код Hello принимает любой пользователь, который происходит tooauthenticate tooour сервера.</span><span class="sxs-lookup"><span data-stu-id="ad42a-312">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="ad42a-313">Это называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="ad42a-313">This is known as auto-registration.</span></span> <span data-ttu-id="ad42a-314">На рабочих серверах мы не рекомендуем разрешать вход без прохождения определенного процесса регистрации, который вы сочтете приемлемым.</span><span class="sxs-lookup"><span data-stu-id="ad42a-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="ad42a-315">Обычно это является шаблон hello в потребительские приложения, которые позволяет tooregister с Facebook, а затем попросите toofill дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="ad42a-315">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="ad42a-316">Если это не было программы командной строки, мы удалось извлекли hello электронной почты из hello токен объекта, который возвращается и затем предложено hello toofill пользователя дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="ad42a-316">If this wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="ad42a-317">Так как на тестовом сервере, мы просто добавьте toohello базы данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="ad42a-317">Because this is a test server, we simply add them toohello in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="ad42a-318">Защита некоторых конечных точек</span><span class="sxs-lookup"><span data-stu-id="ad42a-318">Protect some endpoints</span></span>
<span data-ttu-id="ad42a-319">Защита конечных точек, указав hello `passport.authenticate()` вызов с протоколом hello, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="ad42a-319">You protect endpoints by specifying hello `passport.authenticate()` call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="ad42a-320">toomake наш код сервера сделать что-нибудь интереснее, изменим hello маршрута.</span><span class="sxs-lookup"><span data-stu-id="ad42a-320">toomake our server code do something more interesting, let’s edit hello route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="ad42a-321">Шаг 19. Снова запустите свой сервер приложения и убедитесь, что он вас отклоняет.</span><span class="sxs-lookup"><span data-stu-id="ad42a-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="ad42a-322">Воспользуемся `curl` снова toosee Если теперь у нас есть OAuth2 защиты на основе наших конечных точек.</span><span class="sxs-lookup"><span data-stu-id="ad42a-322">Let's use `curl` again toosee if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="ad42a-323">Этот тест мы выполним до того, как запускать клиентские пакеты SDK для этой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ad42a-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="ad42a-324">Hello заголовки, которые возвращаются должно быть достаточно tootell нам, если мы будем вниз hello правильный путь.</span><span class="sxs-lookup"><span data-stu-id="ad42a-324">hello headers that are returned should be enough tootell us if we're going down hello right path.</span></span>

1. <span data-ttu-id="ad42a-325">Сначала убедитесь, что запущен экземпляр MongoDB:</span><span class="sxs-lookup"><span data-stu-id="ad42a-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="ad42a-326">Затем измените toohello каталог и запустите изгиб.</span><span class="sxs-lookup"><span data-stu-id="ad42a-326">Then, change toohello directory and start curling.</span></span>

      <span data-ttu-id="ad42a-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="ad42a-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="ad42a-328">Попробуйте выполнить простую команду POST.</span><span class="sxs-lookup"><span data-stu-id="ad42a-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="ad42a-329">401 — ответ hello, которую вы ищете здесь.</span><span class="sxs-lookup"><span data-stu-id="ad42a-329">A 401 is hello response you are looking for here.</span></span> <span data-ttu-id="ad42a-330">Этот ответ означает, что этот слой Passport hello пытается tooredirect toohello прав конечной точки, что именно вы хотите.</span><span class="sxs-lookup"><span data-stu-id="ad42a-330">This response indicates that hello Passport layer is trying tooredirect toohello authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad42a-331">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad42a-331">Next steps</span></span>
<span data-ttu-id="ad42a-332">Мы уже сделали с этим сервером все, что можно реализовать без использования клиента OAuth2.</span><span class="sxs-lookup"><span data-stu-id="ad42a-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="ad42a-333">Вам потребуется toogo через дополнительные пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="ad42a-333">You will need toogo through an additional walkthrough.</span></span>

<span data-ttu-id="ad42a-334">Вы узнали как tooimplement API REST с помощью Restify и OAuth2.</span><span class="sxs-lookup"><span data-stu-id="ad42a-334">You've now learned how tooimplement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="ad42a-335">Также имеется более чем достаточно tookeep кода при разработке службы, а также знание как toobuild по этому примеру.</span><span class="sxs-lookup"><span data-stu-id="ad42a-335">You also have more than enough code tookeep developing your service and learning how toobuild on this example.</span></span>

<span data-ttu-id="ad42a-336">Если вы заинтересованы в следующие шаги hello в поездке ADAL, ниже приведены некоторые поддерживаемые клиенты ADAL, мы рекомендуем, чтобы продолжить работу с.</span><span class="sxs-lookup"><span data-stu-id="ad42a-336">If you are interested in hello next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="ad42a-337">Клонировать работу машины tooyour разработчика и настроить, как описано в пошаговом руководстве hello.</span><span class="sxs-lookup"><span data-stu-id="ad42a-337">Clone down tooyour developer machine and configure as described in hello walkthrough.</span></span>

[<span data-ttu-id="ad42a-338">ADAL для iOS</span><span class="sxs-lookup"><span data-stu-id="ad42a-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="ad42a-339">ADAL для Android</span><span class="sxs-lookup"><span data-stu-id="ad42a-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
