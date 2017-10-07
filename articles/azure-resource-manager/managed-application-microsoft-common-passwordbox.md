---
title: "элемент пользовательского интерфейса PasswordBox управляемого приложения aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Common.PasswordBox для управляемых приложений Azure"
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="f8d30-103">Элемент пользовательского интерфейса Microsoft.Common.PasswordBox</span><span class="sxs-lookup"><span data-stu-id="f8d30-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="f8d30-104">Элемент управления, можно использовать tooprovide и подтвердить пароль.</span><span class="sxs-lookup"><span data-stu-id="f8d30-104">A control that can be used tooprovide and confirm a password.</span></span> <span data-ttu-id="f8d30-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f8d30-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f8d30-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="f8d30-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="f8d30-108">Схема</span><span class="sxs-lookup"><span data-stu-id="f8d30-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="f8d30-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="f8d30-109">Remarks</span></span>
- <span data-ttu-id="f8d30-110">Этот элемент не поддерживает hello `defaultValue` свойство.</span><span class="sxs-lookup"><span data-stu-id="f8d30-110">This element doesn't support hello `defaultValue` property.</span></span>
- <span data-ttu-id="f8d30-111">Дополнительные сведения о реализации `constraints` см. в статье [Элемент пользовательского интерфейса Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="f8d30-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="f8d30-112">Если `options.hideConfirmation` задано слишком**true**, hello второе текстовое поле для подтверждения пароля пользователя hello скрыт.</span><span class="sxs-lookup"><span data-stu-id="f8d30-112">If `options.hideConfirmation` is set too**true**, hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="f8d30-113">значение по умолчанию Hello — **false**.</span><span class="sxs-lookup"><span data-stu-id="f8d30-113">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f8d30-114">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="f8d30-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="f8d30-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8d30-115">Next steps</span></span>
* <span data-ttu-id="f8d30-116">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8d30-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f8d30-117">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8d30-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f8d30-118">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f8d30-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
