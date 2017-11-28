---
title: "Элемент пользовательского интерфейса Section управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Common.Section для управляемых приложений Azure"
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
ms.openlocfilehash: 34c0f2f88e6af5a0f822ec116e7e2334e4e29e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="3ac6a-103">Элемент пользовательского интерфейса Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="3ac6a-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="3ac6a-104">Элемент управления, группирующий один или несколько элементов под заголовком.</span><span class="sxs-lookup"><span data-stu-id="3ac6a-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="3ac6a-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3ac6a-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="3ac6a-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="3ac6a-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="3ac6a-108">Схема</span><span class="sxs-lookup"><span data-stu-id="3ac6a-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="3ac6a-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="3ac6a-109">Remarks</span></span>
- <span data-ttu-id="3ac6a-110">Параметр `elements` должен содержать по крайней мере один элемент, а также может содержать все типы элементов, кроме `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="3ac6a-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="3ac6a-111">Этот элемент не поддерживает свойство `toolTip`.</span><span class="sxs-lookup"><span data-stu-id="3ac6a-111">This element doesn't support the `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="3ac6a-112">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="3ac6a-112">Sample output</span></span>
<span data-ttu-id="3ac6a-113">Для доступа к выходным значениям элементов в `elements` используйте функции [basics()](managed-application-createuidefinition-functions.md#basics) или [steps()](managed-application-createuidefinition-functions.md#steps) и точечную нотацию:</span><span class="sxs-lookup"><span data-stu-id="3ac6a-113">To access the output values of elements in `elements`, use the [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="3ac6a-114">Элементы типа `Microsoft.Common.Section` не содержат выходные значения.</span><span class="sxs-lookup"><span data-stu-id="3ac6a-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ac6a-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ac6a-115">Next steps</span></span>
* <span data-ttu-id="3ac6a-116">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ac6a-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="3ac6a-117">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ac6a-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="3ac6a-118">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="3ac6a-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
