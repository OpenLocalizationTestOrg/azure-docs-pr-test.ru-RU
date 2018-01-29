---
title: "Элемент пользовательского интерфейса FileUpload управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Common.FileUpload управляемых приложений Azure"
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
ms.openlocfilehash: 095880322ba801895a22efcf3476fa37d9e2ac3c
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Common.FileUpload
Элемент управления, который позволяет пользователю указать один или несколько файлов для отправки. Этот элемент используется при [создании управляемого приложения Azure](publish-service-catalog-app.md).

## <a name="ui-sample"></a>Пример элемента пользовательского интерфейса
![Элемент пользовательского интерфейса Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>Схема
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>Примечания
- `constraints.accept` — указывает типы файлов, которые отображаются в файловом диалоговом окне браузера. Сведения о допустимых значениях см. в [спецификации HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept). Значение по умолчанию — **null**.
- Если `options.multiple` имеет значение **true**, пользователь может выбрать несколько файлов в файловом диалоговом окне браузера. Значение по умолчанию — **false**.
- Этот элемент поддерживает отправку файлов в двух режимах, которые задаются в параметре `options.uploadMode`. Если указан **file**, тогда выходные данные предоставляют содержимое файла в виде большого двоичного объекта. Если указан **url**, тогда файл отравляется во временное расположение и выходные данные содержат URL-адрес большого двоичного объекта. Временные большие двоичные объекты очищаются через 24 часа. Значение по умолчанию — **file**.
- Значение `options.openMode` определяет режим, в котором открывается файл. Если предполагается, что файл содержит обычный текст, укажите **text**. В противном случае укажите **binary**. Значение по умолчанию — **text**.
- Если `options.uploadMode` имеет значение **file**, а `options.openMode` имеет значение **binary**, то выходные данные закодированы в формате Base64.
- `options.encoding` — указывает кодирование, которое используется при чтении файла. Значение по умолчанию — **UTF-8**, которое используется только если для параметра `options.openMode` задано значение **text**.

## <a name="sample-output"></a>Пример выходных данных
Если options.multiple имеет значение false и options.uploadMode — file, тогда выходные данные предоставляют содержимое файла в виде строки JSON:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Если options.multiple имеет значение true и options.uploadMode — file, тогда выходные данные предоставляют содержимое файла в виде массива JSON:

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

Если options.multiple имеет значение false и uploadMode — url, тогда выходные данные содержат ULR-адрес в виде строки JSON:

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

Если options.multiple имеет значение true и uploadMode — url, тогда выходные данные содержат список ULR-адресов в виде массива JSON:
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

При тестировании определения CreateUiDefinition некоторые браузеры (например, Google Chrome) обрезают ULR-адреса, созданные элементом Microsoft.Common.FileUpload, в консоли браузера. Чтобы скопировать полные URL-адреса, вам может потребоваться щелкнуть правой кнопкой мыши отдельные ссылки.


## <a name="next-steps"></a>Дальнейшие действия
* Общие сведения об управляемых приложениях Azure см. в [этой статье](overview.md).
* Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](create-uidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](create-uidefinition-elements.md).
