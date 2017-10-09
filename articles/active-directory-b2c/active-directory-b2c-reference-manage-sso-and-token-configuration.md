---
title: "Azure Active Directory B2C. Управление SSO и настройкой токенов с помощью пользовательских политик | Документация Майкрософт"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="a64aa-102">Azure Active Directory B2C. Управление SSO и настройкой токенов с помощью пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="a64aa-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="a64aa-103">Использование пользовательских политик предоставляет hello же контроль над маркером, сеанса и единого входа (SSO) конфигураций, через встроенных политик.</span><span class="sxs-lookup"><span data-stu-id="a64aa-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="a64aa-104">toolearn каждого параметра так, см. в разделе документации hello [здесь](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="a64aa-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="a64aa-105">Конфигурация времени существования токенов и утверждений</span><span class="sxs-lookup"><span data-stu-id="a64aa-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="a64aa-106">Параметры hello toochange на ваш времени жизни токенов, необходимо tooadd `<ClaimsProviders>` элемент в файле проверяющей стороной hello hello политики требуется tooimpact.</span><span class="sxs-lookup"><span data-stu-id="a64aa-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="a64aa-107">Hello `<ClaimsProviders>` элемент является дочерним hello `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="a64aa-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="a64aa-108">Внутри сведения понадобятся вам tooput hello, влияющий на времени жизни токенов.</span><span class="sxs-lookup"><span data-stu-id="a64aa-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="a64aa-109">Hello XML выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a64aa-109">hello XML looks like this:</span></span>

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

<span data-ttu-id="a64aa-110">**Доступ к времени жизни токенов** hello доступа, время существования маркера можно изменить, изменив значение hello внутри hello `<Item>` с hello ключ = «token_lifetime_secs» в секундах.</span><span class="sxs-lookup"><span data-stu-id="a64aa-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="a64aa-111">значение по умолчанию Hello в встроенные — 3 600 секунд (60 минут).</span><span class="sxs-lookup"><span data-stu-id="a64aa-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="a64aa-112">**Время существования маркера идентификатор** время существования маркера идентификатор hello можно изменить, изменив значение hello внутри hello `<Item>` с hello ключ = «id_token_lifetime_secs» в секундах.</span><span class="sxs-lookup"><span data-stu-id="a64aa-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="a64aa-113">значение по умолчанию Hello в встроенные — 3 600 секунд (60 минут).</span><span class="sxs-lookup"><span data-stu-id="a64aa-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="a64aa-114">**Обновить время существования маркера** hello время существования маркера обновления можно изменить, изменив значение hello внутри hello `<Item>` с hello ключ = «refresh_token_lifetime_secs» в секундах.</span><span class="sxs-lookup"><span data-stu-id="a64aa-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="a64aa-115">значение по умолчанию Hello в встроенные — 1209600 секунд (14 дней).</span><span class="sxs-lookup"><span data-stu-id="a64aa-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="a64aa-116">**Обновить время существования маркера скользящее окно** при желании tooset токен обновления времени существования tooyour скользящее окно изменить значение hello внутри `<Item>` с hello ключ = «rolling_refresh_token_lifetime_secs» в секундах.</span><span class="sxs-lookup"><span data-stu-id="a64aa-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="a64aa-117">значение по умолчанию Hello в встроенные — 7776000 (90 дней).</span><span class="sxs-lookup"><span data-stu-id="a64aa-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="a64aa-118">Если вы не хотите tooenfore скользящее окно времени существования, замените эту строку с:</span><span class="sxs-lookup"><span data-stu-id="a64aa-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="a64aa-119">**Утверждение издателя (iss)** toochange hello (iss) издателя утверждения, измените значение hello внутри hello `<Item>` с hello Key = «IssuanceClaimPattern».</span><span class="sxs-lookup"><span data-stu-id="a64aa-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="a64aa-120">применимые значения Hello `AuthorityAndTenantGuid` и `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="a64aa-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="a64aa-121">**Параметр утверждения, представляющий идентификатор политики** hello параметры для данного параметра не TFP (политики доверия framework) и контроля доступа (Справочник по контекст проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="a64aa-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="a64aa-122">Мы рекомендуем этот tooTFP toodo Установка этого параметра, убедитесь, hello `<Item>` с hello Key = «AuthenticationContextReferenceClaimPattern» существует и имеет значение hello `None`.</span><span class="sxs-lookup"><span data-stu-id="a64aa-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="a64aa-123">Добавьте этот элемент в элемент `<OutputClaims>`:</span><span class="sxs-lookup"><span data-stu-id="a64aa-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="a64aa-124">Для управления Доступом, удалите hello `<Item>` с hello Key = «AuthenticationContextReferenceClaimPattern».</span><span class="sxs-lookup"><span data-stu-id="a64aa-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="a64aa-125">**Утверждение темы (sub)** этот параметр по умолчанию tooObjectID, если вы хотите tooswitch это слишком`Not Supported`, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a64aa-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="a64aa-126">Замените эту строку:</span><span class="sxs-lookup"><span data-stu-id="a64aa-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="a64aa-127">на следующую:</span><span class="sxs-lookup"><span data-stu-id="a64aa-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="a64aa-128">Режим работы сеанса и SSO</span><span class="sxs-lookup"><span data-stu-id="a64aa-128">Session behavior and SSO</span></span>
<span data-ttu-id="a64aa-129">toochange вашей поведение сеанса и конфигурации единого входа, необходимо tooadd `<UserJourneyBehaviors>` элемент внутри hello `<RelyingParty>` элемента.</span><span class="sxs-lookup"><span data-stu-id="a64aa-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="a64aa-130">Hello `<UserJourneyBehaviors>` элемент должен следовать непосредственно за hello `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="a64aa-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="a64aa-131">Здравствуйте, внутри вашей `<UserJourneyBehavors>` элемент должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a64aa-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="a64aa-132">**Настройка единого входа (SSO)** toochange hello единого входа для конфигурации, требуется значение hello toomodify `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="a64aa-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="a64aa-133">применимые значения Hello `Tenant`, `Application`, `Policy` и `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="a64aa-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="a64aa-134">**Веб-приложение, время жизни сеанса (в минутах)** toochange hello hello веб-приложения время жизни сеанса, необходимо получить значение toomodify из hello `<SessionExpiryInSeconds>` элемента.</span><span class="sxs-lookup"><span data-stu-id="a64aa-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="a64aa-135">значение по умолчанию Hello в встроенных политик — 86400 секунд (1 440 минут).</span><span class="sxs-lookup"><span data-stu-id="a64aa-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="a64aa-136">**Время ожидания сеанса приложения Web** toochange hello web app время ожидания сеанса, необходимо значение hello toomodify `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="a64aa-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="a64aa-137">применимые значения Hello `Absolute` и `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="a64aa-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
