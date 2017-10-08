---
title: "aaaConditional доступ для совместной работы пользователей Azure Active Directory B2B | Документы Microsoft"
description: "Совместная работа Azure Active Directory B2B поддерживает многофакторную проверку подлинности (MFA) для корпоративных приложений tooyour избирательный доступ"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>Условный доступ пользователей в службе совместной работы B2B

## <a name="multi-factor-authentication-for-b2b-users"></a>Многофакторная идентификация для пользователей B2B
Благодаря службе совместной работы Azure AD B2B организации могут применять политики многофакторной проверки подлинности (MFA) к пользователям B2B. Эти политики могут применяться на уровне отдельных пользователей, hello клиента или приложения hello таким же образом, что они включены штатных сотрудников и членов hello организации. Политики многофакторной проверки Подлинности применяются в организации по ресурсам hello.

Пример:
1. Рабочий процесс администратора или сведения в компании A приглашает пользователя из приложения компании B tooan *Foo* в компании а.
2. Приложение *Foo* в компании A — настроенное toorequire многофакторной проверки Подлинности при доступе.
3. Когда пользователь hello компании B пытается tooaccess приложения *Foo* hello компании клиента, они являются задаваемые toocomplete запрос многофакторной проверки Подлинности.
4. Hello пользователя можно настроить их многофакторной проверки Подлинности компании A и выбирает параметр их многофакторной проверки Подлинности.
5. Такой режим применим для любой учетной записи (например, Azure AD или MSA, если пользователи из компании Б используют для проверки подлинности социальные сети).
6. Компания A должна иметь достаточное количество лицензий Azure AD Premium с поддержкой MFA. Hello сотрудником компании B использует лицензии компании A.

приглашение аренды Hello всегда является ответственность за многофакторной проверки Подлинности для пользователей в организации партнера hello, даже если hello партнерской организации возможности многофакторной проверки Подлинности.

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>Настройка MFA для пользователей службы совместной работы B2B
toodiscover примеры tooset копирование многофакторной проверки Подлинности для пользователей B2B совместной работы, как в разделе hello следующие видео:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>Прохождение MFA пользователями службы B2B при активации предложения
См. следующие возможности активации hello toosee анимации hello.

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>Сброс настроек MFA для пользователей службы совместной работы B2B
В настоящее время Здравствуйте, администратор может потребовать B2B совместной работы пользователей tooproof копирование снова только с помощью hello следующие командлеты PowerShell:

1. Подключение tooAzure AD

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. Получение сведений о методах проверки для всех пользователей.

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  Пример:

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. Сменить hello метод многофакторной проверки Подлинности для конкретного пользователя toorequire hello B2B совместную работу пользователя tooset дополнительная защита методов еще раз. Пример:

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>Почему мы выполнять многофакторную проверку Подлинности на аренды ресурса hello?

В текущем выпуске hello многофакторной проверки Подлинности всегда проводится в аренды ресурса hello, по причинам, предсказуемость. Например предположим, что пользователь Contoso (Sally) является приглашенных tooFabrikam и Fabrikam включения многофакторной проверки Подлинности для пользователей B2B.

Если Contoso включенной политикой многофакторной проверки Подлинности для App1, но не App2, затем Если мы рассмотрим hello многофакторной проверки Подлинности Contoso утверждения в маркере hello, мы может отображаться следующая проблема hello.

* День 1. Пользователь, который использует MFA в компании Contoso, обращается к App1 и не получает дополнительный запрос на многофакторную проверку подлинности в Fabrikam.

* Второй день: hello пользователя к 2 приложения в компании Contoso, поэтому теперь при доступе к компании Fabrikam, их необходимо зарегистрировать существует многофакторной проверки подлинности.

Этот процесс может вызывать путаницу и может привести toodrop в завершений вход.

Кроме того даже если компании Contoso есть возможность многофакторной проверки Подлинности, не всегда hello вариантов hello Fabrikam будет доверять hello политики многофакторной проверки Подлинности Contoso.

И наконец, MFA клиента ресурса также поддерживает управляемые учетные записи службы (MSA), идентификаторы из социальных сетей и партнерские организации, в которых не настроена многофакторная проверка подлинности.

Таким образом hello многофакторной проверки подлинности для пользователей B2B рекомендуется tooalways должен требовать многофакторную проверку Подлинности в приглашении клиента hello. Это требование может привести toodouble многофакторной проверки Подлинности, в некоторых случаях, но при каждом обращении к приглашению клиента hello, hello конечным пользователям получается прогнозируемого: необходимо зарегистрировать Sally многофакторной проверки подлинности клиента приглашению hello.

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>Условный доступ на основе устройств, расположения и рисков для пользователей B2B

Когда Contoso включает политик условного доступа на основе устройств для корпоративных данных, доступ к ней с устройств, которые не управляются компанией Contoso и не соответствуют политикам устройства hello Contoso.

Если устройство пользователя hello B2B не находится под управлением Contoso, доступ B2B пользователей из hello партнерские организации будет заблокирован в контекст эти политики применяются. Тем не менее Contoso может создать исключения, списков, содержащих определенный партнер пользователей tooexclude их из hello политики условного доступа на основе устройств.

#### <a name="location-based-conditional-access-for-b2b"></a>Условный доступ на основе расположения для пользователей B2B

Политики условного доступа на основе расположения может применяться для пользователей B2B Если hello приглашению организации могут toocreate доверенных диапазон IP-адресов, который определяет их партнерских организациях.

#### <a name="risk-based-conditional-access-for-b2b"></a>Политики условного доступа на основе рисков для пользователей B2B

В настоящее время риск вход политики на основе не может быть применен tooB2B пользователей, поскольку оценку рисков hello выполняется в домашней организации пользователя hello B2B.

## <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?](active-directory-b2b-admin-add-users.md)
* [Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?](active-directory-b2b-iw-add-users.md)
* [элементы Hello hello электронное приглашение B2B совместной работы](active-directory-b2b-invitation-email.md)
* [Активация приглашения службы совместной работы B2B](active-directory-b2b-redemption-experience.md)
* [Руководство по лицензированию службы совместной работы Azure Active Directory B2B](active-directory-b2b-licensing.md)
* [Устранение неполадок службы совместной работы Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B](active-directory-b2b-faq.md)
* [API службы совместной работы Azure Active Directory B2B и настройка](active-directory-b2b-api.md)
* [Добавление пользователей службы совместной работы B2B без приглашения](active-directory-b2b-add-user-without-invite.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
