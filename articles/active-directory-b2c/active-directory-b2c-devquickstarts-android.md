---
title: "Azure Active Directory B2C: получение токена с помощью приложения Android | Документация Майкрософт"
description: "В этой статье описывается, как создать приложение Android, которое использует AppAuth с Azure Active Directory B2C для управления удостоверениями пользователей и проверки подлинности пользователей."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="d78fa-103">Azure AD B2C. Вход с помощью приложения Android</span><span class="sxs-lookup"><span data-stu-id="d78fa-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="d78fa-104">Платформа Microsoft Identity использует открытые стандарты, такие как OAuth2 и OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="d78fa-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="d78fa-105">Это позволяет разработчикам использовать для интеграции со службами любые библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d78fa-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="d78fa-106">Чтобы объяснить разработчикам, как настроить сторонние библиотеки для подключения к платформе Microsoft Identity, мы написали несколько подобных этому пошаговых руководств.</span><span class="sxs-lookup"><span data-stu-id="d78fa-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="d78fa-107">Большинство библиотек, в которых реализована [спецификация RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) , смогут подключаться к платформе Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="d78fa-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="d78fa-108">Корпорация Майкрософт не предоставляет исправления для библиотек сторонних производителей и не выполняла их проверку.</span><span class="sxs-lookup"><span data-stu-id="d78fa-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="d78fa-109">В этом примере используется библиотека стороннего производителя с именем AppAuth, которая была протестирована в основных сценариях на совместимость со службой Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d78fa-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="d78fa-110">Проблемы и запросы возможностей следует отправлять в проекты с открытым кодом библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d78fa-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="d78fa-111">Дополнительные сведения см. в [этой статье](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="d78fa-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="d78fa-112">Если вы еще не работали с OAuth2 или OpenID Connect, вы не поймете большую часть примера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d78fa-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="d78fa-113">Для начала мы рекомендуем просмотреть [общие сведения о протоколе](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="d78fa-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="d78fa-114">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d78fa-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="d78fa-115">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="d78fa-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="d78fa-116">Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="d78fa-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="d78fa-117">Если каталог B2C еще не создан, [создайте его](active-directory-b2c-get-started.md), прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="d78fa-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="d78fa-118">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="d78fa-118">Create an application</span></span>

<span data-ttu-id="d78fa-119">Затем необходимо создать приложение в каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="d78fa-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="d78fa-120">Таким образом в Azure AD поступят сведения, необходимые для безопасного взаимодействия с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="d78fa-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="d78fa-121">Чтобы создать мобильное приложение, следуйте [этим инструкциям](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d78fa-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="d78fa-122">Не забудьте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="d78fa-122">Be sure to:</span></span>

* <span data-ttu-id="d78fa-123">Включите в приложение **собственный клиент**.</span><span class="sxs-lookup"><span data-stu-id="d78fa-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="d78fa-124">Скопируйте **идентификатор приложения** , назначенный приложению.</span><span class="sxs-lookup"><span data-stu-id="d78fa-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="d78fa-125">Этот идентификатор потребуется позднее.</span><span class="sxs-lookup"><span data-stu-id="d78fa-125">You will need this later.</span></span>
* <span data-ttu-id="d78fa-126">Настройте **URI перенаправления** собственного клиента (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="d78fa-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="d78fa-127">Этот идентификатор также потребуется позднее.</span><span class="sxs-lookup"><span data-stu-id="d78fa-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="d78fa-128">Создание политик</span><span class="sxs-lookup"><span data-stu-id="d78fa-128">Create your policies</span></span>

<span data-ttu-id="d78fa-129">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d78fa-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d78fa-130">Это приложение предусматривает одну процедуру идентификации, сочетающую в себе вход и регистрацию.</span><span class="sxs-lookup"><span data-stu-id="d78fa-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="d78fa-131">Вам нужно создать эту политику, как описано в [справочной статье о политиках](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="d78fa-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="d78fa-132">При создании политики обязательно сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d78fa-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="d78fa-133">Укажите **отображаемое имя** в качестве атрибута входа для политики.</span><span class="sxs-lookup"><span data-stu-id="d78fa-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="d78fa-134">Выберите утверждения приложения **Отображаемое имя** и **Идентификатор объекта** для каждой политики.</span><span class="sxs-lookup"><span data-stu-id="d78fa-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="d78fa-135">Можно также выбрать другие утверждения.</span><span class="sxs-lookup"><span data-stu-id="d78fa-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="d78fa-136">Скопируйте **имя** каждой созданной политики.</span><span class="sxs-lookup"><span data-stu-id="d78fa-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="d78fa-137">У него должен быть префикс `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="d78fa-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="d78fa-138">Эти имена политик понадобятся вам позже.</span><span class="sxs-lookup"><span data-stu-id="d78fa-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="d78fa-139">После создания политик можно приступать к сборке приложения.</span><span class="sxs-lookup"><span data-stu-id="d78fa-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="d78fa-140">Скачивание примера кода</span><span class="sxs-lookup"><span data-stu-id="d78fa-140">Download the sample code</span></span>

<span data-ttu-id="d78fa-141">Мы разместили рабочий пример, использующий AppAuth с Azure AD B2C, [на сайте GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="d78fa-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="d78fa-142">Вы можете скачать код и запустить его.</span><span class="sxs-lookup"><span data-stu-id="d78fa-142">You can download the code and run it.</span></span> <span data-ttu-id="d78fa-143">Вы можете быстро приступить к работе с приложением с использованием конфигурации Azure AD B2C, следуя инструкциям в разделе [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="d78fa-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="d78fa-144">Пример представляет собой измененную версию примера, предоставляемого [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="d78fa-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="d78fa-145">Посетите нашу страницу для получения дополнительных сведений об AppAuth и его функциях.</span><span class="sxs-lookup"><span data-stu-id="d78fa-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="d78fa-146">Изменение приложения для использования Azure AD B2C с AppAuth</span><span class="sxs-lookup"><span data-stu-id="d78fa-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="d78fa-147">AppAuth поддерживает Android API версии 16 (Jellybean) и более поздних.</span><span class="sxs-lookup"><span data-stu-id="d78fa-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="d78fa-148">Мы советуем использовать API версии 23 и более поздних.</span><span class="sxs-lookup"><span data-stu-id="d78fa-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="d78fa-149">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="d78fa-149">Configuration</span></span>

<span data-ttu-id="d78fa-150">Чтобы настроить взаимодействие с Azure AD B2C, укажите URI обнаружения или URI конечных точек авторизации и токенов.</span><span class="sxs-lookup"><span data-stu-id="d78fa-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="d78fa-151">В любом случае вам потребуются следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="d78fa-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="d78fa-152">идентификатор клиента (например, contoso.onmicrosoft.com);</span><span class="sxs-lookup"><span data-stu-id="d78fa-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="d78fa-153">имя политики (например, B2C\_1\_SignUpIn).</span><span class="sxs-lookup"><span data-stu-id="d78fa-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="d78fa-154">Если выбрано автоматическое обнаружение URI конечных точек авторизации и токенов, вам потребуется получить сведения из URI обнаружения.</span><span class="sxs-lookup"><span data-stu-id="d78fa-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="d78fa-155">URI обнаружения можно создать, заменив идентификатор \_клиента и имя\_политики в следующем URL-адресе:</span><span class="sxs-lookup"><span data-stu-id="d78fa-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="d78fa-156">Вы можете получить URI конечных точек авторизации и токенов, а также создать объект AuthorizationServiceConfiguration, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d78fa-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="d78fa-157">Вместо того, чтобы получать URI конечных точек авторизации и токенов путем обнаружения, их можно также явно определить, заменив идентификатор\_клиента и имя\_политики в приведенном ниже URL-адресе:</span><span class="sxs-lookup"><span data-stu-id="d78fa-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="d78fa-158">Выполните следующий код для создания объекта AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="d78fa-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="d78fa-159">Авторизация</span><span class="sxs-lookup"><span data-stu-id="d78fa-159">Authorizing</span></span>

<span data-ttu-id="d78fa-160">После настройки или извлечения конфигурации службы авторизации можно сформировать запрос авторизации.</span><span class="sxs-lookup"><span data-stu-id="d78fa-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="d78fa-161">Для создания запроса вам потребуются следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="d78fa-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="d78fa-162">идентификатор клиента (например, 00000000-0000-0000-0000-000000000000);</span><span class="sxs-lookup"><span data-stu-id="d78fa-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="d78fa-163">URI перенаправления с настраиваемой схемой (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect).</span><span class="sxs-lookup"><span data-stu-id="d78fa-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="d78fa-164">Оба элемента нужно сохранить при [регистрации приложения](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="d78fa-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="d78fa-165">Дополнительные сведения о завершении остальной части процесса см. в [руководстве по AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="d78fa-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="d78fa-166">Если вам нужно быстро приступить к работе с приложением, ознакомьтесь с [нашим примером](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="d78fa-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="d78fa-167">Следуйте указаниям в файле [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md), чтобы ввести собственные значения для настройки Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d78fa-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="d78fa-168">Мы всегда рады вашим отзывам и предложениям!</span><span class="sxs-lookup"><span data-stu-id="d78fa-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="d78fa-169">Если у вас возникли трудности с выполнением действий, описанных в этой статье или у вас есть рекомендации по улучшению этого материала, поделитесь с нами своими наблюдениями, воспользовавшись формой в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d78fa-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="d78fa-170">Запросы функций оставляйте на форуме [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="d78fa-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

