---
title: "Назначение доступа aaaView ресурсов Azure | Документы Microsoft"
description: "Просмотр и управление ими все назначения hello управления доступом на основе ролей для любого пользователя или группу в hello портал Azure"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a><span data-ttu-id="0aedd-103">Просмотр назначений доступ для пользователей и групп в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0aedd-103">View access assignments for users and groups in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0aedd-104">Управление доступом по пользователям или группам</span><span class="sxs-lookup"><span data-stu-id="0aedd-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="0aedd-105">Управление доступом по ресурсам</span><span class="sxs-lookup"><span data-stu-id="0aedd-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="0aedd-106">Управление доступом на основе ролей (RBAC) в hello Azure Active Directory (Azure AD), позволяет управлять доступом tooyour Azure ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0aedd-106">With role-based access control (RBAC) in hello Azure Active Directory (Azure AD), you can manage access tooyour Azure resources.</span></span> 

<span data-ttu-id="0aedd-107">Доступ, которым назначена RBAC детально настроенные так, как можно ограничить разрешения hello двумя способами:</span><span class="sxs-lookup"><span data-stu-id="0aedd-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict hello permissions:</span></span>

* <span data-ttu-id="0aedd-108">**Область:** RBAC назначения ролей, с областью tooa конкретной подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0aedd-108">**Scope:** RBAC role assignments are scoped tooa specific subscription, resource group, or resource.</span></span> <span data-ttu-id="0aedd-109">Пользователь получает доступ tooa одного ресурса не может получить доступ к другие ресурсы в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="0aedd-109">A user given access tooa single resource cannot access any other resources in hello same subscription.</span></span>
* <span data-ttu-id="0aedd-110">**Роль:** внутри области hello назначения hello сведена доступ назначение роли еще продолжается.</span><span class="sxs-lookup"><span data-stu-id="0aedd-110">**Role:** Within hello scope of hello assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="0aedd-111">Роль может быть общей, например "Владелец", или более конкретной, например "Модуль чтения виртуальной машины".</span><span class="sxs-lookup"><span data-stu-id="0aedd-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="0aedd-112">Роли могут назначаться только из внутри hello подписки, группы ресурсов или ресурс, который является областью hello для назначения hello.</span><span class="sxs-lookup"><span data-stu-id="0aedd-112">Roles can only be assigned from within hello subscription, resource group, or resource that is hello scope for hello assignment.</span></span> <span data-ttu-id="0aedd-113">Однако можно просмотреть все назначения hello доступа для данного пользователя или группы в одном месте.</span><span class="sxs-lookup"><span data-stu-id="0aedd-113">But you can view all hello access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="0aedd-114">Можно создать до назначения ролей too2000 в каждой подписке.</span><span class="sxs-lookup"><span data-stu-id="0aedd-114">You can have up too2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="0aedd-115">Получить дополнительные сведения о том, как слишком[использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0aedd-115">Get more information about how too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="0aedd-116">Просмотр назначений доступа</span><span class="sxs-lookup"><span data-stu-id="0aedd-116">View access assignments</span></span>
<span data-ttu-id="0aedd-117">toolook копирование hello доступа назначений для одного пользователя или группы, запуск в Azure Active Directory в hello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0aedd-117">toolook up hello access assignments for a single user or group, start in Azure Active Directory in hello [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="0aedd-118">Выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0aedd-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="0aedd-119">Если этот параметр не отображается в списке навигации, выберите **более служб** и прокрутите вниз toofind **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0aedd-119">If this option is not visible on your navigation list, select **More Services** and then scroll down toofind **Azure Active Directory**.</span></span>
2. <span data-ttu-id="0aedd-120">Выберите **Пользователи и группы**, а затем щелкните **Все пользователи** или **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="0aedd-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="0aedd-121">В этом примере мы рассмотрим отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="0aedd-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="0aedd-122">![Снимок экрана: управление пользователями и группами в Azure Active Directory](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="0aedd-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="0aedd-123">Поиск hello пользователя по имени или имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="0aedd-123">Search for hello user by name or username.</span></span>
4. <span data-ttu-id="0aedd-124">Выберите **ресурсы Azure** колонке hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="0aedd-124">Select **Azure resources** on hello user blade.</span></span> <span data-ttu-id="0aedd-125">Отображаются все назначения hello доступа для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="0aedd-125">All hello access assignments for that user appear.</span></span>

### <a name="read-permissions-tooview-assignments"></a><span data-ttu-id="0aedd-126">Разрешения на чтение tooview назначений</span><span class="sxs-lookup"><span data-stu-id="0aedd-126">Read permissions tooview assignments</span></span>
<span data-ttu-id="0aedd-127">На этой странице отображаются только назначения доступа hello наличие tooread разрешение.</span><span class="sxs-lookup"><span data-stu-id="0aedd-127">This page only shows hello access assignments that you have permission tooread.</span></span> <span data-ttu-id="0aedd-128">Например имеют доступ на чтение toosubscription A и перейти toocheck колонки ресурсов Azure toohello назначений пользователя.</span><span class="sxs-lookup"><span data-stu-id="0aedd-128">For example, you have read access toosubscription A and go toohello Azure resources blade toocheck a user's assignments.</span></span> <span data-ttu-id="0aedd-129">Вы увидите назначения доступа для подписки A, но имеющиеся у пользователя назначения доступа для подписки Б не будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="0aedd-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="0aedd-130">Удаление назначений доступа</span><span class="sxs-lookup"><span data-stu-id="0aedd-130">Delete access assignments</span></span>
<span data-ttu-id="0aedd-131">Из этой колонки можно удалить назначения доступа, которые назначаются напрямую tooa пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="0aedd-131">From this blade, you can delete access assignments that were assigned directly tooa user or group.</span></span> <span data-ttu-id="0aedd-132">Если назначение доступа hello было унаследовано из родительской группы, требуется toogo toohello ресурсов или подписки и управление назначением hello существует.</span><span class="sxs-lookup"><span data-stu-id="0aedd-132">If hello access assignment was inherited from a parent group, you need toogo toohello resource or subscription and manage hello assignment there.</span></span>

1. <span data-ttu-id="0aedd-133">Выберите из списка hello среди всех назначений hello доступа для пользователя или группы hello один требуется toodelete.</span><span class="sxs-lookup"><span data-stu-id="0aedd-133">From hello list of all hello access assignments for a user or group, select hello one you want toodelete.</span></span>
2. <span data-ttu-id="0aedd-134">Выберите **удалить** и затем **Да** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="0aedd-134">Select **Remove** and then **Yes** tooconfirm.</span></span>
    <span data-ttu-id="0aedd-135">![Снимок экрана: удаление назначения доступа](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="0aedd-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0aedd-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0aedd-136">Next steps</span></span>

* <span data-ttu-id="0aedd-137">Приступая к работе с управление доступом на основе ролей слишком[использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="0aedd-137">Get started with Role-Based Access Control too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="0aedd-138">В разделе hello [RBAC встроенные роли](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="0aedd-138">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

