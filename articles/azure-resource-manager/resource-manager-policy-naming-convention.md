---
title: "политики aaaAzure ресурсов для соглашения об именовании | Документы Microsoft"
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
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="a24e1-103">Применение политик ресурсов для имен и текста</span><span class="sxs-lookup"><span data-stu-id="a24e1-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="a24e1-104">В этом разделе показано несколько [политики ресурсов](resource-manager-policy.md) можно применить tooestablish соглашения об именовании и текста.</span><span class="sxs-lookup"><span data-stu-id="a24e1-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="a24e1-105">Эти политики обеспечивают согласованность данных в именах ресурсов и в значениях тегов.</span><span class="sxs-lookup"><span data-stu-id="a24e1-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="a24e1-106">Соглашение об именовании с символами подстановки</span><span class="sxs-lookup"><span data-stu-id="a24e1-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="a24e1-107">Hello следующем примере показано использование подстановочных знаков, которая поддерживается hello hello **как** условие.</span><span class="sxs-lookup"><span data-stu-id="a24e1-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="a24e1-108">Hello условие указано, что если hello имя соответствовать шаблону упомянутых hello (namePrefix\*nameSuffix) затем отклонить запрос hello:</span><span class="sxs-lookup"><span data-stu-id="a24e1-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

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

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="a24e1-109">Соглашение об именовании с шаблоном</span><span class="sxs-lookup"><span data-stu-id="a24e1-109">Set naming convention with pattern</span></span>

<span data-ttu-id="a24e1-110">toospecify, что ресурс имена которых соответствуют шаблону, используйте hello соответствуют условию.</span><span class="sxs-lookup"><span data-stu-id="a24e1-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="a24e1-111">Hello следующего примера требуется toostart имена с `contoso` и содержать буквы шесть дополнительных:</span><span class="sxs-lookup"><span data-stu-id="a24e1-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

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

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="a24e1-112">Настройка шаблона даты для значения тега</span><span class="sxs-lookup"><span data-stu-id="a24e1-112">Set date pattern for tag value</span></span>

<span data-ttu-id="a24e1-113">toorequire шаблон даты, используйте две цифры, тире, три буквы, тире и четыре цифры:</span><span class="sxs-lookup"><span data-stu-id="a24e1-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a24e1-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a24e1-114">Next steps</span></span>
* <span data-ttu-id="a24e1-115">После определения правила политики (как показано в предыдущих примерах hello), требуется определение политики toocreate hello и назначьте его tooa области.</span><span class="sxs-lookup"><span data-stu-id="a24e1-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="a24e1-116">Hello область может быть подписки, группы ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a24e1-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="a24e1-117">политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a24e1-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="a24e1-118">политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="a24e1-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="a24e1-119">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a24e1-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

