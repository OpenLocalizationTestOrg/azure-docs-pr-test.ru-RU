---
title: "Элемент пользовательского интерфейса DropDown управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Common.DropDown для управляемых приложений Azure"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: a3cbb7363c04043eb253e91e058753bc271e4e01
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcommondropdown-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Common.DropDown
Элемент управления для выбора с раскрывающимся списком. Этот элемент используется при [создании управляемого приложения Azure](publish-service-catalog-app.md).

## <a name="ui-sample"></a>Пример элемента пользовательского интерфейса
![Элемент пользовательского интерфейса Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a>Схема
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
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
- Метка для `constraints.allowedValues` — это отображаемый текст элемента. Его значение — это выходное значение при выборе элемента.
- Если указано, значение по умолчанию должно быть меткой в `constraints.allowedValues`. Если не указано, выбирается первый элемент в `constraints.allowedValues`. Значение по умолчанию — **null**.
- Параметр `constraints.allowedValues` должен содержать по крайней мере один элемент.
- Этот элемент не поддерживает свойство `constraints.required`. Чтобы эмулировать такое поведение, добавьте элемент с меткой и значением `""` (пустая строка) в `constraints.allowedValues`.

## <a name="sample-output"></a>Пример выходных данных
```json
"Bar"
```

## <a name="next-steps"></a>Дальнейшие действия
* Общие сведения об управляемых приложениях Azure см. в [этой статье](overview.md).
* Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](create-uidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](create-uidefinition-elements.md).
