---
title: "Azure AD Connect: сквозная аутентификация | Документация Майкрософт"
description: "В этой статье описывается сквозная проверка подлинности Azure Active Directory (Azure AD) и ее применение для входа в Azure AD c помощью проверки пользовательских паролей в локальном каталоге Active Directory."
services: active-directory
keywords: "Что такое сквозная аутентификация Azure AD Connect, установка Active Directory, необходимые компоненты для Azure AD, единый вход"
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
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a>Вход пользователей с помощью сквозной проверки подлинности Azure Active Directory

## <a name="what-is-azure-active-directory-pass-through-authentication"></a>Что такое сквозная проверка подлинности Azure Active Directory?

Сквозная проверка подлинности Azure Active Directory (Azure AD) позволяет вашей toosign пользователей tooboth на локальном компьютере и облачными приложениями с помощью hello одинаковые пароли. Эта функция предоставляет пользователям для повышения удобства - один меньше tooremember пароль и уменьшает ИТ затраты на техническую поддержку, так как они менее вероятно tooforget как toosign в. Если пользователи выполняют вход с помощью Azure AD, эта функция проверяет пароли пользователей непосредственно в локальной службе Active Directory.

Эта функция является альтернативой слишком[синхронизация хэшей паролей Azure AD](active-directory-aadconnectsync-implement-password-synchronization.md), который предоставляет hello же преимущества tooorganizations облачной проверки подлинности. Тем не менее политик безопасности и соответствия требованиям в некоторых организациях не пропускать эти организации toosend паролей, даже в хэшированном за пределами их внутренней границы. Сквозная проверка подлинности — hello верное решение для таких организаций.

![Сквозная аутентификация Azure AD](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

Сквозная проверка подлинности можно объединять с hello [прозрачную Single Sign-On](active-directory-aadconnect-sso.md) компонентов. Таким образом, когда пользователи получают доступ к приложениям на корпоративных компьютерах в корпоративной сети, они не должны tootype в toosign свои пароли в.

>[!IMPORTANT]
>Сквозная проверка подлинности Azure AD доступна в предварительной версии.

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a>Основные преимущества сквозной проверки подлинности Azure AD

- *Удобство работы для пользователей*
  - Пользователи используют hello же toosign паролей в локальных и облачных приложений.
  - Пользователи Сократите затраты времени на взаимодействии toohello ИТ-поддержки и устранения проблем, связанных с паролем.
  - Пользователи могут заполнять [управление паролем самообслуживания](../active-directory-passwords-overview.md) задач в облаке hello.
- *Легко toodeploy & администрирования*
  - Не требуются сложные локальные развертывания или настройка сети.
  - Требуется просто toobe упрощенных агент устанавливается на предприятии.
  - Отсутствие накладных расходов на управление. агент Hello автоматически получает усовершенствования и исправления ошибок.
- *Безопасность*
  - Локальные пароли никогда не сохраняются в облаке hello в любой форме.
  - агент Hello только устанавливает исходящие подключения из сети. Таким образом нет отсутствует требование tooinstall hello агент в сети периметра, также называемой DMZ.
  - Защита учетных записей пользователей благодаря взаимодействию с [политиками условного доступа Azure AD](../active-directory-conditional-access-azure-portal.md), включая Многофакторную Идентификацию (MFA), и [фильтрации атак методом подбора пароля](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).
- *Высокая доступность*
  - Можно установить дополнительные агенты на нескольких локальных серверов tooprovide высокого уровня доступности запросов на вход в.

## <a name="feature-highlights"></a>Краткие сведения о возможностях

- Поддерживает вход пользователей во все браузерные приложения и клиентские приложения Microsoft Office, которые используют [современную проверку подлинности](https://aka.ms/modernauthga).
- Имена входа пользователей могут быть либо имя пользователя по умолчанию hello в локальной среде (`userPrincipalName`) или другой атрибут, настроенные в Azure AD Connect (известный как `Alternate ID`).
- функция Hello работает вместе с [условного доступа](../active-directory-conditional-access.md) функции, такие как многофакторная проверка подлинности (MFA) toohelp защитить пользователей.
- Среды с несколькими лесами поддерживаются, если между лесами AD существуют отношения доверия и правильно настроена маршрутизация по суффиксу имени.
- Это бесплатная функция, и любые платных выпусков toouse Azure AD не нужно его.
- Функцию можно включить с помощью [Azure AD Connect](active-directory-aadconnect.md).
- Она использует агент упрощенных в локальной среде, который прослушивает и отвечает на запросы проверки toopassword.
- Установка нескольких агентов обеспечивает высокий уровень доступности запросов на вход.
- Он [защищает](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) счетам локальные атаки методом принудительно атак пароль в облаке hello.

## <a name="next-steps"></a>Дальнейшие действия

- [**Краткое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-quick-start.md). Настройка и подготовка к работе сквозной проверки подлинности Azure Active Directory.
- [**Текущие ограничения**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) — эта функция в настоящее время находится на стадии предварительной версии. Узнайте, какие сценарии поддерживаются, а какие нет.
- [**Техническое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-how-it-works.md). Сведения о том, как работает эта функция.
- [**Часто задаваемые вопросы** ](active-directory-aadconnect-pass-through-authentication-faq.md) -ответы на вопросы и ответы toofrequently.
- [**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.
- [**Простой единый вход Azure Active Directory**](active-directory-aadconnect-sso.md). Дополнительные сведения об этой дополнительной функции.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.
