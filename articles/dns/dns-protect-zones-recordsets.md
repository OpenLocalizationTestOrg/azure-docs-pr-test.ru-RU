---
title: "Защита зон и записей DNS | Документация Майкрософт"
description: "Как защитить зоны и наборы записей DNS в службе DNS Microsoft Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 0b7040d6273b3a6b85cd55850d596807226b87fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="30925-103">Как защитить зоны и записи DNS</span><span class="sxs-lookup"><span data-stu-id="30925-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="30925-104">Зоны и записи DNS являются критически важными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="30925-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="30925-105">Удаление зоны DNS или даже одной записи DNS может привести к полному отключению службы.</span><span class="sxs-lookup"><span data-stu-id="30925-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="30925-106">Поэтому важно, чтобы критически важные зоны и записи DNS были защищены от несанкционированных или случайных изменений.</span><span class="sxs-lookup"><span data-stu-id="30925-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="30925-107">В этой статье объясняется, как с помощью службы DNS Azure защитить зоны и записи DNS от таких изменений.</span><span class="sxs-lookup"><span data-stu-id="30925-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="30925-108">Мы применяем две эффективные функции безопасности, предоставляемые Azure Resource Manager: [управление доступом на основе ролей](../active-directory/role-based-access-control-what-is.md) и [блокировки ресурсов](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="30925-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="30925-109">Контроль доступа на основе ролей</span><span class="sxs-lookup"><span data-stu-id="30925-109">Role-based access control</span></span>

<span data-ttu-id="30925-110">Управление доступом на основе ролей (RBAC) Azure обеспечивает точное управление доступом для пользователей, групп и ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="30925-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="30925-111">С помощью RBAC вы можете с высокой точностью предоставлять пользователям доступ, необходимый для выполнения поставленных перед ними задач.</span><span class="sxs-lookup"><span data-stu-id="30925-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="30925-112">Дополнительные сведения о том, как RBAC помогает управлять доступом, см. в статье [Начало работы с управлением доступом на портале Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="30925-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="30925-113">Роль DNS Zone Contributor (Участник зоны DNS)</span><span class="sxs-lookup"><span data-stu-id="30925-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="30925-114">DNS Zone Contributor (Участник зоны DNS) — это встроенная роль, предоставляемая Azure для управления ресурсами DNS.</span><span class="sxs-lookup"><span data-stu-id="30925-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="30925-115">Назначение пользователю или группе разрешений участника зоны DNS дает возможность этой группе управлять ресурсами DNS, но не позволяет управлять ресурсами других типов.</span><span class="sxs-lookup"><span data-stu-id="30925-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="30925-116">Предположим, например, что группа ресурсов myzones содержит пять зон для Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="30925-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="30925-117">Если предоставить администратору DNS разрешения DNS Zone Contributor (Участник зоны DNS) для этой группы ресурсов, то он получит полный контроль над этими зонами DNS.</span><span class="sxs-lookup"><span data-stu-id="30925-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="30925-118">Это также позволяет избежать предоставления ненужных разрешений. Например, администратор DNS не сможет создавать или останавливать виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="30925-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="30925-119">Самый простой способ назначения разрешений RBAC — [через портал Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="30925-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="30925-120">Откройте колонку "Управление доступом (IAM)" для группы ресурсов, затем нажмите кнопку "Добавить", выберите роль DNS Zone Contributor (Участник зоны DNS) и выберите пользователей или группы, которым будут предоставлены разрешения.</span><span class="sxs-lookup"><span data-stu-id="30925-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Назначение разрешений RBAC на уровне группы ресурсов через портал Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="30925-122">Разрешения также можно [предоставить с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="30925-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="30925-123">Аналогичную команду также [можно выполнить через интерфейс командной строки Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="30925-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="30925-124">RBAC на уровне зоны</span><span class="sxs-lookup"><span data-stu-id="30925-124">Zone level RBAC</span></span>

<span data-ttu-id="30925-125">Правила RBAC Azure могут применяться к подписке, группе ресурсов или к отдельному ресурсу.</span><span class="sxs-lookup"><span data-stu-id="30925-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="30925-126">В случае службы DNS Azure таким ресурсом может быть отдельная зона DNS или даже отдельный набор записей.</span><span class="sxs-lookup"><span data-stu-id="30925-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="30925-127">Предположим, например, что группа ресурсов myzones содержит зону contoso.com и подзону customers.contoso.com, в которой для каждой учетной записи клиента созданы записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="30925-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="30925-128">Учетной записи, используемой для управления этими записями CNAME, необходимо назначить разрешения на создание записей только в зоне customers.contoso.com. Она не должна иметь доступ к другим зонам.</span><span class="sxs-lookup"><span data-stu-id="30925-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="30925-129">Разрешения RBAC на уровне зоны можно предоставлять через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30925-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="30925-130">Откройте колонку "Управление доступом (IAM)" для зоны, затем нажмите кнопку "Добавить", выберите роль DNS Zone Contributor (Участник зоны DNS) и выберите пользователей или группы, которым будут предоставлены разрешения.</span><span class="sxs-lookup"><span data-stu-id="30925-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Назначение разрешений RBAC на уровне зоны DNS через портал Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="30925-132">Разрешения также можно [предоставить с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="30925-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="30925-133">Аналогичную команду также [можно выполнить через интерфейс командной строки Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="30925-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="30925-134">RBAC на уровне набора записей</span><span class="sxs-lookup"><span data-stu-id="30925-134">Record set level RBAC</span></span>

<span data-ttu-id="30925-135">Мы можем пойти еще дальше.</span><span class="sxs-lookup"><span data-stu-id="30925-135">We can go one step further.</span></span> <span data-ttu-id="30925-136">Давайте рассмотрим пример с администратором почтового сервера в Contoso Corporation, которому требуется доступ к записям MX и TXT на вершине зоны contoso.com.</span><span class="sxs-lookup"><span data-stu-id="30925-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="30925-137">Ему не нужен доступ к другим записям MX и TXT или к записям любого другого типа.</span><span class="sxs-lookup"><span data-stu-id="30925-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="30925-138">Служба DNS Azure позволяет назначить разрешения на уровне набора записей, именно к тем записям, к которым администратору почтового сервера требуется доступ.</span><span class="sxs-lookup"><span data-stu-id="30925-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="30925-139">Администратор почтового сервера получает именно тот уровень контроля, который ему необходим, и не может вносить другие изменения.</span><span class="sxs-lookup"><span data-stu-id="30925-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="30925-140">Разрешения RBAC на уровне набора записей можно настроить через портал Azure (с помощью кнопки "Пользователи" в колонке набора записей):</span><span class="sxs-lookup"><span data-stu-id="30925-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![Назначение разрешений RBAC на уровне набора записей через портал Azure](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="30925-142">Разрешения RBAC на уровне набора записей также можно [предоставить с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="30925-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="30925-143">Аналогичную команду также [можно выполнить через интерфейс командной строки Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="30925-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="30925-144">Пользовательские роли</span><span class="sxs-lookup"><span data-stu-id="30925-144">Custom roles</span></span>

<span data-ttu-id="30925-145">Встроенная роль DNS Zone Contributor (Участник зоны DNS) обеспечивает полный контроль над ресурсом DNS.</span><span class="sxs-lookup"><span data-stu-id="30925-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="30925-146">Можно также создавать собственные пользовательские роли Azure, чтобы обеспечить более детализированный контроль.</span><span class="sxs-lookup"><span data-stu-id="30925-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="30925-147">Давайте снова рассмотрим пример, где в зоне customers.contoso.com для каждой учетной записи клиента Contoso Corporation создана запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="30925-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="30925-148">Учетной записи, используемой для управления этими записями CNAME, необходимо предоставить разрешение на управление только записями CNAME.</span><span class="sxs-lookup"><span data-stu-id="30925-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="30925-149">В этом случае она не сможет изменять записи других типов (такие как записи MX) или выполнять операции на уровне зоны, такие как удаление зоны.</span><span class="sxs-lookup"><span data-stu-id="30925-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="30925-150">В следующем примере показано определение пользовательской роли для управления только записями CNAME:</span><span class="sxs-lookup"><span data-stu-id="30925-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

<span data-ttu-id="30925-151">Свойство Actions определяет следующие разрешения для DNS:</span><span class="sxs-lookup"><span data-stu-id="30925-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="30925-152">`Microsoft.Network/dnsZones/CNAME/*` предоставляет полный контроль над записями CNAME.</span><span class="sxs-lookup"><span data-stu-id="30925-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="30925-153">`Microsoft.Network/dnsZones/read` предоставляет разрешение на чтение зон DNS, но не позволяет их изменять. Таким образом вы можете видеть зону, в которой создается запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="30925-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="30925-154">Остальные элементы свойства Actions копируются из [встроенной роли участника зоны DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="30925-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="30925-155">Применение пользовательской роли RBAC для предотвращения удаления наборов записей, разрешая при этом их обновление, не является эффективным.</span><span class="sxs-lookup"><span data-stu-id="30925-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="30925-156">Наборы записей нельзя удалить, но ничто не препятствует их изменению.</span><span class="sxs-lookup"><span data-stu-id="30925-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="30925-157">К разрешенным изменениям относятся добавление и удаление записей из набора записей, включая удаление всех записей (при этом остается "пустой" набор записей).</span><span class="sxs-lookup"><span data-stu-id="30925-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="30925-158">Это действует так же, как удаление набора записей с точки зрения разрешения DNS.</span><span class="sxs-lookup"><span data-stu-id="30925-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="30925-159">В настоящее время определения пользовательских ролей не определяются через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30925-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="30925-160">Пользовательскую роль на основе этого определения роли можно создать с помощью Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="30925-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="30925-161">Ее также можно создать с помощью интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="30925-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="30925-162">Затем роль можно назначить таким же образом, как и встроенные роли. Этот процесс описан ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="30925-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="30925-163">Дополнительные сведения о создании и назначении пользовательских ролей, а также об управлении ими см. в статье [Пользовательские роли в Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="30925-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="30925-164">Блокировки ресурсов</span><span class="sxs-lookup"><span data-stu-id="30925-164">Resource locks</span></span>

<span data-ttu-id="30925-165">Помимо функции RBAC Azure Resource Manager поддерживает и другой тип защиты — возможность "блокировать" ресурсы.</span><span class="sxs-lookup"><span data-stu-id="30925-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="30925-166">Если правила RBAC позволяют контролировать действия определенных пользователей и групп, то блокировки ресурсов применяются к конкретному ресурсу и действуют для всех пользователей и ролей.</span><span class="sxs-lookup"><span data-stu-id="30925-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="30925-167">Дополнительные сведения см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="30925-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="30925-168">Существует два типа блокировки ресурсов: **DoNotDelete** и **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="30925-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="30925-169">Они могут применяться к зоне DNS или к отдельному набору записей.</span><span class="sxs-lookup"><span data-stu-id="30925-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="30925-170">Следующие разделы описывают несколько распространенных сценариев и способы их поддержки с помощью блокировок ресурсов.</span><span class="sxs-lookup"><span data-stu-id="30925-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="30925-171">Защита от любых изменений</span><span class="sxs-lookup"><span data-stu-id="30925-171">Protecting against all changes</span></span>

<span data-ttu-id="30925-172">Чтобы предотвратить внесение каких-либо изменений, примените к зоне блокировку ReadOnly.</span><span class="sxs-lookup"><span data-stu-id="30925-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="30925-173">Эта блокировка не позволит создавать наборы записей, а также изменять или удалять существующие наборы.</span><span class="sxs-lookup"><span data-stu-id="30925-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="30925-174">Блокировки ресурсов на уровне зоны можно создавать через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30925-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="30925-175">В колонке "Зона DNS" выберите "Блокировки", а затем нажмите кнопку "Добавить":</span><span class="sxs-lookup"><span data-stu-id="30925-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![Блокировка ресурсов на уровне зоны через портал Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="30925-177">Блокировки ресурсов на уровне зоны также можно создать с помощью Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="30925-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="30925-178">В настоящее время настройка блокировки ресурсов Azure с помощью интерфейса командной строки Azure не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="30925-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="30925-179">Защита отдельных записей</span><span class="sxs-lookup"><span data-stu-id="30925-179">Protecting individual records</span></span>

<span data-ttu-id="30925-180">Чтобы предотвратить внесение изменений в существующий набор записей DNS, примените к нему блокировку ReadOnly.</span><span class="sxs-lookup"><span data-stu-id="30925-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="30925-181">Применение к набору записей блокировки DoNotDelete не является эффективным.</span><span class="sxs-lookup"><span data-stu-id="30925-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="30925-182">Набор записей нельзя удалить, но ничто не препятствует его изменению.</span><span class="sxs-lookup"><span data-stu-id="30925-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="30925-183">К разрешенным изменениям относятся добавление и удаление записей из набора записей, включая удаление всех записей (при этом остается "пустой" набор записей).</span><span class="sxs-lookup"><span data-stu-id="30925-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="30925-184">Это действует так же, как удаление набора записей с точки зрения разрешения DNS.</span><span class="sxs-lookup"><span data-stu-id="30925-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="30925-185">В настоящее время блокировки ресурсов на уровне наборов записей можно настраивать только с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30925-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="30925-186">Эта возможность пока не предоставляется через портал Azure или интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="30925-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="30925-187">Защита зоны от удаления</span><span class="sxs-lookup"><span data-stu-id="30925-187">Protecting against zone deletion</span></span>

<span data-ttu-id="30925-188">При удалении зоны в службе DNS Azure все наборы записей в этой зоне также удаляются.</span><span class="sxs-lookup"><span data-stu-id="30925-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="30925-189">Эту операцию нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="30925-189">This operation cannot be undone.</span></span>  <span data-ttu-id="30925-190">Случайное удаление критически важной зоны может оказать серьезное влияние на коммерческую деятельность.</span><span class="sxs-lookup"><span data-stu-id="30925-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="30925-191">Поэтому очень важно защитить зоны от случайного удаления.</span><span class="sxs-lookup"><span data-stu-id="30925-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="30925-192">Применение к зоне блокировки DoNotDelete предотвратит ее удаление.</span><span class="sxs-lookup"><span data-stu-id="30925-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="30925-193">Однако, поскольку блокировки наследуются дочерними ресурсами, это действие также предотвращает удаление всех наборов записей, находящихся в этой зоне, что может быть нежелательно.</span><span class="sxs-lookup"><span data-stu-id="30925-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="30925-194">Более того, как уже говорилось ранее в примечании, это неэффективно, так как записи по-прежнему могут удаляться из существующих наборов записей.</span><span class="sxs-lookup"><span data-stu-id="30925-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="30925-195">Альтернативным решением может быть применение блокировки DoNotDelete к набору записей в зоне, такому как набор записей типа SOA.</span><span class="sxs-lookup"><span data-stu-id="30925-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="30925-196">Так как зону нельзя удалить, не удалив также наборы записей, это обеспечивает защиту зоны от удаления, при этом наборы записей в зоне по-прежнему можно свободно изменять.</span><span class="sxs-lookup"><span data-stu-id="30925-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="30925-197">При попытке удалить зону Azure Resource Manager определяет, что это действие также удалит набор записей типа SOA, и блокирует вызов, так как набор SOA заблокирован.</span><span class="sxs-lookup"><span data-stu-id="30925-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="30925-198">Наборы записей не будут удалены.</span><span class="sxs-lookup"><span data-stu-id="30925-198">No record sets are deleted.</span></span>

<span data-ttu-id="30925-199">Следующая команда PowerShell создает блокировку DoNotDelete для записи типа SOA в заданной зоне:</span><span class="sxs-lookup"><span data-stu-id="30925-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="30925-200">Другой способ предотвратить случайное удаление зоны — настроить пользовательскую роль, благодаря чему в учетных записях оператора и службы, используемых для управления зонами, не будет разрешений на удаление зоны.</span><span class="sxs-lookup"><span data-stu-id="30925-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="30925-201">Если вам понадобится удалить зону, можно применить двухэтапное удаление. Сначала нужно предоставить разрешения на удаление зоны (в области зоны, чтобы предотвратить удаление не той зоны), после чего ее можно будет удалить.</span><span class="sxs-lookup"><span data-stu-id="30925-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="30925-202">Преимущество этого подхода заключается в том, что он работает для всех зон, к которым у этих учетных записей есть доступ, и при этом не нужно создавать блокировки.</span><span class="sxs-lookup"><span data-stu-id="30925-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="30925-203">Но у него также есть недостаток, заключающийся в том, что пользователи учетных записей с разрешениями на удаление зоны, например владелец подписки, по-прежнему могут случайно удалить критическую зону.</span><span class="sxs-lookup"><span data-stu-id="30925-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="30925-204">Оба подхода — блокировки ресурсов и пользовательские роли — можно использовать одновременно в качестве эшелонированного подхода к защите зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="30925-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30925-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30925-205">Next steps</span></span>

* <span data-ttu-id="30925-206">Дополнительные сведения о работе с RBAC см. в статье [Начало работы с управлением доступом на портале Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="30925-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="30925-207">Дополнительные сведения о работе с блокировками ресурсов см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="30925-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

