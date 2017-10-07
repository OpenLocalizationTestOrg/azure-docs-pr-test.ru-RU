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
# <a name="manage-role-based-access-control-with-azure-powershell"></a>Управление доступом на основе ролей с помощью Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Интерфейс командной строки Azure](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

Управление доступом на основе ролей (RBAC) можно использовать в hello портал Azure и API управления Azure ресурсов toomanage доступа tooyour подписки детально уровне. С помощью этой функции можно предоставить доступ для пользователей, группы или субъекты-службы Active Directory путем назначения некоторых ролей toothem на определенную область.

Прежде чем использовать PowerShell toomanage RBAC, требуется hello следующие предварительные требования:

* Azure PowerShell версии 0.8.8 или выше. последнюю версию tooinstall hello и связывание его с подпиской Azure. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
* Командлеты Azure Resource Manager. Установка hello [командлеты диспетчера ресурсов Azure](/powershell/azure/overview) в PowerShell.

## <a name="list-roles"></a>Вывод списка ролей
### <a name="list-all-available-roles"></a>Вывод списка всех доступных ролей
toolist RBAC ролей, доступных для назначения и tooinspect hello операций toowhich они предоставлять доступ, используйте `Get-AzureRmRoleDefinition`.

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>Вывод списка действий роли
Используйте действия hello toolist для определенной роли, `Get-AzureRmRoleDefinition <role name>`.

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell — Get-AzureRmRoleDefinition для конкретной роли — снимок экрана](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>Увидеть, у кого есть доступ
назначения доступа RBAC toolist, используют `Get-AzureRmRoleAssignment`.

### <a name="list-role-assignments-at-a-specific-scope"></a>Вывод списка назначений ролей в конкретной области
Вы увидите все назначения hello доступа для указанной подписки, группы ресурсов или ресурсов. Например, toosee hello все назначения hello активные группы ресурсов, используйте `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell — Get-AzureRmRoleAssignment для группы ресурсов — снимок экрана](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>Список ролей, назначенный пользователь tooa
все роли hello, назначенных tooa указанного пользователя и роли hello, которые назначаются toohello группам принадлежит пользователь toowhich hello, toolist используйте `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell — Get-AzureRmRoleAssignment — для пользователя — снимок экрана](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>Вывод списка назначений ролей классического администратора службы и соадминистратора
назначения toolist доступ для администратора классическую подписку hello и coadministrators, используйте:

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>Предоставление доступа
### <a name="search-for-object-ids"></a>Поиск идентификаторов объектов
tooassign роли необходимо tooidentify hello объекта (пользователя, группы или приложения) и область hello.

Если вы не знаете идентификатор подписки hello, его можно найти в hello **подписки** колонка на hello портал Azure. статье tooquery для подписки с Идентификатором hello, toolearn [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) на сайте MSDN.

Используйте идентификатор объекта hello tooget для группы Azure AD:

    Get-AzureRmADGroup -SearchString <group name in quotes>

Идентификатор объекта tooget hello Azure AD участника-службы или приложения, используйте:

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Назначение роли приложения tooan в области видимости hello подписки
приложение tooan toogrant доступ в области hello подписки, используйте:

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell — New-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Назначить пользователя роли tooa в области группы ресурсов hello
доступ к toogrant tooa пользователю в области группы ресурсов hello, используйте:

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell — New-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Назначение роли tooa группы в области видимости ресурса hello
Группа tooa toogrant доступ в области видимости ресурса hello, используйте:

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell — New-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>Запрет доступа
tooremove доступ для пользователей, групп и приложений, используйте:

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell — Remove-AzureRmRoleAssignment — снимок экрана](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>Создание настраиваемой роли
toocreate пользовательской роли, используйте hello ```New-AzureRmRoleDefinition``` команды. Существует два способа структурирования hello роли, с помощью шаблона JSON или PSRoleDefinitionObject. 

## <a name="get-actions-for-a-resource-provider"></a>Получение действий для поставщика ресурсов
При создании пользовательских ролей с нуля, является важным tooknow все hello возможных операций из поставщиков ресурсов hello.
Используйте hello ```Get-AzureRMProviderOperation``` команды tooget эти сведения.
Например если требуется, чтобы toocheck всех доступных операций hello для виртуальной машины используйте следующую команду:

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>Создание роли с помощью PSRoleDefinitionObject
При использовании PowerShell toocreate пользовательской роли, можно запустить с нуля или использовать один из hello [встроенные роли](role-based-access-built-in-roles.md) отправной точки. пример Hello в этом разделе начинается с встроенной роли и затем настраивает его с больше прав доступа. Изменить hello атрибуты tooadd hello *действия*, *notActions*, или *областей* , а затем сохранить hello в качестве новой роли.

Hello следующий пример начинается с hello *участника виртуальной машины* вызывается роли и использование этой пользовательской роли toocreate *оператор виртуальной машины*. предоставляет новую роль Hello считываемых доступа tooall *Microsoft.Compute*, *хранилища Майкрософт*, и *Microsoft.Network* поставщиков и предоставляет доступ к ресурсам toostart, перезапуска и мониторинга виртуальных машин. Hello пользовательской роли можно использовать в две подписки.

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

### <a name="create-role-with-json-template"></a>Создание роли с помощью шаблона JSON
Можно использовать шаблон JSON как определение источника hello для hello пользовательской роли. Hello следующий пример создает пользовательскую роль, который позволяет toostorage доступ для чтения и вычислительные ресурсы, доступ к toosupport и добавляет этой роли tootwo подписки. Создайте новый файл `C:\CustomRoles\customrole1.json` с hello в следующем примере. Hello Id должно быть установлено слишком`null` на создание начальной роли как новый идентификатор создается автоматически. 

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
tooadd hello роли toohello подписки, запустите следующую команду PowerShell hello:
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>Изменение настраиваемой роли
Аналогичные toocreating пользовательской роли, можно изменить существующие пользовательской роли, с помощью hello PSRoleDefinitionObject или шаблон JSON.

### <a name="modify-role-with-psroledefinitionobject"></a>Изменение роли с помощью PSRoleDefinitionObject
toomodify пользовательской роли, во-первых, используйте hello `Get-AzureRmRoleDefinition` определение роли hello tooretrieve команды. Во-вторых измените hello требуемого toohello определения роли. Наконец, используйте hello `Set-AzureRmRoleDefinition` команда toosave hello изменения определения роли.

Hello следующий пример добавляет hello `Microsoft.Insights/diagnosticSettings/*` toohello операции *оператор виртуальной машины* пользовательской роли.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell — Set-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

Hello пример добавления подписки Azure toohello назначаемых областей из hello *оператор виртуальной машины* пользовательской роли.

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell — Set-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>Изменение роли с помощью шаблона JSON
С помощью предыдущего шаблона JSON hello, можно легко изменить существующий tooadd пользовательской роли или удалить действия. Обновление шаблона JSON hello и добавить действие чтения hello для работы в сети, как показано в следующий пример hello. Hello определений, перечисленных в шаблоне hello не Суммарно примененных tooan существующее определение, это означает, что эта роль hello отображается точно так, как указать в шаблоне hello. Необходимо также поле Id hello tooupdate с Идентификатором hello hello роли. Если вы не уверены, что это значение равно, можно использовать hello `Get-AzureRmRoleDefinition` tooget командлет эти сведения.

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

существующие роли hello tooupdate, запустите следующую команду PowerShell hello:
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>Удаление настраиваемой роли
toodelete пользовательской роли, используйте hello `Remove-AzureRmRoleDefinition` команды.

Hello следующий пример удаляет hello *оператор виртуальной машины* пользовательской роли.

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell — Remove-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>Вывод списка настраиваемых ролей
toolist hello ролей, доступных для назначения в области, используйте hello `Get-AzureRmRoleDefinition` команды.

Следующий пример Hello список всех ролей, доступных для назначения в подписке hello выбран.

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

В следующем примере hello, hello *оператор виртуальной машины* пользовательской роли не предусмотрена в hello *Production4* подписки, так как ее нет в hello  **AssignableScopes** hello роли.

![RBAC PowerShell — Get-AzureRmRoleDefinition — снимок экрана](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>Дополнительные материалы
* [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

