---
title: "элемент пользовательского интерфейса FileUpload управляемого приложения aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Common.FileUpload для управляемых приложений Azure"
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Common.FileUpload
Элемент управления, позволяющий toospecify пользователя один или несколько файлов tooupload. Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).

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
- `constraints.accept`Указывает типы файлов, отображаемых в диалоговом окне браузера hello файл hello. В разделе hello [спецификации HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) для допустимых значений. значение по умолчанию Hello — **null**.
- Если `options.multiple` задано слишком**true**, tooselect более одного файла в диалоговом окне браузера hello файла разрешено пользователю hello. значение по умолчанию Hello — **false**.
- Этот элемент поддерживает отправку файлов в двух режимах на основе значения hello `options.uploadMode`. Если **файл** указан, выходной hello содержит hello содержимое файла hello как большой двоичный объект. Если **URL-адрес** указан, то файл hello отправленного tooa временное расположение, и результат hello содержит URL-адрес hello hello большого двоичного объекта. Временные большие двоичные объекты очищаются через 24 часа. значение по умолчанию Hello — **файл**.
- Здравствуйте, значение `options.openMode` определяет, как прочитать файл hello. Если файл hello ожидаемый toobe обычного текста, укажите **текст**; в противном случае, укажите **двоичных**. значение по умолчанию Hello — **текст**.
- Если `options.uploadMode` задано слишком**файл** и `options.openMode` задано слишком**двоичных**, hello выходные данные в кодировке base64.
- `options.encoding`Указывает кодировки toouse hello при чтении файла hello. значение по умолчанию Hello — **UTF-8**и используется только если `options.openMode` задано слишком**текст**.

## <a name="sample-output"></a>Пример выходных данных
Если options.multiple имеет значение false и options.uploadMode — файл, выходные данные содержат hello содержимое файла hello как строка JSON:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Если истинно options.multiple and'options.uploadMode файлом, то выходные данные содержат hello содержимое файлов hello как массив JSON:

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

При тестировании CreateUiDefinition, некоторые браузеры (например, Google Chrome) приводит к усечению URL-адреса, созданные элементом Microsoft.Common.FileUpload hello в консоли браузера hello. Может потребоваться tooright щелкните отдельные связи toocopy hello полные URL-адреса.


## <a name="next-steps"></a>Дальнейшие действия
* Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).
* Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).
