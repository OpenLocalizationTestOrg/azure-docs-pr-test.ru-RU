---
title: "Политики ресурсов Azure для соглашений об именовании | Документация Майкрософт"
description: "В этой статье описываются политики Azure Resource Manager для соглашений об именовании ресурсов."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 51b3519bbba8cb4c768bfdd7dadf92fced434f22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="2c71f-103">Применение политик ресурсов для имен и текста</span><span class="sxs-lookup"><span data-stu-id="2c71f-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="2c71f-104">В этом разделе показано несколько [политик ресурсов](resource-manager-policy.md), которые можно применить для настройки соглашений об именовании и соглашений текста.</span><span class="sxs-lookup"><span data-stu-id="2c71f-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to establish naming and text conventions.</span></span> <span data-ttu-id="2c71f-105">Эти политики обеспечивают согласованность данных в именах ресурсов и в значениях тегов.</span><span class="sxs-lookup"><span data-stu-id="2c71f-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="2c71f-106">Соглашение об именовании с символами подстановки</span><span class="sxs-lookup"><span data-stu-id="2c71f-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="2c71f-107">В следующем примере показано, как использовать подстановочный знак в условии **like**.</span><span class="sxs-lookup"><span data-stu-id="2c71f-107">The following example shows the use of wildcard, which is supported by the **like** condition.</span></span> <span data-ttu-id="2c71f-108">Это условие означает следующее: если имя не соответствует заданному шаблону (namePrefix\*nameSuffix), запрос будет отклонен.</span><span class="sxs-lookup"><span data-stu-id="2c71f-108">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="2c71f-109">Соглашение об именовании с шаблоном</span><span class="sxs-lookup"><span data-stu-id="2c71f-109">Set naming convention with pattern</span></span>

<span data-ttu-id="2c71f-110">Чтобы указать, что имена ресурсов должны соответствовать шаблону, используйте условие match.</span><span class="sxs-lookup"><span data-stu-id="2c71f-110">To specify that resource names match a pattern, use the match condition.</span></span> <span data-ttu-id="2c71f-111">В следующем примере задано, что имена должны начинаться с `contoso` и содержать 6 дополнительных букв:</span><span class="sxs-lookup"><span data-stu-id="2c71f-111">The following example requires names to start with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="2c71f-112">Настройка шаблона даты для значения тега</span><span class="sxs-lookup"><span data-stu-id="2c71f-112">Set date pattern for tag value</span></span>

<span data-ttu-id="2c71f-113">Чтобы задать дату в формате "две цифры — три буквы — четыре цифры", используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="2c71f-113">To require a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="2c71f-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c71f-114">Next steps</span></span>
* <span data-ttu-id="2c71f-115">После определения правила политики (как показано в приведенных выше примерах) необходимо создать определение политики и назначить ей область.</span><span class="sxs-lookup"><span data-stu-id="2c71f-115">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="2c71f-116">Областью может быть подписка, группа ресурсов или ресурс.</span><span class="sxs-lookup"><span data-stu-id="2c71f-116">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="2c71f-117">Сведения о назначении политик с помощью портала см. в статье [Назначение политик ресурсов и управление ими с помощью портала Azure](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c71f-117">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="2c71f-118">Сведения о назначении политик с помощью REST API, PowerShell или Azure CLI см. в статье [Назначение политик ресурсов и управление ими](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="2c71f-118">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="2c71f-119">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="2c71f-119">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

