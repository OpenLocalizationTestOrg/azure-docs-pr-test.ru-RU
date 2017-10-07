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
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="1819b-103">Предоставление разрешений пользователю toospecific лаборатории политики</span><span class="sxs-lookup"><span data-stu-id="1819b-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="1819b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="1819b-104">Overview</span></span>
<span data-ttu-id="1819b-105">В этой статье показано, как toouse PowerShell toogrant пользователей разрешения tooa определенной лабораторной политики.</span><span class="sxs-lookup"><span data-stu-id="1819b-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="1819b-106">Разрешения могут предоставляться в зависимости от потребностей каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="1819b-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="1819b-107">Например может потребоваться toogrant определенного hello возможность toochange hello ВМ параметры политики пользователя, но не hello стоимости политики.</span><span class="sxs-lookup"><span data-stu-id="1819b-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="1819b-108">Политики как ресурсы</span><span class="sxs-lookup"><span data-stu-id="1819b-108">Policies as resources</span></span>
<span data-ttu-id="1819b-109">Как было сказано в hello [управления доступом на основе ролей Azure](../active-directory/role-based-access-control-configure.md) статье RBAC разрешение подробного управления доступом ресурсов для Azure.</span><span class="sxs-lookup"><span data-stu-id="1819b-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="1819b-110">RBAC можно разделять обязанностей в рамках команды DevOps и предоставить только hello объем toousers доступа, необходимых tooperform свою работу.</span><span class="sxs-lookup"><span data-stu-id="1819b-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="1819b-111">В DevTest Labs политики является тип ресурса, который включает действие hello RBAC **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="1819b-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="1819b-112">Каждой политики лаборатории — это ресурс в hello тип политики ресурсов и могут быть назначены в качестве роли RBAC tooan области.</span><span class="sxs-lookup"><span data-stu-id="1819b-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="1819b-113">Например, в порядке toogrant пользователям чтение и запись разрешение toohello **размеры виртуальных Машин допускается** политики, необходимо создать пользовательскую роль, который работает с hello **Microsoft.DevTestLab/labs/policySets/policies/** * действия, а затем назначить соответствующим пользователям hello toothis пользовательской роли hello области **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="1819b-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="1819b-114">toolearn Дополнительные сведения о пользовательских ролей, в RBAC, в разделе hello [управления доступом к пользовательских ролей](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1819b-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="1819b-115">Создание пользовательской роли лаборатории с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1819b-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="1819b-116">В порядке tooget к работе, вам потребуется hello tooread следующей статьей, в которой объясняется, как tooinstall и настройте командлеты Azure PowerShell hello: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="1819b-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="1819b-117">После настройки hello командлетов Azure PowerShell можно выполнять следующие задачи hello:</span><span class="sxs-lookup"><span data-stu-id="1819b-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="1819b-118">Список всех операций hello или действий для поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="1819b-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="1819b-119">Получать список действий по определенной роли:</span><span class="sxs-lookup"><span data-stu-id="1819b-119">List actions in a particular role:</span></span>
* <span data-ttu-id="1819b-120">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="1819b-120">Create a custom role</span></span>

<span data-ttu-id="1819b-121">Следующий сценарий PowerShell Hello рассмотрены примеры tooperform следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="1819b-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="1819b-122">Назначение пользователя tooa разрешения для конкретной политики с помощью пользовательских ролей</span><span class="sxs-lookup"><span data-stu-id="1819b-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="1819b-123">После определения пользовательских ролей, можно назначить их toousers.</span><span class="sxs-lookup"><span data-stu-id="1819b-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="1819b-124">В порядке tooassign tooa пользовательской роли пользователя, необходимо сначала получить hello **ObjectId** представляющий этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="1819b-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="1819b-125">toodo, использовать hello **Get AzureRmADUser** командлета.</span><span class="sxs-lookup"><span data-stu-id="1819b-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="1819b-126">В следующем примере hello, hello **ObjectId** из hello *SomeUser* 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 пользователя.</span><span class="sxs-lookup"><span data-stu-id="1819b-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="1819b-127">При наличии hello **ObjectId** для пользователя hello и имя пользовательской роли, можно назначить этого пользователя роль toohello с hello **New AzureRmRoleAssignment** командлета:</span><span class="sxs-lookup"><span data-stu-id="1819b-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="1819b-128">В предыдущем примере hello hello **AllowedVmSizesInLab** используется политика.</span><span class="sxs-lookup"><span data-stu-id="1819b-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="1819b-129">Можно использовать любой из следующих политик hello:</span><span class="sxs-lookup"><span data-stu-id="1819b-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="1819b-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="1819b-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="1819b-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="1819b-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="1819b-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="1819b-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="1819b-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="1819b-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="1819b-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1819b-134">Next steps</span></span>
<span data-ttu-id="1819b-135">Один раз вы предоставили политик лаборатории toospecific разрешения пользователя, ниже приведены некоторые Далее tooconsider действия:</span><span class="sxs-lookup"><span data-stu-id="1819b-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="1819b-136">[Безопасный доступ tooa лаборатории](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="1819b-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="1819b-137">[Определение политик лаборатории](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1819b-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="1819b-138">[Создание шаблона лаборатории](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="1819b-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="1819b-139">[Создание пользовательских артефактов для виртуальных машин](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="1819b-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="1819b-140">[Добавить виртуальную Машину с артефакты лаборатории tooa](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="1819b-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

