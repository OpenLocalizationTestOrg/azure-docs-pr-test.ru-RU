---
title: "Azure Active Directory B2C. Добавление Google+ в качестве поставщика удостоверений OAuth2 с помощью пользовательских политик"
description: "Пример использования Google+ в качестве поставщика удостоверений с помощью протокола OAuth2"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: e0aaf710d230f7667fff32b50ddb64104509d740
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="3b9e1-103">Azure Active Directory B2C. Добавление Google+ в качестве поставщика удостоверений OAuth2 с помощью пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="3b9e1-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="3b9e1-104">В этой статье описывается, как включить возможность входа для пользователей из учетной записи Google+ с помощью [пользовательских политик](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-104">This guide shows you how to enable sign-in for users from Google+ account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b9e1-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3b9e1-105">Prerequisites</span></span>

<span data-ttu-id="3b9e1-106">Выполните шаги, описанные в статье [Azure Active Directory B2C. Приступая к работе с настраиваемыми политиками](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="3b9e1-107">А именно:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-107">These steps include:</span></span>

1.  <span data-ttu-id="3b9e1-108">Создание учетной записи в приложении Google+.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="3b9e1-109">Добавление ключа учетной записи Google + в Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-109">Adding the Google+ account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="3b9e1-110">Добавление поставщика утверждений в политику.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="3b9e1-111">Регистрация поставщика утверждений учетной записи Google+ для пути взаимодействия пользователя</span><span class="sxs-lookup"><span data-stu-id="3b9e1-111">Registering the Google+ account claims provider to a user journey</span></span>
5.  <span data-ttu-id="3b9e1-112">Отправка политики в клиент Azure AD B2C и ее проверка.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="3b9e1-113">Создание приложения для учетной записи Google+</span><span class="sxs-lookup"><span data-stu-id="3b9e1-113">Create a Google+ account application</span></span>
<span data-ttu-id="3b9e1-114">Чтобы использовать Google+ в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение Google+ и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-114">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="3b9e1-115">Приложение Google+ можно зарегистрировать здесь: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="3b9e1-116">Перейдите на сайт [Google Developers Console](https://console.developers.google.com/) и выполните вход с учетной записью Google+.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-116">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="3b9e1-117">Щелкните **Create project** (Создать проект), введите значение в поле **Project name** (Имя проекта) и щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="3b9e1-118">Щелкните **меню проектов**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-118">Click on the **Projects menu**.</span></span>

    ![Учетная запись Google+, меню "Выберите проект"](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="3b9e1-120">Нажмите кнопку **+**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-120">Click on the **+** button.</span></span>

    ![Учетная запись Google+, создание проекта](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="3b9e1-122">Введите **имя проекта** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Учетная запись Google+, новый проект](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="3b9e1-124">Подождите, пока проект подготовится, и выберите **меню проектов**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-124">Wait until the project is ready and click on the **Projects menu**.</span></span>

    ![Учетная запись Google+; подождите, пока новый проект будет готов к использованию](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="3b9e1-126">Щелкните имя проекта.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-126">Click on your project name.</span></span>

    ![Учетная запись Google+, выбор нового проекта](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="3b9e1-128">В левой области навигации щелкните **API Manager** (Менеджер API), а затем — **Credentials** (Учетные данные).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-128">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
9.  <span data-ttu-id="3b9e1-129">Щелкните вкладку **OAuth consent screen** (Экран согласия OAuth) вверху.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-129">Click the **OAuth consent screen** tab at the top.</span></span>

    ![Учетная запись Google+, настройка окна запроса доступа OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="3b9e1-131">Выберите или укажите допустимый **электронный адрес**, заполните поле **Product name** (Название продукта) и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+, учетные данные приложения](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="3b9e1-133">Щелкните **New credentials** (Создать учетные данные) и выберите **OAuth client ID** (Идентификатор клиента OAuth).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+, создание учетных данных приложения](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="3b9e1-135">Из списка **Application type** (Тип приложения) выберите **Web application** (Веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+, выбор типа приложения](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="3b9e1-137">В поле **Name** (Имя) введите имя приложения, затем введите `https://login.microsoftonline.com` в поле **Authorized JavaScript origins** (Авторизованные источники JavaScript) и `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` — в поле **Authorized redirect URIs** (Авторизованные URI перенаправления).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="3b9e1-138">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="3b9e1-139">В значении **{клиент}** необходимо учитывать регистр.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-139">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="3b9e1-140">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-140">Click **Create**.</span></span>

    ![Google+, предоставление авторизованных источников JavaScript и URI перенаправления](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="3b9e1-142">Скопируйте значения **идентификатор клиента** и **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-142">Copy the values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="3b9e1-143">Они необходимы для настройки Google+ в качестве поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-143">You need both to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="3b9e1-144">**Секрет клиента** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-144">**Client secret** is an important security credential.</span></span>

    ![Google+, копирование значений идентификатора и секрета клиента](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-the-google-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="3b9e1-146">Добавление ключа учетной записи Google+ в Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="3b9e1-146">Add the Google+ account application key to Azure AD B2C</span></span>
<span data-ttu-id="3b9e1-147">Федерации с учетными записями Google+ нужен секрет клиента, чтобы учетная запись Google+ смогла установить отношения доверия с Azure AD B2C от имени приложения.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-147">Federation with Google+ accounts requires a client secret for Google+ account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="3b9e1-148">Вам необходимо сохранить секрет Google+ в клиенте Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-148">You need to store your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="3b9e1-149">Перейдите к клиенту Azure AD B2C и выберите **B2C Settings** (Параметры B2C)  > **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-149">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="3b9e1-150">Выберите **Policy Keys** (Ключи политики), чтобы просмотреть доступные в клиенте ключи.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-150">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="3b9e1-151">Щелкните **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="3b9e1-152">В пункте **Параметры** используйте вариант **Вручную**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="3b9e1-153">Для параметра **Имя** используйте значение `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="3b9e1-154">Префикс `B2C_1A_` может быть добавлен автоматически.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-154">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="3b9e1-155">В поле **Секрет** введите свой секрет приложения Майкрософт с сайта https://apps.dev.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-155">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="3b9e1-156">Для параметра **Использование ключа** задайте значение **Подпись**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="3b9e1-157">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="3b9e1-157">Click **Create**</span></span>
9.  <span data-ttu-id="3b9e1-158">Убедитесь, что вы создали ключ `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-158">Confirm that you've created the key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="3b9e1-159">Добавление поставщика утверждений в политику расширения</span><span class="sxs-lookup"><span data-stu-id="3b9e1-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="3b9e1-160">Чтобы пользователи выполняли вход с помощью учетной записи Google+, необходимо определить ее в качестве поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-160">If you want users to sign in by using Google+ account, you need to define Google+ account as a claims provider.</span></span> <span data-ttu-id="3b9e1-161">Другими словами, необходимо указать конечную точку, с которой взаимодействует Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-161">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="3b9e1-162">Конечная точка предоставляет набор утверждений, используемых Azure AD B2C, чтобы проверить, была ли выполнена проверка подлинности определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-162">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="3b9e1-163">Определите учетную запись Google+ в качестве поставщика утверждений, добавив узел `<ClaimsProvider>` в файл расширения политики:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="3b9e1-164">Откройте файл политики расширения (TrustFrameworkExtensions.xml) из рабочего каталога.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-164">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="3b9e1-165">Если вам нужен редактор XML, [попробуйте Visual Studio Code](https://code.visualstudio.com/download) — упрощенный кроссплатформенный редактор.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="3b9e1-166">Найдите раздел `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-166">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="3b9e1-167">Добавьте следующий фрагмент XML-кода в элемент `ClaimsProviders` и замените значение `client_id` на ваш идентификатор клиента учетной записи клиента Google+ перед сохранением файла.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-167">Add the following XML snippet under the `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving the file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want the user to select his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-google-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="3b9e1-168">Регистрация поставщика утверждений учетной записи Google+ для пути взаимодействия пользователя "Регистрация" или "Вход"</span><span class="sxs-lookup"><span data-stu-id="3b9e1-168">Register the Google+ account claims provider to Sign up or Sign in user journey</span></span>

<span data-ttu-id="3b9e1-169">Поставщик удостоверений настроен.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-169">The identity provider has been set up.</span></span>  <span data-ttu-id="3b9e1-170">Однако он недоступен ни на одном из экранов регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-170">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="3b9e1-171">Добавьте поставщик идентификатора учетной записи Google+ в пути взаимодействия пользователя `SignUpOrSignIn`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-171">Add the Google+ account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="3b9e1-172">Чтобы сделать его доступным, необходимо создать дубликат имеющегося шаблона пути взаимодействия пользователя,</span><span class="sxs-lookup"><span data-stu-id="3b9e1-172">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="3b9e1-173">а затем добавить поставщик удостоверений учетной записи Google+:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-173">Then we add the Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="3b9e1-174">Если вы скопировали элемент `<UserJourneys>` из основного файла политики в файл расширения (TrustFrameworkExtensions.xml), можно пропустить этот раздел.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-174">If you copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml), you can skip to this section.</span></span>

1.  <span data-ttu-id="3b9e1-175">Откройте базовый файл политики (например, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-175">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="3b9e1-176">Найдите элемент `<UserJourneys>` и скопируйте все содержимое узла `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-176">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="3b9e1-177">Откройте файл расширения (например, TrustFrameworkExtensions.xml) и найдите элемент `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-177">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="3b9e1-178">Если элемент не существует, добавьте его.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-178">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="3b9e1-179">Вставьте весь скопированный узел `<UserJournesy>` как дочерний узел элемента `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-179">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="3b9e1-180">Отображение кнопки</span><span class="sxs-lookup"><span data-stu-id="3b9e1-180">Display the button</span></span>
<span data-ttu-id="3b9e1-181">Элемент `<ClaimsProviderSelections>` определяет список параметров выбора поставщика утверждений и их порядок.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-181">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="3b9e1-182">Элемент `<ClaimsProviderSelection>` является аналогом кнопки поставщика удостоверений на странице регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-182">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="3b9e1-183">Если вы добавите для учетной записи Google+ элемент `<ClaimsProviderSelection>`, при переходе пользователя на страницу отобразится новая кнопка.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="3b9e1-184">Для этого:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-184">To add this element:</span></span>

1.  <span data-ttu-id="3b9e1-185">Найдите узел `<UserJourney>`, содержащий `Id="SignUpOrSignIn"` в скопированном пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-185">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="3b9e1-186">Найдите узел `<OrchestrationStep>`, содержащий `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-186">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="3b9e1-187">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="3b9e1-188">Связывание кнопки с действием</span><span class="sxs-lookup"><span data-stu-id="3b9e1-188">Link the button to an action</span></span>
<span data-ttu-id="3b9e1-189">Теперь, когда у вас есть кнопка, вам необходимо связать ее с действием.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-189">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="3b9e1-190">В этом случае действие — это возможность взаимодействия Azure AD B2C с учетной записью Google+ для получения токена.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-190">The action, in this case, is for Azure AD B2C to communicate with Google+ account to receive a token.</span></span>

1.  <span data-ttu-id="3b9e1-191">Найдите `<OrchestrationStep>`, который содержит `Order="2"` в узле `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-191">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="3b9e1-192">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="3b9e1-193">Убедитесь, что `Id` имеет то же значение, что и `TargetClaimsExchangeId` в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-193">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
> * <span data-ttu-id="3b9e1-194">Убедитесь, что для идентификатора `TechnicalProfileReferenceId` задано значение ранее созданного технического профиля (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-194">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="3b9e1-195">Отправка политики в клиент</span><span class="sxs-lookup"><span data-stu-id="3b9e1-195">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="3b9e1-196">На [портале Azure](https://portal.azure.com) переключитесь в [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) и откройте колонку **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-196">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="3b9e1-197">Выберите **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="3b9e1-198">Откройте колонку **Все политики**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-198">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="3b9e1-199">Щелкните **Отправить политику**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="3b9e1-200">Установите флажок **Перезаписать политику, если она существует**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-200">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="3b9e1-201">**Отправьте** файл TrustFrameworkExtensions.xml и немного подождите, чтобы удостовериться в отсутствии сбоя при проверке.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="3b9e1-202">Тестирование настраиваемой политики с помощью команды "Запустить сейчас"</span><span class="sxs-lookup"><span data-stu-id="3b9e1-202">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="3b9e1-203">Откройте **Параметры Azure AD B2C** и перейдите к элементу **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-203">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="3b9e1-204">Для использования команды **Запустить сейчас** необходимо, чтобы в клиенте было предварительно зарегистрировано хотя бы одно приложение.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-204">**Run now** requires at least one application to be preregistered on the tenant.</span></span> 
    >    <span data-ttu-id="3b9e1-205">Дополнительные сведения о регистрации приложений см. в статье [Azure AD B2C: начало работы](active-directory-b2c-get-started.md) или [Регистрация приложения](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-205">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="3b9e1-206">Откройте **B2C_1A_signup_signin**, отправленную вами пользовательскую политику проверяющей стороны.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-206">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="3b9e1-207">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="3b9e1-208">У вас должна появиться возможность входа с использованием учетной записи Google +.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-208">You should be able to sign in using Google+ account.</span></span>

## <a name="optional-register-the-google-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="3b9e1-209">[Необязательно] Регистрация поставщика утверждений учетной записи Google+ для пути взаимодействия пользователя "Изменение профиля"</span><span class="sxs-lookup"><span data-stu-id="3b9e1-209">[Optional] Register the Google+ account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="3b9e1-210">Вы также можете добавить поставщик удостоверений учетной записи Google+ для пути взаимодействия пользователя `ProfileEdit`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-210">You may want to add the Google+ account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="3b9e1-211">Чтобы сделать его доступным, необходимо повторить последние два шага:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-211">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="3b9e1-212">Отображение кнопки</span><span class="sxs-lookup"><span data-stu-id="3b9e1-212">Display the button</span></span>
1.  <span data-ttu-id="3b9e1-213">Откройте файл расширения политики (например, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="3b9e1-213">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="3b9e1-214">Найдите узел `<UserJourney>`, содержащий `Id="ProfileEdit"` в скопированном пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-214">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="3b9e1-215">Найдите узел `<OrchestrationStep>`, содержащий `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-215">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="3b9e1-216">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="3b9e1-217">Связывание кнопки с действием</span><span class="sxs-lookup"><span data-stu-id="3b9e1-217">Link the button to an action</span></span>
1.  <span data-ttu-id="3b9e1-218">Найдите `<OrchestrationStep>`, который содержит `Order="2"` в узле `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-218">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="3b9e1-219">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="3b9e1-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="3b9e1-220">Тестирование пользовательской политики изменения профиля с помощью команды "Запустить сейчас"</span><span class="sxs-lookup"><span data-stu-id="3b9e1-220">Test the custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="3b9e1-221">Откройте **Параметры Azure AD B2C** и перейдите к элементу **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-221">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="3b9e1-222">Откройте **B2C_1A_ProfileEdit**, отправленную пользовательскую политику проверяющей стороны.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-222">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="3b9e1-223">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="3b9e1-224">У вас должна появиться возможность входа с использованием учетной записи Google +.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-224">You should be able to sign in using Google+ account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="3b9e1-225">Загрузка завершенных файлов политики</span><span class="sxs-lookup"><span data-stu-id="3b9e1-225">Download the complete policy files</span></span>
<span data-ttu-id="3b9e1-226">Необязательно. Мы советуем создать свой сценарий, используя собственные файлы пользовательской политики, а не эти примеры файлов, после того, как вы ознакомитесь с пошаговым руководством по началу работы с пользовательскими политиками.</span><span class="sxs-lookup"><span data-stu-id="3b9e1-226">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="3b9e1-227">Примеры файлов политики для справки</span><span class="sxs-lookup"><span data-stu-id="3b9e1-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
