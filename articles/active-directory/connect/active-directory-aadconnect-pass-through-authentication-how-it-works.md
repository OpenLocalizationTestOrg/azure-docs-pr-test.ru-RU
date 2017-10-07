---
title: "Сквозная аутентификация в Azure AD Connect — как это работает? | Документация Майкрософт"
description: "В этой статье описывается процедура сквозной аутентификации Azure Active Directory."
services: active-directory
keywords: "сквозная аутентификация azure ad connect, установка active directory, необходимые компоненты для azure ad, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Сквозная аутентификация Azure Active Directory — подробное техническое руководство

>[!IMPORTANT]
>Сквозная проверка подлинности Azure AD доступна в предварительной версии. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Как работает сквозная аутентификация Azure Active Directory?

Когда пользователь пытается toosign в приложении, защищенном Azure Active Directory (Azure AD) и если сквозная проверка подлинности включена на клиенте hello hello выполняются следующие действия.

1. Hello пользователь пытается tooaccess приложения (например, hello Outlook Web App - https://outlook.office365.com/owa/).
2. Если пользователь hello не уже выполнил вход, пользователь hello не перенаправленный toohello Azure AD на странице входа.
3. Hello пользователь вводит свое имя пользователя и пароль в hello Azure AD на странице входа и нажимает кнопку «Вход» hello.
4. Azure AD, получив запрос вход hello, помещает hello имя пользователя и пароль (зашифрованный с помощью открытого ключа) в очередь.
5. Агента сквозной проверки подлинности в локальной делает очередь toohello исходящего вызова и получает имя пользователя hello и зашифрованный пароль.
6. агент Hello расшифровывает пароль hello, используя свой закрытый ключ.
7. агент Hello затем проверяет hello имя пользователя и пароль в Active Directory с использованием стандартных API Windows (аналогично toowhat механизм используется служб федерации Active Directory). Hello имя пользователя может быть либо имя пользователя по умолчанию hello в локальной среде (обычно `userPrincipalName`) или другой атрибут, настроенные в Azure AD Connect (известный как `Alternate ID`).
8. локальный контроллер домена Active Directory (DC) Hello то оценивает hello запрос и возвращает hello соответствующий ответ (успех, отказ, срок действия пароля истек, или пользователь заблокирован) toohello агента.
9. агент Hello, в свою очередь, возвращает этот ответ назад tooAzure AD.
10. Azure AD оценивает ответа hello и отвечает пользователь toohello соответствующим образом — например, он сразу же входе пользователя hello или запросы для многофакторной проверки подлинности (MFA).
11. Если вход hello пользователей прошла успешно, hello пользователь не может tooaccess приложения hello.

Hello следующей схеме показаны все компоненты hello и этапы hello.

![Сквозная проверка подлинности](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>Дальнейшие действия
- [**Текущие ограничения**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) — эта функция в настоящее время находится на стадии предварительной версии. Узнайте, какие сценарии поддерживаются, а какие нет.
- [**Краткое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-quick-start.md). Настройка и подготовка к работе сквозной проверки подлинности Azure Active Directory.
- [**Часто задаваемые вопросы** ](active-directory-aadconnect-pass-through-authentication-faq.md) -ответы на вопросы и ответы toofrequently.
- [**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.
- [**Простой единый вход Azure Active Directory**](active-directory-aadconnect-sso.md). Дополнительные сведения об этой дополнительной функции.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.
