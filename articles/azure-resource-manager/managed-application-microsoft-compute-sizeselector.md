---
title: "Элемент пользовательского интерфейса SizeSelector управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Compute.SizeSelector для управляемых приложений Azure"
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
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="0f81f-103">Элемент пользовательского интерфейса Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="0f81f-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="0f81f-104">Элемент управления для выбора размера одного или нескольких экземпляров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0f81f-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="0f81f-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0f81f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="0f81f-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="0f81f-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="0f81f-108">Схема</span><span class="sxs-lookup"><span data-stu-id="0f81f-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="0f81f-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="0f81f-109">Remarks</span></span>
- <span data-ttu-id="0f81f-110">Параметр `recommendedSizes` должен содержать по крайней мере один размер.</span><span class="sxs-lookup"><span data-stu-id="0f81f-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="0f81f-111">По умолчанию используется первый рекомендуемый размер.</span><span class="sxs-lookup"><span data-stu-id="0f81f-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="0f81f-112">Если в выбранном расположении рекомендуемый размер недоступен, он автоматически пропускается.</span><span class="sxs-lookup"><span data-stu-id="0f81f-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="0f81f-113">Вместо него используется следующий рекомендуемый размер.</span><span class="sxs-lookup"><span data-stu-id="0f81f-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="0f81f-114">Любой размер, не указанный в параметре `constraints.allowedSizes`, скрыт. При этом любой размер, не указанный в параметре `constraints.excludedSizes`, отображается.</span><span class="sxs-lookup"><span data-stu-id="0f81f-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="0f81f-115">Параметры `constraints.allowedSizes` и `constraints.excludedSizes` являются необязательными. При этом их нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="0f81f-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="0f81f-116">Сведения о получении списка доступных размеров виртуальных машин для подписки см. в [этой статье](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="0f81f-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="0f81f-117">Необходимо задать значение для параметра `osPlatform` (**Windows** или **Linux**).</span><span class="sxs-lookup"><span data-stu-id="0f81f-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="0f81f-118">Он используется для определения затрат на оборудование виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0f81f-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="0f81f-119">Параметр `imageReference` не указывается для основных образов, но указывается для сторонних.</span><span class="sxs-lookup"><span data-stu-id="0f81f-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="0f81f-120">Он используется для определения затрат на программное обеспечение виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0f81f-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="0f81f-121">Параметр `count` используется для задания соответствующего числа для элемента.</span><span class="sxs-lookup"><span data-stu-id="0f81f-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="0f81f-122">Он поддерживает статическое значение, например **2**, или динамическое значение из другого элемента, например `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="0f81f-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="0f81f-123">Значение по умолчанию — **1**.</span><span class="sxs-lookup"><span data-stu-id="0f81f-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="0f81f-124">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="0f81f-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="0f81f-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f81f-125">Next steps</span></span>
* <span data-ttu-id="0f81f-126">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f81f-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0f81f-127">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f81f-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="0f81f-128">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="0f81f-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
