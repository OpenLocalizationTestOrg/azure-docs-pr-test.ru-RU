---
title: "Azure AD Connect: простой единый вход | Документы Майкрософт"
description: "В этом разделе описываются Azure Active Directory (Azure AD) прозрачную единого входа и как позволяет вам tooprovide true единого входа для корпоративных пользователей настольных компьютеров в корпоративной сети."
services: active-directory
keywords: "что такое Azure AD Connect, установка Active Directory, необходимые компоненты для Azure AD, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Простой единый вход Azure Active Directory

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>Что такое простой единый вход Azure Active Directory?

Azure Active Directory прозрачную единого входа (Azure AD, эффективная SSO) автоматически подписывает пользователей они находятся в своей корпоративной сети подключенных tooyour корпоративных устройств. Если включено, пользователи не нужны tootype в toosign свои пароли в tooAzure AD и обычно даже введите их имена пользователей. Эта функция обеспечивает пользователям простой доступ tooyour облачных приложений без необходимости какие-либо дополнительные локальные компоненты.

Эффективная единого входа может сочетаться с либо hello [синхронизация хэшей паролей](active-directory-aadconnectsync-implement-password-synchronization.md) или [сквозная проверка подлинности](active-directory-aadconnect-pass-through-authentication.md) входа в методы.

![Простой единый вход](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>Простой единый вход находится на этапе предварительной версии. Этот компонент является _не_ применимо tooActive службы федерации Directory (ADFS).

## <a name="key-benefits"></a>Основные преимущества

- *Удобство работы для пользователей*
  - Пользователи автоматически входят как в локальные, так и в облачные приложения.
  - Пользователи не имеют tooenter свои пароли несколько раз.
- *Легко toodeploy & администрирования*
  - Никакие дополнительные компоненты, необходимые локальной toomake эту работу.
  - Эта функция работает с любым методом аутентификации в облаке: [синхронизацией хэша паролей](active-directory-aadconnectsync-implement-password-synchronization.md) и [сквозной аутентификацией](active-directory-aadconnect-pass-through-authentication.md).
  - Может быть распространен toosome или всех пользователей с помощью групповой политики.
  - Регистрация устройств Windows 10 в Azure AD без необходимости hello в любой инфраструктуре AD FS. Эта возможность требуется, вы toouse версии 2.1 или более поздней hello [клиента к рабочему месту](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="feature-highlights"></a>Краткие сведения о возможностях

- Имя входа пользователя может быть либо имя пользователя по умолчанию hello в локальной среде (`userPrincipalName`) или другой атрибут, настроенные в Azure AD Connect (`Alternate ID`). Как использовать случаях рабочих, так как прозрачную SSO использует hello `securityIdentifier` утверждения в toolook билет Kerberos hello копирование hello соответствующего объекта пользователя в Azure AD.
- Простой единый вход — ситуативно-обусловленная функция. В случае неудачи по любой причине hello пользователя входа в систему возвращается tooits регулярного поведение — т. е., hello пользователь должен tooenter свой пароль на странице входа hello.
- Если приложение отправляет `domain_hint` (OpenID Connect) или `whr` (SAML) параметр - Идентификация вашего клиента или `login_hint` параметр - Идентификация пользователя hello в Azure AD входа в запросе, пользователи автоматически входите без них Введите имена пользователей и пароли.
- Функцию можно включить с помощью Azure AD Connect.
- Это бесплатная функция, и любые платных выпусков toouse Azure AD не нужно его.
- Она доступна в клиентах на основе веб-браузера и клиентах Office, поддерживающих [современную проверку подлинности](https://aka.ms/modernauthga) на платформах и в браузерах с поддержкой проверки подлинности Kerberos.

| Операционная система и браузер |Internet Explorer|Edge|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|Да|Нет|Да|Да\*|Недоступно
|Windows 8.1|Да|Недоступно|Да|Да\*|Недоступно
|Windows 8|Да|Недоступно|Да|Да\*|Недоступно
|Windows 7|Да|Недоступно|Да|Да\*|Недоступно
|Mac OS X|Недоступно|Недоступно|Да\*|Да\*|Да\*

\*Требуется [дополнительная настройка](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!IMPORTANT]
>Мы недавно откат поддержка Edge tooinvestigate устранения проблем клиента.

>[!NOTE]
>Для Windows 10 hello рекомендации — toouse [присоединения Azure AD](../active-directory-azureadjoin-overview.md) для hello оптимальной единого входа опыт работы с Azure AD.

## <a name="next-steps"></a>Дальнейшие действия

- [**Краткое руководство**](active-directory-aadconnect-sso-quick-start.md). Настройка и подготовка к работе простого единого входа Azure AD.
- [**Техническое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-sso-how-it-works.md). Сведения о том, как работает эта функция.
- [**Часто задаваемые вопросы** ](active-directory-aadconnect-sso-faq.md) -ответы на вопросы и ответы toofrequently.
- [**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-sso.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.
