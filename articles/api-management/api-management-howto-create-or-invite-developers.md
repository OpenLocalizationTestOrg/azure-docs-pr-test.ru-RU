---
title: "aaaHow управление учетными записями пользователей в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toocreate или приглашения пользователей в службе управления API Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a>Как toomanage учетные записи в службе управления API Azure
В службе управления API разработчики, пользователи hello hello API-интерфейсы, доступ к которым предоставляется с помощью API-интерфейса управления. Это руководство по показано toohow toocreate и приглашения разработчики toouse hello API-интерфейсов и сделать доступной toothem, API управления экземпляром продуктов. Сведения об управлении учетными записями пользователей программным образом см hello [сущности пользователя](https://msdn.microsoft.com/library/azure/dn776330.aspx) документации в hello [API REST управления](https://msdn.microsoft.com/library/azure/dn776326.aspx) ссылки.

## <a name="create-developer"> </a>Создание нового разработчика
Щелкните toocreate нового разработчика **портал издателя** в hello портала Azure для службы управления API. Откроется портал издателя управления API toohello. Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.

![Портал издателя][api-management-management-console]

Нажмите кнопку **пользователей** из hello **API управления** меню hello слева, а затем нажмите **добавить пользователя**.

![Создание разработчика][api-management-create-developer]

Введите hello **электронной почты**, **пароль**, и **имя** для новых разработчиков hello и нажмите кнопку **Сохранить**.

![Создание разработчика][api-management-add-new-user]

По умолчанию, являются учетными записями разработчиков в только что созданный **Active**и связанные с hello **разработчики** группы.

![Новый разработчик][api-management-new-developer]

Разработчик учетные записи, которые **active** состояние можно использовать tooaccess все API-интерфейсы hello, для которого имеются подписки. developer Привет только что созданный tooassociate дополнительными группами в разделе [как tooassociate группирует с разработчиками][How tooassociate groups with developers].

## <a name="invite-developer"> </a>Приглашение разработчика
Щелкните tooinvite разработчик, **пользователей** из hello **API управления** меню hello слева, а затем нажмите **пригласить пользователя**.

![Приглашение разработчика][api-management-invite-developer]

Введите hello имя и адрес электронной почты hello разработчика и нажмите кнопку **пригласить**.

![Приглашение разработчика][api-management-invite-developer-window]

Отображается сообщение с подтверждением, но разработчик вновь приглашены hello не отображается в списке hello до, после принятия приглашения hello. 

![Подтверждение приглашения][api-management-invite-developer-confirmation]

Когда разработчик приглашение, сообщение электронной почты отправляется toohello разработчика. Это сообщение создается с помощью шаблона и может настраиваться. Дополнительные сведения см. в разделе [Настройка почтовых шаблонов][Configure email templates].

После принятия приглашения hello hello учетная запись становится активным.

## <a name="block-developer"> </a> Деактивация или повторная активация учетной записи разработчика
По умолчанию недавно созданные или приглашенные учетные записи разработчика являются **активными**. Нажмите кнопку toodeactivate учетной записью разработчика, **блок**. Щелкните tooreactivate учетной записью разработчика, заблокированных, **активировать**. Учетную запись разработчика заблокированных можно получить доступ к порталу developer Привет или не вызвать API. toodelete учетной записи пользователя, нажмите кнопку **удалить**.

![Блокировка разработчика][api-management-new-developer]

## <a name="reset-a-user-password"></a>Сброс пароля пользователя
tooreset hello пароль для учетной записи пользователя, щелкните имя hello hello учетной записи.

![Сброс пароля][api-management-view-developer]

Нажмите кнопку **сброс пароля** toosend tooreset ссылку toohello пользователя пароль.

![Сброс пароля][api-management-reset-password]

tooprogrammatically работы с учетными записями, в разделе hello [сущности пользователя](https://msdn.microsoft.com/library/azure/dn776330.aspx) документации в hello [API REST управления](https://msdn.microsoft.com/library/azure/dn776326.aspx) ссылки. tooreset пользователя учетной записи пароль tooa определенное значение, можно использовать hello [обновления пользователя](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) операцию и укажите пароль hello.

## <a name="pending-verification"></a>Ожидание проверки
![Ожидание проверки][api-management-pending-verification]

## <a name="next-steps"> </a>Дальнейшие действия
После создания учетной записи разработчика, можно связать его с ролями и подписаться его tooproducts и API-интерфейсы. Дополнительные сведения см. в разделе [как toocreate и использования групп][How toocreate and use groups].

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
