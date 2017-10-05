---
title: "Управление доступом на основе ролей (RBAC) с помощью Azure PowerShell | Документация Майкрософт"
description: "Узнайте, как осуществлять управление доступом на основе ролей (RBAC) с помощью Azure PowerShell, включая вывод списка ролей, назначение ролей и удаление назначений ролей."
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
ms.openlocfilehash: d7b11df21650b5cb27f9c3dd8306f8d12664185e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="6199e-103">Управление доступом на основе ролей с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6199e-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6199e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6199e-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="6199e-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="6199e-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="6199e-106">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="6199e-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="6199e-107">Функция управления доступом на основе ролей (RBAC) на портале Azure и в API управления ресурсами Azure позволяет управлять доступом к подписке с высокой точностью.</span><span class="sxs-lookup"><span data-stu-id="6199e-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Management API to manage access to your subscription at a fine-grained level.</span></span> <span data-ttu-id="6199e-108">С ее помощью вы можете предоставлять доступ пользователям, группам и субъектам-службам Active Directory, назначая им роли с определенной областью.</span><span class="sxs-lookup"><span data-stu-id="6199e-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="6199e-109">Чтобы использовать PowerShell для управления RBAC, необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="6199e-109">Before you can use PowerShell to manage RBAC, you need the following prerequisites:</span></span>

* <span data-ttu-id="6199e-110">Azure PowerShell версии 0.8.8 или выше.</span><span class="sxs-lookup"><span data-stu-id="6199e-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="6199e-111">Чтобы установить последнюю версию и связать ее со своей подпиской Azure, см. раздел об [установке и настройке Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6199e-111">To install the latest version and associate it with your Azure subscription, see [how to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="6199e-112">Командлеты Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6199e-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="6199e-113">Установите [командлеты Azure Resource Manager](/powershell/azure/overview) в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6199e-113">Install the [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="6199e-114">Вывод списка ролей</span><span class="sxs-lookup"><span data-stu-id="6199e-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="6199e-115">Вывод списка всех доступных ролей</span><span class="sxs-lookup"><span data-stu-id="6199e-115">List all available roles</span></span>
<span data-ttu-id="6199e-116">Для вывода списка доступных для назначения ролей RBAC и для просмотра операций, к которым они предоставляют доступ, воспользуйтесь командой `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="6199e-116">To list RBAC roles that are available for assignment and to inspect the operations to which they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="6199e-118">Вывод списка действий роли</span><span class="sxs-lookup"><span data-stu-id="6199e-118">List actions of a role</span></span>
<span data-ttu-id="6199e-119">Для вывода списка действий для определенной роли воспользуйтесь командой `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="6199e-119">To list the actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell — Get-AzureRmRoleDefinition для конкретной роли — снимок экрана](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="6199e-121">Увидеть, у кого есть доступ</span><span class="sxs-lookup"><span data-stu-id="6199e-121">See who has access</span></span>
<span data-ttu-id="6199e-122">Чтобы вывести список назначений доступа RBAC, используйте команду `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="6199e-122">To list RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="6199e-123">Вывод списка назначений ролей в конкретной области</span><span class="sxs-lookup"><span data-stu-id="6199e-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="6199e-124">Можно вывести список назначений доступа, действующих для указанной подписки, группы ресурсов или отдельного ресурса.</span><span class="sxs-lookup"><span data-stu-id="6199e-124">You can see all the access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="6199e-125">Например, чтобы просмотреть все активные назначения для группы ресурсов, используйте команду `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="6199e-125">For example, to see the all the active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell — Get-AzureRmRoleAssignment для группы ресурсов — снимок экрана](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-to-a-user"></a><span data-ttu-id="6199e-127">Вывод списка ролей, назначенных пользователю</span><span class="sxs-lookup"><span data-stu-id="6199e-127">List roles assigned to a user</span></span>
<span data-ttu-id="6199e-128">Чтобы вывести список всех ролей, назначенных пользователю, включая роли, назначенные группам, в которые он входит, используйте команду `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="6199e-128">To list all the roles that are assigned to a specified user and the roles that are assigned to the groups to which the user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell — Get-AzureRmRoleAssignment — для пользователя — снимок экрана](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="6199e-130">Вывод списка назначений ролей классического администратора службы и соадминистратора</span><span class="sxs-lookup"><span data-stu-id="6199e-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="6199e-131">Для вывода списка назначений доступа для классического администратора подписки и соадминистраторов воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6199e-131">To list access assignments for the classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="6199e-132">Предоставление доступа</span><span class="sxs-lookup"><span data-stu-id="6199e-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="6199e-133">Поиск идентификаторов объектов</span><span class="sxs-lookup"><span data-stu-id="6199e-133">Search for object IDs</span></span>
<span data-ttu-id="6199e-134">Чтобы назначить роль, необходимо определить объект (пользователя, группу или приложение) и область.</span><span class="sxs-lookup"><span data-stu-id="6199e-134">To assign a role, you need to identify both the object (user, group, or application) and the scope.</span></span>

<span data-ttu-id="6199e-135">Если вам неизвестен идентификатор подписки, его можно найти в колонке **Подписки** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6199e-135">If you don't know the subscription ID, you can find it in the **Subscriptions** blade on the Azure portal.</span></span> <span data-ttu-id="6199e-136">Узнайте на сайте MSDN, как запросить идентификатор подписки с помощью [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="6199e-136">To learn how to query for the subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="6199e-137">Для поиска идентификатора объекта для группы Azure AD воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6199e-137">To get the object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="6199e-138">Чтобы получить идентификатор объекта для субъекта-службы Azure AD или приложения, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6199e-138">To get the object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="6199e-139">Назначение роли для приложения в области действия подписки</span><span class="sxs-lookup"><span data-stu-id="6199e-139">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="6199e-140">Чтобы предоставить доступ к приложению в области действия подписки, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6199e-140">To grant access to an application at the subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell — New-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="6199e-142">Назначение роли пользователю в области действия группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="6199e-142">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="6199e-143">Для предоставления доступа пользователю в области действия группы ресурсов воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6199e-143">To grant access to a user at the resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell — New-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="6199e-145">Назначение роли для группы в области действия ресурса</span><span class="sxs-lookup"><span data-stu-id="6199e-145">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="6199e-146">Для предоставления доступа группе в области действия ресурса воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6199e-146">To grant access to a group at the resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell — New-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="6199e-148">Запрет доступа</span><span class="sxs-lookup"><span data-stu-id="6199e-148">Remove access</span></span>
<span data-ttu-id="6199e-149">Чтобы запретить доступ для пользователей, групп и приложений, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="6199e-149">To remove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell — Remove-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="6199e-151">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="6199e-151">Create a custom role</span></span>
<span data-ttu-id="6199e-152">Чтобы создать настраиваемую роль, используйте команду ```New-AzureRmRoleDefinition``` .</span><span class="sxs-lookup"><span data-stu-id="6199e-152">To create a custom role, use the ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="6199e-153">Существует два способа структурирования роли: с помощью PSRoleDefinitionObject и с помощью шаблона JSON.</span><span class="sxs-lookup"><span data-stu-id="6199e-153">There are two methods of structuring the role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="6199e-154">Получение действий для поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="6199e-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="6199e-155">При создании пользовательских ролей с нуля важно знать все возможные операции поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6199e-155">When You are creating custom roles from scratch, it is important to know all the possible operations from the resource providers.</span></span>
<span data-ttu-id="6199e-156">Используйте команду ```Get-AzureRMProviderOperation``` для получения этих сведений.</span><span class="sxs-lookup"><span data-stu-id="6199e-156">Use the ```Get-AzureRMProviderOperation``` command to get this information.</span></span>
<span data-ttu-id="6199e-157">Например, если вы хотите проверить все доступные операции для виртуальной машины, то используйте эту команду:</span><span class="sxs-lookup"><span data-stu-id="6199e-157">For example, if you want to check all the available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="6199e-158">Создание роли с помощью PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="6199e-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="6199e-159">При создании пользовательской роли с помощью PowerShell можно начать с нуля или использовать одну из [встроенных ролей](role-based-access-built-in-roles.md) в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="6199e-159">When you use PowerShell to create a custom role, you can start from scratch or use one of the [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="6199e-160">В этом разделе приводится пример, в котором встроенная роль берется за основу, а затем настраивается с помощью дополнительных привилегий.</span><span class="sxs-lookup"><span data-stu-id="6199e-160">The example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="6199e-161">Измените атрибуты и добавьте необходимые действия *Actions*, *notActions* и области *scopes*, а затем сохраните изменения как новую роль.</span><span class="sxs-lookup"><span data-stu-id="6199e-161">Edit the attributes to add the *Actions*, *notActions*, or *scopes* that you want, and then save the changes as a new role.</span></span>

<span data-ttu-id="6199e-162">Следующий пример начинается с роли *Участник виртуальной машины*, с помощью которой создается настраиваемая роль *Оператор виртуальной машины*.</span><span class="sxs-lookup"><span data-stu-id="6199e-162">The following example starts with the *Virtual Machine Contributor* role and uses that to create a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="6199e-163">Новая роль предоставляет доступ ко всем операциям чтения поставщиков ресурсов *Microsoft.Compute*, *Microsoft.Storage* и *Microsoft.Network*, а также доступ для запуска, перезапуска и мониторинга виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="6199e-163">The new role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="6199e-164">Настраиваемую роль можно использовать в двух подписках.</span><span class="sxs-lookup"><span data-stu-id="6199e-164">The custom role can be used in two subscriptions.</span></span>

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

### <a name="create-role-with-json-template"></a><span data-ttu-id="6199e-166">Создание роли с помощью шаблона JSON</span><span class="sxs-lookup"><span data-stu-id="6199e-166">Create role with JSON template</span></span>
<span data-ttu-id="6199e-167">Шаблон JSON может использоваться в качестве определения источника для пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="6199e-167">A JSON template can be used as the source definition for the custom role.</span></span> <span data-ttu-id="6199e-168">В следующем примере создается пользовательская роль, которая разрешает доступ на чтение к хранилищу и вычислительным ресурсам, доступ для поддержки, и добавляет эту роль к двум подпискам.</span><span class="sxs-lookup"><span data-stu-id="6199e-168">The following example creates a custom role that allows read access to storage and compute resources, access to support, and adds that role to two subscriptions.</span></span> <span data-ttu-id="6199e-169">Создайте файл `C:\CustomRoles\customrole1.json` с приведенным ниже содержимым.</span><span class="sxs-lookup"><span data-stu-id="6199e-169">Create a new file `C:\CustomRoles\customrole1.json` with the following example.</span></span> <span data-ttu-id="6199e-170">При первичном создании роли идентификатору должно быть присвоено значение `null`, так как новый идентификатор создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="6199e-170">The Id should be set to `null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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
<span data-ttu-id="6199e-171">Чтобы добавить роль к подпискам, выполните следующую команду PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6199e-171">To add the role to the subscriptions, run the following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="6199e-172">Изменение настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="6199e-172">Modify a custom role</span></span>
<span data-ttu-id="6199e-173">Аналогично созданию пользовательской роли вы можете изменить существующую пользовательскую роль с помощью PSRoleDefinitionObject или шаблона JSON.</span><span class="sxs-lookup"><span data-stu-id="6199e-173">Similar to creating a custom role, you can modify an existing custom role using either the PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="6199e-174">Изменение роли с помощью PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="6199e-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="6199e-175">Чтобы изменить настраиваемую роль, сначала используйте команду `Get-AzureRmRoleDefinition` для получения определения роли.</span><span class="sxs-lookup"><span data-stu-id="6199e-175">To modify a custom role, first, use the `Get-AzureRmRoleDefinition` command to retrieve the role definition.</span></span> <span data-ttu-id="6199e-176">Затем внесите необходимые изменения в определение роли.</span><span class="sxs-lookup"><span data-stu-id="6199e-176">Second, make the desired changes to the role definition.</span></span> <span data-ttu-id="6199e-177">Наконец, с помощью команды `Set-AzureRmRoleDefinition` сохраните измененное определение роли.</span><span class="sxs-lookup"><span data-stu-id="6199e-177">Finally, use the `Set-AzureRmRoleDefinition` command to save the modified role definition.</span></span>

<span data-ttu-id="6199e-178">В следующем примере показано добавление операции `Microsoft.Insights/diagnosticSettings/*` к настраиваемой роли *Оператор виртуальной машины* .</span><span class="sxs-lookup"><span data-stu-id="6199e-178">The following example adds the `Microsoft.Insights/diagnosticSettings/*` operation to the *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell — Set-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="6199e-180">В следующем примере показано добавление подписки Azure в назначаемые области настраиваемой роли *Оператор виртуальной машины* .</span><span class="sxs-lookup"><span data-stu-id="6199e-180">The following example adds an Azure subscription to the assignable scopes of the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell — Set-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="6199e-182">Изменение роли с помощью шаблона JSON</span><span class="sxs-lookup"><span data-stu-id="6199e-182">Modify role with JSON template</span></span>
<span data-ttu-id="6199e-183">С помощью предыдущего шаблона JSON можно легко изменить существующую пользовательскую роль, чтобы добавить или удалить действия.</span><span class="sxs-lookup"><span data-stu-id="6199e-183">Using the previous JSON template, you can easily modify an existing custom role to add or remove Actions.</span></span> <span data-ttu-id="6199e-184">Обновите шаблон JSON и добавьте действие чтения для сетевых подключений, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="6199e-184">Update the JSON template and add the read action for networking as shown in the following example.</span></span> <span data-ttu-id="6199e-185">Определения, перечисленные в шаблоне, не применяются все вместе к существующему определению. Это означает, что роль отображается так, как указано в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="6199e-185">The definitions listed in the template are not cumulatively applied to an existing definition, meaning that the role appears exactly as you specify in the template.</span></span> <span data-ttu-id="6199e-186">Кроме того, необходимо обновить поле идентификатора с помощью идентификатора роли.</span><span class="sxs-lookup"><span data-stu-id="6199e-186">You also need to update the Id field with the ID of the role.</span></span> <span data-ttu-id="6199e-187">Если вы не уверены, каким является это значение, для получения этой информации можно использовать командлет `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="6199e-187">If you aren't sure what this value is, you can use the `Get-AzureRmRoleDefinition` cmdlet to get this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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

<span data-ttu-id="6199e-188">Чтобы обновить существующую роль, выполните следующую команду PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6199e-188">To update the existing role, run the following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="6199e-189">Удаление настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="6199e-189">Delete a custom role</span></span>
<span data-ttu-id="6199e-190">Чтобы удалить настраиваемую роль, используйте команду `Remove-AzureRmRoleDefinition` .</span><span class="sxs-lookup"><span data-stu-id="6199e-190">To delete a custom role, use the `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="6199e-191">В следующем примере показано удаление настраиваемой роли *Оператор виртуальной машины* .</span><span class="sxs-lookup"><span data-stu-id="6199e-191">The following example removes the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell — Remove-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="6199e-193">Вывод списка настраиваемых ролей</span><span class="sxs-lookup"><span data-stu-id="6199e-193">List custom roles</span></span>
<span data-ttu-id="6199e-194">Чтобы получить список ролей, доступных для назначения в области, используйте команду `Get-AzureRmRoleDefinition` .</span><span class="sxs-lookup"><span data-stu-id="6199e-194">To list the roles that are available for assignment at a scope, use the `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="6199e-195">В следующем примере перечисляются все роли, доступные для назначения в выбранной подписке.</span><span class="sxs-lookup"><span data-stu-id="6199e-195">The following example lists all roles that are available for assignment in the selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="6199e-197">В следующем примере настраиваемая роль *Оператор виртуальной машины* не доступна в подписке *Production4*, так как эта подписка не входит в **AssignableScopes** роли.</span><span class="sxs-lookup"><span data-stu-id="6199e-197">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="6199e-199">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="6199e-199">See also</span></span>
* <span data-ttu-id="6199e-200">[Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="6199e-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

