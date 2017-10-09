---
title: "элемент управляемого пользовательского интерфейса приложения раздел aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Common.Section для управляемых приложений Azure"
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="dd839-103">Элемент пользовательского интерфейса Microsoft.Common.Section</span><span class="sxs-lookup"><span data-stu-id="dd839-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="dd839-104">Элемент управления, группирующий один или несколько элементов под заголовком.</span><span class="sxs-lookup"><span data-stu-id="dd839-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="dd839-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="dd839-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="dd839-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="dd839-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="dd839-108">Схема</span><span class="sxs-lookup"><span data-stu-id="dd839-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="dd839-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="dd839-109">Remarks</span></span>
- <span data-ttu-id="dd839-110">Параметр `elements` должен содержать по крайней мере один элемент, а также может содержать все типы элементов, кроме `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="dd839-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="dd839-111">Этот элемент не поддерживает hello `toolTip` свойство.</span><span class="sxs-lookup"><span data-stu-id="dd839-111">This element doesn't support hello `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="dd839-112">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="dd839-112">Sample output</span></span>
<span data-ttu-id="dd839-113">tooaccess hello выходных значений элементов в `elements`, использовать hello [basics()](managed-application-createuidefinition-functions.md#basics) или [steps()](managed-application-createuidefinition-functions.md#steps) функции и точечной нотации:</span><span class="sxs-lookup"><span data-stu-id="dd839-113">tooaccess hello output values of elements in `elements`, use hello [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="dd839-114">Элементы типа `Microsoft.Common.Section` не содержат выходные значения.</span><span class="sxs-lookup"><span data-stu-id="dd839-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd839-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd839-115">Next steps</span></span>
* <span data-ttu-id="dd839-116">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd839-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="dd839-117">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd839-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="dd839-118">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="dd839-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
