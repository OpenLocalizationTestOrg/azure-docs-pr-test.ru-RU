---
title: "Указание настраиваемого образа в шаблоне масштабируемого набора Azure | Документация Майкрософт"
description: "Узнайте, как tooadd пользовательского образа tooan существующего шаблона Azure масштабный набор виртуальных машин"
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>Добавить пользовательский образ tooan масштабирование Azure задать шаблон

В этой статье показано, как toomodify hello [Минимальный масштаб допустимого шаблона набора](./virtual-machine-scale-sets-mvss-start.md) toodeploy из пользовательского образа.

## <a name="change-hello-template-definition"></a>Измените определение шаблона hello

Наш шаблон Минимальный масштаб допустимого набора может видеть [здесь](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), и можно будет увидеть нашей шаблон для развертывания набора с помощью пользовательского образа шкалы hello [здесь](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Давайте рассмотрим toocreate hello diff использовать этот шаблон (`git diff minimum-viable-scale-set custom-image`) по частям:

### <a name="creating-a-managed-disk-image"></a>Создание образа управляемого диска

Если вы уже создали настраиваемый образ управляемого диска (ресурс типа `Microsoft.Compute/images`), можете пропустить этот раздел.

Во-первых, мы добавляем `sourceImageVhdUri` параметра, который является hello URI toohello обобщенный blob в хранилище Azure, содержащий toodeploy hello пользовательского образа из.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

Далее добавим ресурс типа `Microsoft.Compute/images`, который основан на hello обобщенный большой двоичный объект, расположенный в URI изображения hello управляемого диска `sourceImageVhdUri`. Этот образ должен находиться в hello же регионе, что набор масштабирования hello, который его использует. В свойствах образа hello hello мы укажите тип hello ОС, расположение hello hello BLOB-объекта (из hello `sourceImageVhdUri` параметра) и тип учетной записи хранения hello:

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

В hello набора масштабирования ресурсов, мы добавим `dependsOn` предложение ссылается toomake пользовательского образа toohello убедиться, что изображение hello создается до набора масштабирования hello пытается toodeploy из этого образа:

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>Изменение масштаба задать свойства toouse hello управляемого диска изображение

В hello `imageReference` шкалы hello задать `storageProfile`, вместо указания hello издателя, предложение, sku и версия образа платформы, мы указываем hello `id` из hello `Microsoft.Compute/images` ресурсов:

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

В этом примере мы используем hello `resourceId` созданные tooget функции hello идентификатор ресурса изображения hello в hello же шаблона. Если заранее после создания образа управляемого диска hello, необходимо предоставить идентификатор hello этого образа вместо. Этот идентификатор должен иметь форму hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
