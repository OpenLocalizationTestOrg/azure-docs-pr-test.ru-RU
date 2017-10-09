---
title: "aaaConvert масштабе диспетчера ресурсов Azure задайте управляемого диска toouse шаблона | Документы Microsoft"
description: "Преобразуйте шкалы набор шаблонов tooa управляемого диска шкалы набор шаблон."
keywords: "наборы масштабирования виртуальных машин"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>Преобразовать шкалы набор шаблонов tooa управляемого диска шкалы набор шаблон

Клиенты с помощью шаблона диспетчера ресурсов для создания наборе не с помощью управляемого диска масштабирования можно назвать toomodify его toouse управляемого диска. В этой статье показано, как toodo это, используя в качестве примера запрос на включение из hello [шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates), сообщество ведет репозитория для образца шаблонов диспетчера ресурсов. Здесь можно увидеть полную запросу Hello: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), и hello соответствующих частей hello различий между приведены ниже, а также описания:

## <a name="making-hello-os-disks-managed"></a>Создание управляемых диски ОС hello

В ниже diff hello мы видим, что мы удалили несколько связанных toostorage учетной записи и диск свойства переменных. Тип учетной записи хранения больше не требуется (Standard_LRS является hello по умолчанию), но мы может по-прежнему указывать, если мы хотели. Для управляемых дисков поддерживаются только типы Standard_LRS и Premium_LRS. Новый суффикс учетной записи хранилища, уникальная строка массива и число sa использовались в hello старый шаблон toogenerate имена учетной записи хранения. Эти переменные более не нужны в новый шаблон hello поскольку управляемого диска автоматически создает учетные записи хранения на основе имени пользователя hello. Аналогичным образом имя контейнера vhd и имя диска ОС отпала поскольку управляемого диска автоматически имени hello базовой контейнеров больших двоичных объектов хранилища и дисков.

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


В diff hello ниже мы можно см. в разделе, обновлены hello вычислить api версии too2016-04-30-preview, являющееся hello самой ранней требуемую версию для поддержки управляемого диска с набора масштабирования. Обратите внимание, что может по-прежнему используется неуправляемый дисков в новой версии api hello с Здравствуй, старый синтаксис при необходимости. Другими словами если только обновить hello вычислений версия api и не вносите никаких других изменений, hello шаблона следует продолжить toowork как перед.

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

В ниже diff hello мы видим, что мы удаляем hello ресурс учетной записи хранения из массива hello ресурсы полностью. Он нам не нужен, так как управляемый диск автоматически создает учетные записи от нашего имени.

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

В diff hello ниже мы можно см. в разделе мы удаляем hello зависит от предложения ссылками из hello шкалы набор toohello цикл, который Создание учетных записей хранилища. В hello старый шаблон это убедившись, что учетные записи хранения hello были создан до набора масштабирования hello начала создания, но это предложение больше не требуется для управляемого диска. Мы также удалить свойство контейнеры vhd hello и hello свойством имя диска ОС, как эти свойства автоматически обрабатываются кулисами hello управляемого диска. Если мы желавших, мы добавим `"managedDisk": { "storageAccountType": "Premium_LRS" }` в конфигурации «osDisk» hello, если бы мы хотели ОС дисков "премиум". Только виртуальные машины с заглавных букв или в нижнем регистре "в hello ВМ sku можно использовать диски premium.

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

Нет явного свойства в конфигурации набора масштабирования hello ли toouse управляемые или неуправляемые диска. набор масштабирования Hello знает, какой toouse на основе свойств hello, которые присутствуют в профиле хранилища hello. Таким образом важно при изменении tooensure шаблона hello, свойства прав hello в профиле хранилища hello набора масштабирования hello.


## <a name="data-disks"></a>Диски данных

С изменениями hello выше hello шкалы набор использует управляемый дисков для hello ОС на диске, но что о дисках с данными? tooadd диски с данными, добавьте hello свойства «dataDisks» в разделе «storageProfile» в hello же уровня, как «osDisk». Hello значение свойства hello является JSON список объектов, каждый из которых имеет свойства «lun» (он должен быть уникальным для каждого диска данных на виртуальной Машине), «createOption» («Очистить» является в настоящее время hello параметр поддерживается только) и «diskSizeGB» (hello размер hello диска в гигабайтах, должны быть больше 0 и меньше 1024) как в hello в следующем примере: 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

При указании `n` дисков в этом массиве каждой виртуальной Машины на шкале hello задать возвращает `n` диски с данными. Но при этом не забывайте, что эти диски данных — необработанные устройства. Они не отформатированы. Это tooattach toohello клиента, раздела и диски в формате hello перед их использованием. Кроме того, мы также можно указать `"managedDisk": { "storageAccountType": "Premium_LRS" }` в каждый объект toospecify диск данных, следует использовать диск данных premium. Только виртуальные машины с заглавных букв или в нижнем регистре "в hello ВМ sku можно использовать диски premium.

toolearn Подробнее об использовании дисков с данными с помощью набора масштабирования в разделе [в этой статье](./virtual-machine-scale-sets-attached-disks.md).


## <a name="next-steps"></a>Дальнейшие действия
Например шаблоны диспетчера ресурсов, с помощью набора масштабирования, поиска «vmss» в hello [шаблоны быстрый запуск Azure в репозитории github](https://github.com/Azure/azure-quickstart-templates).

Для получения общих сведений посетите hello [Главная целевая страница для набора масштабирования](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

