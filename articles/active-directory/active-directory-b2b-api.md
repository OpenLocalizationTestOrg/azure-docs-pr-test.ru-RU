---
title: "aaaAzure Active Directory B2B API совместной работы и настройки | Документы Microsoft"
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>API службы совместной работы Azure Active Directory B2B и настройка

Имеется большое количество клиентов Расскажите, они должны toocustomize процесса приглашения hello в способом, который лучше всего подходит для своей организации. С помощью нашего интерфейса API это можно сделать. [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Возможности hello приглашения API
Hello API предоставляет следующие возможности hello.

1. Пригласите внешнего пользователя, используя *любой* адрес электронной почты.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. Настройте место вашей tooland пользователей после принятия приглашения их.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. Выберите toosend hello Стандартная приглашения почту через нам

    ```
    "sendInvitationMessage": true
    ```

  с toohello получатель сообщения, которые можно настроить

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. И выберите toocc: людей, которым tookeep в hello цикла вашей приглашение этого участника совместной работы.

5. Или полностью настроить приглашения и рабочий процесс адаптации, выбрав не toosend уведомления через Azure AD.

    ```
    "sendInvitationMessage": false
    ```

  В этом случае можно получить URL-адрес активации из hello API, который можно внедрить в шаблона сообщения электронной почты, обмена мгновенными Сообщениями или другим методом по своему усмотрению.

6. Наконец Если вы являетесь администратором, вы можете tooinvite hello пользователя как член.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>Модель авторизации
Hello API может работать в hello следующие режимы авторизации:

### <a name="app--user-mode"></a>Приложение + пользователь
В этом режиме, кто использует потребностей hello API toohave hello разрешения toobe создавать приглашения B2B.

### <a name="app-only-mode"></a>Только приложение
В контексте только приложения приложение hello должен hello User.ReadWrite.All или Directory.ReadWrite.All областей для toosucceed приглашения hello.

Дополнительные сведения: https://graph.microsoft.io/docs/authorization/permission_scopes


## <a name="powershell"></a>PowerShell
Он является теперь возможно toouse PowerShell tooadd приглашение внешних пользователей tooan организацией, легко. Создание с помощью командлета hello приглашение:

```
New-AzureADMSInvitation
```

Можно использовать следующие варианты hello.

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

Также можно проверить ссылку приглашения API hello в [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

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
