---
title: "aaaDynamic групп и совместной работы Azure Active Directory B2B | Документы Microsoft"
description: "Службу совместной работы Azure Active Directory B2B можно использовать с динамическими группами Azure AD."
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Динамические группы и служба совместной работы Azure Active Directory B2B

## <a name="what-are-dynamic-groups"></a>Что такое динамические группы?
Динамическая настройка членства в группах для Azure Active Directory (Azure AD) доступен в [hello портал Azure](https://portal.azure.com). Администраторы могут задать правила, которые toopopulate группы, созданные в Azure Active Directory на основе атрибутов пользователя (например, userType, отделу или страны). Элементы могут добавляться автоматически tooor удалены из группы безопасности на основе их атрибутов. Эти группы можно предоставить доступ tooapplications или облачные ресурсы (сайтов SharePoint, документы) и tooassign лицензирует toomembers. Дополнительные сведения о динамических групп см. в статье [Выделенные группы в Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).

Hello соответствующие [лицензирования Azure AD Premium P1 и P2](https://azure.microsoft.com/pricing/details/active-directory/) необходимые toocreate и использование динамических групп. Дополнительные сведения см. в статье hello [создавать правила на основе атрибутов для динамического членства в группе в Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-hello-built-in-dynamic-groups"></a>Что такое hello встроенных динамические группы?
Hello **всех пользователей** динамическая группа включает toocreate администраторов клиента, выберите группы, содержащей всех пользователей в клиенте hello с одним. По умолчанию hello **всех пользователей** группа включает всех пользователей в каталоге hello, включая элементы и гостевых систем.
Hello новый портал администрирования Azure Active Directory, можно выбрать tooenable hello **всех пользователей** в hello, просмотреть параметры группы.

![встроенные группы](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>Усиление hello все динамические группы пользователей
По умолчанию hello **всех пользователей** группа содержит также пользователей совместной работы (гостевая) B2B. Могут дополнительно обеспечить безопасность вашей **всех пользователей** группу с помощью правила tooremove гостевых пользователей. Hello ниже показан hello **всех пользователей** tooexclude Гости изменения группы.

![включение группы "Все пользователи"](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

Может также оказаться полезным toocreate новый динамическую группу, содержащую только гостевых пользователей, так, чтобы можно было применить toothem политики (такие как политики Azure AD условного доступа).
Как такая группа может выглядеть:

![исключение гостевых пользователей](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Свойства пользователя службы совместной работы Azure Active Directory B2B](active-directory-b2b-user-properties.md)
* [Добавление роли пользователя tooa B2B совместной работы](active-directory-b2b-add-guest-to-role.md)
* [Делегирование приглашений для службы совместной работы Azure Active Directory B2B](active-directory-b2b-delegate-invitations.md)
* [Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B](active-directory-b2b-code-samples.md)
* [Настройка приложений SaaS для службы совместной работы B2B](active-directory-b2b-configure-saas-apps.md)
* [Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B](active-directory-b2b-user-token.md)
* [Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory](active-directory-b2b-claims-mapping.md)
* [Доступ внешних пользователей к Office 365](active-directory-b2b-o365-external-user.md)
* [Текущие ограничения службы совместной работы Azure Active Directory B2B](active-directory-b2b-current-limitations.md)
