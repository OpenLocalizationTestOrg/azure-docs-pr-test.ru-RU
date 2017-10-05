---
title: "Приступая к работе с Azure AD для Android | Документация Майкрософт"
description: "Практическое руководство по созданию приложения для Android, которое интегрируется с Azure AD для входа в систему и вызывает программные интерфейсы приложения, защищенные Azure AD, по протоколу OAuth."
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
ms.openlocfilehash: 746cad19093fd2a1ad23ddd9412394f8d9da331c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="9bce3-103">Интеграция Azure AD в приложение для Android</span><span class="sxs-lookup"><span data-stu-id="9bce3-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="9bce3-104">Воспользуйтесь предварительной версией нашего нового [портала разработчиков](https://identity.microsoft.com/Docs/Android), который поможет вам приступить к работе с Azure AD через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="9bce3-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="9bce3-105">Портал разработчиков поможет зарегистрировать приложение и интегрировать Azure AD в коде.</span><span class="sxs-lookup"><span data-stu-id="9bce3-105">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="9bce3-106">Завершив работу, вы получите простое приложение, с помощью которого выполняется проверка подлинности пользователей в клиенте и на сервере, принимающем маркеры и проводящем проверку.</span><span class="sxs-lookup"><span data-stu-id="9bce3-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="9bce3-107">При разработке классического приложения служба Azure Active Directory позволяет разработчику упростить аутентификацию локальных учетных записей пользователей в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9bce3-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="9bce3-108">Это также позволяет вашему приложению безопасно использовать любые веб-интерфейсы API, защищаемые с помощью Azure AD, например интерфейсы Office 365 API или Azure API.</span><span class="sxs-lookup"><span data-stu-id="9bce3-108">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="9bce3-109">Клиентские приложения для Android, которым необходим доступ к защищенным ресурсам, могут использовать библиотеку проверки подлинности Azure AD (ADAL).</span><span class="sxs-lookup"><span data-stu-id="9bce3-109">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="9bce3-110">Единственное предназначение ADAL — упростить процесс получения маркеров доступа.</span><span class="sxs-lookup"><span data-stu-id="9bce3-110">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="9bce3-111">Чтобы показать, насколько это просто, мы создадим приложение To-Do List для Android, которое:</span><span class="sxs-lookup"><span data-stu-id="9bce3-111">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="9bce3-112">получает маркеры доступа для вызова интерфейса API приложения To-Do List с помощью [протокола проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx);</span><span class="sxs-lookup"><span data-stu-id="9bce3-112">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="9bce3-113">получает список дел пользователя;</span><span class="sxs-lookup"><span data-stu-id="9bce3-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="9bce3-114">выполняет выход из системы для пользователей.</span><span class="sxs-lookup"><span data-stu-id="9bce3-114">Signs out users.</span></span>

<span data-ttu-id="9bce3-115">Чтобы приступить к работе, потребуется клиент Azure AD, в котором можно создавать пользователей и регистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="9bce3-115">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="9bce3-116">Если клиента нет, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="9bce3-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="9bce3-117">Этап 1. Скачивание и запуск образца службы, реализующей интерфейс REST API приложения To Do List для Node.js</span><span class="sxs-lookup"><span data-stu-id="9bce3-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="9bce3-118">Описываемый в этой статье образец специально создается так, чтобы можно было сравнить его работу с существующим образцом, создающим интерфейс REST API для однотенантного приложения To Do List под управлением Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bce3-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="9bce3-119">Вышеупомянутый образец службы необходим для данного примера быстрого старта.</span><span class="sxs-lookup"><span data-stu-id="9bce3-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="9bce3-120">Сведения о том, как выполнить такую настройку, см. в существующих примерах в статье [Приступая к работе с веб-интерфейсом API для узла](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9bce3-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="9bce3-121">Этап 2. Регистрация веб-API с помощью клиента Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bce3-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="9bce3-122">Служба каталогов Active Directory позволяет добавлять приложения двух типов:</span><span class="sxs-lookup"><span data-stu-id="9bce3-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="9bce3-123">веб-интерфейсы API, которые предоставляют услуги пользователям,</span><span class="sxs-lookup"><span data-stu-id="9bce3-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="9bce3-124">и приложения (работающие через Интернет или на устройстве), использующие эти веб-API.</span><span class="sxs-lookup"><span data-stu-id="9bce3-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="9bce3-125">На этом этапе вы зарегистрируете веб-API, который будет работать локально для тестирования данного образца.</span><span class="sxs-lookup"><span data-stu-id="9bce3-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="9bce3-126">Обычно этот веб-API является службой REST, предоставляющей приложению необходимую функциональность.</span><span class="sxs-lookup"><span data-stu-id="9bce3-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="9bce3-127">Azure AD может помочь защитить любую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="9bce3-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="9bce3-128">Предполагается, что вы будете регистрировать пример To Do REST API, упомянутый ранее.</span><span class="sxs-lookup"><span data-stu-id="9bce3-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="9bce3-129">Но это работает для любого веб-API, который требуется защитить с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9bce3-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="9bce3-130">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9bce3-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9bce3-131">На верхней панели щелкните свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="9bce3-131">On the top bar, click your account.</span></span> <span data-ttu-id="9bce3-132">В списке **Каталог** выберите клиент Azure AD, в котором будет зарегистрировано приложение.</span><span class="sxs-lookup"><span data-stu-id="9bce3-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="9bce3-133">В области слева щелкните **Больше служб** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9bce3-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9bce3-134">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9bce3-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="9bce3-135">Введите понятное имя для приложения, например **TodoListService**, выберите **Веб-приложение и/или веб-API** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9bce3-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="9bce3-136">В качестве URL-адреса единого входа введите базовый URL-адрес для образца.</span><span class="sxs-lookup"><span data-stu-id="9bce3-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="9bce3-137">По умолчанию это `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="9bce3-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="9bce3-138">Для завершения регистрации нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9bce3-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="9bce3-139">Оставаясь на портале Azure, перейдите на страницу приложения, найдите значение идентификатора и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="9bce3-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="9bce3-140">Оно понадобится позже при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="9bce3-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="9bce3-141">На странице **Параметры** -> **Свойства** измените универсальный код ресурса (URI) идентификатора приложения, введя `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="9bce3-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="9bce3-142">Замените `<your_tenant_name>` именем вашего клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bce3-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="9bce3-143">Этап 3. Регистрация образца нативного клиентского приложения для Android</span><span class="sxs-lookup"><span data-stu-id="9bce3-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="9bce3-144">В этом примере необходимо зарегистрировать веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="9bce3-144">You must register your web application in this sample.</span></span> <span data-ttu-id="9bce3-145">Это позволяет приложению взаимодействовать с только что зарегистрированным веб-API.</span><span class="sxs-lookup"><span data-stu-id="9bce3-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="9bce3-146">Если приложение не зарегистрировано, то Azure AD не позволит ему даже запросить данные для входа.</span><span class="sxs-lookup"><span data-stu-id="9bce3-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="9bce3-147">Это часть модели безопасности.</span><span class="sxs-lookup"><span data-stu-id="9bce3-147">That's part of the security of the model.</span></span>

<span data-ttu-id="9bce3-148">Предполагается, что вы регистрируете пример приложения, упомянутый ранее.</span><span class="sxs-lookup"><span data-stu-id="9bce3-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="9bce3-149">Но эта процедура подходит для любого приложения, которое вы разрабатываете.</span><span class="sxs-lookup"><span data-stu-id="9bce3-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="9bce3-150">Может возникнуть вопрос, почему приложение и веб-интерфейс API размещаются в одном клиенте?</span><span class="sxs-lookup"><span data-stu-id="9bce3-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="9bce3-151">Как вы могли догадаться, можно создать приложение, которое обращается к внешнему интерфейсу API, зарегистрированному в Azure AD из другого клиента.</span><span class="sxs-lookup"><span data-stu-id="9bce3-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="9bce3-152">При этом пользователям будет предложено дать согласие на использование этого интерфейса API в приложении.</span><span class="sxs-lookup"><span data-stu-id="9bce3-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="9bce3-153">Библиотека проверки подлинности Active Directory для iOS выполняет все необходимые операции для обработки данного согласия.</span><span class="sxs-lookup"><span data-stu-id="9bce3-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="9bce3-154">В более сложных задачах становится очевидным, что обработка согласия является важной составляющей доступа к интерфейсам Microsoft API от Azure и Office, а также любого другого поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="9bce3-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="9bce3-155">Пока приложение и веб-интерфейс зарегистрированы в рамках одного и того же клиента, пользователь не увидит запросы на согласие.</span><span class="sxs-lookup"><span data-stu-id="9bce3-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="9bce3-156">Это типично для приложений, предназначенных для использования только внутри компании.</span><span class="sxs-lookup"><span data-stu-id="9bce3-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="9bce3-157">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9bce3-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9bce3-158">На верхней панели щелкните свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="9bce3-158">On the top bar, click your account.</span></span> <span data-ttu-id="9bce3-159">В списке **Каталог** выберите клиент Azure AD, в котором будет зарегистрировано приложение.</span><span class="sxs-lookup"><span data-stu-id="9bce3-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="9bce3-160">В области слева щелкните **Больше служб** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9bce3-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9bce3-161">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9bce3-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="9bce3-162">Введите понятное имя для приложения, например **TodoListService**, выберите **Собственное клиентское приложение** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9bce3-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="9bce3-163">В качестве URI переадресации введите `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="9bce3-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="9bce3-164">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="9bce3-164">Click **Finish**.</span></span>
7. <span data-ttu-id="9bce3-165">На странице приложения найдите значение идентификатора приложения и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="9bce3-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="9bce3-166">Оно понадобится позже при настройке приложения.</span><span class="sxs-lookup"><span data-stu-id="9bce3-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="9bce3-167">На странице **Параметры** выберите **Необходимые разрешения** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9bce3-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="9bce3-168">Выберите TodoListService, добавьте разрешение **Access TodoListService** (Доступ к TodoListService) в списке **Делегированные разрешения** и щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="9bce3-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="9bce3-169">Для сборки с помощью Maven можно использовать файл pom.xml на верхнем уровне.</span><span class="sxs-lookup"><span data-stu-id="9bce3-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="9bce3-170">Клонируйте этот репозиторий в любой каталог по своему усмотрению:</span><span class="sxs-lookup"><span data-stu-id="9bce3-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="9bce3-171">Выполните действия, описанные в [предварительных требованиях для настройки среды Maven для Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="9bce3-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="9bce3-172">Установите эмулятор с пакетом SDK 19.</span><span class="sxs-lookup"><span data-stu-id="9bce3-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="9bce3-173">Перейдите в корневую папку, куда клонирован репозиторий.</span><span class="sxs-lookup"><span data-stu-id="9bce3-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="9bce3-174">Выполните следующую команду: `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="9bce3-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="9bce3-175">Перейдите в каталог примера краткого руководства `cd samples\hello`.</span><span class="sxs-lookup"><span data-stu-id="9bce3-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="9bce3-176">Выполните следующую команду: `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="9bce3-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="9bce3-177">Приложение будет запущено.</span><span class="sxs-lookup"><span data-stu-id="9bce3-177">You should see the app starting.</span></span>
8. <span data-ttu-id="9bce3-178">Введите учетные данные тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="9bce3-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="9bce3-179">JAR-пакеты будут также отправляться наряду с AAR-пакетом.</span><span class="sxs-lookup"><span data-stu-id="9bce3-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="9bce3-180">Этап 4. Скачивание библиотеки ADAL для Android и добавление ее в рабочую область платформы Eclipse</span><span class="sxs-lookup"><span data-stu-id="9bce3-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="9bce3-181">Существует несколько способов использования библиотеки ADAL в проекте для Android:</span><span class="sxs-lookup"><span data-stu-id="9bce3-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="9bce3-182">Можно импортировать библиотеку в платформу Eclipse в виде исходного кода и связать с приложением.</span><span class="sxs-lookup"><span data-stu-id="9bce3-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="9bce3-183">В Android Studio можно использовать пакет AAR и сослаться на двоичные файлы.</span><span class="sxs-lookup"><span data-stu-id="9bce3-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="9bce3-184">Способ 1: ZIP-архив с файлами исходного кода</span><span class="sxs-lookup"><span data-stu-id="9bce3-184">Option 1: Source Zip</span></span>
<span data-ttu-id="9bce3-185">Чтобы скачать копию исходного кода, в правой части страницы щелкните **Download ZIP** (Загрузить ZIP).</span><span class="sxs-lookup"><span data-stu-id="9bce3-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="9bce3-186">Или [скачайте его с GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="9bce3-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="9bce3-187">Способ 2: исходные файлы через Git</span><span class="sxs-lookup"><span data-stu-id="9bce3-187">Option 2: Source via Git</span></span>
<span data-ttu-id="9bce3-188">Чтобы получить исходный код пакета SDK через Git, введите:</span><span class="sxs-lookup"><span data-stu-id="9bce3-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="9bce3-189">Способ 3: двоичные файлы через Gradle</span><span class="sxs-lookup"><span data-stu-id="9bce3-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="9bce3-190">Двоичные файлы можно получить из центрального репозитория Maven.</span><span class="sxs-lookup"><span data-stu-id="9bce3-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="9bce3-191">Пакет AAR может быть включен в проект Android Studio следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9bce3-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

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

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="9bce3-192">Способ 4: AAR через Maven</span><span class="sxs-lookup"><span data-stu-id="9bce3-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="9bce3-193">Если используется подключаемый модуль M2Eclipse, можно задать зависимость в файле pom.xml:</span><span class="sxs-lookup"><span data-stu-id="9bce3-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="9bce3-194">Способ 5: JAR-пакет в папке libs</span><span class="sxs-lookup"><span data-stu-id="9bce3-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="9bce3-195">Можно перетащить JAR-файл из репозитория Maven в папку **libs** проекта.</span><span class="sxs-lookup"><span data-stu-id="9bce3-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="9bce3-196">Вы должны скопировать требуемые ресурсы в свой проект, так как они не включены в JAR-пакеты.</span><span class="sxs-lookup"><span data-stu-id="9bce3-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="9bce3-197">Этап 5: добавление ссылки на библиотеку ADAL для Android в проект</span><span class="sxs-lookup"><span data-stu-id="9bce3-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="9bce3-198">Добавьте в проект ссылку на библиотеку для Android.</span><span class="sxs-lookup"><span data-stu-id="9bce3-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="9bce3-199">Если вы не знаете, как это сделать, ознакомьтесь с дополнительными сведениями на [сайте Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="9bce3-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="9bce3-200">Добавьте в параметры проекта зависимость проекта для отладки.</span><span class="sxs-lookup"><span data-stu-id="9bce3-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="9bce3-201">Добавьте в файл проекта AndroidManifest.xml следующее:</span><span class="sxs-lookup"><span data-stu-id="9bce3-201">Update your project's AndroidManifest.xml file to include:</span></span>

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

4. <span data-ttu-id="9bce3-202">Создайте экземпляр класса AuthenticationContext с вашим MainActivity.</span><span class="sxs-lookup"><span data-stu-id="9bce3-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="9bce3-203">Описание этого вызова выходит за рамки данной статьи, но вы можете получить дополнительные сведения в разделе с [образцом собственного клиентского приложения для Android](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="9bce3-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="9bce3-204">Ниже приведен пример, где SharedPreferences используется как кэш по умолчанию и права представлены в виде `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="9bce3-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="9bce3-205">Скопируйте этот блок кода для обработки в конец AuthenticationActivity после фрагмента, где пользователь вводит учетные данные и получает код авторизации:</span><span class="sxs-lookup"><span data-stu-id="9bce3-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="9bce3-206">Чтобы запросить маркер, определите функцию обратного вызова:</span><span class="sxs-lookup"><span data-stu-id="9bce3-206">To ask for a token, define a callback:</span></span>

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

7. <span data-ttu-id="9bce3-207">Наконец, запросите маркер с помощью данного обратного вызова:</span><span class="sxs-lookup"><span data-stu-id="9bce3-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="9bce3-208">Объяснение параметров:</span><span class="sxs-lookup"><span data-stu-id="9bce3-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="9bce3-209">Параметр *resource* является обязательным и указывает ресурс, к которому требуется получить доступ.</span><span class="sxs-lookup"><span data-stu-id="9bce3-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="9bce3-210">Параметр *clientId* является обязательным и поступает из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bce3-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="9bce3-211">Параметр *RedirectUri* не требуется для вызова acquireToken.</span><span class="sxs-lookup"><span data-stu-id="9bce3-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="9bce3-212">В качестве него можно задать имя пакета.</span><span class="sxs-lookup"><span data-stu-id="9bce3-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="9bce3-213">Параметр *PromptBehavior* указывает на необходимость запроса учетных данных, а не получения их из кэша или файла cookie.</span><span class="sxs-lookup"><span data-stu-id="9bce3-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="9bce3-214">Параметр *callback* вызывается после обмена кода авторизации на маркер.</span><span class="sxs-lookup"><span data-stu-id="9bce3-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="9bce3-215">Он получает объект AuthenticationResult, который имеет маркер доступа, дату окончания срока действия и сведения об идентификаторе маркера.</span><span class="sxs-lookup"><span data-stu-id="9bce3-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="9bce3-216">Параметр *acquireTokenSilent* является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9bce3-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="9bce3-217">Его можно вызвать для обработки кэшированных данных и обновления маркеров.</span><span class="sxs-lookup"><span data-stu-id="9bce3-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="9bce3-218">Также данный метод обеспечивает возможность выполнить синхронный вызов.</span><span class="sxs-lookup"><span data-stu-id="9bce3-218">It also provides the sync version.</span></span> <span data-ttu-id="9bce3-219">Он принимает *userid* в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="9bce3-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="9bce3-220">Данное пошаговое руководство предоставляет все необходимое для успешной интеграции с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bce3-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="9bce3-221">Дополнительные примеры представлены в репозитории AzureADSamples/ на портале GitHub.</span><span class="sxs-lookup"><span data-stu-id="9bce3-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="9bce3-222">Важные сведения</span><span class="sxs-lookup"><span data-stu-id="9bce3-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="9bce3-223">Настройка</span><span class="sxs-lookup"><span data-stu-id="9bce3-223">Customization</span></span>
<span data-ttu-id="9bce3-224">Ресурсы проекта библиотеки могут быть перезаписаны ресурсами вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9bce3-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="9bce3-225">Перезапись происходит при сборке приложения.</span><span class="sxs-lookup"><span data-stu-id="9bce3-225">This happens when your app is being built.</span></span> <span data-ttu-id="9bce3-226">Поэтому вы можете настроить макет AuthenticationActivity так, как требуется.</span><span class="sxs-lookup"><span data-stu-id="9bce3-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="9bce3-227">Необходимо обязательно сохранять идентификаторы элементов управления, которые используются библиотекой ADAL (веб-представление).</span><span class="sxs-lookup"><span data-stu-id="9bce3-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="9bce3-228">Broker</span><span class="sxs-lookup"><span data-stu-id="9bce3-228">Broker</span></span>
<span data-ttu-id="9bce3-229">Компонент broker предоставляется приложением корпоративного портала Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="9bce3-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="9bce3-230">Учетная запись создается в диспетчере учетных записей.</span><span class="sxs-lookup"><span data-stu-id="9bce3-230">The account is created in AccountManager.</span></span> <span data-ttu-id="9bce3-231">Тип учетной записи — com.microsoft.workaccount.</span><span class="sxs-lookup"><span data-stu-id="9bce3-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="9bce3-232">Диспетчер учетных записей разрешает только одну учетную запись единого входа.</span><span class="sxs-lookup"><span data-stu-id="9bce3-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="9bce3-233">Этот компонент создает файл cookie единого входа для данного пользователя после завершения запроса устройства одним из приложений.</span><span class="sxs-lookup"><span data-stu-id="9bce3-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="9bce3-234">Библиотека ADAL использует учетную запись broker, если существует одноименная пользовательская учетная запись, созданная в этой структуре проверки подлинности, и вы решили не игнорировать ее.</span><span class="sxs-lookup"><span data-stu-id="9bce3-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="9bce3-235">Вы можете пропустить пользователя broker с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="9bce3-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="9bce3-236">Для использования broker необходимо зарегистрировать специальный URI перенаправления.</span><span class="sxs-lookup"><span data-stu-id="9bce3-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="9bce3-237">URI перенаправления имеет формат `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="9bce3-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="9bce3-238">Можно получить URI перенаправления для приложения с помощью скрипта brokerRedirectPrint.ps1 или с помощью вызова метода API mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="9bce3-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="9bce3-239">Подпись связана с вашими сертификатами подписи.</span><span class="sxs-lookup"><span data-stu-id="9bce3-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="9bce3-240">Текущая модель broker предназначена для одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="9bce3-240">The current broker model is for one user.</span></span> <span data-ttu-id="9bce3-241">Класс AuthenticationContext предоставляет метод API для получения пользователя broker:</span><span class="sxs-lookup"><span data-stu-id="9bce3-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="9bce3-242">Манифест приложения должен иметь следующие разрешения на использование учетных записей в диспетчере учетных записей.</span><span class="sxs-lookup"><span data-stu-id="9bce3-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="9bce3-243">Дополнительные сведения см. на странице [AccountManager на сайте Android](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="9bce3-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="9bce3-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="9bce3-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="9bce3-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="9bce3-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="9bce3-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="9bce3-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="9bce3-247">URL-адрес центра и службы федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="9bce3-247">Authority URL and AD FS</span></span>
<span data-ttu-id="9bce3-248">Службы федерации Active Directory не считаются службой маркеров безопасности, поэтому необходимо включить обнаружение экземпляра службы и передать значение false в конструктор AuthenticationContext.</span><span class="sxs-lookup"><span data-stu-id="9bce3-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="9bce3-249">URL-адресу центра необходим экземпляр службы маркеров безопасности и [имя клиента](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="9bce3-249">The authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="9bce3-250">Запрос элементов кэша</span><span class="sxs-lookup"><span data-stu-id="9bce3-250">Querying cache items</span></span>
<span data-ttu-id="9bce3-251">Библиотека ADAL предоставляет кэш по умолчанию в SharedPrefrecens и несколько простых функций для запроса данных из кэша.</span><span class="sxs-lookup"><span data-stu-id="9bce3-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="9bce3-252">Вот как можно получить текущий кэш из AuthenticationContext.</span><span class="sxs-lookup"><span data-stu-id="9bce3-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="9bce3-253">Кроме того, можно предоставить собственную реализацию кэша, если вы хотите его настроить.</span><span class="sxs-lookup"><span data-stu-id="9bce3-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="9bce3-254">Поведения запроса</span><span class="sxs-lookup"><span data-stu-id="9bce3-254">Prompt behavior</span></span>
<span data-ttu-id="9bce3-255">ADAL предоставляет возможность указать, требуется ли отображать диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="9bce3-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="9bce3-256">При указании параметра PromptBehavior.Auto будет отображено диалоговое окно, только если маркер обновления недействителен и требуются учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="9bce3-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="9bce3-257">При указании параметра PromptBehavior.Always данные кэша игнорируются, и диалоговое окно запроса учетных данных будет отображаться всегда.</span><span class="sxs-lookup"><span data-stu-id="9bce3-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="9bce3-258">Автоматический запрос маркера из кэша и обновление</span><span class="sxs-lookup"><span data-stu-id="9bce3-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="9bce3-259">Автоматический запрос маркера не использует диалоговое окно запроса учетных данных и не требует от пользователя каких-либо действий.</span><span class="sxs-lookup"><span data-stu-id="9bce3-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="9bce3-260">Он возвращает маркер из кэша, если тот доступен.</span><span class="sxs-lookup"><span data-stu-id="9bce3-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="9bce3-261">Если срок действия маркера истек, метод попытается обновить его.</span><span class="sxs-lookup"><span data-stu-id="9bce3-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="9bce3-262">Если срок действия маркера обновления истек или маркер ошибочен, метод вызовет исключение AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="9bce3-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="9bce3-263">Также данный метод обеспечивает возможность выполнить синхронный вызов.</span><span class="sxs-lookup"><span data-stu-id="9bce3-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="9bce3-264">Для параметра callback используйте acquireTokenSilentSync или задайте значение null.</span><span class="sxs-lookup"><span data-stu-id="9bce3-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="9bce3-265">Диагностика</span><span class="sxs-lookup"><span data-stu-id="9bce3-265">Diagnostics</span></span>
<span data-ttu-id="9bce3-266">Ниже представлены основные источники информации для диагностики проблем.</span><span class="sxs-lookup"><span data-stu-id="9bce3-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="9bce3-267">Исключения</span><span class="sxs-lookup"><span data-stu-id="9bce3-267">Exceptions</span></span>
* <span data-ttu-id="9bce3-268">Журналы</span><span class="sxs-lookup"><span data-stu-id="9bce3-268">Logs</span></span>
* <span data-ttu-id="9bce3-269">Данные трассировки сети</span><span class="sxs-lookup"><span data-stu-id="9bce3-269">Network traces</span></span>

<span data-ttu-id="9bce3-270">Следует отметить, что в библиотеке наиболее важными для диагностики являются идентификаторы корреляции.</span><span class="sxs-lookup"><span data-stu-id="9bce3-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="9bce3-271">Вы можете установить собственные идентификаторы корреляции для отдельных запросов, если требуется сопоставить запрос ADAL с другими операциями в коде.</span><span class="sxs-lookup"><span data-stu-id="9bce3-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="9bce3-272">Если идентификатор корреляции не задан, то библиотека ADAL создает случайный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9bce3-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="9bce3-273">Все сообщения журнала и сетевые вызовы будут помечены этим идентификатором корреляции.</span><span class="sxs-lookup"><span data-stu-id="9bce3-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="9bce3-274">Генерируемый идентификатор изменяется при каждом запросе.</span><span class="sxs-lookup"><span data-stu-id="9bce3-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="9bce3-275">Исключения</span><span class="sxs-lookup"><span data-stu-id="9bce3-275">Exceptions</span></span>
<span data-ttu-id="9bce3-276">Исключения — это первый этап диагностики.</span><span class="sxs-lookup"><span data-stu-id="9bce3-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="9bce3-277">Мы стараемся предоставить содержательные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="9bce3-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="9bce3-278">Если вы не считаете какое-либо сообщение содержательным, пожалуйста, сообщите нам об этом.</span><span class="sxs-lookup"><span data-stu-id="9bce3-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="9bce3-279">Укажите такие сведения об устройстве, как модель и версия SDK.</span><span class="sxs-lookup"><span data-stu-id="9bce3-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="9bce3-280">Журналы</span><span class="sxs-lookup"><span data-stu-id="9bce3-280">Logs</span></span>
<span data-ttu-id="9bce3-281">Можно настроить библиотеку на создание сообщений журнала, которые будут использоваться для диагностики проблем.</span><span class="sxs-lookup"><span data-stu-id="9bce3-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="9bce3-282">Чтобы настроить ведение журнала, используйте следующую функцию обратного вызова, которая будет вызываться библиотекой ADAL для передачи сообщений журнала при их создании.</span><span class="sxs-lookup"><span data-stu-id="9bce3-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="9bce3-283">Сообщения могут записываться в файл пользовательского журнала, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9bce3-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="9bce3-284">К сожалению, нет стандартного способа получения журналов с устройств.</span><span class="sxs-lookup"><span data-stu-id="9bce3-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="9bce3-285">Существуют некоторые службы, которые могут в этом помочь.</span><span class="sxs-lookup"><span data-stu-id="9bce3-285">There are some services that can help you with this.</span></span> <span data-ttu-id="9bce3-286">Также вы можете создать свою службу, например для отправки файла на сервер.</span><span class="sxs-lookup"><span data-stu-id="9bce3-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="9bce3-287">Уровни протоколирования:</span><span class="sxs-lookup"><span data-stu-id="9bce3-287">These are the logging levels:</span></span>
* <span data-ttu-id="9bce3-288">Error (исключение);</span><span class="sxs-lookup"><span data-stu-id="9bce3-288">Error (exceptions)</span></span>
* <span data-ttu-id="9bce3-289">Warn (предупреждение);</span><span class="sxs-lookup"><span data-stu-id="9bce3-289">Warn (warning)</span></span>
* <span data-ttu-id="9bce3-290">Info (информирование);</span><span class="sxs-lookup"><span data-stu-id="9bce3-290">Info (information purposes)</span></span>
* <span data-ttu-id="9bce3-291">Verbose (дополнительные сведения).</span><span class="sxs-lookup"><span data-stu-id="9bce3-291">Verbose (more details)</span></span>

<span data-ttu-id="9bce3-292">Настройка уровня ведения журнала происходит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9bce3-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="9bce3-293">Все сообщения журнала передаются в logcat в дополнение ко всем обратным вызовам пользовательского журнала.</span><span class="sxs-lookup"><span data-stu-id="9bce3-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="9bce3-294">Ниже показано, как получить файл журнала из logcat.</span><span class="sxs-lookup"><span data-stu-id="9bce3-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="9bce3-295">Дополнительные сведения о командах adb см. на [странице сведений о logcat на сайте Android](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="9bce3-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="9bce3-296">Данные трассировки сети</span><span class="sxs-lookup"><span data-stu-id="9bce3-296">Network traces</span></span>
<span data-ttu-id="9bce3-297">Для перехвата HTTP-трафика, который создает библиотека ADAL, можно использовать различные инструменты.</span><span class="sxs-lookup"><span data-stu-id="9bce3-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="9bce3-298">Это очень полезно, если вы знакомы с протоколом OAuth или если необходимо предоставить диагностические сведения в корпорацию Майкрософт или другие каналы поддержки.</span><span class="sxs-lookup"><span data-stu-id="9bce3-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="9bce3-299">Fiddler является простым инструментом трассировки HTTP.</span><span class="sxs-lookup"><span data-stu-id="9bce3-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="9bce3-300">Используйте следующие ссылки для получения информации о правильной настройке инструмента Fiddler для записи сетевого трафика библиотеки ADAL.</span><span class="sxs-lookup"><span data-stu-id="9bce3-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="9bce3-301">Чтобы достичь положительного результата, средство трассировки, например Fiddler или Charles, должно быть настроено для записи незашифрованного трафика SSL.</span><span class="sxs-lookup"><span data-stu-id="9bce3-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="9bce3-302">Данные трассировки, записанные таким образом, могут содержать конфиденциальные сведения, такие как маркеры доступа, имена пользователей и пароли.</span><span class="sxs-lookup"><span data-stu-id="9bce3-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="9bce3-303">При использовании рабочих учетных записей не передавайте данные трассировки третьим сторонам.</span><span class="sxs-lookup"><span data-stu-id="9bce3-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="9bce3-304">Если для получения поддержки необходимо предоставить данные трассировки другому пользователю, воспроизведите проблему с временной учетной записью, используя имена пользователей и пароли, которые не будут использоваться для реальных пользователей.</span><span class="sxs-lookup"><span data-stu-id="9bce3-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="9bce3-305">Использование веб-сайта компании Telerik: [Настройка Fiddler для Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="9bce3-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="9bce3-306">Использование GitHub : [Настройка правил Fiddler для библиотеки ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="9bce3-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="9bce3-307">Режим диалогового окна</span><span class="sxs-lookup"><span data-stu-id="9bce3-307">Dialog mode</span></span>
<span data-ttu-id="9bce3-308">Метод acquireToken с нулевым первым параметром приведет к отображению диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9bce3-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="9bce3-309">Шифрование</span><span class="sxs-lookup"><span data-stu-id="9bce3-309">Encryption</span></span>
<span data-ttu-id="9bce3-310">ADAL шифрует маркеры и по умолчанию хранит их в SharedPreferences.</span><span class="sxs-lookup"><span data-stu-id="9bce3-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="9bce3-311">Вы можете подробно рассмотреть класс StorageHelper.</span><span class="sxs-lookup"><span data-stu-id="9bce3-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="9bce3-312">В Android 4.3 (API уровня 18) введено безопасное хранилище закрытых ключей AndroidKeyStore.</span><span class="sxs-lookup"><span data-stu-id="9bce3-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="9bce3-313">Библиотека ADAL использует это хранилище при работе с API уровня 18 и выше.</span><span class="sxs-lookup"><span data-stu-id="9bce3-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="9bce3-314">Если требуется использовать ADAL с более ранними версиями SDK, необходимо предоставить секретный ключ в AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="9bce3-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="9bce3-315">Запрос носителя OAuth2</span><span class="sxs-lookup"><span data-stu-id="9bce3-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="9bce3-316">Класс AuthenticationParameters предоставляет функциональные возможности для получения authorization_uri из запроса носителя OAuth2.</span><span class="sxs-lookup"><span data-stu-id="9bce3-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="9bce3-317">Файлы cookie сеанса в веб-представлении</span><span class="sxs-lookup"><span data-stu-id="9bce3-317">Session cookies in WebView</span></span>
<span data-ttu-id="9bce3-318">После закрытия приложения веб-представление Android не очищает файлы cookie сеанса.</span><span class="sxs-lookup"><span data-stu-id="9bce3-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="9bce3-319">Это можно сделать с помощью следующего примера кода.</span><span class="sxs-lookup"><span data-stu-id="9bce3-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="9bce3-320">Дополнительные сведения о файлах cookie см. на [странице сведений о CookieSyncManager на сайте Android](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="9bce3-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="9bce3-321">Переопределения ресурсов</span><span class="sxs-lookup"><span data-stu-id="9bce3-321">Resource overrides</span></span>
<span data-ttu-id="9bce3-322">Библиотека ADAL содержит строки на английском языке для элементов пользовательского интерфейса диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="9bce3-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="9bce3-323">Разработчику следует перезаписать эти сроки, если требуется их локализовать.</span><span class="sxs-lookup"><span data-stu-id="9bce3-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="9bce3-324">Диалоговое окно NTLM</span><span class="sxs-lookup"><span data-stu-id="9bce3-324">NTLM dialog box</span></span>
<span data-ttu-id="9bce3-325">Версия ADAL 1.1.0 поддерживает диалоговое окно NTLM, которое отображается по событию onReceivedHttpAuthRequest, поступающему из WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="9bce3-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="9bce3-326">Макет и строки диалогового окна можно настроить.</span><span class="sxs-lookup"><span data-stu-id="9bce3-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="9bce3-327">Единый вход для нескольких приложений</span><span class="sxs-lookup"><span data-stu-id="9bce3-327">Cross-app SSO</span></span>
<span data-ttu-id="9bce3-328">Узнайте, [как включить единый вход для нескольких приложений Android с помощью ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="9bce3-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
