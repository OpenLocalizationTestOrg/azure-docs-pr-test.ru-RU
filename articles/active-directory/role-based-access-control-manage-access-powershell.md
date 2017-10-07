---
title: "aaaManage Role-Based ролей (RBAC) с помощью Azure PowerShell | Документы Microsoft"
description: "Как toomanage RBAC с помощью Azure PowerShell, включая список ролей, назначение ролей и удаление назначений ролей."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="a84af-103">Управление доступом на основе ролей с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a84af-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a84af-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a84af-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="a84af-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="a84af-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="a84af-106">REST API</span><span class="sxs-lookup"><span data-stu-id="a84af-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="a84af-107">Управление доступом на основе ролей (RBAC) можно использовать в hello портал Azure и API управления Azure ресурсов toomanage доступа tooyour подписки детально уровне.</span><span class="sxs-lookup"><span data-stu-id="a84af-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Management API toomanage access tooyour subscription at a fine-grained level.</span></span> <span data-ttu-id="a84af-108">С помощью этой функции можно предоставить доступ для пользователей, группы или субъекты-службы Active Directory путем назначения некоторых ролей toothem на определенную область.</span><span class="sxs-lookup"><span data-stu-id="a84af-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="a84af-109">Прежде чем использовать PowerShell toomanage RBAC, требуется hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="a84af-109">Before you can use PowerShell toomanage RBAC, you need hello following prerequisites:</span></span>

* <span data-ttu-id="a84af-110">Azure PowerShell версии 0.8.8 или выше.</span><span class="sxs-lookup"><span data-stu-id="a84af-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="a84af-111">последнюю версию tooinstall hello и связывание его с подпиской Azure. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a84af-111">tooinstall hello latest version and associate it with your Azure subscription, see [how tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="a84af-112">Командлеты Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a84af-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="a84af-113">Установка hello [командлеты диспетчера ресурсов Azure](/powershell/azure/overview) в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a84af-113">Install hello [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="a84af-114">Вывод списка ролей</span><span class="sxs-lookup"><span data-stu-id="a84af-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="a84af-115">Вывод списка всех доступных ролей</span><span class="sxs-lookup"><span data-stu-id="a84af-115">List all available roles</span></span>
<span data-ttu-id="a84af-116">toolist RBAC ролей, доступных для назначения и tooinspect hello операций toowhich они предоставлять доступ, используйте `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="a84af-116">toolist RBAC roles that are available for assignment and tooinspect hello operations toowhich they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="a84af-118">Вывод списка действий роли</span><span class="sxs-lookup"><span data-stu-id="a84af-118">List actions of a role</span></span>
<span data-ttu-id="a84af-119">Используйте действия hello toolist для определенной роли, `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="a84af-119">toolist hello actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell — Get-AzureRmRoleDefinition для конкретной роли — снимок экрана](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="a84af-121">Увидеть, у кого есть доступ</span><span class="sxs-lookup"><span data-stu-id="a84af-121">See who has access</span></span>
<span data-ttu-id="a84af-122">назначения доступа RBAC toolist, используют `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="a84af-122">toolist RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="a84af-123">Вывод списка назначений ролей в конкретной области</span><span class="sxs-lookup"><span data-stu-id="a84af-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="a84af-124">Вы увидите все назначения hello доступа для указанной подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a84af-124">You can see all hello access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="a84af-125">Например, toosee hello все назначения hello активные группы ресурсов, используйте `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="a84af-125">For example, toosee hello all hello active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell — Get-AzureRmRoleAssignment для группы ресурсов — снимок экрана](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a><span data-ttu-id="a84af-127">Список ролей, назначенный пользователь tooa</span><span class="sxs-lookup"><span data-stu-id="a84af-127">List roles assigned tooa user</span></span>
<span data-ttu-id="a84af-128">все роли hello, назначенных tooa указанного пользователя и роли hello, которые назначаются toohello группам принадлежит пользователь toowhich hello, toolist используйте `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="a84af-128">toolist all hello roles that are assigned tooa specified user and hello roles that are assigned toohello groups toowhich hello user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell — Get-AzureRmRoleAssignment — для пользователя — снимок экрана](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="a84af-130">Вывод списка назначений ролей классического администратора службы и соадминистратора</span><span class="sxs-lookup"><span data-stu-id="a84af-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="a84af-131">назначения toolist доступ для администратора классическую подписку hello и coadministrators, используйте:</span><span class="sxs-lookup"><span data-stu-id="a84af-131">toolist access assignments for hello classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="a84af-132">Предоставление доступа</span><span class="sxs-lookup"><span data-stu-id="a84af-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="a84af-133">Поиск идентификаторов объектов</span><span class="sxs-lookup"><span data-stu-id="a84af-133">Search for object IDs</span></span>
<span data-ttu-id="a84af-134">tooassign роли необходимо tooidentify hello объекта (пользователя, группы или приложения) и область hello.</span><span class="sxs-lookup"><span data-stu-id="a84af-134">tooassign a role, you need tooidentify both hello object (user, group, or application) and hello scope.</span></span>

<span data-ttu-id="a84af-135">Если вы не знаете идентификатор подписки hello, его можно найти в hello **подписки** колонка на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a84af-135">If you don't know hello subscription ID, you can find it in hello **Subscriptions** blade on hello Azure portal.</span></span> <span data-ttu-id="a84af-136">статье tooquery для подписки с Идентификатором hello, toolearn [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="a84af-136">toolearn how tooquery for hello subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="a84af-137">Используйте идентификатор объекта hello tooget для группы Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a84af-137">tooget hello object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="a84af-138">Идентификатор объекта tooget hello Azure AD участника-службы или приложения, используйте:</span><span class="sxs-lookup"><span data-stu-id="a84af-138">tooget hello object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="a84af-139">Назначение роли приложения tooan в области видимости hello подписки</span><span class="sxs-lookup"><span data-stu-id="a84af-139">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="a84af-140">приложение tooan toogrant доступ в области hello подписки, используйте:</span><span class="sxs-lookup"><span data-stu-id="a84af-140">toogrant access tooan application at hello subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell — New-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="a84af-142">Назначить пользователя роли tooa в области группы ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="a84af-142">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="a84af-143">доступ к toogrant tooa пользователю в области группы ресурсов hello, используйте:</span><span class="sxs-lookup"><span data-stu-id="a84af-143">toogrant access tooa user at hello resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell — New-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="a84af-145">Назначение роли tooa группы в области видимости ресурса hello</span><span class="sxs-lookup"><span data-stu-id="a84af-145">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="a84af-146">Группа tooa toogrant доступ в области видимости ресурса hello, используйте:</span><span class="sxs-lookup"><span data-stu-id="a84af-146">toogrant access tooa group at hello resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell — New-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="a84af-148">Запрет доступа</span><span class="sxs-lookup"><span data-stu-id="a84af-148">Remove access</span></span>
<span data-ttu-id="a84af-149">tooremove доступ для пользователей, групп и приложений, используйте:</span><span class="sxs-lookup"><span data-stu-id="a84af-149">tooremove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell — Remove-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="a84af-151">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="a84af-151">Create a custom role</span></span>
<span data-ttu-id="a84af-152">toocreate пользовательской роли, используйте hello ```New-AzureRmRoleDefinition``` команды.</span><span class="sxs-lookup"><span data-stu-id="a84af-152">toocreate a custom role, use hello ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="a84af-153">Существует два способа структурирования hello роли, с помощью шаблона JSON или PSRoleDefinitionObject.</span><span class="sxs-lookup"><span data-stu-id="a84af-153">There are two methods of structuring hello role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="a84af-154">Получение действий для поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="a84af-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="a84af-155">При создании пользовательских ролей с нуля, является важным tooknow все hello возможных операций из поставщиков ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="a84af-155">When You are creating custom roles from scratch, it is important tooknow all hello possible operations from hello resource providers.</span></span>
<span data-ttu-id="a84af-156">Используйте hello ```Get-AzureRMProviderOperation``` команды tooget эти сведения.</span><span class="sxs-lookup"><span data-stu-id="a84af-156">Use hello ```Get-AzureRMProviderOperation``` command tooget this information.</span></span>
<span data-ttu-id="a84af-157">Например если требуется, чтобы toocheck всех доступных операций hello для виртуальной машины используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a84af-157">For example, if you want toocheck all hello available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="a84af-158">Создание роли с помощью PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="a84af-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="a84af-159">При использовании PowerShell toocreate пользовательской роли, можно запустить с нуля или использовать один из hello [встроенные роли](role-based-access-built-in-roles.md) отправной точки.</span><span class="sxs-lookup"><span data-stu-id="a84af-159">When you use PowerShell toocreate a custom role, you can start from scratch or use one of hello [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="a84af-160">пример Hello в этом разделе начинается с встроенной роли и затем настраивает его с больше прав доступа.</span><span class="sxs-lookup"><span data-stu-id="a84af-160">hello example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="a84af-161">Изменить hello атрибуты tooadd hello *действия*, *notActions*, или *областей* , а затем сохранить hello в качестве новой роли.</span><span class="sxs-lookup"><span data-stu-id="a84af-161">Edit hello attributes tooadd hello *Actions*, *notActions*, or *scopes* that you want, and then save hello changes as a new role.</span></span>

<span data-ttu-id="a84af-162">Hello следующий пример начинается с hello *участника виртуальной машины* вызывается роли и использование этой пользовательской роли toocreate *оператор виртуальной машины*.</span><span class="sxs-lookup"><span data-stu-id="a84af-162">hello following example starts with hello *Virtual Machine Contributor* role and uses that toocreate a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="a84af-163">предоставляет новую роль Hello считываемых доступа tooall *Microsoft.Compute*, *хранилища Майкрософт*, и *Microsoft.Network* поставщиков и предоставляет доступ к ресурсам toostart, перезапуска и мониторинга виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a84af-163">hello new role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="a84af-164">Hello пользовательской роли можно использовать в две подписки.</span><span class="sxs-lookup"><span data-stu-id="a84af-164">hello custom role can be used in two subscriptions.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a><span data-ttu-id="a84af-166">Создание роли с помощью шаблона JSON</span><span class="sxs-lookup"><span data-stu-id="a84af-166">Create role with JSON template</span></span>
<span data-ttu-id="a84af-167">Можно использовать шаблон JSON как определение источника hello для hello пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="a84af-167">A JSON template can be used as hello source definition for hello custom role.</span></span> <span data-ttu-id="a84af-168">Hello следующий пример создает пользовательскую роль, который позволяет toostorage доступ для чтения и вычислительные ресурсы, доступ к toosupport и добавляет этой роли tootwo подписки.</span><span class="sxs-lookup"><span data-stu-id="a84af-168">hello following example creates a custom role that allows read access toostorage and compute resources, access toosupport, and adds that role tootwo subscriptions.</span></span> <span data-ttu-id="a84af-169">Создайте новый файл `C:\CustomRoles\customrole1.json` с hello в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="a84af-169">Create a new file `C:\CustomRoles\customrole1.json` with hello following example.</span></span> <span data-ttu-id="a84af-170">Hello Id должно быть установлено слишком`null` на создание начальной роли как новый идентификатор создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="a84af-170">hello Id should be set too`null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
<span data-ttu-id="a84af-171">tooadd hello роли toohello подписки, запустите следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="a84af-171">tooadd hello role toohello subscriptions, run hello following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="a84af-172">Изменение настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="a84af-172">Modify a custom role</span></span>
<span data-ttu-id="a84af-173">Аналогичные toocreating пользовательской роли, можно изменить существующие пользовательской роли, с помощью hello PSRoleDefinitionObject или шаблон JSON.</span><span class="sxs-lookup"><span data-stu-id="a84af-173">Similar toocreating a custom role, you can modify an existing custom role using either hello PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="a84af-174">Изменение роли с помощью PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="a84af-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="a84af-175">toomodify пользовательской роли, во-первых, используйте hello `Get-AzureRmRoleDefinition` определение роли hello tooretrieve команды.</span><span class="sxs-lookup"><span data-stu-id="a84af-175">toomodify a custom role, first, use hello `Get-AzureRmRoleDefinition` command tooretrieve hello role definition.</span></span> <span data-ttu-id="a84af-176">Во-вторых измените hello требуемого toohello определения роли.</span><span class="sxs-lookup"><span data-stu-id="a84af-176">Second, make hello desired changes toohello role definition.</span></span> <span data-ttu-id="a84af-177">Наконец, используйте hello `Set-AzureRmRoleDefinition` команда toosave hello изменения определения роли.</span><span class="sxs-lookup"><span data-stu-id="a84af-177">Finally, use hello `Set-AzureRmRoleDefinition` command toosave hello modified role definition.</span></span>

<span data-ttu-id="a84af-178">Hello следующий пример добавляет hello `Microsoft.Insights/diagnosticSettings/*` toohello операции *оператор виртуальной машины* пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="a84af-178">hello following example adds hello `Microsoft.Insights/diagnosticSettings/*` operation toohello *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell — Set-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="a84af-180">Hello пример добавления подписки Azure toohello назначаемых областей из hello *оператор виртуальной машины* пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="a84af-180">hello following example adds an Azure subscription toohello assignable scopes of hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell — Set-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="a84af-182">Изменение роли с помощью шаблона JSON</span><span class="sxs-lookup"><span data-stu-id="a84af-182">Modify role with JSON template</span></span>
<span data-ttu-id="a84af-183">С помощью предыдущего шаблона JSON hello, можно легко изменить существующий tooadd пользовательской роли или удалить действия.</span><span class="sxs-lookup"><span data-stu-id="a84af-183">Using hello previous JSON template, you can easily modify an existing custom role tooadd or remove Actions.</span></span> <span data-ttu-id="a84af-184">Обновление шаблона JSON hello и добавить действие чтения hello для работы в сети, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="a84af-184">Update hello JSON template and add hello read action for networking as shown in hello following example.</span></span> <span data-ttu-id="a84af-185">Hello определений, перечисленных в шаблоне hello не Суммарно примененных tooan существующее определение, это означает, что эта роль hello отображается точно так, как указать в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="a84af-185">hello definitions listed in hello template are not cumulatively applied tooan existing definition, meaning that hello role appears exactly as you specify in hello template.</span></span> <span data-ttu-id="a84af-186">Необходимо также поле Id hello tooupdate с Идентификатором hello hello роли.</span><span class="sxs-lookup"><span data-stu-id="a84af-186">You also need tooupdate hello Id field with hello ID of hello role.</span></span> <span data-ttu-id="a84af-187">Если вы не уверены, что это значение равно, можно использовать hello `Get-AzureRmRoleDefinition` tooget командлет эти сведения.</span><span class="sxs-lookup"><span data-stu-id="a84af-187">If you aren't sure what this value is, you can use hello `Get-AzureRmRoleDefinition` cmdlet tooget this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

<span data-ttu-id="a84af-188">существующие роли hello tooupdate, запустите следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="a84af-188">tooupdate hello existing role, run hello following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="a84af-189">Удаление настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="a84af-189">Delete a custom role</span></span>
<span data-ttu-id="a84af-190">toodelete пользовательской роли, используйте hello `Remove-AzureRmRoleDefinition` команды.</span><span class="sxs-lookup"><span data-stu-id="a84af-190">toodelete a custom role, use hello `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="a84af-191">Hello следующий пример удаляет hello *оператор виртуальной машины* пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="a84af-191">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell — Remove-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="a84af-193">Вывод списка настраиваемых ролей</span><span class="sxs-lookup"><span data-stu-id="a84af-193">List custom roles</span></span>
<span data-ttu-id="a84af-194">toolist hello ролей, доступных для назначения в области, используйте hello `Get-AzureRmRoleDefinition` команды.</span><span class="sxs-lookup"><span data-stu-id="a84af-194">toolist hello roles that are available for assignment at a scope, use hello `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="a84af-195">Следующий пример Hello список всех ролей, доступных для назначения в подписке hello выбран.</span><span class="sxs-lookup"><span data-stu-id="a84af-195">hello following example lists all roles that are available for assignment in hello selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="a84af-197">В следующем примере hello, hello *оператор виртуальной машины* пользовательской роли не предусмотрена в hello *Production4* подписки, так как ее нет в hello  **AssignableScopes** hello роли.</span><span class="sxs-lookup"><span data-stu-id="a84af-197">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="a84af-199">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a84af-199">See also</span></span>
* <span data-ttu-id="a84af-200">[Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="a84af-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

