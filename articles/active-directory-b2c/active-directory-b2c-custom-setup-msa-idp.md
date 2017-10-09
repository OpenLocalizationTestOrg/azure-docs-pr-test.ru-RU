---
title: "Azure Active Directory B2C. Добавление учетной записи Майкрософт (MSA) в качестве поставщика удостоверений с помощью пользовательских политик"
description: "Пример использования Майкрософт в качестве поставщика удостоверений с помощью протокола OpenID Connect (OIDC)"
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="60767-103">Azure Active Directory B2C. Добавление учетной записи Майкрософт (MSA) в качестве поставщика удостоверений с помощью пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="60767-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="60767-104">В этой статье показано, как tooenable вход для пользователей из учетной записи Майкрософт (MSA) с использованием hello [настраиваемые политики](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="60767-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60767-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="60767-105">Prerequisites</span></span>
<span data-ttu-id="60767-106">Hello завершения шагов в hello [Приступая к работе с помощью настроенных политик](active-directory-b2c-get-started-custom.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="60767-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="60767-107">А именно:</span><span class="sxs-lookup"><span data-stu-id="60767-107">These steps include:</span></span>

1.  <span data-ttu-id="60767-108">Создание приложения для учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60767-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="60767-109">Добавление hello Microsoft учетной записи приложения ключа tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="60767-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="60767-110">Добавление политики tooa поставщика утверждений</span><span class="sxs-lookup"><span data-stu-id="60767-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="60767-111">Регистрация пользователя hello учетной записи Майкрософт утверждений поставщика tooa пути</span><span class="sxs-lookup"><span data-stu-id="60767-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="60767-112">Отправка tooan политики hello Azure AD B2C клиента и его проверка</span><span class="sxs-lookup"><span data-stu-id="60767-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="60767-113">Создание приложения для учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="60767-113">Create a Microsoft account application</span></span>
<span data-ttu-id="60767-114">Учетная запись Майкрософт toouse как поставщик удостоверений в Azure Active Directory (Azure AD) B2C, требуется toocreate приложение учетной записи Microsoft и передайте в него hello нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="60767-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="60767-115">Вам потребуется учетная запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60767-115">You need a Microsoft account.</span></span> <span data-ttu-id="60767-116">Если у вас нет учетной записи, создайте ее на сайте [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="60767-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="60767-117">Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) и выполните вход с помощью учетных данных вашей учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60767-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="60767-118">Нажмите кнопку **Добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="60767-118">Click **Add an app**.</span></span>

    ![Учетная запись Майкрософт, добавление приложения](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="60767-120">Укажите **имя** вашего приложения, **адрес электронной почты**, снимите флажок **Мы поможем вам начать работу** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="60767-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Учетная запись Майкрософт, регистрация приложения](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="60767-122">Скопируйте значение hello **идентификатор приложения**. Необходимо tooconfigure учетную запись Майкрософт как поставщик удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="60767-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Учетная запись Майкрософт — скопировать hello значение идентификатора приложения](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="60767-124">Щелкните **Добавление платформы**.</span><span class="sxs-lookup"><span data-stu-id="60767-124">Click on **Add platform**</span></span>

    ![Учетная запись Майкрософт: добавление платформы](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="60767-126">Hello списке платформ выберите **Web**.</span><span class="sxs-lookup"><span data-stu-id="60767-126">From hello platform list, choose **Web**.</span></span>

    ![Учетная запись Майкрософт — hello платформы списке выберите Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="60767-128">Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **URI перенаправления** поля.</span><span class="sxs-lookup"><span data-stu-id="60767-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="60767-129">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="60767-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Учетная запись Майкрософт, установка URL-адресов перенаправления](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="60767-131">Щелкните **создать новый пароль** под hello **секреты приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="60767-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="60767-132">Скопируйте новый пароль hello отображается на экране.</span><span class="sxs-lookup"><span data-stu-id="60767-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="60767-133">Необходимо tooconfigure учетную запись Майкрософт как поставщик удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="60767-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="60767-134">Данный пароль — важный элемент обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="60767-134">This password is an important security credential.</span></span>

    ![Microsoft учетной записи: создание нового пароля](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Учетная запись Майкрософт — Копировать hello новый пароль](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="60767-137">Hello флажок **поддержки пакета SDK Live** под hello **Дополнительно** раздела.</span><span class="sxs-lookup"><span data-stu-id="60767-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="60767-138">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="60767-138">Click **Save**.</span></span>

    ![Учетная запись Майкрософт: поддержка Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="60767-140">Добавить hello Microsoft учетной записи приложения ключа tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="60767-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="60767-141">Федерации с учетными записями Microsoft требуется секрет клиента tootrust учетной записи Microsoft Azure AD B2C имени приложения hello.</span><span class="sxs-lookup"><span data-stu-id="60767-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="60767-142">Необходимые toostore вашей учетной записи для Microsoft приложения secert в клиенте Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="60767-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="60767-143">Клиент Azure AD B2C tooyour перейдите и выберите **B2C параметры** > **Identity Framework качества**</span><span class="sxs-lookup"><span data-stu-id="60767-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="60767-144">Выберите **ключей политики** ключей tooview hello, доступных в клиенте.</span><span class="sxs-lookup"><span data-stu-id="60767-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="60767-145">Щелкните **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="60767-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="60767-146">В пункте **Параметры** используйте вариант **Вручную**.</span><span class="sxs-lookup"><span data-stu-id="60767-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="60767-147">Для параметра **Имя** используйте значение `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="60767-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="60767-148">префикс Hello `B2C_1A_` могут быть добавлены автоматически.</span><span class="sxs-lookup"><span data-stu-id="60767-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="60767-149">В hello **секрет** введите ваш секрет приложения Майкрософт от https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="60767-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="60767-150">Для параметра **Использование ключа** задайте значение **Подпись**.</span><span class="sxs-lookup"><span data-stu-id="60767-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="60767-151">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="60767-151">Click **Create**</span></span>
9.  <span data-ttu-id="60767-152">Убедитесь, что вы создали ключ hello `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="60767-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="60767-153">Добавление поставщика утверждений в политику расширения</span><span class="sxs-lookup"><span data-stu-id="60767-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="60767-154">Если требуется toosign пользователей в с помощью учетной записи Майкрософт, как поставщик утверждений необходимо toodefine учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60767-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="60767-155">Другими словами необходимо toospecify, Azure AD B2C взаимодействует с конечной точки.</span><span class="sxs-lookup"><span data-stu-id="60767-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="60767-156">Конечная точка Hello предоставляет набор утверждений, которые используются в Azure AD B2C tooverify проверку определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="60767-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="60767-157">Определите учетную запись Майкрософт в качестве поставщика утверждений, добавив узел `<ClaimsProvider>` в файл расширения политики:</span><span class="sxs-lookup"><span data-stu-id="60767-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="60767-158">Откройте файл политики для расширения hello (TrustFrameworkExtensions.xml) из рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="60767-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="60767-159">Если вам нужен редактор XML, [попробуйте Visual Studio Code](https://code.visualstudio.com/download) — упрощенный кроссплатформенный редактор.</span><span class="sxs-lookup"><span data-stu-id="60767-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="60767-160">Найти hello `<ClaimsProviders>` раздела</span><span class="sxs-lookup"><span data-stu-id="60767-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="60767-161">Добавьте следующий фрагмент XML в hello `ClaimsProviders` элемента:</span><span class="sxs-lookup"><span data-stu-id="60767-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  <span data-ttu-id="60767-162">Замените значение `client_id` на идентификатор клиента приложения учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60767-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="60767-163">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="60767-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="60767-164">Зарегистрировать tooSign поставщика утверждений учетной записи Майкрософт hello вверх или входа в пути пользователя</span><span class="sxs-lookup"><span data-stu-id="60767-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="60767-165">На этом этапе Настройка поставщика удостоверений hello, но он не доступен в любом hello регистрации-повышение/вход экранов.</span><span class="sxs-lookup"><span data-stu-id="60767-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="60767-166">Теперь необходимо tooyour пользователя поставщика удостоверений tooadd hello учетную запись Майкрософт `SignUpOrSignIn` пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="60767-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="60767-167">toomake его доступным, мы создаем копию существующего шаблона пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="60767-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="60767-168">Затем мы добавьте поставщик удостоверений hello учетной записи Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="60767-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="60767-169">Если ранее вы скопировали hello `<UserJourneys>` элемент из основного файла из файла модуля политики toohello `TrustFrameworkExtensions.xml`, toothis раздел можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="60767-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="60767-170">Откройте файл базовый hello политики (например, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="60767-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="60767-171">Найти hello `<UserJourneys>` элемент и скопируйте hello всему содержимому `<UserJourneys>` узла.</span><span class="sxs-lookup"><span data-stu-id="60767-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="60767-172">Откройте файл hello расширения (например, TrustFrameworkExtensions.xml) и найти hello `<UserJourneys>` элемента.</span><span class="sxs-lookup"><span data-stu-id="60767-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="60767-173">Если элемент hello не существует, добавьте его.</span><span class="sxs-lookup"><span data-stu-id="60767-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="60767-174">Вставьте hello всему содержимому `<UserJournesy>` узел, который вы скопировали как дочерний hello `<UserJourneys>` элемента.</span><span class="sxs-lookup"><span data-stu-id="60767-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="60767-175">Отображение кнопки hello</span><span class="sxs-lookup"><span data-stu-id="60767-175">Display hello button</span></span>
<span data-ttu-id="60767-176">Hello `<ClaimsProviderSelections>` элемент определяет список hello параметры выбора поставщика утверждений и их порядок.</span><span class="sxs-lookup"><span data-stu-id="60767-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="60767-177">`<ClaimsProviderSelection>`элемент является аналогом tooan кнопку поставщика удостоверений на странице регистрации-повышение/вход.</span><span class="sxs-lookup"><span data-stu-id="60767-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="60767-178">При добавлении `<ClaimsProviderSelection>` элемент для учетной записи Майкрософт, новая кнопка отображается, когда пользователь попадает на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="60767-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="60767-179">tooadd этого элемента:</span><span class="sxs-lookup"><span data-stu-id="60767-179">tooadd this element:</span></span>

1.  <span data-ttu-id="60767-180">Найти hello `<UserJourney>` узел, который содержит `Id="SignUpOrSignIn"` в пути пользователя hello, скопированный.</span><span class="sxs-lookup"><span data-stu-id="60767-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="60767-181">Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="60767-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="60767-182">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="60767-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="60767-183">Действие tooan кнопки ссылки hello</span><span class="sxs-lookup"><span data-stu-id="60767-183">Link hello button tooan action</span></span>
<span data-ttu-id="60767-184">Теперь, когда имеется кнопка на месте, необходимо toolink его tooan действие.</span><span class="sxs-lookup"><span data-stu-id="60767-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="60767-185">Действие Hello в этом случае является для Azure AD B2C toocommunicate с учетной записью Майкрософт tooreceive маркер.</span><span class="sxs-lookup"><span data-stu-id="60767-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="60767-186">Свяжите действие tooan кнопки hello, связывания hello технические профиля для поставщика утверждений вашей учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60767-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="60767-187">Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.</span><span class="sxs-lookup"><span data-stu-id="60767-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="60767-188">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="60767-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="60767-189">Убедитесь, hello `Id` имеет одинаковое значение, что и hello `TargetClaimsExchangeId` в предшествующих раздел hello</span><span class="sxs-lookup"><span data-stu-id="60767-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="60767-190">Убедитесь, `TechnicalProfileReferenceId` идентификатор задан toohello технические профиль, созданный ранее (MSA-OIDC).</span><span class="sxs-lookup"><span data-stu-id="60767-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="60767-191">Отправка hello политики tooyour клиента</span><span class="sxs-lookup"><span data-stu-id="60767-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="60767-192">В hello [портал Azure](https://portal.azure.com), для переключения в hello [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)и откройте hello **Azure AD B2C** колонку.</span><span class="sxs-lookup"><span data-stu-id="60767-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="60767-193">Выберите **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="60767-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="60767-194">Откройте hello **все политики** колонку.</span><span class="sxs-lookup"><span data-stu-id="60767-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="60767-195">Щелкните **Отправить политику**.</span><span class="sxs-lookup"><span data-stu-id="60767-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="60767-196">Проверьте **перезаписать hello политики, если он существует** поле.</span><span class="sxs-lookup"><span data-stu-id="60767-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="60767-197">**Отправка** TrustFrameworkExtensions.xml и убедитесь, что он не позволяет проверки hello</span><span class="sxs-lookup"><span data-stu-id="60767-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="60767-198">Тестирование настраиваемой политики hello с использованием выполнить</span><span class="sxs-lookup"><span data-stu-id="60767-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="60767-199">Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.</span><span class="sxs-lookup"><span data-stu-id="60767-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="60767-200">**Теперь запустите** требует по крайней мере одно приложение toobe предварительно зарегистрирован на приветствия клиента.</span><span class="sxs-lookup"><span data-stu-id="60767-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="60767-201">toolearn приложений tooregister. в статье hello Azure AD B2C [приступить к работе](active-directory-b2c-get-started.md) статьи или hello [регистрацию приложения](active-directory-b2c-app-registration.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="60767-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="60767-202">Откройте **B2C_1A_signup_signin**, hello проверяющей стороны (RP) настраиваемой политики загруженный.</span><span class="sxs-lookup"><span data-stu-id="60767-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="60767-203">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="60767-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="60767-204">Необходимо будет toosign учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60767-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="60767-205">[Необязательно] Регистрация пользователя hello учетной записи Майкрософт утверждений поставщика tooProfile изменения пути</span><span class="sxs-lookup"><span data-stu-id="60767-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="60767-206">Вы можете поставщика удостоверений tooadd hello учетную запись Майкрософт также пользователя tooyour `ProfileEdit` пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="60767-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="60767-207">toomake доступно, мы повторяем hello последние два этапа:</span><span class="sxs-lookup"><span data-stu-id="60767-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="60767-208">Отображение кнопки hello</span><span class="sxs-lookup"><span data-stu-id="60767-208">Display hello button</span></span>
1.  <span data-ttu-id="60767-209">Откройте файл hello расширения политики (например, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="60767-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="60767-210">Найти hello `<UserJourney>` узел, который содержит `Id="ProfileEdit"` в пути пользователя hello, скопированный.</span><span class="sxs-lookup"><span data-stu-id="60767-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="60767-211">Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="60767-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="60767-212">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="60767-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="60767-213">Действие tooan кнопки ссылки hello</span><span class="sxs-lookup"><span data-stu-id="60767-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="60767-214">Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.</span><span class="sxs-lookup"><span data-stu-id="60767-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="60767-215">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="60767-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="60767-216">Тестирование настраиваемой политики профиля Редактирование hello с использованием выполнить</span><span class="sxs-lookup"><span data-stu-id="60767-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="60767-217">Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.</span><span class="sxs-lookup"><span data-stu-id="60767-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="60767-218">Откройте **B2C_1A_ProfileEdit**, hello проверяющей стороны (RP) настраиваемой политики загруженный.</span><span class="sxs-lookup"><span data-stu-id="60767-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="60767-219">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="60767-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="60767-220">Необходимо будет toosign учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60767-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="60767-221">Загрузка файлов политики завершения hello</span><span class="sxs-lookup"><span data-stu-id="60767-221">Download hello complete policy files</span></span>
<span data-ttu-id="60767-222">Необязательно: Мы рекомендуем Построение сценария используется файлы политики настраиваемый после завершения работы Приступая к работе с пользовательских политик перемещайтесь вместо использования этих файлов образца hello.</span><span class="sxs-lookup"><span data-stu-id="60767-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="60767-223">Примеры файлов политики для справки</span><span class="sxs-lookup"><span data-stu-id="60767-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
