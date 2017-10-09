---
title: "aaaCompare B2B совместной работы и B2C в Azure Active Directory | Документы Microsoft"
description: "Что такое hello разницу между совместной работы Azure Active Directory B2B и Azure AD B2C"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>Сравнение службы совместной работы B2B и B2C в Azure Active Directory

Совместная работа Azure Active Directory (Azure AD) B2B и Azure AD B2C позволяют toowork с внешними пользователями в Azure AD. Но чем они отличаются?


Возможности службы совместной работы B2B |     Изолированное предложение Azure AD B2C
-------- | --------
Предназначен для: организаций, которые пользователи могут tooauthenticate toobe от организации-партнера, независимо от поставщика удостоверений. | Назначение: приглашение в Azure AD пользователей мобильных приложений и веб-приложений, как отдельных клиентов, так и учреждений или организаций.
Поддерживаемые удостоверения: сотрудники с рабочим или учебными учетными записями, партнеры с рабочим или учебными учетными записями или любой адрес электронной почты. Скоро toosupport прямой федерации.  | Поддерживаемые удостоверения: потребители с учетными записями в локальных приложениях (любой адрес электронной почты или имя пользователя) или какой-либо поддерживаемый внешний идентификатор с прямой федерацией.
Каталог hello партнера пользователей, находящихся в: партнера пользователей из внешних организаций hello осуществляется в специально hello же каталоге, что сотрудники, но заметками. Ими можно управлять hello таким же способом, как сотрудники, может быть добавлены toohello одну группу и так далее  | Каталог hello клиента пользовательские сущности, присутствующие в: В каталоге приложения hello. Управлять отдельно от hello сотрудников и партнеров каталога организации (если таковые имеются.
Единый вход (SSO) tooall Azure поддерживается AD подключенных приложений. Например чтобы обеспечить доступ tooOffice 365 или локальных приложений и tooother приложений SaaS, таких как Salesforce рабочего дня.  |  Toocustomer единого входа, которым владеет приложений в клиентах Azure AD B2C hello поддерживается. SSO tooOffice 365 или tooother приложений Майкрософт и SaaS, отличных от Microsoft не поддерживается.
Жизненный цикл партнера: управляется hello приглашении организации или узла.  | Жизненный цикл клиента: самообслуживание или управляемого приложения hello.
Политика безопасности и соответствия: управляется hello приглашении организации или узла.  | Политика безопасности и соответствия: под управлением приложения hello.
Фирменная символика: используется торговая марка основной или приглашающей организации.  |    Фирменная символика: управление приложением. Обычно, как правило, продукт toobe типизированной со постепенно организации hello в фоновой hello.
Дополнительные сведения: [запись блога](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [документация](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b).  | Дополнительные сведения: [страница продукта](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [документация](https://docs.microsoft.com/en-us/azure/active-directory-b2c/).


### <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Свойства пользователя службы совместной работы Azure Active Directory B2B](active-directory-b2b-user-properties.md)
* [Добавление роли пользователя tooa B2B совместной работы](active-directory-b2b-add-guest-to-role.md)
* [Делегирование приглашений для службы совместной работы Azure Active Directory B2B](active-directory-b2b-delegate-invitations.md)
* [Динамические группы и служба совместной работы Azure Active Directory B2B](active-directory-b2b-dynamic-groups.md)
* [Настройка приложений SaaS для службы совместной работы B2B](active-directory-b2b-configure-saas-apps.md)
* [Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B](active-directory-b2b-user-token.md)
* [Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory](active-directory-b2b-claims-mapping.md)
* [Доступ внешних пользователей к Office 365](active-directory-b2b-o365-external-user.md)
* [Текущие ограничения службы совместной работы Azure Active Directory B2B](active-directory-b2b-current-limitations.md)
* [Получение поддержки для службы совместной работы B2B](active-directory-b2b-support.md)
