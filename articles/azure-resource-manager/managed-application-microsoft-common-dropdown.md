---
title: "элемент пользовательского интерфейса раскрывающийся список управляемых приложений aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Common.DropDown для управляемых приложений Azure"
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="105a2-103">Элемент пользовательского интерфейса Microsoft.Common.DropDown</span><span class="sxs-lookup"><span data-stu-id="105a2-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="105a2-104">Элемент управления для выбора с раскрывающимся списком.</span><span class="sxs-lookup"><span data-stu-id="105a2-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="105a2-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="105a2-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="105a2-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="105a2-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="105a2-108">Схема</span><span class="sxs-lookup"><span data-stu-id="105a2-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="105a2-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="105a2-109">Remarks</span></span>
- <span data-ttu-id="105a2-110">Метка Hello `constraints.allowedValues` hello отображаемый текст для элемента, который его значение hello выходное значение при выборе элемента hello.</span><span class="sxs-lookup"><span data-stu-id="105a2-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="105a2-111">Если указано, значение по умолчанию hello должен быть в метку `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="105a2-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="105a2-112">Если не указан, hello первого элемента в `constraints.allowedValues` выбран.</span><span class="sxs-lookup"><span data-stu-id="105a2-112">If not specified, hello first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="105a2-113">значение по умолчанию Hello — **null**.</span><span class="sxs-lookup"><span data-stu-id="105a2-113">hello default value is **null**.</span></span>
- <span data-ttu-id="105a2-114">Параметр `constraints.allowedValues` должен содержать по крайней мере один элемент.</span><span class="sxs-lookup"><span data-stu-id="105a2-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="105a2-115">Этот элемент не поддерживает hello `constraints.required` свойство.</span><span class="sxs-lookup"><span data-stu-id="105a2-115">This element doesn't support hello `constraints.required` property.</span></span> <span data-ttu-id="105a2-116">tooemulate такое поведение, добавить элемент с подписью и значение `""` (пустая строка) слишком`constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="105a2-116">tooemulate this behavior, add an item with a label and value of `""` (empty string) too`constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="105a2-117">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="105a2-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="105a2-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="105a2-118">Next steps</span></span>
* <span data-ttu-id="105a2-119">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="105a2-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="105a2-120">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="105a2-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="105a2-121">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="105a2-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
