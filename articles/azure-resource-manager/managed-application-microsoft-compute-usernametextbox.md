---
title: "Элемент пользовательского интерфейса UserNameTextBox управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе Microsoft.Compute.UserNameTextBox для управляемых приложений Azure"
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
ms.openlocfilehash: c90be5a0ed3aadda81d7ec9b5388a96472f69af0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="1e794-103">Элемент пользовательского интерфейса Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="1e794-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="1e794-104">Элемент управления "Текстовое поле" со встроенной проверкой имен пользователей Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="1e794-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="1e794-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="1e794-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="1e794-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="1e794-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="1e794-108">Схема</span><span class="sxs-lookup"><span data-stu-id="1e794-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="1e794-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="1e794-109">Remarks</span></span>
- <span data-ttu-id="1e794-110">Если для параметра `constraints.required` задано значение **true**, то текстовое поле должно содержать значение, чтобы пройти проверку.</span><span class="sxs-lookup"><span data-stu-id="1e794-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="1e794-111">Значение по умолчанию — **true**.</span><span class="sxs-lookup"><span data-stu-id="1e794-111">The default value is **true**.</span></span>
- <span data-ttu-id="1e794-112">Необходимо задать значение для параметра `osPlatform` (**Windows** или **Linux**).</span><span class="sxs-lookup"><span data-stu-id="1e794-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="1e794-113">`constraints.regex` — это шаблон регулярного выражения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1e794-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="1e794-114">Если параметр указан, значение текстового поля должно соответствовать шаблону, чтобы пройти проверку.</span><span class="sxs-lookup"><span data-stu-id="1e794-114">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="1e794-115">Значение по умолчанию — **null**.</span><span class="sxs-lookup"><span data-stu-id="1e794-115">The default value is **null**.</span></span>
- <span data-ttu-id="1e794-116">`constraints.validationMessage` — это строка, которая отображается, когда значение текстового поля не проходит проверку, указанную в `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="1e794-116">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span></span> <span data-ttu-id="1e794-117">Если параметр не указан, используются встроенные сообщения проверки текстового поля.</span><span class="sxs-lookup"><span data-stu-id="1e794-117">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="1e794-118">Значение по умолчанию — **null**.</span><span class="sxs-lookup"><span data-stu-id="1e794-118">The default value is **null**.</span></span>
- <span data-ttu-id="1e794-119">Этот элемент содержит встроенную проверку, которая основана на значении, заданном для параметра `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="1e794-119">This element has built-in validation that is based on the value specified for `osPlatform`.</span></span> <span data-ttu-id="1e794-120">Встроенная проверка может использоваться вместе с настраиваемым регулярным выражением.</span><span class="sxs-lookup"><span data-stu-id="1e794-120">The built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="1e794-121">Если для параметра `constraints.regex` значение указано, активируются встроенные и пользовательские проверки.</span><span class="sxs-lookup"><span data-stu-id="1e794-121">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="1e794-122">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="1e794-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="1e794-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e794-123">Next steps</span></span>
* <span data-ttu-id="1e794-124">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e794-124">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="1e794-125">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e794-125">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="1e794-126">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="1e794-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
