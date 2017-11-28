---
title: "Элемент пользовательского интерфейса StorageAccountSelector управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Storage.StorageAccountSelector для управляемых приложений Azure"
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
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="a4a30-103">Элемент пользовательского интерфейса Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="a4a30-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="a4a30-104">Элемент управления для выбора новой или имеющейся учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a4a30-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="a4a30-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a4a30-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="a4a30-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a4a30-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="a4a30-108">Схема</span><span class="sxs-lookup"><span data-stu-id="a4a30-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="a4a30-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="a4a30-109">Remarks</span></span>
- <span data-ttu-id="a4a30-110">Если необходимо, параметр `defaultValue.name` автоматически проверяется на уникальность.</span><span class="sxs-lookup"><span data-stu-id="a4a30-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="a4a30-111">Если имя учетной записи хранения не является уникальным, пользователь должен указать другое имя или выбрать имеющуюся учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a4a30-111">If the storage account name is not unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="a4a30-112">Значением по умолчанию для параметра `defaultValue.type` является **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="a4a30-112">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="a4a30-113">Любой тип, не указанный в `constraints.allowedTypes`, скрыт, а любой тип, не указанный в `constraints.excludedTypes`, отображается.</span><span class="sxs-lookup"><span data-stu-id="a4a30-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="a4a30-114">Параметры `constraints.allowedTypes` и `constraints.excludedTypes` являются необязательными. При этом их нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="a4a30-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="a4a30-115">Если для параметра `options.hideExisting` задано значение **true**, пользователь не может выбрать имеющуюся учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a4a30-115">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="a4a30-116">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="a4a30-116">The default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="a4a30-117">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="a4a30-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="a4a30-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4a30-118">Next steps</span></span>
* <span data-ttu-id="a4a30-119">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4a30-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a4a30-120">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4a30-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="a4a30-121">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="a4a30-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
