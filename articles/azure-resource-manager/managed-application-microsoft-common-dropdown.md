---
title: "Элемент пользовательского интерфейса DropDown управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Common.DropDown для управляемых приложений Azure"
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
ms.openlocfilehash: a769e14efbae928b811fa1f1b1c2d4fba3c7692b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="5571d-103">Элемент пользовательского интерфейса Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="5571d-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="5571d-104">Элемент управления для выбора с раскрывающимся списком.</span><span class="sxs-lookup"><span data-stu-id="5571d-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="5571d-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5571d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5571d-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="5571d-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="5571d-108">Схема</span><span class="sxs-lookup"><span data-stu-id="5571d-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5571d-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="5571d-109">Remarks</span></span>
- <span data-ttu-id="5571d-110">Метка для `constraints.allowedValues` — это отображаемый текст элемента. Его значение — это выходное значение при выборе элемента.</span><span class="sxs-lookup"><span data-stu-id="5571d-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="5571d-111">Если указано, значение по умолчанию должно быть меткой в `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="5571d-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="5571d-112">Если не указано, выбирается первый элемент в `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="5571d-112">If not specified, the first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="5571d-113">Значение по умолчанию — **null**.</span><span class="sxs-lookup"><span data-stu-id="5571d-113">The default value is **null**.</span></span>
- <span data-ttu-id="5571d-114">Параметр `constraints.allowedValues` должен содержать по крайней мере один элемент.</span><span class="sxs-lookup"><span data-stu-id="5571d-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="5571d-115">Этот элемент не поддерживает свойство `constraints.required`.</span><span class="sxs-lookup"><span data-stu-id="5571d-115">This element doesn't support the `constraints.required` property.</span></span> <span data-ttu-id="5571d-116">Чтобы эмулировать такое поведение, добавьте элемент с меткой и значением `""` (пустая строка) в `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="5571d-116">To emulate this behavior, add an item with a label and value of `""` (empty string) to `constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5571d-117">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="5571d-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="5571d-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5571d-118">Next steps</span></span>
* <span data-ttu-id="5571d-119">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5571d-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5571d-120">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5571d-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5571d-121">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="5571d-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
