---
title: "элемент управляемого пользовательского интерфейса приложения CredentialsCombo aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Compute.CredentialsCombo для управляемых приложений Azure"
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Compute.CredentialsCombo
Группа элементов управления со встроенной проверкой паролей и открытых ключей SSH для Windows и Linux. Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Пример элемента пользовательского интерфейса
![Элемент пользовательского интерфейса Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>Схема
Если `osPlatform` — **Windows**, а затем hello используется следующая схема:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

Если `osPlatform` — **Linux**, а затем hello используется следующая схема:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a>Примечания
- Необходимо задать значение для параметра `osPlatform` (**Windows** или **Linux**).
- Если `constraints.required` задано слишком**true**, затем hello пароль или SSH открытого ключа текстовые поля должны содержать значения toovalidate успешно. значение по умолчанию Hello — **true**.
- Если `options.hideConfirmation` задано слишком**true**, скрыта hello второе текстовое поле для подтверждения пароля пользователя hello. значение по умолчанию Hello — **false**.
- Если `options.hidePassword` задано слишком**true**, скрыта hello параметр toouse пароля. Его можно использовать только тогда, когда параметр `osPlatform` имеет значение **Linux**. Значение по умолчанию — **false**.
- Дополнительные ограничения на hello допускается пароли можно реализовать с помощью hello `customPasswordRegex` свойство. Здравствуйте, строки в `customValidationMessage` отображается, если пароль не соответствует пользовательской проверки. Hello значение по умолчанию для обоих свойств — **null**.

## <a name="sample-output"></a>Пример выходных данных
Если `osPlatform` — **Windows**, или предоставляемое hello пользователем пароля вместо открытого ключа SSH, а затем hello следующие ожидаются выходные данные:

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

Если пользователь hello открытый ключ SSH, затем hello следующие выходные данные ожидается:
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>Дальнейшие действия
* Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).
* Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).
