---
title: "Azure Active Directory B2C. Изменение регистрации в пользовательских политиках и настройка самоподтвержденного поставщика"
description: "Пошаговое руководство по добавлению утверждений toosign вверх и настройте hello ввод данных пользователем"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="3cbb6-103">Azure Active Directory B2C: Изменить регистрации новых утверждений tooadd и настроить ввод данных пользователем.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="3cbb6-104">В этой статье вы добавите новые пути пользователя tooyour запись (утверждения) предоставленные пользователем при регистрации.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="3cbb6-105">Будет настроить запись hello как раскрывающийся список и определить, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="3cbb6-106">Редактировать перемещение Sipi tootrigger тестирования вручную.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cbb6-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3cbb6-107">Prerequisites</span></span>

* <span data-ttu-id="3cbb6-108">Hello завершения действия в статье hello [Приступая к работе с пользовательских политик](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="3cbb6-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="3cbb6-109">Протестируйте toosignup пути при регистрации или входа пользователя hello новую локальную учетную запись, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="3cbb6-110">Сбор исходных данных от пользователей осуществляется при регистрации или входе.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="3cbb6-111">Дополнительные утверждения можно собрать позже при изменении профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="3cbb6-112">Каждый раз, когда Azure AD B2C собирает информацию непосредственно из hello пользователю интерактивно, hello использует возможности платформы идентификации его `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="3cbb6-113">Hello шаги применяются каждый раз, когда используется этот поставщик.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="3cbb6-114">Определения утверждений hello, его отображаемое имя и hello тип вводимых пользователем данных</span><span class="sxs-lookup"><span data-stu-id="3cbb6-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="3cbb6-115">Позволяет запрашивать пользователя hello для их города.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="3cbb6-116">Добавьте следующий элемент toohello hello `<ClaimsSchema>` элемент в файл политики TrustFrameWorkExtensions hello:</span><span class="sxs-lookup"><span data-stu-id="3cbb6-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="3cbb6-117">Существуют дополнительные параметры, которые можно здесь выбрать hello toocustomize утверждения.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="3cbb6-118">Полную схему, см. в разделе toohello **удостоверения качества Framework технических руководство**.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="3cbb6-119">В этом руководстве будут опубликованы в ближайшее время в справочном разделе hello.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="3cbb6-120">`<DisplayName>`является строкой, которая определяет пользовательского интерфейса hello *метки*</span><span class="sxs-lookup"><span data-stu-id="3cbb6-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="3cbb6-121">`<UserHelpText>`помогает понять требования пользователей hello</span><span class="sxs-lookup"><span data-stu-id="3cbb6-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="3cbb6-122">`<UserInputType>`hello следующие четыре варианта выделены ниже:</span><span class="sxs-lookup"><span data-stu-id="3cbb6-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="3cbb6-123">`RadioSingleSelectduration` предоставляет один элемент на выбор.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * <span data-ttu-id="3cbb6-124">`DropdownSingleSelect`-Выбор hello только допустимое значение.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

![Снимок экрана с раскрывающимся списком](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* <span data-ttu-id="3cbb6-126">`CheckboxMultiSelect`Разрешает выбор hello одно или несколько значений.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

![Снимок экрана с вариантом множественного выбора](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="3cbb6-128">Добавить hello утверждения toohello входа вверх/знак в пути пользователя</span><span class="sxs-lookup"><span data-stu-id="3cbb6-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="3cbb6-129">Добавьте утверждение, hello `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (см. в файле политики TrustFrameworkBase hello).</span><span class="sxs-lookup"><span data-stu-id="3cbb6-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="3cbb6-130">Обратите внимание, что это TechnicalProfile использует hello SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, toobe collected from hello user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. <span data-ttu-id="3cbb6-131">Добавление утверждений hello toohello AAD UserWriteUsingLogonEmail как `<PersistedClaim ClaimTypeReferenceId="city" />` каталога AAD toohello утверждения hello toowrite после сбор hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="3cbb6-132">Если вы предпочитаете не toopersist hello утверждения в каталоге hello для использования в будущем, можно пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. <span data-ttu-id="3cbb6-133">Добавление утверждений hello toohello TechnicalProfile, который считывает данные из каталога hello при входе пользователя качестве`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="3cbb6-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. <span data-ttu-id="3cbb6-134">Добавить hello `<OutputClaim ClaimTypeReferenceId="city" />` файл политики RP toohello SignUporSignIn.xml таким образом, это утверждение будет отправлено toohello приложения hello токен после пути успешная пользователя.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="3cbb6-135">Тестирование настраиваемой политики hello, с помощью «Немедленном запуске»</span><span class="sxs-lookup"><span data-stu-id="3cbb6-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="3cbb6-136">Откройте hello **колонке Azure AD B2C** и перейдите в слишком**Identity Framework качества > пользовательских политик**.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="3cbb6-137">Выберите настраиваемую политику hello, загруженный и нажмите кнопку hello **запустить сейчас** кнопки.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="3cbb6-138">Должно быть toosign доступ с помощью адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="3cbb6-139">экран регистрации Hello в тестовом режиме должен выглядеть примерно toothis:</span><span class="sxs-lookup"><span data-stu-id="3cbb6-139">hello signup screen in test mode should look similar toothis:</span></span>

![Снимок экрана с измененным вариантом регистрации](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="3cbb6-141">Hello маркера задней tooyour приложения будут включать hello `city` утверждения, как показано ниже</span><span class="sxs-lookup"><span data-stu-id="3cbb6-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="3cbb6-142">Удаление проверки по электронной почте из процесса регистрации (необязательно)</span><span class="sxs-lookup"><span data-stu-id="3cbb6-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="3cbb6-143">tooskip проверки адреса электронной почты, hello политики автор может выбрать tooremove `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="3cbb6-144">Hello адрес электронной почты будет требуется, но не прошли проверку, если «Требуется» = true удаляется.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="3cbb6-145">Подумайте, подходит ли этот вариант в вашем случае.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="3cbb6-146">Проверить, включена поддержка электронной почты по умолчанию в hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` в файле политики TrustFrameworkBase hello в пакете начального приветствия:</span><span class="sxs-lookup"><span data-stu-id="3cbb6-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="3cbb6-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3cbb6-147">Next steps</span></span>

<span data-ttu-id="3cbb6-148">Добавьте новые потоки toohello утверждения hello для социальных сетей учетных записей входа, изменив приветствия TechnicalProfiles перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="3cbb6-149">Это используемые toowrite входа социального/федеративной учетной записи и чтения hello пользовательских данных с помощью hello alternativeSecurityId как hello локатора.</span><span class="sxs-lookup"><span data-stu-id="3cbb6-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
