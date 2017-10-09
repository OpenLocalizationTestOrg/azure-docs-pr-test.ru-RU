---
title: "aaaAssign и управления политиками ресурсов Azure | Документы Microsoft"
description: "Описывает способ tooapply группы ресурсов Azure политики toosubscriptions и ресурсов и как политики tooview ресурсов."
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="0393d-103">Назначение политик ресурсов и управление ими</span><span class="sxs-lookup"><span data-stu-id="0393d-103">Assign and manage resource policies</span></span>

<span data-ttu-id="0393d-104">tooimplement политики, необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0393d-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="0393d-105">Проверьте политики toosee определения (включая встроенных политик, предоставленное Azure), если он уже существует в подписке, отвечающего вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="0393d-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="0393d-106">Если такая политика существует, получите ее имя.</span><span class="sxs-lookup"><span data-stu-id="0393d-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="0393d-107">Если он не существует, определите правила политики hello с JSON и добавить его в качестве определения политики в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="0393d-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="0393d-108">Этот шаг делает доступными для назначения политики hello, но не применяется hello правила tooyour подписки.</span><span class="sxs-lookup"><span data-stu-id="0393d-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="0393d-109">Для обоих случаях назначьте область tooa hello политики (например, подписка или группа ресурсов).</span><span class="sxs-lookup"><span data-stu-id="0393d-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="0393d-110">правила Hello hello политики теперь будут применены.</span><span class="sxs-lookup"><span data-stu-id="0393d-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="0393d-111">В этой статье основное внимание уделяется toocreate действия hello определения политики и назначьте этой области определения tooa через API-Интерфейс REST, PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0393d-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="0393d-112">При желании toouse hello портала tooassign политики в разделе [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0393d-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="0393d-113">В этой статье не рассматривается hello синтаксис для создания определения политики hello.</span><span class="sxs-lookup"><span data-stu-id="0393d-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="0393d-114">Сведения о синтаксисе политики см. в разделе [Общие сведения о политике ресурсов](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0393d-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="0393d-115">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="0393d-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="0393d-116">Создание определения политики</span><span class="sxs-lookup"><span data-stu-id="0393d-116">Create policy definition</span></span>

<span data-ttu-id="0393d-117">Можно создать политику с hello [API REST для определения политик](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="0393d-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="0393d-118">Hello REST API позволяет toocreate и удалять определения политики, а также получение сведений о существующих определений.</span><span class="sxs-lookup"><span data-stu-id="0393d-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="0393d-119">Запустите toocreate Определение политики:</span><span class="sxs-lookup"><span data-stu-id="0393d-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="0393d-120">Включить запрос текст аналогичные toohello, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="0393d-120">Include a request body similar toohello following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

### <a name="assign-policy"></a><span data-ttu-id="0393d-121">Назначение политики</span><span class="sxs-lookup"><span data-stu-id="0393d-121">Assign policy</span></span>

<span data-ttu-id="0393d-122">Можно применить определения политики hello в области hello требуемого по hello [API REST для назначения политик](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="0393d-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="0393d-123">Hello REST API позволяет toocreate и удалять назначения политики, а также получение сведений о существующих назначений.</span><span class="sxs-lookup"><span data-stu-id="0393d-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="0393d-124">Запустите toocreate назначение политики:</span><span class="sxs-lookup"><span data-stu-id="0393d-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="0393d-125">Hello {назначение политики} — hello имя назначения политики hello.</span><span class="sxs-lookup"><span data-stu-id="0393d-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="0393d-126">Включить запрос текст аналогичные toohello, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="0393d-126">Include a request body similar toohello following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="0393d-127">Просмотр политики</span><span class="sxs-lookup"><span data-stu-id="0393d-127">View policy</span></span>
<span data-ttu-id="0393d-128">использовать политику, tooget hello [получить определения политики](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) операции.</span><span class="sxs-lookup"><span data-stu-id="0393d-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="0393d-129">Получение псевдонимов</span><span class="sxs-lookup"><span data-stu-id="0393d-129">Get aliases</span></span>
<span data-ttu-id="0393d-130">Вы можете получить псевдонимы через hello REST API:</span><span class="sxs-lookup"><span data-stu-id="0393d-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="0393d-131">Привет, в следующем примере показано определение псевдонима.</span><span class="sxs-lookup"><span data-stu-id="0393d-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="0393d-132">Как видите, псевдоним определяет пути в различных версиях API, даже если имя свойства изменено.</span><span class="sxs-lookup"><span data-stu-id="0393d-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a><span data-ttu-id="0393d-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0393d-133">PowerShell</span></span>

<span data-ttu-id="0393d-134">Прежде чем продолжить с примерами PowerShell hello, убедитесь, что у вас есть [установлена последняя версия hello](/powershell/azure/install-azurerm-ps) из Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0393d-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="0393d-135">Параметры политики были добавлены в версии 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="0393d-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="0393d-136">При наличии более ранней версии, примеры hello возврата не удается найти параметр, указывающий, hello ошибки.</span><span class="sxs-lookup"><span data-stu-id="0393d-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="0393d-137">Просмотр определений политик</span><span class="sxs-lookup"><span data-stu-id="0393d-137">View policy definitions</span></span>
<span data-ttu-id="0393d-138">toosee все определения политики в вашей подписке hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="0393d-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="0393d-139">Она возвращает все доступные определения политик, включая встроенные политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="0393d-140">Каждая политика возвращается в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="0393d-140">Each policy is returned in hello following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="0393d-141">Перед продолжением toocreate определения политики просмотрите hello встроенных политик.</span><span class="sxs-lookup"><span data-stu-id="0393d-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="0393d-142">Если встроенные политику, которая применяет ограничения hello, что нужно найти, можно пропустить Создание определения политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="0393d-143">Вместо этого назначьте область toohello требуемого hello встроенные политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="0393d-144">Создание определения политики</span><span class="sxs-lookup"><span data-stu-id="0393d-144">Create policy definition</span></span>
<span data-ttu-id="0393d-145">Можно создать с помощью hello определения политики `New-AzureRmPolicyDefinition` командлета.</span><span class="sxs-lookup"><span data-stu-id="0393d-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'
```            

<span data-ttu-id="0393d-146">Hello выходные данные, хранящиеся в `$definition` объект, который используется при назначении политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="0393d-147">Вместо того чтобы задавать hello JSON в качестве параметра, чтобы обеспечить hello путь tooa .json файл, содержащий правила политики hello.</span><span class="sxs-lookup"><span data-stu-id="0393d-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="0393d-148">Hello следующем примере создается определение политики, содержащий параметры.</span><span class="sxs-lookup"><span data-stu-id="0393d-148">hello following example creates a policy definition that includes parameters:</span></span>

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="0393d-149">Назначение политики</span><span class="sxs-lookup"><span data-stu-id="0393d-149">Assign policy</span></span>

<span data-ttu-id="0393d-150">Применение политики hello в hello требуемой области с помощью hello `New-AzureRmPolicyAssignment` командлета.</span><span class="sxs-lookup"><span data-stu-id="0393d-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="0393d-151">Следующий пример Hello назначает группы ресурсов tooa политики hello.</span><span class="sxs-lookup"><span data-stu-id="0393d-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="0393d-152">tooassign политику, которая требует наличия параметров, создания и объекта с этими значениями.</span><span class="sxs-lookup"><span data-stu-id="0393d-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="0393d-153">Hello следующий пример извлекает встроенные политики и передается в значениях параметров:</span><span class="sxs-lookup"><span data-stu-id="0393d-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="0393d-154">Просмотр назначения политики</span><span class="sxs-lookup"><span data-stu-id="0393d-154">View policy assignment</span></span>

<span data-ttu-id="0393d-155">Используйте tooget назначение определенные политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="0393d-156">правило политики hello tooview для определения политики, используйте:</span><span class="sxs-lookup"><span data-stu-id="0393d-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="0393d-157">Удаление назначения политики</span><span class="sxs-lookup"><span data-stu-id="0393d-157">Remove policy assignment</span></span> 

<span data-ttu-id="0393d-158">Используйте tooremove назначение политики:</span><span class="sxs-lookup"><span data-stu-id="0393d-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="0393d-159">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="0393d-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="0393d-160">Просмотр определений политик</span><span class="sxs-lookup"><span data-stu-id="0393d-160">View policy definitions</span></span>
<span data-ttu-id="0393d-161">toosee все определения политики в вашей подписке hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="0393d-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="0393d-162">Она возвращает все доступные определения политик, включая встроенные политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="0393d-163">Каждая политика возвращается в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="0393d-163">Each policy is returned in hello following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

<span data-ttu-id="0393d-164">Перед продолжением toocreate определения политики просмотрите hello встроенных политик.</span><span class="sxs-lookup"><span data-stu-id="0393d-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="0393d-165">Если встроенные политику, которая применяет ограничения hello, что нужно найти, можно пропустить Создание определения политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="0393d-166">Вместо этого назначьте область toohello требуемого hello встроенные политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="0393d-167">Создание определения политики</span><span class="sxs-lookup"><span data-stu-id="0393d-167">Create policy definition</span></span>

<span data-ttu-id="0393d-168">Можно создать с помощью Azure CLI с помощью команды определения политики hello определения политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'    
```

### <a name="assign-policy"></a><span data-ttu-id="0393d-169">Назначение политики</span><span class="sxs-lookup"><span data-stu-id="0393d-169">Assign policy</span></span>

<span data-ttu-id="0393d-170">Можно задать область toohello требуемого hello политики с помощью команды назначения политики hello.</span><span class="sxs-lookup"><span data-stu-id="0393d-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="0393d-171">Следующий пример Hello Назначение группы ресурсов tooa политики.</span><span class="sxs-lookup"><span data-stu-id="0393d-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="0393d-172">Просмотр назначения политики</span><span class="sxs-lookup"><span data-stu-id="0393d-172">View policy assignment</span></span>

<span data-ttu-id="0393d-173">tooview назначение политики предоставить имя назначения политики hello и область hello.</span><span class="sxs-lookup"><span data-stu-id="0393d-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="0393d-174">Удаление назначения политики</span><span class="sxs-lookup"><span data-stu-id="0393d-174">Remove policy assignment</span></span> 

<span data-ttu-id="0393d-175">Используйте tooremove назначение политики:</span><span class="sxs-lookup"><span data-stu-id="0393d-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="0393d-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0393d-176">Next steps</span></span>
* <span data-ttu-id="0393d-177">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="0393d-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

