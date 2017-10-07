---
title: "элемент управляемого пользовательского интерфейса приложения TextBox aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Common.TextBox для управляемых приложений Azure"
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="ccdef-103">Элемент пользовательского интерфейса Microsoft.Common.TextBox</span><span class="sxs-lookup"><span data-stu-id="ccdef-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="ccdef-104">Элемент управления, который может быть используется tooedit неформатированного текста.</span><span class="sxs-lookup"><span data-stu-id="ccdef-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="ccdef-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ccdef-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="ccdef-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ccdef-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="ccdef-108">Схема</span><span class="sxs-lookup"><span data-stu-id="ccdef-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="ccdef-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="ccdef-109">Remarks</span></span>
- <span data-ttu-id="ccdef-110">Если `constraints.required` задано слишком**true**, а затем hello текстовое поле должно содержать toovalidate значение успешно.</span><span class="sxs-lookup"><span data-stu-id="ccdef-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="ccdef-111">значение по умолчанию Hello — **false**.</span><span class="sxs-lookup"><span data-stu-id="ccdef-111">hello default value is **false**.</span></span>
- <span data-ttu-id="ccdef-112">`constraints.regex` — это шаблон регулярного выражения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ccdef-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="ccdef-113">Если указано, затем hello текстовое поле значение должно соответствовать шаблону toovalidate hello успешно.</span><span class="sxs-lookup"><span data-stu-id="ccdef-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="ccdef-114">Значение по умолчанию — **null**.</span><span class="sxs-lookup"><span data-stu-id="ccdef-114">The default value is **null**.</span></span>
- <span data-ttu-id="ccdef-115">`constraints.validationMessage`При toodisplay строка, текстовое поле hello значение не проходит проверку.</span><span class="sxs-lookup"><span data-stu-id="ccdef-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="ccdef-116">Если не указано, то hello встроенной проверке текстовое поле, используются сообщения.</span><span class="sxs-lookup"><span data-stu-id="ccdef-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="ccdef-117">значение по умолчанию Hello — **null**.</span><span class="sxs-lookup"><span data-stu-id="ccdef-117">hello default value is **null**.</span></span>
- <span data-ttu-id="ccdef-118">Его невозможно toospecify значение для `constraints.regex` при `constraints.required` задано слишком**false**.</span><span class="sxs-lookup"><span data-stu-id="ccdef-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="ccdef-119">В этом случае значение не требуется для hello текстовое поле toovalidate успешно.</span><span class="sxs-lookup"><span data-stu-id="ccdef-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="ccdef-120">Если он указан, она должна соответствовать шаблону регулярного выражения hello.</span><span class="sxs-lookup"><span data-stu-id="ccdef-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="ccdef-121">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="ccdef-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="ccdef-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ccdef-122">Next steps</span></span>
* <span data-ttu-id="ccdef-123">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ccdef-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ccdef-124">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ccdef-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="ccdef-125">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="ccdef-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
