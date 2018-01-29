---
title: "Элемент пользовательского интерфейса MultiStorageAccountCombo управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo для управляемых приложений Azure"
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
ms.openlocfilehash: e1dda7917988146807ca6cfab10a3a4eac0b7bb2
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo
Группа элементов управления для создания нескольких учетных записей хранения с именами, которые начинаются с общего префикса. Этот элемент используется при [создании управляемого приложения Azure](publish-service-catalog-app.md).

## <a name="ui-sample"></a>Пример элемента пользовательского интерфейса
![Элемент пользовательского интерфейса Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a>Схема
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Примечания
- Значение для `defaultValue.prefix` объединяется с одним или несколькими целыми числами для создания последовательности имен учетных записей хранения. Например, если для параметра `defaultValue.prefix` задано значение **foobar**, а для параметра `count` задано значение **2**, тогда создаются имена учетной записи хранения **foobar1** и **foobar2**. Созданные имена учетных записей хранения автоматически проверяются на уникальность.
- Имена учетных записей хранения формируются лексикографически на основе `count`. Например, если для параметра `count` задано значение 10, тогда имена учетных записей хранения будут заканчиваться на двухзначное число (01, 02, 03 и т. д.).
- Значением по умолчанию для параметра `defaultValue.prefix` является **null**, а для параметра `defaultValue.type` — **Premium_LRS**.
- Любой тип, не указанный в `constraints.allowedTypes`, скрыт, а любой тип, не указанный в `constraints.excludedTypes`, отображается.
Параметры `constraints.allowedTypes` и `constraints.excludedTypes` являются необязательными. При этом их нельзя использовать одновременно.
- Кроме создания имен учетных записей хранения, параметр `count` используется, чтобы задать соответствующее число для элемента. Он поддерживает статическое значение, например **2**, или динамическое значение из другого элемента, например `[steps('step1').storageAccountCount]`. Значение по умолчанию — **1**.

## <a name="sample-output"></a>Пример выходных данных
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a>Дальнейшие действия
* Общие сведения об управляемых приложениях Azure см. в [этой статье](overview.md).
* Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](create-uidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](create-uidefinition-elements.md).
