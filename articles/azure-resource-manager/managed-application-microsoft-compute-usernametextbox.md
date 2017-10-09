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
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Compute.UserNameTextBox
Элемент управления "Текстовое поле" со встроенной проверкой имен пользователей Windows и Linux. Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Пример элемента пользовательского интерфейса
![Элемент пользовательского интерфейса Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>Схема
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

## <a name="remarks"></a>Примечания
- Если `constraints.required` задано слишком**true**, а затем hello текстовое поле должно содержать toovalidate значение успешно. значение по умолчанию Hello — **true**.
- Необходимо задать значение для параметра `osPlatform` (**Windows** или **Linux**).
- `constraints.regex` — это шаблон регулярного выражения JavaScript. Если указано, затем hello текстовое поле значение должно соответствовать шаблону toovalidate hello успешно. Значение по умолчанию — **null**.
- `constraints.validationMessage`При toodisplay строку hello текстовое поле значение не проходит проверку hello, определяемое `constraints.regex`. Если не указано, то hello встроенной проверке текстовое поле, используются сообщения. значение по умолчанию Hello — **null**.
- Этот элемент имеет встроенной проверке, которая основана на hello значение, указанное для `osPlatform`. Встроенная проверка Hello может использоваться вместе с настраиваемое регулярное выражение.
Если значение параметра `constraints.regex` указано, то оба hello встроенные и пользовательские проверки активации.

## <a name="sample-output"></a>Пример выходных данных
```json
"tabrezm"
```

## <a name="next-steps"></a>Дальнейшие действия
* Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).
* Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).
