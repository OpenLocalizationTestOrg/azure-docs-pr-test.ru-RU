---
title: "Элемент пользовательского интерфейса TextBox управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Common.TextBox для управляемых приложений Azure"
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="8038c-103">Элемент пользовательского интерфейса Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="8038c-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="8038c-104">Элемент управления, который может использоваться для редактирования неформатированного текста.</span><span class="sxs-lookup"><span data-stu-id="8038c-104">A control that can be used to edit unformatted text.</span></span> <span data-ttu-id="8038c-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8038c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="8038c-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="8038c-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="8038c-108">Схема</span><span class="sxs-lookup"><span data-stu-id="8038c-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="8038c-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="8038c-109">Remarks</span></span>
- <span data-ttu-id="8038c-110">Если для параметра `constraints.required` задано значение **true**, то текстовое поле должно содержать значение, чтобы пройти проверку.</span><span class="sxs-lookup"><span data-stu-id="8038c-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="8038c-111">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="8038c-111">The default value is **false**.</span></span>
- <span data-ttu-id="8038c-112">`constraints.regex` — это шаблон регулярного выражения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8038c-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="8038c-113">Если параметр указан, значение текстового поля должно соответствовать шаблону, чтобы пройти проверку.</span><span class="sxs-lookup"><span data-stu-id="8038c-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="8038c-114">Значение по умолчанию — **null**.</span><span class="sxs-lookup"><span data-stu-id="8038c-114">The default value is **null**.</span></span>
- <span data-ttu-id="8038c-115">`constraints.validationMessage` — это строка, которая отображается, когда значение в текстовом поле не проходит проверку.</span><span class="sxs-lookup"><span data-stu-id="8038c-115">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="8038c-116">Если параметр не указан, используются встроенные сообщения проверки текстового поля.</span><span class="sxs-lookup"><span data-stu-id="8038c-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="8038c-117">Значение по умолчанию — **null**.</span><span class="sxs-lookup"><span data-stu-id="8038c-117">The default value is **null**.</span></span>
- <span data-ttu-id="8038c-118">Можно указать значение для `constraints.regex`, если для параметра `constraints.required` задано значение **false**.</span><span class="sxs-lookup"><span data-stu-id="8038c-118">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="8038c-119">В этом случае, чтобы пройти проверку, значение для текстового поля не требуется.</span><span class="sxs-lookup"><span data-stu-id="8038c-119">In this scenario, a value is not required for the text box to validate successfully.</span></span> <span data-ttu-id="8038c-120">Если указано, оно должно соответствовать шаблону регулярного выражения.</span><span class="sxs-lookup"><span data-stu-id="8038c-120">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="8038c-121">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="8038c-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="8038c-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8038c-122">Next steps</span></span>
* <span data-ttu-id="8038c-123">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8038c-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8038c-124">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8038c-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="8038c-125">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="8038c-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
