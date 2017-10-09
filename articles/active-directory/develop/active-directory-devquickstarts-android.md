---
title: "Приступая к работе AD Android aaaAzure | Документы Microsoft"
description: "Как toobuild приложение Android, которое интегрируется с Azure AD для входа в систему и вызовы Azure AD защищены API-интерфейсов с помощью OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="9883f-103">Интеграция Azure AD в приложение для Android</span><span class="sxs-lookup"><span data-stu-id="9883f-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="9883f-104">Испытать предварительную версию hello нашим новым [портал разработчиков](https://identity.microsoft.com/Docs/Android), который поможет вам приступить к работе с Azure AD через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="9883f-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="9883f-105">портал разработчиков Hello поможет hello процесса регистрации приложения и интеграции Azure AD в коде.</span><span class="sxs-lookup"><span data-stu-id="9883f-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="9883f-106">Завершив работу, вы получите простое приложение, с помощью которого выполняется проверка подлинности пользователей в клиенте и на сервере, принимающем маркеры и проводящем проверку.</span><span class="sxs-lookup"><span data-stu-id="9883f-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="9883f-107">При разработке настольного приложения, Azure Active Directory (Azure AD) упрощает простыми и понятными для вас tooauthenticate пользователей с помощью своих локальных учетных записей Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9883f-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="9883f-108">Toosecurely вашего приложения также позволяет использовать любой веб-API, защищенные Azure AD, таких как hello API Office 365 или hello Azure API.</span><span class="sxs-lookup"><span data-stu-id="9883f-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="9883f-109">Для Android клиентов, которые нужно tooaccess защищенных ресурсов Azure AD предоставляет hello библиотеку проверки подлинности Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="9883f-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="9883f-110">Цель Hello ADAL — toomake легко и маркеры доступа tooget вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9883f-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="9883f-111">Это, мы создадим приложение Android список дел, насколько просто toodemonstrate:</span><span class="sxs-lookup"><span data-stu-id="9883f-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="9883f-112">Получает маркеры для вызова API списка задач с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="9883f-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="9883f-113">получает список дел пользователя;</span><span class="sxs-lookup"><span data-stu-id="9883f-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="9883f-114">выполняет выход из системы для пользователей.</span><span class="sxs-lookup"><span data-stu-id="9883f-114">Signs out users.</span></span>

<span data-ttu-id="9883f-115">tooget к работе, потребуется клиент Azure AD, в котором можно создавать пользователей и зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="9883f-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="9883f-116">Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="9883f-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="9883f-117">Шаг 1: Загрузите и запустите сервер образец hello Node.js REST API TODO</span><span class="sxs-lookup"><span data-stu-id="9883f-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="9883f-118">Образец Hello Node.js REST API TODO написан специально toowork с существующие выборка для создания задачи REST API одного клиента для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9883f-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="9883f-119">Это является необходимым условием для hello быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="9883f-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="9883f-120">Сведения о как tooset это, просмотреть наши примеры, существующие в [Microsoft службы Azure Active Directory образец REST API для Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9883f-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="9883f-121">Этап 2. Регистрация веб-API с помощью клиента Azure AD</span><span class="sxs-lookup"><span data-stu-id="9883f-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="9883f-122">Служба каталогов Active Directory позволяет добавлять приложения двух типов:</span><span class="sxs-lookup"><span data-stu-id="9883f-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="9883f-123">Веб-API, которые предоставляют службы toousers</span><span class="sxs-lookup"><span data-stu-id="9883f-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="9883f-124">Запущенное (на веб-hello или на устройстве), открыть веб-API</span><span class="sxs-lookup"><span data-stu-id="9883f-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="9883f-125">На этом шаге регистрация hello веб-API, у вас локально для тестирования этого образца.</span><span class="sxs-lookup"><span data-stu-id="9883f-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="9883f-126">Как правило этот веб-API — службы REST, функциональные возможности предложения, которые должны tooaccess приложения.</span><span class="sxs-lookup"><span data-stu-id="9883f-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="9883f-127">Azure AD может помочь защитить любую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="9883f-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="9883f-128">Мы при условии, что регистрации hello вышеупомянутым API REST TODO.</span><span class="sxs-lookup"><span data-stu-id="9883f-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="9883f-129">Но это применимо к любой веб-API, необходимо защитить toohelp Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9883f-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="9883f-130">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9883f-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9883f-131">На верхней панели hello выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="9883f-131">On hello top bar, click your account.</span></span> <span data-ttu-id="9883f-132">В hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="9883f-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="9883f-133">Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9883f-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9883f-134">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9883f-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="9883f-135">Введите понятное имя для приложения hello (например, **TodoListService**), выберите **веб-приложение или веб-API**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9883f-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="9883f-136">Образец hello hello входа URL-адрес, введите базовый URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="9883f-137">По умолчанию это `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="9883f-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="9883f-138">Нажмите кнопку **ОК** toocomplete hello регистрации.</span><span class="sxs-lookup"><span data-stu-id="9883f-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="9883f-139">Во время по-прежнему hello портал Azure, переход на страницу приложения tooyour, найдите значение идентификатора приложения hello и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="9883f-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="9883f-140">Оно понадобится позже при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="9883f-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="9883f-141">Из hello **параметры** -> **свойства** страницы, обновите URI идентификатора приложения hello - введите `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="9883f-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="9883f-142">Замените `<your_tenant_name>` с именем hello вашего клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9883f-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="9883f-143">Шаг 3: Регистрация приложения Android Native Client образец hello</span><span class="sxs-lookup"><span data-stu-id="9883f-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="9883f-144">В этом примере необходимо зарегистрировать веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="9883f-144">You must register your web application in this sample.</span></span> <span data-ttu-id="9883f-145">Это позволяет toocommunicate вашего приложения с только что зарегистрированные веб-hello API.</span><span class="sxs-lookup"><span data-stu-id="9883f-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="9883f-146">Azure AD будет отказывать в приеме tooeven разрешить tooask вашего приложения для входа в систему, когда он зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="9883f-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="9883f-147">Который является частью безопасности hello hello модели.</span><span class="sxs-lookup"><span data-stu-id="9883f-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="9883f-148">Мы при условии, что регистрации пример приложения hello, ссылка на более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="9883f-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="9883f-149">Но эта процедура подходит для любого приложения, которое вы разрабатываете.</span><span class="sxs-lookup"><span data-stu-id="9883f-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="9883f-150">Может возникнуть вопрос, почему приложение и веб-интерфейс API размещаются в одном клиенте?</span><span class="sxs-lookup"><span data-stu-id="9883f-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="9883f-151">Как вы могли догадаться, можно создать приложение, которое обращается к внешнему интерфейсу API, зарегистрированному в Azure AD из другого клиента.</span><span class="sxs-lookup"><span data-stu-id="9883f-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="9883f-152">Если это сделать, клиентам будет предложено использование toohello tooconsent hello API приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="9883f-153">Библиотека проверки подлинности Active Directory для iOS выполняет все необходимые операции для обработки данного согласия.</span><span class="sxs-lookup"><span data-stu-id="9883f-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="9883f-154">Мы исследуем дополнительных функций, вы увидите, что это является важной частью работы hello необходимые tooaccess набор hello интерфейсы API Microsoft Azure и Office, а также любой другой поставщик службы.</span><span class="sxs-lookup"><span data-stu-id="9883f-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="9883f-155">Сейчас, так как вы зарегистрировали веб-API и тестируемое приложение hello же клиента, вы не увидите каких-либо запросов согласия.</span><span class="sxs-lookup"><span data-stu-id="9883f-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="9883f-156">Это обычно hello вариант, если вы разрабатываете приложения только для собственных toouse компании.</span><span class="sxs-lookup"><span data-stu-id="9883f-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="9883f-157">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9883f-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9883f-158">На верхней панели hello выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="9883f-158">On hello top bar, click your account.</span></span> <span data-ttu-id="9883f-159">В hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="9883f-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="9883f-160">Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9883f-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9883f-161">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9883f-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="9883f-162">Введите понятное имя для приложения hello (например, **TodoListClient Android**), выберите **собственное клиентское приложение**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9883f-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="9883f-163">URI перенаправления hello, введите `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="9883f-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="9883f-164">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="9883f-164">Click **Finish**.</span></span>
7. <span data-ttu-id="9883f-165">Страница "приложение" hello найти значение идентификатора приложения hello и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="9883f-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="9883f-166">Оно понадобится позже при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="9883f-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="9883f-167">Из hello **параметры** выберите **требуемые разрешения** и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="9883f-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="9883f-168">Найдите и выберите TodoListService, добавьте hello **TodoListService доступа** разрешение в списке **делегированные разрешения**и нажмите кнопку **сделать**.</span><span class="sxs-lookup"><span data-stu-id="9883f-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="9883f-169">pom.xml toobuild с Maven, можно использовать на верхнем уровне hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="9883f-170">Клонируйте этот репозиторий в любой каталог по своему усмотрению:</span><span class="sxs-lookup"><span data-stu-id="9883f-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="9883f-171">Следуйте указаниям hello hello [tooset необходимых компонентов, настройку среды Maven для Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="9883f-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="9883f-172">Настройте эмулятор hello с SDK 19.</span><span class="sxs-lookup"><span data-stu-id="9883f-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="9883f-173">Go toohello корневую папку, где клонирования репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="9883f-174">Выполните следующую команду: `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="9883f-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="9883f-175">Изменение образца hello каталог toohello быстрого запуска.`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="9883f-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="9883f-176">Выполните следующую команду: `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="9883f-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="9883f-177">Вы увидите запуск приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="9883f-178">Введите tootry учетные данные тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="9883f-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="9883f-179">Будут отправлены пакеты JAR рядом с hello AAR пакета.</span><span class="sxs-lookup"><span data-stu-id="9883f-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="9883f-180">Шаг 4: Загрузите hello Android ADAL и добавить его в рабочей области Eclipse tooyour</span><span class="sxs-lookup"><span data-stu-id="9883f-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="9883f-181">Мы упрощенной для вас toohave несколько параметров toouse ADAL в проекте Android:</span><span class="sxs-lookup"><span data-stu-id="9883f-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="9883f-182">Можно использовать эту библиотеку hello исходного кода tooimport в Eclipse и связать приложение tooyour.</span><span class="sxs-lookup"><span data-stu-id="9883f-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="9883f-183">Если вы используете Android Studio, можно использовать hello AAR пакета формат и ссылка hello двоичных файлов.</span><span class="sxs-lookup"><span data-stu-id="9883f-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="9883f-184">Способ 1: ZIP-архив с файлами исходного кода</span><span class="sxs-lookup"><span data-stu-id="9883f-184">Option 1: Source Zip</span></span>
<span data-ttu-id="9883f-185">Щелкните toodownload копию исходного кода hello, **загрузить ZIP** hello правой части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="9883f-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="9883f-186">Или [скачайте его с GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="9883f-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="9883f-187">Способ 2: исходные файлы через Git</span><span class="sxs-lookup"><span data-stu-id="9883f-187">Option 2: Source via Git</span></span>
<span data-ttu-id="9883f-188">исходный код hello tooget hello пакет SDK через Git, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9883f-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="9883f-189">Способ 3: двоичные файлы через Gradle</span><span class="sxs-lookup"><span data-stu-id="9883f-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="9883f-190">Двоичные файлы hello можно получить из центрального репозитория hello Maven.</span><span class="sxs-lookup"><span data-stu-id="9883f-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="9883f-191">Hello AAR пакета могут быть включены в проект в Android Studio следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9883f-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="9883f-192">Способ 4: AAR через Maven</span><span class="sxs-lookup"><span data-stu-id="9883f-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="9883f-193">Если вы используете hello M2Eclipse подключаемый модуль, можно указать hello зависимостей в файле pom.xml:</span><span class="sxs-lookup"><span data-stu-id="9883f-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="9883f-194">Параметр 5: Пакет JAR-ФАЙЛ в папке библиотеки hello</span><span class="sxs-lookup"><span data-stu-id="9883f-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="9883f-195">Можно получить из репозитория Maven hello hello JAR-файл и вставьте его в hello **библиотеки** в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="9883f-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="9883f-196">Необходимо toocopy hello необходимые ресурсы tooyour проекта, так как пакеты JAR hello не включайте их.</span><span class="sxs-lookup"><span data-stu-id="9883f-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="9883f-197">Шаг 5: Добавление ссылки на tooAndroid ADAL tooyour проекта</span><span class="sxs-lookup"><span data-stu-id="9883f-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="9883f-198">Добавьте проект tooyour ссылки и указать его как библиотека Android.</span><span class="sxs-lookup"><span data-stu-id="9883f-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="9883f-199">Если вы уверены как toodo это, можно получить дополнительные сведения о hello [Android Studio сайта](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="9883f-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="9883f-200">Добавьте hello зависимостей проекта для отладки в параметрах проекта.</span><span class="sxs-lookup"><span data-stu-id="9883f-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="9883f-201">Обновление tooinclude файла AndroidManifest.xml проекта:</span><span class="sxs-lookup"><span data-stu-id="9883f-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="9883f-202">Создайте экземпляр класса AuthenticationContext с вашим MainActivity.</span><span class="sxs-lookup"><span data-stu-id="9883f-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="9883f-203">Hello сведения данного вызова выходят за рамки этого раздела hello, но достаточно начать можно получить, просмотрев hello [Android Native Client образец](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="9883f-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="9883f-204">В следующем примере hello, SharedPreferences hello кэша по умолчанию, который центр в форме hello `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="9883f-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="9883f-205">Скопируйте этот код блока toohandle hello конец AuthenticationActivity после hello пользователь вводит учетные данные и получает код авторизации:</span><span class="sxs-lookup"><span data-stu-id="9883f-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="9883f-206">tooask к маркеру, определите обратный вызов.</span><span class="sxs-lookup"><span data-stu-id="9883f-206">tooask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="9883f-207">Наконец, запросите маркер с помощью данного обратного вызова:</span><span class="sxs-lookup"><span data-stu-id="9883f-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="9883f-208">Ниже приведено описание параметров hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="9883f-209">*ресурс* является обязательным и находится hello ресурса, которому вы пытаетесь tooaccess.</span><span class="sxs-lookup"><span data-stu-id="9883f-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="9883f-210">Параметр *clientId* является обязательным и поступает из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9883f-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="9883f-211">*RedirectUri* не требуется toobe, предоставленные для вызова acquireToken hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="9883f-212">В качестве него можно задать имя пакета.</span><span class="sxs-lookup"><span data-stu-id="9883f-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="9883f-213">*PromptBehavior* помогает tooask для кэша hello tooskip учетные данные и файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="9883f-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="9883f-214">*обратный вызов* вызывается после того, обмен которыми осуществляется hello код авторизации для маркера.</span><span class="sxs-lookup"><span data-stu-id="9883f-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="9883f-215">Он получает объект AuthenticationResult, который имеет маркер доступа, дату окончания срока действия и сведения об идентификаторе маркера.</span><span class="sxs-lookup"><span data-stu-id="9883f-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="9883f-216">Параметр *acquireTokenSilent* является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9883f-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="9883f-217">Его можно вызвать toohandle кэширование и обновление токена.</span><span class="sxs-lookup"><span data-stu-id="9883f-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="9883f-218">Он также предоставляет версию sync hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-218">It also provides hello sync version.</span></span> <span data-ttu-id="9883f-219">Он принимает *userid* в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="9883f-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="9883f-220">Используя в данном пошаговом руководстве, необходимо иметь какой требуется toosuccessfully интеграции с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9883f-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="9883f-221">Дополнительные примеры этой работы, посетите hello AzureADSamples / репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="9883f-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="9883f-222">Важные сведения</span><span class="sxs-lookup"><span data-stu-id="9883f-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="9883f-223">Настройка</span><span class="sxs-lookup"><span data-stu-id="9883f-223">Customization</span></span>
<span data-ttu-id="9883f-224">Ресурсы проекта библиотеки могут быть перезаписаны ресурсами вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9883f-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="9883f-225">Перезапись происходит при сборке приложения.</span><span class="sxs-lookup"><span data-stu-id="9883f-225">This happens when your app is being built.</span></span> <span data-ttu-id="9883f-226">По этой причине можно настроить проверку подлинности действия макета hello должным образом.</span><span class="sxs-lookup"><span data-stu-id="9883f-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="9883f-227">Быть убедиться, что идентификатор hello tookeep hello элементов управления, ADAL использует (WebView).</span><span class="sxs-lookup"><span data-stu-id="9883f-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="9883f-228">Broker</span><span class="sxs-lookup"><span data-stu-id="9883f-228">Broker</span></span>
<span data-ttu-id="9883f-229">приложение корпоративного портала Microsoft Hello предоставляет компонента broker hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="9883f-230">Hello учетная запись создается в AccountManager.</span><span class="sxs-lookup"><span data-stu-id="9883f-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="9883f-231">Тип учетной записи Hello является «com.microsoft.workaccount».</span><span class="sxs-lookup"><span data-stu-id="9883f-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="9883f-232">Диспетчер учетных записей разрешает только одну учетную запись единого входа.</span><span class="sxs-lookup"><span data-stu-id="9883f-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="9883f-233">Он создает файл cookie единого входа для пользователя hello после завершения запроса hello устройств для одного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="9883f-234">ADAL использует учетную запись broker hello, если одна учетная запись создается в данной структуры проверки подлинности и выборе не tooskip его.</span><span class="sxs-lookup"><span data-stu-id="9883f-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="9883f-235">Вы можете пропустить hello broker пользователя с:</span><span class="sxs-lookup"><span data-stu-id="9883f-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="9883f-236">Для использования посредника должны tooregister специальные RedirectUri.</span><span class="sxs-lookup"><span data-stu-id="9883f-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="9883f-237">RedirectUri указано в формате hello `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="9883f-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="9883f-238">Можно получить ваш RedirectUri для приложения с помощью сценария brokerRedirectPrint.ps1 hello или mContext.getBrokerRedirectUri вызов hello API.</span><span class="sxs-lookup"><span data-stu-id="9883f-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="9883f-239">Сигнатура Hello — связанные tooyour сертификаты подписи.</span><span class="sxs-lookup"><span data-stu-id="9883f-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="9883f-240">Текущая модель broker Hello — для одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="9883f-240">hello current broker model is for one user.</span></span> <span data-ttu-id="9883f-241">AuthenticationContext предоставляет hello API метод tooget hello broker пользователя.</span><span class="sxs-lookup"><span data-stu-id="9883f-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="9883f-242">Манифест приложения должен иметь следующие разрешения toouse AccountManager счетов hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="9883f-243">Дополнительные сведения см. в разделе hello [AccountManager сведения на сайте Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="9883f-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="9883f-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="9883f-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="9883f-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="9883f-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="9883f-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="9883f-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="9883f-247">URL-адрес центра и службы федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="9883f-247">Authority URL and AD FS</span></span>
<span data-ttu-id="9883f-248">Служб федерации Active Directory (AD FS) не распознается как производственной службе маркеров безопасности, поэтому требуется tooturn обнаружения экземпляра и передайте значение false в конструктор AuthenticationContext hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="9883f-249">URL-адрес центра Hello требуется экземпляр службы маркеров безопасности и [имя клиента](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="9883f-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="9883f-250">Запрос элементов кэша</span><span class="sxs-lookup"><span data-stu-id="9883f-250">Querying cache items</span></span>
<span data-ttu-id="9883f-251">Библиотека ADAL предоставляет кэш по умолчанию в SharedPrefrecens и несколько простых функций для запроса данных из кэша.</span><span class="sxs-lookup"><span data-stu-id="9883f-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="9883f-252">Можно получить текущий кэш hello из AuthenticationContext с помощью:</span><span class="sxs-lookup"><span data-stu-id="9883f-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="9883f-253">Можно также предоставить реализации кэша, если требуется, чтобы toocustomize его.</span><span class="sxs-lookup"><span data-stu-id="9883f-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="9883f-254">Поведения запроса</span><span class="sxs-lookup"><span data-stu-id="9883f-254">Prompt behavior</span></span>
<span data-ttu-id="9883f-255">ADAL является поведения запроса toospecify параметр.</span><span class="sxs-lookup"><span data-stu-id="9883f-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="9883f-256">PromptBehavior.Auto покажет hello пользовательского интерфейса, если hello токен обновления является недопустимым, и требуются учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="9883f-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="9883f-257">PromptBehavior.Always пропустит использование кэша hello и всегда показывать hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="9883f-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="9883f-258">Автоматический запрос маркера из кэша и обновление</span><span class="sxs-lookup"><span data-stu-id="9883f-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="9883f-259">Запрос маркера автоматической не использует hello всплывающих пользовательского интерфейса и не требует действия.</span><span class="sxs-lookup"><span data-stu-id="9883f-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="9883f-260">Он возвращает маркер из кэша hello, если он доступен.</span><span class="sxs-lookup"><span data-stu-id="9883f-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="9883f-261">Если истек срок действия маркера hello, этот метод пытается toorefresh его.</span><span class="sxs-lookup"><span data-stu-id="9883f-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="9883f-262">Если сбой или просроченный маркер обновления hello, он возвращает AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="9883f-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="9883f-263">Также данный метод обеспечивает возможность выполнить синхронный вызов.</span><span class="sxs-lookup"><span data-stu-id="9883f-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="9883f-264">Можно задать значение null toocallback или использовать acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="9883f-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="9883f-265">Диагностика</span><span class="sxs-lookup"><span data-stu-id="9883f-265">Diagnostics</span></span>
<span data-ttu-id="9883f-266">Это hello основными источниками информации для диагностики проблем.</span><span class="sxs-lookup"><span data-stu-id="9883f-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="9883f-267">Исключения</span><span class="sxs-lookup"><span data-stu-id="9883f-267">Exceptions</span></span>
* <span data-ttu-id="9883f-268">Журналы</span><span class="sxs-lookup"><span data-stu-id="9883f-268">Logs</span></span>
* <span data-ttu-id="9883f-269">Данные трассировки сети</span><span class="sxs-lookup"><span data-stu-id="9883f-269">Network traces</span></span>

<span data-ttu-id="9883f-270">Обратите внимание, что идентификаторы корреляции toohello центра диагностики в библиотеке hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="9883f-271">При желании toocorrelate ADAL запроса с другими операциями, в коде, можно задать вашей идентификаторов корреляции для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="9883f-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="9883f-272">Если идентификатор корреляции не задан, то библиотека ADAL создает случайный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9883f-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="9883f-273">Все журнала сообщений и затем сетевые вызовы будут помечены с идентификатором hello корреляции.</span><span class="sxs-lookup"><span data-stu-id="9883f-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="9883f-274">Hello самостоятельно сформированный изменения идентификатора для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="9883f-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="9883f-275">Исключения</span><span class="sxs-lookup"><span data-stu-id="9883f-275">Exceptions</span></span>
<span data-ttu-id="9883f-276">Исключениями являются hello сначала диагностики.</span><span class="sxs-lookup"><span data-stu-id="9883f-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="9883f-277">Мы пытаемся tooprovide полезные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="9883f-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="9883f-278">Если вы не считаете какое-либо сообщение содержательным, пожалуйста, сообщите нам об этом.</span><span class="sxs-lookup"><span data-stu-id="9883f-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="9883f-279">Укажите такие сведения об устройстве, как модель и версия SDK.</span><span class="sxs-lookup"><span data-stu-id="9883f-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="9883f-280">Журналы</span><span class="sxs-lookup"><span data-stu-id="9883f-280">Logs</span></span>
<span data-ttu-id="9883f-281">Можно настроить toogenerate библиотеки hello сообщений журнала, которые можно использовать toohelp диагностировать проблемы.</span><span class="sxs-lookup"><span data-stu-id="9883f-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="9883f-282">Настройка ведения журнала, делая hello следующий вызов tooconfigure обратный вызов, ADAL будет использовать toohand off каждое сообщение журнала, как оно генерируется.</span><span class="sxs-lookup"><span data-stu-id="9883f-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="9883f-283">Сообщения могут записываться tooa пользовательский файл журнала, как показано в следующим hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="9883f-284">К сожалению, нет стандартного способа получения журналов с устройств.</span><span class="sxs-lookup"><span data-stu-id="9883f-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="9883f-285">Существуют некоторые службы, которые могут в этом помочь.</span><span class="sxs-lookup"><span data-stu-id="9883f-285">There are some services that can help you with this.</span></span> <span data-ttu-id="9883f-286">Можно также придумать собственный, например, отправляющий сервер tooa файл hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="9883f-287">Существуют следующие уровни ведения журнала hello:</span><span class="sxs-lookup"><span data-stu-id="9883f-287">These are hello logging levels:</span></span>
* <span data-ttu-id="9883f-288">Error (исключение);</span><span class="sxs-lookup"><span data-stu-id="9883f-288">Error (exceptions)</span></span>
* <span data-ttu-id="9883f-289">Warn (предупреждение);</span><span class="sxs-lookup"><span data-stu-id="9883f-289">Warn (warning)</span></span>
* <span data-ttu-id="9883f-290">Info (информирование);</span><span class="sxs-lookup"><span data-stu-id="9883f-290">Info (information purposes)</span></span>
* <span data-ttu-id="9883f-291">Verbose (дополнительные сведения).</span><span class="sxs-lookup"><span data-stu-id="9883f-291">Verbose (more details)</span></span>

<span data-ttu-id="9883f-292">Можно установить уровень журнала hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9883f-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="9883f-293">Все сообщения журнала отправляются toologcat, в обратных вызовах, добавление tooany пользовательского журнала.</span><span class="sxs-lookup"><span data-stu-id="9883f-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="9883f-294">Файл журнала tooa из logcat можно получить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9883f-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="9883f-295">Дополнительные сведения о командах adb см. в разделе hello [logcat сведения на сайте Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="9883f-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="9883f-296">Данные трассировки сети</span><span class="sxs-lookup"><span data-stu-id="9883f-296">Network traces</span></span>
<span data-ttu-id="9883f-297">Можно использовать различные средства toocapture hello трафик HTTP, приводит к возникновению ошибки ADAL.</span><span class="sxs-lookup"><span data-stu-id="9883f-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="9883f-298">Это может пригодиться, если вы знакомы с hello протокола OAuth или при необходимости tooMicrosoft tooprovide диагностической информации или по другим каналам поддержки.</span><span class="sxs-lookup"><span data-stu-id="9883f-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="9883f-299">Fiddler — hello удобное средство трассировки HTTP.</span><span class="sxs-lookup"><span data-stu-id="9883f-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="9883f-300">Используйте hello следующие ссылки tooset его запись toocorrectly ADAL сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="9883f-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="9883f-301">Для средства трассировки как Fiddler или Чарльз toobe полезно необходимо настроить его трафика toorecord без шифрования SSL.</span><span class="sxs-lookup"><span data-stu-id="9883f-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="9883f-302">Данные трассировки, записанные таким образом, могут содержать конфиденциальные сведения, такие как маркеры доступа, имена пользователей и пароли.</span><span class="sxs-lookup"><span data-stu-id="9883f-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="9883f-303">При использовании рабочих учетных записей не передавайте данные трассировки третьим сторонам.</span><span class="sxs-lookup"><span data-stu-id="9883f-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="9883f-304">При необходимости toosupply toosomeone трассировки в порядке tooget поддержки воспроизвести проблему hello, используя временную учетную запись с имена пользователей и пароли, не столь важно для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="9883f-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="9883f-305">С веб-сайта Telerik hello: [параметр вверх Fiddler для Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="9883f-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="9883f-306">Использование GitHub : [Настройка правил Fiddler для библиотеки ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="9883f-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="9883f-307">Режим диалогового окна</span><span class="sxs-lookup"><span data-stu-id="9883f-307">Dialog mode</span></span>
<span data-ttu-id="9883f-308">метод acquireToken Hello без действий поддерживает строки диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9883f-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="9883f-309">Шифрование</span><span class="sxs-lookup"><span data-stu-id="9883f-309">Encryption</span></span>
<span data-ttu-id="9883f-310">ADAL шифрует токены hello и хранилища в SharedPreferences по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9883f-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="9883f-311">Можно просмотреть сведения о классе toosee hello StorageHelper hello.</span><span class="sxs-lookup"><span data-stu-id="9883f-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="9883f-312">В Android 4.3 (API уровня 18) введено безопасное хранилище закрытых ключей AndroidKeyStore.</span><span class="sxs-lookup"><span data-stu-id="9883f-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="9883f-313">Библиотека ADAL использует это хранилище при работе с API уровня 18 и выше.</span><span class="sxs-lookup"><span data-stu-id="9883f-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="9883f-314">Если требуется toouse ADAL для более ранних версиях пакета SDK, необходимо tooprovide секретный ключ по AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="9883f-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="9883f-315">Запрос носителя OAuth2</span><span class="sxs-lookup"><span data-stu-id="9883f-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="9883f-316">Hello AuthenticationParameters класс предоставляет функциональные возможности tooget authorization_uri из hello запрос OAuth2 носителя.</span><span class="sxs-lookup"><span data-stu-id="9883f-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="9883f-317">Файлы cookie сеанса в веб-представлении</span><span class="sxs-lookup"><span data-stu-id="9883f-317">Session cookies in WebView</span></span>
<span data-ttu-id="9883f-318">После закрытия приложения hello Android WebView не удаляет файлы cookie сеанса.</span><span class="sxs-lookup"><span data-stu-id="9883f-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="9883f-319">Это можно сделать с помощью следующего примера кода.</span><span class="sxs-lookup"><span data-stu-id="9883f-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="9883f-320">Дополнительные сведения о файлах cookie см. в разделе hello [CookieSyncManager сведения на сайте Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="9883f-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="9883f-321">Переопределения ресурсов</span><span class="sxs-lookup"><span data-stu-id="9883f-321">Resource overrides</span></span>
<span data-ttu-id="9883f-322">Библиотека ADAL Hello включает английская строк ProgressDialog сообщений.</span><span class="sxs-lookup"><span data-stu-id="9883f-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="9883f-323">Разработчику следует перезаписать эти сроки, если требуется их локализовать.</span><span class="sxs-lookup"><span data-stu-id="9883f-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="9883f-324">Диалоговое окно NTLM</span><span class="sxs-lookup"><span data-stu-id="9883f-324">NTLM dialog box</span></span>
<span data-ttu-id="9883f-325">ADAL версии 1.1.0 поддерживает диалоговое окно с NTLM, который обработает событие onReceivedHttpAuthRequest hello из WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="9883f-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="9883f-326">Можно настроить макет hello и строки для диалоговое окно «hello».</span><span class="sxs-lookup"><span data-stu-id="9883f-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="9883f-327">Единый вход для нескольких приложений</span><span class="sxs-lookup"><span data-stu-id="9883f-327">Cross-app SSO</span></span>
<span data-ttu-id="9883f-328">Дополнительные сведения [как tooenable нескольких приложений единого входа в Android с помощью ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="9883f-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
