---
title: "aaaAzure управляемые приложения создайте определения функций пользовательского интерфейса | Документы Microsoft"
description: "Описывает toouse функции hello при создании определения пользовательского интерфейса для управляемого приложения Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>Элементы CreateUiDefinition
В этой статье описываются hello схему и свойства для всех поддерживаемых элементов CreateUiDefinition. Эти элементы используются при [создании управляемого приложения Azure](managed-application-publishing.md). Схема Hello для большинства элементов выглядит следующим образом:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Свойство | Обязательно | Description (Описание) |
| -------- | -------- | ----------- |
| name | Да | Tooreference внутренний идентификатор конкретного экземпляра элемента. Hello наиболее распространенное использование имени элемента hello находится в `outputs`, если не указано hello выходные значения hello элементы, сопоставленные toohello параметры шаблона hello. Ее можно также использовать toobind hello выходное значение элемента toohello `defaultValue` другого элемента. |
| type | Да | Hello toorender элемента управления пользовательского интерфейса для элемента hello. Список поддерживаемых типов см. в разделе [Элементы](#elements). |
| label | Да | Hello отображать текст hello элемента. Некоторые типы элементов содержат несколько меток, поэтому hello значение может быть объектом, содержащим несколько строк. |
| defaultValue | Нет | значение по умолчанию Hello hello элемента. Некоторые типы элементов поддерживает значения по умолчанию сложным, поэтому hello значение может быть объектом. |
| toolTip | Нет | toodisplay текст Hello hello всплывающая подсказка элемента hello. Аналогичные слишком`label`, некоторые элементы поддерживают несколько строк совет средство. С помощью синтаксиса Markdown можно внедрить встроенные ссылки.
| constraints | Нет | Одно или несколько свойств, используемых toocustomize hello проверки поведения элемента hello. свойства Hello поддерживается для ограничения зависят от типа элемента. Некоторые типы элементов не поддерживают настройку поведения проверки hello и таким образом нет свойства ограничения. |
| options | Нет | Дополнительные свойства для настройки способа hello hello элемента. Аналогичные слишком`constraints`, hello поддерживается свойства зависят от типа элемента. |
| visible | Нет | Указывает, отображается ли элемент hello. Если `true`, отображаются hello и дочерних элементов. значение по умолчанию Hello — `true`. Используйте [логические функции](managed-application-createuidefinition-functions.md#logical-functions) toodynamically контроля значения этого свойства.

## <a name="elements"></a>Элементы

Здравствуйте, документация для каждого элемента содержит пример пользовательского интерфейса, схемы, примечания на поведение hello элемента hello (обычно используемого для проверки и поддерживаемые настройки), а также пример выходных данных.

- [Элемент пользовательского интерфейса Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Элемент пользовательского интерфейса Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Элемент пользовательского интерфейса Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Элемент пользовательского интерфейса Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Элемент пользовательского интерфейса Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Элемент пользовательского интерфейса Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Элемент пользовательского интерфейса Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Элемент пользовательского интерфейса Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Элемент пользовательского интерфейса Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Элемент пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Элемент пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Элемент пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Элемент пользовательского интерфейса Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Дальнейшие действия
* Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).
* Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).
