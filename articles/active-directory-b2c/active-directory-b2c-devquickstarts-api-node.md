---
title: "Azure AD B2C: защита веб-API с помощью Node.js | Документация Майкрософт"
description: "Как toobuild Node.js веб-API, принимающий токены из клиента B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="e2e4b-103">Azure AD B2C: защита веб-API с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="e2e4b-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="e2e4b-104">С помощью Azure Active Directory (Azure AD) B2C можно защитить веб-API с помощью маркера доступа OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="e2e4b-105">Эти маркеры позволяют клиентских приложений, использующих Azure AD B2C tooauthenticate toohello API.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="e2e4b-106">В этой статье показано, как toocreate API «список дел», которая позволяет пользователям tooadd и список задач.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="e2e4b-107">веб-API Hello защищается с помощью Azure AD B2C и позволяет toomanage прошедшим проверку пользователям только их список дел.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="e2e4b-108">Этот образец был написан toobe подключены с помощью tooby наших [iOS B2C образец приложения](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="e2e4b-109">Сначала hello текущего руководство по применению, а затем следуйте вместе с этого образца.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="e2e4b-110">**Passport** — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="e2e4b-111">Гибкая модульная структура Passport позволяет незаметно устанавливать его в любом приложении на основе Express или в веб-приложении Restify.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="e2e4b-112">Полный набор стратегий поддерживает проверку подлинности с помощью имени пользователя и пароля, Facebook, Twitter и других средств.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="e2e4b-113">Мы разработали стратегию для Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e2e4b-114">Установите этот модуль и добавьте hello Azure AD `passport-azure-ad` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="e2e4b-115">toodo этот образец, необходимо:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="e2e4b-116">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e2e4b-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="e2e4b-117">Настройка вашего приложения toouse Passport `azure-ad-passport` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="e2e4b-118">Настройка клиентского приложения toocall hello «список дел» веб-API.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="e2e4b-119">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e2e4b-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="e2e4b-120">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="e2e4b-121">Каталог — это контейнер для всех пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="e2e4b-122">Если каталог B2C еще не создан, [создайте его](active-directory-b2c-get-started.md), прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="e2e4b-123">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="e2e4b-123">Create an application</span></span>
<span data-ttu-id="e2e4b-124">Далее необходимо toocreate приложения в каталоге B2C, которое предоставляет некоторые сведения, необходимые toosecurely Azure AD взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="e2e4b-125">В этом случае клиентское приложение hello и веб-API представлены одним **идентификатор приложения**, так как они включают в себя один логический приложения.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="e2e4b-126">toocreate приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="e2e4b-127">Не забудьте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-127">Be sure to:</span></span>

* <span data-ttu-id="e2e4b-128">Включить **веб-приложения и веб-api** в приложение hello</span><span class="sxs-lookup"><span data-stu-id="e2e4b-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="e2e4b-129">Введите `http://localhost/TodoListService` в качестве значения **URL-адреса ответа**.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="e2e4b-130">Это URL-адрес по умолчанию hello для этого примера кода.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="e2e4b-131">Создайте для своего приложения **секрет приложения** и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="e2e4b-132">Эти данные понадобятся позже.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-132">You need this data later.</span></span> <span data-ttu-id="e2e4b-133">Обратите внимание, что это значение должно toobe [XML переключения](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) перед его использованием.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="e2e4b-134">Копировать hello **идентификатор приложения** , назначенный tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="e2e4b-135">Эти данные понадобятся позже.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="e2e4b-136">Создание политик</span><span class="sxs-lookup"><span data-stu-id="e2e4b-136">Create your policies</span></span>
<span data-ttu-id="e2e4b-137">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="e2e4b-138">Это приложение содержит два действия с удостоверениями: регистрация и вход.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="e2e4b-139">Требуется одна политика toocreate каждого типа, как описано в [статье политики](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="e2e4b-140">При создании трех политик обязательно выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="e2e4b-141">Выберите hello **отображаемое имя** и другие атрибуты регистрации в политике организации доступа к Интернету.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="e2e4b-142">Выберите hello **отображаемое имя** и **идентификатор объекта** утверждений приложения в каждой политике.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="e2e4b-143">Можно также выбрать другие утверждения.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="e2e4b-144">Копировать вниз hello **имя** каждой политики, после его создания.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="e2e4b-145">Он должен иметь префикс hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="e2e4b-146">Имена политик понадобятся вам позже.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="e2e4b-147">После создания трех политик вы будете готовы toobuild приложения.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="e2e4b-148">toolearn о том, как работают политики в Azure AD B2C, начинаться с hello [.NET web app начало учебника](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="e2e4b-149">Загрузка кода hello</span><span class="sxs-lookup"><span data-stu-id="e2e4b-149">Download hello code</span></span>
<span data-ttu-id="e2e4b-150">Здравствуйте, код для этого учебника [сохраняется на сайте GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="e2e4b-151">Образец hello toobuild как можно перейти, вы можете [загрузить каркас проект как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="e2e4b-152">Также можно клонировать основу hello:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="e2e4b-153">также является приложение Hello завершения [доступны как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) или на hello `complete` ветви hello одного репозитория.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="e2e4b-154">Загрузка Node.js для платформы</span><span class="sxs-lookup"><span data-stu-id="e2e4b-154">Download Node.js for your platform</span></span>
<span data-ttu-id="e2e4b-155">в этом примере использовать toosuccessfully, состоящая из Node.js.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="e2e4b-156">Установите Node.js с сайта [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="e2e4b-157">Установка MongoDB на платформе</span><span class="sxs-lookup"><span data-stu-id="e2e4b-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="e2e4b-158">в этом примере использовать toosuccessfully, состоящая из MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="e2e4b-159">Мы используем MongoDB toomake постоянного REST API по экземплярам сервера.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="e2e4b-160">Установите MongoDB с сайта [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="e2e4b-161">Это пошаговое руководство предполагает, что можно использовать конечные точки установки и сервером по умолчанию hello для MongoDB, являющийся на момент написания этой статьи hello `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="e2e4b-162">Установка модулей Restify hello в веб-API</span><span class="sxs-lookup"><span data-stu-id="e2e4b-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="e2e4b-163">Мы используем Restify toobuild API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="e2e4b-164">Restify — это минимальная гибкая платформа приложений Node.j, производная от Express.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="e2e4b-165">Она располагает широким набором функций, позволяющих реализовать интерфейсы REST API поверх Connect.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="e2e4b-166">Установка Restify</span><span class="sxs-lookup"><span data-stu-id="e2e4b-166">Install Restify</span></span>
<span data-ttu-id="e2e4b-167">Из командной строки hello, измените каталог слишком`azuread`.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="e2e4b-168">Если hello `azuread` каталог не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="e2e4b-169">`cd azuread` или `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="e2e4b-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="e2e4b-170">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="e2e4b-171">Эта команда устанавливает Restify.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="e2e4b-172">Вы получили сообщение об ошибке?</span><span class="sxs-lookup"><span data-stu-id="e2e4b-172">Did you get an error?</span></span>
<span data-ttu-id="e2e4b-173">В некоторых операционных системах при использовании `npm`, появляется сообщение об ошибке hello `Error: EPERM, chmod '/usr/local/bin/..'` и запроса на выполнение hello учетной записи с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="e2e4b-174">При возникновении этой проблемы, используйте hello `sudo` toorun команда `npm` на более высоком уровне привилегий.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="e2e4b-175">Вы получили сообщение об ошибке DTrace?</span><span class="sxs-lookup"><span data-stu-id="e2e4b-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="e2e4b-176">При установке Restify вы можете увидеть что-то подобное:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="e2e4b-177">Restify предоставляет мощный механизм для трассировки вызовов REST с помощью DTrace.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="e2e4b-178">Однако во многих операционных системах DTrace отсутствует.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="e2e4b-179">Эти ошибки можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="e2e4b-180">аналогичный текст toothis должны быть выведены Hello hello команды:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-180">hello output of hello command should appear similar toothis text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="e2e4b-181">Установка Passport в веб-API</span><span class="sxs-lookup"><span data-stu-id="e2e4b-181">Install Passport in your web API</span></span>
<span data-ttu-id="e2e4b-182">Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="e2e4b-183">Установите службы Passport, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="e2e4b-184">Hello выходные данные команды hello должно быть аналогичный текст toothis:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="e2e4b-185">Добавить веб-API tooyour passport azuread</span><span class="sxs-lookup"><span data-stu-id="e2e4b-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="e2e4b-186">Добавьте стратегии hello OAuth с помощью `passport-azuread`, набор стратегии, которые подключения Azure AD с Passport.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="e2e4b-187">Используйте эту стратегию для маркеров носителя в образце hello REST API.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="e2e4b-188">Несмотря на то что OAuth2 предоставляет платформу, на которой может быть выдан токен любого известного типа, широкое распространение получили токены только некоторых типов.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="e2e4b-189">Hello маркеры для защиты конечных точек являются маркерами носителя.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="e2e4b-190">Эти типы маркеров являются наиболее широко выданных OAuth2 hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="e2e4b-191">Многие предполагают, что токены носителя являются единственным типом маркера, выданного hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="e2e4b-192">Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="e2e4b-193">Установка hello Passport `passport-azure-ad` модуля с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="e2e4b-194">Hello выходные данные команды hello должно быть аналогичный текст toothis:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-194">hello output of hello command should be similar toothis text:</span></span>

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="e2e4b-195">Добавить MongoDB модули tooyour веб-API</span><span class="sxs-lookup"><span data-stu-id="e2e4b-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="e2e4b-196">В этом примере для хранения данных используется MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="e2e4b-197">Для этого нужно установить Mongoose, широко используемый подключаемый модуль для управления моделями и схемами.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="e2e4b-198">Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="e2e4b-198">Install additional modules</span></span>
<span data-ttu-id="e2e4b-199">После этого установите hello оставшихся необходимые модули.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="e2e4b-200">Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e2e4b-201">Установка модулей hello в вашей `node_modules` каталога:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="e2e4b-202">Создание файла server.js с зависимостями</span><span class="sxs-lookup"><span data-stu-id="e2e4b-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="e2e4b-203">Hello `server.js` файл обеспечивает hello большую часть функций hello для сервера веб-API.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="e2e4b-204">Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e2e4b-205">Создайте в текстовом редакторе файл `server.js` .</span><span class="sxs-lookup"><span data-stu-id="e2e4b-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="e2e4b-206">Добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="e2e4b-207">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-207">Save hello file.</span></span> <span data-ttu-id="e2e4b-208">Возвращает tooit позже.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="e2e4b-209">Создать файл config.js toostore параметры Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2e4b-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="e2e4b-210">Этот файл код передает hello параметры конфигурации из вашего toohello портала Azure AD `Passport.js` файла.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="e2e4b-211">Эти значения конфигурации, созданный при добавлении API toohello hello веб-портала в первой части hello hello руководство по применению.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="e2e4b-212">После копирования кода hello рассказывается какие tooput hello значениями этих параметров.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="e2e4b-213">Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e2e4b-214">Создайте в текстовом редакторе файл `config.js` .</span><span class="sxs-lookup"><span data-stu-id="e2e4b-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="e2e4b-215">Добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="e2e4b-216">Обязательные значения</span><span class="sxs-lookup"><span data-stu-id="e2e4b-216">Required values</span></span>
<span data-ttu-id="e2e4b-217">`clientID`: hello идентификатор клиента приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="e2e4b-218">`IdentityMetadata`: Это место, куда `passport-azure-ad` ищет данные конфигурации для поставщика удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="e2e4b-219">Он также ищет веб-маркеры JSON hello hello ключи toovalidate.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="e2e4b-220">`audience`: hello универсальный код ресурса (URI) с портала hello, определяющий вызывающего приложения.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="e2e4b-221">`tenantName`: имя клиента (например, **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="e2e4b-222">`policyName`: hello политики, которую toovalidate токены hello, поступающие в tooyour server.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="e2e4b-223">Этот параметр должен быть hello же политики, используемого в клиентское приложение hello для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="e2e4b-224">Пока же hello использование политик для установки клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="e2e4b-225">Если вы уже выполнили Пошаговое руководство и создали эти политики, не требуется toodo и опять же.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="e2e4b-226">Поскольку вы выполнили Пошаговое руководство hello, не следует должны tooset копирование новых политик для клиентских приложений на сайте hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="e2e4b-227">Добавьте файл server.js tooyour конфигурации</span><span class="sxs-lookup"><span data-stu-id="e2e4b-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="e2e4b-228">значения hello tooread из hello `config.js` файл был создан, добавить hello `.config` файл как необходимый ресурс в приложении, а затем задайте toothose hello глобальные переменные в hello `config.js` документа.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="e2e4b-229">Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e2e4b-230">Откройте hello `server.js` файл в редакторе.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="e2e4b-231">Добавьте hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="e2e4b-232">Добавить новый раздел слишком`server.js` , включающего hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="e2e4b-233">Далее добавим некоторые заполнители для пользователей hello, мы получаем от вызывающего приложения.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="e2e4b-234">Также создадим средство ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="e2e4b-235">Добавить hello MongoDB модели и данные схемы с помощью Mongoose</span><span class="sxs-lookup"><span data-stu-id="e2e4b-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="e2e4b-236">Hello предыдущих подготовки обеспечивает как вводить эти три файла друг с другом в службе REST API.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="e2e4b-237">Для этого пошагового руководства используйте MongoDB toostore задач, как было сказано ранее.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="e2e4b-238">В hello `config.js` файла, именем базы данных **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="e2e4b-239">Это имя также было поместить в конце hello hello `mongoose_auth_local` URL-адрес подключения.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="e2e4b-240">Не нужно toocreate базы данных, заранее в MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="e2e4b-241">Hello базы данных создается автоматически при первом запуске серверное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="e2e4b-242">После сообщить hello server какие toouse базы данных MongoDB, необходимо toowrite некоторые модели hello toocreate дополнительного кода и схемы для сервера задач.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="e2e4b-243">Разверните узел модели hello</span><span class="sxs-lookup"><span data-stu-id="e2e4b-243">Expand hello model</span></span>
<span data-ttu-id="e2e4b-244">Эта модель схемы очень проста.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-244">This schema model is simple.</span></span> <span data-ttu-id="e2e4b-245">При необходимости можно развернуть ее.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-245">You can expand it as required.</span></span>

<span data-ttu-id="e2e4b-246">`owner`: Кто назначается toohello задачи.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="e2e4b-247">Значение указывается в формате **string**(строка).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-247">This object is a **string**.</span></span>  

<span data-ttu-id="e2e4b-248">`Text`: саму задачу hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-248">`Text`: hello task itself.</span></span> <span data-ttu-id="e2e4b-249">Значение указывается в формате **string**(строка).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-249">This object is a **string**.</span></span>

<span data-ttu-id="e2e4b-250">`date`: hello Дата выполнения этой задачи hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="e2e4b-251">Значение указывается в формате **datetime**(дата и время).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-251">This object is a **datetime**.</span></span>

<span data-ttu-id="e2e4b-252">`completed`: Если hello задача завершена.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="e2e4b-253">Значение указывается в формате **Boolean**(логическое).</span><span class="sxs-lookup"><span data-stu-id="e2e4b-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="e2e4b-254">Создание схемы hello в коде hello</span><span class="sxs-lookup"><span data-stu-id="e2e4b-254">Create hello schema in hello code</span></span>
<span data-ttu-id="e2e4b-255">Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e2e4b-256">Откройте hello `server.js` файл в редакторе.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="e2e4b-257">Добавьте следующую информацию ниже запись конфигурации hello hello:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="e2e4b-258">Сначала создается схема hello и создайте объект модели, используемой toostore данных по всему hello кода при определении вашей **маршруты**.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="e2e4b-259">Добавление маршрутов для сервера задач REST API</span><span class="sxs-lookup"><span data-stu-id="e2e4b-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="e2e4b-260">Теперь, когда toowork модели базы данных с помощью добавления hello маршрутов, которые можно использовать для сервера REST API.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="e2e4b-261">О маршрутах в Restify</span><span class="sxs-lookup"><span data-stu-id="e2e4b-261">About routes in Restify</span></span>
<span data-ttu-id="e2e4b-262">Маршруты работать в Restify в hello таким же способом, что они работают при использовании стека Express hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="e2e4b-263">Определения маршрутов с помощью hello URI, что предполагается toocall приложения hello клиента.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="e2e4b-264">Типичный шаблон для маршрута Restify выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="e2e4b-265">В Restify и Express доступны более мощные функциональные возможности, например определение типов приложений и выполнение сложной маршрутизации между разными конечными точками.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="e2e4b-266">Для целей этого учебника hello нам усложнять эти маршруты.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="e2e4b-267">Добавление сервера tooyour маршруты по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e2e4b-267">Add default routes tooyour server</span></span>
<span data-ttu-id="e2e4b-268">Теперь добавьте hello основные CRUD маршрутам **создания** и **списка** для наших API REST.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="e2e4b-269">Другие маршруты можно найти в hello `complete` ветви образца hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="e2e4b-270">Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="e2e4b-271">Откройте hello `server.js` файл в редакторе.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="e2e4b-272">Ниже записи в базе данных hello внесенные выше добавить hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="e2e4b-273">Добавьте обработку ошибок для маршрутов hello</span><span class="sxs-lookup"><span data-stu-id="e2e4b-273">Add error handling for hello routes</span></span>
<span data-ttu-id="e2e4b-274">Добавление обработки ошибок, чтобы вы могли взаимодействовать проблемы возникают задней toohello клиента, в результате которого оно было понятно.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="e2e4b-275">Добавьте следующий код hello:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a><span data-ttu-id="e2e4b-276">Создание сервера</span><span class="sxs-lookup"><span data-stu-id="e2e4b-276">Create your server</span></span>
<span data-ttu-id="e2e4b-277">Теперь база данных определена, а маршруты созданы.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="e2e4b-278">Hello худшее вы toodo — экземпляр сервера hello tooadd, который управляет вызовов.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="e2e4b-279">Restify Express предоставляют обширные возможности для настройки сервера REST API, а вариант установки основных hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="e2e4b-280">Добавление сервера toohello маршруты hello (без проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="e2e4b-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="e2e4b-281">Добавление сервера API-интерфейса REST tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="e2e4b-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="e2e4b-282">Теперь, когда есть работающий сервер REST API, можно подготовить его к использованию в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="e2e4b-283">Из командной строки hello, измените каталог слишком`azuread`, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="e2e4b-284">Использовать hello OIDCBearerStrategy, который входит в состав passport azure ad</span><span class="sxs-lookup"><span data-stu-id="e2e4b-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="e2e4b-285">При написании API, следует всегда связывать уникальный из токена hello, hello пользователя toosomething данных hello подменить.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="e2e4b-286">Когда элементы ToDo хранятся на сервере hello, используется таким образом на основании hello **oid** пользователя hello в маркере hello (называемые через token.oid), который переходит в поле hello «владелец».</span><span class="sxs-lookup"><span data-stu-id="e2e4b-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="e2e4b-287">Благодаря этому только владелец сможет получить доступ к своим элементам ToDo.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="e2e4b-288">Нет отсутствие проблем в hello API «владелец», поэтому внешний пользователь может запросить элементов ToDo других пользователей, даже если они проходят проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="e2e4b-289">Затем с помощью стратегии носителя hello, входящий в состав `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="e2e4b-290">Passport использует hello же шаблон для всех стратегий.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="e2e4b-291">Вы передаете ему функцию `function()` с параметрами `token` и `done`.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="e2e4b-292">Стратегия Hello возвращаются tooyou после его всю свою работу.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="e2e4b-293">Следует хранить пользователя hello и сохранить токен hello tooask для него не требуется еще раз.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2e4b-294">Приведенный выше код Hello принимает любой пользователь, который происходит tooauthenticate tooyour сервера.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="e2e4b-295">Этот процесс называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-295">This process is known as autoregistration.</span></span> <span data-ttu-id="e2e4b-296">В рабочей среде не позволяйте в любой API hello доступа пользователей без необходимости их пройти процесс регистрации.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="e2e4b-297">Этот процесс обычно является шаблон hello в пользовательские приложения, которые позволяет tooregister с помощью Facebook, а затем попросите toofill дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="e2e4b-298">Если эта программа не была программы командной строки, нам удалось извлекли hello электронной почты из hello токен объекта, который возвращается и затем предложено toofill пользователям Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="e2e4b-299">Так как это образец мы их добавить tooan базы данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="e2e4b-300">Запустите tooverify приложения на сервере что он отклоняет вы</span><span class="sxs-lookup"><span data-stu-id="e2e4b-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="e2e4b-301">Можно использовать `curl` toosee при наличии защиты OAuth2 теперь для конечных точек.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="e2e4b-302">Hello возвращены заголовки должно быть достаточно tootell, вы используете правильный путь hello.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="e2e4b-303">Убедитесь, что ваш экземпляр MongoDB работает.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="e2e4b-304">Измените каталог toohello и выполнения hello server:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="e2e4b-305">Запустите команду `curl`</span><span class="sxs-lookup"><span data-stu-id="e2e4b-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="e2e4b-306">Попробуйте выполнить базовую команду POST:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="e2e4b-307">Ошибку 401 — ответ hello, которые нужно.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="e2e4b-308">Указывает, откуда Passport hello пытается tooredirect toohello конечной точки для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="e2e4b-309">Теперь у вас есть служба REST API, использующая OAuth2</span><span class="sxs-lookup"><span data-stu-id="e2e4b-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="e2e4b-310">Вы завершили создание REST API с использованием Restify и OAuth.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="e2e4b-311">Теперь у вас есть достаточные кода, можно продолжить toodevelop службы и сборку в этом примере.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="e2e4b-312">До сих пор вы применяли этот сервер без использования клиента, совместимого с OAuth2.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="e2e4b-313">Для данного шага далее использовать дополнительные руководство по применению как нашей [подключения tooa веб-API с помощью операций ввода-вывода с B2C](active-directory-b2c-devquickstarts-ios.md) Пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="e2e4b-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2e4b-314">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2e4b-314">Next steps</span></span>
<span data-ttu-id="e2e4b-315">Теперь можно переместить toomore дополнительные разделы, такие как:</span><span class="sxs-lookup"><span data-stu-id="e2e4b-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="e2e4b-316">Подключиться с помощью операций ввода-вывода с B2C tooa веб-API</span><span class="sxs-lookup"><span data-stu-id="e2e4b-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
