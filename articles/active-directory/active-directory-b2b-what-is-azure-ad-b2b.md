---
title: "aaaWhat возможности совместной работы Azure Active Directory B2B | Документация Майкрософт"
description: "Совместная работа Azure Active Directory B2B поддерживает связей между компаниями, включив деловых партнеров tooselectively доступ к корпоративным приложениям."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: 359989b66f3d012c306e8748a607662fffacb919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a>Что такое служба совместной работы Azure AD B2B

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

Возможности (B2B) совместной работы Azure AD бизнес-включить любой организации, с помощью Azure AD toowork безопасно и надежно с пользователями из любую другую организацию, крупных или мелких. наличия Azure AD и даже наличия ИТ-отдела. 

Организации с помощью Azure AD могут предоставлять доступ партнеров tootheir toodocuments, ресурсам и приложениям, сохраняя полный контроль над корпоративных данных. Разработчики могут использовать приложения toowrite API-интерфейсы бизнес-hello Azure AD, объединяющие две организации в более безопасно. Кроме того это довольно просто для toonavigate конечных пользователей.

97% наших клиентов просили, что очень важно toothem совместной работы Azure AD B2B.

![круговая диаграмма](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

По состоянию на начало апреля 2017 года приблизительно 3 миллиона пользователей уже применяли возможности совместной работы Azure AD B2B. Более 23 % организаций со службой Azure AD и числом пользователей более 10 уже применяют эти возможности.

## <a name="hello-key-benefits-of-azure-ad-b2b-collaboration-tooyour-organization"></a>Основные преимущества Hello организации tooyour совместной работы Azure AD B2B

### <a name="work-with-any-user-from-any-partner"></a>Работа с любым пользователем из любой партнерской организации

* Партнеры используют собственные учетные данные

* Не требуется для партнеров toouse Azure AD

* Не требуются внешние каталоги или сложная настройка

### <a name="simple-and-secure-collaboration"></a>Простая и безопасная совместная работа

* Предоставить доступ tooany корпоративному приложению или данных, при применении сложных, Azure AD энергопотреблением политики авторизации

* Простое использование

* Безопасность корпоративного уровня для приложений и данных

### <a name="no-management-overhead"></a>Отсутствие накладных расходов на управление

* Не требуется управлять внешними учетными записями или паролями

* Не требуется синхронизировать учетные записи или управлять их жизненным циклом вручную

* Отсутствие накладных расходов на внешнее администрирование

## <a name="you-can-easily-add-b2b-collaboration-users-tooyour-organization"></a>Можно легко добавить B2B совместной работы пользователей tooyour организации

Администраторы могут добавить пользователей совместной работы (гостевая) B2B на hello [портал Azure](https://portal.azure.com).

![добавление гостевых пользователей](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-toobring-their-own-identity"></a>Включить собственные удостоверения вашей toobring участники совместной работы

Партнеры B2B могут выполнять вход, используя удостоверения на свой выбор. Если пользователь hello не имеет учетной записи Майкрософт или учетную запись Azure AD, он будет создан для них без проблем во время hello для активации предложения.

![выбор удостоверения для входа](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-tooapplication-and-group-owners"></a>Владельцы делегат tooapplication и группы 
Приложения и владельцев группы можно добавлять пользователей B2B непосредственно tooany приложения, который вас интересует, как приложение Microsoft, так и не. Администраторы могут делегировать B2B пользователям разрешение tooadd toonon администраторов. Администраторы не могут использовать hello [панели доступа приложения Azure AD](https://myapps.microsoft.com) tooadd B2B tooapplications совместной работы пользователей или групп.

![панель доступа](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![добавление участника](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a>Защита корпоративного содержимого с помощью политик авторизации

Вы можете применить политики условного доступа, например многофакторную проверку подлинности на следующих уровнях:
- На уровне клиента hello
- На уровне приложения hello
- Для определенных пользователей tooprotect корпоративным приложениям и данным

![добавление участника](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-tooeasily-build-applications-tooonboard"></a>Используйте наши API-интерфейсы и образец кода tooeasily построения приложений tooonboard
Переведите внешними партнерами на них в способов настроенные tooyour с потребностями организации.

С помощью hello [приглашения совместной работы B2B API-интерфейсы](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), вы можете настроить своими впечатлениями адаптации, включая создание порталы самообслуживания, регистрации. В [GitHub](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) вы найдете образец кода для этого портала.

![портал регистрации](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

С совместной работы Azure AD B2B можно получить все возможности Azure AD tooprotect hello связей партнера в результате которого пользователи найти легко и интуитивно понятно. Поэтому действуйте, соединения hello тысяч организаций, которые уже используют Azure AD B2B для совместной работы в их внешних!

## <a name="next-steps"></a>Дальнейшие действия

* Возможности администратора находятся в hello [портал Azure](https://portal.azure.com).

* Опыт работника сведения доступны в hello [панели доступа](https://myapps.microsoft.com).

* И как всегда, связь с группой разработчиков hello за любые отзывы, обсуждения и предложения по нашей [Технический сообщества Майкрософт](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).

Другие статьи о службе совместной работы Azure AD B2B:

* [Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?](active-directory-b2b-admin-add-users.md)
* [Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?](active-directory-b2b-iw-add-users.md)
* [элементы Hello hello электронное приглашение B2B совместной работы](active-directory-b2b-invitation-email.md)
* [Активация приглашения службы совместной работы B2B](active-directory-b2b-redemption-experience.md)
* [Руководство по лицензированию службы совместной работы Azure Active Directory B2B](active-directory-b2b-licensing.md)
* [Устранение неполадок службы совместной работы Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B](active-directory-b2b-faq.md)
* [API службы совместной работы Azure Active Directory B2B и настройка](active-directory-b2b-api.md)
* [Многофакторная идентификация для пользователей службы совместной работы B2B](active-directory-b2b-mfa-instructions.md)
* [Добавление пользователей службы совместной работы B2B без приглашения](active-directory-b2b-add-user-without-invite.md)
* [Auditing and reporting a B2B collaboration user](active-directory-b2b-auditing-and-reporting.md) (Аудит и создание отчетов для пользователей службы совместной работы B2B)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
