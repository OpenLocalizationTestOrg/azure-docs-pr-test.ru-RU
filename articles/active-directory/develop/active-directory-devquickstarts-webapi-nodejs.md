---
title: "Начало работы с Node.js в Azure AD | Документация Майкрософт"
description: "Практическое руководство по созданию на основе Node.js веб-интерфейса REST API, который интегрируется с Azure AD для аутентификации."
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
ms.openlocfilehash: 4f58177f540c14172d7ece8b4bc8c8a2b9787f8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="7fca4-103">Начало работы с веб-API для Node.js</span><span class="sxs-lookup"><span data-stu-id="7fca4-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="7fca4-104">*Passport* — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="7fca4-105">Этот слой имеет гибкую модульную структуру, которая позволяет незаметно размещать его в любом веб-приложении на основе Express или Restify.</span><span class="sxs-lookup"><span data-stu-id="7fca4-105">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="7fca4-106">Он также позволяет использовать разные стратегии с поддержкой аутентификации на основе имени пользователя и пароля, учетных записей Facebook, Twitter и пр.</span><span class="sxs-lookup"><span data-stu-id="7fca4-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="7fca4-107">Мы разработали стратегию для Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7fca4-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7fca4-108">Теперь мы установим этот модуль и добавим подключаемый модуль Microsoft Azure Active Directory `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="7fca4-108">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="7fca4-109">Для этого необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7fca4-109">To do this, you need to:</span></span>

1. <span data-ttu-id="7fca4-110">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7fca4-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="7fca4-111">настроить приложение для использования подключаемого модуля Passport `passport-azure-ad`;</span><span class="sxs-lookup"><span data-stu-id="7fca4-111">Set up your app to use Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="7fca4-112">настроить клиентское приложение для вызова методов веб-API приложения со списком дел.</span><span class="sxs-lookup"><span data-stu-id="7fca4-112">Configure a client application to call the To Do List web API.</span></span>

<span data-ttu-id="7fca4-113">Код в этом учебнике размещен на портале [GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="7fca4-113">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="7fca4-114">В этой статье не рассматривается реализация входа, регистрации и управления профилями с помощью Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7fca4-114">This article doesn't cover how to implement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="7fca4-115">Она посвящена вызову веб-API после того, как пользователь прошел проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="7fca4-115">It focuses on calling web APIs after the user is already authenticated.</span></span>  <span data-ttu-id="7fca4-116">Мы рекомендуем перед началом работы ознакомиться с обзорной статьей, посвященной [интеграции с Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="7fca4-116">We recommend that you start with [How to integrate with Azure Active Directory document](active-directory-how-to-integrate.md) to learn about the basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="7fca4-117">Полный исходный код для этого рабочего примера мы опубликовали в GitHub на условиях лицензии MIT, поэтому вы можете без проблем клонировать (а еще лучше — разветвлять) его, а также оставлять отзывы и отправлять запросы на включение внесенных изменений.</span><span class="sxs-lookup"><span data-stu-id="7fca4-117">We've released all the source code for this running example in GitHub under an MIT license, so feel free to clone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="7fca4-118">Информация о модулях Node.js</span><span class="sxs-lookup"><span data-stu-id="7fca4-118">About Node.js modules</span></span>
<span data-ttu-id="7fca4-119">В этом пошаговом руководстве мы используем модули Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="7fca4-120">Модули — это загружаемые пакеты JavaScript, дающую приложению определенную функциональность.</span><span class="sxs-lookup"><span data-stu-id="7fca4-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="7fca4-121">Обычно для установки модулей применяется средство NPM для командной строки Node.js, которое запускается в каталоге установки NPM.</span><span class="sxs-lookup"><span data-stu-id="7fca4-121">You usually install modules by using the Node.js an NPM command-line tool in the NPM installation directory.</span></span> <span data-ttu-id="7fca4-122">Но некоторые модули, например модуль HTTP, уже включены в основной пакет Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-122">However, some modules, such as the HTTP module, are included in the core Node.js package.</span></span>

<span data-ttu-id="7fca4-123">Установленные модули сохраняются в каталоге **node_modules**, который находится в корневом каталоге установки Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-123">Installed modules are saved in the **node_modules** directory at the root of your Node.js installation directory.</span></span> <span data-ttu-id="7fca4-124">Каждый модуль в каталоге **node_modules** использует свой собственный каталог **node_modules**, в котором хранит свои модули-зависимости.</span><span class="sxs-lookup"><span data-stu-id="7fca4-124">Each module in the **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="7fca4-125">Кроме того, отдельный каталог **node_modules** создается для каждого требуемого модуля.</span><span class="sxs-lookup"><span data-stu-id="7fca4-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="7fca4-126">Такая рекурсивная структура каталога представляет цепочку зависимостей.</span><span class="sxs-lookup"><span data-stu-id="7fca4-126">This recursive directory structure represents the dependency chain.</span></span>

<span data-ttu-id="7fca4-127">Эта структура цепочки зависимостей занимает много дискового пространства.</span><span class="sxs-lookup"><span data-stu-id="7fca4-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="7fca4-128">Но зато она гарантирует, что всегда будут выполнены все зависимости и что версии модулей, используемых в разработке и в производственной среде, будут совпадать.</span><span class="sxs-lookup"><span data-stu-id="7fca4-128">But it also guarantees that all dependencies are met and that the version of the modules that's used in development is also used in production.</span></span> <span data-ttu-id="7fca4-129">Это делает более предсказуемым поведение рабочего приложения и предотвращает проблемы с управлением версиями, которые могут повлиять на работу пользователей.</span><span class="sxs-lookup"><span data-stu-id="7fca4-129">This makes the production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="7fca4-130">Шаг 1. Регистрация клиента Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fca4-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="7fca4-131">Для использования этого примера вам понадобится клиент Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7fca4-131">To use this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="7fca4-132">Если вы не знаете, что это такое и как его получить, ознакомьтесь с [этой статьей о клиенте Azure AD](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7fca4-132">If you're not sure what a tenant is or how to get one, see [How to get an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="7fca4-133">Этап 2. Создание приложения</span><span class="sxs-lookup"><span data-stu-id="7fca4-133">Step 2: Create an application</span></span>
<span data-ttu-id="7fca4-134">Затем создайте приложение в каталоге, которое предоставит Azure AD сведения, необходимые для безопасного взаимодействия с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="7fca4-134">Next you create an app in your directory that gives Azure AD information that it needs to securely communicate with your app.</span></span>  <span data-ttu-id="7fca4-135">В нашем примере и клиентское приложение, и веб-API представлены одним **идентификатором приложения**, так как они представляют одно приложение логики.</span><span class="sxs-lookup"><span data-stu-id="7fca4-135">Both the client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="7fca4-136">Создайте приложение, выполнив [эти указания](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="7fca4-136">To create an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="7fca4-137">Если вы создаете бизнес-приложение, возможно, [вам будут полезны эти дополнительные инструкции](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="7fca4-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="7fca4-138">Выполните эти действия, чтобы создать приложение.</span><span class="sxs-lookup"><span data-stu-id="7fca4-138">To create an application:</span></span>

1. <span data-ttu-id="7fca4-139">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7fca4-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7fca4-140">В меню сверху выберите учетную запись.</span><span class="sxs-lookup"><span data-stu-id="7fca4-140">On the top menu, select your account.</span></span> <span data-ttu-id="7fca4-141">В списке **Каталог** выберите клиент Active Directory, в котором вы решили зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="7fca4-141">Then, under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="7fca4-142">Выберите **Больше служб** в меню слева, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-142">In the menu on the left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="7fca4-143">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="7fca4-144">Следуйте инструкциям на экране, чтобы создать **веб-приложение и (или) веб-API**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-144">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="7fca4-145">**Имя** приложения служит его описанием для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="7fca4-145">The **name** of the application describes your application to end users.</span></span>

      * <span data-ttu-id="7fca4-146">**URL-адрес входа** — это базовый URL-адрес вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7fca4-146">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="7fca4-147">В примере кода указан URL-адрес по умолчанию: `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="7fca4-147">The default URL of the sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="7fca4-148">Когда вы закончите регистрацию, Azure AD назначит приложению уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="7fca4-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="7fca4-149">Это значение вам понадобится в следующих разделах, поэтому не забудьте скопировать его на странице приложения.</span><span class="sxs-lookup"><span data-stu-id="7fca4-149">You need this value in the next sections, so copy it from the application page.</span></span>

7. <span data-ttu-id="7fca4-150">На странице **Параметры** -> **Свойства** приложения обновите его универсальный код ресурса (URI) идентификатора.</span><span class="sxs-lookup"><span data-stu-id="7fca4-150">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="7fca4-151">**URI идентификатора приложения** — это уникальный идентификатор вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7fca4-151">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="7fca4-152">В соответствии с соглашением, следует использовать `https://<tenant-domain>/<app-name>`, например `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="7fca4-152">The convention is to use `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="7fca4-153">Создайте **ключ** приложения на странице **Параметры** и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="7fca4-153">Create a **Key** for your application from the **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="7fca4-154">Скоро он вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="7fca4-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="7fca4-155">Шаг 3. Скачивание Node.js для своей платформы</span><span class="sxs-lookup"><span data-stu-id="7fca4-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="7fca4-156">Чтобы успешно использовать этот пример, необходимо иметь рабочую установку Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-156">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="7fca4-157">Установите Node.js с сайта [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="7fca4-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="7fca4-158">Шаг 4. Установка MongoDB на вашей платформе</span><span class="sxs-lookup"><span data-stu-id="7fca4-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="7fca4-159">Чтобы успешно использовать этот пример, необходимо иметь рабочую установку MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7fca4-159">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="7fca4-160">MongoDB вам нужен для того, чтобы интерфейс REST API оставался неизменным при использовании нескольких экземпляров сервера.</span><span class="sxs-lookup"><span data-stu-id="7fca4-160">You use MongoDB to make the REST API persistent across server instances.</span></span>

<span data-ttu-id="7fca4-161">Установите MongoDB с сайта [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="7fca4-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="7fca4-162">В этом руководстве мы предполагаем, что вы используете для MongoDB заданные по умолчанию конечные точки установки и сервера. На момент написания этой статьи для них используется значение mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="7fca4-162">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="7fca4-163">Шаг 5. Установка модулей Restify для веб-API</span><span class="sxs-lookup"><span data-stu-id="7fca4-163">Step 5: Install the Restify modules in your web API</span></span>
<span data-ttu-id="7fca4-164">Мы будем использовать Restify для создания интерфейса REST API.</span><span class="sxs-lookup"><span data-stu-id="7fca4-164">We are using Restify to build our REST API.</span></span> <span data-ttu-id="7fca4-165">Restify — это минималистичная и гибкая платформа для приложений Node.j, созданная на основе Express.</span><span class="sxs-lookup"><span data-stu-id="7fca4-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="7fca4-166">Она располагает широким набором функций, позволяющих реализовать интерфейсы REST API поверх Connect.</span><span class="sxs-lookup"><span data-stu-id="7fca4-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="7fca4-167">Установка Restify</span><span class="sxs-lookup"><span data-stu-id="7fca4-167">Install Restify</span></span>
1. <span data-ttu-id="7fca4-168">В командной строке перейдите в каталог **azuread**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-168">From the command line, change directories to the **azuread** directory.</span></span> <span data-ttu-id="7fca4-169">Если каталог **azuread** не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="7fca4-169">If the **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="7fca4-170">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7fca4-170">Type the following command:</span></span>

    `npm install restify`

    <span data-ttu-id="7fca4-171">Эта команда устанавливает Restify.</span><span class="sxs-lookup"><span data-stu-id="7fca4-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="7fca4-172">Вы получили сообщение об ошибке?</span><span class="sxs-lookup"><span data-stu-id="7fca4-172">Did you get an error?</span></span>
<span data-ttu-id="7fca4-173">В некоторых операционных системах при использовании параметра NPM может появиться такое сообщение об ошибке (**Error: EPERM, chmod '/usr/local/bin/..'**).</span><span class="sxs-lookup"><span data-stu-id="7fca4-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="7fca4-174">Оно может сопровождаться предложением использовать учетную запись с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="7fca4-174">and a suggestion that you try running the account as an administrator.</span></span> <span data-ttu-id="7fca4-175">Если вы увидите такую ошибку, запустите NPM с более высоким уровнем привилегий, используя команду sudo.</span><span class="sxs-lookup"><span data-stu-id="7fca4-175">If this occurs, use the sudo command to run NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="7fca4-176">Вы получили сообщение об ошибке, которая относится к DTRACE?</span><span class="sxs-lookup"><span data-stu-id="7fca4-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="7fca4-177">При установке Restify может появиться примерно следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="7fca4-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="7fca4-178">Restify предоставляет мощный механизм для трассировки вызовов REST с помощью DTrace.</span><span class="sxs-lookup"><span data-stu-id="7fca4-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="7fca4-179">Но во многих операционных системах DTrace отсутствует.</span><span class="sxs-lookup"><span data-stu-id="7fca4-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="7fca4-180">Эти ошибки можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="7fca4-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="7fca4-181">Результат этой команды должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="7fca4-181">The output of this command should look similar to the following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="7fca4-182">Шаг 6. Установка Passport.js для веб-интерфейса API</span><span class="sxs-lookup"><span data-stu-id="7fca4-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="7fca4-183">[Passport](http://passportjs.org/) — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="7fca4-184">Этот слой имеет гибкую модульную структуру, которая позволяет незаметно размещать его в любом веб-приложении на основе Express или Restify.</span><span class="sxs-lookup"><span data-stu-id="7fca4-184">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="7fca4-185">Он также позволяет использовать разные стратегии с поддержкой аутентификации на основе имени пользователя и пароля, учетных записей Facebook, Twitter и пр.</span><span class="sxs-lookup"><span data-stu-id="7fca4-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="7fca4-186">Мы разработали стратегию для Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7fca4-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="7fca4-187">Мы установим этот модуль, а затем добавим подключаемый модуль стратегии Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7fca4-187">We install this module and then add the Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="7fca4-188">В командной строке перейдите в каталог **azuread**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-188">From the command line, change directories to the **azuread** directory.</span></span>

2. <span data-ttu-id="7fca4-189">Введите следующую команду для установки passport.js:</span><span class="sxs-lookup"><span data-stu-id="7fca4-189">To install passport.js, enter the following command :</span></span>

    `npm install passport`

    <span data-ttu-id="7fca4-190">Результат этой команды должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="7fca4-190">The output of the command should look similar to the following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="7fca4-191">Шаг 7. Добавление Passport-Azure-AD для веб-API</span><span class="sxs-lookup"><span data-stu-id="7fca4-191">Step 7: Add Passport-Azure-AD to your web API</span></span>
<span data-ttu-id="7fca4-192">Теперь мы добавим стратегию OAuth с помощью набора стратегий `passport-azure-ad`, который устанавливает подключение Azure AD к Passport.</span><span class="sxs-lookup"><span data-stu-id="7fca4-192">Next we add the OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory to Passport.</span></span> <span data-ttu-id="7fca4-193">В этом примере REST API мы будем использовать эту стратегию для токенов носителя.</span><span class="sxs-lookup"><span data-stu-id="7fca4-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="7fca4-194">Платформа OAuth2 позволяет выдавать маркеры любого известного типа, но в большинстве случаев используются маркеры только нескольких типов.</span><span class="sxs-lookup"><span data-stu-id="7fca4-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="7fca4-195">Для защиты конечных точек чаще всего применяются токены носителя.</span><span class="sxs-lookup"><span data-stu-id="7fca4-195">Bearer tokens are the most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="7fca4-196">Это самый распространенный тип выдаваемых маркеров в OAuth2.</span><span class="sxs-lookup"><span data-stu-id="7fca4-196">They are the most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="7fca4-197">Во многих реализациях предполагается, что токены носителя — это единственный тип выдаваемых маркеров.</span><span class="sxs-lookup"><span data-stu-id="7fca4-197">Many implementations assume that bearer tokens are the only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="7fca4-198">В командной строке перейдите в каталог **azuread**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-198">From the command line, change directories to the **azuread** directory.</span></span>

<span data-ttu-id="7fca4-199">Введите следующую команду для установки модуля `passport-azure-ad module` для Passport.js:</span><span class="sxs-lookup"><span data-stu-id="7fca4-199">Type the following command to install the Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="7fca4-200">Результат этой команды должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="7fca4-200">The output of the command should look similar to the following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="7fca4-201">Шаг 8. Добавление модулей MongoDB в веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="7fca4-201">Step 8: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="7fca4-202">Мы используем MongoDB в качестве хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="7fca4-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="7fca4-203">Поэтому нам потребуется широко распространенный подключаемый модуль Mongoose для управления моделями и схемами.</span><span class="sxs-lookup"><span data-stu-id="7fca4-203">For that reason, we need to install the widely used plug-in called Mongoose to manage models and schemas.</span></span> <span data-ttu-id="7fca4-204">Еще нам нужно установить драйвер базы данных для MongoDB (который также называется MongoDB).</span><span class="sxs-lookup"><span data-stu-id="7fca4-204">We also need to install the database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="7fca4-205">Шаг 9. Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="7fca4-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="7fca4-206">Далее мы установим остальные необходимые модули.</span><span class="sxs-lookup"><span data-stu-id="7fca4-206">Next we install the remaining required modules.</span></span>

1. <span data-ttu-id="7fca4-207">В окне командной строки перейдите в каталог **azuread** или убедитесь, что вы уже находитесь в нем.</span><span class="sxs-lookup"><span data-stu-id="7fca4-207">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7fca4-208">Введите следующие команды для установки необходимых модулей в каталог **node_modules**:</span><span class="sxs-lookup"><span data-stu-id="7fca4-208">Enter the following commands to install these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="7fca4-209">Шаг 10. Создание server.js с зависимостями</span><span class="sxs-lookup"><span data-stu-id="7fca4-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="7fca4-210">Основная часть функций для сервера веб-API реализована в файле server.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-210">The server.js file provides most of the functionality for our web API server.</span></span> <span data-ttu-id="7fca4-211">В этот файл мы включим основную часть нашего кода.</span><span class="sxs-lookup"><span data-stu-id="7fca4-211">We add most of our code to this file.</span></span> <span data-ttu-id="7fca4-212">Для использования в рабочей среде мы рекомендуем разделить код функций на небольшие файлы, например отдельные маршруты и контроллеры.</span><span class="sxs-lookup"><span data-stu-id="7fca4-212">For production purposes, we recommend that you refactor the functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="7fca4-213">В этом демонстрационном примере мы включим все эти механизмы в файл server.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="7fca4-214">В окне командной строки перейдите в каталог **azuread** или убедитесь, что вы уже находитесь в нем.</span><span class="sxs-lookup"><span data-stu-id="7fca4-214">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7fca4-215">Создайте файл `server.js` в любом удобном редакторе и добавьте в него следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="7fca4-215">Create a `server.js` file in your favorite editor, and then add the following information:</span></span>

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

3. <span data-ttu-id="7fca4-216">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="7fca4-216">Save the file.</span></span> <span data-ttu-id="7fca4-217">Мы вернемся к нему чуть позже.</span><span class="sxs-lookup"><span data-stu-id="7fca4-217">We'll return to it shortly.</span></span>

## <a name="step-11-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="7fca4-218">Шаг 11. Создание файла конфигурации для сохранения параметров Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fca4-218">Step 11: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="7fca4-219">Этот файл кода передает в Passport.js параметры конфигурации из вашего портала Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7fca4-219">This code file passes the configuration parameters from your Azure Active Directory portal to Passport.js.</span></span> <span data-ttu-id="7fca4-220">Эти значения конфигурации были созданы, когда вы добавляли веб-интерфейс API на портал, выполняя первую часть этого руководства.</span><span class="sxs-lookup"><span data-stu-id="7fca4-220">You created these configuration values when you added the web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="7fca4-221">Сейчас мы объясним, какие значения нужно указать для этих параметров в скопированном фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="7fca4-221">We explain what to put in the values of these parameters after you copy the code.</span></span>

1. <span data-ttu-id="7fca4-222">В окне командной строки перейдите в каталог **azuread** или убедитесь, что вы уже находитесь в нем.</span><span class="sxs-lookup"><span data-stu-id="7fca4-222">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7fca4-223">Создайте файл `config.js` в любом удобном редакторе и добавьте в него следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="7fca4-223">Create a `config.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in to your server unless you use the common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in to your server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes to stderr in Unix.

         };
    ```
3. <span data-ttu-id="7fca4-224">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="7fca4-224">Save the file.</span></span>

## <a name="step-12-add-configuration-values-to-your-serverjs-file"></a><span data-ttu-id="7fca4-225">Шаг 12: Добавление значений конфигурации в файл server.js</span><span class="sxs-lookup"><span data-stu-id="7fca4-225">Step 12: Add configuration values to your server.js file</span></span>
<span data-ttu-id="7fca4-226">Нам нужно прочитать эти значения из файла конфигурации, созданного для нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7fca4-226">We need to read these values from the .config file that you created across our application.</span></span> <span data-ttu-id="7fca4-227">Для этого добавим в приложение файл с расширением .config в качестве требуемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="7fca4-227">To do this, we add the .config file as a required resource in our application.</span></span> <span data-ttu-id="7fca4-228">Затем мы настроим глобальные переменные, соответствующие переменным в документе config.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-228">Then we set the global variables to match the variables in the config.js document.</span></span>

1. <span data-ttu-id="7fca4-229">В окне командной строки перейдите в каталог **azuread** или убедитесь, что вы уже находитесь в нем.</span><span class="sxs-lookup"><span data-stu-id="7fca4-229">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7fca4-230">Откройте файл `server.js` в любом удобном редакторе и добавьте в него следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="7fca4-230">Open your `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="7fca4-231">Затем добавьте новый раздел в `server.js` со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="7fca4-231">Then add a new section to `server.js` with the following code:</span></span>

    ```Javascript
    var options = {
        // The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array to hold logged in users and the current logged in user (owner).
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

      // If the logging level is specified, switch to it.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="7fca4-232">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="7fca4-232">Save the file.</span></span>

## <a name="step-13-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="7fca4-233">Шаг 13. Добавление сведений о модели и схеме MongoDB с помощью Mongoose</span><span class="sxs-lookup"><span data-stu-id="7fca4-233">Step 13: Add The MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="7fca4-234">Теперь мы соберем все три файла, подготовленные на предыдущих шагах, и поместим их в службу REST API.</span><span class="sxs-lookup"><span data-stu-id="7fca4-234">Now all this preparation is going to start paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="7fca4-235">В этом руководстве для хранения наших задач мы будем использовать MongoDB, как упоминалось выше в шаге 4.</span><span class="sxs-lookup"><span data-stu-id="7fca4-235">For this walkthrough, we use MongoDB to store our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="7fca4-236">В файле `config.js`, который мы создали на шаге 11, для базы данных использовалось имя `tasklist`. Именно это имя мы указали в конце URL-адреса для подключения в параметре **mogoose_auth_local**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-236">In the `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at the end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="7fca4-237">Не нужно заранее создавать эту базу данных в MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7fca4-237">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="7fca4-238">MongoDB самостоятельно создаст ее при первом запуске нашего серверного приложения (если эта база данных еще не существует).</span><span class="sxs-lookup"><span data-stu-id="7fca4-238">Instead, MongoDB creates this for us on the first run of our server application (assuming that the database doesn't already exist).</span></span>

<span data-ttu-id="7fca4-239">Теперь, когда мы указали серверу, какую базу данных MongoDB мы хотим использовать, необходимо написать дополнительный код для создания модели и схемы задач для нашего сервера.</span><span class="sxs-lookup"><span data-stu-id="7fca4-239">Now that we've told the server which MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's tasks.</span></span>

### <a name="discussion-of-the-model"></a><span data-ttu-id="7fca4-240">Описание модели</span><span class="sxs-lookup"><span data-stu-id="7fca4-240">Discussion of the model</span></span>
<span data-ttu-id="7fca4-241">Мы используем очень простую модель схемы.</span><span class="sxs-lookup"><span data-stu-id="7fca4-241">Our schema model is simple.</span></span> <span data-ttu-id="7fca4-242">Вы можете дополнить ее в соответствии с потребностями.</span><span class="sxs-lookup"><span data-stu-id="7fca4-242">You expand it as required.</span></span>

<span data-ttu-id="7fca4-243">Name — имя исполнителя, назначенного для задачи.</span><span class="sxs-lookup"><span data-stu-id="7fca4-243">NAME: The name of the person who is assigned to the task.</span></span> <span data-ttu-id="7fca4-244">Тип **Строка**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-244">A **String**.</span></span>

<span data-ttu-id="7fca4-245">Task — это сама задача.</span><span class="sxs-lookup"><span data-stu-id="7fca4-245">TASK: The task itself.</span></span> <span data-ttu-id="7fca4-246">Тип **Строка**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-246">A **String**.</span></span>

<span data-ttu-id="7fca4-247">Date — запланированная дата выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="7fca4-247">DATE: The date that the task is due.</span></span> <span data-ttu-id="7fca4-248">Тип **Дата и время**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-248">A **DATETIME**.</span></span>

<span data-ttu-id="7fca4-249">Completed — флаг, обозначающий завершение задачи.</span><span class="sxs-lookup"><span data-stu-id="7fca4-249">COMPLETED: If the task has been completed or not.</span></span> <span data-ttu-id="7fca4-250">Тип **Логическое значение**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-250">A **BOOLEAN**.</span></span>

### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="7fca4-251">Создание схемы в коде</span><span class="sxs-lookup"><span data-stu-id="7fca4-251">Creating the schema in the code</span></span>
1. <span data-ttu-id="7fca4-252">В окне командной строки перейдите в каталог **azuread** или убедитесь, что вы уже находитесь в нем.</span><span class="sxs-lookup"><span data-stu-id="7fca4-252">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7fca4-253">Откройте файл `server.js` в любом удобном редакторе и добавьте следующие сведения под элементом конфигурации:</span><span class="sxs-lookup"><span data-stu-id="7fca4-253">Open your `server.js` file in your favorite editor, and then add the following information below the configuration entry:</span></span>

    ```Javascript
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema to store our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="7fca4-254">Как видно из кода, сначала мы создаем схему данных.</span><span class="sxs-lookup"><span data-stu-id="7fca4-254">As you can tell from the code, we create our schema first.</span></span> <span data-ttu-id="7fca4-255">Затем мы создаем объект модели, который используем для хранения наших данных во всех сегментах кода, где определяются **маршруты**.</span><span class="sxs-lookup"><span data-stu-id="7fca4-255">Then we create a model object that we use to store our data throughout the code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="7fca4-256">Шаг 14. Добавление маршрутов для сервера задач REST API</span><span class="sxs-lookup"><span data-stu-id="7fca4-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="7fca4-257">Теперь у нас есть модель базы данных, с которой можно работать. Давайте добавим маршруты, которые мы будем использовать для сервера REST API.</span><span class="sxs-lookup"><span data-stu-id="7fca4-257">Now that we have a database model to work with, let's add the routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="7fca4-258">О маршрутах в Restify</span><span class="sxs-lookup"><span data-stu-id="7fca4-258">About routes in Restify</span></span>
<span data-ttu-id="7fca4-259">Маршруты работают в Restify точно так же, как и при использовании стека Express.</span><span class="sxs-lookup"><span data-stu-id="7fca4-259">Routes work in Restify the same way they do in the Express stack.</span></span> <span data-ttu-id="7fca4-260">Вы определяете маршруты с помощью идентификатора URI, который, как предполагается, будут вызывать клиентские приложения.</span><span class="sxs-lookup"><span data-stu-id="7fca4-260">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="7fca4-261">Как правило, свои маршруты вы определяете в отдельном файле.</span><span class="sxs-lookup"><span data-stu-id="7fca4-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="7fca4-262">Для этого примера мы поместим маршруты прямо в файл server.js.</span><span class="sxs-lookup"><span data-stu-id="7fca4-262">For our purposes, we put our routes in the server.js file.</span></span> <span data-ttu-id="7fca4-263">Для систем в рабочей среде мы рекомендуем вынести их в отдельный файл.</span><span class="sxs-lookup"><span data-stu-id="7fca4-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="7fca4-264">Типичный шаблон Restify для маршрута выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7fca4-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep the server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="7fca4-265">Это базовый шаблон.</span><span class="sxs-lookup"><span data-stu-id="7fca4-265">This is the pattern at its most basic level.</span></span> <span data-ttu-id="7fca4-266">В Restify (как и в Express) доступны очень мощные функциональные возможности, например для определения типов приложений и выполнения сложной маршрутизации между несколькими конечными точками.</span><span class="sxs-lookup"><span data-stu-id="7fca4-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="7fca4-267">В нашем примере мы используем самые простые маршруты.</span><span class="sxs-lookup"><span data-stu-id="7fca4-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="7fca4-268">Добавление маршрутов по умолчанию на наш сервер</span><span class="sxs-lookup"><span data-stu-id="7fca4-268">Add default routes to our server</span></span>
<span data-ttu-id="7fca4-269">Теперь нужно добавить маршруты для базовых операций CRUD (создание, извлечение, обновление и удаление данных).</span><span class="sxs-lookup"><span data-stu-id="7fca4-269">We now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="7fca4-270">В окне командной строки перейдите в каталог **azuread** или убедитесь, что вы уже находитесь в нем.</span><span class="sxs-lookup"><span data-stu-id="7fca4-270">From the command line, change directories to the **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="7fca4-271">Откройте файл `server.js` в любом удобном редакторе и добавьте следующие сведения под ранее внесенными значениями для базы данных:</span><span class="sxs-lookup"><span data-stu-id="7fca4-271">Open the `server.js` file in your favorite editor, and then add the following information below the previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it to Mongodb.
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

/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

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
            log.warn(err, "There is no tasks in the database. Did you initialize the database as stated in the README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="7fca4-272">Добавление обработки ошибок в интерфейсы API</span><span class="sxs-lookup"><span data-stu-id="7fca4-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back to the client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="7fca4-273">Шаг 15. Создание сервера</span><span class="sxs-lookup"><span data-stu-id="7fca4-273">Step 15: Create your server</span></span>
<span data-ttu-id="7fca4-274">Мы уже определили базу данных и создали все маршруты.</span><span class="sxs-lookup"><span data-stu-id="7fca4-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="7fca4-275">Осталось только добавить экземпляр сервера, который обрабатывает вызовы.</span><span class="sxs-lookup"><span data-stu-id="7fca4-275">The last thing to do is add the server instance that manages our calls.</span></span>

<span data-ttu-id="7fca4-276">В Restify (и в Express) реализованы разные возможности для настройки сервера REST API. Но в этом примере мы снова ограничимся самым простым вариантом настройки.</span><span class="sxs-lookup"><span data-stu-id="7fca4-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going to use the most basic setup for our purposes.</span></span>

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

// Allow five requests per second by IP, and burst to 10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping to REST.
```

## <a name="step-16-add-the-routes-to-the-server-without-authentication-for-now"></a><span data-ttu-id="7fca4-277">Шаг 16. Добавление маршрутов на сервер (пока без аутентификации)</span><span class="sxs-lookup"><span data-stu-id="7fca4-277">Step 16: Add the routes to the server (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In the pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need to maintain session state. You can experiment with removing API protection
/* by removing the passport.authenticate() method as follows:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-the-server-before-adding-oauth-support"></a><span data-ttu-id="7fca4-278">Шаг 17. Запуск сервера (пока без поддержки OAuth)</span><span class="sxs-lookup"><span data-stu-id="7fca4-278">Step 17: Run the server (before adding OAuth support)</span></span>
<span data-ttu-id="7fca4-279">Прежде чем добавить аутентификацию, давайте протестируем сервер.</span><span class="sxs-lookup"><span data-stu-id="7fca4-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="7fca4-280">Проще всего это сделать с помощью curl из командной строки.</span><span class="sxs-lookup"><span data-stu-id="7fca4-280">The easiest way to test your server is by using curl in a command line.</span></span> <span data-ttu-id="7fca4-281">Но прежде чем выполнять тест, нужно подготовить служебную программу, которая сможет анализировать выходные данные в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="7fca4-281">Before we do that, we need a utility that allows us to parse output as JSON.</span></span>

1. <span data-ttu-id="7fca4-282">Установите средство для работы JSON, которое мы будем использовать во всех следующих примерах:</span><span class="sxs-lookup"><span data-stu-id="7fca4-282">Install the following JSON tool (all the following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="7fca4-283">Это обеспечивает глобальную установку средства JSON.</span><span class="sxs-lookup"><span data-stu-id="7fca4-283">This installs the JSON tool globally.</span></span> <span data-ttu-id="7fca4-284">Теперь все готово для экспериментов с сервером.</span><span class="sxs-lookup"><span data-stu-id="7fca4-284">Now that we’ve accomplished that, let’s play with the server:</span></span>

2. <span data-ttu-id="7fca4-285">Сначала убедитесь, что запущен экземпляр MongoDB:</span><span class="sxs-lookup"><span data-stu-id="7fca4-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="7fca4-286">Затем перейдите в другой каталог и запустите curl.</span><span class="sxs-lookup"><span data-stu-id="7fca4-286">Then, change to the directory and start curling:</span></span>

    <span data-ttu-id="7fca4-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="7fca4-287">`$ cd azuread` `$ node server.js`</span></span>

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

4. <span data-ttu-id="7fca4-288">Затем можно добавить задачу следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7fca4-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="7fca4-289">Ответ должен быть следующим:</span><span class="sxs-lookup"><span data-stu-id="7fca4-289">The response should be:</span></span>

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
    <span data-ttu-id="7fca4-290">Для перечисления задач для Brandon можно использовать следующий способ:</span><span class="sxs-lookup"><span data-stu-id="7fca4-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="7fca4-291">Если все это работает, можно добавить OAuth к нашему серверу REST API.</span><span class="sxs-lookup"><span data-stu-id="7fca4-291">If all this works, we're ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="7fca4-292">У вас уже есть сервер REST API с MongoDB!</span><span class="sxs-lookup"><span data-stu-id="7fca4-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="7fca4-293">Шаг 18. Подключение аутентификации для сервера REST API</span><span class="sxs-lookup"><span data-stu-id="7fca4-293">Step 18: Add authentication to our REST API server</span></span>
<span data-ttu-id="7fca4-294">Теперь, когда у нас запущен сервер REST API, мы можем использовать его для работы с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7fca4-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="7fca4-295">В окне командной строки перейдите в каталог **azuread** или убедитесь, что вы уже находитесь в нем.</span><span class="sxs-lookup"><span data-stu-id="7fca4-295">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="7fca4-296">Использование стратегии OIDCBearerStrategy, включенной в passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="7fca4-296">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="7fca4-297">Мы создали стандартный сервер REST TODO без какой-либо авторизации.</span><span class="sxs-lookup"><span data-stu-id="7fca4-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="7fca4-298">Самое время добавить такую функцию.</span><span class="sxs-lookup"><span data-stu-id="7fca4-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="7fca4-299">Сначала необходимо указать, что будет использоваться Passport.</span><span class="sxs-lookup"><span data-stu-id="7fca4-299">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="7fca4-300">Сделайте это сразу после конфигурации другого сервера:</span><span class="sxs-lookup"><span data-stu-id="7fca4-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="7fca4-301">При написании API-интерфейсов старайтесь связывать данные с уникальными параметрами маркера, которые пользователь не сможет подделать.</span><span class="sxs-lookup"><span data-stu-id="7fca4-301">When you write APIs, we recommend that you always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="7fca4-302">Когда наш сервер сохраняет элементы списка дел, он использует идентификатор объекта, используемый в маркере для пользователя (он хранится в свойстве token.oid), и помещает его в поле owner.</span><span class="sxs-lookup"><span data-stu-id="7fca4-302">When this server stores TODO items, it stores them based on the object ID of the user in the token (called through token.oid), which we put in the “owner” field.</span></span> <span data-ttu-id="7fca4-303">Благодаря этому только владелец сможет получить доступ к своим элементам списка дел.</span><span class="sxs-lookup"><span data-stu-id="7fca4-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="7fca4-304">Значение owner не отображается в API, поэтому внешний пользователь может запросить элементы списка дел другого пользователя, даже если он прошел проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="7fca4-304">There is no exposure in the API of “owner,” so an external user can request the TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="7fca4-305">Теперь мы применим стратегию носителя, которая поставляется вместе с `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="7fca4-305">Next let’s use the bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="7fca4-306">Просмотрите код, а остальное мы объясним чуть ниже.</span><span class="sxs-lookup"><span data-stu-id="7fca4-306">Look at the code for now and we'll explain the rest shortly.</span></span> <span data-ttu-id="7fca4-307">Вставьте этот текст после добавленного ранее:</span><span class="sxs-lookup"><span data-stu-id="7fca4-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling the OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides the need to manage users and info tokens
    /* with a FindorCreate() method that must be provided by the implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want to do something smarter.
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
            log.info('verifying the user');
            log.info(token, 'was the token retreived');
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

<span data-ttu-id="7fca4-308">Для Passport свойственно аналогичное поведение для всех стратегий (Twitter, Facebook и т. д.); это поведение учитывают все разработчики модулей стратегий.</span><span class="sxs-lookup"><span data-stu-id="7fca4-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="7fca4-309">Просматривая стратегию, можно увидеть, что она принимает функцию с параметрами token и done.</span><span class="sxs-lookup"><span data-stu-id="7fca4-309">Looking at the strategy, you see we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="7fca4-310">Стратегия будет возвращена, когда завершит свою работу.</span><span class="sxs-lookup"><span data-stu-id="7fca4-310">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="7fca4-311">После этого нам нужно сохранить пользователя и сохранить маркер, чтобы не запрашивать его каждый раз заново.</span><span class="sxs-lookup"><span data-stu-id="7fca4-311">After it does, we store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7fca4-312">Приведенный выше код обрабатывает данные о любом пользователе, который выполняет аутентификацию на сервере.</span><span class="sxs-lookup"><span data-stu-id="7fca4-312">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="7fca4-313">Это называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="7fca4-313">This is known as auto-registration.</span></span> <span data-ttu-id="7fca4-314">На рабочих серверах мы не рекомендуем разрешать вход без прохождения определенного процесса регистрации, который вы сочтете приемлемым.</span><span class="sxs-lookup"><span data-stu-id="7fca4-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="7fca4-315">Это типично для клиентских приложений, в которых разрешается регистрация через Facebook, но затем следуют запросы на предоставление дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="7fca4-315">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="7fca4-316">Если бы мы создавали обычную программу, а не простое средство для командной строки, мы могли бы извлечь адрес электронной почты из полученного объекта маркера и затем запросить у пользователя дополнительную информацию.</span><span class="sxs-lookup"><span data-stu-id="7fca4-316">If this wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="7fca4-317">Так как это всего лишь тестовый сервер, мы просто добавим пользователей в базу данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="7fca4-317">Because this is a test server, we simply add them to the in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="7fca4-318">Защита некоторых конечных точек</span><span class="sxs-lookup"><span data-stu-id="7fca4-318">Protect some endpoints</span></span>
<span data-ttu-id="7fca4-319">Для защиты конечных точек следует указать нужный протокол в вызове функции `passport.authenticate()`.</span><span class="sxs-lookup"><span data-stu-id="7fca4-319">You protect endpoints by specifying the `passport.authenticate()` call with the protocol that you want to use.</span></span>

<span data-ttu-id="7fca4-320">Можно изменить маршрут в коде сервера, чтобы сделать нечто более интересное.</span><span class="sxs-lookup"><span data-stu-id="7fca4-320">To make our server code do something more interesting, let’s edit the route.</span></span>

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

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="7fca4-321">Шаг 19. Снова запустите свой сервер приложения и убедитесь, что он вас отклоняет.</span><span class="sxs-lookup"><span data-stu-id="7fca4-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="7fca4-322">Снова используем `curl`, чтобы определить, если у нас сейчас защита OAuth2 применительно к нашим конечным точкам.</span><span class="sxs-lookup"><span data-stu-id="7fca4-322">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="7fca4-323">Этот тест мы выполним до того, как запускать клиентские пакеты SDK для этой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="7fca4-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="7fca4-324">Возвращенные заголовки должны подтвердить, что мы все сделали правильно.</span><span class="sxs-lookup"><span data-stu-id="7fca4-324">The headers that are returned should be enough to tell us if we're going down the right path.</span></span>

1. <span data-ttu-id="7fca4-325">Сначала убедитесь, что запущен экземпляр MongoDB:</span><span class="sxs-lookup"><span data-stu-id="7fca4-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="7fca4-326">Затем перейдите в рабочий каталог и запустите curl.</span><span class="sxs-lookup"><span data-stu-id="7fca4-326">Then, change to the directory and start curling.</span></span>

      <span data-ttu-id="7fca4-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="7fca4-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="7fca4-328">Попробуйте выполнить простую команду POST.</span><span class="sxs-lookup"><span data-stu-id="7fca4-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="7fca4-329">Здесь мы хотим увидеть именно ответ 401.</span><span class="sxs-lookup"><span data-stu-id="7fca4-329">A 401 is the response you are looking for here.</span></span> <span data-ttu-id="7fca4-330">Он указывает, что уровень Passport пытается перенаправить нас к конечной точке авторизации. Это именно то, что нам нужно.</span><span class="sxs-lookup"><span data-stu-id="7fca4-330">This response indicates that the Passport layer is trying to redirect to the authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fca4-331">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fca4-331">Next steps</span></span>
<span data-ttu-id="7fca4-332">Мы уже сделали с этим сервером все, что можно реализовать без использования клиента OAuth2.</span><span class="sxs-lookup"><span data-stu-id="7fca4-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="7fca4-333">Теперь вам будет нужно поработать с дополнительным пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="7fca4-333">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="7fca4-334">Теперь вы знаете, как реализовать интерфейс API REST с использованием Restify и OAuth2.</span><span class="sxs-lookup"><span data-stu-id="7fca4-334">You've now learned how to implement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="7fca4-335">У вас есть код, на основе которого можно продолжить разработку и освоить новые методы.</span><span class="sxs-lookup"><span data-stu-id="7fca4-335">You also have more than enough code to keep developing your service and learning how to build on this example.</span></span>

<span data-ttu-id="7fca4-336">Если вы намерены более подробно изучать ADAL, мы рекомендуем использовать поддерживаемые клиенты ADAL, которые указаны в списке ниже.</span><span class="sxs-lookup"><span data-stu-id="7fca4-336">If you are interested in the next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="7fca4-337">Клонируйте их на своем компьютере разработчика и настройте, как описано в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="7fca4-337">Clone down to your developer machine and configure as described in the walkthrough.</span></span>

[<span data-ttu-id="7fca4-338">ADAL для iOS</span><span class="sxs-lookup"><span data-stu-id="7fca4-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="7fca4-339">ADAL для Android</span><span class="sxs-lookup"><span data-stu-id="7fca4-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
