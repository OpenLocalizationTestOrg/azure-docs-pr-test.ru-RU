---
title: "Управление учетными записями разработчиков с помощью групп в службе управления API Azure | Документация Майкрософт"
description: "Сведения об управлении учетными записями разработчика с помощью групп в службе управления API Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="b760b-103">Как создавать и использовать группы для управления учетными записями разработчика в службе управления Azure API</span><span class="sxs-lookup"><span data-stu-id="b760b-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="b760b-104">В службе управления API группы используются для управления видимостью продуктов для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="b760b-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="b760b-105">Продукты сначала делаются видимыми для групп, а затем разработчики в таких группах могут просматривать и подписываться на продукты, которые связаны с группами.</span><span class="sxs-lookup"><span data-stu-id="b760b-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="b760b-106">Служба управления API имеет несколько неизменяемых системных групп.</span><span class="sxs-lookup"><span data-stu-id="b760b-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="b760b-107">**Администраторы** — члены этой группы являются администраторами подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="b760b-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="b760b-108">Администраторы управляют экземплярами службы управления API, созданием API, операциями и продуктами, которые используются разработчиками.</span><span class="sxs-lookup"><span data-stu-id="b760b-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="b760b-109">**Разработчики** — в эту группу входят пользователи портала разработчиков, прошедшие проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b760b-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="b760b-110">Разработчики — это клиенты, которые создают приложения с использованием API.</span><span class="sxs-lookup"><span data-stu-id="b760b-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="b760b-111">Разработчикам предоставляется доступ к порталу разработчика, и они могут создавать приложения, вызывающие операции этого API.</span><span class="sxs-lookup"><span data-stu-id="b760b-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="b760b-112">**Гости** — пользователи портала разработчиков, не прошедшие проверку подлинности; например, в эту группу попадают возможные клиенты, посетившие портал разработчиков экземпляра управления API.</span><span class="sxs-lookup"><span data-stu-id="b760b-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="b760b-113">Им может быть предоставлен доступ только для чтения, позволяющий просматривать API, но не вызывать их.</span><span class="sxs-lookup"><span data-stu-id="b760b-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="b760b-114">Помимо системных групп администраторы могут создавать пользовательские группы или [использовать внешние группы в связанных с ними клиентах Azure Active Directory][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="b760b-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="b760b-115">Чтобы обеспечить разработчикам видимость и предоставить доступ к продуктам API, пользовательские и внешние группы можно использовать вместе с системными группами.</span><span class="sxs-lookup"><span data-stu-id="b760b-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="b760b-116">Например, можно создать одну пользовательскую группу для разработчиков, связанных с конкретной партнерской организацией, и предоставить им доступ к интерфейсам API в продукте, содержащем только соответствующие интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="b760b-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="b760b-117">Пользователь может входить в несколько групп.</span><span class="sxs-lookup"><span data-stu-id="b760b-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="b760b-118">В этом руководстве показано, как администраторы экземпляра службы управления API могут добавлять новые группы и связывать их с продуктами и разработчиками.</span><span class="sxs-lookup"><span data-stu-id="b760b-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="b760b-119">Помимо создания групп и управления ими на портале издателя, это можно делать с помощью сущности [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) REST API интерфейса API управления.</span><span class="sxs-lookup"><span data-stu-id="b760b-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="b760b-120"><a name="create-group"> </a>Создание группы</span><span class="sxs-lookup"><span data-stu-id="b760b-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="b760b-121">Чтобы создать группу, щелкните на портале Azure **Publisher portal** (Портал издателя) для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="b760b-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="b760b-122">Будет открыт портал издателя службы управления API.</span><span class="sxs-lookup"><span data-stu-id="b760b-122">This takes you to the API Management publisher portal.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="b760b-124">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="b760b-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="b760b-125">Щелкните **Группы** в расположенном слева меню **Управление API**, а затем — **Добавить группу**.</span><span class="sxs-lookup"><span data-stu-id="b760b-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Добавление новой группы][api-management-add-group]

<span data-ttu-id="b760b-127">Введите уникальное имя для группы и необязательное описание, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b760b-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Добавление новой группы][api-management-add-group-window]

<span data-ttu-id="b760b-129">Новая группа отображается на вкладке групп.</span><span class="sxs-lookup"><span data-stu-id="b760b-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="b760b-130">Чтобы изменить **имя** или **описание** группы, щелкните имя группы в списке.</span><span class="sxs-lookup"><span data-stu-id="b760b-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="b760b-131">Чтобы удалить группу, щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="b760b-131">To delete the group, click **Delete**.</span></span>

![Группа добавлена][api-management-new-group]

<span data-ttu-id="b760b-133">Теперь, когда группа создана, ее можно связать с продуктами и разработчиками.</span><span class="sxs-lookup"><span data-stu-id="b760b-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="b760b-134"><a name="associate-group-product"> </a>Связывание группы с продуктом</span><span class="sxs-lookup"><span data-stu-id="b760b-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="b760b-135">Чтобы связать группу с продуктом, щелкните **Продукты** в расположенном слева меню **Управление API**, а затем щелкните имя нужного продукта.</span><span class="sxs-lookup"><span data-stu-id="b760b-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Настройка видимости][api-management-add-group-to-product]

<span data-ttu-id="b760b-137">Для добавления и удаления групп, а также просмотра текущих групп для продукта перейдите на вкладку **Видимость** .</span><span class="sxs-lookup"><span data-stu-id="b760b-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="b760b-138">Для добавления или удаления групп установите или снимите флажки для требуемых групп и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b760b-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Настройка видимости][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="b760b-140">Дополнительную информацию о добавлении групп Azure Active Directory см. в статье [Авторизация учетных записей разработчиков с помощью Azure Active Directory в управлении API Azure](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="b760b-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="b760b-141">Для настройки групп на вкладке **Видимость** для продукта щелкните **Управление группами**.</span><span class="sxs-lookup"><span data-stu-id="b760b-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="b760b-142">После установления связи между продуктом и группой разработчики в данной группе могут просматривать продукт и подписаться на него.</span><span class="sxs-lookup"><span data-stu-id="b760b-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="b760b-143"><a name="associate-group-developer"> </a>Связывание групп с разработчиками</span><span class="sxs-lookup"><span data-stu-id="b760b-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="b760b-144">Чтобы связать группы с разработчиками, щелкните **Пользователи** в расположенном слева меню **Управление API**, а затем установите флажок рядом с разработчиками, которых необходимо связать с группой.</span><span class="sxs-lookup"><span data-stu-id="b760b-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Добавление разработчика в группу][api-management-add-group-to-developer]

<span data-ttu-id="b760b-146">После выбора требуемых разработчиков щелкните требуемую группу в раскрывающемся списке **Добавить в группу** .</span><span class="sxs-lookup"><span data-stu-id="b760b-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="b760b-147">Для удаления разработчиков из групп используйте раскрывающийся список **Удалить из группы** .</span><span class="sxs-lookup"><span data-stu-id="b760b-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![Разработчики][api-management-add-group-to-developer-saved]

<span data-ttu-id="b760b-149">После добавления связи между разработчиком и группой ее можно просмотреть на вкладке **Пользователи** .</span><span class="sxs-lookup"><span data-stu-id="b760b-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="b760b-150"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b760b-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="b760b-151">После добавления  в группу разработчик может просматривать связанные с данной группой продукты и подписываться на них.</span><span class="sxs-lookup"><span data-stu-id="b760b-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="b760b-152">Дополнительные сведения см. в статье [Создание и публикация продукта в службе управления API Azure][How create and publish a product in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="b760b-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="b760b-153">Помимо создания групп и управления ими на портале издателя, это можно делать с помощью сущности [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) REST API интерфейса API управления.</span><span class="sxs-lookup"><span data-stu-id="b760b-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
