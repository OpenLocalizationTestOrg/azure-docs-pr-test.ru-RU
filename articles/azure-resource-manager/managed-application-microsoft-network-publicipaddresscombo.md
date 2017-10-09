---
title: "элемент управляемого пользовательского интерфейса приложения PublicIpAddressCombo aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo для управляемых приложений Azure"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo
Группа элементов управления для выбора нового или имеющегося общедоступного IP-адреса. Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Пример элемента пользовательского интерфейса
![Элемент пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Если пользователь hello выбирает «None» для общедоступного IP-адреса, hello домена имя метки текстовое поле будет скрыта.
- Если пользователь hello выбирает существующий общедоступный IP-адрес, hello домена имя метки текстовое поле будет отключено. Его значением является метка доменного имени hello hello выбранных IP-адреса.
- Здравствуйте обновлений суффикс (например, westus.cloudapp.azure.com) имя домена, автоматически на основе hello выбранного расположения.

## <a name="schema"></a>Схема
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>Примечания
- Если `constraints.required.domainNameLabel` задано слишком**true**, hello пользователь должен предоставить метку имени домена, создавая новый общедоступный IP-адрес. Имеющиеся общедоступные IP-адреса без метки недоступны для выбора.
- Если `options.hideNone` задано слишком**true**, затем hello параметр tooselect **нет** hello открытый IP-адрес скрыт. значение по умолчанию Hello — **false**.
- Если `options.hideDomainNameLabel` задано слишком**true**, скрыта hello текстовое поле для метка доменного имени. значение по умолчанию Hello — **false**.
- Если `options.hideExisting` имеет значение true, то пользователь hello не может toochoose существующий общедоступный IP-адрес. значение по умолчанию Hello — **false**.

## <a name="sample-output"></a>Пример выходных данных
Если hello пользователь выбирает не общедоступный IP-адрес, hello следующий результат является ожидаемым:
```json
{
  "newOrExistingOrNone": "none"
}
```

Если hello пользователь выбирает новый или существующий IP-адрес, hello следующий результат является ожидаемым:
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- При указании `options.hideNone` `newOrExistingOrNone` всегда возвращает значение **none**.
- При указании `options.hideDomainNameLabel` `domainNameLabel` не объявляется.

## <a name="next-steps"></a>Дальнейшие действия
* Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).
* Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).
