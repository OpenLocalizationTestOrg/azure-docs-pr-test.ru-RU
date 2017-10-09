---
title: "Azure AD B2C: получение токена с помощью приложения iOS | Документация Майкрософт"
description: "В этой статье будет показано, как toocreate приложения iOS, использующее AppAuth удостоверений пользователей Azure Active Directory B2C toomanage и с проверки подлинности пользователей."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="e16a0-103">Azure AD B2C. Вход с помощью приложения iOS</span><span class="sxs-lookup"><span data-stu-id="e16a0-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="e16a0-104">Hello платформы удостоверений использует открытых стандартов, такие как OAuth2 и OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="e16a0-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="e16a0-105">Использование открытый стандартный протокол предоставляет широкий выбор разработчик, при выборе toointegrate библиотеки с помощью наших служб.</span><span class="sxs-lookup"><span data-stu-id="e16a0-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="e16a0-106">Мы предоставили данного пошагового руководства и других подобных тем tooaid разработчики при написании приложения, которые подключаются toohello платформы Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="e16a0-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="e16a0-107">Большинство библиотек, которые реализуют [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) являются платформой удостоверений Microsoft может tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="e16a0-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="e16a0-108">Корпорация Майкрософт не предоставляет исправления для библиотек сторонних производителей и не выполняла их проверку.</span><span class="sxs-lookup"><span data-stu-id="e16a0-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="e16a0-109">Этот образец использует стороннюю библиотеку, вызывается AppAuth которого была протестирована на совместимость в основных сценариях с Azure AD B2C hello.</span><span class="sxs-lookup"><span data-stu-id="e16a0-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="e16a0-110">Проблемы и запрашивать новые функции должно быть проект с открытым исходным направленной toohello библиотеки.</span><span class="sxs-lookup"><span data-stu-id="e16a0-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="e16a0-111">Дополнительные сведения см. в [этой статье](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="e16a0-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="e16a0-112">Если вы новый tooOAuth2 или OpenID Connect, большая часть конфигурации этого образца может оказаться гораздо tooyou смысле.</span><span class="sxs-lookup"><span data-stu-id="e16a0-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="e16a0-113">Рекомендуется рассмотреть приведен краткий [Обзор протокола hello, мы здесь описаны](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="e16a0-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="e16a0-114">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e16a0-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="e16a0-115">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="e16a0-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="e16a0-116">Каталог — это контейнер для всех пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="e16a0-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="e16a0-117">Если каталог B2C еще не создан, [создайте его](active-directory-b2c-get-started.md), прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="e16a0-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="e16a0-118">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="e16a0-118">Create an application</span></span>
<span data-ttu-id="e16a0-119">Далее необходимо toocreate приложения в каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="e16a0-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="e16a0-120">Регистрация приложения Hello информация Azure AD, он должен toocommunicate безопасно вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="e16a0-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="e16a0-121">toocreate мобильного приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="e16a0-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="e16a0-122">Не забудьте сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="e16a0-122">Be sure to:</span></span>

* <span data-ttu-id="e16a0-123">Включить **Native client** в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e16a0-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="e16a0-124">Копировать hello **идентификатор приложения** , назначенный tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="e16a0-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="e16a0-125">Этот GUID понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="e16a0-125">You need this GUID later.</span></span>
* <span data-ttu-id="e16a0-126">Задайте **URI перенаправления** с настраиваемой схемой (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="e16a0-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="e16a0-127">Этот URI понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="e16a0-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="e16a0-128">Создание политик</span><span class="sxs-lookup"><span data-stu-id="e16a0-128">Create your policies</span></span>
<span data-ttu-id="e16a0-129">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e16a0-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="e16a0-130">Это приложение предусматривает одну процедуру идентификации, сочетающую в себе вход и регистрацию.</span><span class="sxs-lookup"><span data-stu-id="e16a0-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="e16a0-131">Создайте эту политику, как описано в [справочной статье о политиках](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="e16a0-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="e16a0-132">При создании политики hello, нужно убедиться, что:</span><span class="sxs-lookup"><span data-stu-id="e16a0-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="e16a0-133">В разделе **регистрации атрибуты**выберите атрибут hello **отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="e16a0-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="e16a0-134">Можно также выбрать другие атрибуты.</span><span class="sxs-lookup"><span data-stu-id="e16a0-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="e16a0-135">В разделе **утверждений приложения**, выберите hello утверждений **отображаемое имя** и **идентификатор объекта пользователя**.</span><span class="sxs-lookup"><span data-stu-id="e16a0-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="e16a0-136">Можно также выбрать другие утверждения.</span><span class="sxs-lookup"><span data-stu-id="e16a0-136">You can select other claims as well.</span></span>
* <span data-ttu-id="e16a0-137">Копировать hello **имя** каждой политики, после его создания.</span><span class="sxs-lookup"><span data-stu-id="e16a0-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="e16a0-138">Имя политики добавляется префикс с `b2c_1_` при сохранении политики hello.</span><span class="sxs-lookup"><span data-stu-id="e16a0-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="e16a0-139">Требуется имя политики hello позже.</span><span class="sxs-lookup"><span data-stu-id="e16a0-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="e16a0-140">После создания политики вы готовы toobuild приложения.</span><span class="sxs-lookup"><span data-stu-id="e16a0-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="e16a0-141">Загрузить пример кода hello</span><span class="sxs-lookup"><span data-stu-id="e16a0-141">Download hello sample code</span></span>
<span data-ttu-id="e16a0-142">Мы разместили рабочий пример, использующий AppAuth с Azure AD B2C, [на сайте GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="e16a0-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="e16a0-143">Можно загрузить кода hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="e16a0-143">You can download hello code and run it.</span></span> <span data-ttu-id="e16a0-144">toouse собственные Azure AD B2C клиента, следуйте инструкциям hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e16a0-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="e16a0-145">В этом примере был создан в соответствии с инструкциями hello README по hello [iOS AppAuth проекта на GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="e16a0-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="e16a0-146">Дополнительные сведения о работе образец hello и библиотеки hello ссылаться hello README AppAuth на GitHub.</span><span class="sxs-lookup"><span data-stu-id="e16a0-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="e16a0-147">Изменение toouse вашего приложения Azure AD B2C, с AppAuth</span><span class="sxs-lookup"><span data-stu-id="e16a0-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="e16a0-148">AppAuth поддерживает iOS 7 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="e16a0-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="e16a0-149">Однако toosupport социальных имена входа в Google, SFSafariViewController потребуется которых требуется iOS 9 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e16a0-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="e16a0-150">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="e16a0-150">Configuration</span></span>

<span data-ttu-id="e16a0-151">Соединение с Azure AD B2C можно настроить, указав конечную точку авторизации hello и маркера URI конечных точек.</span><span class="sxs-lookup"><span data-stu-id="e16a0-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="e16a0-152">toogenerate эти URI необходимо hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="e16a0-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="e16a0-153">идентификатор клиента (например, contoso.onmicrosoft.com);</span><span class="sxs-lookup"><span data-stu-id="e16a0-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="e16a0-154">имя политики (например, B2C\_1\_SignUpIn).</span><span class="sxs-lookup"><span data-stu-id="e16a0-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="e16a0-155">Hello конечная точка маркера URI могут быть вызваны замена hello клиента\_идентификатор и политику hello\_имя в hello URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="e16a0-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="e16a0-156">Hello конечную точку авторизации URI могут быть вызваны замена hello клиента\_идентификатор и политику hello\_имя в hello URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="e16a0-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="e16a0-157">Выполните следующий код toocreate hello объекта AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="e16a0-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="e16a0-158">Авторизация</span><span class="sxs-lookup"><span data-stu-id="e16a0-158">Authorizing</span></span>

<span data-ttu-id="e16a0-159">После настройки или извлечения конфигурации службы авторизации можно сформировать запрос авторизации.</span><span class="sxs-lookup"><span data-stu-id="e16a0-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="e16a0-160">запрос toocreate hello, требуется hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="e16a0-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="e16a0-161">идентификатор клиента (например, 00000000-0000-0000-0000-000000000000);</span><span class="sxs-lookup"><span data-stu-id="e16a0-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="e16a0-162">URI перенаправления с настраиваемой схемой (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="e16a0-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="e16a0-163">Оба элемента нужно сохранить при [регистрации приложения](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="e16a0-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="e16a0-164">tooset копирование вашего приложения toohandle hello перенаправления toohello URI со схемой пользовательские hello список hello tooupdate «Схем URL-адрес» в необходимы вашей Info.pList.</span><span class="sxs-lookup"><span data-stu-id="e16a0-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="e16a0-165">Откройте файл Info.pList.</span><span class="sxs-lookup"><span data-stu-id="e16a0-165">Open Info.pList.</span></span>
* <span data-ttu-id="e16a0-166">Наведите указатель на строку как «Пакет ОС типа кода» и нажмите кнопку hello \+ символов.</span><span class="sxs-lookup"><span data-stu-id="e16a0-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="e16a0-167">Переименуйте hello новый строку «URL-адрес типы».</span><span class="sxs-lookup"><span data-stu-id="e16a0-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="e16a0-168">Щелкните hello стрелка влево toohello дерева hello tooopen «Типы URL-адрес».</span><span class="sxs-lookup"><span data-stu-id="e16a0-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="e16a0-169">Щелкните hello стрелка toohello слева от «0 элементов"tooopen hello дерева.</span><span class="sxs-lookup"><span data-stu-id="e16a0-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="e16a0-170">Переименуйте первый элемент, под элемент 0 too'URL схемы.</span><span class="sxs-lookup"><span data-stu-id="e16a0-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="e16a0-171">Щелкните hello стрелка влево toohello дерева hello tooopen «URL-схем».</span><span class="sxs-lookup"><span data-stu-id="e16a0-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="e16a0-172">В столбце «Значение» hello, остается пустым полем toohello элемента «Элемент 0"под «URL-схем».</span><span class="sxs-lookup"><span data-stu-id="e16a0-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="e16a0-173">Задайте приложение для hello значение tooyour уникальную схему.</span><span class="sxs-lookup"><span data-stu-id="e16a0-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="e16a0-174">Hello значение должно соответствовать hello схемы, используемой в redirectURL, при создании объекта OIDAuthorizationRequest hello.</span><span class="sxs-lookup"><span data-stu-id="e16a0-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="e16a0-175">В нашем примере мы использовали схему hello «com.onmicrosoft.fabrikamb2c.exampleapp».</span><span class="sxs-lookup"><span data-stu-id="e16a0-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="e16a0-176">См. toohello [AppAuth руководство](https://openid.github.io/AppAuth-iOS/) на как toocomplete hello оставшаяся часть процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="e16a0-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="e16a0-177">Если вам требуется tooquickly Приступая к работе с работающем приложении, ознакомьтесь с [выборка](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="e16a0-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="e16a0-178">Следуйте указаниям hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter конфигурацию Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e16a0-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="e16a0-179">Мы всегда являются предложения и откройте toofeedback!</span><span class="sxs-lookup"><span data-stu-id="e16a0-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="e16a0-180">Если возникли проблемы с этим разделом, или иметь рекомендации по улучшению это содержимое, мы ценим ваши отзывы hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="e16a0-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="e16a0-181">Для запросов, компонент, добавьте их слишком[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="e16a0-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
