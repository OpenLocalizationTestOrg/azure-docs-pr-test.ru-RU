---
title: "Azure Active Directory B2C. Добавление поставщика SAML Salesforce с помощью пользовательских политик | Документы Майкрософт"
description: "В этой статье содержатся сведения о создании пользовательских политик Azure Active Directory B2C и управлении ими."
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
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="bd2ca-103">Azure Active Directory B2C. Выполнение входа с помощью учетных записей Salesforce через SAML</span><span class="sxs-lookup"><span data-stu-id="bd2ca-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="bd2ca-104">В этой статье описывается настройка входа для пользователей из определенной организации Salesforce с помощью [пользовательских политик](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd2ca-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bd2ca-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="bd2ca-106">Настройка Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bd2ca-106">Azure AD B2C setup</span></span>

<span data-ttu-id="bd2ca-107">Убедитесь, что вы выполнили все действия, связанные с [началом работы с пользовательскими политиками](active-directory-b2c-get-started-custom.md) в Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="bd2ca-108">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-108">These include:</span></span>

* <span data-ttu-id="bd2ca-109">Создание клиента Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="bd2ca-110">Создание приложения Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="bd2ca-111">Регистрация двух приложений подсистемы политик.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="bd2ca-112">Настройка ключей.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-112">Set up keys.</span></span>
* <span data-ttu-id="bd2ca-113">Настройка начального пакета.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="bd2ca-114">Настройка Salesforce</span><span class="sxs-lookup"><span data-stu-id="bd2ca-114">Salesforce setup</span></span>

<span data-ttu-id="bd2ca-115">Для выполнения действий, описанных в этой статье, вам необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="bd2ca-116">Подписка на учетную запись Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="bd2ca-117">Вы можете зарегистрироваться для получения [бесплатной учетной записи Developer Edition](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="bd2ca-118">[Настройка собственного домена](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) для организации Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="bd2ca-119">Настройка Salesforce для федерации пользователей</span><span class="sxs-lookup"><span data-stu-id="bd2ca-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="bd2ca-120">Чтобы обеспечить взаимодействие Azure AD B2C с Salesforce, необходимо получить URL-адрес метаданных Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="bd2ca-121">Настройка Salesforce в качестве поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="bd2ca-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="bd2ca-122">В этой статье предполагается, что вы используете [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="bd2ca-123">[Войдите в Salesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="bd2ca-124">В меню слева в разделе **Параметры** разверните узел **Удостоверение** и щелкните **Поставщик удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="bd2ca-125">Щелкните **Enable Identity Provider** (Включить поставщик удостоверений).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="bd2ca-126">В разделе **Select the certificate** (Выберите сертификат) выберите сертификат, который необходимо использовать в Salesforce при взаимодействии с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="bd2ca-127">Вы можете использовать сертификат по умолчанию. Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="bd2ca-128">Создание подключенного приложения в Salesforce</span><span class="sxs-lookup"><span data-stu-id="bd2ca-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="bd2ca-129">На странице **Поставщик удостоверений** перейдите в раздел **Поставщики услуг**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="bd2ca-130">Щелкните **Service Providers are now created via Connected Apps. Click here** (Поставщики услуг теперь создаются с помощью подключенных приложений. Щелкните здесь).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="bd2ca-131">В разделе **Основные сведения** введите нужные значения для подключенного приложения.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="bd2ca-132">В разделе **Параметры веб-приложения** установите флажок **Включить SAML**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="bd2ca-133">В поле **Идентификатор сущности** введите следующий URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="bd2ca-134">Проверьте, заменено ли значение `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="bd2ca-135">В поле **ACS URL** (URL-адрес ACS) введите приведенный ниже URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="bd2ca-136">Проверьте, заменено ли значение `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="bd2ca-137">Для остальных параметров оставьте значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="bd2ca-138">Прокрутите до нижней части списка и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="bd2ca-139">Получить URL-адреса метаданных</span><span class="sxs-lookup"><span data-stu-id="bd2ca-139">Get the metadata URL</span></span>

1. <span data-ttu-id="bd2ca-140">На странице общих сведений о подключенном приложении щелкните **Управление**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="bd2ca-141">Скопируйте значение **конечной точки обнаружения метаданных**, а затем сохраните его.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="bd2ca-142">Оно будет использоваться далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="bd2ca-143">Настройка пользователей Salesforce для федерации</span><span class="sxs-lookup"><span data-stu-id="bd2ca-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="bd2ca-144">На странице **Управление** подключенного приложения перейдите в раздел **Профили**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="bd2ca-145">Щелкните **Управление профилями**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="bd2ca-146">Выберите профили (или группы пользователей) для федерации с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="bd2ca-147">Используя права системного администратора, установите флажок **Системный администратор** для федерации с помощью учетной записи Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="bd2ca-148">Создание сертификата подписи для Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bd2ca-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="bd2ca-149">Запросы, отправляемые в Salesforce, должны быть подписаны Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="bd2ca-150">Чтобы создать сертификат подписи, откройте Azure PowerShell и выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="bd2ca-151">Обновите имя клиента и пароль в первых двух строках.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="bd2ca-152">Добавление сертификата подписи SAML в Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bd2ca-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="bd2ca-153">Отправьте сертификат подписи в клиент Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="bd2ca-154">Перейдите в клиент Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="bd2ca-155">Последовательно выберите **Settings** > **Identity Experience Framework** > **Policy Keys** (Параметры, Инфраструктура процедур идентификации, Ключи политики).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="bd2ca-156">Щелкните **+Добавить**, а затем:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="bd2ca-157">Щелкните **Параметры** > **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="bd2ca-158">Введите **имя** (например, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="bd2ca-159">Префикс *B2C_1A_* будет автоматически добавлен к имени ключа.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="bd2ca-160">Чтобы выбрать сертификат, выберите **элемент управления отправкой файла**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="bd2ca-161">Введите пароль сертификата, который задан в скрипте PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="bd2ca-162">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-162">Click **Create**.</span></span>
4. <span data-ttu-id="bd2ca-163">Убедитесь, что ключ создан (например, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="bd2ca-164">Запишите полное имя (включая *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="bd2ca-165">Вы будете ссылаться на этот ключ позднее в политике.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="bd2ca-166">Создание поставщика утверждений SAML Salesforce в базовой политике</span><span class="sxs-lookup"><span data-stu-id="bd2ca-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="bd2ca-167">Чтобы пользователи могли выполнять вход с помощью Salesforce, необходимо определить Salesforce в качестве поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="bd2ca-168">Другими словами, необходимо указать конечную точку, с которой будет взаимодействовать Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="bd2ca-169">Конечная точка *предоставит* набор *утверждений*, используемых Azure AD B2C, чтобы проверить, была ли выполнена проверка подлинности определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="bd2ca-170">Это можно сделать, добавив `<ClaimsProvider>` для Salesforce в файл расширения политики.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="bd2ca-171">Откройте файл расширения (TrustFrameworkExtensions.xml) из рабочего каталога.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="bd2ca-172">Найдите раздел `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="bd2ca-173">Если он не существует, создайте его в корневом узле.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="bd2ca-174">Добавьте новый `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="bd2ca-175">В узле `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="bd2ca-176">Укажите для `<Domain>` уникальное значение, позволяющее отличить этот `<ClaimsProvider>` от других.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="bd2ca-177">Задайте для `<DisplayName>` отображаемое имя поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="bd2ca-178">Сейчас это значение не используется.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="bd2ca-179">Обновление технического профиля</span><span class="sxs-lookup"><span data-stu-id="bd2ca-179">Update the technical profile</span></span>

<span data-ttu-id="bd2ca-180">Чтобы получить токен SAML из Salesforce, определите протоколы, используемые Azure AD B2C для взаимодействия с Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bd2ca-181">Сделайте в элементе `<TechnicalProfile>` поставщика `<ClaimsProvider>` следующее:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="bd2ca-182">Обновите идентификатор узла `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="bd2ca-183">Этот идентификатор используется для ссылки на этот технический профиль из других частей политики.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="bd2ca-184">Обновите значение для `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="bd2ca-185">Это значение отображается на кнопке входа на экране входа.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="bd2ca-186">Обновите значение для `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="bd2ca-187">Salesforce использует протокол SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="bd2ca-188">Убедитесь, что значение для `<Protocol>` — **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="bd2ca-189">Обновите раздел `<Metadata>` в предыдущем коде XML в соответствии с параметрами для определенной учетной записи Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="bd2ca-190">В коде XML обновите значения метаданных:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="bd2ca-191">Измените значение `<Item Key="PartnerEntity">` на скопированный ранее URL-адрес метаданных Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="bd2ca-192">В нем используется следующий формат:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="bd2ca-193">В разделе `<CryptographicKeys>` измените значение для обоих экземпляров `StorageReferenceId` на имя ключа сертификата подписи (например, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="bd2ca-194">Отправка файла расширения для проверки</span><span class="sxs-lookup"><span data-stu-id="bd2ca-194">Upload the extension file for verification</span></span>

<span data-ttu-id="bd2ca-195">Теперь политика настроена, а Azure AD B2C известно, как взаимодействовать с Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="bd2ca-196">Попробуйте отправить файл расширения политики, чтобы убедиться, что все в порядке.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="bd2ca-197">Чтобы отправить файл расширения политики:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="bd2ca-198">В клиенте Azure AD B2C перейдите в колонку **Все политики**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="bd2ca-199">Установите флажок **Перезаписать политику, если она существует**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="bd2ca-200">Отправьте файл расширения (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="bd2ca-201">Убедитесь, что проверка пройдена.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="bd2ca-202">Регистрация поставщика утверждений SAML Salesforce для пути взаимодействия пользователя</span><span class="sxs-lookup"><span data-stu-id="bd2ca-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="bd2ca-203">Теперь вам необходимо добавить поставщик удостоверений SAML Salesforce в один из путей взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="bd2ca-204">На этом этапе поставщик удостоверений уже настроен, но еще не доступен ни на одной странице регистрации или входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="bd2ca-205">Чтобы добавить поставщик на страницу входа, сначала создайте копию существующего шаблона пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="bd2ca-206">Затем измените шаблон, чтобы у него также был поставщик удостоверений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="bd2ca-207">Откройте базовый файл политики (например, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="bd2ca-208">Найдите элемент `<UserJourneys>` и скопируйте полное значение `<UserJourney>`, включая Id="SignUpOrSignIn".</span><span class="sxs-lookup"><span data-stu-id="bd2ca-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="bd2ca-209">Откройте файл расширения (например, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="bd2ca-210">Найдите элемент `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="bd2ca-211">Если элемент не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="bd2ca-212">Вставьте весь скопированный путь `<UserJourney>` как дочерний элемент `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="bd2ca-213">Переименуйте идентификатор нового пути `<UserJourney>` (например, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="bd2ca-214">Отображение кнопки поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="bd2ca-214">Display the identity provider button</span></span>

<span data-ttu-id="bd2ca-215">Элемент `<ClaimsProviderSelection>` является аналогом кнопки поставщика удостоверений на странице регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="bd2ca-216">Если вы добавите для Salesforce элемент `<ClaimsProviderSelection>`, новая кнопка отобразится при переходе пользователя на эту страницу.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="bd2ca-217">Чтобы отобразить кнопку поставщика удостоверений:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="bd2ca-218">В созданном `<UserJourney>` найдите `<OrchestrationStep>` со значением `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="bd2ca-219">Добавьте следующий код XML:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="bd2ca-220">Задайте для `TargetClaimsExchangeId` логическое значение.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="bd2ca-221">Мы советуем следовать общему соглашению: (например, *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="bd2ca-222">Связывание кнопки поставщика удостоверений с действием</span><span class="sxs-lookup"><span data-stu-id="bd2ca-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="bd2ca-223">Теперь, когда у вас есть кнопка поставщика удостоверений, свяжите ее с действием.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="bd2ca-224">В этом случае действие — это возможность взаимодействия Azure AD B2C с Salesforce для получения токена SAML.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="bd2ca-225">Чтобы получить эту возможность, необходимо связать технический профиль для поставщика утверждений SAML Salesforce.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="bd2ca-226">В узле `<UserJourney>` найдите `<OrchestrationStep>` со значением `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="bd2ca-227">Добавьте следующий код XML:</span><span class="sxs-lookup"><span data-stu-id="bd2ca-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="bd2ca-228">Измените `Id` на то же значение, которое ранее использовалось для `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="bd2ca-229">Задайте для `TechnicalProfileReferenceId` значение `Id` ранее созданного технического профиля (например, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="bd2ca-230">Передача обновленного файла расширения</span><span class="sxs-lookup"><span data-stu-id="bd2ca-230">Upload the updated extension file</span></span>

<span data-ttu-id="bd2ca-231">Вы внесли все необходимые изменения в файл расширения.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-231">You are done modifying the extension file.</span></span> <span data-ttu-id="bd2ca-232">Сохраните и отправьте этот файл.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-232">Save and upload this file.</span></span> <span data-ttu-id="bd2ca-233">Убедитесь, что все проверки пройдены успешно.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="bd2ca-234">Обновление файла проверяющей стороны</span><span class="sxs-lookup"><span data-stu-id="bd2ca-234">Update the relying party file</span></span>

<span data-ttu-id="bd2ca-235">Теперь обновите файл проверяющей стороны, который активирует созданный путь взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="bd2ca-236">Создайте копию SignUpOrSignIn.xml в рабочем каталоге.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="bd2ca-237">Затем переименуйте ее (например, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="bd2ca-238">Откройте новый файл и задайте для атрибута `PolicyId` `<TrustFrameworkPolicy>` уникальное значение.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="bd2ca-239">Это имя вашей политики (например, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="bd2ca-240">Измените атрибут `ReferenceId` в `<DefaultUserJourney>` для соответствия `Id` нового созданного пути взаимодействия пользователя (например, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="bd2ca-241">Сохраните изменения и отправьте файл.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="bd2ca-242">Тестирование и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="bd2ca-242">Test and troubleshoot</span></span>

<span data-ttu-id="bd2ca-243">Чтобы протестировать отправленную настраиваемую политику, на портале Azure перейдите к колонке политики и нажмите кнопку **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="bd2ca-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="bd2ca-244">В случае неудачи см. сведения в разделе [Устранение неполадок пользовательских политик](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd2ca-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd2ca-245">Next steps</span></span>

<span data-ttu-id="bd2ca-246">Свои отзывы отправляйте сюда: [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="bd2ca-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
