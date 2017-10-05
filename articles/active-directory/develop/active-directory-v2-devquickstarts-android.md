---
title: "Приложение Android версии 2.0 для Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как создать приложение Android, которое обеспечивает вход пользователей с помощью личной и рабочей или учебной учетной записи Майкрософт, а также использует вызовы API Graph на основе сторонних библиотек."
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
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="1bb3b-103">Добавление функции входа в приложение Android, использующее стороннюю библиотеку и API Graph, с помощью конечной точки версии 2.0</span><span class="sxs-lookup"><span data-stu-id="1bb3b-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="1bb3b-104">Платформа Microsoft Identity использует открытые стандарты, такие как OAuth2 и OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="1bb3b-105">Разработчики могут использовать любую библиотеку на свой выбор для интеграции с нашими службами.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="1bb3b-106">Чтобы помочь разработчикам с использованием нашей платформы с другими библиотеками, мы написали несколько подобных этому пошаговых руководств по настройке сторонних библиотеки для подключения к платформе Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="1bb3b-107">Большинство библиотек, в которых реализована [спецификация RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) , могут подключаться к платформе Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="1bb3b-108">Используя приложение, создаваемое в этом пошаговом руководстве, пользователи смогут войти в инфраструктуру своей организации и найти там себя с помощью API Graph.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="1bb3b-109">Если вы еще не работали с OAuth2 или OpenID Connect, то вы не поймете большую часть примера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="1bb3b-110">Мы рекомендуем прочитать раздел [Протоколы версии 2.0 — поток кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md), чтобы получить соответствующие сведения.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="1bb3b-111">Чтобы использовать функции платформы, которые описаны в этих стандартах OAuth2 или OpenID Connect, такие как управление политиками условного доступа и управление политиками Intune, требуются библиотеки Microsoft Azure Identity с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="1bb3b-112">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="1bb3b-113">Чтобы определить, следует ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="1bb3b-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="1bb3b-114">Скачивание кода с сайта GitHub</span><span class="sxs-lookup"><span data-stu-id="1bb3b-114">Download the code from GitHub</span></span>
<span data-ttu-id="1bb3b-115">Код в этом учебнике размещен на портале [GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="1bb3b-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="1bb3b-116">Для понимания процесса можно [скачать основу приложения как ZIP-файл](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) или клонировать ее.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="1bb3b-117">Можно также просто скачать пример и немедленно приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="1bb3b-118">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="1bb3b-118">Register an app</span></span>
<span data-ttu-id="1bb3b-119">Создайте новое приложение на [портале регистрации приложений](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните подробные инструкции по [регистрации приложения с использованием конечной точки версии 2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="1bb3b-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="1bb3b-120">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="1bb3b-120">Make sure to:</span></span>

* <span data-ttu-id="1bb3b-121">Скопируйте назначенный вашему приложению **идентификатор приложения**. Он вскоре вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="1bb3b-122">Добавьте для приложения **мобильную** платформу.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="1bb3b-123">Примечание. Портал регистрации приложений предоставляет значение **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="1bb3b-124">Однако в этом примере необходимо использовать значение по умолчанию `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="1bb3b-125">Скачивание сторонней библиотеки NXOAuth2 и создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="1bb3b-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="1bb3b-126">Для этого пошагового руководства вы воспользуетесь библиотекой OIDCAndroidLib с сайта GitHub. Это библиотека OAuth2, созданная на основе кода OpenID Connect от Google.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="1bb3b-127">Она реализует профиль собственного приложения и поддерживает конечную точку авторизации пользователей.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="1bb3b-128">Это все, что вам потребуется для интеграции с платформой Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="1bb3b-129">Клонируйте репозиторий OIDCAndroidLib на свой компьютер.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="1bb3b-131">Настройка среды Android Studio</span><span class="sxs-lookup"><span data-stu-id="1bb3b-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="1bb3b-132">Создайте новый проект Android Studio и примите значения по умолчанию в мастере.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Создание нового проекта в Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Целевые устройства Android](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Добавление действия для мобильных устройств](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="1bb3b-136">Чтобы установить модули проекта, переместите клонированный репозиторий в расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="1bb3b-137">Можно также сначала создать проект, а затем клонировать его непосредственно в расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![Модули проекта](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="1bb3b-139">Откройте параметры модулей проекта с помощью контекстного меню или нажав клавиши CTRL+ALT+SHIFT+S.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Параметры модулей проекта](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="1bb3b-141">Удалите модуль приложения по умолчанию, так как нам нужны только параметры контейнера проекта.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![Модуль приложения по умолчанию](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="1bb3b-143">Импортируйте модули из клонированного репозитория в текущий проект.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="1bb3b-144">![Импорт проекта gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![создать новую страницу модуля](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="1bb3b-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="1bb3b-145">Повторите эти действия для модуля `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="1bb3b-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="1bb3b-146">Проверьте зависимости oidclib в модуле `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="1bb3b-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![Зависимости oidclib в модуле oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="1bb3b-148">Нажмите кнопку **ОК** и дождитесь завершения синхронизации с Gradle.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="1bb3b-149">Раздел settings.gradle должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-149">Your settings.gradle should look like:</span></span>
   
    ![Снимок экрана settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="1bb3b-151">Выполните сборку примера приложения, чтобы убедиться, что он работает правильно.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="1bb3b-152">Вы пока не сможете использовать этот пример с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="1bb3b-153">Сначала необходимо настроить некоторые конечные точки.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="1bb3b-154">Так еще до начала настройки примера приложения мы сможем убедиться, что с Android Studio не возникают проблемы.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="1bb3b-155">Выполните сборку `oidlib-sample` и запустите его в Android Studio в качестве целевого приложения.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![Ход выполнения сборки oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="1bb3b-157">Удалите каталог `app ` , который остался после удаления модуля из проекта, так как в целях безопасности Android Studio не удаляет его.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Структура файлов, содержащая каталог приложения](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="1bb3b-159">Откройте меню **Изменить конфигурации** , чтобы удалить конфигурацию запуска, которая также осталась после удаления модуля из проекта.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="1bb3b-160">![Меню "Изменить конфигурации"](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Конфигурация запуска приложения](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="1bb3b-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="1bb3b-161">Настройка конечных точек примера</span><span class="sxs-lookup"><span data-stu-id="1bb3b-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="1bb3b-162">После успешного запуска `oidlib-sample` можно приступить к изменению некоторых конечных точек для их подключения к Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="1bb3b-163">Настройка клиента посредством редактирования файла oidc_clientconf.xml</span><span class="sxs-lookup"><span data-stu-id="1bb3b-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="1bb3b-164">Так как для получения токена и вызова API Graph используются потоки OAuth2, настроим для клиента только протокол OAuth2.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="1bb3b-165">В примере, который станет доступен позже, мы будем использовать OIDC.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="1bb3b-166">Настройте идентификатор клиента, полученный с портала регистрации.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="1bb3b-167">Настройте универсальный код ресурса (URI) перенаправления, указав приведенное ниже значение.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="1bb3b-168">Настройте области, необходимые для доступа к API Graph.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="1bb3b-169">Значение `User.Read` в `oidc_scopes` позволяет считывать базовый профиль вошедшего пользователя.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="1bb3b-170">Дополнительные сведения о всех доступных областях действия см. в разделе [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes) (Области действия разрешений Microsoft Graph).</span><span class="sxs-lookup"><span data-stu-id="1bb3b-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="1bb3b-171">Пояснения об использовании `openid` или `offline_access` в качестве областей действия в OpenID Connect см. в разделе [Протоколы версии 2.0 — поток кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="1bb3b-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="1bb3b-172">Настройка конечных точек клиента посредством редактирования файла oidc_endpoints.xml</span><span class="sxs-lookup"><span data-stu-id="1bb3b-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="1bb3b-173">Откройте файл `oidc_endpoints.xml` и внесите в него следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="1bb3b-174">Если используется протокол OAuth2, эти конечные точки никогда не должны изменяться.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="1bb3b-175">В настоящее время конечные точки для `userInfoEndpoint` и `revocationEndpoint` не поддерживаются в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="1bb3b-176">Если оставить значение по умолчанию example.com, то появится напоминание о том, в примере они недоступны.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="1bb3b-177">Настройка вызова API Graph</span><span class="sxs-lookup"><span data-stu-id="1bb3b-177">Configure a Graph API call</span></span>
* <span data-ttu-id="1bb3b-178">Откройте файл `HomeActivity.java` и внесите в него следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="1bb3b-179">Здесь простой вызов API Graph возвращает нашу информацию.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="1bb3b-180">Это все изменения, которые необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="1bb3b-181">Запустите приложение `oidlib-sample` и щелкните **Sign in**(Войти).</span><span class="sxs-lookup"><span data-stu-id="1bb3b-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="1bb3b-182">После аутентификации нажмите кнопку **Request Protected Resource** (Запросить защищенный ресурс), чтобы проверить вызов к API Graph.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="1bb3b-183">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="1bb3b-183">Get security updates for our product</span></span>
<span data-ttu-id="1bb3b-184">Рекомендуем вам получать уведомления об инцидентах безопасности. Для этого посетите [Технический центр безопасности](https://technet.microsoft.com/security/dd252948) и подпишитесь на уведомления о советах безопасности.</span><span class="sxs-lookup"><span data-stu-id="1bb3b-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

