---
title: "Azure AD B2C: защита веб-API с помощью Node.js | Документация Майкрософт"
description: "Создание веб-API Node.js, который принимает токены от клиента B2C"
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
ms.openlocfilehash: 6480be75c314ede1b786e959a79c0385dd2edea8
ms.sourcegitcommit: 73f159cdbc122ffe42f3e1f7a3de05f77b6a4725
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="89dc2-103">Azure AD B2C: защита веб-API с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="89dc2-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="89dc2-104">С помощью Azure Active Directory (Azure AD) B2C можно защитить веб-API с помощью маркера доступа OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="89dc2-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="89dc2-105">Эти маркеры позволяют клиентским приложениям, использующим Azure AD B2C, проходить проверку подлинности для API.</span><span class="sxs-lookup"><span data-stu-id="89dc2-105">These tokens allow your client apps that use Azure AD B2C to authenticate to the API.</span></span> <span data-ttu-id="89dc2-106">В этой статье показано, как создать интерфейс веб-API .NET "Список дел", который позволяет пользователям добавлять и просматривать задачи.</span><span class="sxs-lookup"><span data-stu-id="89dc2-106">This article shows you how to create a "to-do list" API that allows users to add and list tasks.</span></span> <span data-ttu-id="89dc2-107">Этот веб-API защищен с помощью Azure AD B2C. Управлять списком дел могут только пользователи, прошедшие проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="89dc2-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="89dc2-108">Этот пример рассчитан на подключение с использованием [примера приложения iOS B2C](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="89dc2-108">This sample was written to be connected to by using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="89dc2-109">Сначала изучите это руководство, а затем переходите к указанному примеру.</span><span class="sxs-lookup"><span data-stu-id="89dc2-109">Do the current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="89dc2-110">**Passport** — промежуточный слой проверки подлинности для Node.js.</span><span class="sxs-lookup"><span data-stu-id="89dc2-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="89dc2-111">Гибкая модульная структура Passport позволяет незаметно устанавливать его в любом приложении на основе Express или в веб-приложении Restify.</span><span class="sxs-lookup"><span data-stu-id="89dc2-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="89dc2-112">Полный набор стратегий поддерживает проверку подлинности с помощью имени пользователя и пароля, Facebook, Twitter и других средств.</span><span class="sxs-lookup"><span data-stu-id="89dc2-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="89dc2-113">Мы разработали стратегию для Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89dc2-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="89dc2-114">Сначала следует установить этот модуль, а затем добавить подключаемый модуль Azure AD `passport-azure-ad` .</span><span class="sxs-lookup"><span data-stu-id="89dc2-114">You install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="89dc2-115">Для выполнения этого примера необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="89dc2-115">To do this sample, you need to:</span></span>

1. <span data-ttu-id="89dc2-116">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="89dc2-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="89dc2-117">настроить приложение для использования подключаемого модуля Passport `azure-ad-passport` ;</span><span class="sxs-lookup"><span data-stu-id="89dc2-117">Set up your application to use Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="89dc2-118">настроить клиентское приложение для вызова веб-API с именем to-do list.</span><span class="sxs-lookup"><span data-stu-id="89dc2-118">Configure a client application to call the "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="89dc2-119">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="89dc2-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="89dc2-120">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="89dc2-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="89dc2-121">Каталог — это контейнер для всех пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="89dc2-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="89dc2-122">Если каталог B2C еще не создан, [создайте его](active-directory-b2c-get-started.md), прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="89dc2-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="89dc2-123">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="89dc2-123">Create an application</span></span>
<span data-ttu-id="89dc2-124">Затем необходимо создать приложение в каталоге B2C. Оно будет передавать в Azure AD сведения, необходимые для безопасного взаимодействия с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="89dc2-124">Next, you need to create an app in your B2C directory that gives Azure AD some information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="89dc2-125">В нашем примере и клиентское приложение, и веб-API представлены одним **идентификатором приложения**, так как они представляют одно приложение логики.</span><span class="sxs-lookup"><span data-stu-id="89dc2-125">In this case, both the client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="89dc2-126">Создайте приложение, выполнив [эти указания](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="89dc2-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="89dc2-127">Не забудьте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="89dc2-127">Be sure to:</span></span>

* <span data-ttu-id="89dc2-128">Включите в приложение **веб-приложение или веб-API** .</span><span class="sxs-lookup"><span data-stu-id="89dc2-128">Include a **web app/web api** in the application</span></span>
* <span data-ttu-id="89dc2-129">Введите `http://localhost/TodoListService` в качестве **URL-адреса ответа**.</span><span class="sxs-lookup"><span data-stu-id="89dc2-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="89dc2-130">Это URL-адрес по умолчанию для данного примера кода.</span><span class="sxs-lookup"><span data-stu-id="89dc2-130">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="89dc2-131">Создайте для своего приложения **секрет приложения** и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="89dc2-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="89dc2-132">Эти данные понадобятся позже.</span><span class="sxs-lookup"><span data-stu-id="89dc2-132">You need this data later.</span></span> <span data-ttu-id="89dc2-133">Обратите внимание, что перед использованием это значение должно быть [экранировано для XML](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) .</span><span class="sxs-lookup"><span data-stu-id="89dc2-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="89dc2-134">Скопируйте **идентификатор приложения** , назначенный приложению.</span><span class="sxs-lookup"><span data-stu-id="89dc2-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="89dc2-135">Эти данные понадобятся позже.</span><span class="sxs-lookup"><span data-stu-id="89dc2-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="89dc2-136">Создание политик</span><span class="sxs-lookup"><span data-stu-id="89dc2-136">Create your policies</span></span>
<span data-ttu-id="89dc2-137">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="89dc2-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="89dc2-138">Это приложение содержит два действия с удостоверениями: регистрация и вход.</span><span class="sxs-lookup"><span data-stu-id="89dc2-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="89dc2-139">Вам нужно создать по одной политике каждого типа, как описано в [справочной статье о политиках](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="89dc2-139">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="89dc2-140">При создании трех политик обязательно выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="89dc2-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="89dc2-141">В политике регистрации укажите **отображаемое имя** и другие атрибуты регистрации.</span><span class="sxs-lookup"><span data-stu-id="89dc2-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="89dc2-142">Выберите утверждения приложения **Отображаемое имя** и **Идентификатор объекта** для каждой политики.</span><span class="sxs-lookup"><span data-stu-id="89dc2-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="89dc2-143">Можно также выбрать другие утверждения.</span><span class="sxs-lookup"><span data-stu-id="89dc2-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="89dc2-144">Скопируйте **имя** каждой политики после ее создания.</span><span class="sxs-lookup"><span data-stu-id="89dc2-144">Copy down the **Name** of each policy after you create it.</span></span> <span data-ttu-id="89dc2-145">У него должен быть префикс `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="89dc2-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="89dc2-146">Имена политик понадобятся вам позже.</span><span class="sxs-lookup"><span data-stu-id="89dc2-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="89dc2-147">Создав три политики, можно приступать к сборке приложения.</span><span class="sxs-lookup"><span data-stu-id="89dc2-147">After you have created your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="89dc2-148">Дополнительные сведения о работе политик в Azure AD B2C см. в [руководстве по началу работы с веб-приложениями .NET](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="89dc2-148">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-the-code"></a><span data-ttu-id="89dc2-149">Загрузка кода</span><span class="sxs-lookup"><span data-stu-id="89dc2-149">Download the code</span></span>
<span data-ttu-id="89dc2-150">Код для этого руководства размещен на портале [GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="89dc2-150">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="89dc2-151">Чтобы выполнить сборку примера, [скачайте схему проекта в ZIP-архиве](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="89dc2-151">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="89dc2-152">Ее также можно клонировать:</span><span class="sxs-lookup"><span data-stu-id="89dc2-152">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="89dc2-153">Кроме того, можно скачать готовое приложение [в виде ZIP-архива](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) или получить его из ветви `complete` того же репозитория.</span><span class="sxs-lookup"><span data-stu-id="89dc2-153">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="89dc2-154">Загрузка Node.js для платформы</span><span class="sxs-lookup"><span data-stu-id="89dc2-154">Download Node.js for your platform</span></span>
<span data-ttu-id="89dc2-155">Чтобы этот пример у вас заработал, потребуется рабочая установка Node.js.</span><span class="sxs-lookup"><span data-stu-id="89dc2-155">To successfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="89dc2-156">Установите Node.js с сайта [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="89dc2-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="89dc2-157">Установка MongoDB на платформе</span><span class="sxs-lookup"><span data-stu-id="89dc2-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="89dc2-158">Чтобы этот пример у вас заработал, потребуется рабочая установка MongoDB.</span><span class="sxs-lookup"><span data-stu-id="89dc2-158">To successfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="89dc2-159">MongoDB мы используем для того, чтобы интерфейс REST API устойчиво работал с несколькими экземплярами сервера.</span><span class="sxs-lookup"><span data-stu-id="89dc2-159">We use MongoDB to make your REST API persistent across server instances.</span></span>

<span data-ttu-id="89dc2-160">Установите MongoDB с сайта [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="89dc2-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="89dc2-161">В данном руководстве предполагается, что вы используете стандартный установочный пакет и стандартные конечные точки сервера для MongoDB. На момент написания статьи это `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="89dc2-161">This walk-through assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="89dc2-162">Установка модулей Restify для веб-API</span><span class="sxs-lookup"><span data-stu-id="89dc2-162">Install the Restify modules in your web API</span></span>
<span data-ttu-id="89dc2-163">Restify мы используем для сборки REST API.</span><span class="sxs-lookup"><span data-stu-id="89dc2-163">We use Restify to build your REST API.</span></span> <span data-ttu-id="89dc2-164">Restify — это минимальная гибкая платформа приложений Node.j, производная от Express.</span><span class="sxs-lookup"><span data-stu-id="89dc2-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="89dc2-165">Она располагает широким набором функций, позволяющих реализовать интерфейсы REST API поверх Connect.</span><span class="sxs-lookup"><span data-stu-id="89dc2-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="89dc2-166">Установка Restify</span><span class="sxs-lookup"><span data-stu-id="89dc2-166">Install Restify</span></span>
<span data-ttu-id="89dc2-167">В командной строке перейдите в каталог `azuread`.</span><span class="sxs-lookup"><span data-stu-id="89dc2-167">From the command line, change your directory to `azuread`.</span></span> <span data-ttu-id="89dc2-168">Если каталог `azuread` не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="89dc2-168">If the `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="89dc2-169">`cd azuread` или `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="89dc2-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="89dc2-170">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="89dc2-170">Enter the following command:</span></span>

`npm install restify`

<span data-ttu-id="89dc2-171">Эта команда устанавливает Restify.</span><span class="sxs-lookup"><span data-stu-id="89dc2-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="89dc2-172">Вы получили сообщение об ошибке?</span><span class="sxs-lookup"><span data-stu-id="89dc2-172">Did you get an error?</span></span>
<span data-ttu-id="89dc2-173">В некоторых операционных системах при использовании `npm` вы можете увидеть ошибку `Error: EPERM, chmod '/usr/local/bin/..'` и предложение запустить учетную запись с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="89dc2-173">In some operating systems, when you use `npm`, you may receive the error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run the account as an administrator.</span></span> <span data-ttu-id="89dc2-174">В этом случае необходимо с помощью команды `sudo` запустить `npm` с более высоким уровнем привилегий.</span><span class="sxs-lookup"><span data-stu-id="89dc2-174">If this problem occurs, use the `sudo` command to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="89dc2-175">Вы получили сообщение об ошибке DTrace?</span><span class="sxs-lookup"><span data-stu-id="89dc2-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="89dc2-176">При установке Restify вы можете увидеть что-то подобное:</span><span class="sxs-lookup"><span data-stu-id="89dc2-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="89dc2-177">Restify предоставляет мощный механизм для трассировки вызовов REST с помощью DTrace.</span><span class="sxs-lookup"><span data-stu-id="89dc2-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="89dc2-178">Однако во многих операционных системах DTrace отсутствует.</span><span class="sxs-lookup"><span data-stu-id="89dc2-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="89dc2-179">Эти ошибки можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="89dc2-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="89dc2-180">Результат этой команды должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89dc2-180">The output of the command should appear similar to this text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="89dc2-181">Установка Passport в веб-API</span><span class="sxs-lookup"><span data-stu-id="89dc2-181">Install Passport in your web API</span></span>
<span data-ttu-id="89dc2-182">В командной строке перейдите в каталог `azuread`, если он еще не выбран.</span><span class="sxs-lookup"><span data-stu-id="89dc2-182">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="89dc2-183">Установите Passport с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="89dc2-183">Install Passport using the following command:</span></span>

`npm install passport`

<span data-ttu-id="89dc2-184">Результат этой команды должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89dc2-184">The output of the command should be similar to this text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-to-your-web-api"></a><span data-ttu-id="89dc2-185">Добавление passport-azuread в веб-API</span><span class="sxs-lookup"><span data-stu-id="89dc2-185">Add passport-azuread to your web API</span></span>
<span data-ttu-id="89dc2-186">Добавьте стратегию OAuth с помощью набора стратегий `passport-azuread`, который устанавливает подключение Azure AD к Passport.</span><span class="sxs-lookup"><span data-stu-id="89dc2-186">Next, add the OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="89dc2-187">Используйте эту стратегию для токенов носителя в примере REST API.</span><span class="sxs-lookup"><span data-stu-id="89dc2-187">Use this strategy for bearer tokens in the REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="89dc2-188">Несмотря на то что OAuth2 предоставляет платформу, на которой может быть выдан токен любого известного типа, широкое распространение получили токены только некоторых типов.</span><span class="sxs-lookup"><span data-stu-id="89dc2-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="89dc2-189">Токены для защиты конечных точек являются токенами носителя.</span><span class="sxs-lookup"><span data-stu-id="89dc2-189">The tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="89dc2-190">Это самый распространенный тип токенов, которые выдаются в OAuth2.</span><span class="sxs-lookup"><span data-stu-id="89dc2-190">These types of tokens are the most widely issued in OAuth2.</span></span> <span data-ttu-id="89dc2-191">Во многих реализациях предполагается, что токены носителя — это единственный тип выданного токена.</span><span class="sxs-lookup"><span data-stu-id="89dc2-191">Many implementations assume that bearer tokens are the only type of token issued.</span></span>
>
>

<span data-ttu-id="89dc2-192">В командной строке перейдите в каталог `azuread`, если он еще не выбран.</span><span class="sxs-lookup"><span data-stu-id="89dc2-192">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="89dc2-193">Введите указанную ниже команду для установки модуля Passport `passport-azure-ad` :</span><span class="sxs-lookup"><span data-stu-id="89dc2-193">Install the Passport `passport-azure-ad` module using the following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="89dc2-194">Результат этой команды должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89dc2-194">The output of the command should be similar to this text:</span></span>

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

## <a name="add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="89dc2-195">Добавление модулей MongoDB в веб-API</span><span class="sxs-lookup"><span data-stu-id="89dc2-195">Add MongoDB modules to your web API</span></span>
<span data-ttu-id="89dc2-196">В этом примере для хранения данных используется MongoDB.</span><span class="sxs-lookup"><span data-stu-id="89dc2-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="89dc2-197">Для этого нужно установить Mongoose, широко используемый подключаемый модуль для управления моделями и схемами.</span><span class="sxs-lookup"><span data-stu-id="89dc2-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="89dc2-198">Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="89dc2-198">Install additional modules</span></span>
<span data-ttu-id="89dc2-199">Теперь необходимо установить остальные требуемые модули.</span><span class="sxs-lookup"><span data-stu-id="89dc2-199">Next, install the remaining required modules.</span></span>

<span data-ttu-id="89dc2-200">В командной строке перейдите в каталог `azuread`, если он еще не выбран.</span><span class="sxs-lookup"><span data-stu-id="89dc2-200">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="89dc2-201">Установите модули в каталог `node_modules` :</span><span class="sxs-lookup"><span data-stu-id="89dc2-201">Install the modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="89dc2-202">Создание файла server.js с зависимостями</span><span class="sxs-lookup"><span data-stu-id="89dc2-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="89dc2-203">Основная часть функций для сервера веб-API реализована в файле `server.js` .</span><span class="sxs-lookup"><span data-stu-id="89dc2-203">The `server.js` file provides the majority of the functionality for your Web API server.</span></span>

<span data-ttu-id="89dc2-204">В командной строке перейдите в каталог `azuread`, если он еще не выбран.</span><span class="sxs-lookup"><span data-stu-id="89dc2-204">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="89dc2-205">Создайте в текстовом редакторе файл `server.js` .</span><span class="sxs-lookup"><span data-stu-id="89dc2-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="89dc2-206">Добавьте следующие данные:</span><span class="sxs-lookup"><span data-stu-id="89dc2-206">Add the following information:</span></span>

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

<span data-ttu-id="89dc2-207">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="89dc2-207">Save the file.</span></span> <span data-ttu-id="89dc2-208">Он нам понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="89dc2-208">You return to it later.</span></span>

## <a name="create-a-configjs-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="89dc2-209">Создание файла config.js для хранения параметров Azure AD</span><span class="sxs-lookup"><span data-stu-id="89dc2-209">Create a config.js file to store your Azure AD settings</span></span>
<span data-ttu-id="89dc2-210">Данный фрагмент кода передает параметры конфигурации с вашего портала Azure AD в файл `Passport.js` .</span><span class="sxs-lookup"><span data-stu-id="89dc2-210">This code file passes the configuration parameters from your Azure AD Portal to the `Passport.js` file.</span></span> <span data-ttu-id="89dc2-211">Эти значения конфигурации были созданы во время добавления веб-интерфейса API на портал в первой части пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="89dc2-211">You created these configuration values when you added the web API to the portal in the first part of the walk-through.</span></span> <span data-ttu-id="89dc2-212">Сейчас мы объясним, какие значения нужно указать для этих параметров в скопированном фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="89dc2-212">We explain what to put in the values of these parameters after you copy the code.</span></span>

<span data-ttu-id="89dc2-213">В командной строке перейдите в каталог `azuread`, если он еще не выбран.</span><span class="sxs-lookup"><span data-stu-id="89dc2-213">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="89dc2-214">Создайте в текстовом редакторе файл `config.js` .</span><span class="sxs-lookup"><span data-stu-id="89dc2-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="89dc2-215">Добавьте следующие данные:</span><span class="sxs-lookup"><span data-stu-id="89dc2-215">Add the following information:</span></span>

```Javascript
// Don't commit this file to your public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in the portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // the Client ID of the application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add the B2C tenant name in the <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is the policy you'll want to validate against in B2C. Usually this is your Sign-in policy (as users sign in to this API)
passReqToCallback: false // This is a node.js construct that lets you pass the req all the way back to any upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="89dc2-216">Обязательные значения</span><span class="sxs-lookup"><span data-stu-id="89dc2-216">Required values</span></span>
<span data-ttu-id="89dc2-217">`clientID`: идентификатор клиента для приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="89dc2-217">`clientID`: The client ID of your Web API application.</span></span>

<span data-ttu-id="89dc2-218">`IdentityMetadata`: здесь `passport-azure-ad` будет искать данные конфигурации для поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="89dc2-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for the identity provider.</span></span> <span data-ttu-id="89dc2-219">Кроме того, здесь будет выполняться поиск ключей для проверки веб-токенов JSON.</span><span class="sxs-lookup"><span data-stu-id="89dc2-219">It also looks for the keys to validate the JSON web tokens.</span></span>

<span data-ttu-id="89dc2-220">`audience`: универсальный код ресурса (URI), который идентифицирует вашу службу. Его нужно взять на портале.</span><span class="sxs-lookup"><span data-stu-id="89dc2-220">`audience`: The uniform resource identifier (URI) from the portal that identifies your calling application.</span></span>

<span data-ttu-id="89dc2-221">`tenantName`: имя клиента (например, **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="89dc2-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="89dc2-222">`policyName`: политика проверки токенов, поступающих на сервер.</span><span class="sxs-lookup"><span data-stu-id="89dc2-222">`policyName`: The policy that you want to validate the tokens coming in to your server.</span></span> <span data-ttu-id="89dc2-223">Здесь нужно указать ту же политику, которую вы используете для входа в клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="89dc2-223">This policy should be the same policy that you use on the client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="89dc2-224">Пока что используйте одни и те же политики в параметрах клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="89dc2-224">For now, use the same policies across both client and server setup.</span></span> <span data-ttu-id="89dc2-225">Если вы уже выполнили действия из пошагового руководства и создали эти политики, делать это еще раз не требуется.</span><span class="sxs-lookup"><span data-stu-id="89dc2-225">If you have already completed a walk-through and created these policies, you don't need to do so again.</span></span> <span data-ttu-id="89dc2-226">Поскольку вы выполнили пошаговые инструкции, нет необходимости настраивать на сайте новые политики для клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="89dc2-226">Because you completed the walk-through, you shouldn't need to set up new policies for client walk-throughs on the site.</span></span>
>
>

## <a name="add-configuration-to-your-serverjs-file"></a><span data-ttu-id="89dc2-227">Добавление конфигурации в файл server.js</span><span class="sxs-lookup"><span data-stu-id="89dc2-227">Add configuration to your server.js file</span></span>
<span data-ttu-id="89dc2-228">Чтобы получить значения из файла `config.js`, добавьте в свое приложение файл `.config` в качестве обязательного ресурса, а затем настройте глобальные переменные для переменных, содержащихся в документе `config.js`.</span><span class="sxs-lookup"><span data-stu-id="89dc2-228">To read the values from the `config.js` file you created, add the `.config` file as a required resource in your application, and then set the global variables to those in the `config.js` document.</span></span>

<span data-ttu-id="89dc2-229">В командной строке перейдите в каталог `azuread`, если он еще не выбран.</span><span class="sxs-lookup"><span data-stu-id="89dc2-229">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="89dc2-230">Откройте файл `server.js` в редакторе.</span><span class="sxs-lookup"><span data-stu-id="89dc2-230">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="89dc2-231">Добавьте следующие данные:</span><span class="sxs-lookup"><span data-stu-id="89dc2-231">Add the following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="89dc2-232">Добавьте в `server.js` новый раздел со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="89dc2-232">Add a new section to `server.js` that includes the following code:</span></span>

```Javascript
// We pass these options in to the ODICBearerStrategy.

var options = {
    // The URL of the metadata document for your app. We put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="89dc2-233">Теперь добавьте заполнители для пользователей, которых мы получаем от наших вызывающих приложений.</span><span class="sxs-lookup"><span data-stu-id="89dc2-233">Next, let's add some placeholders for the users we receive from our calling applications.</span></span>

```Javascript
// array to hold logged in users and the current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="89dc2-234">Также создадим средство ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="89dc2-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="89dc2-235">Добавление сведений о модели и схеме MongoDB с помощью Moongoose</span><span class="sxs-lookup"><span data-stu-id="89dc2-235">Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="89dc2-236">Все, что мы сделали ранее, теперь поможет нам подключить все три файла к службе REST API.</span><span class="sxs-lookup"><span data-stu-id="89dc2-236">The earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="89dc2-237">В данном пошаговом руководстве используйте MongoDB для хранения задач, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="89dc2-237">For this walk-through, use MongoDB to store your tasks, as discussed earlier.</span></span>

<span data-ttu-id="89dc2-238">В файле `config.js` для имени базы данных указано значение **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="89dc2-238">In the `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="89dc2-239">Это же значение указывается в конце URL-адреса для подключения `mongoose_auth_local` .</span><span class="sxs-lookup"><span data-stu-id="89dc2-239">That name was also what you put at the end of the `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="89dc2-240">Не нужно заранее создавать эту базу данных в MongoDB.</span><span class="sxs-lookup"><span data-stu-id="89dc2-240">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="89dc2-241">База данных будет автоматически создана при первом запуске приложения сервера.</span><span class="sxs-lookup"><span data-stu-id="89dc2-241">It creates the database for you on the first run of your server application.</span></span>

<span data-ttu-id="89dc2-242">После того как вы укажете серверу, какую базу данных MongoDB необходимо использовать, вам потребуется написать дополнительный код, чтобы создать модель и схему для ваших задач на сервере.</span><span class="sxs-lookup"><span data-stu-id="89dc2-242">After you tell the server which MongoDB database to use, you need to write some additional code to create the model and schema for your server tasks.</span></span>

### <a name="expand-the-model"></a><span data-ttu-id="89dc2-243">Развертывание узла модели</span><span class="sxs-lookup"><span data-stu-id="89dc2-243">Expand the model</span></span>
<span data-ttu-id="89dc2-244">Эта модель схемы очень проста.</span><span class="sxs-lookup"><span data-stu-id="89dc2-244">This schema model is simple.</span></span> <span data-ttu-id="89dc2-245">При необходимости можно развернуть ее.</span><span class="sxs-lookup"><span data-stu-id="89dc2-245">You can expand it as required.</span></span>

<span data-ttu-id="89dc2-246">`owner`: кому назначено это задание.</span><span class="sxs-lookup"><span data-stu-id="89dc2-246">`owner`: Who is assigned to the task.</span></span> <span data-ttu-id="89dc2-247">Значение указывается в формате **string**(строка).</span><span class="sxs-lookup"><span data-stu-id="89dc2-247">This object is a **string**.</span></span>  

<span data-ttu-id="89dc2-248">`Text`: сама задача.</span><span class="sxs-lookup"><span data-stu-id="89dc2-248">`Text`: The task itself.</span></span> <span data-ttu-id="89dc2-249">Значение указывается в формате **string**(строка).</span><span class="sxs-lookup"><span data-stu-id="89dc2-249">This object is a **string**.</span></span>

<span data-ttu-id="89dc2-250">`date`: дата ожидаемого выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="89dc2-250">`date`: The date that the task is due.</span></span> <span data-ttu-id="89dc2-251">Значение указывается в формате **datetime**(дата и время).</span><span class="sxs-lookup"><span data-stu-id="89dc2-251">This object is a **datetime**.</span></span>

<span data-ttu-id="89dc2-252">`completed`: статус завершения задачи.</span><span class="sxs-lookup"><span data-stu-id="89dc2-252">`completed`: If the task is complete.</span></span> <span data-ttu-id="89dc2-253">Значение указывается в формате **Boolean**(логическое).</span><span class="sxs-lookup"><span data-stu-id="89dc2-253">This object is a **Boolean**.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="89dc2-254">Создание схемы в коде</span><span class="sxs-lookup"><span data-stu-id="89dc2-254">Create the schema in the code</span></span>
<span data-ttu-id="89dc2-255">В командной строке перейдите в каталог `azuread`, если он еще не выбран.</span><span class="sxs-lookup"><span data-stu-id="89dc2-255">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="89dc2-256">Откройте файл `server.js` в редакторе.</span><span class="sxs-lookup"><span data-stu-id="89dc2-256">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="89dc2-257">Добавьте следующие сведения под записью конфигурации:</span><span class="sxs-lookup"><span data-stu-id="89dc2-257">Add the following information below the configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect to MongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema to store our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use the schema to register a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="89dc2-258">Сначала создайте схему, а затем — объект модели для хранения данных, который вы используете в коде при определении **маршрутов**.</span><span class="sxs-lookup"><span data-stu-id="89dc2-258">You first create the schema, and then you create a model object that you use to store your data throughout the code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="89dc2-259">Добавление маршрутов для сервера задач REST API</span><span class="sxs-lookup"><span data-stu-id="89dc2-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="89dc2-260">Теперь модель базы данных готова к использованию. Добавьте маршруты, которые используются для сервера REST API.</span><span class="sxs-lookup"><span data-stu-id="89dc2-260">Now that you have a database model to work with, add the routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="89dc2-261">О маршрутах в Restify</span><span class="sxs-lookup"><span data-stu-id="89dc2-261">About routes in Restify</span></span>
<span data-ttu-id="89dc2-262">Маршруты работают в Restify точно так же, как при использовании стека Express.</span><span class="sxs-lookup"><span data-stu-id="89dc2-262">Routes work in Restify in the same way that they work when they use the Express stack.</span></span> <span data-ttu-id="89dc2-263">Вы определяете маршруты с помощью идентификатора URI, который, как предполагается, будут вызывать клиентские приложения.</span><span class="sxs-lookup"><span data-stu-id="89dc2-263">You define routes by using the URI that you expect the client applications to call.</span></span>

<span data-ttu-id="89dc2-264">Типичный шаблон для маршрута Restify выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="89dc2-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep the server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="89dc2-265">В Restify и Express доступны более мощные функциональные возможности, например определение типов приложений и выполнение сложной маршрутизации между разными конечными точками.</span><span class="sxs-lookup"><span data-stu-id="89dc2-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="89dc2-266">В этом руководстве мы будем использовать только простые маршруты.</span><span class="sxs-lookup"><span data-stu-id="89dc2-266">For the purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="89dc2-267">Добавление на сервер маршрутов по умолчанию</span><span class="sxs-lookup"><span data-stu-id="89dc2-267">Add default routes to your server</span></span>
<span data-ttu-id="89dc2-268">Теперь добавьте базовые маршруты CRUD для операций **create** (создание) и **list**(список) интерфейса REST API.</span><span class="sxs-lookup"><span data-stu-id="89dc2-268">You now add the basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="89dc2-269">Другие маршруты можно найти в ветви `complete` примера.</span><span class="sxs-lookup"><span data-stu-id="89dc2-269">Other routes can be found in the `complete` branch of the sample.</span></span>

<span data-ttu-id="89dc2-270">В командной строке перейдите в каталог `azuread`, если он еще не выбран.</span><span class="sxs-lookup"><span data-stu-id="89dc2-270">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="89dc2-271">Откройте файл `server.js` в редакторе.</span><span class="sxs-lookup"><span data-stu-id="89dc2-271">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="89dc2-272">Добавьте следующие сведения под записями о базе данных, которые вы добавили ранее:</span><span class="sxs-lookup"><span data-stu-id="89dc2-272">Below the database entries you made above add the following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it to Mongodb
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
            req.log.warn(err, 'createTask: unable to save');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

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
            log.warn(err, "There is no tasks in the database. Add one!");
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


#### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="89dc2-273">Добавление обработки ошибок для маршрутов</span><span class="sxs-lookup"><span data-stu-id="89dc2-273">Add error handling for the routes</span></span>
<span data-ttu-id="89dc2-274">Добавьте обработку ошибок, чтобы в понятной форме передавать клиенту данные о возникших проблемах.</span><span class="sxs-lookup"><span data-stu-id="89dc2-274">Add some error handling so that you can communicate any problems you encounter back to the client in a way that it can understand.</span></span>

<span data-ttu-id="89dc2-275">Добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="89dc2-275">Add the following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back to the client
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


## <a name="create-your-server"></a><span data-ttu-id="89dc2-276">Создание сервера</span><span class="sxs-lookup"><span data-stu-id="89dc2-276">Create your server</span></span>
<span data-ttu-id="89dc2-277">Теперь база данных определена, а маршруты созданы.</span><span class="sxs-lookup"><span data-stu-id="89dc2-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="89dc2-278">Осталось только добавить экземпляр сервера, который обрабатывает вызовы.</span><span class="sxs-lookup"><span data-stu-id="89dc2-278">The last thing for you to do is to add the server instance that manages your calls.</span></span>

<span data-ttu-id="89dc2-279">Restify и Express предоставляют широкие возможности для настройки сервера REST API, но здесь мы используем самый простой вариант.</span><span class="sxs-lookup"><span data-stu-id="89dc2-279">Restify and Express provide deep customization for a REST API server, but we use the most basic setup here.</span></span>

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

// Allow 5 requests/second by IP, and burst to 10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping to REST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-the-routes-to-the-server-without-authentication"></a><span data-ttu-id="89dc2-280">Добавление маршрутов на сервер (без проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="89dc2-280">Add the routes to the server (without authentication)</span></span>
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
    consoleMessage += '\n Open your browser to %s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-to-your-rest-api-server"></a><span data-ttu-id="89dc2-281">Добавление функции проверки подлинности на сервер REST API</span><span class="sxs-lookup"><span data-stu-id="89dc2-281">Add authentication to your REST API server</span></span>
<span data-ttu-id="89dc2-282">Теперь, когда есть работающий сервер REST API, можно подготовить его к использованию в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89dc2-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="89dc2-283">В командной строке перейдите в каталог `azuread`, если он еще не выбран.</span><span class="sxs-lookup"><span data-stu-id="89dc2-283">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="89dc2-284">Использование стратегии OIDCBearerStrategy, включенной в passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="89dc2-284">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="89dc2-285">При написании интерфейсов API обязательно нужно связывать данные с уникальными параметрами токена, которые пользователь не сможет подделать.</span><span class="sxs-lookup"><span data-stu-id="89dc2-285">When you write APIs, you should always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="89dc2-286">Этот сервер сохраняет элементы ToDo на основании **идентификатора объекта** пользователя, указанного в токене (свойство token.oid). Это значение сохраняется в поле owner.</span><span class="sxs-lookup"><span data-stu-id="89dc2-286">When the server stores ToDo items, it does so based on the **oid** of the user in the token (called through token.oid), which goes in the “owner” field.</span></span> <span data-ttu-id="89dc2-287">Благодаря этому только владелец сможет получить доступ к своим элементам ToDo.</span><span class="sxs-lookup"><span data-stu-id="89dc2-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="89dc2-288">Значение owner не отображается в API, поэтому внешний пользователь может запросить элементы ToDo другого пользователя, даже если он прошел проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="89dc2-288">There is no exposure in the API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="89dc2-289">Далее используйте стратегию носителя, которая поставляется с `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="89dc2-289">Next, use the bearer strategy that comes with `passport-azure-ad`.</span></span>

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
        log.info('verifying the user');
        log.info(token, 'was the token retreived');
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

<span data-ttu-id="89dc2-290">Passport использует стандартный шаблон для всех своих стратегий.</span><span class="sxs-lookup"><span data-stu-id="89dc2-290">Passport uses the same pattern for all its strategies.</span></span> <span data-ttu-id="89dc2-291">Вы передаете ему функцию `function()` с параметрами `token` и `done`.</span><span class="sxs-lookup"><span data-stu-id="89dc2-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="89dc2-292">Стратегия будет возвращена после выполнения всех задач.</span><span class="sxs-lookup"><span data-stu-id="89dc2-292">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="89dc2-293">Затем следует сохранить данные пользователя и токен, чтобы не задавать их в следующий раз повторно.</span><span class="sxs-lookup"><span data-stu-id="89dc2-293">You should then store the user and save the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89dc2-294">Приведенный выше код принимает всех пользователей, которые прошли проверку подлинности на сервере.</span><span class="sxs-lookup"><span data-stu-id="89dc2-294">The code above takes any user who happens to authenticate to your server.</span></span> <span data-ttu-id="89dc2-295">Этот процесс называется автоматической регистрацией.</span><span class="sxs-lookup"><span data-stu-id="89dc2-295">This process is known as autoregistration.</span></span> <span data-ttu-id="89dc2-296">На рабочих серверах нельзя разрешать пользователям использовать API без предварительной регистрации.</span><span class="sxs-lookup"><span data-stu-id="89dc2-296">In production servers, don't let in any users access the API without first having them go through a registration process.</span></span> <span data-ttu-id="89dc2-297">Такой подход обычно используется для клиентских приложений, которые позволяют войти с помощью учетной записи Facebook, а затем предлагают ввести дополнительную информацию.</span><span class="sxs-lookup"><span data-stu-id="89dc2-297">This process is usually the pattern you see in consumer apps that allow you to register by using Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="89dc2-298">В других вариантах, кроме запуска программы из командной строки, адрес электронной почты можно получить из возвращенного объекта токена, а после этого запросить у пользователя дополнительную информацию.</span><span class="sxs-lookup"><span data-stu-id="89dc2-298">If this program wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked users to fill out additional information.</span></span> <span data-ttu-id="89dc2-299">В нашем упрощенном примере мы сохраняем их в базу данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="89dc2-299">Because this is a sample, we add them to an in-memory database.</span></span>
>
>

## <a name="run-your-server-application-to-verify-that-it-rejects-you"></a><span data-ttu-id="89dc2-300">Запуск серверного приложения для подтверждения отказа в доступе</span><span class="sxs-lookup"><span data-stu-id="89dc2-300">Run your server application to verify that it rejects you</span></span>
<span data-ttu-id="89dc2-301">Вы можете использовать `curl` , чтобы определить, активирована ли защита OAuth2 применительно к конечным точкам.</span><span class="sxs-lookup"><span data-stu-id="89dc2-301">You can use `curl` to see if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="89dc2-302">Возвращенные заголовки должны подтвердить, что пока все сделано правильно.</span><span class="sxs-lookup"><span data-stu-id="89dc2-302">The headers returned should be enough to tell you that you are on the right path.</span></span>

<span data-ttu-id="89dc2-303">Убедитесь, что ваш экземпляр MongoDB работает.</span><span class="sxs-lookup"><span data-stu-id="89dc2-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="89dc2-304">Перейдите в нужный каталог и запустите сервер:</span><span class="sxs-lookup"><span data-stu-id="89dc2-304">Change to the directory and run the server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="89dc2-305">Запустите команду `curl`</span><span class="sxs-lookup"><span data-stu-id="89dc2-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="89dc2-306">Попробуйте выполнить базовую команду POST:</span><span class="sxs-lookup"><span data-stu-id="89dc2-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="89dc2-307">Если система функционирует правильно, отобразится сообщение об ошибке 401.</span><span class="sxs-lookup"><span data-stu-id="89dc2-307">A 401 error is the response you want.</span></span> <span data-ttu-id="89dc2-308">Это означает, что уровень Passport пытается выполнить перенаправление к конечной точке авторизации.</span><span class="sxs-lookup"><span data-stu-id="89dc2-308">It indicates that the Passport layer is trying to redirect to the authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="89dc2-309">Теперь у вас есть служба REST API, использующая OAuth2</span><span class="sxs-lookup"><span data-stu-id="89dc2-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="89dc2-310">Вы завершили создание REST API с использованием Restify и OAuth.</span><span class="sxs-lookup"><span data-stu-id="89dc2-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="89dc2-311">Этого кода будет достаточно, чтобы продолжить создание службы на основе предложенного примера.</span><span class="sxs-lookup"><span data-stu-id="89dc2-311">You now have sufficient code so that you can continue to develop your service and build on this example.</span></span> <span data-ttu-id="89dc2-312">До сих пор вы применяли этот сервер без использования клиента, совместимого с OAuth2.</span><span class="sxs-lookup"><span data-stu-id="89dc2-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="89dc2-313">На следующем этапе вам пригодятся дополнительные инструкции, которые есть, например, в пошаговом руководстве [Azure AD B2C: вызов веб-API из приложения iOS с использованием сторонней библиотеки](active-directory-b2c-devquickstarts-ios.md) .</span><span class="sxs-lookup"><span data-stu-id="89dc2-313">For that next step use an additional walk-through like our [Connect to a web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89dc2-314">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89dc2-314">Next steps</span></span>
<span data-ttu-id="89dc2-315">Теперь можно перейти к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="89dc2-315">You can now move to more advanced topics, such as:</span></span>

[<span data-ttu-id="89dc2-316">Подключение к веб-API с помощью iOS с B2C</span><span class="sxs-lookup"><span data-stu-id="89dc2-316">Connect to a web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
