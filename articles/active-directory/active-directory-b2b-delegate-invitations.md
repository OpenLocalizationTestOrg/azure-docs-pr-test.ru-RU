---
title: "aaaDelegate приглашения для совместной работы Azure Active Directory B2B | Документы Microsoft"
description: "Свойства пользователя службы совместной работы Azure Active Directory B2B можно настраивать."
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
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Делегирование приглашений для службы совместной работы Azure Active Directory B2B

В сотрудничестве бизнес бизнес (B2B) Azure Active Directory (Azure AD) у вас toobe приглашения toosend глобального администратора. Вместо этого можно использовать политики и делегировать toousers приглашения, роли которой разрешить их toosend приглашения. Важные новый способ toodelegate гостевой пользователь приглашения выполняется с помощью роли приглашающего гостевой hello.

## <a name="guest-inviter-role"></a>Роль Guest Inviter
Можно назначить пользователя tooGuest hello приглашающего роли toosend приглашения. У вас нет toobe членом приглашения toosend роли глобального администратора hello. По умолчанию обычных пользователей можно также вызвать API приглашения hello глобального администратора отключить приглашения для обычных пользователей. Пользователь также может вызвать API hello, с помощью портала Azure hello или PowerShell.

Ниже приведен пример, в котором показано, как tooadd PowerShell toouse toohello гостевой приглашающего роль пользователя:

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>Управление пользователями, имеющими разрешение на приглашение

![Элемент управления как tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

С совместной работы Azure AD B2B администратор клиента можно задать следующие политики приглашения hello.

- отключение приглашений;
- Только администраторы и пользователи с ролью гостя приглашающего hello можно пригласить
- Администраторы, роль гостя приглашающего hello и члены можно пригласить
- приглашать могут все пользователи, включая гостей.

По умолчанию, клиенты настроены слишком № 4. (приглашать пользователей B2B могут все пользователи, включая гостей).

## <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Свойства пользователя службы совместной работы Azure Active Directory B2B](active-directory-b2b-user-properties.md)
* [Добавление роли пользователя tooa B2B совместной работы](active-directory-b2b-add-guest-to-role.md)
* [Динамические группы и служба совместной работы Azure Active Directory B2B](active-directory-b2b-dynamic-groups.md)
* [Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B](active-directory-b2b-code-samples.md)
* [Настройка приложений SaaS для службы совместной работы B2B](active-directory-b2b-configure-saas-apps.md)
* [Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B](active-directory-b2b-user-token.md)
* [Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory](active-directory-b2b-claims-mapping.md)
* [Доступ внешних пользователей к Office 365](active-directory-b2b-o365-external-user.md)
* [Текущие ограничения службы совместной работы Azure Active Directory B2B](active-directory-b2b-current-limitations.md)
