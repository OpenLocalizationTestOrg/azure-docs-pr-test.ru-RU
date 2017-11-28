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
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="5e523-103">Как toomanage учетные записи в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="5e523-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="5e523-104">В службе управления API разработчики, пользователи hello hello API-интерфейсы, доступ к которым предоставляется с помощью API-интерфейса управления.</span><span class="sxs-lookup"><span data-stu-id="5e523-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="5e523-105">Это руководство по показано toohow toocreate и приглашения разработчики toouse hello API-интерфейсов и сделать доступной toothem, API управления экземпляром продуктов.</span><span class="sxs-lookup"><span data-stu-id="5e523-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="5e523-106">Сведения об управлении учетными записями пользователей программным образом см hello [сущности пользователя](https://msdn.microsoft.com/library/azure/dn776330.aspx) документации в hello [API REST управления](https://msdn.microsoft.com/library/azure/dn776326.aspx) ссылки.</span><span class="sxs-lookup"><span data-stu-id="5e523-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="5e523-107"><a name="create-developer"> </a>Создание нового разработчика</span><span class="sxs-lookup"><span data-stu-id="5e523-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="5e523-108">Щелкните toocreate нового разработчика **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="5e523-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="5e523-109">Откроется портал издателя управления API toohello.</span><span class="sxs-lookup"><span data-stu-id="5e523-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="5e523-110">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="5e523-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="5e523-112">Нажмите кнопку **пользователей** из hello **API управления** меню hello слева, а затем нажмите **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="5e523-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![Создание разработчика][api-management-create-developer]

<span data-ttu-id="5e523-114">Введите hello **электронной почты**, **пароль**, и **имя** для новых разработчиков hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5e523-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![Создание разработчика][api-management-add-new-user]

<span data-ttu-id="5e523-116">По умолчанию, являются учетными записями разработчиков в только что созданный **Active**и связанные с hello **разработчики** группы.</span><span class="sxs-lookup"><span data-stu-id="5e523-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![Новый разработчик][api-management-new-developer]

<span data-ttu-id="5e523-118">Разработчик учетные записи, которые **active** состояние можно использовать tooaccess все API-интерфейсы hello, для которого имеются подписки.</span><span class="sxs-lookup"><span data-stu-id="5e523-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="5e523-119">developer Привет только что созданный tooassociate дополнительными группами в разделе [как tooassociate группирует с разработчиками][How tooassociate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="5e523-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="5e523-120"><a name="invite-developer"> </a>Приглашение разработчика</span><span class="sxs-lookup"><span data-stu-id="5e523-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="5e523-121">Щелкните tooinvite разработчик, **пользователей** из hello **API управления** меню hello слева, а затем нажмите **пригласить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="5e523-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![Приглашение разработчика][api-management-invite-developer]

<span data-ttu-id="5e523-123">Введите hello имя и адрес электронной почты hello разработчика и нажмите кнопку **пригласить**.</span><span class="sxs-lookup"><span data-stu-id="5e523-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![Приглашение разработчика][api-management-invite-developer-window]

<span data-ttu-id="5e523-125">Отображается сообщение с подтверждением, но разработчик вновь приглашены hello не отображается в списке hello до, после принятия приглашения hello.</span><span class="sxs-lookup"><span data-stu-id="5e523-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![Подтверждение приглашения][api-management-invite-developer-confirmation]

<span data-ttu-id="5e523-127">Когда разработчик приглашение, сообщение электронной почты отправляется toohello разработчика.</span><span class="sxs-lookup"><span data-stu-id="5e523-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="5e523-128">Это сообщение создается с помощью шаблона и может настраиваться.</span><span class="sxs-lookup"><span data-stu-id="5e523-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="5e523-129">Дополнительные сведения см. в разделе [Настройка почтовых шаблонов][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="5e523-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="5e523-130">После принятия приглашения hello hello учетная запись становится активным.</span><span class="sxs-lookup"><span data-stu-id="5e523-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="5e523-131"><a name="block-developer"> </a> Деактивация или повторная активация учетной записи разработчика</span><span class="sxs-lookup"><span data-stu-id="5e523-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="5e523-132">По умолчанию недавно созданные или приглашенные учетные записи разработчика являются **активными**.</span><span class="sxs-lookup"><span data-stu-id="5e523-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="5e523-133">Нажмите кнопку toodeactivate учетной записью разработчика, **блок**.</span><span class="sxs-lookup"><span data-stu-id="5e523-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="5e523-134">Щелкните tooreactivate учетной записью разработчика, заблокированных, **активировать**.</span><span class="sxs-lookup"><span data-stu-id="5e523-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="5e523-135">Учетную запись разработчика заблокированных можно получить доступ к порталу developer Привет или не вызвать API.</span><span class="sxs-lookup"><span data-stu-id="5e523-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="5e523-136">toodelete учетной записи пользователя, нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="5e523-136">toodelete a user account, click **Delete**.</span></span>

![Блокировка разработчика][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="5e523-138">Сброс пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="5e523-138">Reset a user password</span></span>
<span data-ttu-id="5e523-139">tooreset hello пароль для учетной записи пользователя, щелкните имя hello hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5e523-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![Сброс пароля][api-management-view-developer]

<span data-ttu-id="5e523-141">Нажмите кнопку **сброс пароля** toosend tooreset ссылку toohello пользователя пароль.</span><span class="sxs-lookup"><span data-stu-id="5e523-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![Сброс пароля][api-management-reset-password]

<span data-ttu-id="5e523-143">tooprogrammatically работы с учетными записями, в разделе hello [сущности пользователя](https://msdn.microsoft.com/library/azure/dn776330.aspx) документации в hello [API REST управления](https://msdn.microsoft.com/library/azure/dn776326.aspx) ссылки.</span><span class="sxs-lookup"><span data-stu-id="5e523-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="5e523-144">tooreset пользователя учетной записи пароль tooa определенное значение, можно использовать hello [обновления пользователя](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) операцию и укажите пароль hello.</span><span class="sxs-lookup"><span data-stu-id="5e523-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="5e523-145">Ожидание проверки</span><span class="sxs-lookup"><span data-stu-id="5e523-145">Pending verification</span></span>
![Ожидание проверки][api-management-pending-verification]

## <span data-ttu-id="5e523-147"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e523-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="5e523-148">После создания учетной записи разработчика, можно связать его с ролями и подписаться его tooproducts и API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="5e523-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="5e523-149">Дополнительные сведения см. в разделе [как toocreate и использования групп][How toocreate and use groups].</span><span class="sxs-lookup"><span data-stu-id="5e523-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

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
