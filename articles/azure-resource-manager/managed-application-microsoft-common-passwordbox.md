---
title: "Элемент пользовательского интерфейса PasswordBox управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Common.PasswordBox для управляемых приложений Azure"
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="e2b0d-103">Элемент пользовательского интерфейса Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="e2b0d-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="e2b0d-104">Элемент управления, который может использоваться для указания и подтверждения пароля.</span><span class="sxs-lookup"><span data-stu-id="e2b0d-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="e2b0d-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e2b0d-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="e2b0d-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="e2b0d-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="e2b0d-108">Схема</span><span class="sxs-lookup"><span data-stu-id="e2b0d-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="e2b0d-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="e2b0d-109">Remarks</span></span>
- <span data-ttu-id="e2b0d-110">Этот элемент не поддерживает свойство `defaultValue`.</span><span class="sxs-lookup"><span data-stu-id="e2b0d-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="e2b0d-111">Дополнительные сведения о реализации `constraints` см. в статье [Элемент пользовательского интерфейса Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="e2b0d-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="e2b0d-112">Если для параметра `options.hideConfirmation` задано значение **true**, второе текстовое поле для подтверждения пароля скрыто.</span><span class="sxs-lookup"><span data-stu-id="e2b0d-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="e2b0d-113">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="e2b0d-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="e2b0d-114">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="e2b0d-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="e2b0d-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2b0d-115">Next steps</span></span>
* <span data-ttu-id="e2b0d-116">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2b0d-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e2b0d-117">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2b0d-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="e2b0d-118">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="e2b0d-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
