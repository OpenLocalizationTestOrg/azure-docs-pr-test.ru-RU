---
title: "портал регистрации aaaSelf службы для совместной работы Azure Active Directory B2B | Документы Microsoft"
description: "Совместная работа Azure Active Directory B2B поддерживает связей между компаниями, позволяя корпоративным приложениям доступа tooselectively деловых партнеров"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Самостоятельная регистрация на портале для службы совместной работы Azure AD B2B

Клиент может выполнить много с hello встроенных функций, предоставляемых через наших ИТ-администратору [портал Azure](https://portal.azure.com) и на нашем [панели доступа приложения](https://myapps.microsoft.com) для конечных пользователей. Но мы также помнить, что бизнеса требуется рабочего процесса адаптации hello toocustomize для B2B пользователей toofit их с требованиями организации. Они могут это сделать с помощью [нашего интерфейса API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).

Обсуждая этот вопрос с нашими клиентами, мы выяснили, что есть одна общая потребность, которая преобладает над всеми остальными. Hello приглашении организации может не знать заранее, кто hello пребывание, требуется доступ к ресурсам tootheir отдельных внешними участниками. Нужно было способом для пользователей от компаний-партнеров слишком зарегистрироваться сами набор политик, hello приглашении организации элементов управления. Такой сценарий можно реализовать с помощью наших API-интерфейсов, что мы и сделали в опубликованном на GitHub проекте: [пример проекта на портале GitHub](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

Наш проект Github показан способ организации можно использовать нашими API и предоставляют возможность регистрации на основе политик, самообслуживания для их доверенных партнеров, с помощью правила, определяющие приложения hello, они могут получить доступ. Партнер пользователи могут получить tooresources доступ, им необходимы, безопасно, без необходимости hello приглашении освоить toomanually организации их. Можно легко развернуть проект hello в подписку Azure по своему усмотрению.

## <a name="as-is-code"></a>Код "как есть"

Помните, что этот код предоставляется для использования toodemonstrate образец hello Azure Active Directory B2B приглашения API. Перед развертыванием в рабочем сценарии его должна настроить и проверить ваша команда разработчиков или ваш партнер.

## <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:
* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?](active-directory-b2b-admin-add-users.md)
* [Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?](active-directory-b2b-iw-add-users.md)
* [элементы Hello hello электронное приглашение B2B совместной работы](active-directory-b2b-invitation-email.md)
* [Активация приглашения службы совместной работы B2B](active-directory-b2b-redemption-experience.md)
* [Руководство по лицензированию службы совместной работы Azure Active Directory B2B](active-directory-b2b-licensing.md)
* [Устранение неполадок службы совместной работы Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B](active-directory-b2b-faq.md)
* [Многофакторная идентификация для пользователей службы совместной работы B2B](active-directory-b2b-mfa-instructions.md)
* [Добавление пользователей службы совместной работы B2B без приглашения](active-directory-b2b-add-user-without-invite.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)