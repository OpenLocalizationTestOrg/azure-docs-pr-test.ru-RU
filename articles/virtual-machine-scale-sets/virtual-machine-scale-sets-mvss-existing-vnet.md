---
title: "Указание существующей виртуальной сети в шаблоне масштабируемого набора Azure | Документация Майкрософт"
description: "Узнайте, как добавить виртуальную сеть в существующий шаблон масштабируемого набора виртуальных машин Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: eb35975de5864e129f97b614a61487456dd972ef
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/20/2017
---
# <a name="add-reference-to-an-existing-virtual-network-in-an-azure-scale-set-template"></a>Добавление ссылки на существующую виртуальную сеть в шаблон масштабируемого набора Azure

В этой статье показано, как изменить [шаблон минимального приемлемого масштабируемого набора](./virtual-machine-scale-sets-mvss-start.md) для развертывания в существующей виртуальной сети вместо создания новой.

## <a name="change-the-template-definition"></a>Изменение определения шаблона

Шаблон Минимальный масштаб допустимого набора может видеть [здесь](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), и шаблон для развертывания наборе в существующей виртуальной сети масштабирования можно будет увидеть [здесь](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Давайте рассмотрим DIFF-файл, с помощью которого можно постепенно создать этот шаблон (`git diff minimum-viable-scale-set existing-vnet`).

Сначала добавьте `subnetId` параметра. Эта строка передается в конфигурацию набора масштабирования, позволяя шкалы, задайте для идентификации предварительно созданной для развертывания виртуальных машин в подсети. Эта строка должна иметь следующий формат: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Например, чтобы развернуть масштабируемый набор в существующей виртуальной сети с именем `myvnet`, подсети `mysubnet`, группе ресурсов `myrg` и подписке `00000000-0000-0000-0000-000000000000`, идентификатор подсети должен быть таким: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

Затем удалите ресурс виртуальной сети из `resources` массива, как использовать существующую виртуальную сеть и не требуется развернуть новое.

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

Виртуальная сеть уже существовала до развертывания шаблона, поэтому нет необходимости указывать предложение dependsOn из масштабируемого набора для виртуальной сети. Удалите следующие строки:

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

Наконец, передайте в `subnetId` пользователь задал параметр (вместо использования `resourceId` Чтобы получить идентификатор виртуальной сети в одном развертывании, не являющийся содержимое Минимальный масштаб допустимого набора шаблона).

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
