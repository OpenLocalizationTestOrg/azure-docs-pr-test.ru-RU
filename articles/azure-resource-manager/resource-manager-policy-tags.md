---
title: "политики aaaAzure ресурсов для тегов | Документы Microsoft"
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
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="ed05d-103">Применение политик ресурсов для тегов</span><span class="sxs-lookup"><span data-stu-id="ed05d-103">Apply resource policies for tags</span></span>

<span data-ttu-id="ed05d-104">В этом разделе предоставляет политики общих правил, которые можно применять tooensure согласованное использование тегов для ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ed05d-104">This topic provides common policy rules you can apply tooensure consistent use of tags on resources.</span></span>

<span data-ttu-id="ed05d-105">Применение группы ресурсов tooa политики тег или подписки с существующими ресурсами не применяются задним числом hello политики toothose ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ed05d-105">Applying a tag policy tooa resource group or subscription with existing resources does not retroactively apply hello policy toothose resources.</span></span> <span data-ttu-id="ed05d-106">политика hello tooenforce на эти ресурсы включать обновления toohello существующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ed05d-106">tooenforce hello policies on those resources, trigger an update toohello existing resources.</span></span> <span data-ttu-id="ed05d-107">Эта статья содержит пример PowerShell для активации обновления.</span><span class="sxs-lookup"><span data-stu-id="ed05d-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="ed05d-108">Обеспечение всех ресурсов в группе ресурсов значением или тегом</span><span class="sxs-lookup"><span data-stu-id="ed05d-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="ed05d-109">Общим требованием является наличие определенного тега и значения у всех ресурсов в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ed05d-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="ed05d-110">Это требование не часто необходимые tootrack затраты по отделам.</span><span class="sxs-lookup"><span data-stu-id="ed05d-110">This requirement is often needed tootrack costs by department.</span></span> <span data-ttu-id="ed05d-111">должны быть выполнены следующие условия Hello.</span><span class="sxs-lookup"><span data-stu-id="ed05d-111">hello following conditions must be met:</span></span>

* <span data-ttu-id="ed05d-112">Hello требуется тег значение присоединенных toonew и являются обновленные ресурсы, у которых нет тегов hello.</span><span class="sxs-lookup"><span data-stu-id="ed05d-112">hello required tag and value are appended toonew and updated resources that do not have hello tag.</span></span>
* <span data-ttu-id="ed05d-113">Hello необходимые тега и значение нельзя удалить из любые существующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ed05d-113">hello required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="ed05d-114">Это требование можно сделать путем применения две группы ресурсов tooa встроенных политик.</span><span class="sxs-lookup"><span data-stu-id="ed05d-114">You accomplish this requirement by applying two built-in policies tooa resource group.</span></span>

| <span data-ttu-id="ed05d-115">ИД</span><span class="sxs-lookup"><span data-stu-id="ed05d-115">ID</span></span> | <span data-ttu-id="ed05d-116">Описание</span><span class="sxs-lookup"><span data-stu-id="ed05d-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="ed05d-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="ed05d-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="ed05d-118">Применяет обязательный тег и его значение по умолчанию, если она не указана пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="ed05d-118">Applies a required tag and its default value when it is not specified by hello user.</span></span> |
| <span data-ttu-id="ed05d-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="ed05d-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="ed05d-120">Принудительно применяет обязательный тег и его значение.</span><span class="sxs-lookup"><span data-stu-id="ed05d-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="ed05d-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed05d-121">PowerShell</span></span>

<span data-ttu-id="ed05d-122">Следующий сценарий PowerShell Hello назначает hello две встроенные определения tooa ресурсов группы политики.</span><span class="sxs-lookup"><span data-stu-id="ed05d-122">hello following PowerShell script assigns hello two built-in policy definitions tooa resource group.</span></span> <span data-ttu-id="ed05d-123">Перед выполнением сценария hello, назначьте группе ресурсов toohello все требуемые теги.</span><span class="sxs-lookup"><span data-stu-id="ed05d-123">Before running hello script, assign all required tags toohello resource group.</span></span> <span data-ttu-id="ed05d-124">Каждый тег в группе ресурсов hello является обязательным для hello ресурсов в группе hello.</span><span class="sxs-lookup"><span data-stu-id="ed05d-124">Each tag on hello resource group is required for hello resources in hello group.</span></span> <span data-ttu-id="ed05d-125">группы ресурсов tooall tooassign в вашей подписке не предоставляют hello `-Name` параметр при получении групп ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="ed05d-125">tooassign tooall resource groups in your subscription, do not provide hello `-Name` parameter when getting hello resource groups.</span></span>

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

<span data-ttu-id="ed05d-126">После назначения политики hello, вы можете активировать tooall обновления существующих политик тег hello tooenforce ресурсов, добавленных вами.</span><span class="sxs-lookup"><span data-stu-id="ed05d-126">After assigning hello policies, you can trigger an update tooall existing resources tooenforce hello tag policies you have added.</span></span> <span data-ttu-id="ed05d-127">Hello следующий сценарий сохраняет все прочие теги, существовавшие в hello ресурсы:</span><span class="sxs-lookup"><span data-stu-id="ed05d-127">hello following script retains any other tags that existed on hello resources:</span></span>

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

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="ed05d-128">Требование тегов для типа ресурса</span><span class="sxs-lookup"><span data-stu-id="ed05d-128">Require tags for a resource type</span></span>
<span data-ttu-id="ed05d-129">Hello в следующем примере показано, как тег toorequire логические операторы toonest приложения для только указанный тип ресурса (в этом случае учетных записей хранилища).</span><span class="sxs-lookup"><span data-stu-id="ed05d-129">hello following example shows how toonest logical operators toorequire an application tag for only a specified resource type (in this case, storage accounts).</span></span>

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

## <a name="require-tag"></a><span data-ttu-id="ed05d-130">Требование тега</span><span class="sxs-lookup"><span data-stu-id="ed05d-130">Require tag</span></span>
<span data-ttu-id="ed05d-131">Hello следующая политика запрещает запросы, у которых нет тега, содержащего ключ «Центр затрат» (могут применяться любое значение):</span><span class="sxs-lookup"><span data-stu-id="ed05d-131">hello following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ed05d-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed05d-132">Next steps</span></span>
* <span data-ttu-id="ed05d-133">После определения правила политики (как показано в предыдущих примерах hello), требуется определение политики toocreate hello и назначьте его tooa области.</span><span class="sxs-lookup"><span data-stu-id="ed05d-133">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="ed05d-134">Hello область может быть подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ed05d-134">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="ed05d-135">политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ed05d-135">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="ed05d-136">политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="ed05d-136">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="ed05d-137">Введение tooresource политики, в разделе [Общие сведения о политике ресурсов](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ed05d-137">For an introduction tooresource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="ed05d-138">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ed05d-138">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

