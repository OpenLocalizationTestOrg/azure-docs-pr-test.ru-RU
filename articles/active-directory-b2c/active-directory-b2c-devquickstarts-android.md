---
title: "Azure Active Directory B2C: получение токена с помощью приложения Android | Документация Майкрософт"
description: "В этой статье будет показано, как toocreate Android приложение, которое использует AppAuth с учетными данными пользователей Azure Active Directory B2C toomanage и проверки подлинности пользователей."
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
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="4a6b9-103">Azure AD B2C. Вход с помощью приложения Android</span><span class="sxs-lookup"><span data-stu-id="4a6b9-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="4a6b9-104">Hello платформы удостоверений использует открытых стандартов, такие как OAuth2 и OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="4a6b9-105">Это позволяет разработчикам tooleverage всех библиотек, которые они будут toointegrate с наших служб.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="4a6b9-106">Разработчики tooaid с помощью платформы с другими библиотеками, мы написали несколько пошаговых руководств, как это один toodemonstrate как tooconfigure сторонних производителей библиотеки tooconnect toohello платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="4a6b9-107">Большинство библиотек, которые реализуют [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) будут работать на платформе Microsoft Identity может tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="4a6b9-108">Корпорация Майкрософт не предоставляет исправления для библиотек сторонних производителей и не выполняла их проверку.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="4a6b9-109">В этом примере использует сторонних производителей библиотеку вызывается AppAuth которого была протестирована на совместимость в основных сценариях с Azure AD B2C hello.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="4a6b9-110">Проблемы и запрашивать новые функции должно быть проект с открытым исходным направленной toohello библиотеки.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="4a6b9-111">Дополнительные сведения см. в [этой статье](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="4a6b9-112">Если вы новый tooOAuth2 или OpenID Connect большая часть конфигурации этого образца может оказаться гораздо tooyou смысле.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="4a6b9-113">Рекомендуется рассмотреть приведен краткий [Обзор протокола hello, мы здесь описаны](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="4a6b9-114">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="4a6b9-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="4a6b9-115">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="4a6b9-116">Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="4a6b9-117">Если каталог B2C еще не создан, [создайте его](active-directory-b2c-get-started.md), прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="4a6b9-118">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="4a6b9-118">Create an application</span></span>

<span data-ttu-id="4a6b9-119">Далее необходимо toocreate приложения в каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="4a6b9-120">Это предоставляет сведения Azure AD, что ему требуется toocommunicate безопасно вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="4a6b9-121">toocreate мобильного приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="4a6b9-122">Не забудьте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-122">Be sure to:</span></span>

* <span data-ttu-id="4a6b9-123">Включить **Native Client** в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="4a6b9-124">Копировать hello **идентификатор приложения** , назначенный tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="4a6b9-125">Этот идентификатор потребуется позднее.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-125">You will need this later.</span></span>
* <span data-ttu-id="4a6b9-126">Настройте **URI перенаправления** собственного клиента (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="4a6b9-127">Этот идентификатор также потребуется позднее.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="4a6b9-128">Создание политик</span><span class="sxs-lookup"><span data-stu-id="4a6b9-128">Create your policies</span></span>

<span data-ttu-id="4a6b9-129">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4a6b9-130">Это приложение предусматривает одну процедуру идентификации, сочетающую в себе вход и регистрацию.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="4a6b9-131">Необходимые toocreate этой политики, как описано в [статье политики](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="4a6b9-132">При создании политики hello, нужно убедиться, что:</span><span class="sxs-lookup"><span data-stu-id="4a6b9-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="4a6b9-133">Выберите hello **отображаемое имя** как атрибут регистрации в политике.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="4a6b9-134">Выберите hello **отображаемое имя** и **идентификатор объекта** утверждений приложения в каждой политике.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="4a6b9-135">Можно также выбрать другие утверждения.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="4a6b9-136">Копировать hello **имя** каждой политики, после его создания.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="4a6b9-137">Он должен иметь префикс hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="4a6b9-138">Имя политики hello потребуется позднее.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="4a6b9-139">После создания политики вы готовы toobuild приложения.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="4a6b9-140">Загрузить пример кода hello</span><span class="sxs-lookup"><span data-stu-id="4a6b9-140">Download hello sample code</span></span>

<span data-ttu-id="4a6b9-141">Мы разместили рабочий пример, использующий AppAuth с Azure AD B2C, [на сайте GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="4a6b9-142">Можно загрузить кода hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-142">You can download hello code and run it.</span></span> <span data-ttu-id="4a6b9-143">Вы можете быстро приступить к работе с приложением с помощью Azure AD B2C конфигурацию в соответствии с инструкциями hello в hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="4a6b9-144">Образец Hello является модификацией образца hello, предоставляемые [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="4a6b9-145">Посетите их toolearn страницы, Дополнительные сведения о AppAuth и его компонентов.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="4a6b9-146">Изменение toouse вашего приложения Azure AD B2C, с AppAuth</span><span class="sxs-lookup"><span data-stu-id="4a6b9-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="4a6b9-147">AppAuth поддерживает Android API версии 16 (Jellybean) и более поздних.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="4a6b9-148">Мы советуем использовать API версии 23 и более поздних.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="4a6b9-149">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="4a6b9-149">Configuration</span></span>

<span data-ttu-id="4a6b9-150">Соединение можно настроить с помощью Azure AD B2C, либо указав обнаружение hello URI или указав конечную точку авторизации hello и маркера URI конечных точек.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="4a6b9-151">В любом случае потребуется hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="4a6b9-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="4a6b9-152">идентификатор клиента (например, contoso.onmicrosoft.com);</span><span class="sxs-lookup"><span data-stu-id="4a6b9-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="4a6b9-153">имя политики (например, B2C\_1\_SignUpIn).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="4a6b9-154">Если выбрана tooautomatically обнаружение hello авторизации и маркер URI конечных точек, вы должны будете toofetch сведения из процесса обнаружения hello URI.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="4a6b9-155">URI могут быть вызваны замена hello клиента обнаружения Hello\_идентификатор и политику hello\_имя в hello URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="4a6b9-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="4a6b9-156">Затем вы можете получать hello авторизации и маркеров URI конечных точек и создания объекта AuthorizationServiceConfiguration, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="4a6b9-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

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
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="4a6b9-157">Вместо обнаружения tooobtain hello авторизации и маркеров URI конечных точек, можно также указать их явным образом, заменив hello клиента\_идентификатор и политику hello\_имя в hello URL ниже:</span><span class="sxs-lookup"><span data-stu-id="4a6b9-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="4a6b9-158">Выполните следующий код toocreate hello объекта AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="4a6b9-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="4a6b9-159">Авторизация</span><span class="sxs-lookup"><span data-stu-id="4a6b9-159">Authorizing</span></span>

<span data-ttu-id="4a6b9-160">После настройки или извлечения конфигурации службы авторизации можно сформировать запрос авторизации.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="4a6b9-161">запрос toocreate hello, вам потребуется hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="4a6b9-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="4a6b9-162">идентификатор клиента (например, 00000000-0000-0000-0000-000000000000);</span><span class="sxs-lookup"><span data-stu-id="4a6b9-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="4a6b9-163">URI перенаправления с настраиваемой схемой (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="4a6b9-164">Оба элемента нужно сохранить при [регистрации приложения](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="4a6b9-165">См. toohello [AppAuth руководство](https://openid.github.io/AppAuth-Android/) на как toocomplete hello оставшаяся часть процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="4a6b9-166">Если вам требуется tooquickly Приступая к работе с работающем приложении, ознакомьтесь с [выборка](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="4a6b9-167">Следуйте указаниям hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter конфигурацию Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="4a6b9-168">Мы всегда являются предложения и откройте toofeedback!</span><span class="sxs-lookup"><span data-stu-id="4a6b9-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="4a6b9-169">Если возникли проблемы с этим разделом, или иметь рекомендации по улучшению это содержимое, мы ценим ваши отзывы hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="4a6b9-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="4a6b9-170">Для запросов, компонент, добавьте их слишком[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="4a6b9-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

