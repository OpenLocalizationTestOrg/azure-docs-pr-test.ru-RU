---
title: "Azure AD Connect: простой единый вход — как это работает | Документы Майкрософт"
description: "В этой статье описано, как работает функция hello Azure Active Directory прозрачную единого входа."
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Подробное техническое руководство по простому единому входу Azure Active Directory

В этой статье приводятся технические сведения в работе системы hello Azure Active Directory прозрачную единого входа (прозрачную SSO).

>[!IMPORTANT]
>компонент Hello прозрачную единого входа в настоящий момент в режиме предварительного просмотра.

## <a name="how-does-seamless-sso-work"></a>Как работает простой единый вход?

Этот раздел состоит из двух частей tooit.
1. Настройка Hello функции hello прозрачную единого входа.
2. Как транзакция единого входа пользователя работает с простым единым входом.

### <a name="how-does-set-up-work"></a>Как выполняется настройка?

Простой единый вход включается с помощью Azure AD Connect, как показано [здесь](active-directory-aadconnect-sso-quick-start.md). При включении компонента hello, происходят hello следующие шаги:
- В локальной службе Active Directory (AD) создается учетная запись компьютера с именем `AZUREADSSOACCT` (представляет Azure AD).
- ключ расшифровки Kerberos учетная запись компьютера Hello безопасно совместно с Azure AD.
- Кроме того два Kerberos имен участников-служб (SPN) создаются toorepresent два URL-адреса, используемые при входе в Azure AD.

>[!NOTE]
> в каждом лесу создаются Hello учетной записи компьютера и Kerberos приветствия имен участников-служб синхронизации tooAzure AD (с помощью Azure AD Connect) и для пользователей, для которого требуется эффективная единого входа. Переместить hello `AZUREADSSOACCT` tooan учетной записи компьютера подразделение (OU) которых хранимые tooensure, которые управляются в другие учетные записи компьютеров hello таким же способом, а не удаляется.

>[!IMPORTANT]
>Настоятельно рекомендуется, чтобы вы [, наведите курсор на ключ расшифровки Kerberos hello](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) из hello `AZUREADSSOACCT` учетная запись компьютера каждые 30 дней.

### <a name="how-does-sign-in-with-seamless-sso-work"></a>Как работает вход с функцией простого единого входа?

После завершения установки hello прозрачную SSO работает hello таким же способом, как любой другой вход, использующего встроенную проверку подлинности Windows (IWA). Hello поток выглядит следующим образом:

1. Hello пользователь пытается tooaccess приложения (например, hello Outlook Web App - https://outlook.office365.com/owa/) с корпоративной устройства в корпоративной сети, присоединенных к домену.
2. Если пользователь hello не уже выполнил вход, пользователь hello не перенаправленный toohello Azure AD на странице входа.

  >[!NOTE]
  >Если запрос вход hello Azure AD включает `domain_hint` (идентификации клиента - например, contoso.onmicrosoft.com) или `login_hint` (Идентификация пользователя hello - например, user@contoso.onmicrosoft.com или user@contoso.com) пропущен параметр, а затем шаг 2.

3. пользователь вводит свои имя пользователя в hello Azure AD на странице входа Hello.
4. С помощью JavaScript в фоновом режиме hello, Azure AD предлагает hello браузера, через 401 несанкционированный ответа tooprovide билет Kerberos.
5. Hello браузера, в свою очередь, запрашивает билет у Active Directory для hello `AZUREADSSOACCT` учетной записи компьютера (представляющий Azure AD).
6. Active Directory находит учетную запись компьютера hello и возвращается обозревателя toohello билет Kerberos, зашифрованные с помощью учетной записи компьютера hello секрет.
7. hello билет Kerberos, полученную из Active Directory tooAzure AD перенаправляет браузер Hello (на одном hello [URL-адреса Azure AD, ранее добавленных настроек зоны toohello обозревателя](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).
8. Azure AD расшифровывает hello билет Kerberos, включающий hello удостоверение пользователя hello, вход в корпоративных устройств hello, ранее с помощью hello общий ключ.
9. После оценки Azure AD возвращается токен задней toohello приложение или запрашивает у пользователя tooperform hello дополнительных экспериментов, например многофакторной проверки подлинности.
10. Если вход hello пользователей прошла успешно, hello пользователь не может tooaccess приложения hello.

Hello следующей схеме показаны все компоненты hello и этапы hello.

![Простой единый вход](./media/active-directory-aadconnect-sso/sso2.png)

Эффективная SSO нежестких, что означает, что в случае неудачи hello входа в систему возвращается tooits регулярного поведение — т. е., hello пользователь должен tooenter их toosign пароль в.

## <a name="next-steps"></a>Дальнейшие действия

- [**Краткое руководство**](active-directory-aadconnect-sso-quick-start.md). Настройка и подготовка к работе простого единого входа Azure AD.
- [**Часто задаваемые вопросы** ](active-directory-aadconnect-sso-faq.md) -ответы на вопросы и ответы toofrequently.
- [**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-sso.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.
