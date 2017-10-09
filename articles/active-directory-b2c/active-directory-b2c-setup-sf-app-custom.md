---
title: "Azure Active Directory B2C. Добавление поставщика SAML Salesforce с помощью пользовательских политик | Документы Майкрософт"
description: "Дополнительные сведения о том, как toocreate Azure Active Directory B2C пользовательской политики и управлять ими."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="7654c-103">Azure Active Directory B2C. Выполнение входа с помощью учетных записей Salesforce через SAML</span><span class="sxs-lookup"><span data-stu-id="7654c-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7654c-104">В этой статье показано, как toouse [настраиваемые политики](active-directory-b2c-overview-custom.md) tooset копирование вход для пользователей в определенной организации Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7654c-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7654c-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7654c-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="7654c-106">Настройка Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7654c-106">Azure AD B2C setup</span></span>

<span data-ttu-id="7654c-107">Убедитесь, что выполнены все шаги hello, которые показывают, как слишком[приступить к работе с помощью настроенных политик](active-directory-b2c-get-started-custom.md) в Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="7654c-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="7654c-108">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="7654c-108">These include:</span></span>

* <span data-ttu-id="7654c-109">Создание клиента Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7654c-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="7654c-110">Создание приложения Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7654c-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="7654c-111">Регистрация двух приложений подсистемы политик.</span><span class="sxs-lookup"><span data-stu-id="7654c-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="7654c-112">Настройка ключей.</span><span class="sxs-lookup"><span data-stu-id="7654c-112">Set up keys.</span></span>
* <span data-ttu-id="7654c-113">Настройка пакета начального приветствия.</span><span class="sxs-lookup"><span data-stu-id="7654c-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="7654c-114">Настройка Salesforce</span><span class="sxs-lookup"><span data-stu-id="7654c-114">Salesforce setup</span></span>

<span data-ttu-id="7654c-115">В этой статье предполагается, что уже выполнены следующие hello:</span><span class="sxs-lookup"><span data-stu-id="7654c-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="7654c-116">Подписка на учетную запись Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7654c-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="7654c-117">Вы можете зарегистрироваться для получения [бесплатной учетной записи Developer Edition](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="7654c-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="7654c-118">[Настройка собственного домена](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) для организации Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7654c-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="7654c-119">Настройка Salesforce для федерации пользователей</span><span class="sxs-lookup"><span data-stu-id="7654c-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="7654c-120">toohelp Azure AD B2C взаимодействовать с Salesforce, необходимо, чтобы URL-адрес метаданных Salesforce tooget hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="7654c-121">Настройка Salesforce в качестве поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="7654c-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="7654c-122">В этой статье предполагается, что вы используете [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="7654c-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="7654c-123">[Войдите в tooSalesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="7654c-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="7654c-124">На hello влево меню в разделе **параметры**, разверните **удостоверение**и нажмите кнопку **поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="7654c-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="7654c-125">Щелкните **Enable Identity Provider** (Включить поставщик удостоверений).</span><span class="sxs-lookup"><span data-stu-id="7654c-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="7654c-126">В разделе **сертификата выберите hello**выберите hello сертификат, который будет toocommunicate toouse Salesforce с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7654c-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="7654c-127">(Можно использовать сертификат по умолчанию hello.) Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7654c-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="7654c-128">Создание подключенного приложения в Salesforce</span><span class="sxs-lookup"><span data-stu-id="7654c-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="7654c-129">На hello **поставщика удостоверений** страницы, перейдите в слишком**поставщиков услуг**.</span><span class="sxs-lookup"><span data-stu-id="7654c-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="7654c-130">Щелкните **Service Providers are now created via Connected Apps. Click here** (Поставщики услуг теперь создаются с помощью подключенных приложений. Щелкните здесь).</span><span class="sxs-lookup"><span data-stu-id="7654c-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="7654c-131">В разделе **основные сведения**, введите подключенного приложения hello необходимые значения.</span><span class="sxs-lookup"><span data-stu-id="7654c-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="7654c-132">В разделе **параметры веб-приложения**выберите hello **включить SAML** флажок.</span><span class="sxs-lookup"><span data-stu-id="7654c-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="7654c-133">В hello **идентификатор сущности** введите следующий URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="7654c-134">Заменили hello значение `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="7654c-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="7654c-135">В hello **URL-адрес ACS** введите следующий URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="7654c-136">Заменили hello значение `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="7654c-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="7654c-137">Оставьте значения по умолчанию hello другие параметры.</span><span class="sxs-lookup"><span data-stu-id="7654c-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="7654c-138">Прокрутите toohello нижней части списка hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7654c-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="7654c-139">Получить URL-адрес метаданных hello</span><span class="sxs-lookup"><span data-stu-id="7654c-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="7654c-140">На странице Общие сведения о подключенных приложения hello, нажмите кнопку **управление**.</span><span class="sxs-lookup"><span data-stu-id="7654c-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="7654c-141">Скопируйте значение hello для **конечную точку обнаружения метаданных**, а затем сохраните его.</span><span class="sxs-lookup"><span data-stu-id="7654c-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="7654c-142">Оно будет использоваться далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7654c-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="7654c-143">Настройка toofederate пользователей Salesforce</span><span class="sxs-lookup"><span data-stu-id="7654c-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="7654c-144">На hello **управление** страницы подключенных приложений, перейти слишком**профилей**.</span><span class="sxs-lookup"><span data-stu-id="7654c-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="7654c-145">Щелкните **Управление профилями**.</span><span class="sxs-lookup"><span data-stu-id="7654c-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="7654c-146">Выберите профили hello (или группы пользователей), которые должны toofederate с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7654c-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="7654c-147">Системный администратор, выберите hello **системный администратор** флажок, так что можно создать федерацию с помощью учетной записи Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7654c-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="7654c-148">Создание сертификата подписи для Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7654c-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="7654c-149">Подписанные Azure AD B2C toobe необходимость tooSalesforce отправлены запросы.</span><span class="sxs-lookup"><span data-stu-id="7654c-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="7654c-150">toogenerate сертификата подписи, откройте Azure PowerShell и выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="7654c-151">Убедитесь, что необходимо обновить имя клиента hello и пароль в верхнем две строки hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="7654c-152">Добавить tooAzure подписи сертификата hello SAML AD B2C</span><span class="sxs-lookup"><span data-stu-id="7654c-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="7654c-153">Отправьте подписи сертификата клиента Azure AD B2C tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="7654c-154">Go tooyour Azure AD B2C клиента.</span><span class="sxs-lookup"><span data-stu-id="7654c-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="7654c-155">Последовательно выберите **Settings** > **Identity Experience Framework** > **Policy Keys** (Параметры, Инфраструктура процедур идентификации, Ключи политики).</span><span class="sxs-lookup"><span data-stu-id="7654c-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="7654c-156">Щелкните **+Добавить**, а затем:</span><span class="sxs-lookup"><span data-stu-id="7654c-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="7654c-157">Щелкните **Параметры** > **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="7654c-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="7654c-158">Введите **имя** (например, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="7654c-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="7654c-159">префикс Hello *B2C_1A_* автоматически добавляется toohello имя ключа.</span><span class="sxs-lookup"><span data-stu-id="7654c-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="7654c-160">tooselect свой сертификат, выберите **отправить файл управления**.</span><span class="sxs-lookup"><span data-stu-id="7654c-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="7654c-161">Введите пароль сертификата hello, заданный в скрипте PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="7654c-162">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7654c-162">Click **Create**.</span></span>
4. <span data-ttu-id="7654c-163">Убедитесь, что ключ создан (например, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="7654c-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="7654c-164">Запишите hello полное имя (включая *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="7654c-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="7654c-165">Можно будет ссылаться toothis ключ позже в политике hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="7654c-166">Создать hello поставщика утверждений Salesforce SAML в базовый политике</span><span class="sxs-lookup"><span data-stu-id="7654c-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="7654c-167">Вам требуется toodefine Salesforce в качестве поставщика утверждений, пользователи могут войти в с помощью Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7654c-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="7654c-168">Другими словами вы должны hello toospecify конечную точку, которая будет взаимодействовать Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7654c-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="7654c-169">Конечная точка Hello будет *предоставляют* набор *утверждений* , Azure AD B2C использует tooverify проверку определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="7654c-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="7654c-170">toodo это, добавьте `<ClaimsProvider>` для Salesforce в файле расширения hello политики:</span><span class="sxs-lookup"><span data-stu-id="7654c-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="7654c-171">В рабочий каталог откройте файл расширения hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="7654c-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="7654c-172">Найти hello `<ClaimsProviders>` раздела.</span><span class="sxs-lookup"><span data-stu-id="7654c-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="7654c-173">Если он не существует, создайте его в корневом узле hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="7654c-174">Добавьте новый `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="7654c-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

<span data-ttu-id="7654c-175">В разделе hello `<ClaimsProvider>` узла:</span><span class="sxs-lookup"><span data-stu-id="7654c-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="7654c-176">Измените значение hello `<Domain>` tooa уникальное значение, отличающее `<ClaimsProvider>` от других поставщиков удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7654c-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="7654c-177">Измените значение в hello `<DisplayName>` tooa отображаемое имя для hello поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="7654c-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="7654c-178">Сейчас это значение не используется.</span><span class="sxs-lookup"><span data-stu-id="7654c-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="7654c-179">Обновление профиля технические hello</span><span class="sxs-lookup"><span data-stu-id="7654c-179">Update hello technical profile</span></span>

<span data-ttu-id="7654c-180">tooget маркер SAML из Salesforce, определите протоколы hello, использование Azure AD B2C toocommunicate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7654c-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7654c-181">Для этого в hello `<TechnicalProfile>` элемент `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="7654c-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="7654c-182">Обновить идентификатор hello hello `<TechnicalProfile>` узла.</span><span class="sxs-lookup"><span data-stu-id="7654c-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="7654c-183">Этот идентификатор является toothis используется toorefer технические профиль из других частей hello политики.</span><span class="sxs-lookup"><span data-stu-id="7654c-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="7654c-184">Измените значение в hello `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="7654c-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="7654c-185">Это значение отображается hello вход кнопку на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="7654c-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="7654c-186">Измените значение в hello `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="7654c-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="7654c-187">SalesForce с помощью протокола hello SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="7654c-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="7654c-188">Убедитесь, что значение hello для `<Protocol>` — **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="7654c-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="7654c-189">Обновление hello `<Metadata>` раздела hello, предшествующий настройки hello tooreflect XML для определенной учетной записи Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7654c-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="7654c-190">Обновление hello значения метаданных для hello XML:</span><span class="sxs-lookup"><span data-stu-id="7654c-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="7654c-191">Обновите значение hello `<Item Key="PartnerEntity">` с hello Salesforce URL-адрес метаданных скопированное ранее.</span><span class="sxs-lookup"><span data-stu-id="7654c-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="7654c-192">Он имеет следующий формат hello:</span><span class="sxs-lookup"><span data-stu-id="7654c-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="7654c-193">В hello `<CryptographicKeys>` статьи, значение hello обновления для обоих экземпляров `StorageReferenceId` toohello имя hello ключа сертификата подписи (например, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="7654c-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="7654c-194">Отправить файл hello расширения для проверки</span><span class="sxs-lookup"><span data-stu-id="7654c-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="7654c-195">Политика настроена, чтобы Azure AD B2C известно как toocommunicate с Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7654c-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="7654c-196">Попробуйте отправить файл hello расширения политики, tooverify, что в нем не все проблемы до сих.</span><span class="sxs-lookup"><span data-stu-id="7654c-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="7654c-197">файл расширения hello tooupload политики:</span><span class="sxs-lookup"><span data-stu-id="7654c-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="7654c-198">В клиенте Azure AD B2C go toohello **все политики** колонку.</span><span class="sxs-lookup"><span data-stu-id="7654c-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="7654c-199">Выберите hello **перезаписать hello политики, если он существует** флажок.</span><span class="sxs-lookup"><span data-stu-id="7654c-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="7654c-200">Отправьте файл расширения hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="7654c-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="7654c-201">Убедитесь, что проверка пройдена.</span><span class="sxs-lookup"><span data-stu-id="7654c-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="7654c-202">Регистрация hello Salesforce SAML утверждения поставщика tooa пользователя пути</span><span class="sxs-lookup"><span data-stu-id="7654c-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="7654c-203">Затем добавьте hello tooone поставщика удостоверений Salesforce SAML для вашего пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="7654c-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="7654c-204">На этом этапе Настройка поставщика удостоверений hello, но он не доступен на всех страницах регистрации или входа пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="7654c-205">tooadd hello удостоверение поставщика tooa страницы входа, сначала необходимо создать копию существующего шаблона пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="7654c-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="7654c-206">Измените шаблон hello, придав ему hello поставщика удостоверений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7654c-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="7654c-207">Откройте файл базовый hello политики (например, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="7654c-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="7654c-208">Найти hello `<UserJourneys>` элемент, а затем hello Копировать всю `<UserJourney>` значений, включая идентификатор = «SignUpOrSignIn».</span><span class="sxs-lookup"><span data-stu-id="7654c-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="7654c-209">Откройте файл hello расширения (например, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="7654c-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="7654c-210">Найти hello `<UserJourneys>` элемента.</span><span class="sxs-lookup"><span data-stu-id="7654c-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="7654c-211">Если элемент hello не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="7654c-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="7654c-212">Вставить hello всего скопировать `<UserJourney>` как дочерний hello `<UserJourneys>` элемента.</span><span class="sxs-lookup"><span data-stu-id="7654c-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="7654c-213">Переименуйте идентификатор hello hello новый `<UserJourney>` (например, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="7654c-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="7654c-214">Кнопку поставщика удостоверений hello отображения</span><span class="sxs-lookup"><span data-stu-id="7654c-214">Display hello identity provider button</span></span>

<span data-ttu-id="7654c-215">Hello `<ClaimsProviderSelection>` элемент является аналогом tooan кнопку поставщика удостоверений на странице регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="7654c-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="7654c-216">Добавив `<ClaimsProviderSelection>` элемент для Salesforce новая кнопка отображается при посещении toothis страницы.</span><span class="sxs-lookup"><span data-stu-id="7654c-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="7654c-217">Кнопка поставщика удостоверений hello toodisplay:</span><span class="sxs-lookup"><span data-stu-id="7654c-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="7654c-218">В hello `<UserJourney>` , созданный, найти hello `<OrchestrationStep>` с `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="7654c-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="7654c-219">Добавьте следующий XML-код hello:</span><span class="sxs-lookup"><span data-stu-id="7654c-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="7654c-220">Задать `TargetClaimsExchangeId` tooa логическое значение.</span><span class="sxs-lookup"><span data-stu-id="7654c-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="7654c-221">Мы рекомендуем следующие hello же соглашениями, что и другие (например,  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="7654c-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="7654c-222">Действие tooan кнопку поставщика удостоверений ссылки hello</span><span class="sxs-lookup"><span data-stu-id="7654c-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="7654c-223">Теперь, когда имеется кнопка поставщика удостоверений в месте, свяжите его tooan действие.</span><span class="sxs-lookup"><span data-stu-id="7654c-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="7654c-224">В этом случае hello действии для Azure AD B2C toocommunicate с Salesforce tooreceive маркера SAML.</span><span class="sxs-lookup"><span data-stu-id="7654c-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="7654c-225">Это можно сделать путем связывания hello технические профиля для вашего Salesforce SAML поставщика утверждений:</span><span class="sxs-lookup"><span data-stu-id="7654c-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="7654c-226">В hello `<UserJourney>` узел, найти hello `<OrchestrationStep>` с `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="7654c-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="7654c-227">Добавьте следующий XML-код hello:</span><span class="sxs-lookup"><span data-stu-id="7654c-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="7654c-228">Обновление `Id` toohello одинаковое значение, которые использовали для `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="7654c-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="7654c-229">Обновление `TechnicalProfileReferenceId` toohello `Id` hello технические профиля созданную ранее (например, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="7654c-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="7654c-230">Отправка файла обновленного расширения hello</span><span class="sxs-lookup"><span data-stu-id="7654c-230">Upload hello updated extension file</span></span>

<span data-ttu-id="7654c-231">Изменение файла hello расширения завершено.</span><span class="sxs-lookup"><span data-stu-id="7654c-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="7654c-232">Сохраните и отправьте этот файл.</span><span class="sxs-lookup"><span data-stu-id="7654c-232">Save and upload this file.</span></span> <span data-ttu-id="7654c-233">Убедитесь, что все проверки пройдены успешно.</span><span class="sxs-lookup"><span data-stu-id="7654c-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="7654c-234">Обновить проверяющей стороной файл hello</span><span class="sxs-lookup"><span data-stu-id="7654c-234">Update hello relying party file</span></span>

<span data-ttu-id="7654c-235">Затем обновите hello проверяющей стороны (RP) файл, который инициирует hello пути пользователя, созданный вами:</span><span class="sxs-lookup"><span data-stu-id="7654c-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="7654c-236">Создайте копию SignUpOrSignIn.xml в рабочем каталоге.</span><span class="sxs-lookup"><span data-stu-id="7654c-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="7654c-237">Затем переименуйте ее (например, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="7654c-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="7654c-238">Привет открыть новый файл и обновление hello `PolicyId` для атрибута `<TrustFrameworkPolicy>` с уникальным значением.</span><span class="sxs-lookup"><span data-stu-id="7654c-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="7654c-239">Это имя hello политики (например, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="7654c-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="7654c-240">Изменение hello `ReferenceId` атрибута в `<DefaultUserJourney>` toomatch hello `Id` из нового пользователя пути hello созданный вами (например, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="7654c-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="7654c-241">Сохранить изменения, а затем отправьте файл hello.</span><span class="sxs-lookup"><span data-stu-id="7654c-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="7654c-242">Тестирование и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7654c-242">Test and troubleshoot</span></span>

<span data-ttu-id="7654c-243">пользовательские политики hello tootest, только что переданного, в hello портал Azure, перейдите в колонку toohello политики и нажмите кнопку **запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="7654c-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="7654c-244">В случае неудачи см. сведения в разделе [Устранение неполадок пользовательских политик](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="7654c-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7654c-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7654c-245">Next steps</span></span>

<span data-ttu-id="7654c-246">Отправить отзыв слишком[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7654c-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
