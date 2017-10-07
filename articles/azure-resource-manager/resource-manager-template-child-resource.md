---
title: "aaaDefine дочерний ресурс в шаблоне Azure | Документы Microsoft"
description: "Показано, как tooset hello тип ресурса и имя для дочерних ресурса в шаблоне диспетчера ресурсов Azure"
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>Указание имени и типа дочернего ресурса в шаблоне Resource Manager
При создании шаблона, необходимо часто tooinclude дочерний ресурс, который является связанные tooa родительский ресурс. Например, шаблон может содержать сервер SQL Server и базу данных. Hello SQL server hello родительский ресурс, который hello базы данных hello дочерний ресурс. 

Hello hello дочерний ресурс типа выглядит следующим образом:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

Hello имени ресурса дочерних hello выглядит следующим образом:`{parent-resource-name}/{child-resource-name}`

Однако указать hello тип и имя в шаблоне по-разному на основе он вложен в родительский ресурс hello, или сам по себе на верхнем уровне hello. В этом разделе показано, как подход к toohandle оба.

При создании ресурса tooa полную ссылку, toocombine порядок hello сегменты из типа hello и имя не является просто объединение двух hello.  Вместо этого после приветствия имен, используйте последовательность *тип/имя* пар из определенного в указанном toomost:

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

Например:

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` — правильно, `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` — неправильно.

## <a name="nested-child-resource"></a>Вложенный дочерний ресурс
toodefine простым способом Hello дочерний ресурс является toonest его в родительский ресурс hello. Hello пример базы данных SQL, вложенных в SQL Server.

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

Для hello дочерних ресурса, тип hello установлен слишком`databases` , но его тип ресурсов — `Microsoft.Sql/servers/databases`. Не указано `Microsoft.Sql/servers/` так, как предполагалось, из типа ресурса родительского hello. слишком задано имя ресурса дочерних Hello`exampledatabase` но hello полное имя включает имя родительского hello. Не указано `exampleserver` так, как предполагалось, из родительского ресурса hello.

## <a name="top-level-child-resource"></a>Дочерний ресурс верхнего уровня
Можно определить hello дочерний ресурс на верхнем уровне hello. Этот подход можно использовать, если родительский ресурс hello не развернут в hello того же шаблона или, если хотите toouse `copy` toocreate несколько дочерние ресурсы. При таком подходе необходимо указать тип полного ресурса hello и включить имя родительского ресурса hello в имя ресурса дочернего hello.

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

Hello базы данных является дочерним сервером toohello ресурсов, даже если они определены в hello же уровня в шаблоне hello.

## <a name="next-steps"></a>Дальнейшие действия
* Рекомендации о том, как toocreate шаблонов, см. раздел [советы и рекомендации по созданию шаблонов диспетчера ресурсов Azure](resource-manager-template-best-practices.md).
* Пример создания нескольких дочерних ресурсов см. в разделе [Развертывание нескольких экземпляров ресурсов в шаблонах Azure Resource Manager](resource-group-create-multiple.md).
