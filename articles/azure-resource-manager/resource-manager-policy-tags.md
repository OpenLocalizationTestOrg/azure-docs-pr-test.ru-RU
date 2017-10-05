---
title: "Политики ресурсов Azure для тегов | Документация Майкрософт"
description: "Статья содержит примеры политик ресурсов для управления тегами ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 469bd8d637337e5900ea84c6bfaf88064695fb7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="ab47e-103">Применение политик ресурсов для тегов</span><span class="sxs-lookup"><span data-stu-id="ab47e-103">Apply resource policies for tags</span></span>

<span data-ttu-id="ab47e-104">Этот раздел содержит общие правила политики, которые можно применять, чтобы обеспечить согласованное использование тегов для ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ab47e-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span></span>

<span data-ttu-id="ab47e-105">Применение политики тегов к группе ресурсов или подпискам с существующими ресурсами не позволяет применить ее к этим ресурсам задним числом.</span><span class="sxs-lookup"><span data-stu-id="ab47e-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span></span> <span data-ttu-id="ab47e-106">Чтобы применить политики к этим ресурсам, активируйте обновление существующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ab47e-106">To enforce the policies on those resources, trigger an update to the existing resources.</span></span> <span data-ttu-id="ab47e-107">Эта статья содержит пример PowerShell для активации обновления.</span><span class="sxs-lookup"><span data-stu-id="ab47e-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="ab47e-108">Обеспечение всех ресурсов в группе ресурсов значением или тегом</span><span class="sxs-lookup"><span data-stu-id="ab47e-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="ab47e-109">Общим требованием является наличие определенного тега и значения у всех ресурсов в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ab47e-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="ab47e-110">Это требование обычно необходимо для отслеживания затрат по отделу.</span><span class="sxs-lookup"><span data-stu-id="ab47e-110">This requirement is often needed to track costs by department.</span></span> <span data-ttu-id="ab47e-111">Должны быть выполнены следующие условия.</span><span class="sxs-lookup"><span data-stu-id="ab47e-111">The following conditions must be met:</span></span>

* <span data-ttu-id="ab47e-112">Обязательные тег и значение добавляются к новым и обновленным ресурсам, у которых нет тега.</span><span class="sxs-lookup"><span data-stu-id="ab47e-112">The required tag and value are appended to new and updated resources that do not have the tag.</span></span>
* <span data-ttu-id="ab47e-113">Обязательные тег и значение невозможно удалить из каких-либо существующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ab47e-113">The required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="ab47e-114">Это требование можно выполнить, применив к группе ресурсов две встроенные политики.</span><span class="sxs-lookup"><span data-stu-id="ab47e-114">You accomplish this requirement by applying two built-in policies to a resource group.</span></span>

| <span data-ttu-id="ab47e-115">ИД</span><span class="sxs-lookup"><span data-stu-id="ab47e-115">ID</span></span> | <span data-ttu-id="ab47e-116">Описание</span><span class="sxs-lookup"><span data-stu-id="ab47e-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="ab47e-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="ab47e-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="ab47e-118">Применяет обязательный тег и его значение по умолчанию, если его не задал пользователь.</span><span class="sxs-lookup"><span data-stu-id="ab47e-118">Applies a required tag and its default value when it is not specified by the user.</span></span> |
| <span data-ttu-id="ab47e-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="ab47e-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="ab47e-120">Принудительно применяет обязательный тег и его значение.</span><span class="sxs-lookup"><span data-stu-id="ab47e-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="ab47e-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab47e-121">PowerShell</span></span>

<span data-ttu-id="ab47e-122">Следующий сценарий PowerShell назначает группе ресурсов два определения встроенных политик.</span><span class="sxs-lookup"><span data-stu-id="ab47e-122">The following PowerShell script assigns the two built-in policy definitions to a resource group.</span></span> <span data-ttu-id="ab47e-123">Перед запуском сценария назначьте группе ресурсов все необходимые теги.</span><span class="sxs-lookup"><span data-stu-id="ab47e-123">Before running the script, assign all required tags to the resource group.</span></span> <span data-ttu-id="ab47e-124">Каждый тег в группе ресурсов нужен для содержащегося в ней ресурса.</span><span class="sxs-lookup"><span data-stu-id="ab47e-124">Each tag on the resource group is required for the resources in the group.</span></span> <span data-ttu-id="ab47e-125">Чтобы охватить все группы ресурсов в подписке, не указывайте параметр `-Name` при получении групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ab47e-125">To assign to all resource groups in your subscription, do not provide the `-Name` parameter when getting the resource groups.</span></span>

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

<span data-ttu-id="ab47e-126">После назначения политик можно активировать обновление для всех существующих ресурсов, чтобы применить добавленные политики тегов.</span><span class="sxs-lookup"><span data-stu-id="ab47e-126">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span></span> <span data-ttu-id="ab47e-127">Следующий сценарий сохраняет другие теги, которые существовали в ресурсах:</span><span class="sxs-lookup"><span data-stu-id="ab47e-127">The following script retains any other tags that existed on the resources:</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="ab47e-128">Требование тегов для типа ресурса</span><span class="sxs-lookup"><span data-stu-id="ab47e-128">Require tags for a resource type</span></span>
<span data-ttu-id="ab47e-129">В следующем примере показано, как вложить логические операторы, согласно которым приложение будет помечать тегами только ресурсы определенного типа (в этом случае это учетные записи хранения).</span><span class="sxs-lookup"><span data-stu-id="ab47e-129">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="ab47e-130">Требование тега</span><span class="sxs-lookup"><span data-stu-id="ab47e-130">Require tag</span></span>
<span data-ttu-id="ab47e-131">Следующая политика отклоняет запросы без тега с ключом costCenter (может иметь любое значение).</span><span class="sxs-lookup"><span data-stu-id="ab47e-131">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="ab47e-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab47e-132">Next steps</span></span>
* <span data-ttu-id="ab47e-133">После определения правила политики (как показано в приведенных выше примерах) необходимо создать определение политики и назначить ей область.</span><span class="sxs-lookup"><span data-stu-id="ab47e-133">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="ab47e-134">Областью может быть подписка, группа ресурсов или ресурс.</span><span class="sxs-lookup"><span data-stu-id="ab47e-134">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="ab47e-135">Сведения о назначении политик с помощью портала см. в статье [Назначение политик ресурсов и управление ими с помощью портала Azure](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ab47e-135">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="ab47e-136">Сведения о назначении политик с помощью REST API, PowerShell или Azure CLI см. в статье [Назначение политик ресурсов и управление ими](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="ab47e-136">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="ab47e-137">Введение в политики ресурсов представлено в разделе [Общие сведения о политике ресурсов](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ab47e-137">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="ab47e-138">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="ab47e-138">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

