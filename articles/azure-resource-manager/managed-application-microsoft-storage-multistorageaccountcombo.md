---
title: "элемент управляемого пользовательского интерфейса приложения MultiStorageAccountCombo aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo для управляемых приложений Azure"
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="94b28-103">Элемент пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo</span><span class="sxs-lookup"><span data-stu-id="94b28-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="94b28-104">Группа элементов управления для создания нескольких учетных записей хранения с именами, которые начинаются с общего префикса.</span><span class="sxs-lookup"><span data-stu-id="94b28-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="94b28-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="94b28-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="94b28-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="94b28-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="94b28-108">Схема</span><span class="sxs-lookup"><span data-stu-id="94b28-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="94b28-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="94b28-109">Remarks</span></span>
- <span data-ttu-id="94b28-110">Здравствуйте, значение для `defaultValue.prefix` сцепляется с одной или более целых чисел toogenerate hello последовательность имена учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="94b28-110">hello value for `defaultValue.prefix` is concatenated with one or more integers toogenerate hello sequence of storage account names.</span></span> <span data-ttu-id="94b28-111">Например, если для параметра `defaultValue.prefix` задано значение **foobar**, а для параметра `count` задано значение **2**, тогда создаются имена учетной записи хранения **foobar1** и **foobar2**.</span><span class="sxs-lookup"><span data-stu-id="94b28-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="94b28-112">Созданные имена учетных записей хранения автоматически проверяются на уникальность.</span><span class="sxs-lookup"><span data-stu-id="94b28-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="94b28-113">имена учетной записи хранения Hello создаются на основе лексикографически `count`.</span><span class="sxs-lookup"><span data-stu-id="94b28-113">hello storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="94b28-114">Например если `count` равно 10, то имена учетной записи хранения hello заканчиваться 2-значное целое число (01, 02, 03, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="94b28-114">For example, if `count` is 10, then hello storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="94b28-115">Здравствуйте, значение по умолчанию для `defaultValue.prefix` — **null**и для `defaultValue.type` — **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="94b28-115">hello default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="94b28-116">Любой тип, не указанный в `constraints.allowedTypes`, скрыт, а любой тип, не указанный в `constraints.excludedTypes`, отображается.</span><span class="sxs-lookup"><span data-stu-id="94b28-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="94b28-117">Параметры `constraints.allowedTypes` и `constraints.excludedTypes` являются необязательными. При этом их нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="94b28-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="94b28-118">В именах учетных записей хранилища toogenerating сложения `count` имеет соответствующий коэффициент для элемента hello используется tooset.</span><span class="sxs-lookup"><span data-stu-id="94b28-118">In addition toogenerating storage account names, `count` is used tooset the appropriate multiplier for hello element.</span></span> <span data-ttu-id="94b28-119">Он поддерживает статическое значение, например **2**, или динамическое значение из другого элемента, например `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="94b28-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="94b28-120">значение по умолчанию Hello — **1**.</span><span class="sxs-lookup"><span data-stu-id="94b28-120">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="94b28-121">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="94b28-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="94b28-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="94b28-122">Next steps</span></span>
* <span data-ttu-id="94b28-123">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94b28-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="94b28-124">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94b28-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="94b28-125">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="94b28-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
