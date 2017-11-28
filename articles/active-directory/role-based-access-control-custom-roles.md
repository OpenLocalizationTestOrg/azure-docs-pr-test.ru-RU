---
title: "aaaCreate пользовательских ролей в RBAC Azure. | Документы Microsoft"
description: "Узнайте, как пользовательские роли toodefine с контроля доступа для более точного управления удостоверениями в вашей подписке Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="37f10-103">Создание пользовательских ролей для управления доступом на основе ролей в Azure</span><span class="sxs-lookup"><span data-stu-id="37f10-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="37f10-104">Создайте пользовательскую роль в управления доступом Azure Role-Based (RBAC), если ни один из встроенных ролей hello соответствует потребностям специальный доступ.</span><span class="sxs-lookup"><span data-stu-id="37f10-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="37f10-105">Можно создать настраиваемые роли с помощью [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [интерфейса командной строки Azure](role-based-access-control-manage-access-azure-cli.md) (CLI) и hello [API-интерфейса REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="37f10-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="37f10-106">Так же, как и встроенные роли можно назначить toousers пользовательские роли, группы и приложения в подписке, группы ресурсов и ресурсов областей.</span><span class="sxs-lookup"><span data-stu-id="37f10-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="37f10-107">Пользовательские роли хранятся в клиенте Azure AD и могут использоваться несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="37f10-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="37f10-108">Каждый клиент можно создать пользовательские роли too2000.</span><span class="sxs-lookup"><span data-stu-id="37f10-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="37f10-109">Hello ниже приведен пример пользовательской роли для мониторинга и перезапуска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="37f10-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a><span data-ttu-id="37f10-110">Действия</span><span class="sxs-lookup"><span data-stu-id="37f10-110">Actions</span></span>
<span data-ttu-id="37f10-111">Hello **действия** свойства пользовательской роли указывает hello Azure операций toowhich hello роль предоставляет доступ.</span><span class="sxs-lookup"><span data-stu-id="37f10-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="37f10-112">Это коллекция строк операций, которые определяют защищенные действия поставщиков ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="37f10-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="37f10-113">Формат hello выполните операцию строки `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="37f10-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="37f10-114">Операции строк, которые содержат подстановочные знаки (\*) предоставить доступ tooall операций, которые сопоставляют строку hello операции.</span><span class="sxs-lookup"><span data-stu-id="37f10-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="37f10-115">например</span><span class="sxs-lookup"><span data-stu-id="37f10-115">For instance:</span></span>

* <span data-ttu-id="37f10-116">`*/read`предоставляет доступ к tooread операции для всех типов ресурсов для всех поставщиков ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="37f10-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="37f10-117">`Microsoft.Compute/*`предоставляет доступ к tooall операции для всех типов ресурсов в поставщике ресурсов Microsoft.Compute hello.</span><span class="sxs-lookup"><span data-stu-id="37f10-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="37f10-118">`Microsoft.Network/*/read`предоставляет доступ к tooread операции для всех типов ресурсов в поставщике ресурсов Microsoft.Network hello Azure.</span><span class="sxs-lookup"><span data-stu-id="37f10-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="37f10-119">`Microsoft.Compute/virtualMachines/*`предоставляет доступ к операции tooall виртуальных машин и его дочерние типы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="37f10-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="37f10-120">`Microsoft.Web/sites/restart/Action`предоставляет доступ к toorestart веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="37f10-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="37f10-121">Используйте `Get-AzureRmProviderOperation` (в PowerShell) или `azure provider operations show` (в Azure CLI) toolist операций поставщиков ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="37f10-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="37f10-122">Можно также использовать эти tooverify команд, что операция строка является допустимой и строки операции tooexpand подстановочный знак.</span><span class="sxs-lookup"><span data-stu-id="37f10-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Снимок экрана PowerShell: Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="37f10-124">Снимок экрана Azure CLI: azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="37f10-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="37f10-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="37f10-125">NotActions</span></span>
<span data-ttu-id="37f10-126">Используйте hello **NotActions** свойства, если набор операций, что вы хотите tooallow hello проще определить, исключив ограниченные операции.</span><span class="sxs-lookup"><span data-stu-id="37f10-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="37f10-127">Hello доступа, предоставляемого пользовательской роли вычисляется путем вычитания hello **NotActions** операций из hello **действия** операций.</span><span class="sxs-lookup"><span data-stu-id="37f10-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="37f10-128">Если пользователю назначена роль, исключающей операции в **NotActions**и назначается как вторая роль, предоставляющую доступ toohello же операция, пользователь hello допускается tooperform этой операции.</span><span class="sxs-lookup"><span data-stu-id="37f10-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="37f10-129">**NotActions** не deny правила — это просто toocreate удобный способ набор разрешенных операций при определенных операций требуется toobe исключен.</span><span class="sxs-lookup"><span data-stu-id="37f10-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="37f10-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="37f10-130">AssignableScopes</span></span>
<span data-ttu-id="37f10-131">Hello **AssignableScopes** свойства пользовательской роли hello указывает области hello (подписки, группы ресурсов или ресурсов), в течение которого hello пользовательской роли доступна для назначения.</span><span class="sxs-lookup"><span data-stu-id="37f10-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="37f10-132">Hello пользовательской роли можно сделать доступными для назначения в hello подписки или групп ресурсов, которые требуют, а не пользователя помехи взаимодействия для оставшихся hello hello подписок или групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="37f10-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="37f10-133">Примеры допустимых назначаемых областей:</span><span class="sxs-lookup"><span data-stu-id="37f10-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="37f10-134">«/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e», «/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624» - делает доступными для назначения роли hello в две подписки.</span><span class="sxs-lookup"><span data-stu-id="37f10-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="37f10-135">«/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e» - делает доступными для назначения роли hello в одной подписке.</span><span class="sxs-lookup"><span data-stu-id="37f10-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="37f10-136">«/ подписок или c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups сеть» - делает hello роли, назначаемые только в группе ресурсов сети hello.</span><span class="sxs-lookup"><span data-stu-id="37f10-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="37f10-137">Необходимо использовать по крайней мере одну подписку, группу ресурсов или идентификатор ресурса.</span><span class="sxs-lookup"><span data-stu-id="37f10-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="37f10-138">Контроль доступа к пользовательским ролям</span><span class="sxs-lookup"><span data-stu-id="37f10-138">Custom roles access control</span></span>
<span data-ttu-id="37f10-139">Hello **AssignableScopes** свойства пользовательской роли hello также управляет, кто может просматривать, изменения и удаления роли hello.</span><span class="sxs-lookup"><span data-stu-id="37f10-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="37f10-140">Кто может создавать пользовательские роли?</span><span class="sxs-lookup"><span data-stu-id="37f10-140">Who can create a custom role?</span></span>
    <span data-ttu-id="37f10-141">Создавать пользовательские роли для использования в подписках, группах ресурсов и отдельных ресурсах могут владельцы (и администраторы доступа пользователей) этих областей.</span><span class="sxs-lookup"><span data-stu-id="37f10-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="37f10-142">Hello Создание роли hello пользователю возможности tooperform toobe `Microsoft.Authorization/roleDefinition/write` операцию для всех hello **AssignableScopes** hello роли.</span><span class="sxs-lookup"><span data-stu-id="37f10-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="37f10-143">Кто может изменять пользовательские роли?</span><span class="sxs-lookup"><span data-stu-id="37f10-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="37f10-144">Изменять пользовательские роли для использования в подписках, группах ресурсов и отдельных ресурсах могут владельцы (и администраторы доступа пользователей) этих областей.</span><span class="sxs-lookup"><span data-stu-id="37f10-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="37f10-145">Пользователи должны hello может tooperform toobe `Microsoft.Authorization/roleDefinition/write` операцию для всех hello **AssignableScopes** пользовательские роли.</span><span class="sxs-lookup"><span data-stu-id="37f10-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="37f10-146">Кто может просматривать пользовательские роли?</span><span class="sxs-lookup"><span data-stu-id="37f10-146">Who can view custom roles?</span></span>
    <span data-ttu-id="37f10-147">Все стандартные роли Azure RBAC позволяют просматривать список ролей, доступных для назначения.</span><span class="sxs-lookup"><span data-stu-id="37f10-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="37f10-148">Пользователи, которые можно выполнять hello `Microsoft.Authorization/roleDefinition/read` операции на уровне области можно просмотреть hello RBAC ролей, доступных для назначения в этой области.</span><span class="sxs-lookup"><span data-stu-id="37f10-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="37f10-149">См. также</span><span class="sxs-lookup"><span data-stu-id="37f10-149">See also</span></span>
* <span data-ttu-id="37f10-150">[Управление доступом на основе ролей](role-based-access-control-configure.md): Приступая к работе с RBAC в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="37f10-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="37f10-151">Узнайте, как доступ к toomanage с:</span><span class="sxs-lookup"><span data-stu-id="37f10-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="37f10-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37f10-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="37f10-153">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="37f10-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="37f10-154">REST API</span><span class="sxs-lookup"><span data-stu-id="37f10-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="37f10-155">[Встроенные роли](role-based-access-built-in-roles.md): получение сведений о ролях hello, которые поставляются в RBAC.</span><span class="sxs-lookup"><span data-stu-id="37f10-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
