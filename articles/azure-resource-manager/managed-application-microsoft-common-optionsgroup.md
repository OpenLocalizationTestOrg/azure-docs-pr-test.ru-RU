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
# <a name="microsoftcommonoptionsgroup-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Common.OptionsGroup
Элемент управления для выбора со строкой доступных вариантов. Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Пример элемента пользовательского интерфейса
![Элемент пользовательского интерфейса Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a>Схема
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

## <a name="remarks"></a>Примечания
- Метка Hello `constraints.allowedValues` hello отображаемый текст для элемента, который его значение hello выходное значение при выборе элемента hello.
- Если указано, значение по умолчанию hello должен быть в метку `constraints.allowedValues`. Если не указан, hello первого элемента в `constraints.allowedValues` выбран по умолчанию. значение по умолчанию Hello — **null**.
- Параметр `constraints.allowedValues` должен содержать по крайней мере один элемент.
- Этот элемент не поддерживает hello `constraints.required` свойства; элемент должен иметь выбранного toovalidate успешно.

## <a name="sample-output"></a>Пример выходных данных
```json
"Bar"
```

## <a name="next-steps"></a>Дальнейшие действия
* Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).
* Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).
