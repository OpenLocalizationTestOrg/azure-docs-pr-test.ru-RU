---
title: "элемент управляемого пользовательского интерфейса приложения StorageAccountSelector aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Storage.StorageAccountSelector для управляемых приложений Azure"
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="32910-103">Элемент пользовательского интерфейса Microsoft.Storage.StorageAccountSelector</span><span class="sxs-lookup"><span data-stu-id="32910-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="32910-104">Элемент управления для выбора новой или имеющейся учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="32910-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="32910-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="32910-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="32910-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="32910-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="32910-108">Схема</span><span class="sxs-lookup"><span data-stu-id="32910-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="32910-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="32910-109">Remarks</span></span>
- <span data-ttu-id="32910-110">Если необходимо, параметр `defaultValue.name` автоматически проверяется на уникальность.</span><span class="sxs-lookup"><span data-stu-id="32910-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="32910-111">Если имя учетной записи хранения hello не является уникальным, hello пользователь должен указать другое имя или выберите существующую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="32910-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="32910-112">Здравствуйте, значение по умолчанию для `defaultValue.type` — **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="32910-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="32910-113">Любой тип, не указанный в `constraints.allowedTypes`, скрыт, а любой тип, не указанный в `constraints.excludedTypes`, отображается.</span><span class="sxs-lookup"><span data-stu-id="32910-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="32910-114">Параметры `constraints.allowedTypes` и `constraints.excludedTypes` являются необязательными. При этом их нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="32910-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="32910-115">Если `options.hideExisting` — **true**, hello пользователь не может выбрать существующую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="32910-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="32910-116">значение по умолчанию Hello — **false**.</span><span class="sxs-lookup"><span data-stu-id="32910-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="32910-117">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="32910-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="32910-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32910-118">Next steps</span></span>
* <span data-ttu-id="32910-119">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32910-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="32910-120">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32910-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="32910-121">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="32910-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
