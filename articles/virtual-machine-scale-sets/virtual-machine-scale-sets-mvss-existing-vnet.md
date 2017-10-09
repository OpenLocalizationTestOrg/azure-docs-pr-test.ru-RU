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
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="dbe27-103">Добавить ссылку tooan существующей виртуальной сети в шаблоне набор масштабирование Azure</span><span class="sxs-lookup"><span data-stu-id="dbe27-103">Add reference tooan existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="dbe27-104">В этой статье показано, как toomodify hello [Минимальный масштаб допустимого шаблона набора](./virtual-machine-scale-sets-mvss-start.md) toodeploy в рамках существующей виртуальной сети, вместо создания нового.</span><span class="sxs-lookup"><span data-stu-id="dbe27-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="dbe27-105">Измените определение шаблона hello</span><span class="sxs-lookup"><span data-stu-id="dbe27-105">Change hello template definition</span></span>

<span data-ttu-id="dbe27-106">Наш шаблон Минимальный масштаб допустимого набора может видеть [здесь](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), и можно будет увидеть нашей шаблон для развертывания наборе в существующей виртуальной сети масштабирования hello [здесь](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="dbe27-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="dbe27-107">Давайте рассмотрим toocreate hello diff использовать этот шаблон (`git diff minimum-viable-scale-set existing-vnet`) по частям:</span><span class="sxs-lookup"><span data-stu-id="dbe27-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="dbe27-108">Сначала мы добавим параметр `subnetId`.</span><span class="sxs-lookup"><span data-stu-id="dbe27-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="dbe27-109">Эта строка будет передан в конфигурацию набора масштабирования hello, позволяя шкалы hello набора предварительно созданных подсети hello tooidentify toodeploy виртуальных машин в.</span><span class="sxs-lookup"><span data-stu-id="dbe27-109">This string will be passed into hello scale set configuration, allowing hello scale set tooidentify hello pre-created subnet toodeploy virtual machines into.</span></span> <span data-ttu-id="dbe27-110">Эта строка должна быть в формате hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="dbe27-110">This string must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="dbe27-111">Для экземпляра набора масштабирования toodeploy hello в существующей виртуальной сети с именем `myvnet`, подсети `mysubnet`, группа ресурсов `myrg`, подписки и `00000000-0000-0000-0000-000000000000`, будет hello subnetId: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="dbe27-111">For instance, toodeploy hello scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, hello subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

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

<span data-ttu-id="dbe27-112">Затем можно удалить ресурс виртуального сетевого hello из hello `resources` массива, потому что используется существующей виртуальной сети и нет необходимости toodeploy новый.</span><span class="sxs-lookup"><span data-stu-id="dbe27-112">Next, we can delete hello virtual network resource from hello `resources` array, since we are using an existing virtual network and don't need toodeploy a new one.</span></span>

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

<span data-ttu-id="dbe27-113">Hello виртуальной сети уже существует, прежде чем развертывать hello шаблона, поэтому нет необходимости toospecify предложение dependsOn от шкалы hello задан toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="dbe27-113">hello virtual network already exists before hello template is deployed, so there is no need toospecify a dependsOn clause from hello scale set toohello virtual network.</span></span> <span data-ttu-id="dbe27-114">Следовательно, мы удаляем такие строки:</span><span class="sxs-lookup"><span data-stu-id="dbe27-114">Thus, we delete these lines:</span></span>

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

<span data-ttu-id="dbe27-115">Наконец, мы передаем hello `subnetId` параметра устанавливается пользователем hello (вместо использования `resourceId` tooget hello идентификатор виртуальной сети в hello же развертывания шаблона набор какие Минимальный масштаб реальную hello).</span><span class="sxs-lookup"><span data-stu-id="dbe27-115">Finally, we pass in hello `subnetId` parameter set by hello user (instead of using `resourceId` tooget hello id of a vnet in hello same deployment, which is what hello minimum viable scale set template does).</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="dbe27-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dbe27-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
