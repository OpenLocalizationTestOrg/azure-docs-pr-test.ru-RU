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
ms.openlocfilehash: 8f5703d15766f221517cd89352d41685652d32d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="9a4ee-102">Azure Active Directory B2C. Управление SSO и настройкой токенов с помощью пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="9a4ee-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="9a4ee-103">Использование пользовательских политик предоставляет тот же контроль над конфигурациями токена, сеанса и единого входа, что и при использовании встроенных политик.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-103">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="9a4ee-104">Ознакомиться с функциями каждого параметра вы можете в [этом руководстве](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="9a4ee-104">To learn what each setting does, please see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="9a4ee-105">Конфигурация времени существования токенов и утверждений</span><span class="sxs-lookup"><span data-stu-id="9a4ee-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="9a4ee-106">Чтобы изменить настройки времени существования токенов, вам необходимо добавить элемент `<ClaimsProviders>` в файл проверяющей стороны политики, которую следует изменить.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-106">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="9a4ee-107">Элемент `<ClaimsProviders>` является дочерним элементом `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-107">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="9a4ee-108">Внутри необходимо разместить сведения, влияющие на время существования токенов.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-108">Inside you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="9a4ee-109">Код XML будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="9a4ee-109">The XML looks like this:</span></span>

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

<span data-ttu-id="9a4ee-110">**Время существования маркера доступа.** Время существования маркера доступа можно изменить, изменив значение внутри `<Item>`, используя Key="token_lifetime_secs" в качестве значения времени в секундах.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-110">**Access token lifetimes** The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="9a4ee-111">Значение по умолчанию во встроенных политиках составляет 3600 секунд (60 минут).</span><span class="sxs-lookup"><span data-stu-id="9a4ee-111">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="9a4ee-112">**Время существования токена идентификатора.** Время существования токена идентификатора можно изменить, изменив значение внутри `<Item>`, используя Key="token_lifetime_secs" в качестве значения времени в секундах.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-112">**ID token lifetime** The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="9a4ee-113">Значение по умолчанию во встроенных политиках составляет 3600 секунд (60 минут).</span><span class="sxs-lookup"><span data-stu-id="9a4ee-113">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="9a4ee-114">**Время существования токена обновления.** Время существования токена обновления можно изменить, изменив значение внутри `<Item>`, используя Key="token_lifetime_secs" в качестве значения времени в секундах.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-114">**Refresh token lifetime** The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="9a4ee-115">Значение по умолчанию во встроенных политиках составляет 1 209 600 секунд (14 дней).</span><span class="sxs-lookup"><span data-stu-id="9a4ee-115">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="9a4ee-116">**Время существования скользящего окна токена обновления.** Если вы хотите настроить время существования скользящего окна для токена обновления, измените значение внутри `<Item>`, используя Key="token_lifetime_secs" в качестве значения времени в секундах.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-116">**Refresh token sliding window lifetime** If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="9a4ee-117">Значение по умолчанию во встроенных политиках составляет 7 776 000 секунд (90 дней).</span><span class="sxs-lookup"><span data-stu-id="9a4ee-117">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="9a4ee-118">Если вы не хотите задавать определенное время существования скользящего окна, замените эту строку следующей:</span><span class="sxs-lookup"><span data-stu-id="9a4ee-118">If you don't want to enfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="9a4ee-119">**Утверждение издателя (iss).** Если вы хотите изменить утверждение издателя (iss), измените значение внутри `<Item>`, используя Key="IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="9a4ee-119">**Issuer (iss) claim** If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="9a4ee-120">Применимые значения — `AuthorityAndTenantGuid` и `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-120">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="9a4ee-121">**Утверждение настройки, представляющее идентификатор политики.** Параметры, использующиеся для настройки этого значения, — TFP (инфраструктура доверия) и ACR (ссылка на контекст проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="9a4ee-121">**Setting claim representing policy ID** The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="9a4ee-122">Мы рекомендуем задать значение TFP. Для этого должны существовать `<Item>` с Key="AuthenticationContextReferenceClaimPattern", а установленное значение должно быть `None`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-122">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="9a4ee-123">Добавьте этот элемент в элемент `<OutputClaims>`:</span><span class="sxs-lookup"><span data-stu-id="9a4ee-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="9a4ee-124">Чтобы использовать ACR, удалите `<Item>` со значением Key="AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="9a4ee-124">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="9a4ee-125">**Утверждение субъекта (sub).** По умолчанию для этого параметра задано значение ObjectID. Если вы хотите установить значение `Not Supported`, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9a4ee-125">**Subject (sub) claim** This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="9a4ee-126">Замените эту строку:</span><span class="sxs-lookup"><span data-stu-id="9a4ee-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="9a4ee-127">на следующую:</span><span class="sxs-lookup"><span data-stu-id="9a4ee-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="9a4ee-128">Режим работы сеанса и SSO</span><span class="sxs-lookup"><span data-stu-id="9a4ee-128">Session behavior and SSO</span></span>
<span data-ttu-id="9a4ee-129">Чтобы изменить конфигурации режима работы сеанса и SSO, вам необходимо добавить элемент `<UserJourneyBehaviors>` в элемент `<RelyingParty>`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-129">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="9a4ee-130">Элемент `<UserJourneyBehaviors>` должен сразу же следовать за элементом `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-130">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="9a4ee-131">Содержимое элемента `<UserJourneyBehavors>` должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9a4ee-131">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="9a4ee-132">**Конфигурация единого входа (SSO).** Чтобы изменить конфигурацию единого входа, вам необходимо изменить значение `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-132">**Single sign-on (SSO) configuration** To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="9a4ee-133">Применимые значения — `Tenant`, `Application`, `Policy` и `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-133">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="9a4ee-134">**Время существования сеанса веб-приложения (в минутах).** Чтобы изменить время существования сеанса веб-приложения, вам необходимо изменить значение элемента `<SessionExpiryInSeconds>`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-134">**Web app session lifetime (minutes)** To change the the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="9a4ee-135">Значение по умолчанию во встроенных политиках составляет 86 400 секунд (1440 минут).</span><span class="sxs-lookup"><span data-stu-id="9a4ee-135">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="9a4ee-136">**Время ожидания сеанса веб-приложения.** Чтобы изменить время ожидания сеанса веб-приложения, вам необходимо изменить значение `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-136">**Web app session timeout** To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="9a4ee-137">Применимые значения — `Absolute` и `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="9a4ee-137">The applicable values are `Absolute` and `Rolling`.</span></span>
