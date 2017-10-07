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
# <a name="microsoftcommontextbox-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Common.TextBox
Элемент управления, который может быть используется tooedit неформатированного текста. Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Пример элемента пользовательского интерфейса
![Элемент пользовательского интерфейса Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>Схема
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

## <a name="remarks"></a>Примечания
- Если `constraints.required` задано слишком**true**, а затем hello текстовое поле должно содержать toovalidate значение успешно. значение по умолчанию Hello — **false**.
- `constraints.regex` — это шаблон регулярного выражения JavaScript. Если указано, затем hello текстовое поле значение должно соответствовать шаблону toovalidate hello успешно. Значение по умолчанию — **null**.
- `constraints.validationMessage`При toodisplay строка, текстовое поле hello значение не проходит проверку. Если не указано, то hello встроенной проверке текстовое поле, используются сообщения. значение по умолчанию Hello — **null**.
- Его невозможно toospecify значение для `constraints.regex` при `constraints.required` задано слишком**false**. В этом случае значение не требуется для hello текстовое поле toovalidate успешно. Если он указан, она должна соответствовать шаблону регулярного выражения hello.

## <a name="sample-output"></a>Пример выходных данных

```json
"foobar"
```

## <a name="next-steps"></a>Дальнейшие действия
* Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).
* Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).
