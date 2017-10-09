---
title: "Текущие ограничения сквозной проверки подлинности Azure AD Connect | Документация Майкрософт"
description: "В этой статье описываются hello текущего ограничения сквозная проверка подлинности Azure Active Directory (Azure AD)."
services: active-directory
keywords: "сквозная проверка подлинности azure ad connect, установка active directory, необходимые компоненты для azure ad, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Текущие ограничения сквозной проверки подлинности Azure Active Directory

>[!IMPORTANT]
>Сквозная проверка подлинности Azure AD доступна в предварительной версии. Это бесплатная функция, и любые платных выпусков toouse Azure AD не нужно его. Сквозная проверка подлинности доступна только в hello world wide экземпляра Azure AD, а не в [Германия Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) и [государственных облако Microsoft Azure](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.

следующие сценарии Hello, полностью поддерживаются во время предварительного просмотра:

- Вход пользователей во все браузерные приложения.
- Вход пользователей в клиентские приложения Office 365, поддерживающие [современную проверку подлинности](https://aka.ms/modernauthga).
- Присоединение устройств Windows 10 к Azure AD.
- Поддержка Exchange ActiveSync.

## <a name="unsupported-scenarios"></a>Неподдерживаемые сценарии

Hello ниже сценарии являются _не_ поддерживается во время предварительного просмотра:

- Вход пользователей в устаревшие клиентские приложения Office (Office 2013 или более ранних версий). Организаций, рекомендуется tooswitch toomodern проверки подлинности, если это возможно. Современная аутентификация обеспечивает поддержку сквозной аутентификации, а также помогает защитить учетные записи пользователей с помощью таких функций [условного доступа](../active-directory-conditional-access.md), как Многофакторная идентификация (MFA).
- Вход пользователей в клиентские приложения Skype для бизнеса, включая Skype для бизнеса 2016.
- Вход пользователей в PowerShell версии 1.0. Вместо этого рекомендуется использовать PowerShell версии 2.0.

>[!IMPORTANT]
>В качестве решения для неподдерживаемых сценариях Включение синхронизация хэшей паролей hello [дополнительных компонентов](active-directory-aadconnect-get-started-custom.md#optional-features) страница в мастере hello Azure AD Connect. Синхронизация хэшей паролей действует как переход на резервный ресурс hello предшествующий сценарии _только_ (и _не_ как универсальный резервной tooPass сквозной проверки подлинности). Если эти сценарии не требуются, отключите синхронизацию хэша паролей.

## <a name="next-steps"></a>Дальнейшие действия
- [**Краткое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-quick-start.md). Настройка и подготовка к работе сквозной проверки подлинности Azure Active Directory.
- [**Техническое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-how-it-works.md). Сведения о том, как работает эта функция.
- [**Часто задаваемые вопросы** ](active-directory-aadconnect-pass-through-authentication-faq.md) -ответы на вопросы и ответы toofrequently.
- [**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.
- [**Простой единый вход Azure Active Directory**](active-directory-aadconnect-sso.md). Дополнительные сведения об этой дополнительной функции.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.
