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
# <a name="how-tooprotect-dns-zones-and-records"></a>Как tooprotect DNS-зоны и записи

Зоны и записи DNS являются критически важными ресурсами. Удаление зоны DNS или даже одной записи DNS может привести к полному отключению службы.  Поэтому важно, чтобы критически важные зоны и записи DNS были защищены от несанкционированных или случайных изменений.

В этой статье объясняется, как Azure DNS позволяет вам tooprotect зон DNS и записи для таких изменений.  Мы применяем две эффективные функции безопасности, предоставляемые Azure Resource Manager: [управление доступом на основе ролей](../active-directory/role-based-access-control-what-is.md) и [блокировки ресурсов](../azure-resource-manager/resource-group-lock-resources.md).

## <a name="role-based-access-control"></a>Контроль доступа на основе ролей

Управление доступом на основе ролей (RBAC) Azure обеспечивает точное управление доступом для пользователей, групп и ресурсов Azure. С помощью RBAC, можно предоставить точно hello уровень доступа, пользователи должны tooperform свою работу. Дополнительные сведения о том, как RBAC помогает управлять доступом, см. в статье [Начало работы с управлением доступом на портале Azure](../active-directory/role-based-access-control-what-is.md).

### <a name="hello-dns-zone-contributor-role"></a>роль «Участника зоны DNS» Hello

роль «Участника зоны DNS» Hello — это встроенная роль, предоставляемые Azure для управления ресурсами DNS.  Назначение пользователя tooa разрешения участника зоны DNS или группы обеспечивает этой группы toomanage DNS ресурсы, но не к ресурсам любого другого типа.

Например предположим, что группа ресурсов hello «myzones» содержит пять зон для Contoso Corporation. Предоставление hello DNS администратора «Участник зоны DNS» разрешения toothat группы ресурсов, позволяет полный контроль над этих зон DNS. Это также устраняет необходимость предоставлять ненужные разрешения, например Здравствуйте, администратор DNS не удается создать или остановка виртуальных машин.

Hello простейший способ разрешения RBAC, tooassign [через портал Azure hello](../active-directory/role-based-access-control-configure.md).  Открыть колонку hello «управление доступом (IAM)» для группы ресурсов hello, а затем нажмите кнопку «Добавить», а затем выберите роль «Участника зоны DNS» hello и выберите hello необходимых пользователей или групп toogrant разрешения.

![Уровень группы ресурсов RBAC через портал Azure hello](./media/dns-protect-zones-recordsets/rbac1.png)

Разрешения также можно [предоставить с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

также является Hello эквивалентную команду [доступны через hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>RBAC на уровне зоны

Правила RBAC Azure может быть применен tooa подписки, ресурс группы или tooan отдельных ресурсов. В случае hello Azure DNS этот ресурс может быть отдельные зоны DNS, или даже набор отдельных записей.

Например предположим, что группа ресурсов hello «myzones» содержит зоны hello «contoso.com» и subzone «customers.contoso.com» создания записи CNAME для каждой учетной записи клиента.  toomanage учетная запись, используемая Hello эти записи CNAME должны назначаться разрешения записи toocreate hello «customers.contoso.com» только в зоне, он не должен иметь toohello доступ других зон.

Разрешения РОЛЕЙ уровня зоны могут предоставляться через портал Azure hello.  Открыть колонку «Управление доступом (IAM)» hello hello зоны, затем нажмите кнопку «Добавить», а затем выберите роль «Участника зоны DNS» hello и выберите hello необходимых пользователей или групп toogrant разрешения.

![Зона DNS уровня RBAC через портал Azure hello](./media/dns-protect-zones-recordsets/rbac2.png)

Разрешения также можно [предоставить с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

также является Hello эквивалентную команду [доступны через hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>RBAC на уровне набора записей

Мы можем пойти еще дальше. Рассмотрите возможность hello администратору почтового сервера для Contoso Corporation, которым необходим доступ toohello MX и записи TXT на вершине зоны «contoso.com» hello hello.  Она не требуется доступ к tooany других записей MX или TXT или записи tooany любого другого типа.  Azure DNS позволяет вам tooassign разрешения в hello набора записей уровня, tooprecisely hello записей, которые Здравствуйте, администратор почты требуется доступ к.  Hello почты администратору предоставляется точно контролировать hello ей нужны и будет невозможно toomake любые другие изменения.

Разрешения на уровне RBAC набор записей можно настроить с помощью hello портал Azure, с помощью кнопки hello «пользователи» в колонке hello набор записей:

![Набор записей уровне RBAC через портал Azure hello](./media/dns-protect-zones-recordsets/rbac3.png)

Разрешения RBAC на уровне набора записей также можно [предоставить с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

также является Hello эквивалентную команду [доступны через hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>Пользовательские роли

Встроенная роль «Участник зоны DNS» Hello обеспечивает полный контроль над ресурсов DNS. Он является также возможно toobuild собственного клиента Azure роли, tooprovide даже детальный контроль.

Снова рассмотрим пример hello, в котором создается запись CNAME в зоне hello «customers.contoso.com» для каждой учетной записи клиента Contoso Corporation.  Учетная запись, используемая toomanage Hello этих записей CNAME должны предоставляться записи CNAME toomanage разрешение только.  Это то записи не удается toomodify других типов (например, изменение записи MX) или уровня зоны операций, таких как удаление зоны.

Hello в следующем примере показано определение пользовательской роли для управления только для записей CNAME.

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

Свойства действия Hello определяет hello после разрешения DNS:

* `Microsoft.Network/dnsZones/CNAME/*` предоставляет полный контроль над записями CNAME.
* `Microsoft.Network/dnsZones/read`предоставляет разрешение tooread DNS-зон, но не toomodify их включение вы toosee hello зону, в которой hello создается запись CNAME.

Привет, оставшиеся действия копируются из hello [встроенная роль участника зоны DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).

> [!NOTE]
> Использование пользовательских tooprevent роли RBAC, удаление записи наборов, хотя по-прежнему обеспечивая toobe обновления не эффективный контроль. Наборы записей нельзя удалить, но ничто не препятствует их изменению.  Разрешенные изменения включают добавление и удаление записей из набора записей hello, включая удаление всех записей tooleave «пустой» набор записей. У него есть hello же эффект, что удаление записи hello набор с точки зрения разрешение DNS.

В настоящее время невозможно определить пользовательские определения роли через портал Azure hello. Пользовательскую роль на основе этого определения роли можно создать с помощью Azure PowerShell:

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

Он также могут создаваться через hello Azure CLI:

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

Hello роли могут быть предоставлены в hello таким же образом как встроенные роли, как описано ранее в этой статье.

Дополнительные сведения о том, как toocreate, управление и назначить пользовательских ролей в разделе [настраиваемые роли в Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).

## <a name="resource-locks"></a>Блокировки ресурсов

В tooRBAC Добавление диспетчера ресурсов Azure поддерживает контроль безопасности, а именно: hello too'lock возможность другого типа "ресурсов. Где RBAC правила разрешают передачу toocontrol hello действия конкретных пользователей и групп, блокировки ресурсов, примененные toohello ресурсов и вступают в силу для всех пользователей и ролей. Дополнительные сведения см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).

Существует два типа блокировки ресурсов: **DoNotDelete** и **ReadOnly**. Они могут применяться tooa зоны DNS или tooan набор отдельных записей.  Hello следующих разделах описаны некоторые распространенные сценарии и как toosupport их с помощью блокировки ресурсов.

### <a name="protecting-against-all-changes"></a>Защита от любых изменений

tooprevent изменения внесенные, применить зоны toohello блокировки только для чтения.  Эта блокировка не позволит создавать наборы записей, а также изменять или удалять существующие наборы.

Блокировки уровня ресурсов зоны могут создаваться через портал Azure hello.  Из колонки зоны DNS hello, нажмите кнопку «Блокировка» нажмите «Добавить»:

![Блокировки уровня ресурсов зоны через портал Azure hello](./media/dns-protect-zones-recordsets/locks1.png)

Блокировки ресурсов на уровне зоны также можно создать с помощью Azure PowerShell:

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

Настройка блокировки ресурсов Azure не поддерживается в настоящее время через hello Azure CLI.

### <a name="protecting-individual-records"></a>Защита отдельных записей

tooprevent установить для изменения существующей записи DNS применяются только для чтения блокировки toohello набор записей.

> [!NOTE]
> Применение блокировки DoNotDelete tooa набор записей не эффективный контроль. Он предотвращает набора от удаления записей hello, но она не предотвращает его изменение.  Разрешенные изменения включают добавление и удаление записей из набора записей hello, включая удаление всех записей tooleave «пустой» набор записей. У него есть hello же эффект, что удаление записи hello набор с точки зрения разрешение DNS.

В настоящее время блокировки ресурсов на уровне наборов записей можно настраивать только с помощью Azure PowerShell.  Они не поддерживаются в hello портал Azure или Azure CLI.

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>Защита зоны от удаления

При удалении зоны Azure DNS, также удаляются все наборы записей в зоне hello.  Эту операцию нельзя отменить.  Случайное удаление критическую зону имеет потенциальные toohave hello значительные значимым.  Поэтому это очень важно tooprotect от зоны случайного удаления.

Зоны tooa блокировки DoNotDelete позволяет предотвратить hello зоны от удаления.  Тем не менее поскольку блокировки, наследуются дочерними ресурсами, он также препятствует любой наборов записей в зоне hello от удаления, который может быть нежелательно.  Более того как описано выше примечании hello, также является неэффективным с момента записи по-прежнему могут быть удалены из существующих наборов записей hello.

В качестве альтернативы рассмотрите возможность применения блокировки tooa DoNotDelete запись набора в зоне hello, такие как набор записей SOA hello.  Так как не удается удалить зону hello удаляя hello наборы записей, это обеспечивает защиту от удаления зоны, по-прежнему предоставляя наборами записей в рамках свободно изменить toobe зоны hello. При попытке toodelete hello зоны, диспетчера ресурсов Azure обнаруживает это также удалит набор записей SOA hello и блоки hello вызовов, поскольку hello SOA заблокирован.  Наборы записей не будут удалены.

Hello следующую команду PowerShell создает DoNotDelete блокировку для записи SOA hello hello, учитывая зоны:

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

Другим способом является использование оператора hello tooensure пользовательской роли и службы учетных записей, используемых toomanage зон не имеют зоны tooprevent зоны случайного удаления удаление разрешений. При необходимости toodelete зону можно принудительно выполнить удаление из двух, первый предоставлении разрешений удаления зоны (в области зоны hello tooprevent удаление hello неправильный зоны) и второй toodelete hello зоны.

Такой подход имеет преимущество hello, его работы для всех зон, использованным этих учетных записей без необходимости tooremember toocreate все блокировки. Он имеет недостаток hello, что все учетные записи с разрешениями удаления зоны, например hello владелец подписки, может по-прежнему случайно удалить критическую зону.

Это возможно toouse оба подхода — блокировки ресурсов и пользовательские роли — на hello же время, в целях защиты зоны tooDNS подход глубокой обороны.

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о работе с RBAC см. в разделе [Приступая к управлению доступом в hello портал Azure](../active-directory/role-based-access-control-what-is.md).
* Дополнительные сведения о работе с блокировками ресурсов см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).

