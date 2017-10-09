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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C. Управление SSO и настройкой токенов с помощью пользовательских политик
Использование пользовательских политик предоставляет hello же контроль над маркером, сеанса и единого входа (SSO) конфигураций, через встроенных политик.  toolearn каждого параметра так, см. в разделе документации hello [здесь](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Конфигурация времени существования токенов и утверждений
Параметры hello toochange на ваш времени жизни токенов, необходимо tooadd `<ClaimsProviders>` элемент в файле проверяющей стороной hello hello политики требуется tooimpact.  Hello `<ClaimsProviders>` элемент является дочерним hello `<TrustFrameworkPolicy>`.  Внутри сведения понадобятся вам tooput hello, влияющий на времени жизни токенов.  Hello XML выглядит следующим образом:

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

**Доступ к времени жизни токенов** hello доступа, время существования маркера можно изменить, изменив значение hello внутри hello `<Item>` с hello ключ = «token_lifetime_secs» в секундах.  значение по умолчанию Hello в встроенные — 3 600 секунд (60 минут).

**Время существования маркера идентификатор** время существования маркера идентификатор hello можно изменить, изменив значение hello внутри hello `<Item>` с hello ключ = «id_token_lifetime_secs» в секундах.  значение по умолчанию Hello в встроенные — 3 600 секунд (60 минут).

**Обновить время существования маркера** hello время существования маркера обновления можно изменить, изменив значение hello внутри hello `<Item>` с hello ключ = «refresh_token_lifetime_secs» в секундах.  значение по умолчанию Hello в встроенные — 1209600 секунд (14 дней).

**Обновить время существования маркера скользящее окно** при желании tooset токен обновления времени существования tooyour скользящее окно изменить значение hello внутри `<Item>` с hello ключ = «rolling_refresh_token_lifetime_secs» в секундах.  значение по умолчанию Hello в встроенные — 7776000 (90 дней).  Если вы не хотите tooenfore скользящее окно времени существования, замените эту строку с:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Утверждение издателя (iss)** toochange hello (iss) издателя утверждения, измените значение hello внутри hello `<Item>` с hello Key = «IssuanceClaimPattern».  применимые значения Hello `AuthorityAndTenantGuid` и `AuthorityWithTfp`.

**Параметр утверждения, представляющий идентификатор политики** hello параметры для данного параметра не TFP (политики доверия framework) и контроля доступа (Справочник по контекст проверки подлинности).  
Мы рекомендуем этот tooTFP toodo Установка этого параметра, убедитесь, hello `<Item>` с hello Key = «AuthenticationContextReferenceClaimPattern» существует и имеет значение hello `None`.
Добавьте этот элемент в элемент `<OutputClaims>`:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
Для управления Доступом, удалите hello `<Item>` с hello Key = «AuthenticationContextReferenceClaimPattern».

**Утверждение темы (sub)** этот параметр по умолчанию tooObjectID, если вы хотите tooswitch это слишком`Not Supported`, hello следующие:

Замените эту строку: 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
на следующую:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Режим работы сеанса и SSO
toochange вашей поведение сеанса и конфигурации единого входа, необходимо tooadd `<UserJourneyBehaviors>` элемент внутри hello `<RelyingParty>` элемента.  Hello `<UserJourneyBehaviors>` элемент должен следовать непосредственно за hello `<DefaultUserJourney>`.  Здравствуйте, внутри вашей `<UserJourneyBehavors>` элемент должен выглядеть следующим образом:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Настройка единого входа (SSO)** toochange hello единого входа для конфигурации, требуется значение hello toomodify `<SingleSignOn>`.  применимые значения Hello `Tenant`, `Application`, `Policy` и `Disabled`. 

**Веб-приложение, время жизни сеанса (в минутах)** toochange hello hello веб-приложения время жизни сеанса, необходимо получить значение toomodify из hello `<SessionExpiryInSeconds>` элемента.  значение по умолчанию Hello в встроенных политик — 86400 секунд (1 440 минут).

**Время ожидания сеанса приложения Web** toochange hello web app время ожидания сеанса, необходимо значение hello toomodify `<SessionExpiryType>`.  применимые значения Hello `Absolute` и `Rolling`.
