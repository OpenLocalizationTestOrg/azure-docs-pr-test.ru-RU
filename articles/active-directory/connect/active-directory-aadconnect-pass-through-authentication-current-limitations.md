---
title: "Текущие ограничения сквозной проверки подлинности Azure AD Connect | Документация Майкрософт"
description: "Эта статья содержит сведения о текущих ограничениях сквозной проверки подлинности Azure Active Directory (Azure AD)."
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
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Текущие ограничения сквозной проверки подлинности Azure Active Directory

>[!IMPORTANT]
>Сквозная проверка подлинности Azure AD доступна в предварительной версии. Это бесплатная функция, и для ее использования не требуются платные выпуски Azure AD. Сквозная проверка подлинности доступна только в общедоступном экземпляре Azure AD, а не в [Microsoft Cloud для Германии](http://www.microsoft.de/cloud-deutschland) и [облаке Microsoft Azure для государственных организаций](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.

На этапе предварительной версии полностью поддерживаются следующие сценарии.

- Вход пользователей во все браузерные приложения.
- Вход пользователей в клиентские приложения Office 365, поддерживающие [современную проверку подлинности](https://aka.ms/modernauthga).
- Присоединение устройств Windows 10 к Azure AD.
- Поддержка Exchange ActiveSync.

## <a name="unsupported-scenarios"></a>Неподдерживаемые сценарии

На этапе предварительной версии _не_ поддерживаются следующие сценарии.

- Вход пользователей в устаревшие клиентские приложения Office (Office 2013 или более ранних версий). Организациям рекомендуется перейти на современные способы аутентификации, если это возможно. Современная аутентификация обеспечивает поддержку сквозной аутентификации, а также помогает защитить учетные записи пользователей с помощью таких функций [условного доступа](../active-directory-conditional-access.md), как Многофакторная идентификация (MFA).
- Вход пользователей в клиентские приложения Skype для бизнеса, включая Skype для бизнеса 2016.
- Вход пользователей в PowerShell версии 1.0. Вместо этого рекомендуется использовать PowerShell версии 2.0.

>[!IMPORTANT]
>В качестве временного решения для неподдерживаемых сценариев включите синхронизацию хэша паролей на странице [Дополнительные возможности](active-directory-aadconnect-get-started-custom.md#optional-features) в мастере Azure AD Connect. Синхронизация хэша паролей используется в качестве запасного варианта _только_ для предыдущих сценариев (а _не_ в качестве универсального варианта для сквозной проверки подлинности). Если эти сценарии не требуются, отключите синхронизацию хэша паролей.

## <a name="next-steps"></a>Дальнейшие действия
- [**Краткое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-quick-start.md). Настройка и подготовка к работе сквозной проверки подлинности Azure Active Directory.
- [**Azure Active Directory Pass-through Authentication: Technical deep dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) (Техническое руководство по сквозной проверке подлинности Azure Active Directory). Сведения о том, как работает эта функция.
- [**Часто задаваемые вопросы**](active-directory-aadconnect-pass-through-authentication-faq.md). Ответы на часто задаваемые вопросы.
- [**Устранение неполадок**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md). Узнайте, как устранить самые распространенные проблемы с этой функцией.
- [**Простой единый вход Azure Active Directory**](active-directory-aadconnect-sso.md). Дополнительные сведения об этой дополнительной функции.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.
