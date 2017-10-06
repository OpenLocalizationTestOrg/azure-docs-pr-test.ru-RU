---
title: "Azure Active Directory B2C: Основные сведения о настраиваемых политик пакет начального приветствия | Документы Microsoft"
description: "В этой статье описываются пользовательские политики Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>Основные сведения о настраиваемых политик hello пакета начального hello Azure AD B2C настраиваемой политики

В этом разделе перечислены все ключевые элементы hello hello B2C_1A_base политики, входящий в состав hello **пакет начального** и который используется для создания собственных политик через наследование hello hello *B2C_1A_base_ расширения политики*.

Таким образом он более особенно посвящено hello уже определен утверждения типы, преобразования утверждений, определения содержимого, поставщиками утверждений с их профилями технические и hello поездок основных пользователей.

> [!IMPORTANT]
> Корпорация Майкрософт не дает каких-либо гарантий, явных или подразумеваемых, относительно toohello сведения, предоставленные здесь и далее. Изменения могут быть внесены в любое время: до, во время или после выпуска общедоступной версии.

Hello B2C_1A_base_extensions политики и собственные политики можно переопределить эти определения и распространить действие этой политики родительского, предоставляя дополнительные шаблоны, при необходимости.

Здравствуйте, ключевые элементы hello *B2C_1A_base политики* : типы утверждений, преобразования утверждений и определения содержимого. Эти элементы можно подвержены toobe, на которые ссылается собственные политики, а также как hello *B2C_1A_base_extensions политики*.

## <a name="claims-schemas"></a>Схемы утверждений

Схемы утверждений состоят из трех разделов:

1.  Первый раздел, в котором перечислены hello минимальное утверждения, которые необходимы для hello пользователя поездок toowork должным образом.
2.  Второй раздел, что списки hello утверждениями, необходимыми для параметров строки запроса и другие специальные параметры toobe передан tooother поставщиков утверждений, особенно login.microsoftonline.com для проверки подлинности. **Не изменяйте эти утверждения**.
3.  В результате и третий раздел, в котором перечислены дополнительные утверждения, которые могут быть собраны от пользователя hello, хранятся в каталоге hello отправляются в токенах во время входа в. В этом разделе можно добавить новые утверждения типа toobe полученные от пользователя hello и/или отправки в маркере hello.

> [!IMPORTANT]
> Схема утверждений Hello содержит ограничения на определенных утверждений, например пароли и имена пользователей. Hello политики доверия Framework (TF) рассматривает Azure AD как любой другой поставщик утверждений и все ограничения modelled в политике premium hello. Политика может быть измененный tooadd дополнительные ограничения или использовать другого поставщика утверждений для хранения учетных данных, который будет иметь свои собственные ограничения.

Ниже перечислены типы доступных утверждений Hello.

### <a name="claims-that-are-required-for-hello-user-journeys"></a>Утверждения, которые требуются для поездок пользователя hello

После утверждения Hello требуются toowork поездок пользователя должным образом.

| Тип утверждения | Описание |
|-------------|-------------|
| *UserId* | Имя пользователя |
| *signInName* | Имя входа |
| *tenantId* | Идентификатор клиента (ID) hello объекта-пользователя в Azure AD B2C Premium |
| *objectId* | Идентификатор объекта (ID) hello объекта пользователя в Azure AD B2C Premium |
| *password* | Пароль |
| *newPassword* | |
| *reenterPassword* | |
| *passwordPolicies* | Политики паролей, используемых стойкость пароля Azure AD B2C Premium toodetermine, срока действия и т. д. |
| *sub* | |
| *alternativeSecurityId* | |
| *identityProvider* | |
| *displayName* | |
| *strongAuthenticationPhoneNumber* | Номер телефона пользователя |
| *Verified.strongAuthenticationPhoneNumber* | |
| *email* | Адрес электронной почты, может быть пользователя используется toocontact hello |
| *signInNamesInfo.emailAddress* | Адрес электронной почты, hello пользователя можно использовать toosign в |
| *otherMails* | Адреса электронной почты, которые могут быть пользователя используется toocontact hello |
| *userPrincipalName* | Имя пользователя, сохраненного в Azure AD B2C Premium hello |
| *upnUserName* | Имя пользователя для создания имени субъекта-пользователя |
| *mailNickName* | Имя ник почты пользователя, сохраненного в Azure AD B2C Premium hello |
| *newUser* | |
| *executed-SelfAsserted-Input* | Утверждения с указанием ли атрибуты, собранные от пользователя hello |
| *executed-PhoneFactor-Input* | Утверждения с указанием, собираются ли новый номер телефона пользователя hello |
| *authenticationSource* | Указывает, была ли проверка подлинности пользователя hello в социальных поставщика удостоверений, login.microsoftonline.com или локальной учетной записи |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>Утверждения, необходимые для параметров строки запроса и других особых параметров

Hello следующие утверждения — это обязательный toopass на поставщиков утверждений tooother специальных параметров (включая некоторые параметры строки запроса):

| Тип утверждения | Описание |
|-------------|-------------|
| *nux* | Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com |
| *nca* | Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com |
| *prompt* | Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com |
| *mkt* | Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com |
| *lc* | Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com |
| *grant_type* | Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com |
| *scope* | Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com |
| *client_id* | Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com |
| *objectIdFromSession* | Параметр, предоставляемые hello по умолчанию сеанса управления поставщика tooindicate, hello объекта с идентификатором были получены из сеанса единого входа |
| *isActiveMFASession* | Параметр с hello многофакторной проверки Подлинности сеанса управления tooindicate при условии, что этот пользователь hello имеет активный сеанс многофакторной проверки Подлинности |

### <a name="additional-optional-claims-that-can-be-collected"></a>Дополнительные (необязательные) утверждения для сбора

Hello следующих утверждений дополнительные утверждения, которые могут быть собраны от пользователей hello, хранятся в каталоге hello и отправляются в маркере hello. Как описано перед дополнительные утверждения можно добавить список toothis.

| Тип утверждения | Описание |
|-------------|-------------|
| *givenName* | Имя пользователя |
| *surname* | Фамилия пользователя |
| *Extension_picture* | Фотография пользователя из социальных сетей |

## <a name="claim-transformations"></a>Преобразования утверждения

Ниже перечислены преобразования доступных утверждений Hello.

| Преобразования утверждения | Описание |
|----------------------|-------------|
| *CreateOtherMailsFromEmail* | |
| *CreateRandomUPNUserName* | |
| *CreateUserPrincipalName* | |
| *CreateSubjectClaimFromObjectID* | |
| *CreateSubjectClaimFromAlternativeSecurityId* | |
| *CreateAlternativeSecurityId* | |

## <a name="content-definitions"></a>Определения содержимого

В этом разделе описываются определения hello содержимого, уже объявлен в hello *B2C_1A_base* политики. Эти определения содержимого будут подвержены toobe ссылка, переопределения и/или расширено по мере необходимости в собственные политики, а также как hello *B2C_1A_base_extensions* политики.

| Поставщик утверждений | Описание |
|-----------------|-------------|
| *Facebook* | |
| *Вход с использованием локальной учетной записи* | |
| *PhoneFactor* | |
| *Azure Active Directory* | |
| *Самоподтверждение* | |
| *Локальная учетная запись* | |
| *Управление сеансами* | |
| *Подсистема политик инфраструктуры доверия* | |
| *Технические профили* | |
| *Поставщик токенов* | |

## <a name="technical-profiles"></a>Технические профили

В этом разделе описывается технические профили hello уже объявлен каждого поставщика утверждений в hello *B2C_1A_base* политики. Эти технические профили будут подвержены toobe Дополнительные ссылки, переопределении или расширено по мере необходимости в собственные политики, а также как hello *B2C_1A_base_extensions* политики.

### <a name="technical-profiles-for-facebook"></a>Технические профили для Facebook

| Технический профиль | Описание |
|-------------------|-------------|
| *Facebook-OAUTH* | |

### <a name="technical-profiles-for-local-account-signin"></a>Технические профили для входа с использованием локальной учетной записи

| Технический профиль | Описание |
|-------------------|-------------|
| *Login-NonInteractive* | |

### <a name="technical-profiles-for-phone-factor"></a>Технические профили для PhoneFactor

| Технический профиль | Описание |
|-------------------|-------------|
| *PhoneFactor-Input* | |
| *PhoneFactor-InputOrVerify* | |
| *PhoneFactor-Verify* | |

### <a name="technical-profiles-for-azure-active-directory"></a>Технические профили для Azure Active Directory

| Технический профиль | Описание |
|-------------------|-------------|
| *AAD-Common* | Включен технические профиль hello другие профили технические AAD-xxx |
| *AAD-UserWriteUsingAlternativeSecurityId* | Технический профиль для входа в социальные сети |
| *AAD-UserReadUsingAlternativeSecurityId* | Технический профиль для входа в социальные сети |
| *AAD-UserReadUsingAlternativeSecurityId-NoError* | Технический профиль для входа в социальные сети |
| *AAD-UserWritePasswordUsingLogonEmail* | Технический профиль для локальных учетных записей |
| *AAD-UserReadUsingEmailAddress* | Технический профиль для локальных учетных записей |
| *AAD-UserWriteProfileUsingObjectId* | Технический профиль для обновления записи пользователя с помощью objectId |
| *AAD-UserWritePhoneNumberUsingObjectId* | Технический профиль для обновления записи пользователя с помощью objectId |
| *AAD-UserWritePasswordUsingObjectId* | Технический профиль для обновления записи пользователя с помощью objectId |
| *AAD-UserReadUsingObjectId* | Технические профиль является данных используется tooread после аутентификации пользователя |

### <a name="technical-profiles-for-self-asserted"></a>Технические профили для самоподтверждения

| Технический профиль | Описание |
|-------------------|-------------|
| *SelfAsserted-Social* | |
| *SelfAsserted-ProfileUpdate* | |

### <a name="technical-profiles-for-local-account"></a>Технические профили для локальной учетной записи

| Технический профиль | Описание |
|-------------------|-------------|
| *LocalAccountSignUpWithLogonEmail* | |

### <a name="technical-profiles-for-session-management"></a>Технические профили для управления сеансами

| Технический профиль | Описание |
|-------------------|-------------|
| *SM-Noop* | |
| *SM-AAD* | |
| *SM-SocialSignup* | Имя профиля, используемых toodisambiguate AAD сеанса между входами вверх и вход |
| *SM-SocialLogin* | |
| *SM-MFA* | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Технические профили для технических профилей и подсистемы политик инфраструктуры доверия

В настоящее время нет технических профили задаются для hello **TechnicalProfiles модуль политики Trustframework** поставщика утверждений.

### <a name="technical-profiles-for-token-issuer"></a>Технические профили для поставщика токенов

| Технический профиль | Описание |
|-------------------|-------------|
| *JwtIssuer* | |

## <a name="user-journeys"></a>Пути взаимодействия пользователя

В этом разделе описывается hello пользователя пути уже объявлен в hello *B2C_1A_base* политики. Эти пути пользователя, подвержены toobe Дополнительные ссылки, переопределении или расширено по мере необходимости в собственные политики, а также как hello *B2C_1A_base_extensions* политики.

| Пути взаимодействия пользователя | Описание |
|--------------|-------------|
| *SignUp* | |
| *SignIn* | |
| *SignUpOrSignIn* | |
| *EditProfile* | |
| *PasswordReset* | |
