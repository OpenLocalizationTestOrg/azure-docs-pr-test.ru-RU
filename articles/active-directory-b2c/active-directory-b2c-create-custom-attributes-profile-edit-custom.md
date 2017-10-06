---
title: "Azure Active Directory B2C: Добавить собственные политики toocustom атрибуты и использовать редактирования профиля | Документы Microsoft"
description: "Пошаговое руководство по использованию свойства расширения, настраиваемые атрибуты и включить их в пользовательском интерфейсе hello"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="6e002-103">Azure Active Directory B2C. Создание и использование настраиваемых атрибутов в пользовательской политике изменения профиля</span><span class="sxs-lookup"><span data-stu-id="6e002-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="6e002-104">В этой статье создайте настраиваемый атрибут в вашем каталоге Azure AD B2C и использовать этот новый атрибут в качестве пользовательского утверждения в пути пользователя изменить профиль hello.</span><span class="sxs-lookup"><span data-stu-id="6e002-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e002-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6e002-105">Prerequisites</span></span>

<span data-ttu-id="6e002-106">Hello завершения действия в статье hello [Приступая к работе с пользовательских политик](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6e002-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="6e002-107">Используйте настраиваемые атрибуты toocollect сведения о клиентах в Azure Active Directory B2C использование пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="6e002-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="6e002-108">Каталог Azure Active Directory (Azure AD) B2C поставляется со встроенным набором атрибутов: Given Name, Surname, City, Postal Code, userPrincipalName и т. д.  Часто требуется toocreate собственные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="6e002-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="6e002-109">Например:</span><span class="sxs-lookup"><span data-stu-id="6e002-109">For example:</span></span>
* <span data-ttu-id="6e002-110">В приложении с клиентом требуются toopersist атрибут, например «LoyaltyNumber.»</span><span class="sxs-lookup"><span data-stu-id="6e002-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="6e002-111">Поставщик удостоверений имеет уникальный идентификатор пользователя, который необходимо сохранить, например uniqueUserGUID.</span><span class="sxs-lookup"><span data-stu-id="6e002-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="6e002-112">Пути пользовательского должен toopersist hello состояние пользователя, например «migrationStatus.»</span><span class="sxs-lookup"><span data-stu-id="6e002-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="6e002-113">С помощью Azure AD B2C можно расширить hello набор атрибутов, хранящихся на каждой учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="6e002-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="6e002-114">Можно также чтение и запись данных атрибутов с помощью hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6e002-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="6e002-115">Свойства расширения расширить схему hello hello пользовательских объектов в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="6e002-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="6e002-116">свойство расширения условия Hello, настраиваемых атрибутов и пользовательских утверждений см. toohello, же в контексте hello этой статьи и hello имя изменяется в зависимости от контекста hello (приложения, объект, политики).</span><span class="sxs-lookup"><span data-stu-id="6e002-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="6e002-117">Свойства расширения можно зарегистрировать только в объекте приложения, даже если они содержат данные для пользователя.</span><span class="sxs-lookup"><span data-stu-id="6e002-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="6e002-118">Hello свойство вложенного toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="6e002-118">hello property is attached toohello application.</span></span> <span data-ttu-id="6e002-119">объект приложения Hello должен быть предоставленный доступ на запись tooregister свойства расширения.</span><span class="sxs-lookup"><span data-stu-id="6e002-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="6e002-120">100 свойства расширения (для всех типов и всех приложений) могут быть записаны tooany один объект.</span><span class="sxs-lookup"><span data-stu-id="6e002-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="6e002-121">Свойства расширения добавляются toohello тип целевого каталога и сразу становится доступным в клиенте каталога Azure AD B2C hello.</span><span class="sxs-lookup"><span data-stu-id="6e002-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="6e002-122">При удалении приложения hello, эти свойства расширения, а также данные, содержащиеся в них для всех пользователей также удаляются.</span><span class="sxs-lookup"><span data-stu-id="6e002-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="6e002-123">Если свойство расширения удаляется с hello приложения, оно будет удалено на hello целевые объекты каталога, а hello значения удалены.</span><span class="sxs-lookup"><span data-stu-id="6e002-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="6e002-124">Свойства расширения существуют только в контексте hello зарегистрированного приложения в клиенте hello.</span><span class="sxs-lookup"><span data-stu-id="6e002-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="6e002-125">Идентификатор объекта Hello этого приложения должны быть включены в hello TechnicalProfile, использующих его.</span><span class="sxs-lookup"><span data-stu-id="6e002-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="6e002-126">каталог Azure AD B2C Hello обычно включает веб-приложения с именем `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="6e002-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="6e002-127">Это приложение главным образом используется hello b2c встроенных политик для пользовательских утверждений hello, созданные с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6e002-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="6e002-128">С помощью этого расширения tooregister приложений для пользовательских политик b2c рекомендуется для опытных пользователей.</span><span class="sxs-lookup"><span data-stu-id="6e002-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="6e002-129">Инструкции, включаются в hello раздел следующие шаги в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6e002-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="6e002-130">Создание нового toostore приложения hello расширение свойств</span><span class="sxs-lookup"><span data-stu-id="6e002-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="6e002-131">Откройте сеанс браузера и перейдите toohello [Azure портальных](https://portal.azure.com) и выполните вход с учетными данными администратора hello нужно tooconfigure каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="6e002-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="6e002-132">Нажмите кнопку **Azure Active Directory** hello меню навигации слева.</span><span class="sxs-lookup"><span data-stu-id="6e002-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="6e002-133">Может потребоваться его, выбрав более служб toofind >.</span><span class="sxs-lookup"><span data-stu-id="6e002-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="6e002-134">Щелкните **Регистрация приложений** и выберите пункт **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="6e002-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="6e002-135">Предоставляют следующие hello рекомендуется записей:</span><span class="sxs-lookup"><span data-stu-id="6e002-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="6e002-136">Укажите имя для веб-приложения hello: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="6e002-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="6e002-137">Тип приложения: веб-приложение или API.</span><span class="sxs-lookup"><span data-stu-id="6e002-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="6e002-138">URL-адрес входа: https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions.</span><span class="sxs-lookup"><span data-stu-id="6e002-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="6e002-139">Выберите "Создать".</span><span class="sxs-lookup"><span data-stu-id="6e002-139">Select **Create.</span></span> <span data-ttu-id="6e002-140">Успешное завершение отображается в hello **уведомления**</span><span class="sxs-lookup"><span data-stu-id="6e002-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="6e002-141">Выберите только что созданный hello веб-приложение: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="6e002-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="6e002-142">Выберите параметры: **Необходимые разрешения**</span><span class="sxs-lookup"><span data-stu-id="6e002-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="6e002-143">Выберите API: **Windows Active Directory**</span><span class="sxs-lookup"><span data-stu-id="6e002-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="6e002-144">Установите флажки в разделе "Разрешения приложения": **Чтение и запись данных каталога** и **Сохранение**</span><span class="sxs-lookup"><span data-stu-id="6e002-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="6e002-145">Выберите команду **Предоставить разрешения** и нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="6e002-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="6e002-146">Буфер обмена tooyour скопировать и сохранить следующие идентификаторы из WebApp-GraphAPI-DirectoryExtensions hello > Параметры > Свойства ></span><span class="sxs-lookup"><span data-stu-id="6e002-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="6e002-147">**Идентификатор приложения**.</span><span class="sxs-lookup"><span data-stu-id="6e002-147">**Application ID** .</span></span> <span data-ttu-id="6e002-148">Пример: `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="6e002-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="6e002-149">**Идентификатор объекта**.</span><span class="sxs-lookup"><span data-stu-id="6e002-149">**Object ID**.</span></span> <span data-ttu-id="6e002-150">Пример: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="6e002-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="6e002-151">Изменение вашей настраиваемой политики tooadd hello ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="6e002-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
><span data-ttu-id="6e002-152">Hello <TechnicalProfile Id="AAD-Common"> является ссылка tooas «Общие», поскольку его элементы включаются в и повторно использовать в все hello Azure Active Directory TechnicalProfiles при помощи элемента hello:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="6e002-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="6e002-153">При hello TechnicalProfile записывает для первого свойства в расширение времени toohello только что созданный hello, могут возникнуть одноразовый ошибки.</span><span class="sxs-lookup"><span data-stu-id="6e002-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="6e002-154">свойства расширения Hello создается hello первый раз, в которой он используется.</span><span class="sxs-lookup"><span data-stu-id="6e002-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="6e002-155">С помощью нового свойства расширения hello / настраиваемый атрибут в пути пользователя</span><span class="sxs-lookup"><span data-stu-id="6e002-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="6e002-156">Откройте hello проверяющей Party(RP) файл, который описывает политикой изменение пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="6e002-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="6e002-157">При запуске, возможно, рекомендуется toodownload, уже настроенные версии hello RP PolicyEdit файл непосредственно из hello Azure B2C настраиваемой политики раздела hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6e002-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="6e002-158">Вы также можете открыть XML-файл из папки хранилища.</span><span class="sxs-lookup"><span data-stu-id="6e002-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="6e002-159">Добавьте пользовательское утверждение `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="6e002-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="6e002-160">Включая hello пользовательских утверждений в hello `<RelyingParty>` элемент, он передается в качестве параметра toohello UserJourney TechnicalProfiles и состава hello маркер для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6e002-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. <span data-ttu-id="6e002-161">Добавьте файл расширения политики утверждений определения toohello `TrustFrameworkExtensions.xml` внутри hello `<ClaimsSchema>` элемента, как показано.</span><span class="sxs-lookup"><span data-stu-id="6e002-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. <span data-ttu-id="6e002-162">Добавить hello же утверждения политики базовый файл определения toohello `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="6e002-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="6e002-163">Добавление `ClaimType` определение в hello base и hello расширения файла не обычно требуется, однако поскольку hello дальнейшие действия добавит hello extension_loyaltyId tooTechnicalProfiles в базовом файле hello, проверяющий элемент управления политики hello отклонит передачи hello hello основного файла без него.</span><span class="sxs-lookup"><span data-stu-id="6e002-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="6e002-164">Может оказаться полезным tootrace выполнение hello hello пути пользователя, с именем «ProfileEdit» в файле TrustFrameworkBase.xml hello.</span><span class="sxs-lookup"><span data-stu-id="6e002-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="6e002-165">Поиск пользователя позволят hello hello таким же именем в редакторе и обратите внимание, что шаг 5 Orchestration вызывает hello TechnicalProfileReferenceID = «SelfAsserted ProfileUpdate».</span><span class="sxs-lookup"><span data-stu-id="6e002-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="6e002-166">Поиск и проверить этот toofamiliarize TechnicalProfile самостоятельно с потоком hello.</span><span class="sxs-lookup"><span data-stu-id="6e002-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="6e002-167">Добавить loyaltyId как входной и выходной утверждений в hello TechnicalProfile «SelfAsserted ProfileUpdate»</span><span class="sxs-lookup"><span data-stu-id="6e002-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="6e002-168">Добавление утверждения в TechnicalProfile «AAD UserWriteProfileUsingObjectId» toopersist hello значение утверждения hello в свойство расширения hello, для hello текущего пользователя в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="6e002-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. <span data-ttu-id="6e002-169">Добавление утверждения в TechnicalProfile «AAD UserReadUsingObjectId» tooread hello значение атрибута расширения hello, каждый раз, когда пользователь входит в.</span><span class="sxs-lookup"><span data-stu-id="6e002-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="6e002-170">До сих hello TechnicalProfiles были изменены в потоке hello локальных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="6e002-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="6e002-171">При желании hello новый атрибут потока hello социального/федеративной учетной записи другой набор TechnicalProfiles должен toobe изменен.</span><span class="sxs-lookup"><span data-stu-id="6e002-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="6e002-172">Ознакомьтесь с разделом "Дальнейшие действия".</span><span class="sxs-lookup"><span data-stu-id="6e002-172">See Next Steps.</span></span>

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
><span data-ttu-id="6e002-173">элемент IncludeTechnicalProfile Hello добавляет все элементы hello общие AAD toothis TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="6e002-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="6e002-174">Тестирование настраиваемой политики hello, с помощью «Немедленном запуске»</span><span class="sxs-lookup"><span data-stu-id="6e002-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="6e002-175">Откройте hello **колонке Azure AD B2C** и перейдите в слишком**Identity Framework качества > пользовательских политик**.</span><span class="sxs-lookup"><span data-stu-id="6e002-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="6e002-176">Выберите настраиваемую политику hello, загруженный и нажмите кнопку hello **запустить сейчас** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6e002-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="6e002-177">Должно быть toosign доступ с помощью адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="6e002-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="6e002-178">маркер идентификатора Hello отправлено обратно tooyour приложение включает hello нового свойства расширения как предшествует extension_loyaltyId пользовательского утверждения.</span><span class="sxs-lookup"><span data-stu-id="6e002-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="6e002-179">Ознакомьтесь с примером ниже.</span><span class="sxs-lookup"><span data-stu-id="6e002-179">See example.</span></span>

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="6e002-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e002-180">Next steps</span></span>

<span data-ttu-id="6e002-181">Добавьте новые потоки toohello утверждения hello для социальных сетей учетных записей входа, изменив приветствия TechnicalProfiles в списке.</span><span class="sxs-lookup"><span data-stu-id="6e002-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="6e002-182">Эти два TechnicalProfiles используются с toowrite входа социального/федеративной учетной записи и чтения hello пользовательских данных с помощью hello alternativeSecurityId как hello локатора hello объекта пользователя.</span><span class="sxs-lookup"><span data-stu-id="6e002-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="6e002-183">С помощью hello одинаковые атрибуты расширения между встроенные и пользовательские политики.</span><span class="sxs-lookup"><span data-stu-id="6e002-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="6e002-184">При добавлении атрибутов расширения (также называемого настраиваемые атрибуты) через взаимодействие с порталом hello те атрибуты, регистрируются с использованием hello ** b2c-расширений приложение, которое существует в каждый клиент b2c.</span><span class="sxs-lookup"><span data-stu-id="6e002-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="6e002-185">toouse эти атрибуты расширения в пользовательскую политику:</span><span class="sxs-lookup"><span data-stu-id="6e002-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="6e002-186">К клиенту b2c portal.azure.com, переход в слишком**Azure Active Directory** и выберите **регистрации приложения**</span><span class="sxs-lookup"><span data-stu-id="6e002-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="6e002-187">Найдите свое приложение **b2c-extensions-app** и выберите его.</span><span class="sxs-lookup"><span data-stu-id="6e002-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="6e002-188">В разделе «Основы» hello записи **идентификатор приложения** и hello **идентификатор объекта**</span><span class="sxs-lookup"><span data-stu-id="6e002-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="6e002-189">Добавьте их в метаданные технического профиля AAD-Common следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6e002-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="6e002-190">tookeep согласованности hello портала процесс, создайте эти атрибуты с помощью портала hello пользовательского интерфейса *перед* использовать их в пользовательских политик.</span><span class="sxs-lookup"><span data-stu-id="6e002-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="6e002-191">При создании атрибута «ActivationStatus» на портале hello, должны ссылаться tooit следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6e002-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="6e002-192">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="6e002-192">Reference</span></span>

* <span data-ttu-id="6e002-193">Объект **технические профиля (TP)** — это тип элемента, можно рассматривать как *функция* , определяющий имя конечной точки, ее метаданные, его протокол и сведения hello exchange утверждений, которые hello удостоверений Взаимодействие с Framework должна быть выполнена.</span><span class="sxs-lookup"><span data-stu-id="6e002-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="6e002-194">Если это *функция* вызывается orchestration шаг или из другой TechnicalProfile, hello InputClaims и OutputClaims предоставляются как параметры hello вызывающим объектом.</span><span class="sxs-lookup"><span data-stu-id="6e002-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="6e002-195">Полный список свойств расширений в статье hello [расширения СХЕМЫ КАТАЛОГОВ | ОСНОВНЫЕ ПОНЯТИЯ API GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="6e002-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="6e002-196">Расширения атрибутов в Graph API именуются с использованием соглашения о hello `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="6e002-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="6e002-197">Настраиваемые политики называем атрибуты tooextensions extension_attributename, тем самым исключая hello ApplicationObjectId в hello XML</span><span class="sxs-lookup"><span data-stu-id="6e002-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
