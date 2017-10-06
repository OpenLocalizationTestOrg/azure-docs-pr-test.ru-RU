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
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="b0757-103">Azure Active Directory B2C. Добавление Google+ в качестве поставщика удостоверений OAuth2 с помощью пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="b0757-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="b0757-104">В этом руководстве показано, как tooenable вход для пользователей с учетной записью Google + за счет использования hello [настраиваемые политики](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b0757-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0757-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b0757-105">Prerequisites</span></span>

<span data-ttu-id="b0757-106">Hello завершения шагов в hello [Приступая к работе с помощью настроенных политик](active-directory-b2c-get-started-custom.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="b0757-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="b0757-107">А именно:</span><span class="sxs-lookup"><span data-stu-id="b0757-107">These steps include:</span></span>

1.  <span data-ttu-id="b0757-108">Создание учетной записи в приложении Google+.</span><span class="sxs-lookup"><span data-stu-id="b0757-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="b0757-109">Добавление hello Google + учетная запись приложения ключа tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="b0757-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="b0757-110">Добавление политики tooa поставщика утверждений</span><span class="sxs-lookup"><span data-stu-id="b0757-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="b0757-111">Регистрация hello Google + учетной записи утверждения поставщика tooa пользователя пути</span><span class="sxs-lookup"><span data-stu-id="b0757-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="b0757-112">Отправка tooan политики hello Azure AD B2C клиента и его проверка</span><span class="sxs-lookup"><span data-stu-id="b0757-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="b0757-113">Создание приложения для учетной записи Google+</span><span class="sxs-lookup"><span data-stu-id="b0757-113">Create a Google+ account application</span></span>
<span data-ttu-id="b0757-114">toouse Google + как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения Google + и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="b0757-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="b0757-115">Приложение Google+ можно зарегистрировать здесь: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="b0757-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="b0757-116">Go toohello [Google Developers Console](https://console.developers.google.com/) и выполните вход с помощью Google + данные своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b0757-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="b0757-117">Щелкните **Create project** (Создать проект), введите значение в поле **Project name** (Имя проекта) и щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="b0757-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="b0757-118">Щелкните hello **меню проекты**.</span><span class="sxs-lookup"><span data-stu-id="b0757-118">Click on hello **Projects menu**.</span></span>

    ![Учетная запись Google+, меню "Выберите проект"](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="b0757-120">Щелкните hello  **+**  кнопки.</span><span class="sxs-lookup"><span data-stu-id="b0757-120">Click on hello **+** button.</span></span>

    ![Учетная запись Google+, создание проекта](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="b0757-122">Введите **имя проекта** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b0757-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Учетная запись Google+, новый проект](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="b0757-124">Подождите, пока проект hello готов и щелкнуть hello **меню проекты**.</span><span class="sxs-lookup"><span data-stu-id="b0757-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Подождите, пока новый проект будет готов toouse Google + учетная запись —](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="b0757-126">Щелкните имя проекта.</span><span class="sxs-lookup"><span data-stu-id="b0757-126">Click on your project name.</span></span>

    ![Google + учетная запись — нового проекта выберите hello](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="b0757-128">Нажмите кнопку **API диспетчера** и нажмите кнопку **учетные данные** в hello навигации слева.</span><span class="sxs-lookup"><span data-stu-id="b0757-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="b0757-129">Нажмите кнопку hello **экран согласия OAuth** вкладку вверху hello.</span><span class="sxs-lookup"><span data-stu-id="b0757-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Учетная запись Google+, настройка окна запроса доступа OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="b0757-131">Выберите или укажите допустимый **электронный адрес**, заполните поле **Product name** (Название продукта) и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="b0757-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+, учетные данные приложения](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="b0757-133">Щелкните **New credentials** (Создать учетные данные) и выберите **OAuth client ID** (Идентификатор клиента OAuth).</span><span class="sxs-lookup"><span data-stu-id="b0757-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+, создание учетных данных приложения](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="b0757-135">Из списка **Application type** (Тип приложения) выберите **Web application** (Веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="b0757-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+, выбор типа приложения](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="b0757-137">Укажите **имя** приложения, введите `https://login.microsoftonline.com` в hello **право JavaScript origins** поля, и `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **авторизованные URIперенаправления**поля.</span><span class="sxs-lookup"><span data-stu-id="b0757-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="b0757-138">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="b0757-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="b0757-139">Hello **{tenant}** значение учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="b0757-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="b0757-140">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b0757-140">Click **Create**.</span></span>

    ![Google+, предоставление авторизованных источников JavaScript и URI перенаправления](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="b0757-142">Скопируйте значения hello **идентификатор клиента** и **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="b0757-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="b0757-143">Требуется обоих tooconfigure Google + как поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="b0757-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="b0757-144">**Секрет клиента** — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="b0757-144">**Client secret** is an important security credential.</span></span>

    ![Google + - копирования значения hello клиента идентификатор и секрет клиента](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="b0757-146">Добавить hello Google + учетная запись приложения ключа tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="b0757-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="b0757-147">С помощью учетных записей Google + отношению федерации требуется секрет клиента tootrust учетной записи Google + Azure AD B2C имени приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b0757-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="b0757-148">Необходимые toostore секрет приложения Google + в клиенте Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b0757-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="b0757-149">Клиент Azure AD B2C tooyour перейдите и выберите **B2C параметры** > **Identity Framework качества**</span><span class="sxs-lookup"><span data-stu-id="b0757-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="b0757-150">Выберите **ключей политики** ключей tooview hello, доступных в клиенте.</span><span class="sxs-lookup"><span data-stu-id="b0757-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="b0757-151">Щелкните **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b0757-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="b0757-152">В пункте **Параметры** используйте вариант **Вручную**.</span><span class="sxs-lookup"><span data-stu-id="b0757-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="b0757-153">Для параметра **Имя** используйте значение `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="b0757-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="b0757-154">префикс Hello `B2C_1A_` могут быть добавлены автоматически.</span><span class="sxs-lookup"><span data-stu-id="b0757-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="b0757-155">В hello **секрет** введите ваш секрет приложения Майкрософт от https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="b0757-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="b0757-156">Для параметра **Использование ключа** задайте значение **Подпись**.</span><span class="sxs-lookup"><span data-stu-id="b0757-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="b0757-157">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="b0757-157">Click **Create**</span></span>
9.  <span data-ttu-id="b0757-158">Убедитесь, что вы создали ключ hello `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="b0757-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="b0757-159">Добавление поставщика утверждений в политику расширения</span><span class="sxs-lookup"><span data-stu-id="b0757-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="b0757-160">Если требуется с помощью учетной записи Google + toosign пользователей в качестве поставщика утверждений требуется toodefine Google + учетная запись.</span><span class="sxs-lookup"><span data-stu-id="b0757-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="b0757-161">Другими словами необходимо toospecify, Azure AD B2C взаимодействует с конечной точки.</span><span class="sxs-lookup"><span data-stu-id="b0757-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="b0757-162">Конечная точка Hello предоставляет набор утверждений, которые используются в Azure AD B2C tooverify проверку определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b0757-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="b0757-163">Определите учетную запись Google+ в качестве поставщика утверждений, добавив узел `<ClaimsProvider>` в файл расширения политики:</span><span class="sxs-lookup"><span data-stu-id="b0757-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="b0757-164">Откройте файл политики для расширения hello (TrustFrameworkExtensions.xml) из рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="b0757-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="b0757-165">Если вам нужен редактор XML, [попробуйте Visual Studio Code](https://code.visualstudio.com/download) — упрощенный кроссплатформенный редактор.</span><span class="sxs-lookup"><span data-stu-id="b0757-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="b0757-166">Найти hello `<ClaimsProviders>` раздела</span><span class="sxs-lookup"><span data-stu-id="b0757-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="b0757-167">Добавьте следующий фрагмент XML в hello hello `ClaimsProviders` и замените `client_id` значение с Google + учетная запись приложения ИД клиента перед сохранением файла hello.</span><span class="sxs-lookup"><span data-stu-id="b0757-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

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
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="b0757-168">Регистрация hello Google + учетной записи утверждения поставщика tooSign вверх или вход в пути пользователя</span><span class="sxs-lookup"><span data-stu-id="b0757-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="b0757-169">Поставщик удостоверений Hello настроена.</span><span class="sxs-lookup"><span data-stu-id="b0757-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="b0757-170">Тем не менее не доступен в любом hello регистрации-повышение/вход экранов.</span><span class="sxs-lookup"><span data-stu-id="b0757-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="b0757-171">Добавить hello Google + пользователя учетной записи удостоверения поставщика tooyour `SignUpOrSignIn` пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="b0757-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="b0757-172">toomake его доступным, мы создаем копию существующего шаблона пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="b0757-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="b0757-173">Затем мы добавьте поставщик удостоверений, hello Google + учетной записи:</span><span class="sxs-lookup"><span data-stu-id="b0757-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="b0757-174">Если вы скопировали hello `<UserJourneys>` элемент из основного файла политики toohello расширение файла (TrustFrameworkExtensions.xml) toothis раздел можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="b0757-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="b0757-175">Откройте файл базовый hello политики (например, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="b0757-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="b0757-176">Найти hello `<UserJourneys>` элемент и скопируйте hello всему содержимому `<UserJourneys>` узла.</span><span class="sxs-lookup"><span data-stu-id="b0757-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="b0757-177">Откройте файл hello расширения (например, TrustFrameworkExtensions.xml) и найти hello `<UserJourneys>` элемента.</span><span class="sxs-lookup"><span data-stu-id="b0757-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="b0757-178">Если элемент hello не существует, добавьте его.</span><span class="sxs-lookup"><span data-stu-id="b0757-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="b0757-179">Вставьте hello всему содержимому `<UserJournesy>` узел, который вы скопировали как дочерний hello `<UserJourneys>` элемента.</span><span class="sxs-lookup"><span data-stu-id="b0757-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="b0757-180">Отображение кнопки hello</span><span class="sxs-lookup"><span data-stu-id="b0757-180">Display hello button</span></span>
<span data-ttu-id="b0757-181">Hello `<ClaimsProviderSelections>` элемент определяет список hello параметры выбора поставщика утверждений и их порядок.</span><span class="sxs-lookup"><span data-stu-id="b0757-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="b0757-182">`<ClaimsProviderSelection>`элемент является аналогом tooan кнопку поставщика удостоверений на странице регистрации-повышение/вход.</span><span class="sxs-lookup"><span data-stu-id="b0757-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="b0757-183">При добавлении `<ClaimsProviderSelection>` элемент для учетной записи Google + новая кнопка отображается, когда пользователь попадает на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="b0757-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="b0757-184">tooadd этого элемента:</span><span class="sxs-lookup"><span data-stu-id="b0757-184">tooadd this element:</span></span>

1.  <span data-ttu-id="b0757-185">Найти hello `<UserJourney>` узел, который содержит `Id="SignUpOrSignIn"` в пути пользователя hello, скопированный.</span><span class="sxs-lookup"><span data-stu-id="b0757-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="b0757-186">Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="b0757-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="b0757-187">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="b0757-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="b0757-188">Действие tooan кнопки ссылки hello</span><span class="sxs-lookup"><span data-stu-id="b0757-188">Link hello button tooan action</span></span>
<span data-ttu-id="b0757-189">Теперь, когда имеется кнопка на месте, необходимо toolink его tooan действие.</span><span class="sxs-lookup"><span data-stu-id="b0757-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="b0757-190">Действие Hello в этом случае является для Azure AD B2C toocommunicate с tooreceive учетной записи Google + маркер.</span><span class="sxs-lookup"><span data-stu-id="b0757-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="b0757-191">Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.</span><span class="sxs-lookup"><span data-stu-id="b0757-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="b0757-192">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="b0757-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="b0757-193">Убедитесь, hello `Id` имеет одинаковое значение, что и hello `TargetClaimsExchangeId` в предшествующих раздел hello</span><span class="sxs-lookup"><span data-stu-id="b0757-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="b0757-194">Убедитесь, `TechnicalProfileReferenceId` идентификатор задан toohello технические профиль, созданный ранее (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="b0757-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="b0757-195">Отправка hello политики tooyour клиента</span><span class="sxs-lookup"><span data-stu-id="b0757-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="b0757-196">В hello [портал Azure](https://portal.azure.com), для переключения в hello [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)и откройте hello **Azure AD B2C** колонку.</span><span class="sxs-lookup"><span data-stu-id="b0757-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="b0757-197">Выберите **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="b0757-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="b0757-198">Откройте hello **все политики** колонку.</span><span class="sxs-lookup"><span data-stu-id="b0757-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="b0757-199">Щелкните **Отправить политику**.</span><span class="sxs-lookup"><span data-stu-id="b0757-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="b0757-200">Проверьте **перезаписать hello политики, если он существует** поле.</span><span class="sxs-lookup"><span data-stu-id="b0757-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="b0757-201">**Отправка** TrustFrameworkExtensions.xml и убедитесь, что он не позволяет проверки hello</span><span class="sxs-lookup"><span data-stu-id="b0757-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="b0757-202">Тестирование настраиваемой политики hello с использованием выполнить</span><span class="sxs-lookup"><span data-stu-id="b0757-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="b0757-203">Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.</span><span class="sxs-lookup"><span data-stu-id="b0757-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="b0757-204">**Теперь запустите** требует по крайней мере одно приложение toobe предварительно зарегистрирован на приветствия клиента.</span><span class="sxs-lookup"><span data-stu-id="b0757-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="b0757-205">toolearn приложений tooregister. в статье hello Azure AD B2C [приступить к работе](active-directory-b2c-get-started.md) статьи или hello [регистрацию приложения](active-directory-b2c-app-registration.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="b0757-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="b0757-206">Откройте **B2C_1A_signup_signin**, hello проверяющей стороны (RP) настраиваемой политики загруженный.</span><span class="sxs-lookup"><span data-stu-id="b0757-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="b0757-207">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="b0757-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="b0757-208">Необходимо будет toosign Google + учетной записью.</span><span class="sxs-lookup"><span data-stu-id="b0757-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="b0757-209">[Необязательно] Регистрация hello Google + учетной записи утверждения поставщика tooProfile изменить пользователя пути</span><span class="sxs-lookup"><span data-stu-id="b0757-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="b0757-210">Вы можете tooadd hello Google + учетной записи поставщика удостоверений также пользователя tooyour `ProfileEdit` пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="b0757-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="b0757-211">toomake доступно, мы повторяем hello последние два этапа:</span><span class="sxs-lookup"><span data-stu-id="b0757-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="b0757-212">Отображение кнопки hello</span><span class="sxs-lookup"><span data-stu-id="b0757-212">Display hello button</span></span>
1.  <span data-ttu-id="b0757-213">Откройте файл hello расширения политики (например, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="b0757-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="b0757-214">Найти hello `<UserJourney>` узел, который содержит `Id="ProfileEdit"` в пути пользователя hello, скопированный.</span><span class="sxs-lookup"><span data-stu-id="b0757-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="b0757-215">Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="b0757-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="b0757-216">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="b0757-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="b0757-217">Действие tooan кнопки ссылки hello</span><span class="sxs-lookup"><span data-stu-id="b0757-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="b0757-218">Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.</span><span class="sxs-lookup"><span data-stu-id="b0757-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="b0757-219">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="b0757-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="b0757-220">Тестирование настраиваемой политики профиля Редактирование hello с использованием выполнить</span><span class="sxs-lookup"><span data-stu-id="b0757-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="b0757-221">Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.</span><span class="sxs-lookup"><span data-stu-id="b0757-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="b0757-222">Откройте **B2C_1A_ProfileEdit**, hello проверяющей стороны (RP) настраиваемой политики загруженный.</span><span class="sxs-lookup"><span data-stu-id="b0757-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="b0757-223">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="b0757-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="b0757-224">Необходимо будет toosign Google + учетной записью.</span><span class="sxs-lookup"><span data-stu-id="b0757-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="b0757-225">Загрузка файлов политики завершения hello</span><span class="sxs-lookup"><span data-stu-id="b0757-225">Download hello complete policy files</span></span>
<span data-ttu-id="b0757-226">Необязательно: Мы рекомендуем Построение сценария используется файлы политики настраиваемый после завершения работы Приступая к работе с пользовательских политик перемещайтесь вместо использования этих файлов образца hello.</span><span class="sxs-lookup"><span data-stu-id="b0757-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="b0757-227">Примеры файлов политики для справки</span><span class="sxs-lookup"><span data-stu-id="b0757-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
