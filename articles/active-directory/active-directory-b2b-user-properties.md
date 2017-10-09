---
title: "aaaProperties совместной работы пользователя Azure Active Directory B2B | Документы Microsoft"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Свойства пользователя службы совместной работы Azure Active Directory B2B

В Azure Active Directory B2B (бизнес — бизнес) пользователем службы совместной работы называется пользователь с гостевой учетной записью (UserType = Guest). Как правило, этого пользователя guest из партнерской организации и предоставлены ограниченные права в приглашении каталога, по умолчанию hello.

В зависимости от hello приглашение с потребностями организации совместной работы пользователя с Azure AD B2B может находиться в одном из hello следующие состояния учетной записи:

- Состояние 1: Расположенные на внешнем экземпляре Azure AD и представленные в виде существование пользователя guest в приглашении организации hello. В этом случае hello B2B входе пользователя с учетной записью Azure AD, к которому относится приглашены toohello клиента. Если hello партнерская организация не использует Azure AD, по-прежнему создается hello пользователя guest в Azure AD. Hello требования, что они активировать их приглашения и Azure AD проверяет свой адрес электронной почты. Такой подход также называется JIT-клиентом или вирусным клиентом.

- Состояние 2: Находящуюся в учетной записи Майкрософт и представленные в виде существование пользователя guest в организации hello узла. В этом случае hello гостевой пользователь выполняет вход с учетной записью Майкрософт. Hello приглашены социальных удостоверение пользователя (google.com или аналогичные), который не является учетной записью Майкрософт, создается как учетная запись Майкрософт во время активации предложения.

- Состояния 3: Находящуюся в Active Directory в локальной организации узла hello и синхронизированы с Azure hello узла организации AD. Во время этой версии необходимо использовать PowerShell toomanually изменение hello UserType таких пользователей в облаке hello.

- Состояние 4: Находящуюся в узле организации Azure AD с помощью UserType = гостевых систем и учетные данные, которыми управляет организация узла hello.

  ![Отображение инициалы приглашающего hello](media/active-directory-b2b-user-properties/redemption-diagram.png)


Теперь давайте рассмотрим, как в Azure AD выглядит пользователь службы совместной работы Azure AD B2B с состоянием 1.

### <a name="before-invitation-redemption"></a>До активации приглашения

![До активации предложения](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>После активации приглашения

![После активации предложения](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>Ключевые свойства пользователя совместной работы Azure AD B2B hello
### <a name="usertype"></a>UserType
Это свойство указывает связь hello hello пользователя toohello узла аренду. Оно может иметь два значения:
- Элемент: Это значение указывает сотрудник организации узла hello и пользователь в организации hello заработной платы. Например этот пользователь ожидает toohave доступ только для toointernal узлов. Этот пользователь не должен считаться внешним сотрудником.

- Гость: Это значение указывает пользователь, который не считается внутренней toohello компании, например внешнего участника совместной работы, партнера, клиента или аналогичные пользователя. Такой пользователь не быть ожидаемым tooreceive внутреннего типа memo Директора или получения преимуществ компании, например.

  > [!NOTE]
  > Hello UserType имеет нет отношения toohow hello пользователь выполняет вход, hello роли каталога пользователя hello и т. д. Просто это свойство указывает hello связь toohello узла организация пользователя и позволяет организации hello tooenforce политики, которые зависят от этого свойства.

### <a name="source"></a>Источник
Это свойство указывает, каким образом hello входе пользователя в систему.

- Приглашенный пользователь. Это пользователь, который был приглашен, но еще не активировал свое приглашение.

- Внешних Active Directory: Этот пользователь расположенные на внешних организаций и выполняет проверку подлинности с помощью учетной записи Azure AD, к которому относится toohello другой организации. Этот тип входа в систему, соответствует tooState 1.

- Учетная запись Майкрософт. У этого пользователя есть учетная запись Майкрософт, которую он использует для проверки подлинности. Этот тип входа в систему, соответствует tooState 2.

- Windows Server Active Directory: Этого пользователя является вход из локальной Active Directory, к которому относится toothis организации. Этот тип входа в систему, соответствует tooState 3.

- Azure Active Directory: Этот пользователь проходит проверку подлинности с помощью учетной записи Azure AD, к которому относится toothis организации. Этот тип входа в систему, соответствует tooState 4.
  > [!NOTE]
  > Свойства Source и UserType не зависят друг от друга. Значение атрибута Source не подразумевает определенного значения UserType.

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>Можно ли добавить пользователей Azure AD B2B в качестве участников (Member), а не гостей (Guest)?
Как правило, понятия "пользователь службы Azure AD B2B" и "гостевой пользователь" являются синонимами. Поэтому пользователь службы совместной работы Azure AD B2B по умолчанию добавляется как гостевой пользователь (UserType = Guest). Однако в некоторых случаях hello партнерской организации является членом более крупной организации toowhich hello узла организации также входит. В этом случае hello узле организации может возникнуть tootreat пользователей в партнерской организации hello в качестве членов вместо гостевых систем. Используйте API-интерфейсов Azure AD B2B приглашение диспетчера tooadd hello или пригласить пользователя из hello партнерской организации toohello узла организации в качестве члена.

## <a name="filter-for-guest-users-in-hello-directory"></a>Фильтр для гостевых пользователей в каталоге hello

![Фильтрация гостевых пользователей](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>Преобразование UserType
В настоящее время существует возможность для пользователей tooconvert UserType из tooGuest члена и наоборот с помощью PowerShell. Однако hello Свойство UserType должен организация toohello отношения пользователя toorepresent hello. Таким образом hello значение этого свойства следует изменять только в том случае, если изменяется связь hello hello пользователя toohello организации. Если изменяется связь hello hello пользователя, следует проблем, например, следует ли изменить hello имя участника-пользователя (UPN), можно обращаться? Hello пользователя продолжать toohello доступа toohave столько же ресурсов? Нужно ли назначить почтовый ящик? Таким образом изменения hello UserType с помощью PowerShell как atomic действие не рекомендуется. Кроме того, мы советуем не полагаться на использование этого свойства, так как возможность его изменять с помощью PowerShell может быть отключена.

## <a name="remove-guest-user-limitations"></a>Снятие ограничений для гостевых пользователей
Возможны ситуации, место toogive более высокие привилегии пользователей гостя. Можно добавить роль пользователя tooany гостевой и даже удалять ограничения пользователей гостя по умолчанию hello в каталоге toogive hello hello пользователя, одинаковыми правами как члены.

Это возможно tooturn отключение ограничения пользователей гостя по умолчанию hello, чтобы имея существование пользователя guest в каталоге компании hello hello одинаковые разрешения имени пользователя члена.

![Снятие ограничений для гостевых пользователей](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Добавление роли пользователя tooa B2B совместной работы](active-directory-b2b-add-guest-to-role.md)
* [Делегирование приглашений для службы совместной работы Azure Active Directory B2B](active-directory-b2b-delegate-invitations.md)
* [Auditing and reporting a B2B collaboration user](active-directory-b2b-auditing-and-reporting.md) (Аудит и создание отчетов для пользователей службы совместной работы B2B)
* [Динамические группы и служба совместной работы Azure Active Directory B2B](active-directory-b2b-dynamic-groups.md)
* [Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B](active-directory-b2b-code-samples.md)
* [Настройка приложений SaaS для службы совместной работы B2B](active-directory-b2b-configure-saas-apps.md)
* [Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B](active-directory-b2b-user-token.md)
* [Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory](active-directory-b2b-claims-mapping.md)
* [Доступ внешних пользователей к Office 365](active-directory-b2b-o365-external-user.md)
* [Текущие ограничения службы совместной работы Azure Active Directory B2B](active-directory-b2b-current-limitations.md)
