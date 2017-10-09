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
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="2f174-103">Azure Active Directory B2C. Выполнение входа с помощью учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f174-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="2f174-104">В этой статье показано, как tooenable вход для пользователей в определенной организации Azure Active Directory (Azure AD) через использование hello [настраиваемые политики](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2f174-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f174-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2f174-105">Prerequisites</span></span>

<span data-ttu-id="2f174-106">Hello завершения шагов в hello [Приступая к работе с помощью настроенных политик](active-directory-b2c-get-started-custom.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="2f174-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="2f174-107">А именно:</span><span class="sxs-lookup"><span data-stu-id="2f174-107">These steps include:</span></span>

1. <span data-ttu-id="2f174-108">Создание клиента Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="2f174-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="2f174-109">Создание приложения Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2f174-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="2f174-110">Регистрация двух приложений подсистемы политик.</span><span class="sxs-lookup"><span data-stu-id="2f174-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="2f174-111">Настройка ключей.</span><span class="sxs-lookup"><span data-stu-id="2f174-111">Setting up keys.</span></span>
5. <span data-ttu-id="2f174-112">Настройка пакета начального приветствия.</span><span class="sxs-lookup"><span data-stu-id="2f174-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="2f174-113">Создание приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f174-113">Create an Azure AD app</span></span>

<span data-ttu-id="2f174-114">tooenable вход для пользователей в конкретной организации Azure AD необходимо tooregister приложения в рамках клиента hello организации Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f174-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="2f174-115">Мы используем «contoso.com» для клиента hello организации Azure AD и «fabrikamb2c.onmicrosoft.com», как клиент Azure AD B2C hello в hello, следуя инструкциям.</span><span class="sxs-lookup"><span data-stu-id="2f174-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="2f174-116">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f174-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2f174-117">На верхней панели hello выберите вашу учетную запись.</span><span class="sxs-lookup"><span data-stu-id="2f174-117">On hello top bar, select your account.</span></span> <span data-ttu-id="2f174-118">Из hello **каталога** выберите клиента hello организации Azure AD, где требуется tooregister приложения (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="2f174-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="2f174-119">Выберите **больше услуг** в левой области hello и выполните поиск «Регистрации приложения».</span><span class="sxs-lookup"><span data-stu-id="2f174-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="2f174-120">Выберите **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="2f174-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="2f174-121">Введите значение имя для приложения (например, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="2f174-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="2f174-122">Выберите **веб-приложения и API** для типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2f174-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="2f174-123">Для **URL-адрес входа**, введите URL-адреса, hello где `yourtenant` заменяется именем hello вашего клиента Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="2f174-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="2f174-124">Сохранить код приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2f174-124">Save hello application ID.</span></span>
1. <span data-ttu-id="2f174-125">Выберите только что созданный hello приложение.</span><span class="sxs-lookup"><span data-stu-id="2f174-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="2f174-126">В разделе hello **параметры** колонке выберите **ключей**.</span><span class="sxs-lookup"><span data-stu-id="2f174-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="2f174-127">Создайте ключ и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="2f174-127">Create a new key, and save it.</span></span> <span data-ttu-id="2f174-128">Используется в hello действия, описанные в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="2f174-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="2f174-129">Добавление ключа tooAzure hello Azure AD AD B2C</span><span class="sxs-lookup"><span data-stu-id="2f174-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="2f174-130">Требуется ключ приложения contoso.com toostore hello в клиенте Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2f174-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="2f174-131">toodo это:</span><span class="sxs-lookup"><span data-stu-id="2f174-131">toodo this:</span></span>
1. <span data-ttu-id="2f174-132">Клиент Azure AD B2C tooyour перейдите и выберите **B2C параметры** > **Identity Framework качества** > **ключи политики**.</span><span class="sxs-lookup"><span data-stu-id="2f174-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="2f174-133">Щелкните **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2f174-133">Select **+Add**.</span></span>
1. <span data-ttu-id="2f174-134">Выберите или введите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="2f174-134">Select or enter these options:</span></span>
   * <span data-ttu-id="2f174-135">Выберите **Вручную**.</span><span class="sxs-lookup"><span data-stu-id="2f174-135">Select **Manual**.</span></span>
   * <span data-ttu-id="2f174-136">Для параметра **Имя** выберите имя, соответствующее имени клиента Azure AD (например, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="2f174-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="2f174-137">префикс Hello `B2C_1A_` автоматически добавляется toohello имя ключа.</span><span class="sxs-lookup"><span data-stu-id="2f174-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="2f174-138">Вставьте ключ приложения hello **секрет** поле.</span><span class="sxs-lookup"><span data-stu-id="2f174-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="2f174-139">Выберите **Подпись**.</span><span class="sxs-lookup"><span data-stu-id="2f174-139">Select **Signature**.</span></span>
1. <span data-ttu-id="2f174-140">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2f174-140">Select **Create**.</span></span>
1. <span data-ttu-id="2f174-141">Убедитесь, что вы создали ключ hello `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="2f174-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="2f174-142">Добавление поставщика утверждений в базовую политику</span><span class="sxs-lookup"><span data-stu-id="2f174-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="2f174-143">Если требуется в toosign пользователей с помощью Azure AD необходимо toodefine Azure AD в качестве поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="2f174-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="2f174-144">Другими словами необходимо toospecify конечную точку, которая будет взаимодействовать Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2f174-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="2f174-145">Конечная точка Hello предоставит набор утверждений, которые используются в Azure AD B2C tooverify проверку определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="2f174-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="2f174-146">Azure AD можно определить в качестве поставщика утверждений, добавив Azure AD toohello `<ClaimsProvider>` узла в файле расширения hello политики:</span><span class="sxs-lookup"><span data-stu-id="2f174-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="2f174-147">Откройте файл расширения hello (TrustFrameworkExtensions.xml) из рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="2f174-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="2f174-148">Найти hello `<ClaimsProviders>` раздела.</span><span class="sxs-lookup"><span data-stu-id="2f174-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="2f174-149">Если он не существует, добавьте его в корневом узле hello.</span><span class="sxs-lookup"><span data-stu-id="2f174-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="2f174-150">Добавьте новый `<ClaimsProvider>`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2f174-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="2f174-151">В разделе hello `<ClaimsProvider>` узел, значение hello обновления для `<Domain>` tooa уникальное значение, которое может быть используется toodistinguish его от других поставщиков удостоверений.</span><span class="sxs-lookup"><span data-stu-id="2f174-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="2f174-152">В разделе hello `<ClaimsProvider>` узел, значение hello обновления для `<DisplayName>` tooa понятное имя для hello поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="2f174-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="2f174-153">В настоящее время это значение не используется.</span><span class="sxs-lookup"><span data-stu-id="2f174-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="2f174-154">Обновление профиля технические hello</span><span class="sxs-lookup"><span data-stu-id="2f174-154">Update hello technical profile</span></span>

<span data-ttu-id="2f174-155">tooget токена из конечной точки Azure AD hello необходимо протоколы hello toodefine использование Azure AD B2C toocommunicate с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f174-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="2f174-156">Это выполняется внутри hello `<TechnicalProfile>` элемент `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="2f174-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="2f174-157">Обновить идентификатор hello hello `<TechnicalProfile>` узла.</span><span class="sxs-lookup"><span data-stu-id="2f174-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="2f174-158">Этот идентификатор является toothis используется toorefer технические профиль из других частей hello политики.</span><span class="sxs-lookup"><span data-stu-id="2f174-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="2f174-159">Измените значение в hello `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="2f174-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="2f174-160">Это значение будет отображаться hello вход кнопку на экране входа.</span><span class="sxs-lookup"><span data-stu-id="2f174-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="2f174-161">Измените значение в hello `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="2f174-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="2f174-162">Azure AD использует протокол OpenID Connect hello, поэтому убедитесь, это значение hello для `<Protocol>` — `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="2f174-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="2f174-163">Требуется tooupdate hello `<Metadata>` раздела hello XML-файл называется tooearlier tooreflect hello настройки для конкретных клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f174-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="2f174-164">В XML-файле hello обновите значения метаданных hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2f174-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="2f174-165">Задать `<Item Key="METADATA">` слишком`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, где `yourAzureADtenant` — это имя клиента Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="2f174-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="2f174-166">Откройте ваш браузер и перейдите toohello `METADATA` URL-адрес, который был обновлен.</span><span class="sxs-lookup"><span data-stu-id="2f174-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="2f174-167">В браузере hello поиска hello объекта «issuer» и скопируйте его значение.</span><span class="sxs-lookup"><span data-stu-id="2f174-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="2f174-168">Он должен выглядеть hello следующим образом: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="2f174-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="2f174-169">Вставьте значение hello `<Item Key="ProviderName">` hello XML-файл.</span><span class="sxs-lookup"><span data-stu-id="2f174-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="2f174-170">Задать `<Item Key="client_id">` toohello код приложения от регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2f174-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="2f174-171">Задать `<Item Key="IdTokenAudience">` toohello код приложения от регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2f174-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="2f174-172">Убедитесь, что `<Item Key="response_types">` задано слишком`id_token`.</span><span class="sxs-lookup"><span data-stu-id="2f174-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="2f174-173">Убедитесь, что `<Item Key="UsePolicyInRedirectUri">` задано слишком`false`.</span><span class="sxs-lookup"><span data-stu-id="2f174-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="2f174-174">Также необходим секретный hello Azure AD toolink, который зарегистрирован в вашей toohello клиента Azure AD B2C Azure AD `<ClaimsProvider>` сведения:</span><span class="sxs-lookup"><span data-stu-id="2f174-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="2f174-175">В hello `<CryptographicKeys>` раздела hello предшествующий XML-файл, измените значение в hello `StorageReferenceId` toohello идентификатор ссылки секрета hello, которое было определено (например, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="2f174-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="2f174-176">Отправить файл hello расширения для проверки</span><span class="sxs-lookup"><span data-stu-id="2f174-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="2f174-177">К этому моменту вы настроили политикой, чтобы Azure AD B2C известно как toocommunicate с каталогом Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f174-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="2f174-178">Попробуйте отправить файл расширения hello вашей tooconfirm только политики, нет ли проблем в данный момент.</span><span class="sxs-lookup"><span data-stu-id="2f174-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="2f174-179">toodo так:</span><span class="sxs-lookup"><span data-stu-id="2f174-179">toodo so:</span></span>

1. <span data-ttu-id="2f174-180">Откройте hello **все политики** колонки в клиенте Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2f174-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="2f174-181">Проверьте hello **перезаписать hello политики, если он существует** поле.</span><span class="sxs-lookup"><span data-stu-id="2f174-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="2f174-182">Отправить файл расширения hello (TrustFrameworkExtensions.xml) и что он не выдал hello проверки.</span><span class="sxs-lookup"><span data-stu-id="2f174-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="2f174-183">Регистрация пользователя hello Azure AD утверждений поставщика tooa пути</span><span class="sxs-lookup"><span data-stu-id="2f174-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="2f174-184">Необходимо tooone tooadd hello Azure AD identity поставщика для вашего пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="2f174-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="2f174-185">На этом этапе Настройка поставщика удостоверений hello, но он не доступен в любом hello регистрации-повышение/вход экранов.</span><span class="sxs-lookup"><span data-stu-id="2f174-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="2f174-186">toomake ее доступной, она будет создана копия существующего шаблона пути пользователя и затем изменить ее, чтобы он также поставщика удостоверений hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="2f174-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="2f174-187">Откройте файл базовый hello политики (например, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="2f174-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="2f174-188">Найти hello `<UserJourneys>` элемент и скопируйте hello всей `<UserJourney>` узел, который содержит `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="2f174-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="2f174-189">Откройте файл hello расширения (например, TrustFrameworkExtensions.xml) и найти hello `<UserJourneys>` элемента.</span><span class="sxs-lookup"><span data-stu-id="2f174-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="2f174-190">Если элемент hello не существует, добавьте его.</span><span class="sxs-lookup"><span data-stu-id="2f174-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="2f174-191">Вставить hello всей `<UserJourney>` узел, который вы скопировали как дочерний hello `<UserJourneys>` элемента.</span><span class="sxs-lookup"><span data-stu-id="2f174-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="2f174-192">Переименуйте идентификатор hello hello новый пользователь пути (например, переименуйте как `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="2f174-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="2f174-193">Экран приветствия «кнопка»</span><span class="sxs-lookup"><span data-stu-id="2f174-193">Display hello "button"</span></span>

<span data-ttu-id="2f174-194">Hello `<ClaimsProviderSelection>` элемент является аналогом tooan удостоверение поставщика кнопку на экране регистрации-повышение/вход.</span><span class="sxs-lookup"><span data-stu-id="2f174-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="2f174-195">При добавлении `<ClaimsProviderSelection>` элемент для Azure AD новая кнопка отображается, когда пользователь попадает на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="2f174-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="2f174-196">tooadd этого элемента:</span><span class="sxs-lookup"><span data-stu-id="2f174-196">tooadd this element:</span></span>

1. <span data-ttu-id="2f174-197">Найти hello `<OrchestrationStep>` узел, который содержит `Order="1"` в только что созданный пользователь путешествия hello.</span><span class="sxs-lookup"><span data-stu-id="2f174-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="2f174-198">Добавьте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="2f174-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="2f174-199">Задать `TargetClaimsExchangeId` tooan соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="2f174-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="2f174-200">Мы рекомендуем следующие hello же соглашениями, что и другие:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="2f174-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="2f174-201">Действие tooan кнопки ссылки hello</span><span class="sxs-lookup"><span data-stu-id="2f174-201">Link hello button tooan action</span></span>

<span data-ttu-id="2f174-202">Теперь, когда имеется кнопка на месте, необходимо toolink его tooan действие.</span><span class="sxs-lookup"><span data-stu-id="2f174-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="2f174-203">Действие Hello в этом случае является для Azure AD B2C toocommunicate с Azure AD tooreceive маркер.</span><span class="sxs-lookup"><span data-stu-id="2f174-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="2f174-204">Свяжите действие tooan кнопки hello, связывания hello технические профиля для поставщика утверждений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f174-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="2f174-205">Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.</span><span class="sxs-lookup"><span data-stu-id="2f174-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="2f174-206">Добавьте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="2f174-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="2f174-207">Обновление `Id` toohello одинаковое значение, что и `TargetClaimsExchangeId` в предшествующих раздел hello.</span><span class="sxs-lookup"><span data-stu-id="2f174-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="2f174-208">Обновление `TechnicalProfileReferenceId` toohello идентификатор hello технические профиля, созданную ранее (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="2f174-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="2f174-209">Отправка файла обновленного расширения hello</span><span class="sxs-lookup"><span data-stu-id="2f174-209">Upload hello updated extension file</span></span>

<span data-ttu-id="2f174-210">Изменение файла hello расширения завершено.</span><span class="sxs-lookup"><span data-stu-id="2f174-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="2f174-211">Сохраните его.</span><span class="sxs-lookup"><span data-stu-id="2f174-211">Save it.</span></span> <span data-ttu-id="2f174-212">Затем отправьте файл hello и убедитесь, что успешного выполнения всех проверок.</span><span class="sxs-lookup"><span data-stu-id="2f174-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="2f174-213">Обновить файл RP hello</span><span class="sxs-lookup"><span data-stu-id="2f174-213">Update hello RP file</span></span>

<span data-ttu-id="2f174-214">Требуется tooupdate hello проверяющей стороны (RP) файл, который будет инициировать только что созданный пользователь путешествия hello:</span><span class="sxs-lookup"><span data-stu-id="2f174-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="2f174-215">Создайте копию SignUpOrSignIn.xml в рабочий каталог и переименуйте его (например, переименуйте его tooSignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="2f174-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="2f174-216">Привет открыть новый файл и обновление hello `PolicyId` для атрибута `<TrustFrameworkPolicy>` с уникальным значением (например, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="2f174-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="2f174-217">Это будет имя hello политики (например, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="2f174-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="2f174-218">Изменение hello `ReferenceId` атрибута в `<DefaultUserJourney>` toomatch идентификатор hello hello пути нового пользователя, созданного (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="2f174-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="2f174-219">Сохранить изменения и отправить файл hello.</span><span class="sxs-lookup"><span data-stu-id="2f174-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2f174-220">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="2f174-220">Troubleshooting</span></span>

<span data-ttu-id="2f174-221">Тестирование hello пользовательскую политику, которая только что переданный, команду колонке **запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="2f174-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="2f174-222">Узнайте, как проблемы toodiagnose [Устранение неполадок](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2f174-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f174-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f174-223">Next steps</span></span>

<span data-ttu-id="2f174-224">Отправить отзыв слишком[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2f174-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
