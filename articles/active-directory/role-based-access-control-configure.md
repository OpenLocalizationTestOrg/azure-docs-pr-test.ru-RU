---
title: "Контроль доступа на основе ролей на портале Azure | Документация Майкрософт"
description: "Узнайте, как управлять доступом с помощью RBAC на портале Azure. Использование назначений ролей для назначения разрешений в вашем каталоге."
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
ms.openlocfilehash: 9df7f7851ef1fc6b4ed03b981aa5062d6b0913ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-role-based-access-control-to-manage-access-to-your-azure-subscription-resources"></a><span data-ttu-id="b97df-104">Использование управления доступом на основе ролей для контроля доступа к ресурсам в подписке Azure</span><span class="sxs-lookup"><span data-stu-id="b97df-104">Use Role-Based Access Control to manage access to your Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b97df-105">Управление доступом по пользователям или группам</span><span class="sxs-lookup"><span data-stu-id="b97df-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="b97df-106">Управление доступом по ресурсам</span><span class="sxs-lookup"><span data-stu-id="b97df-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="b97df-107">Контроль доступа на основе ролей (RBAC) Azure обеспечивает точное управление доступом для Azure.</span><span class="sxs-lookup"><span data-stu-id="b97df-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="b97df-108">С помощью RBAC можно предоставлять пользователям доступ, необходимый только для выполнения поставленных перед ними задач.</span><span class="sxs-lookup"><span data-stu-id="b97df-108">Using RBAC, you can grant only the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="b97df-109">Эта статья поможет вам приступить к работе с RBAC на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b97df-109">This article helps you get up and running with RBAC in the Azure portal.</span></span> <span data-ttu-id="b97df-110">Дополнительные сведения о том, как RBAC помогает управлять доступом, см. в статье [Начало работы с управлением доступом на портале Azure](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="b97df-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="b97df-111">В рамках каждой подписки вы можете назначить до 2000 ролей.</span><span class="sxs-lookup"><span data-stu-id="b97df-111">Within each subscription, you can grant up to 2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="b97df-112">Просмотр прав доступа</span><span class="sxs-lookup"><span data-stu-id="b97df-112">View access</span></span>
<span data-ttu-id="b97df-113">Вы можете увидеть, у кого есть доступ к ресурсу, группе ресурсов или подписке, в основной колонке на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b97df-113">You can see who has access to a resource, resource group, or subscription from its main blade in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b97df-114">Например, мы хотим узнать, кто имеет доступ к одной из наших групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b97df-114">For example, we want to see who has access to one of our resource groups:</span></span>

1. <span data-ttu-id="b97df-115">Щелкните значок **Группы ресурсов** на панели навигации слева.</span><span class="sxs-lookup"><span data-stu-id="b97df-115">Select **Resource groups** in the navigation bar on the left.</span></span>  
    <span data-ttu-id="b97df-116">![Группы ресурсов — значок](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="b97df-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="b97df-117">В колонке **Группы ресурсов** выберите имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b97df-117">Select the name of the resource group from the **Resource groups** blade.</span></span>
3. <span data-ttu-id="b97df-118">В меню слева выберите **Управление доступом (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="b97df-118">Select **Access control (IAM)** from the left menu.</span></span>  
4. <span data-ttu-id="b97df-119">В колонке "Контроль доступа" содержится список всех пользователей, групп и приложений, которым предоставлен доступ к группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b97df-119">The Access control blade lists all users, groups, and applications that have been granted access to the resource group.</span></span>  
   
    ![Колонка "Пользователи" — унаследованные и назначенные права доступа — снимок экрана](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="b97df-121">Обратите внимание, что некоторые роли привязаны к **этому ресурсу**, а другие **унаследованы** из другой области.</span><span class="sxs-lookup"><span data-stu-id="b97df-121">Notice that some roles are scoped to **This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="b97df-122">Доступ специально назначается группе ресурсов или наследуется в результате назначения родительской подписке.</span><span class="sxs-lookup"><span data-stu-id="b97df-122">Access is either assigned specifically to the resource group or inherited from an assignment to the parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b97df-123">Классические администраторы и соадминистраторы подписки считаются владельцами подписки в новой модели RBAC.</span><span class="sxs-lookup"><span data-stu-id="b97df-123">Classic subscription admins and co-admins are considered owners of the subscription in the new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="b97df-124">Добавление доступа</span><span class="sxs-lookup"><span data-stu-id="b97df-124">Add Access</span></span>
<span data-ttu-id="b97df-125">Вы можете предоставить доступ в рамках ресурса, группы ресурсов или подписки, которые входят в область назначения роли.</span><span class="sxs-lookup"><span data-stu-id="b97df-125">You grant access from within the resource, resource group, or subscription that is the scope of the role assignment.</span></span>

1. <span data-ttu-id="b97df-126">В колонке "Контроль доступа" выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b97df-126">Select **Add** on the Access control blade.</span></span>  
2. <span data-ttu-id="b97df-127">Выберите роль, которую следует назначить, в колонке **Выбор роли** .</span><span class="sxs-lookup"><span data-stu-id="b97df-127">Select the role that you wish to assign from the **Select a role** blade.</span></span>
3. <span data-ttu-id="b97df-128">В каталоге выберите пользователя, группу или приложение, которым нужно предоставить доступ.</span><span class="sxs-lookup"><span data-stu-id="b97df-128">Select the user, group, or application in your directory that you wish to grant access to.</span></span> <span data-ttu-id="b97df-129">Поиск в каталоге можно выполнить по отображаемым именам, адресам электронной почты и идентификаторам объектов.</span><span class="sxs-lookup"><span data-stu-id="b97df-129">You can search the directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Колонка "Добавить пользователей" — "Поиск" — снимок экрана](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="b97df-131">Щелкните **ОК** , чтобы создать назначение.</span><span class="sxs-lookup"><span data-stu-id="b97df-131">Select **OK** to create the assignment.</span></span> <span data-ttu-id="b97df-132">Во всплывающем окне **Добавление пользователя** будет отображаться ход операции.</span><span class="sxs-lookup"><span data-stu-id="b97df-132">The **Adding user** popup tracks the progress.</span></span>  
    <span data-ttu-id="b97df-133">![Индикатор выполнения при добавлении пользователя — снимок экрана](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="b97df-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="b97df-134">Назначенная роль отобразится в колонке **Пользователи** .</span><span class="sxs-lookup"><span data-stu-id="b97df-134">After successfully adding a role assignment, it will appear on the **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="b97df-135">Запрет доступа</span><span class="sxs-lookup"><span data-stu-id="b97df-135">Remove Access</span></span>
1. <span data-ttu-id="b97df-136">Наведите курсор на имя назначения, которое нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="b97df-136">Hover your cursor over the name of the assignment that you want to remove.</span></span> <span data-ttu-id="b97df-137">Рядом с именем появится флажок.</span><span class="sxs-lookup"><span data-stu-id="b97df-137">A check box appears next to the name.</span></span>
2. <span data-ttu-id="b97df-138">Установите флажки, чтобы выбрать одно или несколько назначений ролей.</span><span class="sxs-lookup"><span data-stu-id="b97df-138">Use the check boxes to select one or more role assignments.</span></span>
2. <span data-ttu-id="b97df-139">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="b97df-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="b97df-140">Выберите **Да**, чтобы подтвердить удаление.</span><span class="sxs-lookup"><span data-stu-id="b97df-140">Select **Yes** to confirm the removal.</span></span>

<span data-ttu-id="b97df-141">Унаследованные назначения нельзя удалить.</span><span class="sxs-lookup"><span data-stu-id="b97df-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="b97df-142">Если необходимо удалить наследуемое назначение, это необходимо сделать в области, в которой было создано назначение роли.</span><span class="sxs-lookup"><span data-stu-id="b97df-142">If you need to remove an inherited assignment, you need to do it at the scope where the role assignment was created.</span></span> <span data-ttu-id="b97df-143">В столбце **Область** возле элемента **Унаследованный** есть ссылка, по которой можно перейти к ресурсам, которым была назначена эта роль.</span><span class="sxs-lookup"><span data-stu-id="b97df-143">In the **Scope** column, next to **Inherited** there is a link that takes you to the resources where this role was assigned.</span></span> <span data-ttu-id="b97df-144">Перейдите к ресурсу, который указан в этом разделе, чтобы удалить назначение роли.</span><span class="sxs-lookup"><span data-stu-id="b97df-144">Go to the resource listed there to remove the role assignment.</span></span>

![Колонка "Пользователи" — унаследованные права доступа отключают кнопку "Удалить" — снимок экрана](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-to-manage-access"></a><span data-ttu-id="b97df-146">Другие средства управления доступом</span><span class="sxs-lookup"><span data-stu-id="b97df-146">Other tools to manage access</span></span>
<span data-ttu-id="b97df-147">Вы можете назначать роли и управлять доступом с помощью модели RBAC Azure не только на портале Azure, но и с помощью других средств.</span><span class="sxs-lookup"><span data-stu-id="b97df-147">You can assign roles and manage access with Azure RBAC commands in tools other than the Azure portal.</span></span>  <span data-ttu-id="b97df-148">Ниже представлены ссылки на ресурсы с дополнительными сведениями о предварительных требованиях и начале работы с командами RBAC Azure.</span><span class="sxs-lookup"><span data-stu-id="b97df-148">Follow the links to learn more about the prerequisites and get started with the Azure RBAC commands.</span></span>

* [<span data-ttu-id="b97df-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b97df-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="b97df-150">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b97df-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="b97df-151">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="b97df-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="b97df-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b97df-152">Next Steps</span></span>
* [<span data-ttu-id="b97df-153">Создание отчета по журналу изменений доступа</span><span class="sxs-lookup"><span data-stu-id="b97df-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="b97df-154">Ознакомьтесь со статьей [RBAC: встроенные роли](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="b97df-154">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="b97df-155">Определите собственные [пользовательские роли в RBAC Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="b97df-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

