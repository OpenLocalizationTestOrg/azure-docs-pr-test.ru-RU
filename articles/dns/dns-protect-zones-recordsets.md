---
title: "aaaProtecting зоны и записи DNS | Документы Microsoft"
description: "Как tooprotect зон DNS и запись задает в Microsoft Azure DNS."
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
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="e00c4-103">Как tooprotect DNS-зоны и записи</span><span class="sxs-lookup"><span data-stu-id="e00c4-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="e00c4-104">Зоны и записи DNS являются критически важными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="e00c4-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="e00c4-105">Удаление зоны DNS или даже одной записи DNS может привести к полному отключению службы.</span><span class="sxs-lookup"><span data-stu-id="e00c4-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="e00c4-106">Поэтому важно, чтобы критически важные зоны и записи DNS были защищены от несанкционированных или случайных изменений.</span><span class="sxs-lookup"><span data-stu-id="e00c4-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="e00c4-107">В этой статье объясняется, как Azure DNS позволяет вам tooprotect зон DNS и записи для таких изменений.</span><span class="sxs-lookup"><span data-stu-id="e00c4-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="e00c4-108">Мы применяем две эффективные функции безопасности, предоставляемые Azure Resource Manager: [управление доступом на основе ролей](../active-directory/role-based-access-control-what-is.md) и [блокировки ресурсов](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e00c4-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="e00c4-109">Контроль доступа на основе ролей</span><span class="sxs-lookup"><span data-stu-id="e00c4-109">Role-based access control</span></span>

<span data-ttu-id="e00c4-110">Управление доступом на основе ролей (RBAC) Azure обеспечивает точное управление доступом для пользователей, групп и ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e00c4-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="e00c4-111">С помощью RBAC, можно предоставить точно hello уровень доступа, пользователи должны tooperform свою работу.</span><span class="sxs-lookup"><span data-stu-id="e00c4-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="e00c4-112">Дополнительные сведения о том, как RBAC помогает управлять доступом, см. в статье [Начало работы с управлением доступом на портале Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="e00c4-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="e00c4-113">роль «Участника зоны DNS» Hello</span><span class="sxs-lookup"><span data-stu-id="e00c4-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="e00c4-114">роль «Участника зоны DNS» Hello — это встроенная роль, предоставляемые Azure для управления ресурсами DNS.</span><span class="sxs-lookup"><span data-stu-id="e00c4-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="e00c4-115">Назначение пользователя tooa разрешения участника зоны DNS или группы обеспечивает этой группы toomanage DNS ресурсы, но не к ресурсам любого другого типа.</span><span class="sxs-lookup"><span data-stu-id="e00c4-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="e00c4-116">Например предположим, что группа ресурсов hello «myzones» содержит пять зон для Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="e00c4-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="e00c4-117">Предоставление hello DNS администратора «Участник зоны DNS» разрешения toothat группы ресурсов, позволяет полный контроль над этих зон DNS.</span><span class="sxs-lookup"><span data-stu-id="e00c4-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="e00c4-118">Это также устраняет необходимость предоставлять ненужные разрешения, например Здравствуйте, администратор DNS не удается создать или остановка виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e00c4-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="e00c4-119">Hello простейший способ разрешения RBAC, tooassign [через портал Azure hello](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e00c4-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="e00c4-120">Открыть колонку hello «управление доступом (IAM)» для группы ресурсов hello, а затем нажмите кнопку «Добавить», а затем выберите роль «Участника зоны DNS» hello и выберите hello необходимых пользователей или групп toogrant разрешения.</span><span class="sxs-lookup"><span data-stu-id="e00c4-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Уровень группы ресурсов RBAC через портал Azure hello](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="e00c4-122">Разрешения также можно [предоставить с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="e00c4-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="e00c4-123">также является Hello эквивалентную команду [доступны через hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="e00c4-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="e00c4-124">RBAC на уровне зоны</span><span class="sxs-lookup"><span data-stu-id="e00c4-124">Zone level RBAC</span></span>

<span data-ttu-id="e00c4-125">Правила RBAC Azure может быть применен tooa подписки, ресурс группы или tooan отдельных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e00c4-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="e00c4-126">В случае hello Azure DNS этот ресурс может быть отдельные зоны DNS, или даже набор отдельных записей.</span><span class="sxs-lookup"><span data-stu-id="e00c4-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="e00c4-127">Например предположим, что группа ресурсов hello «myzones» содержит зоны hello «contoso.com» и subzone «customers.contoso.com» создания записи CNAME для каждой учетной записи клиента.</span><span class="sxs-lookup"><span data-stu-id="e00c4-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="e00c4-128">toomanage учетная запись, используемая Hello эти записи CNAME должны назначаться разрешения записи toocreate hello «customers.contoso.com» только в зоне, он не должен иметь toohello доступ других зон.</span><span class="sxs-lookup"><span data-stu-id="e00c4-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="e00c4-129">Разрешения РОЛЕЙ уровня зоны могут предоставляться через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e00c4-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="e00c4-130">Открыть колонку «Управление доступом (IAM)» hello hello зоны, затем нажмите кнопку «Добавить», а затем выберите роль «Участника зоны DNS» hello и выберите hello необходимых пользователей или групп toogrant разрешения.</span><span class="sxs-lookup"><span data-stu-id="e00c4-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Зона DNS уровня RBAC через портал Azure hello](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="e00c4-132">Разрешения также можно [предоставить с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="e00c4-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="e00c4-133">также является Hello эквивалентную команду [доступны через hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="e00c4-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="e00c4-134">RBAC на уровне набора записей</span><span class="sxs-lookup"><span data-stu-id="e00c4-134">Record set level RBAC</span></span>

<span data-ttu-id="e00c4-135">Мы можем пойти еще дальше.</span><span class="sxs-lookup"><span data-stu-id="e00c4-135">We can go one step further.</span></span> <span data-ttu-id="e00c4-136">Рассмотрите возможность hello администратору почтового сервера для Contoso Corporation, которым необходим доступ toohello MX и записи TXT на вершине зоны «contoso.com» hello hello.</span><span class="sxs-lookup"><span data-stu-id="e00c4-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="e00c4-137">Она не требуется доступ к tooany других записей MX или TXT или записи tooany любого другого типа.</span><span class="sxs-lookup"><span data-stu-id="e00c4-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="e00c4-138">Azure DNS позволяет вам tooassign разрешения в hello набора записей уровня, tooprecisely hello записей, которые Здравствуйте, администратор почты требуется доступ к.</span><span class="sxs-lookup"><span data-stu-id="e00c4-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="e00c4-139">Hello почты администратору предоставляется точно контролировать hello ей нужны и будет невозможно toomake любые другие изменения.</span><span class="sxs-lookup"><span data-stu-id="e00c4-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="e00c4-140">Разрешения на уровне RBAC набор записей можно настроить с помощью hello портал Azure, с помощью кнопки hello «пользователи» в колонке hello набор записей:</span><span class="sxs-lookup"><span data-stu-id="e00c4-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![Набор записей уровне RBAC через портал Azure hello](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="e00c4-142">Разрешения RBAC на уровне набора записей также можно [предоставить с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="e00c4-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="e00c4-143">также является Hello эквивалентную команду [доступны через hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="e00c4-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="e00c4-144">Пользовательские роли</span><span class="sxs-lookup"><span data-stu-id="e00c4-144">Custom roles</span></span>

<span data-ttu-id="e00c4-145">Встроенная роль «Участник зоны DNS» Hello обеспечивает полный контроль над ресурсов DNS.</span><span class="sxs-lookup"><span data-stu-id="e00c4-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="e00c4-146">Он является также возможно toobuild собственного клиента Azure роли, tooprovide даже детальный контроль.</span><span class="sxs-lookup"><span data-stu-id="e00c4-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="e00c4-147">Снова рассмотрим пример hello, в котором создается запись CNAME в зоне hello «customers.contoso.com» для каждой учетной записи клиента Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="e00c4-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="e00c4-148">Учетная запись, используемая toomanage Hello этих записей CNAME должны предоставляться записи CNAME toomanage разрешение только.</span><span class="sxs-lookup"><span data-stu-id="e00c4-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="e00c4-149">Это то записи не удается toomodify других типов (например, изменение записи MX) или уровня зоны операций, таких как удаление зоны.</span><span class="sxs-lookup"><span data-stu-id="e00c4-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="e00c4-150">Hello в следующем примере показано определение пользовательской роли для управления только для записей CNAME.</span><span class="sxs-lookup"><span data-stu-id="e00c4-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="e00c4-151">Свойства действия Hello определяет hello после разрешения DNS:</span><span class="sxs-lookup"><span data-stu-id="e00c4-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="e00c4-152">`Microsoft.Network/dnsZones/CNAME/*` предоставляет полный контроль над записями CNAME.</span><span class="sxs-lookup"><span data-stu-id="e00c4-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="e00c4-153">`Microsoft.Network/dnsZones/read`предоставляет разрешение tooread DNS-зон, но не toomodify их включение вы toosee hello зону, в которой hello создается запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="e00c4-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="e00c4-154">Привет, оставшиеся действия копируются из hello [встроенная роль участника зоны DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="e00c4-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="e00c4-155">Использование пользовательских tooprevent роли RBAC, удаление записи наборов, хотя по-прежнему обеспечивая toobe обновления не эффективный контроль.</span><span class="sxs-lookup"><span data-stu-id="e00c4-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="e00c4-156">Наборы записей нельзя удалить, но ничто не препятствует их изменению.</span><span class="sxs-lookup"><span data-stu-id="e00c4-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="e00c4-157">Разрешенные изменения включают добавление и удаление записей из набора записей hello, включая удаление всех записей tooleave «пустой» набор записей.</span><span class="sxs-lookup"><span data-stu-id="e00c4-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="e00c4-158">У него есть hello же эффект, что удаление записи hello набор с точки зрения разрешение DNS.</span><span class="sxs-lookup"><span data-stu-id="e00c4-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="e00c4-159">В настоящее время невозможно определить пользовательские определения роли через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e00c4-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="e00c4-160">Пользовательскую роль на основе этого определения роли можно создать с помощью Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e00c4-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="e00c4-161">Он также могут создаваться через hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="e00c4-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="e00c4-162">Hello роли могут быть предоставлены в hello таким же образом как встроенные роли, как описано ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e00c4-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="e00c4-163">Дополнительные сведения о том, как toocreate, управление и назначить пользовательских ролей в разделе [настраиваемые роли в Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e00c4-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="e00c4-164">Блокировки ресурсов</span><span class="sxs-lookup"><span data-stu-id="e00c4-164">Resource locks</span></span>

<span data-ttu-id="e00c4-165">В tooRBAC Добавление диспетчера ресурсов Azure поддерживает контроль безопасности, а именно: hello too'lock возможность другого типа "ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e00c4-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="e00c4-166">Где RBAC правила разрешают передачу toocontrol hello действия конкретных пользователей и групп, блокировки ресурсов, примененные toohello ресурсов и вступают в силу для всех пользователей и ролей.</span><span class="sxs-lookup"><span data-stu-id="e00c4-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="e00c4-167">Дополнительные сведения см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e00c4-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="e00c4-168">Существует два типа блокировки ресурсов: **DoNotDelete** и **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="e00c4-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="e00c4-169">Они могут применяться tooa зоны DNS или tooan набор отдельных записей.</span><span class="sxs-lookup"><span data-stu-id="e00c4-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="e00c4-170">Hello следующих разделах описаны некоторые распространенные сценарии и как toosupport их с помощью блокировки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e00c4-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="e00c4-171">Защита от любых изменений</span><span class="sxs-lookup"><span data-stu-id="e00c4-171">Protecting against all changes</span></span>

<span data-ttu-id="e00c4-172">tooprevent изменения внесенные, применить зоны toohello блокировки только для чтения.</span><span class="sxs-lookup"><span data-stu-id="e00c4-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="e00c4-173">Эта блокировка не позволит создавать наборы записей, а также изменять или удалять существующие наборы.</span><span class="sxs-lookup"><span data-stu-id="e00c4-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="e00c4-174">Блокировки уровня ресурсов зоны могут создаваться через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e00c4-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="e00c4-175">Из колонки зоны DNS hello, нажмите кнопку «Блокировка» нажмите «Добавить»:</span><span class="sxs-lookup"><span data-stu-id="e00c4-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![Блокировки уровня ресурсов зоны через портал Azure hello](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="e00c4-177">Блокировки ресурсов на уровне зоны также можно создать с помощью Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e00c4-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="e00c4-178">Настройка блокировки ресурсов Azure не поддерживается в настоящее время через hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e00c4-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="e00c4-179">Защита отдельных записей</span><span class="sxs-lookup"><span data-stu-id="e00c4-179">Protecting individual records</span></span>

<span data-ttu-id="e00c4-180">tooprevent установить для изменения существующей записи DNS применяются только для чтения блокировки toohello набор записей.</span><span class="sxs-lookup"><span data-stu-id="e00c4-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="e00c4-181">Применение блокировки DoNotDelete tooa набор записей не эффективный контроль.</span><span class="sxs-lookup"><span data-stu-id="e00c4-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="e00c4-182">Он предотвращает набора от удаления записей hello, но она не предотвращает его изменение.</span><span class="sxs-lookup"><span data-stu-id="e00c4-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="e00c4-183">Разрешенные изменения включают добавление и удаление записей из набора записей hello, включая удаление всех записей tooleave «пустой» набор записей.</span><span class="sxs-lookup"><span data-stu-id="e00c4-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="e00c4-184">У него есть hello же эффект, что удаление записи hello набор с точки зрения разрешение DNS.</span><span class="sxs-lookup"><span data-stu-id="e00c4-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="e00c4-185">В настоящее время блокировки ресурсов на уровне наборов записей можно настраивать только с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e00c4-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="e00c4-186">Они не поддерживаются в hello портал Azure или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e00c4-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="e00c4-187">Защита зоны от удаления</span><span class="sxs-lookup"><span data-stu-id="e00c4-187">Protecting against zone deletion</span></span>

<span data-ttu-id="e00c4-188">При удалении зоны Azure DNS, также удаляются все наборы записей в зоне hello.</span><span class="sxs-lookup"><span data-stu-id="e00c4-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="e00c4-189">Эту операцию нельзя отменить.</span><span class="sxs-lookup"><span data-stu-id="e00c4-189">This operation cannot be undone.</span></span>  <span data-ttu-id="e00c4-190">Случайное удаление критическую зону имеет потенциальные toohave hello значительные значимым.</span><span class="sxs-lookup"><span data-stu-id="e00c4-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="e00c4-191">Поэтому это очень важно tooprotect от зоны случайного удаления.</span><span class="sxs-lookup"><span data-stu-id="e00c4-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="e00c4-192">Зоны tooa блокировки DoNotDelete позволяет предотвратить hello зоны от удаления.</span><span class="sxs-lookup"><span data-stu-id="e00c4-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="e00c4-193">Тем не менее поскольку блокировки, наследуются дочерними ресурсами, он также препятствует любой наборов записей в зоне hello от удаления, который может быть нежелательно.</span><span class="sxs-lookup"><span data-stu-id="e00c4-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="e00c4-194">Более того как описано выше примечании hello, также является неэффективным с момента записи по-прежнему могут быть удалены из существующих наборов записей hello.</span><span class="sxs-lookup"><span data-stu-id="e00c4-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="e00c4-195">В качестве альтернативы рассмотрите возможность применения блокировки tooa DoNotDelete запись набора в зоне hello, такие как набор записей SOA hello.</span><span class="sxs-lookup"><span data-stu-id="e00c4-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="e00c4-196">Так как не удается удалить зону hello удаляя hello наборы записей, это обеспечивает защиту от удаления зоны, по-прежнему предоставляя наборами записей в рамках свободно изменить toobe зоны hello.</span><span class="sxs-lookup"><span data-stu-id="e00c4-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="e00c4-197">При попытке toodelete hello зоны, диспетчера ресурсов Azure обнаруживает это также удалит набор записей SOA hello и блоки hello вызовов, поскольку hello SOA заблокирован.</span><span class="sxs-lookup"><span data-stu-id="e00c4-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="e00c4-198">Наборы записей не будут удалены.</span><span class="sxs-lookup"><span data-stu-id="e00c4-198">No record sets are deleted.</span></span>

<span data-ttu-id="e00c4-199">Hello следующую команду PowerShell создает DoNotDelete блокировку для записи SOA hello hello, учитывая зоны:</span><span class="sxs-lookup"><span data-stu-id="e00c4-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="e00c4-200">Другим способом является использование оператора hello tooensure пользовательской роли и службы учетных записей, используемых toomanage зон не имеют зоны tooprevent зоны случайного удаления удаление разрешений.</span><span class="sxs-lookup"><span data-stu-id="e00c4-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="e00c4-201">При необходимости toodelete зону можно принудительно выполнить удаление из двух, первый предоставлении разрешений удаления зоны (в области зоны hello tooprevent удаление hello неправильный зоны) и второй toodelete hello зоны.</span><span class="sxs-lookup"><span data-stu-id="e00c4-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="e00c4-202">Такой подход имеет преимущество hello, его работы для всех зон, использованным этих учетных записей без необходимости tooremember toocreate все блокировки.</span><span class="sxs-lookup"><span data-stu-id="e00c4-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="e00c4-203">Он имеет недостаток hello, что все учетные записи с разрешениями удаления зоны, например hello владелец подписки, может по-прежнему случайно удалить критическую зону.</span><span class="sxs-lookup"><span data-stu-id="e00c4-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="e00c4-204">Это возможно toouse оба подхода — блокировки ресурсов и пользовательские роли — на hello же время, в целях защиты зоны tooDNS подход глубокой обороны.</span><span class="sxs-lookup"><span data-stu-id="e00c4-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e00c4-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e00c4-205">Next steps</span></span>

* <span data-ttu-id="e00c4-206">Дополнительные сведения о работе с RBAC см. в разделе [Приступая к управлению доступом в hello портал Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="e00c4-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="e00c4-207">Дополнительные сведения о работе с блокировками ресурсов см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e00c4-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

