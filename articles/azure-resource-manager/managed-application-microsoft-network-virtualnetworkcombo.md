---
title: "элемент управляемого пользовательского интерфейса приложения VirtualNetworkCombo aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo для управляемых приложений Azure"
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Элемент пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo
Группа элементов управления для выбора новой или имеющейся виртуальной сети. Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Пример элемента пользовательского интерфейса
![Элемент пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- В верхней каркаса hello пользователь hello выбравший новую виртуальную сеть, поэтому hello пользователь может настроить префикса имя и адрес каждой подсети. Настройка подсетей в этом случае является необязательной.
- В каркас нижней hello hello пользователь, выбравший существующей виртуальной сети, поэтому hello пользователя необходимо сопоставить каждой подсети hello развертывания шаблона требуется tooan существующей подсети. Настройка подсетей в этом случае является обязательной.

## <a name="schema"></a>Схема
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>Примечания
- Если указано, hello первый неперекрывающиеся префикс адреса размер `defaultValue.addressPrefixSize` определяется автоматически на основании существующих виртуальных сетей в подписке hello пользователя.
- Здравствуйте, значение по умолчанию для `defaultValue.name` и `defaultValue.addressPrefixSize` — **null**.
- Обязательно должен быть указан параметр `constraints.minAddressPrefixSize`. Все существующие виртуальные сети с адресным пространством меньше, чем hello указанное значение, становятся недоступными для выбора.
- Для каждой подсети должны быть определены `subnets` и `constraints.minAddressPrefixSize`.
- При создании новой виртуальной сети, префикс адреса для каждой подсети вычисляется автоматически на основе префикса адреса hello виртуальной сети, а соответствующее `addressPrefixSize`.
- При использовании имеющейся виртуальной сети любые подсети со значением меньше, чем у `constraints.minAddressPrefixSize`, — недоступны. Кроме того (если указано), подсети, которые не содержат минимальное число доступных адресов (`minAddressCount`), — недоступны.
значение по умолчанию Hello — **0**. tooensure, hello доступных адресов являются смежными, укажите **true** для `requireContiguousAddresses`. значение по умолчанию Hello — **true**.
- Создание подсетей в имеющейся виртуальной сети не поддерживается.
- Если `options.hideExisting` — **true**, hello пользователь не может выбрать существующую виртуальную сеть. значение по умолчанию Hello — **false**.

## <a name="sample-output"></a>Пример выходных данных
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>Дальнейшие действия
* Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).
* Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).
