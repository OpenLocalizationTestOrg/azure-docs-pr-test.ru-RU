---
title: "политики лаборатории toospecific разрешения пользователя aaaGrant | Документы Microsoft"
description: "Узнайте, как политики toogrant пользователя разрешения toospecific лаборатории в DevTest Labs исходя из потребностей каждого пользователя"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a>Предоставление разрешений пользователю toospecific лаборатории политики
## <a name="overview"></a>Обзор
В этой статье показано, как toouse PowerShell toogrant пользователей разрешения tooa определенной лабораторной политики. Разрешения могут предоставляться в зависимости от потребностей каждого пользователя. Например может потребоваться toogrant определенного hello возможность toochange hello ВМ параметры политики пользователя, но не hello стоимости политики.

## <a name="policies-as-resources"></a>Политики как ресурсы
Как было сказано в hello [управления доступом на основе ролей Azure](../active-directory/role-based-access-control-configure.md) статье RBAC разрешение подробного управления доступом ресурсов для Azure. RBAC можно разделять обязанностей в рамках команды DevOps и предоставить только hello объем toousers доступа, необходимых tooperform свою работу.

В DevTest Labs политики является тип ресурса, который включает действие hello RBAC **Microsoft.DevTestLab/labs/policySets/policies/**. Каждой политики лаборатории — это ресурс в hello тип политики ресурсов и могут быть назначены в качестве роли RBAC tooan области.

Например, в порядке toogrant пользователям чтение и запись разрешение toohello **размеры виртуальных Машин допускается** политики, необходимо создать пользовательскую роль, который работает с hello **Microsoft.DevTestLab/labs/policySets/policies/** * действия, а затем назначить соответствующим пользователям hello toothis пользовательской роли hello области **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.

toolearn Дополнительные сведения о пользовательских ролей, в RBAC, в разделе hello [управления доступом к пользовательских ролей](../active-directory/role-based-access-control-custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>Создание пользовательской роли лаборатории с помощью PowerShell
В порядке tooget к работе, вам потребуется hello tooread следующей статьей, в которой объясняется, как tooinstall и настройте командлеты Azure PowerShell hello: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).

После настройки hello командлетов Azure PowerShell можно выполнять следующие задачи hello:

* Список всех операций hello или действий для поставщика ресурсов
* Получать список действий по определенной роли:
* Создание настраиваемой роли

Следующий сценарий PowerShell Hello рассмотрены примеры tooperform следующие задачи:

    ‘List all hello operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a>Назначение пользователя tooa разрешения для конкретной политики с помощью пользовательских ролей
После определения пользовательских ролей, можно назначить их toousers. В порядке tooassign tooa пользовательской роли пользователя, необходимо сначала получить hello **ObjectId** представляющий этого пользователя. toodo, использовать hello **Get AzureRmADUser** командлета.

В следующем примере hello, hello **ObjectId** из hello *SomeUser* 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 пользователя.

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

При наличии hello **ObjectId** для пользователя hello и имя пользовательской роли, можно назначить этого пользователя роль toohello с hello **New AzureRmRoleAssignment** командлета:

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

В предыдущем примере hello hello **AllowedVmSizesInLab** используется политика. Можно использовать любой из следующих политик hello:

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Дальнейшие действия
Один раз вы предоставили политик лаборатории toospecific разрешения пользователя, ниже приведены некоторые Далее tooconsider действия:

* [Безопасный доступ tooa лаборатории](devtest-lab-add-devtest-user.md).
* [Определение политик лаборатории](devtest-lab-set-lab-policy.md).
* [Создание шаблона лаборатории](devtest-lab-create-template.md).
* [Создание пользовательских артефактов для виртуальных машин](devtest-lab-artifact-author.md).
* [Добавить виртуальную Машину с артефакты лаборатории tooa](devtest-lab-add-vm-with-artifacts.md).

