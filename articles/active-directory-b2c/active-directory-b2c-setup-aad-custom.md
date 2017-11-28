---
title: "Azure Active Directory B2C. Добавление поставщика Azure AD с помощью пользовательских политик | Документы Майкрософт"
description: "Сведения о пользовательских политиках Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 6c073d70debfdc3560405955d65fa9ccaa7d8b1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="fe02c-103">Azure Active Directory B2C. Выполнение входа с помощью учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe02c-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="fe02c-104">В этой статье описывается включение входа для пользователей из определенной организации Azure Active Directory (Azure AD) с помощью [пользовательских политик](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="fe02c-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe02c-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fe02c-105">Prerequisites</span></span>

<span data-ttu-id="fe02c-106">Выполните шаги, описанные в статье [Azure Active Directory B2C. Приступая к работе с настраиваемыми политиками](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="fe02c-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="fe02c-107">А именно:</span><span class="sxs-lookup"><span data-stu-id="fe02c-107">These steps include:</span></span>

1. <span data-ttu-id="fe02c-108">Создание клиента Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="fe02c-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="fe02c-109">Создание приложения Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fe02c-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="fe02c-110">Регистрация двух приложений подсистемы политик.</span><span class="sxs-lookup"><span data-stu-id="fe02c-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="fe02c-111">Настройка ключей.</span><span class="sxs-lookup"><span data-stu-id="fe02c-111">Setting up keys.</span></span>
5. <span data-ttu-id="fe02c-112">Настройка начального пакета.</span><span class="sxs-lookup"><span data-stu-id="fe02c-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="fe02c-113">Создание приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe02c-113">Create an Azure AD app</span></span>

<span data-ttu-id="fe02c-114">Чтобы включить вход для пользователей из определенной организации Azure AD, вам необходимо зарегистрировать приложение в клиенте организации Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe02c-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="fe02c-115">В следующих инструкциях клиент организации Azure AD будет называться "contoso.com", а клиент Azure AD B2C — "fabrikamb2c.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="fe02c-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="fe02c-116">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe02c-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="fe02c-117">На верхней панели выберите учетную запись.</span><span class="sxs-lookup"><span data-stu-id="fe02c-117">On the top bar, select your account.</span></span> <span data-ttu-id="fe02c-118">В списке **Каталог** выберите клиент организации Azure AD, в котором вы хотите зарегистрировать приложение (например, contoso.com).</span><span class="sxs-lookup"><span data-stu-id="fe02c-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
1. <span data-ttu-id="fe02c-119">В левой области щелкните **Больше служб** и выполните поиск по запросу "регистрация приложений".</span><span class="sxs-lookup"><span data-stu-id="fe02c-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="fe02c-120">Выберите **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="fe02c-121">Введите значение имя для приложения (например, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="fe02c-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="fe02c-122">Выберите в качестве типа приложения **Веб-приложение или API**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-122">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="fe02c-123">В поле **URL-адрес входа** введите следующий URL-адрес, где `yourtenant` заменяется на имя вашего клиента Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="fe02c-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="fe02c-124">Сохраните идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="fe02c-124">Save the application ID.</span></span>
1. <span data-ttu-id="fe02c-125">Щелкните созданное приложение.</span><span class="sxs-lookup"><span data-stu-id="fe02c-125">Select the newly created application.</span></span>
1. <span data-ttu-id="fe02c-126">В колонке **Параметры** щелкните **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-126">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="fe02c-127">Создайте ключ и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="fe02c-127">Create a new key, and save it.</span></span> <span data-ttu-id="fe02c-128">Он понадобится для выполнения действий в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="fe02c-128">You will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="fe02c-129">Добавление ключа Azure AD в Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="fe02c-129">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="fe02c-130">Вам необходимо сохранить ключ приложения contoso.com в клиенте Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fe02c-130">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="fe02c-131">Для этого:</span><span class="sxs-lookup"><span data-stu-id="fe02c-131">To do this:</span></span>
1. <span data-ttu-id="fe02c-132">Перейдите к клиенту Azure AD B2C и последовательно выберите **B2C Settings** > **Identity Experience Framework** > **Policy Keys** (Параметры B2C > Инфраструктура процедур идентификации > Ключи политики).</span><span class="sxs-lookup"><span data-stu-id="fe02c-132">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="fe02c-133">Щелкните **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-133">Select **+Add**.</span></span>
1. <span data-ttu-id="fe02c-134">Выберите или введите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="fe02c-134">Select or enter these options:</span></span>
   * <span data-ttu-id="fe02c-135">Выберите **Вручную**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-135">Select **Manual**.</span></span>
   * <span data-ttu-id="fe02c-136">Для параметра **Имя** выберите имя, соответствующее имени клиента Azure AD (например, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="fe02c-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="fe02c-137">Префикс `B2C_1A_` будет автоматически добавлен к имени ключа.</span><span class="sxs-lookup"><span data-stu-id="fe02c-137">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="fe02c-138">Вставьте ключ приложения в текстовое поле **Секрет**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-138">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="fe02c-139">Выберите **Подпись**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-139">Select **Signature**.</span></span>
1. <span data-ttu-id="fe02c-140">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-140">Select **Create**.</span></span>
1. <span data-ttu-id="fe02c-141">Убедитесь, что вы создали ключ `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-141">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="fe02c-142">Добавление поставщика утверждений в базовую политику</span><span class="sxs-lookup"><span data-stu-id="fe02c-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="fe02c-143">Чтобы пользователи выполняли вход с помощью Azure AD, необходимо определить Azure AD в качестве поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="fe02c-143">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="fe02c-144">Другими словами, необходимо указать конечную точку, с которой будет взаимодействовать Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fe02c-144">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="fe02c-145">Конечная точка предоставит набор утверждений, используемых Azure AD B2C, чтобы проверить, была ли выполнена проверка подлинности определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="fe02c-145">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="fe02c-146">Можно определить Azure AD в качестве поставщика утверждений, добавив Azure AD в узел `<ClaimsProvider>` в файл расширения политики.</span><span class="sxs-lookup"><span data-stu-id="fe02c-146">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="fe02c-147">Откройте файл расширения (TrustFrameworkExtensions.xml) из рабочего каталога.</span><span class="sxs-lookup"><span data-stu-id="fe02c-147">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="fe02c-148">Найдите раздел `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-148">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="fe02c-149">Если он не существует, добавьте его в корневой узел.</span><span class="sxs-lookup"><span data-stu-id="fe02c-149">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="fe02c-150">Добавьте новый `<ClaimsProvider>`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fe02c-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
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

1. <span data-ttu-id="fe02c-151">В узле `<ClaimsProvider>` укажите для `<Domain>` уникальное значение, позволяющее отличить этот поставщик удостоверений от других.</span><span class="sxs-lookup"><span data-stu-id="fe02c-151">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="fe02c-152">В узле `<ClaimsProvider>` задайте для `<DisplayName>` понятное имя поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="fe02c-152">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="fe02c-153">В настоящее время это значение не используется.</span><span class="sxs-lookup"><span data-stu-id="fe02c-153">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="fe02c-154">Обновление технического профиля</span><span class="sxs-lookup"><span data-stu-id="fe02c-154">Update the technical profile</span></span>

<span data-ttu-id="fe02c-155">Чтобы получить токен из конечной точки Azure AD, вам необходимо определить протоколы, используемые Azure AD B2C для взаимодействия с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe02c-155">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="fe02c-156">Этот процесс происходит внутри элемента `<TechnicalProfile>` поставщика `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-156">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="fe02c-157">Обновите идентификатор узла `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-157">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="fe02c-158">Этот идентификатор используется для ссылки на этот технический профиль из других частей политики.</span><span class="sxs-lookup"><span data-stu-id="fe02c-158">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="fe02c-159">Обновите значение для `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-159">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="fe02c-160">Это значение будет отображаться на кнопке входа на экране входа в систему.</span><span class="sxs-lookup"><span data-stu-id="fe02c-160">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="fe02c-161">Обновите значение для `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-161">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="fe02c-162">Azure AD использует протокол OpenID Connect, поэтому для `<Protocol>` должно быть задано значение `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-162">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="fe02c-163">Вам следует обновить раздел `<Metadata>` в приведенном выше коде XML, чтобы добавить параметры конфигурации для определенного клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe02c-163">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="fe02c-164">В XML-файле обновите значения метаданных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fe02c-164">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="fe02c-165">Задайте для параметра `<Item Key="METADATA">` значение `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, где `yourAzureADtenant` — это имя клиента Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="fe02c-165">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="fe02c-166">Откройте браузер и перейдите к URL-адресу `METADATA`, который вы только что обновили.</span><span class="sxs-lookup"><span data-stu-id="fe02c-166">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="fe02c-167">Найдите на этой странице в браузере объект issuer и скопируйте его значение.</span><span class="sxs-lookup"><span data-stu-id="fe02c-167">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="fe02c-168">Вы должны увидеть примерно следующее: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-168">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="fe02c-169">Вставьте значение для `<Item Key="ProviderName">` в XML-файл.</span><span class="sxs-lookup"><span data-stu-id="fe02c-169">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="fe02c-170">Задайте для параметра `<Item Key="client_id">` значение идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="fe02c-170">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="fe02c-171">Задайте для параметра `<Item Key="IdTokenAudience">` значение идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="fe02c-171">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="fe02c-172">Задайте для параметра `<Item Key="response_types">` значение `id_token`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-172">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="fe02c-173">Задайте для параметра `<Item Key="UsePolicyInRedirectUri">` значение `false`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="fe02c-174">Вам также необходимо связать секрет Azure AD, зарегистрированный в клиенте Azure AD B2C, с информацией о `<ClaimsProvider>` Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe02c-174">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="fe02c-175">В разделе `<CryptographicKeys>` в приведенном выше XML-файле задайте для `StorageReferenceId` эталонный идентификатор определенного секрета (например, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="fe02c-175">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="fe02c-176">Отправка файла расширения для проверки</span><span class="sxs-lookup"><span data-stu-id="fe02c-176">Upload the extension file for verification</span></span>

<span data-ttu-id="fe02c-177">К этому моменту политика настроена, так что Azure AD B2C знает, как взаимодействовать с каталогом Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe02c-177">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="fe02c-178">Попробуйте отправить файл расширения политики, чтобы убедиться, что все в порядке.</span><span class="sxs-lookup"><span data-stu-id="fe02c-178">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="fe02c-179">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fe02c-179">To do so:</span></span>

1. <span data-ttu-id="fe02c-180">Откройте колонку **Все политики** в клиенте Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fe02c-180">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="fe02c-181">Установите флажок **Перезаписать политику, если она существует**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-181">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="fe02c-182">Отправьте файл расширения (TrustFrameworkExtensions.xml) и немного подождите, чтобы удостовериться в отсутствии сбоя при проверке.</span><span class="sxs-lookup"><span data-stu-id="fe02c-182">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="fe02c-183">Регистрация поставщика утверждений Azure AD для пути взаимодействия пользователя</span><span class="sxs-lookup"><span data-stu-id="fe02c-183">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="fe02c-184">Теперь вам необходимо добавить поставщик удостоверений Azure AD в один из путей взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="fe02c-184">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="fe02c-185">На этом этапе поставщик удостоверений уже настроен, но еще не доступен ни на одном экране регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="fe02c-185">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="fe02c-186">Чтобы сделать его доступным, необходимо создать дубликат существующего шаблона пути взаимодействия пользователя, а затем изменить его таким образом, чтобы он также содержал поставщик удостоверений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe02c-186">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="fe02c-187">Откройте базовый файл политики (например, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="fe02c-187">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="fe02c-188">Найдите элемент `<UserJourneys>` и скопируйте полный узел `<UserJourney>` с `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-188">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="fe02c-189">Откройте файл расширения (например, TrustFrameworkExtensions.xml) и найдите элемент `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-189">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="fe02c-190">Если элемент не существует, добавьте его.</span><span class="sxs-lookup"><span data-stu-id="fe02c-190">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="fe02c-191">Вставьте весь скопированный узел `<UserJourney>` как дочерний элемент `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-191">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="fe02c-192">Переименуйте идентификатор нового пути пользователя (например, переименуйте как `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="fe02c-192">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="fe02c-193">Отображение кнопки</span><span class="sxs-lookup"><span data-stu-id="fe02c-193">Display the "button"</span></span>

<span data-ttu-id="fe02c-194">Элемент `<ClaimsProviderSelection>` является аналогом кнопки поставщика удостоверений на экране регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="fe02c-194">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="fe02c-195">Если вы добавите для Azure AD элемент `<ClaimsProviderSelection>`, новая кнопка отобразится при переходе пользователя на страницу.</span><span class="sxs-lookup"><span data-stu-id="fe02c-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="fe02c-196">Для этого:</span><span class="sxs-lookup"><span data-stu-id="fe02c-196">To add this element:</span></span>

1. <span data-ttu-id="fe02c-197">Найдите узел `<OrchestrationStep>`, который содержит `Order="1"` в только что созданном пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="fe02c-197">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="fe02c-198">Добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="fe02c-198">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="fe02c-199">Задайте для параметра `TargetClaimsExchangeId` соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="fe02c-199">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="fe02c-200">Мы советуем следовать общему соглашению: *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="fe02c-200">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="fe02c-201">Связывание кнопки с действием</span><span class="sxs-lookup"><span data-stu-id="fe02c-201">Link the button to an action</span></span>

<span data-ttu-id="fe02c-202">Теперь, когда у вас есть кнопка, вам необходимо связать ее с действием.</span><span class="sxs-lookup"><span data-stu-id="fe02c-202">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="fe02c-203">В этом случае действие — это возможность взаимодействия Azure AD B2C с Azure AD для получения токена.</span><span class="sxs-lookup"><span data-stu-id="fe02c-203">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="fe02c-204">Свяжите кнопку с действием, связав технический профиль для поставщика утверждений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe02c-204">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="fe02c-205">Найдите `<OrchestrationStep>`, который содержит `Order="2"` в узле `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="fe02c-205">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="fe02c-206">Добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="fe02c-206">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="fe02c-207">Обновите `Id` до того же значения, которое имеет `TargetClaimsExchangeId` в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="fe02c-207">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="fe02c-208">Задайте для `TechnicalProfileReferenceId` значение идентификатора ранее созданного технического профиля (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="fe02c-208">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="fe02c-209">Передача обновленного файла расширения</span><span class="sxs-lookup"><span data-stu-id="fe02c-209">Upload the updated extension file</span></span>

<span data-ttu-id="fe02c-210">Вы внесли все необходимые изменения в файл расширения.</span><span class="sxs-lookup"><span data-stu-id="fe02c-210">You are done modifying the extension file.</span></span> <span data-ttu-id="fe02c-211">Сохраните его.</span><span class="sxs-lookup"><span data-stu-id="fe02c-211">Save it.</span></span> <span data-ttu-id="fe02c-212">Затем отправьте этот файл. Подождите немного, чтобы убедиться, что все проверки завершены успешно.</span><span class="sxs-lookup"><span data-stu-id="fe02c-212">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="fe02c-213">Обновление файла проверяющей стороны</span><span class="sxs-lookup"><span data-stu-id="fe02c-213">Update the RP file</span></span>

<span data-ttu-id="fe02c-214">Теперь необходимо обновить файл проверяющей стороны, который активирует созданный путь взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="fe02c-214">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="fe02c-215">Создайте копию SignUpOrSignIn.xml в рабочем каталоге и переименуйте его (например, на SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="fe02c-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="fe02c-216">Откройте новый файл и задайте для атрибута `PolicyId` для `<TrustFrameworkPolicy>` новое уникальное значение (например, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="fe02c-216">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="fe02c-217">Это будет имя вашей политики (например, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="fe02c-217">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="fe02c-218">Задайте для атрибута `ReferenceId` в `<DefaultUserJourney>` идентификатор созданного пути взаимодействия пользователя (например, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="fe02c-218">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="fe02c-219">Сохраните изменения и отправьте файл.</span><span class="sxs-lookup"><span data-stu-id="fe02c-219">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fe02c-220">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="fe02c-220">Troubleshooting</span></span>

<span data-ttu-id="fe02c-221">Проверьте пользовательскую политику, которую вы отправили. Для этого откройте ее колонку и щелкните **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="fe02c-221">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="fe02c-222">Для диагностики проблем ознакомьтесь со статьей по [устранению неполадок](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="fe02c-222">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe02c-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe02c-223">Next steps</span></span>

<span data-ttu-id="fe02c-224">Свои отзывы отправляйте сюда: [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="fe02c-224">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
