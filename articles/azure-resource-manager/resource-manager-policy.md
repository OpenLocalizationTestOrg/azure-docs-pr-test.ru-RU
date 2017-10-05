---
title: "Политики ресурсов Azure | Документация Майкрософт"
description: "Использование политик Azure Resource Manager, обеспечивающих согласованную настройку свойств ресурсов при развертывании. Политики можно применять на уровне подписки или группы ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="62b84-104">Общие сведения о политике ресурсов</span><span class="sxs-lookup"><span data-stu-id="62b84-104">Resource policy overview</span></span>
<span data-ttu-id="62b84-105">Политики ресурсов позволяют настроить определенные соглашения для ресурсов в организации.</span><span class="sxs-lookup"><span data-stu-id="62b84-105">Resource policies enable you to establish conventions for resources in your organization.</span></span> <span data-ttu-id="62b84-106">Это соглашения помогут вам контролировать расходы и управлять ресурсами.</span><span class="sxs-lookup"><span data-stu-id="62b84-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="62b84-107">Например, можно указать, что разрешены только определенные типы виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="62b84-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="62b84-108">Кроме того, можно требовать наличие определенного тега для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="62b84-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="62b84-109">Политики наследуются всеми дочерними ресурсами.</span><span class="sxs-lookup"><span data-stu-id="62b84-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="62b84-110">Это значит, что политики, применяемые к группе ресурсов, применяются также ко всем ресурсам в этой группе.</span><span class="sxs-lookup"><span data-stu-id="62b84-110">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="62b84-111">При работе с политиками нужно знать две важные концепции:</span><span class="sxs-lookup"><span data-stu-id="62b84-111">There are two concepts to understand about policies:</span></span>

* <span data-ttu-id="62b84-112">определение политики описывает, когда и как политика будет применяться;</span><span class="sxs-lookup"><span data-stu-id="62b84-112">policy definition - you describe when the policy is enforced and what action to take</span></span>
* <span data-ttu-id="62b84-113">назначение политики привязывает эту политику к определенной области (к подписке или группе ресурсов).</span><span class="sxs-lookup"><span data-stu-id="62b84-113">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span></span>

<span data-ttu-id="62b84-114">В этой статье рассматривается только определение политики.</span><span class="sxs-lookup"><span data-stu-id="62b84-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="62b84-115">Сведения о назначении политик см. в статьях [Назначение политик ресурсов и управление ими с помощью портала Azure](resource-manager-policy-portal.md) и [Назначение политик ресурсов и управление ими](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="62b84-115">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="62b84-116">Политики оцениваются при создании и обновлении ресурсов (операции PUT и PATCH).</span><span class="sxs-lookup"><span data-stu-id="62b84-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="62b84-117">Сейчас политика не вычисляет типы ресурсов, которые не поддерживают теги, вид и расположение, например тип ресурса Microsoft.Resources/deployments.</span><span class="sxs-lookup"><span data-stu-id="62b84-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="62b84-118">Их поддержка будет добавлена в будущем.</span><span class="sxs-lookup"><span data-stu-id="62b84-118">This support will be added at a future time.</span></span> <span data-ttu-id="62b84-119">Чтобы избежать проблем с обратной совместимостью, необходимо явно указывать тип при создании политик.</span><span class="sxs-lookup"><span data-stu-id="62b84-119">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="62b84-120">Например, политика тегов, которая не указывает типы, применяется для всех типов.</span><span class="sxs-lookup"><span data-stu-id="62b84-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="62b84-121">В этом случае может произойти ошибка развертывания шаблона, если существует вложенный ресурс, который не поддерживает тег, и в вычисление политики был добавлен тип ресурса развертывания.</span><span class="sxs-lookup"><span data-stu-id="62b84-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="62b84-122">Чем это отличается от управления доступом на основе ролей?</span><span class="sxs-lookup"><span data-stu-id="62b84-122">How is it different from RBAC?</span></span>
<span data-ttu-id="62b84-123">Существует ряд ключевых различий между политиками и управлением доступом на основе ролей (RBAC).</span><span class="sxs-lookup"><span data-stu-id="62b84-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="62b84-124">RBAC определяет действия **пользователя** в различных областях.</span><span class="sxs-lookup"><span data-stu-id="62b84-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="62b84-125">Например, если вам назначена роль участника для группы ресурсов в требуемой области, вы можете вносить изменения в эту группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="62b84-125">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span></span> <span data-ttu-id="62b84-126">Политика определяет свойства **ресурсов** во время их развертывания.</span><span class="sxs-lookup"><span data-stu-id="62b84-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="62b84-127">Например, с помощью политик можно управлять типами ресурсов, которые можно подготовить,</span><span class="sxs-lookup"><span data-stu-id="62b84-127">For example, through policies, you can control the types of resources that can be provisioned.</span></span> <span data-ttu-id="62b84-128">или ограничить расположения, в которых можно подготовить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="62b84-128">Or, you can restrict the locations in which the resources can be provisioned.</span></span> <span data-ttu-id="62b84-129">В отличие от RBAC, политика представляет собой систему разрешения по умолчанию и явного запрета.</span><span class="sxs-lookup"><span data-stu-id="62b84-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="62b84-130">Чтобы использовать политики, нужно пройти аутентификацию с помощью RBAC.</span><span class="sxs-lookup"><span data-stu-id="62b84-130">To use policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="62b84-131">В частности, для учетной записи должны быть предоставлены:</span><span class="sxs-lookup"><span data-stu-id="62b84-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="62b84-132">`Microsoft.Authorization/policydefinitions/write` разрешение на создание политики;</span><span class="sxs-lookup"><span data-stu-id="62b84-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span></span>
* <span data-ttu-id="62b84-133">`Microsoft.Authorization/policyassignments/write` разрешение на назначение политики.</span><span class="sxs-lookup"><span data-stu-id="62b84-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span></span> 

<span data-ttu-id="62b84-134">Эти разрешения не включаются в роль **Участник**.</span><span class="sxs-lookup"><span data-stu-id="62b84-134">These permissions are not included in the **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="62b84-135">Встроенные политики</span><span class="sxs-lookup"><span data-stu-id="62b84-135">Built-in policies</span></span>

<span data-ttu-id="62b84-136">В Azure доступно несколько встроенных определений политик, которые сокращают число соответствующих политик.</span><span class="sxs-lookup"><span data-stu-id="62b84-136">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="62b84-137">Прежде чем приступить к работе с определениями политик, следует проверить, не обеспечивает ли какая-либо встроенная политика нужные вам ограничения.</span><span class="sxs-lookup"><span data-stu-id="62b84-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides the definition you need.</span></span> <span data-ttu-id="62b84-138">Определения встроенных политик приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="62b84-138">The built-in policy definitions are:</span></span>

* <span data-ttu-id="62b84-139">Allowed locations;</span><span class="sxs-lookup"><span data-stu-id="62b84-139">Allowed locations</span></span>
* <span data-ttu-id="62b84-140">Допустимые типы ресурсов</span><span class="sxs-lookup"><span data-stu-id="62b84-140">Allowed resource types</span></span>
* <span data-ttu-id="62b84-141">Allowed storage account SKUs;</span><span class="sxs-lookup"><span data-stu-id="62b84-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="62b84-142">Allowed virtual machine SKUs;</span><span class="sxs-lookup"><span data-stu-id="62b84-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="62b84-143">Apply tag and default value;</span><span class="sxs-lookup"><span data-stu-id="62b84-143">Apply tag and default value</span></span>
* <span data-ttu-id="62b84-144">Enforce tag and value;</span><span class="sxs-lookup"><span data-stu-id="62b84-144">Enforce tag and value</span></span>
* <span data-ttu-id="62b84-145">Not allowed resource types;</span><span class="sxs-lookup"><span data-stu-id="62b84-145">Not allowed resource types</span></span>
* <span data-ttu-id="62b84-146">Require SQL Server version 12.0;</span><span class="sxs-lookup"><span data-stu-id="62b84-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="62b84-147">Require storage account encryption.</span><span class="sxs-lookup"><span data-stu-id="62b84-147">Require storage account encryption</span></span>

<span data-ttu-id="62b84-148">Любую из этих политик можно назначить с помощью [портала](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell) или [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="62b84-148">You can assign any of these policies through the [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="62b84-149">Структура определения политики</span><span class="sxs-lookup"><span data-stu-id="62b84-149">Policy definition structure</span></span>
<span data-ttu-id="62b84-150">Для создания определения политики используется JSON.</span><span class="sxs-lookup"><span data-stu-id="62b84-150">You use JSON to create a policy definition.</span></span> <span data-ttu-id="62b84-151">Определение политики содержит следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="62b84-151">The policy definition contains elements for:</span></span>

* <span data-ttu-id="62b84-152">parameters</span><span class="sxs-lookup"><span data-stu-id="62b84-152">parameters</span></span>
* <span data-ttu-id="62b84-153">display name</span><span class="sxs-lookup"><span data-stu-id="62b84-153">display name</span></span>
* <span data-ttu-id="62b84-154">description</span><span class="sxs-lookup"><span data-stu-id="62b84-154">description</span></span>
* <span data-ttu-id="62b84-155">policy rule</span><span class="sxs-lookup"><span data-stu-id="62b84-155">policy rule</span></span>
  * <span data-ttu-id="62b84-156">logical evaluation</span><span class="sxs-lookup"><span data-stu-id="62b84-156">logical evaluation</span></span>
  * <span data-ttu-id="62b84-157">effect</span><span class="sxs-lookup"><span data-stu-id="62b84-157">effect</span></span>

<span data-ttu-id="62b84-158">В следующем примере показана политика, которая налагает ограничения на набор расположений для развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="62b84-158">The following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
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

## <a name="parameters"></a><span data-ttu-id="62b84-159">Параметры</span><span class="sxs-lookup"><span data-stu-id="62b84-159">Parameters</span></span>
<span data-ttu-id="62b84-160">Использование параметров помогает упростить управление политиками за счет сокращения числа определений политики.</span><span class="sxs-lookup"><span data-stu-id="62b84-160">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="62b84-161">Вы можете определить политику для свойства ресурса (например, чтобы ограничить набор расположений для развертывания этих ресурсов), включив в определение параметры.</span><span class="sxs-lookup"><span data-stu-id="62b84-161">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span></span> <span data-ttu-id="62b84-162">Затем это определение политики можно неоднократно использовать в разных сценариях, передавая в него разные значения (например, набор расположений для определенной подписки) при назначении политики.</span><span class="sxs-lookup"><span data-stu-id="62b84-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span></span>

<span data-ttu-id="62b84-163">А параметры объявляются при создании определения политики.</span><span class="sxs-lookup"><span data-stu-id="62b84-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="62b84-164">Типом параметра может быть строка или массив.</span><span class="sxs-lookup"><span data-stu-id="62b84-164">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="62b84-165">Свойство метаданных используется в таких инструментах, как портал Azure, для отображения удобных для пользователя сведений.</span><span class="sxs-lookup"><span data-stu-id="62b84-165">The metadata property is used for tools like Azure portal to display user-friendly information.</span></span> 

<span data-ttu-id="62b84-166">В правилах политики полученные параметры используются так:</span><span class="sxs-lookup"><span data-stu-id="62b84-166">In the policy rule, you reference parameters with the following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="62b84-167">Отображаемое имя и описание</span><span class="sxs-lookup"><span data-stu-id="62b84-167">Display name and description</span></span>

<span data-ttu-id="62b84-168">Параметры **displayName** и **description** позволяют идентифицировать определение политики и описать контекст для ее использования.</span><span class="sxs-lookup"><span data-stu-id="62b84-168">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="62b84-169">Правило политики</span><span class="sxs-lookup"><span data-stu-id="62b84-169">Policy rule</span></span>

<span data-ttu-id="62b84-170">Правило политики состоит из блоков **If** и **Then**.</span><span class="sxs-lookup"><span data-stu-id="62b84-170">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="62b84-171">В блоке **If** указываются одно или несколько условий. Они определяют, когда применяется эта политика.</span><span class="sxs-lookup"><span data-stu-id="62b84-171">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="62b84-172">В этих условиях можно использовать логические операторы, чтобы точно определить сценарии для использования политики.</span><span class="sxs-lookup"><span data-stu-id="62b84-172">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span> <span data-ttu-id="62b84-173">В блоке **Then** описываются результаты, которые вступают в силу при соблюдении условий из блока **If**.</span><span class="sxs-lookup"><span data-stu-id="62b84-173">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="62b84-174">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="62b84-174">Logical operators</span></span>
<span data-ttu-id="62b84-175">Ниже перечислены поддерживаемые логические операторы.</span><span class="sxs-lookup"><span data-stu-id="62b84-175">The supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="62b84-176">Оператор **not** инвертирует результат условия.</span><span class="sxs-lookup"><span data-stu-id="62b84-176">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="62b84-177">Оператор **allOf** действует как логическая операция **And**, то есть требует соблюдения всех входящих в него условий.</span><span class="sxs-lookup"><span data-stu-id="62b84-177">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="62b84-178">Оператор **anyOf** действует как логическая операция **Or**, то есть проверяет соблюдение хотя бы одного из входящих в него условий.</span><span class="sxs-lookup"><span data-stu-id="62b84-178">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="62b84-179">Допускается вложение логических операторов.</span><span class="sxs-lookup"><span data-stu-id="62b84-179">You can nest logical operators.</span></span> <span data-ttu-id="62b84-180">В следующем примере представлена операция **not**, вложенная в операцию **allOf**.</span><span class="sxs-lookup"><span data-stu-id="62b84-180">The following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

```json
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
```

### <a name="conditions"></a><span data-ttu-id="62b84-181">Условия</span><span class="sxs-lookup"><span data-stu-id="62b84-181">Conditions</span></span>
<span data-ttu-id="62b84-182">Условие определяет, соответствует ли свойство **field** определенным параметрам.</span><span class="sxs-lookup"><span data-stu-id="62b84-182">The condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="62b84-183">Поддерживаются такие условия:</span><span class="sxs-lookup"><span data-stu-id="62b84-183">The supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="62b84-184">В значении для условия **like** можно использовать подстановочный знак (*).</span><span class="sxs-lookup"><span data-stu-id="62b84-184">When using the **like** condition, you can provide a wildcard (*) in the value.</span></span>

<span data-ttu-id="62b84-185">При использовании условия **match** для цифры используйте `#`, для буквы — `?` и любые другие соответствующие символы.</span><span class="sxs-lookup"><span data-stu-id="62b84-185">When using the **match** condition, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span></span> <span data-ttu-id="62b84-186">Примеры приведены в разделе [Применение политик ресурсов для имен и текста](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="62b84-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="62b84-187">Поля</span><span class="sxs-lookup"><span data-stu-id="62b84-187">Fields</span></span>
<span data-ttu-id="62b84-188">Условия создаются на основе полей.</span><span class="sxs-lookup"><span data-stu-id="62b84-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="62b84-189">Поле представляет свойства в полезных данных запроса ресурса, используемые для описания состояния ресурса.</span><span class="sxs-lookup"><span data-stu-id="62b84-189">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="62b84-190">Поддерживаются следующие поля.</span><span class="sxs-lookup"><span data-stu-id="62b84-190">The following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="62b84-191">Список псевдонимов свойств указан в разделе [Псевдонимы](#aliases).</span><span class="sxs-lookup"><span data-stu-id="62b84-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="62b84-192">Результат</span><span class="sxs-lookup"><span data-stu-id="62b84-192">Effect</span></span>
<span data-ttu-id="62b84-193">Политика поддерживает три типа результатов — `deny`, `audit` и `append`.</span><span class="sxs-lookup"><span data-stu-id="62b84-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="62b84-194">**deny** создает событие в журнале аудита и отклоняет запрос.</span><span class="sxs-lookup"><span data-stu-id="62b84-194">**Deny** generates an event in the audit log and fails the request</span></span>
* <span data-ttu-id="62b84-195">**audit** создает событие в журнале аудита, но выполняет запрос.</span><span class="sxs-lookup"><span data-stu-id="62b84-195">**Audit** generates a warning event in audit log but does not fail the request</span></span>
* <span data-ttu-id="62b84-196">**append** добавляет в запрос некоторый набор полей.</span><span class="sxs-lookup"><span data-stu-id="62b84-196">**Append** adds the defined set of fields to the request</span></span> 

<span data-ttu-id="62b84-197">Для типа **append**необходимо указать следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="62b84-197">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

<span data-ttu-id="62b84-198">Значением может быть строка или объект формата JSON.</span><span class="sxs-lookup"><span data-stu-id="62b84-198">The value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="62b84-199">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="62b84-199">Aliases</span></span>

<span data-ttu-id="62b84-200">Псевдонимы свойств позволяют обращаться к определенным свойствам для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="62b84-200">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="62b84-201">Псевдонимы позволяют ограничить значения или условия, разрешенные для свойства ресурса.</span><span class="sxs-lookup"><span data-stu-id="62b84-201">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="62b84-202">Каждый псевдоним сопоставляется с путями в разных версиях API для заданного типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="62b84-202">Each alias maps to paths in different API versions for a given resource type.</span></span> <span data-ttu-id="62b84-203">Во время оценки политики модуль политики получает путь свойства для этой версии API.</span><span class="sxs-lookup"><span data-stu-id="62b84-203">During policy evaluation, the policy engine gets the property path for that API version.</span></span>

<span data-ttu-id="62b84-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="62b84-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="62b84-205">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-205">Alias</span></span> | <span data-ttu-id="62b84-206">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="62b84-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="62b84-208">Указывает, включен ли на сервере Redis порт без поддержки SSL (6379).</span><span class="sxs-lookup"><span data-stu-id="62b84-208">Set whether the non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="62b84-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="62b84-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="62b84-210">Задает число сегментов, создаваемых в кэше кластера уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="62b84-210">Set the number of shards to be created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="62b84-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="62b84-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="62b84-212">Задает размер развертываемого кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="62b84-212">Set the size of the Redis cache to deploy.</span></span>  |
| <span data-ttu-id="62b84-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="62b84-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="62b84-214">Задает используемое семейство SKU.</span><span class="sxs-lookup"><span data-stu-id="62b84-214">Set the SKU family to use.</span></span> |
| <span data-ttu-id="62b84-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="62b84-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="62b84-216">Задает тип развертываемого кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="62b84-216">Set the type of Redis Cache to deploy.</span></span> |

<span data-ttu-id="62b84-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="62b84-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="62b84-218">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-218">Alias</span></span> | <span data-ttu-id="62b84-219">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="62b84-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="62b84-221">Задает имя ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="62b84-221">Set the name of the pricing tier.</span></span> |

<span data-ttu-id="62b84-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="62b84-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="62b84-223">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-223">Alias</span></span> | <span data-ttu-id="62b84-224">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="62b84-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="62b84-226">Задает предложение образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-226">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="62b84-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="62b84-228">Задает издатель образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-228">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="62b84-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="62b84-230">Задает номер SKU образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-230">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="62b84-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="62b84-232">Задает версию образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-232">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |


<span data-ttu-id="62b84-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="62b84-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="62b84-234">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-234">Alias</span></span> | <span data-ttu-id="62b84-235">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="62b84-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="62b84-237">Задайте идентификатор образа, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-237">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="62b84-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="62b84-239">Задает предложение образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-239">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="62b84-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="62b84-241">Задает издатель образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-241">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="62b84-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="62b84-243">Задает номер SKU образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-243">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="62b84-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="62b84-245">Задает версию образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-245">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="62b84-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="62b84-247">Указывает, используется ли для образа или диска локальная лицензия.</span><span class="sxs-lookup"><span data-stu-id="62b84-247">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="62b84-248">Это значение используется только для образов, содержащих операционную систему Windows Server.</span><span class="sxs-lookup"><span data-stu-id="62b84-248">This value is only used for images that contain the Windows Server operating system.</span></span>  |
| <span data-ttu-id="62b84-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="62b84-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="62b84-250">Задает предложение образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-250">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="62b84-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="62b84-252">Задает издатель образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-252">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="62b84-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="62b84-254">Задает номер SKU образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-254">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="62b84-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="62b84-256">Задает версию образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-256">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="62b84-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="62b84-258">Задает универсальный код ресурса (URI) виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="62b84-258">Set the vhd URI.</span></span> |
| <span data-ttu-id="62b84-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="62b84-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="62b84-260">Задайте размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-260">Set the size of the virtual machine.</span></span> |

<span data-ttu-id="62b84-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="62b84-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="62b84-262">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-262">Alias</span></span> | <span data-ttu-id="62b84-263">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="62b84-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="62b84-265">Задает имя издателя расширения.</span><span class="sxs-lookup"><span data-stu-id="62b84-265">Set the name of the extension’s publisher.</span></span> |
| <span data-ttu-id="62b84-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="62b84-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="62b84-267">Задает тип расширения.</span><span class="sxs-lookup"><span data-stu-id="62b84-267">Set the type of extension.</span></span> |
| <span data-ttu-id="62b84-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="62b84-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="62b84-269">Задает версию расширения.</span><span class="sxs-lookup"><span data-stu-id="62b84-269">Set the version of the extension.</span></span> |

<span data-ttu-id="62b84-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="62b84-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="62b84-271">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-271">Alias</span></span> | <span data-ttu-id="62b84-272">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="62b84-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="62b84-274">Задайте идентификатор образа, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-274">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="62b84-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="62b84-276">Задает предложение образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-276">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="62b84-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="62b84-278">Задает издатель образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-278">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="62b84-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="62b84-280">Задает номер SKU образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-280">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="62b84-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="62b84-282">Задает версию образа платформы или образа Marketplace, используемого для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62b84-282">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="62b84-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="62b84-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="62b84-284">Указывает, используется ли для образа или диска локальная лицензия.</span><span class="sxs-lookup"><span data-stu-id="62b84-284">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="62b84-285">Это значение используется только для образов, содержащих операционную систему Windows Server.</span><span class="sxs-lookup"><span data-stu-id="62b84-285">This value is only used for images that contain the Windows Server operating system.</span></span> |
| <span data-ttu-id="62b84-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="62b84-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="62b84-287">Задает префикс имени компьютера для всех виртуальных машин в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="62b84-287">Set the computer name prefix for all  the virtual machines in the scale set.</span></span> |
| <span data-ttu-id="62b84-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="62b84-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="62b84-289">Задает универсальный код ресурса (URI) большого двоичного объекта для пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="62b84-289">Set the blob URI for user image.</span></span> |
| <span data-ttu-id="62b84-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="62b84-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="62b84-291">Задает URL-адреса контейнеров, которые используются для хранения ОС для масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="62b84-291">Set the container URLs that are used to store operating system disks for the scale set.</span></span> |
| <span data-ttu-id="62b84-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="62b84-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="62b84-293">Задает размер виртуальных машин в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="62b84-293">Set the size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="62b84-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="62b84-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="62b84-295">Задает уровень виртуальных машин в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="62b84-295">Set the tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="62b84-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="62b84-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="62b84-297">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-297">Alias</span></span> | <span data-ttu-id="62b84-298">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="62b84-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="62b84-300">Задает размер шлюза.</span><span class="sxs-lookup"><span data-stu-id="62b84-300">Set the size of the gateway.</span></span> |

<span data-ttu-id="62b84-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="62b84-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="62b84-302">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-302">Alias</span></span> | <span data-ttu-id="62b84-303">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="62b84-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="62b84-305">Задает тип шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="62b84-305">Set the type of this virtual network gateway.</span></span> |
| <span data-ttu-id="62b84-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="62b84-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="62b84-307">Задает номера SKU шлюза.</span><span class="sxs-lookup"><span data-stu-id="62b84-307">Set the gateway SKU name.</span></span> |

<span data-ttu-id="62b84-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="62b84-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="62b84-309">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-309">Alias</span></span> | <span data-ttu-id="62b84-310">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="62b84-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="62b84-312">Задает версию сервера.</span><span class="sxs-lookup"><span data-stu-id="62b84-312">Set the version of the server.</span></span> |

<span data-ttu-id="62b84-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="62b84-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="62b84-314">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-314">Alias</span></span> | <span data-ttu-id="62b84-315">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="62b84-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="62b84-317">Задает выпуск базы данных.</span><span class="sxs-lookup"><span data-stu-id="62b84-317">Set the edition of the database.</span></span> |
| <span data-ttu-id="62b84-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="62b84-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="62b84-319">Задает имя эластичного пула, в котором размещена база данных.</span><span class="sxs-lookup"><span data-stu-id="62b84-319">Set the name of the elastic pool the database is in.</span></span> |
| <span data-ttu-id="62b84-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="62b84-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="62b84-321">Задает идентификатор настроенного целевого уровня обслуживания для базы данных.</span><span class="sxs-lookup"><span data-stu-id="62b84-321">Set the configured service level objective ID of the database.</span></span> |
| <span data-ttu-id="62b84-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="62b84-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="62b84-323">Задает имя настроенного целевого уровня обслуживания для базы данных.</span><span class="sxs-lookup"><span data-stu-id="62b84-323">Set the name of the configured service level objective of the database.</span></span>  |

<span data-ttu-id="62b84-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="62b84-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="62b84-325">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-325">Alias</span></span> | <span data-ttu-id="62b84-326">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="62b84-327">servers/elasticpools</span></span> | <span data-ttu-id="62b84-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="62b84-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="62b84-329">Задает совокупное число общих единиц DTU для эластичного пула базы данных.</span><span class="sxs-lookup"><span data-stu-id="62b84-329">Set the total shared DTU for the database elastic pool.</span></span> |
| <span data-ttu-id="62b84-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="62b84-330">servers/elasticpools</span></span> | <span data-ttu-id="62b84-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="62b84-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="62b84-332">Задает выпуск эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="62b84-332">Set the edition of the elastic pool.</span></span> |

<span data-ttu-id="62b84-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="62b84-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="62b84-334">Alias</span><span class="sxs-lookup"><span data-stu-id="62b84-334">Alias</span></span> | <span data-ttu-id="62b84-335">Описание</span><span class="sxs-lookup"><span data-stu-id="62b84-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62b84-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="62b84-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="62b84-337">Задает уровень доступа, используемый для выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="62b84-337">Set the access tier used for billing.</span></span> |
| <span data-ttu-id="62b84-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="62b84-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="62b84-339">Задает имя SKU.</span><span class="sxs-lookup"><span data-stu-id="62b84-339">Set the SKU name.</span></span> |
| <span data-ttu-id="62b84-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="62b84-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="62b84-341">Указывает, шифрует ли служба данные, хранящиеся в службе хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="62b84-341">Set whether the service encrypts the data as it is stored in the blob storage service.</span></span> |
| <span data-ttu-id="62b84-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="62b84-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="62b84-343">Указывает, шифрует ли служба данные, хранящиеся в службе хранилища файлов.</span><span class="sxs-lookup"><span data-stu-id="62b84-343">Set whether the service encrypts the data as it is stored in the file storage service.</span></span> |
| <span data-ttu-id="62b84-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="62b84-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="62b84-345">Задает имя SKU.</span><span class="sxs-lookup"><span data-stu-id="62b84-345">Set the SKU name.</span></span> |
| <span data-ttu-id="62b84-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="62b84-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="62b84-347">Позволяет разрешить только передачу трафика HTTPS в службу хранилища.</span><span class="sxs-lookup"><span data-stu-id="62b84-347">Set to allow only https traffic to storage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="62b84-348">Примеры политик</span><span class="sxs-lookup"><span data-stu-id="62b84-348">Policy examples</span></span>

<span data-ttu-id="62b84-349">Следующие статьи содержат примеры политик.</span><span class="sxs-lookup"><span data-stu-id="62b84-349">The following topics contain policy examples:</span></span>

* <span data-ttu-id="62b84-350">Примеры политик для тегов см. в статье [Apply resource policies for tags](resource-manager-policy-tags.md) (Применение политик ресурсов для тегов).</span><span class="sxs-lookup"><span data-stu-id="62b84-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="62b84-351">Примеры именования и шаблоны текста приведены в разделе [Применение политик ресурсов для имен и текста](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="62b84-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="62b84-352">Примеры политик для хранения см. в статье [Применение политик ресурсов Azure для учетных записей хранения](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="62b84-352">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="62b84-353">Примеры политик для виртуальных машин есть в статьях о применении политик к виртуальным машинам Azure Resource Manager [для Linux](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) и [для Windows](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62b84-353">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="62b84-354">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62b84-354">Next steps</span></span>
* <span data-ttu-id="62b84-355">Определив правило политики, назначьте эту политику для области.</span><span class="sxs-lookup"><span data-stu-id="62b84-355">After defining a policy rule, assign it to a scope.</span></span> <span data-ttu-id="62b84-356">Сведения о назначении политик с помощью портала см. в статье [Назначение политик ресурсов и управление ими с помощью портала Azure](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="62b84-356">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="62b84-357">Сведения о назначении политик с помощью REST API, PowerShell или Azure CLI см. в статье [Назначение политик ресурсов и управление ими](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="62b84-357">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="62b84-358">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="62b84-358">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="62b84-359">Схема политики опубликована на странице [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="62b84-359">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

