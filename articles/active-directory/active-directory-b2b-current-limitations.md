---
title: "aaaLimitations совместной работы Azure Active Directory B2B | Документы Microsoft"
description: "Текущие ограничения службы совместной работы Azure Active Directory B2B."
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a>Ограничения службы совместной работы Azure Active Directory B2B
Совместная работа Azure Active Directory (Azure AD) B2B сейчас субъекта toohello ограничения, описанные в этой статье.

## <a name="possible-double-multi-factor-authentication"></a>Возможное дублирование Многофакторной идентификации
С помощью Azure AD B2B можно применять многофакторную проверку подлинности на hello организации по ресурсам (hello приглашении организации). Hello причины такой подход подробно описаны в [условный доступ для совместной работы пользователей B2B](active-directory-b2b-mfa-instructions.md). Если партнер уже многофакторной проверки подлинности и применяются, их пользователи могут иметь проверки подлинности hello tooperform один раз в домашней организации и затем снова в указанное имя.

## <a name="instant-on"></a>Мгновенное включение
В потоках hello B2B совместной работы добавьте каталог toohello пользователей и динамически обновлять их во время активации приглашения, назначение приложения и т. д. Hello обновления записи обычно происходят в один каталог экземпляра и должны быть реплицированы на всех экземплярах. Репликация будет завершена после обновления всех экземпляров. Иногда при hello объекта записывается или обновлены в одном экземпляре и hello вызовите tooretrieve этого объекта — tooanother экземпляр, могут возникнуть задержки репликации. В этом случае обновите или повторите toohelp. При создании приложения с помощью наших API, а затем повторные попытки с некоторыми отсрочки является tooalleviate хорошим и защитного практике эту проблему.

## <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Свойства пользователя службы совместной работы Azure Active Directory B2B](active-directory-b2b-user-properties.md)
* [Добавление роли пользователя tooa B2B совместной работы](active-directory-b2b-add-guest-to-role.md)
* [Делегирование приглашений для службы совместной работы Azure Active Directory B2B](active-directory-b2b-delegate-invitations.md)
* [Динамические группы и служба совместной работы Azure Active Directory B2B](active-directory-b2b-dynamic-groups.md)
* [Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B](active-directory-b2b-code-samples.md)
* [Настройка приложений SaaS для службы совместной работы B2B](active-directory-b2b-configure-saas-apps.md)
* [Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B](active-directory-b2b-user-token.md)
* [Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory](active-directory-b2b-claims-mapping.md)
* [Доступ внешних пользователей к Office 365](active-directory-b2b-o365-external-user.md)
