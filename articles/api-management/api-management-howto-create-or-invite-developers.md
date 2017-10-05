---
title: "Управление учетными записями пользователей в службе управления API Azure | Документация Майкрософт"
description: "Создание или приглашение пользователей в службе управления API Azure"
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
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="5c8bd-103">Управление учетными записями пользователей в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="5c8bd-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="5c8bd-104">В службе управления API разработчики – это пользователи интерфейсов API, которые вы предоставляете с помощью службы управления API.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="5c8bd-105">В этом руководстве показано, как создавать и приглашать разработчиков использовать интерфейсы API и продукты, которые вы делаете доступными для них с помощью своего экземпляра API Management.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="5c8bd-106">Сведения о программном управлении учетными записями пользователей см. в документации по [сущностям пользователя](https://msdn.microsoft.com/library/azure/dn776330.aspx) [в справочнике по REST управления API](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c8bd-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="5c8bd-107"><a name="create-developer"> </a>Создание нового разработчика</span><span class="sxs-lookup"><span data-stu-id="5c8bd-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="5c8bd-108">Чтобы создать разработчика, щелкните на портале Azure **Publisher portal** (Портал издателя) для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="5c8bd-109">Будет открыт портал издателя службы управления API.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="5c8bd-110">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="5c8bd-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Портал издателя][api-management-management-console]

<span data-ttu-id="5c8bd-112">В расположенном слева меню **Управление API** выберите пункт **Пользователи**, а затем щелкните элемент **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Создание разработчика][api-management-create-developer]

<span data-ttu-id="5c8bd-114">Введите **адрес электронной почты**, **пароль** и **имя** для нового разработчика, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Создание разработчика][api-management-add-new-user]

<span data-ttu-id="5c8bd-116">По умолчанию недавно созданные учетные записи разработчика являются **активными** и связаны с группой **Разработчики**.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![Новый разработчик][api-management-new-developer]

<span data-ttu-id="5c8bd-118">Учетные записи разработчика, которые находятся в **активном** состоянии, можно использовать для доступа ко всем интерфейсам API, на которые у них есть подписки.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="5c8bd-119">Процедуру связывания недавно созданного разработчика с дополнительными группами см. в разделе [Связывание групп с разработчиками][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="5c8bd-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="5c8bd-120"><a name="invite-developer"> </a>Приглашение разработчика</span><span class="sxs-lookup"><span data-stu-id="5c8bd-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="5c8bd-121">Чтобы пригласить разработчика, выберите пункт **Пользователи** в расположенном слева меню **Управление API**, а затем щелкните элемент **Пригласить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Приглашение разработчика][api-management-invite-developer]

<span data-ttu-id="5c8bd-123">Введите имя и адрес электронной почты разработчика, а затем щелкните **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Приглашение разработчика][api-management-invite-developer-window]

<span data-ttu-id="5c8bd-125">Вы увидите сообщение-подтверждение, но недавно приглашенный разработчик не появится в списке, пока не примет приглашение.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Подтверждение приглашения][api-management-invite-developer-confirmation]

<span data-ttu-id="5c8bd-127">После приглашения разработчика ему отправляется сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="5c8bd-128">Это сообщение создается с помощью шаблона и может настраиваться.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="5c8bd-129">Дополнительные сведения см. в разделе [Настройка почтовых шаблонов][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="5c8bd-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="5c8bd-130">После принятия приглашения учетная запись становится активной.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="5c8bd-131"><a name="block-developer"> </a> Деактивация или повторная активация учетной записи разработчика</span><span class="sxs-lookup"><span data-stu-id="5c8bd-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="5c8bd-132">По умолчанию недавно созданные или приглашенные учетные записи разработчика являются **активными**.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="5c8bd-133">Для деактивации учетной записи разработчика щелкните **Блокировать**.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="5c8bd-134">Для повторной активации блокированной учетной записи разработчика щелкните **Активировать**.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="5c8bd-135">Блокированная учетная запись разработчика не может получать доступ к порталу разработчика или вызвать любые интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="5c8bd-136">Чтобы удалить учетную запись пользователя, щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-136">To delete a user account, click **Delete**.</span></span>

![Блокировка разработчика][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="5c8bd-138">Сброс пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="5c8bd-138">Reset a user password</span></span>
<span data-ttu-id="5c8bd-139">Чтобы сбросить пароль для учетной записи пользователя, щелкните имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-139">To reset the password for a user account, click the name of the account.</span></span>

![Сбросить пароль][api-management-view-developer]

<span data-ttu-id="5c8bd-141">Щелкните **Сбросить пароль** , чтобы отправить пользователю ссылку для сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![Сброс пароля][api-management-reset-password]

<span data-ttu-id="5c8bd-143">Сведения о программной работе с учетными записями пользователей см. в документации по [сущностям пользователя](https://msdn.microsoft.com/library/azure/dn776330.aspx) в [справочнике по REST управления API](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c8bd-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="5c8bd-144">Чтобы сбросить пароль учетной записи пользователя до определенного значения, можно использовать операцию [обновления пользователя](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) и указать нужный пароль.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="5c8bd-145">Ожидание проверки</span><span class="sxs-lookup"><span data-stu-id="5c8bd-145">Pending verification</span></span>
![Ожидание проверки][api-management-pending-verification]

## <span data-ttu-id="5c8bd-147"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c8bd-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="5c8bd-148">После создания учетной записи разработчика ее можно связать с ролями и подписать ее на продукты и интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="5c8bd-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="5c8bd-149">Дополнительные сведения см. в статье [Как создавать и использовать группы для управления учетными записями разработчика в службе управления Azure API][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="5c8bd-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

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
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
