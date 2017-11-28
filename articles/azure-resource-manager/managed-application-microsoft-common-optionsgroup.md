---
title: "элемент управляемого пользовательского интерфейса приложения OptionsGroup aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Common.OptionsGroup для управляемых приложений Azure"
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="d5a5b-103">Элемент пользовательского интерфейса Microsoft.Common.OptionsGroup</span><span class="sxs-lookup"><span data-stu-id="d5a5b-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="d5a5b-104">Элемент управления для выбора со строкой доступных вариантов.</span><span class="sxs-lookup"><span data-stu-id="d5a5b-104">A selection control with a row of available options.</span></span> <span data-ttu-id="d5a5b-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="d5a5b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d5a5b-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="d5a5b-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="d5a5b-108">Схема</span><span class="sxs-lookup"><span data-stu-id="d5a5b-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="d5a5b-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="d5a5b-109">Remarks</span></span>
- <span data-ttu-id="d5a5b-110">Метка Hello `constraints.allowedValues` hello отображаемый текст для элемента, который его значение hello выходное значение при выборе элемента hello.</span><span class="sxs-lookup"><span data-stu-id="d5a5b-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="d5a5b-111">Если указано, значение по умолчанию hello должен быть в метку `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="d5a5b-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="d5a5b-112">Если не указан, hello первого элемента в `constraints.allowedValues` выбран по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d5a5b-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="d5a5b-113">значение по умолчанию Hello — **null**.</span><span class="sxs-lookup"><span data-stu-id="d5a5b-113">hello default value is **null**.</span></span>
- <span data-ttu-id="d5a5b-114">Параметр `constraints.allowedValues` должен содержать по крайней мере один элемент.</span><span class="sxs-lookup"><span data-stu-id="d5a5b-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="d5a5b-115">Этот элемент не поддерживает hello `constraints.required` свойства; элемент должен иметь выбранного toovalidate успешно.</span><span class="sxs-lookup"><span data-stu-id="d5a5b-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d5a5b-116">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="d5a5b-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="d5a5b-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5a5b-117">Next steps</span></span>
* <span data-ttu-id="d5a5b-118">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5a5b-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d5a5b-119">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5a5b-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d5a5b-120">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d5a5b-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
