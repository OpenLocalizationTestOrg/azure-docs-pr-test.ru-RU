---
title: "aaaDevelop приложений для Azure AD | Документы Microsoft"
description: "Предназначено для ИТ-специалистов hello, в этой статье рекомендации по интеграции с Active Directory приложения Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>Разработка бизнес-приложений для Azure Active Directory
Это руководство предоставляет сведения о разработке бизнес-приложений (LoB) для Azure Active Directory (AD) .hello нужной аудитория — Глобальные администраторы Active Directory и Office 365.

## <a name="overview"></a>Обзор
Создание приложений, интегрированных с Azure AD, предоставляет пользователям в вашей организации возможность единого входа в Office 365. Наличие приложения hello в Azure AD позволяет управлять hello политики проверки подлинности для приложения hello. Дополнительные сведения о условного доступа и tooprotect приложений с помощью многофакторной проверки подлинности (MFA). в статье toolearn [Настройка правил доступа](active-directory-conditional-access-azuread-connected-apps.md).

Зарегистрируйте toouse вашего приложения Azure Active Directory. Регистрации приложения hello означает, что разработчики могут использовать tooauthenticate пользователи Azure AD и запрос доступа к ресурсам toouser, например по электронной почте, календарю и документы.

Любой член каталога (не являющийся гостем) может зарегистрировать приложение, данный процесс также называется *созданием объекта приложения*.

Регистрация приложения позволяет любого пользователя toodo hello следующего:

* получение для своего приложения удостоверения, которое распознается Azure AD;
* Получить лицензию или дополнительные секреты и ключи, которые hello приложения можно использовать tooauthenticate самого tooAD
* Приложение hello фирменной символики в hello портал Azure с пользовательское имя, эмблемы, и т. д.
* Применить приложения tootheir функции авторизации Azure AD, включая:

  * Управление доступа на основе ролей
  * Azure Active Directory в качестве сервера авторизации oAuth (безопасный интерфейс API, предоставляемые приложением hello)
* Объявите необходимые разрешения необходимые для toofunction приложения hello, как ожидалось, включая:

      - 1. Разрешения приложения (только глобальные администраторы). Например: членство в роли в другой Azure AD приложения или роли членства относительный tooan ресурсов, группы ресурсов Azure, или подписки
      - 2. Делегированные разрешения (любой пользователь). Например: Azure AD, вход и чтение профиля.

> [!NOTE]
> По умолчанию любой член может зарегистрировать приложение. toolearn toorestrict разрешения для регистрации приложений toospecific членов, в статье [способ добавления приложений tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).
>
>

Ниже приведен теми, которые, глобальный администратор hello, требуется разработчики toohelp toodo подготовить свои приложения для производства.

* настройка правил доступа (политика доступа и многофакторная проверка подлинности);
* Настройте назначение пользователя toorequire приложение hello и назначить пользователей
* Отключение взаимодействие согласия пользователя по умолчанию hello

## <a name="configure-access-rules"></a>Настройка правил доступа
Настройка приложений SaaS tooyour правила доступа на уровне приложения. Например можно требовать многофакторную проверку Подлинности или разрешить доступ toousers только в надежных сетях. Hello сведения для этого доступны в документе hello [Настройка правил доступа](active-directory-conditional-access-azuread-connected-apps.md).

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>Настройте назначение пользователя toorequire приложение hello и назначить пользователей
По умолчанию пользователи могут получить доступ к приложениям без назначения. Тем не менее если приложение hello предоставляет доступ к роли или если требуется tooappear приложения hello на пользовательской панели доступа, вам требуется назначение пользователей.

[Требование назначения пользователей](active-directory-applications-guiding-developers-requiring-user-assignment.md)

Если вы являетесь подписчиком Azure AD Premium или Enterprise Mobility Suite (EMS), то настоятельно рекомендуется использовать группы. Назначение группы toohello приложения позволяет toodelegate управления постоянный доступ toohello владельца группы hello. Можно создать группы hello, или попросите Ответственный субъект hello в вашей организации toocreate hello группы с помощью механизма управления вашей группы.

[Назначение пользователей tooan приложения](active-directory-applications-guiding-developers-assigning-users.md)  
[Назначение группы tooan приложения](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>Упрощение процедуры получения согласия пользователей
По умолчанию каждый пользователь проходит через toosign взаимодействие согласия в. взаимодействие согласия Hello, запросом toogrant пользователям разрешения на доступ приложения tooan может сбить с толку для пользователей, не знакомых с таких решений.

Для приложений, которым вы доверяете можно упростить взаимодействие с пользователем hello, соглашаетесь toohello приложения от имени вашей организации.

Дополнительные сведения о согласие пользователя и hello согласия в Azure качества программного обеспечения см. в разделе [интеграция приложений с Azure Active Directory](active-directory-integrating-applications.md).

## <a name="related-articles"></a>Связанные статьи
* [Включение безопасного удаленного доступа tooon локальные приложения с помощью прокси приложения Azure AD](active-directory-application-proxy-get-started.md)
* [Предварительная версия Azure условного доступа для приложений SaaS](active-directory-conditional-access-azuread-connected-apps.md)
* [Управление tooapps доступ с помощью Azure AD](active-directory-managing-access-to-apps.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
