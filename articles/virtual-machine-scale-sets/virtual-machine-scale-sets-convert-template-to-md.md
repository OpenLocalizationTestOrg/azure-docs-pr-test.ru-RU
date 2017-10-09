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
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="d5236-104">Преобразовать шкалы набор шаблонов tooa управляемого диска шкалы набор шаблон</span><span class="sxs-lookup"><span data-stu-id="d5236-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="d5236-105">Клиенты с помощью шаблона диспетчера ресурсов для создания наборе не с помощью управляемого диска масштабирования можно назвать toomodify его toouse управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="d5236-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="d5236-106">В этой статье показано, как toodo это, используя в качестве примера запрос на включение из hello [шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates), сообщество ведет репозитория для образца шаблонов диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d5236-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="d5236-107">Здесь можно увидеть полную запросу Hello: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), и hello соответствующих частей hello различий между приведены ниже, а также описания:</span><span class="sxs-lookup"><span data-stu-id="d5236-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="d5236-108">Создание управляемых диски ОС hello</span><span class="sxs-lookup"><span data-stu-id="d5236-108">Making hello OS disks managed</span></span>

<span data-ttu-id="d5236-109">В ниже diff hello мы видим, что мы удалили несколько связанных toostorage учетной записи и диск свойства переменных.</span><span class="sxs-lookup"><span data-stu-id="d5236-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="d5236-110">Тип учетной записи хранения больше не требуется (Standard_LRS является hello по умолчанию), но мы может по-прежнему указывать, если мы хотели.</span><span class="sxs-lookup"><span data-stu-id="d5236-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="d5236-111">Для управляемых дисков поддерживаются только типы Standard_LRS и Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="d5236-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="d5236-112">Новый суффикс учетной записи хранилища, уникальная строка массива и число sa использовались в hello старый шаблон toogenerate имена учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d5236-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="d5236-113">Эти переменные более не нужны в новый шаблон hello поскольку управляемого диска автоматически создает учетные записи хранения на основе имени пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="d5236-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="d5236-114">Аналогичным образом имя контейнера vhd и имя диска ОС отпала поскольку управляемого диска автоматически имени hello базовой контейнеров больших двоичных объектов хранилища и дисков.</span><span class="sxs-lookup"><span data-stu-id="d5236-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="d5236-115">В diff hello ниже мы можно см. в разделе, обновлены hello вычислить api версии too2016-04-30-preview, являющееся hello самой ранней требуемую версию для поддержки управляемого диска с набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d5236-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="d5236-116">Обратите внимание, что может по-прежнему используется неуправляемый дисков в новой версии api hello с Здравствуй, старый синтаксис при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d5236-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="d5236-117">Другими словами если только обновить hello вычислений версия api и не вносите никаких других изменений, hello шаблона следует продолжить toowork как перед.</span><span class="sxs-lookup"><span data-stu-id="d5236-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

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

<span data-ttu-id="d5236-118">В ниже diff hello мы видим, что мы удаляем hello ресурс учетной записи хранения из массива hello ресурсы полностью.</span><span class="sxs-lookup"><span data-stu-id="d5236-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="d5236-119">Он нам не нужен, так как управляемый диск автоматически создает учетные записи от нашего имени.</span><span class="sxs-lookup"><span data-stu-id="d5236-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="d5236-120">В diff hello ниже мы можно см. в разделе мы удаляем hello зависит от предложения ссылками из hello шкалы набор toohello цикл, который Создание учетных записей хранилища.</span><span class="sxs-lookup"><span data-stu-id="d5236-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="d5236-121">В hello старый шаблон это убедившись, что учетные записи хранения hello были создан до набора масштабирования hello начала создания, но это предложение больше не требуется для управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="d5236-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="d5236-122">Мы также удалить свойство контейнеры vhd hello и hello свойством имя диска ОС, как эти свойства автоматически обрабатываются кулисами hello управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="d5236-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="d5236-123">Если мы желавших, мы добавим `"managedDisk": { "storageAccountType": "Premium_LRS" }` в конфигурации «osDisk» hello, если бы мы хотели ОС дисков "премиум".</span><span class="sxs-lookup"><span data-stu-id="d5236-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="d5236-124">Только виртуальные машины с заглавных букв или в нижнем регистре "в hello ВМ sku можно использовать диски premium.</span><span class="sxs-lookup"><span data-stu-id="d5236-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

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

<span data-ttu-id="d5236-125">Нет явного свойства в конфигурации набора масштабирования hello ли toouse управляемые или неуправляемые диска.</span><span class="sxs-lookup"><span data-stu-id="d5236-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="d5236-126">набор масштабирования Hello знает, какой toouse на основе свойств hello, которые присутствуют в профиле хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="d5236-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="d5236-127">Таким образом важно при изменении tooensure шаблона hello, свойства прав hello в профиле хранилища hello набора масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="d5236-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="d5236-128">Диски данных</span><span class="sxs-lookup"><span data-stu-id="d5236-128">Data disks</span></span>

<span data-ttu-id="d5236-129">С изменениями hello выше hello шкалы набор использует управляемый дисков для hello ОС на диске, но что о дисках с данными? tooadd диски с данными, добавьте hello свойства «dataDisks» в разделе «storageProfile» в hello же уровня, как «osDisk».</span><span class="sxs-lookup"><span data-stu-id="d5236-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="d5236-130">Hello значение свойства hello является JSON список объектов, каждый из которых имеет свойства «lun» (он должен быть уникальным для каждого диска данных на виртуальной Машине), «createOption» («Очистить» является в настоящее время hello параметр поддерживается только) и «diskSizeGB» (hello размер hello диска в гигабайтах, должны быть больше 0 и меньше 1024) как в hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="d5236-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="d5236-131">При указании `n` дисков в этом массиве каждой виртуальной Машины на шкале hello задать возвращает `n` диски с данными.</span><span class="sxs-lookup"><span data-stu-id="d5236-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="d5236-132">Но при этом не забывайте, что эти диски данных — необработанные устройства.</span><span class="sxs-lookup"><span data-stu-id="d5236-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="d5236-133">Они не отформатированы.</span><span class="sxs-lookup"><span data-stu-id="d5236-133">They are not formatted.</span></span> <span data-ttu-id="d5236-134">Это tooattach toohello клиента, раздела и диски в формате hello перед их использованием.</span><span class="sxs-lookup"><span data-stu-id="d5236-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="d5236-135">Кроме того, мы также можно указать `"managedDisk": { "storageAccountType": "Premium_LRS" }` в каждый объект toospecify диск данных, следует использовать диск данных premium.</span><span class="sxs-lookup"><span data-stu-id="d5236-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="d5236-136">Только виртуальные машины с заглавных букв или в нижнем регистре "в hello ВМ sku можно использовать диски premium.</span><span class="sxs-lookup"><span data-stu-id="d5236-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="d5236-137">toolearn Подробнее об использовании дисков с данными с помощью набора масштабирования в разделе [в этой статье](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="d5236-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d5236-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5236-138">Next steps</span></span>
<span data-ttu-id="d5236-139">Например шаблоны диспетчера ресурсов, с помощью набора масштабирования, поиска «vmss» в hello [шаблоны быстрый запуск Azure в репозитории github](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="d5236-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="d5236-140">Для получения общих сведений посетите hello [Главная целевая страница для набора масштабирования](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="d5236-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

