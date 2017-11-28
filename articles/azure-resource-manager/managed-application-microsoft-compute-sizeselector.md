---
title: "элемент управляемого пользовательского интерфейса приложения SizeSelector aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Compute.SizeSelector для управляемых приложений Azure"
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="69a53-103">Элемент пользовательского интерфейса Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="69a53-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="69a53-104">Элемент управления для выбора размера одного или нескольких экземпляров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="69a53-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="69a53-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="69a53-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="69a53-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="69a53-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="69a53-108">Схема</span><span class="sxs-lookup"><span data-stu-id="69a53-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="69a53-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="69a53-109">Remarks</span></span>
- <span data-ttu-id="69a53-110">Параметр `recommendedSizes` должен содержать по крайней мере один размер.</span><span class="sxs-lookup"><span data-stu-id="69a53-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="69a53-111">Hello рекомендуется сначала используется размер по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="69a53-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="69a53-112">Если рекомендуемый размер недоступен в расположении hello выбран, размер hello автоматически пропускается.</span><span class="sxs-lookup"><span data-stu-id="69a53-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="69a53-113">Вместо этого hello Далее рекомендуемый размер используется.</span><span class="sxs-lookup"><span data-stu-id="69a53-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="69a53-114">Любого размера, не указан в hello `constraints.allowedSizes` скрыта и любого размера, не указан в `constraints.excludedSizes` отображается.</span><span class="sxs-lookup"><span data-stu-id="69a53-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="69a53-115">Параметры `constraints.allowedSizes` и `constraints.excludedSizes` являются необязательными. При этом их нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="69a53-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="69a53-116">Список доступных размеров Hello можно определить путем вызова [список доступных размеров виртуальной машины для подписки](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="69a53-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="69a53-117">Необходимо задать значение для параметра `osPlatform` (**Windows** или **Linux**).</span><span class="sxs-lookup"><span data-stu-id="69a53-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="69a53-118">Он использовал затраты на оборудование toodetermine hello hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="69a53-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="69a53-119">Параметр `imageReference` не указывается для основных образов, но указывается для сторонних.</span><span class="sxs-lookup"><span data-stu-id="69a53-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="69a53-120">Он использовал toodetermine затраты на программное обеспечение hello hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="69a53-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="69a53-121">`count`— используется tooset hello соответствующий коэффициент пересчета для элемента hello.</span><span class="sxs-lookup"><span data-stu-id="69a53-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="69a53-122">Он поддерживает статическое значение, например **2**, или динамическое значение из другого элемента, например `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="69a53-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="69a53-123">значение по умолчанию Hello — **1**.</span><span class="sxs-lookup"><span data-stu-id="69a53-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="69a53-124">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="69a53-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="69a53-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69a53-125">Next steps</span></span>
* <span data-ttu-id="69a53-126">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69a53-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="69a53-127">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69a53-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="69a53-128">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="69a53-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
