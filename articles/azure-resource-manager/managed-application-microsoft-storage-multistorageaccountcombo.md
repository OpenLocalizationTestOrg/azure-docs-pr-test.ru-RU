---
title: "Элемент пользовательского интерфейса MultiStorageAccountCombo управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo для управляемых приложений Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="f9931-103">Элемент пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="f9931-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="f9931-104">Группа элементов управления для создания нескольких учетных записей хранения с именами, которые начинаются с общего префикса.</span><span class="sxs-lookup"><span data-stu-id="f9931-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="f9931-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f9931-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f9931-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="f9931-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="f9931-108">Схема</span><span class="sxs-lookup"><span data-stu-id="f9931-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="f9931-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="f9931-109">Remarks</span></span>
- <span data-ttu-id="f9931-110">Значение для `defaultValue.prefix` объединяется с одним или несколькими целыми числами для создания последовательности имен учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="f9931-110">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span></span> <span data-ttu-id="f9931-111">Например, если для параметра `defaultValue.prefix` задано значение **foobar**, а для параметра `count` задано значение **2**, тогда создаются имена учетной записи хранения **foobar1** и **foobar2**.</span><span class="sxs-lookup"><span data-stu-id="f9931-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="f9931-112">Созданные имена учетных записей хранения автоматически проверяются на уникальность.</span><span class="sxs-lookup"><span data-stu-id="f9931-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="f9931-113">Имена учетных записей хранения формируются лексикографически на основе `count`.</span><span class="sxs-lookup"><span data-stu-id="f9931-113">The storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="f9931-114">Например, если для параметра `count` задано значение 10, тогда имена учетных записей хранения будут заканчиваться на двухзначное число (01, 02, 03 и т. д.).</span><span class="sxs-lookup"><span data-stu-id="f9931-114">For example, if `count` is 10, then the storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="f9931-115">Значением по умолчанию для параметра `defaultValue.prefix` является **null**, а для параметра `defaultValue.type` — **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="f9931-115">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="f9931-116">Любой тип, не указанный в `constraints.allowedTypes`, скрыт, а любой тип, не указанный в `constraints.excludedTypes`, отображается.</span><span class="sxs-lookup"><span data-stu-id="f9931-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="f9931-117">Параметры `constraints.allowedTypes` и `constraints.excludedTypes` являются необязательными. При этом их нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="f9931-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="f9931-118">Кроме создания имен учетных записей хранения, параметр `count` используется, чтобы задать соответствующее число для элемента.</span><span class="sxs-lookup"><span data-stu-id="f9931-118">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="f9931-119">Он поддерживает статическое значение, например **2**, или динамическое значение из другого элемента, например `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="f9931-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="f9931-120">Значение по умолчанию — **1**.</span><span class="sxs-lookup"><span data-stu-id="f9931-120">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f9931-121">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="f9931-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="f9931-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9931-122">Next steps</span></span>
* <span data-ttu-id="f9931-123">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9931-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f9931-124">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9931-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f9931-125">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f9931-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
