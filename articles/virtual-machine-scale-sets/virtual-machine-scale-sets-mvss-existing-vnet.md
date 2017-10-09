---
title: "Указание существующей виртуальной сети в шаблоне масштабируемого набора Azure | Документация Майкрософт"
description: "Узнайте, как tooadd в виртуальной сети tooan существующего шаблона набора масштабирования виртуальных машин Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
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
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>Добавить ссылку tooan существующей виртуальной сети в шаблоне набор масштабирование Azure

В этой статье показано, как toomodify hello [Минимальный масштаб допустимого шаблона набора](./virtual-machine-scale-sets-mvss-start.md) toodeploy в рамках существующей виртуальной сети, вместо создания нового.

## <a name="change-hello-template-definition"></a>Измените определение шаблона hello

Наш шаблон Минимальный масштаб допустимого набора может видеть [здесь](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), и можно будет увидеть нашей шаблон для развертывания наборе в существующей виртуальной сети масштабирования hello [здесь](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Давайте рассмотрим toocreate hello diff использовать этот шаблон (`git diff minimum-viable-scale-set existing-vnet`) по частям:

Сначала мы добавим параметр `subnetId`. Эта строка будет передан в конфигурацию набора масштабирования hello, позволяя шкалы hello набора предварительно созданных подсети hello tooidentify toodeploy виртуальных машин в. Эта строка должна быть в формате hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Для экземпляра набора масштабирования toodeploy hello в существующей виртуальной сети с именем `myvnet`, подсети `mysubnet`, группа ресурсов `myrg`, подписки и `00000000-0000-0000-0000-000000000000`, будет hello subnetId: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

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

Затем можно удалить ресурс виртуального сетевого hello из hello `resources` массива, потому что используется существующей виртуальной сети и нет необходимости toodeploy новый.

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

Hello виртуальной сети уже существует, прежде чем развертывать hello шаблона, поэтому нет необходимости toospecify предложение dependsOn от шкалы hello задан toohello виртуальной сети. Следовательно, мы удаляем такие строки:

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

Наконец, мы передаем hello `subnetId` параметра устанавливается пользователем hello (вместо использования `resourceId` tooget hello идентификатор виртуальной сети в hello же развертывания шаблона набор какие Минимальный масштаб реальную hello).

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
