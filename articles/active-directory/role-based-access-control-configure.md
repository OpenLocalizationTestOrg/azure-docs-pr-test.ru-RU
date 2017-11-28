---
title: "Управление доступом на основе aaaRole в hello портал Azure | Документы Microsoft"
description: "Начало работы в управление доступом с элементом управления доступом на основе ролей в hello портала Azure. Используйте роль назначения tooassign разрешения tooyour ресурсы."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a><span data-ttu-id="6f54c-104">Подписка Azure tooyour ресурсы для управления доступом на основе ролей toomanage доступа</span><span class="sxs-lookup"><span data-stu-id="6f54c-104">Use Role-Based Access Control toomanage access tooyour Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f54c-105">Управление доступом по пользователям или группам</span><span class="sxs-lookup"><span data-stu-id="6f54c-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="6f54c-106">Управление доступом по ресурсам</span><span class="sxs-lookup"><span data-stu-id="6f54c-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="6f54c-107">Контроль доступа на основе ролей (RBAC) Azure обеспечивает точное управление доступом для Azure.</span><span class="sxs-lookup"><span data-stu-id="6f54c-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="6f54c-108">С помощью RBAC, можно предоставить только hello уровень доступа, пользователи должны tooperform свою работу.</span><span class="sxs-lookup"><span data-stu-id="6f54c-108">Using RBAC, you can grant only hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="6f54c-109">Эта статья поможет вам приступить к работе с RBAC в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6f54c-109">This article helps you get up and running with RBAC in hello Azure portal.</span></span> <span data-ttu-id="6f54c-110">Дополнительные сведения о том, как RBAC помогает управлять доступом, см. в статье [Начало работы с управлением доступом на портале Azure](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="6f54c-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="6f54c-111">В пределах каждой подписки можно предоставить копию too2000 назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="6f54c-111">Within each subscription, you can grant up too2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="6f54c-112">Просмотр прав доступа</span><span class="sxs-lookup"><span data-stu-id="6f54c-112">View access</span></span>
<span data-ttu-id="6f54c-113">Можно увидеть, кто имеет доступ tooa ресурсов, группы ресурсов или подписки в главной колонке в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f54c-113">You can see who has access tooa resource, resource group, or subscription from its main blade in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6f54c-114">Например мы хотим toosee, кто имеет доступ tooone нашей групп ресурсов:</span><span class="sxs-lookup"><span data-stu-id="6f54c-114">For example, we want toosee who has access tooone of our resource groups:</span></span>

1. <span data-ttu-id="6f54c-115">Выберите **групп ресурсов** hello панели навигации слева hello.</span><span class="sxs-lookup"><span data-stu-id="6f54c-115">Select **Resource groups** in hello navigation bar on hello left.</span></span>  
    <span data-ttu-id="6f54c-116">![Группы ресурсов — значок](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="6f54c-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="6f54c-117">Привет, выберите имя группы ресурсов hello из hello **групп ресурсов** колонку.</span><span class="sxs-lookup"><span data-stu-id="6f54c-117">Select hello name of hello resource group from hello **Resource groups** blade.</span></span>
3. <span data-ttu-id="6f54c-118">Выберите **(IAM) управления доступом к** из меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="6f54c-118">Select **Access control (IAM)** from hello left menu.</span></span>  
4. <span data-ttu-id="6f54c-119">колонке управления доступом Hello список всех пользователей, групп и приложений, которые были предоставлены группе ресурсов toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="6f54c-119">hello Access control blade lists all users, groups, and applications that have been granted access toohello resource group.</span></span>  
   
    ![Колонка "Пользователи" — унаследованные и назначенные права доступа — снимок экрана](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="6f54c-121">Обратите внимание, что некоторые роли находятся в области видимости слишком**этот ресурс** а другие представляют собой **Inherited** его из другой области.</span><span class="sxs-lookup"><span data-stu-id="6f54c-121">Notice that some roles are scoped too**This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="6f54c-122">Доступа специально toohello группу ресурсов или унаследовано из родительского подписки toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="6f54c-122">Access is either assigned specifically toohello resource group or inherited from an assignment toohello parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="6f54c-123">Администраторы классический подписки и соадминистраторам считаются владельцев подписки hello в новой модели RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="6f54c-123">Classic subscription admins and co-admins are considered owners of hello subscription in hello new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="6f54c-124">Добавление доступа</span><span class="sxs-lookup"><span data-stu-id="6f54c-124">Add Access</span></span>
<span data-ttu-id="6f54c-125">Разрешить доступ из внутри hello ресурсов, группы ресурсов или подписку, которая является областью hello hello назначение ролей.</span><span class="sxs-lookup"><span data-stu-id="6f54c-125">You grant access from within hello resource, resource group, or subscription that is hello scope of hello role assignment.</span></span>

1. <span data-ttu-id="6f54c-126">Выберите **добавить** колонке управления доступом hello.</span><span class="sxs-lookup"><span data-stu-id="6f54c-126">Select **Add** on hello Access control blade.</span></span>  
2. <span data-ttu-id="6f54c-127">Обратиться в tooassign из hello роли выберите hello **выберите роль** колонку.</span><span class="sxs-lookup"><span data-stu-id="6f54c-127">Select hello role that you wish tooassign from hello **Select a role** blade.</span></span>
3. <span data-ttu-id="6f54c-128">Выберите в каталоге, из которого будут toogrant доступ к hello пользователя, группы или приложения.</span><span class="sxs-lookup"><span data-stu-id="6f54c-128">Select hello user, group, or application in your directory that you wish toogrant access to.</span></span> <span data-ttu-id="6f54c-129">Можно выполнить поиск каталога hello отображаемые имена, адреса электронной почты и идентификаторов объектов.</span><span class="sxs-lookup"><span data-stu-id="6f54c-129">You can search hello directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Колонка "Добавить пользователей" — "Поиск" — снимок экрана](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="6f54c-131">Выберите **ОК** toocreate hello назначения.</span><span class="sxs-lookup"><span data-stu-id="6f54c-131">Select **OK** toocreate hello assignment.</span></span> <span data-ttu-id="6f54c-132">Hello **Добавление пользователя** всплывающее окно отслеживает ход выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="6f54c-132">hello **Adding user** popup tracks hello progress.</span></span>  
    <span data-ttu-id="6f54c-133">![Индикатор выполнения при добавлении пользователя — снимок экрана](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="6f54c-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="6f54c-134">После успешного добавления назначение ролей, оно будет отображаться для hello **пользователей** колонку.</span><span class="sxs-lookup"><span data-stu-id="6f54c-134">After successfully adding a role assignment, it will appear on hello **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="6f54c-135">Запрет доступа</span><span class="sxs-lookup"><span data-stu-id="6f54c-135">Remove Access</span></span>
1. <span data-ttu-id="6f54c-136">Наведите указатель на имя hello hello назначения, которое следует tooremove.</span><span class="sxs-lookup"><span data-stu-id="6f54c-136">Hover your cursor over hello name of hello assignment that you want tooremove.</span></span> <span data-ttu-id="6f54c-137">Флажок отображается имя следующего toohello.</span><span class="sxs-lookup"><span data-stu-id="6f54c-137">A check box appears next toohello name.</span></span>
2. <span data-ttu-id="6f54c-138">Использовать флажки tooselect hello один или несколько назначений ролей.</span><span class="sxs-lookup"><span data-stu-id="6f54c-138">Use hello check boxes tooselect one or more role assignments.</span></span>
2. <span data-ttu-id="6f54c-139">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="6f54c-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="6f54c-140">Выберите **Да** tooconfirm hello удаления.</span><span class="sxs-lookup"><span data-stu-id="6f54c-140">Select **Yes** tooconfirm hello removal.</span></span>

<span data-ttu-id="6f54c-141">Унаследованные назначения нельзя удалить.</span><span class="sxs-lookup"><span data-stu-id="6f54c-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="6f54c-142">Если требуется tooremove наследуемые назначения необходимо toodo его в параметре hello области, где создавался hello назначение ролей.</span><span class="sxs-lookup"><span data-stu-id="6f54c-142">If you need tooremove an inherited assignment, you need toodo it at hello scope where hello role assignment was created.</span></span> <span data-ttu-id="6f54c-143">В hello **область** столбец, далее слишком**Inherited** есть ссылка, которое знакомит вас toohello ресурсы которой было назначено этой роли.</span><span class="sxs-lookup"><span data-stu-id="6f54c-143">In hello **Scope** column, next too**Inherited** there is a link that takes you toohello resources where this role was assigned.</span></span> <span data-ttu-id="6f54c-144">Перейдите в списке ресурсов toohello назначение ролей tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="6f54c-144">Go toohello resource listed there tooremove hello role assignment.</span></span>

![Колонка "Пользователи" — унаследованные права доступа отключают кнопку "Удалить" — снимок экрана](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a><span data-ttu-id="6f54c-146">Другие средства доступа toomanage</span><span class="sxs-lookup"><span data-stu-id="6f54c-146">Other tools toomanage access</span></span>
<span data-ttu-id="6f54c-147">Можно назначать роли и управление доступом с помощью Azure RBAC команды в средствах, отличные от hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6f54c-147">You can assign roles and manage access with Azure RBAC commands in tools other than hello Azure portal.</span></span>  <span data-ttu-id="6f54c-148">Выполните дополнительные о предварительных требованиях hello toolearn ссылки hello и приступить к работе с командами hello Azure RBAC.</span><span class="sxs-lookup"><span data-stu-id="6f54c-148">Follow hello links toolearn more about hello prerequisites and get started with hello Azure RBAC commands.</span></span>

* [<span data-ttu-id="6f54c-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f54c-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="6f54c-150">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="6f54c-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="6f54c-151">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="6f54c-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="6f54c-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f54c-152">Next Steps</span></span>
* [<span data-ttu-id="6f54c-153">Создание отчета по журналу изменений доступа</span><span class="sxs-lookup"><span data-stu-id="6f54c-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="6f54c-154">В разделе hello [RBAC встроенные роли](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="6f54c-154">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="6f54c-155">Определите собственные [пользовательские роли в RBAC Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="6f54c-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

