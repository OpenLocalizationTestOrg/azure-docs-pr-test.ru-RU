---
title: "элемент управляемого пользовательского интерфейса приложения UserNameTextBox aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Compute.UserNameTextBox для управляемых приложений Azure"
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="dfad2-103">Элемент пользовательского интерфейса Microsoft.Compute.UserNameTextBox</span><span class="sxs-lookup"><span data-stu-id="dfad2-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="dfad2-104">Элемент управления "Текстовое поле" со встроенной проверкой имен пользователей Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="dfad2-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="dfad2-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="dfad2-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="dfad2-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="dfad2-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="dfad2-108">Схема</span><span class="sxs-lookup"><span data-stu-id="dfad2-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="dfad2-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="dfad2-109">Remarks</span></span>
- <span data-ttu-id="dfad2-110">Если `constraints.required` задано слишком**true**, а затем hello текстовое поле должно содержать toovalidate значение успешно.</span><span class="sxs-lookup"><span data-stu-id="dfad2-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="dfad2-111">значение по умолчанию Hello — **true**.</span><span class="sxs-lookup"><span data-stu-id="dfad2-111">hello default value is **true**.</span></span>
- <span data-ttu-id="dfad2-112">Необходимо задать значение для параметра `osPlatform` (**Windows** или **Linux**).</span><span class="sxs-lookup"><span data-stu-id="dfad2-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="dfad2-113">`constraints.regex` — это шаблон регулярного выражения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="dfad2-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="dfad2-114">Если указано, затем hello текстовое поле значение должно соответствовать шаблону toovalidate hello успешно.</span><span class="sxs-lookup"><span data-stu-id="dfad2-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="dfad2-115">Значение по умолчанию — **null**.</span><span class="sxs-lookup"><span data-stu-id="dfad2-115">The default value is **null**.</span></span>
- <span data-ttu-id="dfad2-116">`constraints.validationMessage`При toodisplay строку hello текстовое поле значение не проходит проверку hello, определяемое `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="dfad2-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="dfad2-117">Если не указано, то hello встроенной проверке текстовое поле, используются сообщения.</span><span class="sxs-lookup"><span data-stu-id="dfad2-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="dfad2-118">значение по умолчанию Hello — **null**.</span><span class="sxs-lookup"><span data-stu-id="dfad2-118">hello default value is **null**.</span></span>
- <span data-ttu-id="dfad2-119">Этот элемент имеет встроенной проверке, которая основана на hello значение, указанное для `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="dfad2-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="dfad2-120">Встроенная проверка Hello может использоваться вместе с настраиваемое регулярное выражение.</span><span class="sxs-lookup"><span data-stu-id="dfad2-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="dfad2-121">Если значение параметра `constraints.regex` указано, то оба hello встроенные и пользовательские проверки активации.</span><span class="sxs-lookup"><span data-stu-id="dfad2-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="dfad2-122">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="dfad2-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="dfad2-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dfad2-123">Next steps</span></span>
* <span data-ttu-id="dfad2-124">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfad2-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="dfad2-125">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfad2-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="dfad2-126">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="dfad2-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
