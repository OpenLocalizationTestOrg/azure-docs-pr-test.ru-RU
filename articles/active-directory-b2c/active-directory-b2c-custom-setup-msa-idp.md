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
ms.openlocfilehash: 8c981046ff41d3927ff60d6dc4f40366ae25ba74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="0fa0f-103">Azure Active Directory B2C. Добавление учетной записи Майкрософт (MSA) в качестве поставщика удостоверений с помощью пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="0fa0f-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="0fa0f-104">В этой статье описывается, как включить возможность входа для пользователей из учетной записи Майкрософт (MSA) с помощью [пользовательских политик](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0fa0f-104">This article shows you how to enable sign-in for users from Microsoft account (MSA) through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fa0f-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0fa0f-105">Prerequisites</span></span>
<span data-ttu-id="0fa0f-106">Выполните шаги, описанные в статье [Azure Active Directory B2C. Приступая к работе с настраиваемыми политиками](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0fa0f-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="0fa0f-107">А именно:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-107">These steps include:</span></span>

1.  <span data-ttu-id="0fa0f-108">Создание приложения для учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="0fa0f-109">Добавление ключа учетной записи Microsoft в Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-109">Adding the Microsoft account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="0fa0f-110">Добавление поставщика утверждений в политику.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="0fa0f-111">Регистрация поставщика утверждений учетной записи Microsoft для пути взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-111">Registering the Microsoft Account claims provider to a user journey</span></span>
5.  <span data-ttu-id="0fa0f-112">Отправка политики в клиент Azure AD B2C и ее проверка.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="0fa0f-113">Создание приложения для учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="0fa0f-113">Create a Microsoft account application</span></span>
<span data-ttu-id="0fa0f-114">Чтобы использовать учетную запись Майкрософт в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать приложение для учетной записи Майкрософт и задать в нем правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-114">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="0fa0f-115">Вам потребуется учетная запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-115">You need a Microsoft account.</span></span> <span data-ttu-id="0fa0f-116">Если у вас нет учетной записи, создайте ее на сайте [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="0fa0f-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="0fa0f-117">Перейдите в [Центр регистрации приложений Майкрософт](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) и войдите с помощью своей учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-117">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="0fa0f-118">Нажмите кнопку **Добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-118">Click **Add an app**.</span></span>

    ![Учетная запись Майкрософт, добавление приложения](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="0fa0f-120">Укажите **имя** вашего приложения, **адрес электронной почты**, снимите флажок **Мы поможем вам начать работу** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Учетная запись Майкрософт, регистрация приложения](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="0fa0f-122">Скопируйте значение **Идентификатор приложения**. Он необходим для настройки учетной записи Майкрософт в качестве поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-122">Copy the value of **Application Id**. You need it to configure Microsoft account as an identity provider in your tenant.</span></span>

    ![Учетная запись Майкрософт, копирование значения идентификатора приложения](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="0fa0f-124">Щелкните **Добавление платформы**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-124">Click on **Add platform**</span></span>

    ![Учетная запись Майкрософт: добавление платформы](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="0fa0f-126">В списке платформ выберите **Интернет**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-126">From the platform list, choose **Web**.</span></span>

    ![Учетная запись Майкрософт, выбор "Интернет" из списка платформ](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="0fa0f-128">Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в поле **URI перенаправления** .</span><span class="sxs-lookup"><span data-stu-id="0fa0f-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="0fa0f-129">Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="0fa0f-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Учетная запись Майкрософт, установка URL-адресов перенаправления](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="0fa0f-131">Щелкните **Создать новый пароль** в разделе **Секреты приложения**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-131">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="0fa0f-132">Скопируйте новый пароль с экрана.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-132">Copy the new password displayed on screen.</span></span> <span data-ttu-id="0fa0f-133">Он необходим для настройки учетной записи Майкрософт в качестве поставщика удостоверений в вашем клиенте.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-133">You need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="0fa0f-134">Данный пароль — важный элемент обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-134">This password is an important security credential.</span></span>

    ![Microsoft учетной записи: создание нового пароля](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Учетная запись Майкрософт, копирование нового пароля](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="0fa0f-137">Установите флажок **Поддержка Live SDK** в разделе **Дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-137">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="0fa0f-138">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-138">Click **Save**.</span></span>

    ![Учетная запись Майкрософт: поддержка Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-the-microsoft-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="0fa0f-140">Добавление ключа приложения учетной записи Майкрософт в Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="0fa0f-140">Add the Microsoft account application key to Azure AD B2C</span></span>
<span data-ttu-id="0fa0f-141">Федерации с учетными записями Майкрософт нужен секрет клиента, чтобы учетная запись Майкрософт смогла установить отношения доверия с Azure AD B2C от имени приложения.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-141">Federation with Microsoft accounts requires a client secret for Microsoft account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="0fa0f-142">Вам необходимо сохранить свой секрет Майкрософт в клиенте Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-142">You need to store your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="0fa0f-143">Перейдите к клиенту Azure AD B2C и выберите **B2C Settings** (Параметры B2C)  > **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-143">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="0fa0f-144">Выберите **Policy Keys** (Ключи политики), чтобы просмотреть доступные в клиенте ключи.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-144">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="0fa0f-145">Щелкните **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="0fa0f-146">В пункте **Параметры** используйте вариант **Вручную**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="0fa0f-147">Для параметра **Имя** используйте значение `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="0fa0f-148">Префикс `B2C_1A_` может быть добавлен автоматически.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-148">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="0fa0f-149">В поле **Секрет** введите свой секрет приложения Майкрософт с сайта https://apps.dev.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-149">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="0fa0f-150">Для параметра **Использование ключа** задайте значение **Подпись**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="0fa0f-151">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="0fa0f-151">Click **Create**</span></span>
9.  <span data-ttu-id="0fa0f-152">Убедитесь, что вы создали ключ `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-152">Confirm that you've created the key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="0fa0f-153">Добавление поставщика утверждений в политику расширения</span><span class="sxs-lookup"><span data-stu-id="0fa0f-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="0fa0f-154">Чтобы пользователи выполняли вход с помощью учетной записи Майкрософт, необходимо определить ее в качестве поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-154">If you want users to sign in by using Microsoft Account, you need to define Microsoft Account as a claims provider.</span></span> <span data-ttu-id="0fa0f-155">Другими словами, необходимо указать конечную точку, с которой взаимодействует Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-155">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="0fa0f-156">Конечная точка предоставляет набор утверждений, используемых Azure AD B2C, чтобы проверить, была ли выполнена проверка подлинности определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-156">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="0fa0f-157">Определите учетную запись Майкрософт в качестве поставщика утверждений, добавив узел `<ClaimsProvider>` в файл расширения политики:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="0fa0f-158">Откройте файл политики расширения (TrustFrameworkExtensions.xml) из рабочего каталога.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-158">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="0fa0f-159">Если вам нужен редактор XML, [попробуйте Visual Studio Code](https://code.visualstudio.com/download) — упрощенный кроссплатформенный редактор.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="0fa0f-160">Найдите раздел `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-160">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="0fa0f-161">Добавьте в элемент `ClaimsProviders` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-161">Add following XML snippet under the `ClaimsProviders` element:</span></span>

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

4.  <span data-ttu-id="0fa0f-162">Замените значение `client_id` на идентификатор клиента приложения учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="0fa0f-163">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-163">Save the file.</span></span>

## <a name="register-the-microsoft-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="0fa0f-164">Регистрация поставщика утверждений учетной записи Майкрософт для пути взаимодействия пользователя "Регистрация" или "Вход"</span><span class="sxs-lookup"><span data-stu-id="0fa0f-164">Register the Microsoft Account claims provider to Sign up or Sign-in user journey</span></span>

<span data-ttu-id="0fa0f-165">На этом этапе поставщик удостоверений уже настроен, но еще не доступен ни на одном экране регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-165">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="0fa0f-166">Теперь необходимо добавить поставщик удостоверений учетной записи Майкрософт для пути взаимодействия пользователя `SignUpOrSignIn`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-166">Now you need to add the Microsoft Account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="0fa0f-167">Чтобы сделать его доступным, необходимо создать дубликат имеющегося шаблона пути взаимодействия пользователя,</span><span class="sxs-lookup"><span data-stu-id="0fa0f-167">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="0fa0f-168">а затем добавить поставщик удостоверений учетной записи Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-168">Then we add the Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="0fa0f-169">Если вы уже скопировали элемент `<UserJourneys>` из основного файла политики в файл расширения`TrustFrameworkExtensions.xml`, можно пропустить этот раздел.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-169">If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file `TrustFrameworkExtensions.xml`, you can skip to this section.</span></span>

1.  <span data-ttu-id="0fa0f-170">Откройте базовый файл политики (например, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="0fa0f-170">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="0fa0f-171">Найдите элемент `<UserJourneys>` и скопируйте все содержимое узла `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-171">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="0fa0f-172">Откройте файл расширения (например, TrustFrameworkExtensions.xml) и найдите элемент `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-172">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="0fa0f-173">Если элемент не существует, добавьте его.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-173">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="0fa0f-174">Вставьте весь скопированный узел `<UserJournesy>` как дочерний узел элемента `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-174">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="0fa0f-175">Отображение кнопки</span><span class="sxs-lookup"><span data-stu-id="0fa0f-175">Display the button</span></span>
<span data-ttu-id="0fa0f-176">Элемент `<ClaimsProviderSelections>` определяет список параметров выбора поставщика утверждений и их порядок.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-176">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="0fa0f-177">Элемент `<ClaimsProviderSelection>` является аналогом кнопки поставщика удостоверений на странице регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-177">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="0fa0f-178">Если вы добавите для учетной записи Майкрософт элемент `<ClaimsProviderSelection>`, при переходе пользователя на страницу отобразится новая кнопка.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="0fa0f-179">Для этого:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-179">To add this element:</span></span>

1.  <span data-ttu-id="0fa0f-180">Найдите узел `<UserJourney>`, содержащий `Id="SignUpOrSignIn"` в скопированном пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-180">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="0fa0f-181">Найдите узел `<OrchestrationStep>`, содержащий `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-181">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="0fa0f-182">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="0fa0f-183">Связывание кнопки с действием</span><span class="sxs-lookup"><span data-stu-id="0fa0f-183">Link the button to an action</span></span>
<span data-ttu-id="0fa0f-184">Теперь, когда у вас есть кнопка, вам необходимо связать ее с действием.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-184">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="0fa0f-185">В этом случае действие — это возможность взаимодействия Azure AD B2C с учетной записью Майкрософт для получения токена.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-185">The action, in this case, is for Azure AD B2C to communicate with Microsoft Account to receive a token.</span></span> <span data-ttu-id="0fa0f-186">Свяжите кнопку с действием, связав технический профиль для поставщика утверждений учетной записи Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-186">Link the button to an action by linking the technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="0fa0f-187">Найдите `<OrchestrationStep>`, который содержит `Order="2"` в узле `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-187">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="0fa0f-188">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="0fa0f-189">Убедитесь, что `Id` имеет то же значение, что и `TargetClaimsExchangeId` в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-189">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
>   * <span data-ttu-id="0fa0f-190">Убедитесь, что для идентификатора `TechnicalProfileReferenceId` задано значение ранее созданного технического профиля (MSA-OIDC).</span><span class="sxs-lookup"><span data-stu-id="0fa0f-190">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="0fa0f-191">Отправка политики в клиент</span><span class="sxs-lookup"><span data-stu-id="0fa0f-191">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="0fa0f-192">На [портале Azure](https://portal.azure.com) переключитесь в [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) и откройте колонку **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-192">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="0fa0f-193">Выберите **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="0fa0f-194">Откройте колонку **Все политики**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-194">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="0fa0f-195">Щелкните **Отправить политику**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="0fa0f-196">Установите флажок **Перезаписать политику, если она существует**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-196">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="0fa0f-197">**Отправьте** файл TrustFrameworkExtensions.xml и немного подождите, чтобы удостовериться в отсутствии сбоя при проверке.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="0fa0f-198">Тестирование настраиваемой политики с помощью команды "Запустить сейчас"</span><span class="sxs-lookup"><span data-stu-id="0fa0f-198">Test the custom policy by using Run Now</span></span>

1.  <span data-ttu-id="0fa0f-199">Откройте **Параметры Azure AD B2C** и перейдите к элементу **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-199">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="0fa0f-200">Для использования команды **Запустить сейчас** необходимо, чтобы в клиенте было предварительно зарегистрировано хотя бы одно приложение.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-200">**Run now** requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="0fa0f-201">Дополнительные сведения о регистрации приложений см. в статье [Azure AD B2C: начало работы](active-directory-b2c-get-started.md) или [Регистрация приложения](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="0fa0f-201">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="0fa0f-202">Откройте **B2C_1A_signup_signin**, отправленную вами пользовательскую политику проверяющей стороны.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-202">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="0fa0f-203">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="0fa0f-204">У вас должна появиться возможность входа с использованием учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-204">You should be able to sign in using Microsoft account.</span></span>

## <a name="optional-register-the-microsoft-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="0fa0f-205">[Необязательно] Регистрация поставщика утверждений учетной записи Майкрософт для пути взаимодействия пользователя "Изменение профиля"</span><span class="sxs-lookup"><span data-stu-id="0fa0f-205">[Optional] Register the Microsoft Account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="0fa0f-206">Вы также можете добавить поставщик удостоверений учетной записи Майкрософт для пути взаимодействия пользователя `ProfileEdit`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-206">You may want to add the Microsoft Account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="0fa0f-207">Чтобы сделать его доступным, необходимо повторить последние два шага:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-207">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="0fa0f-208">Отображение кнопки</span><span class="sxs-lookup"><span data-stu-id="0fa0f-208">Display the button</span></span>
1.  <span data-ttu-id="0fa0f-209">Откройте файл расширения политики (например, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="0fa0f-209">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="0fa0f-210">Найдите узел `<UserJourney>`, содержащий `Id="ProfileEdit"` в скопированном пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-210">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="0fa0f-211">Найдите узел `<OrchestrationStep>`, содержащий `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-211">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="0fa0f-212">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="0fa0f-213">Связывание кнопки с действием</span><span class="sxs-lookup"><span data-stu-id="0fa0f-213">Link the button to an action</span></span>
1.  <span data-ttu-id="0fa0f-214">Найдите `<OrchestrationStep>`, который содержит `Order="2"` в узле `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-214">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="0fa0f-215">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="0fa0f-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="0fa0f-216">Тестирование пользовательской политики изменения профиля с помощью команды "Запустить сейчас"</span><span class="sxs-lookup"><span data-stu-id="0fa0f-216">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="0fa0f-217">Откройте **Параметры Azure AD B2C** и перейдите к элементу **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-217">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="0fa0f-218">Откройте **B2C_1A_ProfileEdit**, отправленную пользовательскую политику проверяющей стороны.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-218">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="0fa0f-219">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="0fa0f-220">У вас должна появиться возможность входа с использованием учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-220">You should be able to sign in using Microsoft account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="0fa0f-221">Загрузка завершенных файлов политики</span><span class="sxs-lookup"><span data-stu-id="0fa0f-221">Download the complete policy files</span></span>
<span data-ttu-id="0fa0f-222">Необязательно. Мы советуем создать свой сценарий, используя собственные файлы пользовательской политики, а не эти примеры файлов, после того, как вы ознакомитесь с пошаговым руководством по началу работы с пользовательскими политиками.</span><span class="sxs-lookup"><span data-stu-id="0fa0f-222">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="0fa0f-223">Примеры файлов политики для справки</span><span class="sxs-lookup"><span data-stu-id="0fa0f-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
