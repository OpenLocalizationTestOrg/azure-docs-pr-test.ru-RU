---
title: "Определение дочернего ресурса в шаблоне Azure | Документация Майкрософт"
description: "В этой статье показано, как задать тип и имя дочернего ресурса в шаблоне Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>Указание имени и типа дочернего ресурса в шаблоне Resource Manager
При создании шаблона нередко требуется добавить в него дочерний ресурс, связанный с родительским ресурсом. Например, шаблон может содержать сервер SQL Server и базу данных. Сервер SQL Server является родительским ресурсом, а база данных — дочерним. 

Формат типа дочернего ресурса: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

Формат имени дочернего ресурса: `{parent-resource-name}/{child-resource-name}`

Тип и имя указываются в шаблоне по-разному в зависимости от того, является ли дочерний ресурс вложенным в родительский ресурс или самостоятельным ресурсом на верхнем уровне. В этой статье описываются оба варианта.

При создании полной ссылки на ресурс порядок объединения сегментов из типа и имени представляет собой не только использование этих двух вариантов.  Вместо этого после пространства имен используйте пары *типа и имени*, начиная от наименее подходящей к наиболее подходящей.

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

Например:

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` — правильно, `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` — неправильно.

## <a name="nested-child-resource"></a>Вложенный дочерний ресурс
Самый простой способ определить дочерний ресурс — вложить его в родительский ресурс. В следующем примере показана база данных SQL, вложенная в сервер SQL Server.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

Для дочернего ресурса задается тип `databases`, но его полным типом ресурса является `Microsoft.Sql/servers/databases`. `Microsoft.Sql/servers/` не указывается, так как предполагается из типа родительского ресурса. Дочернему ресурсу присваивается имя `exampledatabase`, но его полное имя включает в себя имя родительского ресурса. `exampleserver` не указывается, так как предполагается из родительского ресурса.

## <a name="top-level-child-resource"></a>Дочерний ресурс верхнего уровня
Дочерний ресурс можно определить на верхнем уровне. Этот подход можно использовать, если родительский ресурс не развертывается в том же шаблоне или требуется использовать `copy` для создания нескольких дочерних ресурсов. В этом случае нужно указать полный тип ресурса и добавить в имя дочернего ресурса имя родительского ресурса.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

База данных является дочерним ресурсом для сервера, даже если они определены на одном уровне в шаблоне.

## <a name="next-steps"></a>Дальнейшие действия
* См. дополнительные рекомендации по [созданию шаблонов Azure Resource Manager](resource-manager-template-best-practices.md).
* Пример создания нескольких дочерних ресурсов см. в разделе [Развертывание нескольких экземпляров ресурсов в шаблонах Azure Resource Manager](resource-group-create-multiple.md).
