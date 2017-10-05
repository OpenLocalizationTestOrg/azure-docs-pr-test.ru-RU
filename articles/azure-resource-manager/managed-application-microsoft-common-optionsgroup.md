---
title: "Элемент пользовательского интерфейса OptionsGroup управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Common.OptionsGroup для управляемых приложений Azure"
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
ms.openlocfilehash: 6e147ed28c8248f7f17cb36fd7ae13468141dced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="58192-103">Элемент пользовательского интерфейса Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="58192-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="58192-104">Элемент управления для выбора со строкой доступных вариантов.</span><span class="sxs-lookup"><span data-stu-id="58192-104">A selection control with a row of available options.</span></span> <span data-ttu-id="58192-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="58192-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="58192-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="58192-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="58192-108">Схема</span><span class="sxs-lookup"><span data-stu-id="58192-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
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

## <a name="remarks"></a><span data-ttu-id="58192-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="58192-109">Remarks</span></span>
- <span data-ttu-id="58192-110">Метка для `constraints.allowedValues` — это отображаемый текст элемента. Его значение — это выходное значение при выборе элемента.</span><span class="sxs-lookup"><span data-stu-id="58192-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="58192-111">Если указано, значение по умолчанию должно быть меткой в `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="58192-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="58192-112">Если не указано, по умолчанию выбирается первый элемент в `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="58192-112">If not specified, the first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="58192-113">Значение по умолчанию — **null**.</span><span class="sxs-lookup"><span data-stu-id="58192-113">The default value is **null**.</span></span>
- <span data-ttu-id="58192-114">Параметр `constraints.allowedValues` должен содержать по крайней мере один элемент.</span><span class="sxs-lookup"><span data-stu-id="58192-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="58192-115">Этот элемент не поддерживает свойство `constraints.required`. Необходимо выбрать элемент, чтобы пройти проверку.</span><span class="sxs-lookup"><span data-stu-id="58192-115">This element doesn't support the `constraints.required` property; an item must be selected to validate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="58192-116">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="58192-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="58192-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58192-117">Next steps</span></span>
* <span data-ttu-id="58192-118">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58192-118">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="58192-119">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58192-119">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="58192-120">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="58192-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
