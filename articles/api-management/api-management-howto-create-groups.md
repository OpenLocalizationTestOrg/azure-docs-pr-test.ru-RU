---
title: "с помощью групп в Azure API управления учетными записями разработчиков aaaManage | Документы Microsoft"
description: "Узнайте, как разработчик toomanage учетных записей с помощью групп в службе управления API Azure"
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
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="2737f-103">Как разработчик toomanage группы toocreate и использование учетных записей в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="2737f-103">How toocreate and use groups toomanage developer accounts in Azure API Management</span></span>
<span data-ttu-id="2737f-104">В службе управления API группы — видимость hello используется toomanage toodevelopers продуктов.</span><span class="sxs-lookup"><span data-stu-id="2737f-104">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="2737f-105">Продукты, первый toogroups сделан видимым и затем разработчики в эти группы могут просматривать и подписываться toohello продуктов, которые связаны с группами hello.</span><span class="sxs-lookup"><span data-stu-id="2737f-105">Products are first made visible toogroups, and then developers in those groups can view and subscribe toohello products that are associated with hello groups.</span></span> 

<span data-ttu-id="2737f-106">Управление API имеет следующие группы неизменяемые hello.</span><span class="sxs-lookup"><span data-stu-id="2737f-106">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="2737f-107">**Администраторы** — члены этой группы являются администраторами подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="2737f-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="2737f-108">Администраторы управления экземплярами службы управления API, создание hello API, операции и продукты, которые используются разработчиками.</span><span class="sxs-lookup"><span data-stu-id="2737f-108">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="2737f-109">**Разработчики** — в эту группу входят пользователи портала разработчиков, прошедшие проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="2737f-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="2737f-110">Разработчики, hello пользователи, создающие приложения, использующие собственные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="2737f-110">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="2737f-111">Разработчики предоставляются портал разработчиков toohello доступа и создавать приложения, которые вызывают hello операции API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2737f-111">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="2737f-112">**Гостевые системы** -непроверенных пользователей портала разработчиков, например потенциальных клиентов, посетив портал разработчиков hello падения экземпляр управления API в эту группу.</span><span class="sxs-lookup"><span data-stu-id="2737f-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="2737f-113">Они могут быть предоставлены определенные доступа только для чтения, например tooview hello возможности API-интерфейсов, но не их вызова.</span><span class="sxs-lookup"><span data-stu-id="2737f-113">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="2737f-114">В дополнение toothese системные группы, администраторы могут создавать настраиваемые группы или [использование внешних групп в связанных клиентов Azure Active Directory][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="2737f-114">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="2737f-115">Пользовательские и внешних групп могут использоваться вместе со системные группы в предоставляя разработчикам видимость и доступ к tooAPI продуктов.</span><span class="sxs-lookup"><span data-stu-id="2737f-115">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="2737f-116">Например, можно создать одну пользовательскую группу для разработчиков, связано с определенным организации партнера и разрешить им доступ toohello API-интерфейсы для продукта, содержащий соответствующие интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="2737f-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="2737f-117">Пользователь может входить в несколько групп.</span><span class="sxs-lookup"><span data-stu-id="2737f-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="2737f-118">В этом руководстве показано, как администраторы экземпляра службы управления API могут добавлять новые группы и связывать их с продуктами и разработчиками.</span><span class="sxs-lookup"><span data-stu-id="2737f-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="2737f-119">В дополнение к этому toocreating групп и управление ими в портал издателя hello, можно создать и управлять группами с помощью API REST управления hello [группы](https://msdn.microsoft.com/library/azure/dn776329.aspx) сущности.</span><span class="sxs-lookup"><span data-stu-id="2737f-119">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="2737f-120"><a name="create-group"> </a>Создание группы</span><span class="sxs-lookup"><span data-stu-id="2737f-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="2737f-121">toocreate новую группу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="2737f-121">toocreate a new group, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="2737f-122">Откроется портал издателя управления API toohello.</span><span class="sxs-lookup"><span data-stu-id="2737f-122">This takes you toohello API Management publisher portal.</span></span>

![Портал издателя][api-management-management-console]

> <span data-ttu-id="2737f-124">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="2737f-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="2737f-125">Нажмите кнопку **группы** из hello **API управления** меню hello слева, а затем нажмите **добавить группу**.</span><span class="sxs-lookup"><span data-stu-id="2737f-125">Click **Groups** from hello **API Management** menu on hello left, and then click **Add Group**.</span></span>

![Добавление новой группы][api-management-add-group]

<span data-ttu-id="2737f-127">Введите уникальное имя для группы hello и описание (необязательно) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2737f-127">Enter a unique name for hello group and an optional description, and click **Save**.</span></span>

![Добавление новой группы][api-management-add-group-window]

<span data-ttu-id="2737f-129">Hello новая группа появится в hello tooedit вкладку групп hello **имя** или **описание** hello группы, щелкните имя hello hello группы в списке hello.</span><span class="sxs-lookup"><span data-stu-id="2737f-129">hello new group is displayed in hello groups tab. tooedit hello **Name** or **Description** of hello group, click hello name of hello group in hello list.</span></span> <span data-ttu-id="2737f-130">toodelete hello группы, нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="2737f-130">toodelete hello group, click **Delete**.</span></span>

![Группа добавлена][api-management-new-group]

<span data-ttu-id="2737f-132">Теперь, когда hello группа будет создана, его можно связать с продуктами и разработчиков.</span><span class="sxs-lookup"><span data-stu-id="2737f-132">Now that hello group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="2737f-133"><a name="associate-group-product"> </a>Связывание группы с продуктом</span><span class="sxs-lookup"><span data-stu-id="2737f-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="2737f-134">Щелкните tooassociate группы с продуктом, **продуктов** из hello **API управления** меню hello и выберите команду hello имя нужного продукта hello.</span><span class="sxs-lookup"><span data-stu-id="2737f-134">tooassociate a group with a product, click **Products** from hello **API Management** menu on hello left, and then click hello name of hello desired product.</span></span>

![Настройка видимости][api-management-add-group-to-product]

<span data-ttu-id="2737f-136">Выберите hello **видимость** вкладке tooadd и удаление групп и tooview hello текущих групп hello продукта.</span><span class="sxs-lookup"><span data-stu-id="2737f-136">Select hello **Visibility** tab tooadd and remove groups, and tooview hello current groups for hello product.</span></span> <span data-ttu-id="2737f-137">tooadd или удалите группы, установите или снимите флажки hello в случае, для hello требуемого группы и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2737f-137">tooadd or remove groups, check or uncheck hello checkboxes for hello desired groups and click **Save**.</span></span>

![Настройка видимости][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="2737f-139">tooadd группы Azure Active Directory, см. [как разработчик tooauthorize учетных записей с помощью Azure Active Directory в Azure API Management](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="2737f-139">tooadd Azure Active Directory groups, see [How tooauthorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="2737f-140">tooconfigure группы из hello **видимость** для продукта, щелкните **Управление группами**.</span><span class="sxs-lookup"><span data-stu-id="2737f-140">tooconfigure groups from hello **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="2737f-141">Если продукт связан с группой, разработчики в этой группе можно просматривать и подписываться toohello продукта.</span><span class="sxs-lookup"><span data-stu-id="2737f-141">Once a product is associated with a group, developers in that group can view and subscribe toohello product.</span></span>

## <span data-ttu-id="2737f-142"><a name="associate-group-developer"> </a>Связывание групп с разработчиками</span><span class="sxs-lookup"><span data-stu-id="2737f-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="2737f-143">tooassociate групп с разработчиками, нажмите кнопку **пользователей** из hello **управления API** меню hello слева, а затем hello флажок рядом с hello разработчикам нужно tooassociate с группой.</span><span class="sxs-lookup"><span data-stu-id="2737f-143">tooassociate groups with developers, click **Users** from hello **API Management** menu on hello left, and then check hello box beside hello developers you wish tooassociate with a group.</span></span>

![Добавить toogroup разработчика][api-management-add-group-to-developer]

<span data-ttu-id="2737f-145">После hello требуемого разработчикам проверяются, щелкните hello нужной группы в hello **добавить tooGroup** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="2737f-145">Once hello desired developers are checked, click hello desired group in hello **Add tooGroup** drop-down.</span></span> <span data-ttu-id="2737f-146">Разработчики могут быть удалены из групп с помощью hello **удалить из группы** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="2737f-146">Developers can be removed from groups by using hello **Remove from Group** drop-down.</span></span> 

![Разработчики][api-management-add-group-to-developer-saved]

<span data-ttu-id="2737f-148">После добавления hello связь между разработчиком hello и группой hello его можно просмотреть в hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="2737f-148">Once hello association is added between hello developer and hello group, you can view it in hello **Users** tab.</span></span>

## <span data-ttu-id="2737f-149"><a name="next-steps"> </a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2737f-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="2737f-150">После добавления группы tooa разработчик можно просматривать и подписываться toohello продукты, связанные с данной группой.</span><span class="sxs-lookup"><span data-stu-id="2737f-150">Once a developer is added tooa group, they can view and subscribe toohello products associated with that group.</span></span> <span data-ttu-id="2737f-151">Дополнительные сведения см. в статье [Создание и публикация продукта в службе управления API Azure][How create and publish a product in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2737f-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="2737f-152">В дополнение к этому toocreating групп и управление ими в портал издателя hello, можно создать и управлять группами с помощью API REST управления hello [группы](https://msdn.microsoft.com/library/azure/dn776329.aspx) сущности.</span><span class="sxs-lookup"><span data-stu-id="2737f-152">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
