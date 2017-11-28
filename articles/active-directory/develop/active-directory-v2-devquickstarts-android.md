---
title: "приложение Android v2.0 Active Directory aaaAzure | Документы Microsoft"
description: "Как приложение Android, выполняющий вход пользователей с личной учетной записи Майкрософт и рабочих или учебных учетных записей и вызовы toobuild hello Graph API с помощью библиотек сторонних производителей."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="f340a-103">Добавить tooan входа в приложение Android с помощью библиотеки сторонних разработчиков с API Graph с помощью конечной точки v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="f340a-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="f340a-104">Hello платформы удостоверений использует открытых стандартов, такие как OAuth2 и OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f340a-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="f340a-105">Разработчики могут использовать любую библиотеку, они должны toointegrate с наших служб.</span><span class="sxs-lookup"><span data-stu-id="f340a-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="f340a-106">toohelp разработчики используют нашей платформы с другими библиотеками, мы написали несколько пошаговых руководств, как это один toodemonstrate как tooconfigure сторонних библиотек tooconnect toohello платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f340a-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="f340a-107">Большинство библиотек, которые реализуют [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) могут подключаться toohello платформы удостоверений.</span><span class="sxs-lookup"><span data-stu-id="f340a-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="f340a-108">С помощью приложения hello, создает в этом пошаговом руководстве пользователей можно войти в организации tootheir и выполните поиск сами в своей организации с помощью Graph API hello.</span><span class="sxs-lookup"><span data-stu-id="f340a-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="f340a-109">Если вы новый tooOAuth2 или OpenID Connect, большая часть конфигурации этого образца может оказаться tooyou смысле.</span><span class="sxs-lookup"><span data-stu-id="f340a-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="f340a-110">Мы рекомендуем прочитать раздел [Протоколы версии 2.0 — поток кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md), чтобы получить соответствующие сведения.</span><span class="sxs-lookup"><span data-stu-id="f340a-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="f340a-111">Некоторые возможности платформы, имеющие выражения в hello OAuth2 или OpenID Connect стандартами, например условный доступ и управление политикой Intune, требуется вы toouse нашей открытой библиотеки удостоверений Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f340a-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="f340a-112">Конечная точка v2.0 Hello не поддерживает все сценарии Azure Active Directory и возможности.</span><span class="sxs-lookup"><span data-stu-id="f340a-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="f340a-113">toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="f340a-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="f340a-114">Загрузка кода hello из GitHub</span><span class="sxs-lookup"><span data-stu-id="f340a-114">Download hello code from GitHub</span></span>
<span data-ttu-id="f340a-115">поддерживается Hello кода для этого учебника [на GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="f340a-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="f340a-116">можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) или основу hello клона:</span><span class="sxs-lookup"><span data-stu-id="f340a-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="f340a-117">Можно также просто загрузить образец hello и начать работу прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="f340a-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="f340a-118">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="f340a-118">Register an app</span></span>
<span data-ttu-id="f340a-119">Создание нового приложения в hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните hello подробное описание действий по [как tooregister приложения с конечной точкой v2.0 hello](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f340a-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="f340a-120">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="f340a-120">Make sure to:</span></span>

* <span data-ttu-id="f340a-121">Копировать hello **идентификатор приложения** это назначенные tooyour приложения, так как он понадобится скоро.</span><span class="sxs-lookup"><span data-stu-id="f340a-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="f340a-122">Добавить hello **Mobile** платформы для приложения.</span><span class="sxs-lookup"><span data-stu-id="f340a-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="f340a-123">Примечание: предоставляет портал регистрации приложения hello **URI перенаправления** значение.</span><span class="sxs-lookup"><span data-stu-id="f340a-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="f340a-124">Однако в этом примере необходимо использовать значение по умолчанию hello `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="f340a-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="f340a-125">Загрузить библиотеки стороннего NXOAuth2 hello и создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="f340a-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="f340a-126">В этом пошаговом руководстве будет использоваться hello OIDCAndroidLib из GitHub, который является библиотекой OAuth2 основании hello код Google OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f340a-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="f340a-127">Он реализует профиля собственное приложение hello и поддерживает конечную точку авторизации hello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="f340a-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="f340a-128">Это все, что hello потребуется toointegrate с платформой удостоверений Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="f340a-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="f340a-129">Клонирование репозитория tooyour hello OIDCAndroidLib компьютера.</span><span class="sxs-lookup"><span data-stu-id="f340a-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="f340a-131">Настройка среды Android Studio</span><span class="sxs-lookup"><span data-stu-id="f340a-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="f340a-132">Создайте новый проект Android Studio и примите значения по умолчанию hello в мастере hello.</span><span class="sxs-lookup"><span data-stu-id="f340a-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![Создание нового проекта в Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Целевые устройства Android](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Добавить действие toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="f340a-136">tooset проекта модулей переместить расположение проекта toohello hello клонирования репозитория.</span><span class="sxs-lookup"><span data-stu-id="f340a-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="f340a-137">Можно также создать проект hello и клонируйте его непосредственно toohello расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="f340a-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![Модули проекта](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="f340a-139">Откройте параметры модулей hello проекта с помощью контекстного меню hello, или с помощью клавиш Ctrl + Alt + Осно + S hello.</span><span class="sxs-lookup"><span data-stu-id="f340a-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Параметры модулей проекта](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="f340a-141">Удалите модуль приложения по умолчанию hello, так как требуется только параметры проекта hello.</span><span class="sxs-lookup"><span data-stu-id="f340a-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![Модуль приложения по умолчанию Hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="f340a-143">Импортировать модули из hello клонированного репозитория toohello текущего проекта.</span><span class="sxs-lookup"><span data-stu-id="f340a-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="f340a-144">![Импорт проекта gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![создать новую страницу модуля](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="f340a-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="f340a-145">Повторите эти шаги для hello `oidlib-sample` модуля.</span><span class="sxs-lookup"><span data-stu-id="f340a-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="f340a-146">Проверка зависимостей oidclib hello на hello `oidlib-sample` модуля.</span><span class="sxs-lookup"><span data-stu-id="f340a-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![oidclib зависимости от модуля oidlib образец hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="f340a-148">Нажмите кнопку **ОК** и дождитесь завершения синхронизации с Gradle.</span><span class="sxs-lookup"><span data-stu-id="f340a-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="f340a-149">Раздел settings.gradle должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f340a-149">Your settings.gradle should look like:</span></span>
   
    ![Снимок экрана settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="f340a-151">Построение toomake пример приложения hello убедиться, что этот образец hello работает правильно.</span><span class="sxs-lookup"><span data-stu-id="f340a-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="f340a-152">Вы не будет возможности toouse это в Azure Active Directory еще.</span><span class="sxs-lookup"><span data-stu-id="f340a-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="f340a-153">Нам нужно tooconfigure некоторые конечные точки сначала.</span><span class="sxs-lookup"><span data-stu-id="f340a-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="f340a-154">Это tooensure Android Studio проблем нет, прежде чем начать настройку пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f340a-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="f340a-155">Построение и запуск `oidlib-sample` hello в качестве назначения Android Studio.</span><span class="sxs-lookup"><span data-stu-id="f340a-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![Ход выполнения сборки oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="f340a-157">Удалить hello `app ` каталог, была оставлена при удалении модуля hello из проекта hello, так как Android Studio не удаляет его в целях безопасности.</span><span class="sxs-lookup"><span data-stu-id="f340a-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Структура файлов, которая включает в себя каталог приложения hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="f340a-159">Откройте hello **изменение конфигураций** меню tooremove hello запустить конфигурацию, которая также была оставлена при удалении модуля hello из проекта hello.</span><span class="sxs-lookup"><span data-stu-id="f340a-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="f340a-160">![Меню "Изменить конфигурации"](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Конфигурация запуска приложения](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="f340a-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="f340a-161">Настройка конечных точек hello образца hello</span><span class="sxs-lookup"><span data-stu-id="f340a-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="f340a-162">Теперь, когда имеется hello `oidlib-sample` выполняется успешно, изменим tooget некоторые конечные точки этой работы с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f340a-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="f340a-163">Настроить клиент путем редактирования файла oidc_clientconf.xml hello</span><span class="sxs-lookup"><span data-stu-id="f340a-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="f340a-164">Поскольку используется только tooget потоки OAuth2 маркер и вызвать hello Graph API, установите hello toodo клиента OAuth2 только.</span><span class="sxs-lookup"><span data-stu-id="f340a-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="f340a-165">В примере, который станет доступен позже, мы будем использовать OIDC.</span><span class="sxs-lookup"><span data-stu-id="f340a-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="f340a-166">Настройте ИД клиента, полученный из портала регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="f340a-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="f340a-167">Настройте на URI перенаправления с одной hello ниже.</span><span class="sxs-lookup"><span data-stu-id="f340a-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="f340a-168">Настройка областей, вы должны в порядке tooaccess hello Graph API.</span><span class="sxs-lookup"><span data-stu-id="f340a-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="f340a-169">Hello `User.Read` значение в `oidc_scopes` позволяет вам tooread hello базовый профиль hello вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="f340a-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="f340a-170">Дополнительные сведения о всех доступных областей hello в [области разрешений Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="f340a-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="f340a-171">Пояснения об использовании `openid` или `offline_access` в качестве областей действия в OpenID Connect см. в разделе [Протоколы версии 2.0 — поток кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="f340a-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="f340a-172">Настройте конечные точки клиента, изменив файл oidc_endpoints.xml hello</span><span class="sxs-lookup"><span data-stu-id="f340a-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="f340a-173">Откройте hello `oidc_endpoints.xml` и создайте hello следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="f340a-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="f340a-174">Если используется протокол OAuth2, эти конечные точки никогда не должны изменяться.</span><span class="sxs-lookup"><span data-stu-id="f340a-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="f340a-175">Здравствуйте, конечные точки для `userInfoEndpoint` и `revocationEndpoint` в настоящее время не поддерживаются в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f340a-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="f340a-176">Если оставить эти значения example.com по умолчанию hello, появится напоминание, они недоступны в образце hello :-)</span><span class="sxs-lookup"><span data-stu-id="f340a-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="f340a-177">Настройка вызова API Graph</span><span class="sxs-lookup"><span data-stu-id="f340a-177">Configure a Graph API call</span></span>
* <span data-ttu-id="f340a-178">Откройте hello `HomeActivity.java` и создайте hello следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="f340a-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="f340a-179">Здесь простой вызов API Graph возвращает нашу информацию.</span><span class="sxs-lookup"><span data-stu-id="f340a-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="f340a-180">Это и есть все изменения hello необходимые toodo.</span><span class="sxs-lookup"><span data-stu-id="f340a-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="f340a-181">Запустите hello `oidlib-sample` приложения и нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="f340a-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="f340a-182">После вы успешно прошли проверку подлинности, выберите hello **запроса защищенный ресурс** кнопку tootest вашей toohello вызова Graph API.</span><span class="sxs-lookup"><span data-stu-id="f340a-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="f340a-183">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="f340a-183">Get security updates for our product</span></span>
<span data-ttu-id="f340a-184">Мы рекомендуем вам tooget уведомления об инцидентах безопасности, перейдя по адресу hello [Технический центр безопасности](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.</span><span class="sxs-lookup"><span data-stu-id="f340a-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

