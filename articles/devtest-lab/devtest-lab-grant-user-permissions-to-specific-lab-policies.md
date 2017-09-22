---
title: "Предоставление пользователю разрешений для определенных политик лаборатории | Документация Майкрософт"
description: "Узнайте, как предоставить пользователю разрешения для определенных политик лаборатории в DevTest Labs исходя из его потребностей."
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
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="9ae30-103">Предоставление пользователю разрешений для определенных политик лаборатории</span><span class="sxs-lookup"><span data-stu-id="9ae30-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="9ae30-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9ae30-104">Overview</span></span>
<span data-ttu-id="9ae30-105">В этой статье рассказывается, как с помощью PowerShell предоставить пользователям разрешения для определенной политики лаборатории.</span><span class="sxs-lookup"><span data-stu-id="9ae30-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="9ae30-106">Разрешения могут предоставляться в зависимости от потребностей каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ae30-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="9ae30-107">Например, определенному пользователю можно разрешить изменить параметры политики виртуальной машины, но не политики затрат.</span><span class="sxs-lookup"><span data-stu-id="9ae30-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="9ae30-108">Политики как ресурсы</span><span class="sxs-lookup"><span data-stu-id="9ae30-108">Policies as resources</span></span>
<span data-ttu-id="9ae30-109">Как уже обсуждалось в одноименной статье, [управление доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md) обеспечивает точное управление доступом для Azure.</span><span class="sxs-lookup"><span data-stu-id="9ae30-109">As discussed in the [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="9ae30-110">С помощью RBAC вы можете распределить обязанности внутри команды разработчиков и предоставить пользователям доступ на том уровне, который им необходим для выполнения поставленных задач.</span><span class="sxs-lookup"><span data-stu-id="9ae30-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="9ae30-111">В DevTest Labs политика — это тип ресурса, который включает действие RBAC **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="9ae30-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="9ae30-112">Каждая политика лаборатории представляет собой ресурс типа "Политика" и может быть назначена в качестве области действия для роли RBAC.</span><span class="sxs-lookup"><span data-stu-id="9ae30-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="9ae30-113">Например, чтобы предоставить пользователям разрешения на чтение и запись для **размеры виртуальных Машин допускается** политики, необходимо создать пользовательскую роль, которая работает с **Microsoft.DevTestLab/labs/policySets/policies/*** действие, а затем назначить соответствующим пользователям пользовательской роли в области **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="9ae30-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="9ae30-114">Дополнительные сведения о пользовательских ролях в RBAC см. в статье [Пользовательские роли в Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9ae30-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="9ae30-115">Создание пользовательской роли лаборатории с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ae30-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="9ae30-116">Чтобы начать работу, прочтите статью [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre), в которой рассказывается, как установить и настроить командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ae30-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="9ae30-117">Настроив командлеты Azure PowerShell, вы сможете выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="9ae30-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="9ae30-118">Получать список всех операций и действий по тому или иному поставщику ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9ae30-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="9ae30-119">Получать список действий по определенной роли:</span><span class="sxs-lookup"><span data-stu-id="9ae30-119">List actions in a particular role:</span></span>
* <span data-ttu-id="9ae30-120">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="9ae30-120">Create a custom role</span></span>

<span data-ttu-id="9ae30-121">Примеры выполнения этих задач демонстрирует следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9ae30-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
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

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="9ae30-122">Предоставление пользователю разрешений в отношении определенной политики с помощью пользовательских ролей</span><span class="sxs-lookup"><span data-stu-id="9ae30-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="9ae30-123">Определив пользовательские роли, можно назначить их пользователям.</span><span class="sxs-lookup"><span data-stu-id="9ae30-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="9ae30-124">Чтобы назначить пользовательскую роль, необходимо получить **ObjectId** соответствующего пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ae30-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="9ae30-125">Для этого используйте командлет **Get-AzureRmADUser** .</span><span class="sxs-lookup"><span data-stu-id="9ae30-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="9ae30-126">В следующем примере **ObjectId** пользователя *SomeUser* имеет значение 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="9ae30-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="9ae30-127">Получив **ObjectId** пользователя и имя пользовательской роли, можно назначить эту роль пользователю с помощью командлета **New-AzureRmRoleAssignment**.</span><span class="sxs-lookup"><span data-stu-id="9ae30-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="9ae30-128">В предыдущем примере использовалась политика **AllowedVmSizesInLab** .</span><span class="sxs-lookup"><span data-stu-id="9ae30-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="9ae30-129">Также можно использовать любую из следующих политик:</span><span class="sxs-lookup"><span data-stu-id="9ae30-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="9ae30-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="9ae30-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="9ae30-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="9ae30-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="9ae30-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="9ae30-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="9ae30-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="9ae30-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="9ae30-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ae30-134">Next steps</span></span>
<span data-ttu-id="9ae30-135">После того как пользователю будут предоставлены разрешения для определенных политик лаборатории, можно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9ae30-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* <span data-ttu-id="9ae30-136">[Безопасный доступ к лаборатории](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="9ae30-136">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="9ae30-137">[Определение политик лаборатории](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9ae30-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="9ae30-138">[Создание шаблона лаборатории](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="9ae30-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="9ae30-139">[Создание пользовательских артефактов для виртуальных машин](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="9ae30-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="9ae30-140">[Добавление виртуальной машины с артефактами в лабораторию](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="9ae30-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

