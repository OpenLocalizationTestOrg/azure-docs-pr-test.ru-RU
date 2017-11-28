---
title: "политики ресурсов aaaAzure | Документы Microsoft"
description: "Описывает, каким образом toouse диспетчера ресурсов Azure политики tooensure согласованное ресурсов задано во время развертывания. Политики могут применяться для групп hello подписка или ресурс."
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
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="27e68-104">Общие сведения о политике ресурсов</span><span class="sxs-lookup"><span data-stu-id="27e68-104">Resource policy overview</span></span>
<span data-ttu-id="27e68-105">Политики ресурсов позволяют tooestablish соглашения для ресурсов в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="27e68-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="27e68-106">Это соглашения помогут вам контролировать расходы и управлять ресурсами.</span><span class="sxs-lookup"><span data-stu-id="27e68-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="27e68-107">Например, можно указать, что разрешены только определенные типы виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="27e68-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="27e68-108">Кроме того, можно требовать наличие определенного тега для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="27e68-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="27e68-109">Политики наследуются всеми дочерними ресурсами.</span><span class="sxs-lookup"><span data-stu-id="27e68-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="27e68-110">Таким образом Если политика не применяется tooa группы ресурсов, это применимо tooall hello ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="27e68-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="27e68-111">Существует два toounderstand основные понятия о политиках.</span><span class="sxs-lookup"><span data-stu-id="27e68-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="27e68-112">Определение политики — описывается при hello включена политика и какие действия tootake</span><span class="sxs-lookup"><span data-stu-id="27e68-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="27e68-113">Назначение политики - применить область tooa политики определения hello (подписка или группа ресурсов)</span><span class="sxs-lookup"><span data-stu-id="27e68-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="27e68-114">В этой статье рассматривается только определение политики.</span><span class="sxs-lookup"><span data-stu-id="27e68-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="27e68-115">Сведения о назначении политики см. в разделе [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md) или [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="27e68-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="27e68-116">Политики оцениваются при создании и обновлении ресурсов (операции PUT и PATCH).</span><span class="sxs-lookup"><span data-stu-id="27e68-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="27e68-117">В настоящее время политики не вычисляет типы ресурсов, которые не поддерживают теги, тип и расположение, например тип ресурса Microsoft.Resources/deployments hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="27e68-118">Их поддержка будет добавлена в будущем.</span><span class="sxs-lookup"><span data-stu-id="27e68-118">This support will be added at a future time.</span></span> <span data-ttu-id="27e68-119">проблемы совместимости с предыдущими версиями tooavoid, следует явно указать тип при создании политики.</span><span class="sxs-lookup"><span data-stu-id="27e68-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="27e68-120">Например, политика тегов, которая не указывает типы, применяется для всех типов.</span><span class="sxs-lookup"><span data-stu-id="27e68-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="27e68-121">В этом случае шаблона-развертывания может завершиться ошибкой, если вложенные ресурс, который не поддерживает теги и тип ресурса развертывания hello добавлен toopolicy оценки.</span><span class="sxs-lookup"><span data-stu-id="27e68-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="27e68-122">Чем это отличается от управления доступом на основе ролей?</span><span class="sxs-lookup"><span data-stu-id="27e68-122">How is it different from RBAC?</span></span>
<span data-ttu-id="27e68-123">Существует ряд ключевых различий между политиками и управлением доступом на основе ролей (RBAC).</span><span class="sxs-lookup"><span data-stu-id="27e68-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="27e68-124">RBAC определяет действия **пользователя** в различных областях.</span><span class="sxs-lookup"><span data-stu-id="27e68-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="27e68-125">Например вы добавляются toohello роль участника для группы ресурсов в области hello требуемого для внесения изменений группы ресурсов toothat.</span><span class="sxs-lookup"><span data-stu-id="27e68-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="27e68-126">Политика определяет свойства **ресурсов** во время их развертывания.</span><span class="sxs-lookup"><span data-stu-id="27e68-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="27e68-127">Например через политики, можно управлять hello типы ресурсов, которые могут быть подготовлены.</span><span class="sxs-lookup"><span data-stu-id="27e68-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="27e68-128">Или вы можете ограничить hello расположения, в которых можно подготовить ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="27e68-129">В отличие от RBAC, политика представляет собой систему разрешения по умолчанию и явного запрета.</span><span class="sxs-lookup"><span data-stu-id="27e68-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="27e68-130">политики toouse, вы должны пройти проверку подлинности через RBAC.</span><span class="sxs-lookup"><span data-stu-id="27e68-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="27e68-131">В частности, для учетной записи должны быть предоставлены:</span><span class="sxs-lookup"><span data-stu-id="27e68-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="27e68-132">`Microsoft.Authorization/policydefinitions/write`разрешение toodefine политики</span><span class="sxs-lookup"><span data-stu-id="27e68-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="27e68-133">`Microsoft.Authorization/policyassignments/write`разрешение tooassign политики</span><span class="sxs-lookup"><span data-stu-id="27e68-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="27e68-134">Эти разрешения не включаются в hello **участника** роли.</span><span class="sxs-lookup"><span data-stu-id="27e68-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="27e68-135">Встроенные политики</span><span class="sxs-lookup"><span data-stu-id="27e68-135">Built-in policies</span></span>

<span data-ttu-id="27e68-136">Azure предоставляет некоторые определения встроенных политик, которые может сократить число hello политик имеют toodefine.</span><span class="sxs-lookup"><span data-stu-id="27e68-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="27e68-137">Перед продолжением определения политик, следует ли встроенные политики уже предоставляет определение hello, что нужно.</span><span class="sxs-lookup"><span data-stu-id="27e68-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="27e68-138">используются Hello встроенная политика определения.</span><span class="sxs-lookup"><span data-stu-id="27e68-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="27e68-139">Allowed locations;</span><span class="sxs-lookup"><span data-stu-id="27e68-139">Allowed locations</span></span>
* <span data-ttu-id="27e68-140">Допустимые типы ресурсов</span><span class="sxs-lookup"><span data-stu-id="27e68-140">Allowed resource types</span></span>
* <span data-ttu-id="27e68-141">Allowed storage account SKUs;</span><span class="sxs-lookup"><span data-stu-id="27e68-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="27e68-142">Allowed virtual machine SKUs;</span><span class="sxs-lookup"><span data-stu-id="27e68-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="27e68-143">Apply tag and default value;</span><span class="sxs-lookup"><span data-stu-id="27e68-143">Apply tag and default value</span></span>
* <span data-ttu-id="27e68-144">Enforce tag and value;</span><span class="sxs-lookup"><span data-stu-id="27e68-144">Enforce tag and value</span></span>
* <span data-ttu-id="27e68-145">Not allowed resource types;</span><span class="sxs-lookup"><span data-stu-id="27e68-145">Not allowed resource types</span></span>
* <span data-ttu-id="27e68-146">Require SQL Server version 12.0;</span><span class="sxs-lookup"><span data-stu-id="27e68-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="27e68-147">Require storage account encryption.</span><span class="sxs-lookup"><span data-stu-id="27e68-147">Require storage account encryption</span></span>

<span data-ttu-id="27e68-148">Можно назначить любой из этих политик через hello [портала](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), или [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="27e68-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="27e68-149">Структура определения политики</span><span class="sxs-lookup"><span data-stu-id="27e68-149">Policy definition structure</span></span>
<span data-ttu-id="27e68-150">Использовании JSON toocreate определения политики.</span><span class="sxs-lookup"><span data-stu-id="27e68-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="27e68-151">Определение политики Hello содержит элементы для:</span><span class="sxs-lookup"><span data-stu-id="27e68-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="27e68-152">parameters</span><span class="sxs-lookup"><span data-stu-id="27e68-152">parameters</span></span>
* <span data-ttu-id="27e68-153">display name</span><span class="sxs-lookup"><span data-stu-id="27e68-153">display name</span></span>
* <span data-ttu-id="27e68-154">description</span><span class="sxs-lookup"><span data-stu-id="27e68-154">description</span></span>
* <span data-ttu-id="27e68-155">policy rule</span><span class="sxs-lookup"><span data-stu-id="27e68-155">policy rule</span></span>
  * <span data-ttu-id="27e68-156">logical evaluation</span><span class="sxs-lookup"><span data-stu-id="27e68-156">logical evaluation</span></span>
  * <span data-ttu-id="27e68-157">effect</span><span class="sxs-lookup"><span data-stu-id="27e68-157">effect</span></span>

<span data-ttu-id="27e68-158">Следующий пример Hello показано политику, которая ограничивает, где развернуты ресурсы.</span><span class="sxs-lookup"><span data-stu-id="27e68-158">hello following example shows a policy that limits where resources are deployed:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="27e68-159">Параметры</span><span class="sxs-lookup"><span data-stu-id="27e68-159">Parameters</span></span>
<span data-ttu-id="27e68-160">С помощью параметров помогает упростить управление политики за счет сокращения числа hello определения политик.</span><span class="sxs-lookup"><span data-stu-id="27e68-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="27e68-161">Определить политику для свойства ресурса (например, ограничение расположения hello, где может развертываться ресурсы) и включения параметров в определении hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="27e68-162">Затем можно повторно использовать определения политик для различных сценариев, передавая различные значения (например, указать один набор расположений для подписки) при назначении политики hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="27e68-163">А параметры объявляются при создании определения политики.</span><span class="sxs-lookup"><span data-stu-id="27e68-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="27e68-164">Тип Hello параметра может быть строка или массив.</span><span class="sxs-lookup"><span data-stu-id="27e68-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="27e68-165">Свойство метаданных Hello используется для средств, таких как Azure портала toodisplay понятные сведения.</span><span class="sxs-lookup"><span data-stu-id="27e68-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="27e68-166">В правиле политики hello параметры ссылок с hello, используя синтаксис:</span><span class="sxs-lookup"><span data-stu-id="27e68-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="27e68-167">Отображаемое имя и описание</span><span class="sxs-lookup"><span data-stu-id="27e68-167">Display name and description</span></span>

<span data-ttu-id="27e68-168">Использовать hello **displayName** и **описание** tooidentify hello определения политики и обеспечения при использовании контекста.</span><span class="sxs-lookup"><span data-stu-id="27e68-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="27e68-169">Правило политики</span><span class="sxs-lookup"><span data-stu-id="27e68-169">Policy rule</span></span>

<span data-ttu-id="27e68-170">правило политики Hello состоит из **Если** и **затем** блоков.</span><span class="sxs-lookup"><span data-stu-id="27e68-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="27e68-171">В hello **Если** блока, можно определить одно или несколько условий, указывающие, когда применяется политика hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="27e68-172">Логические операторы toothese условия можно применить tooprecisely определить hello сценарий для политики.</span><span class="sxs-lookup"><span data-stu-id="27e68-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="27e68-173">В hello **затем** блок, определяется hello эффект, который происходит, когда hello **Если** условия будут выполнены.</span><span class="sxs-lookup"><span data-stu-id="27e68-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

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

### <a name="logical-operators"></a><span data-ttu-id="27e68-174">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="27e68-174">Logical operators</span></span>
<span data-ttu-id="27e68-175">Hello поддерживается логическим операторам относятся:</span><span class="sxs-lookup"><span data-stu-id="27e68-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="27e68-176">Hello **не** синтаксис Инвертирует результат hello hello условия.</span><span class="sxs-lookup"><span data-stu-id="27e68-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="27e68-177">Hello **все** синтаксис (аналогично toohello логических **и** операции) требует true toobe все условия.</span><span class="sxs-lookup"><span data-stu-id="27e68-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="27e68-178">Hello **anyOf** синтаксис (аналогично toohello логических **или** операции) требует одного или нескольких toobe условия значение true.</span><span class="sxs-lookup"><span data-stu-id="27e68-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="27e68-179">Допускается вложение логических операторов.</span><span class="sxs-lookup"><span data-stu-id="27e68-179">You can nest logical operators.</span></span> <span data-ttu-id="27e68-180">Следующий пример показывает Hello **не** операции, вложенные в **все** операции.</span><span class="sxs-lookup"><span data-stu-id="27e68-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

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

### <a name="conditions"></a><span data-ttu-id="27e68-181">Условия</span><span class="sxs-lookup"><span data-stu-id="27e68-181">Conditions</span></span>
<span data-ttu-id="27e68-182">условие Hello ли **поле** заданным критериям.</span><span class="sxs-lookup"><span data-stu-id="27e68-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="27e68-183">Hello поддерживается условиям относятся:</span><span class="sxs-lookup"><span data-stu-id="27e68-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="27e68-184">При использовании hello **как** условие, можно указать подстановочный знак (*) в значение hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="27e68-185">При использовании hello **соответствует** условия, укажите `#` toorepresent цифры, `?` для письма и любой другой символ toorepresent, фактический символ.</span><span class="sxs-lookup"><span data-stu-id="27e68-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="27e68-186">Примеры приведены в разделе [Применение политик ресурсов для имен и текста](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="27e68-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="27e68-187">Поля</span><span class="sxs-lookup"><span data-stu-id="27e68-187">Fields</span></span>
<span data-ttu-id="27e68-188">Условия создаются на основе полей.</span><span class="sxs-lookup"><span data-stu-id="27e68-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="27e68-189">Поле представляет свойства в полезных данных запроса hello ресурсов, используемых toodescribe hello состояние hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="27e68-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="27e68-190">поддерживаются следующие поля Hello:</span><span class="sxs-lookup"><span data-stu-id="27e68-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="27e68-191">Список псевдонимов свойств указан в разделе [Псевдонимы](#aliases).</span><span class="sxs-lookup"><span data-stu-id="27e68-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="27e68-192">Результат</span><span class="sxs-lookup"><span data-stu-id="27e68-192">Effect</span></span>
<span data-ttu-id="27e68-193">Политика поддерживает три типа результатов — `deny`, `audit` и `append`.</span><span class="sxs-lookup"><span data-stu-id="27e68-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="27e68-194">**Запретить** создает событие в журнал аудита hello и происходит сбой запроса hello</span><span class="sxs-lookup"><span data-stu-id="27e68-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="27e68-195">**Аудит** приводит к возникновению события предупреждения в журнал аудита, но не позволяет hello запроса</span><span class="sxs-lookup"><span data-stu-id="27e68-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="27e68-196">**Добавление** добавляет набор hello определенные поля toohello запроса</span><span class="sxs-lookup"><span data-stu-id="27e68-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="27e68-197">Для **append**, необходимо предоставить hello, приведенные ниже сведения:</span><span class="sxs-lookup"><span data-stu-id="27e68-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="27e68-198">Hello значение может быть строка или объект формата JSON.</span><span class="sxs-lookup"><span data-stu-id="27e68-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="27e68-199">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="27e68-199">Aliases</span></span>

<span data-ttu-id="27e68-200">Используйте свойство псевдонимы tooaccess определенных свойств для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="27e68-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="27e68-201">Псевдонимы включают toorestrict, какие значения или условия являются допустимыми для свойства ресурса.</span><span class="sxs-lookup"><span data-stu-id="27e68-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="27e68-202">Каждый псевдоним сопоставляет toopaths в различных версиях API для заданного типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="27e68-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="27e68-203">Во время оценки политики hello модуль политики возвращает путь к свойству hello для этой версии API.</span><span class="sxs-lookup"><span data-stu-id="27e68-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="27e68-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="27e68-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="27e68-205">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-205">Alias</span></span> | <span data-ttu-id="27e68-206">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="27e68-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="27e68-208">Задать ли сервер Redis hello не ssl-порта (6379) включен.</span><span class="sxs-lookup"><span data-stu-id="27e68-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="27e68-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="27e68-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="27e68-210">Задайте количество hello toobe сегментов, созданные на кластер кэша Premium.</span><span class="sxs-lookup"><span data-stu-id="27e68-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="27e68-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="27e68-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="27e68-212">Задать размер hello toodeploy кэша Redis hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="27e68-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="27e68-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="27e68-214">Задать семейства toouse hello SKU.</span><span class="sxs-lookup"><span data-stu-id="27e68-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="27e68-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="27e68-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="27e68-216">Выбор типа hello toodeploy кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="27e68-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="27e68-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="27e68-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="27e68-218">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-218">Alias</span></span> | <span data-ttu-id="27e68-219">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="27e68-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="27e68-221">Имя набора hello hello ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="27e68-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="27e68-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="27e68-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="27e68-223">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-223">Alias</span></span> | <span data-ttu-id="27e68-224">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="27e68-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="27e68-226">Предложение SET hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="27e68-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="27e68-228">Набор hello издатель образа платформы hello или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="27e68-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="27e68-230">Набор hello номер SKU образа платформы hello или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="27e68-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="27e68-232">Версия набора hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="27e68-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="27e68-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="27e68-234">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-234">Alias</span></span> | <span data-ttu-id="27e68-235">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="27e68-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="27e68-237">Задать идентификатор hello hello изображение, используемое toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="27e68-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="27e68-239">Предложение SET hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="27e68-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="27e68-241">Набор hello издатель образа платформы hello или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="27e68-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="27e68-243">Набор hello номер SKU образа платформы hello или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="27e68-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="27e68-245">Версия набора hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="27e68-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="27e68-247">Заданы, hello образа или диска лицензированного в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="27e68-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="27e68-248">Это значение используется только для образов, содержащих hello ОС Windows Server.</span><span class="sxs-lookup"><span data-stu-id="27e68-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="27e68-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="27e68-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="27e68-250">Предложение SET hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="27e68-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="27e68-252">Набор hello издатель образа платформы hello или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="27e68-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="27e68-254">Набор hello номер SKU образа платформы hello или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="27e68-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="27e68-256">Версия набора hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="27e68-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="27e68-258">Задайте hello vhd URI.</span><span class="sxs-lookup"><span data-stu-id="27e68-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="27e68-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="27e68-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="27e68-260">Задайте размер hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="27e68-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="27e68-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="27e68-262">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-262">Alias</span></span> | <span data-ttu-id="27e68-263">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="27e68-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="27e68-265">Задайте имя издателя расширения hello hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="27e68-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="27e68-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="27e68-267">Задайте тип hello расширения.</span><span class="sxs-lookup"><span data-stu-id="27e68-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="27e68-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="27e68-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="27e68-269">Задает версию расширения hello hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="27e68-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="27e68-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="27e68-271">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-271">Alias</span></span> | <span data-ttu-id="27e68-272">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="27e68-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="27e68-274">Задать идентификатор hello hello изображение, используемое toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="27e68-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="27e68-276">Предложение SET hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="27e68-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="27e68-278">Набор hello издатель образа платформы hello или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="27e68-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="27e68-280">Набор hello номер SKU образа платформы hello или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="27e68-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="27e68-282">Версия набора hello hello платформы образа или образа marketplace используется toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27e68-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="27e68-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="27e68-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="27e68-284">Заданы, hello образа или диска лицензированного в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="27e68-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="27e68-285">Это значение используется только для образов, содержащих hello ОС Windows Server.</span><span class="sxs-lookup"><span data-stu-id="27e68-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="27e68-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="27e68-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="27e68-287">Задать hello с префиксом имени компьютера для всех виртуальных машин hello в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="27e68-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="27e68-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="27e68-289">Набор hello URI большого двоичного объекта для пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="27e68-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="27e68-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="27e68-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="27e68-291">Набор hello контейнера URL-адреса, используемые toostore дисков операционной системы для набора масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="27e68-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="27e68-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="27e68-293">Установите размер hello виртуальных машин в наборе масштабирования.</span><span class="sxs-lookup"><span data-stu-id="27e68-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="27e68-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="27e68-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="27e68-295">Задайте уровень hello виртуальных машин в наборе масштабирования.</span><span class="sxs-lookup"><span data-stu-id="27e68-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="27e68-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="27e68-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="27e68-297">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-297">Alias</span></span> | <span data-ttu-id="27e68-298">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="27e68-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="27e68-300">Задайте размер hello hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="27e68-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="27e68-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="27e68-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="27e68-302">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-302">Alias</span></span> | <span data-ttu-id="27e68-303">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="27e68-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="27e68-305">Задайте тип hello этого шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="27e68-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="27e68-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="27e68-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="27e68-307">Задайте имя SKU шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="27e68-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="27e68-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="27e68-309">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-309">Alias</span></span> | <span data-ttu-id="27e68-310">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="27e68-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="27e68-312">Задает версию сервера hello hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="27e68-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="27e68-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="27e68-314">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-314">Alias</span></span> | <span data-ttu-id="27e68-315">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="27e68-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="27e68-317">Установите выпуск hello hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="27e68-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="27e68-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="27e68-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="27e68-319">Имя набора hello hello эластичного пула hello, базы данных находится в.</span><span class="sxs-lookup"><span data-stu-id="27e68-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="27e68-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="27e68-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="27e68-321">Задайте настройки hello уровня идентификатор цели службы hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="27e68-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="27e68-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="27e68-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="27e68-323">Имя набора hello hello настроить цель уровня обслуживания базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="27e68-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="27e68-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="27e68-325">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-325">Alias</span></span> | <span data-ttu-id="27e68-326">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="27e68-327">servers/elasticpools</span></span> | <span data-ttu-id="27e68-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="27e68-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="27e68-329">Всего hello набор общих DTU для эластичного пула hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="27e68-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="27e68-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="27e68-330">servers/elasticpools</span></span> | <span data-ttu-id="27e68-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="27e68-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="27e68-332">Установите выпуск hello hello эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="27e68-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="27e68-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="27e68-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="27e68-334">Alias</span><span class="sxs-lookup"><span data-stu-id="27e68-334">Alias</span></span> | <span data-ttu-id="27e68-335">Описание</span><span class="sxs-lookup"><span data-stu-id="27e68-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="27e68-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="27e68-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="27e68-337">Уровень доступа к hello набор используется для выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="27e68-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="27e68-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="27e68-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="27e68-339">Задайте имя SKU hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="27e68-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="27e68-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="27e68-341">Задается ли служба hello шифрует данные, hello, хранящегося в службе хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="27e68-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="27e68-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="27e68-343">Задается ли служба hello шифрует данные, hello, хранящегося в службе хранилища файла hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="27e68-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="27e68-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="27e68-345">Задайте имя SKU hello.</span><span class="sxs-lookup"><span data-stu-id="27e68-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="27e68-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="27e68-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="27e68-347">Установите службы toostorage трафика tooallow только https.</span><span class="sxs-lookup"><span data-stu-id="27e68-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="27e68-348">Примеры политик</span><span class="sxs-lookup"><span data-stu-id="27e68-348">Policy examples</span></span>

<span data-ttu-id="27e68-349">Привет, следующие разделы содержат примеры политики:</span><span class="sxs-lookup"><span data-stu-id="27e68-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="27e68-350">Примеры политик для тегов см. в статье [Apply resource policies for tags](resource-manager-policy-tags.md) (Применение политик ресурсов для тегов).</span><span class="sxs-lookup"><span data-stu-id="27e68-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="27e68-351">Примеры именования и шаблоны текста приведены в разделе [Применение политик ресурсов для имен и текста](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="27e68-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="27e68-352">Примеры политик хранения см. в разделе [применения учетных записей ресурсов политики toostorage](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="27e68-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="27e68-353">Примеры политик виртуальной машины в разделе [применить tooLinux политики ресурсов виртуальных машин](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) и [применить tooWindows политики ресурсов виртуальных машин](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="27e68-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="27e68-354">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27e68-354">Next steps</span></span>
* <span data-ttu-id="27e68-355">После определения правила политики, назначьте его tooa область.</span><span class="sxs-lookup"><span data-stu-id="27e68-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="27e68-356">политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="27e68-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="27e68-357">политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="27e68-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="27e68-358">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="27e68-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="27e68-359">Схема политики Hello опубликованы по адресу [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="27e68-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

