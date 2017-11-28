---
title: "Преобразование шаблона масштабируемого набора Azure Resource Manager для использования управляемого диска | Документация Майкрософт"
description: "Преобразование шаблона масштабируемого набора в соответствующий шаблон с управляемым диском."
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
ms.openlocfilehash: 2f5cb85703888c5056611d466f508547ee72e44b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="convert-a-scale-set-template-to-a-managed-disk-scale-set-template"></a><span data-ttu-id="99aee-104">Преобразование шаблона масштабируемого набора в соответствующий шаблон с управляемым диском.</span><span class="sxs-lookup"><span data-stu-id="99aee-104">Convert a scale set template to a managed disk scale set template</span></span>

<span data-ttu-id="99aee-105">Клиенты, которые с помощью шаблона Resource Manager создают масштабируемые наборы без поддержки управляемого диска, могут легко добавить поддержку управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="99aee-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span></span> <span data-ttu-id="99aee-106">В этой статье такое преобразование демонстрируется на примере создания запроса на включение внесенных изменений. (Опубликовано в [шаблонах быстрого запуска Azure](https://github.com/Azure/azure-quickstart-templates) — репозитории сообщества пользователей с примерами шаблонов Resource Manager.)</span><span class="sxs-lookup"><span data-stu-id="99aee-106">This article shows how to do this, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="99aee-107">Полную версию этого запроса можно увидеть здесь: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998). Все важные фрагменты, изменения и пояснения к ним приводятся в этой статье.</span><span class="sxs-lookup"><span data-stu-id="99aee-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span></span>

## <a name="making-the-os-disks-managed"></a><span data-ttu-id="99aee-108">Переход на управляемые диски ОС</span><span class="sxs-lookup"><span data-stu-id="99aee-108">Making the OS disks managed</span></span>

<span data-ttu-id="99aee-109">В следующем списке с описанием различий видно, что мы удалили несколько переменных, имеющих отношение к учетной записи хранения и свойствам диска.</span><span class="sxs-lookup"><span data-stu-id="99aee-109">In the diff below, we can see that we have removed several variables related to storage account and disk properties.</span></span> <span data-ttu-id="99aee-110">Тип учетной записи хранения больше не нужно указывать (по умолчанию используется тип Standard_LRS), но при желании это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="99aee-110">Storage account type is no longer necessary (Standard_LRS is the default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="99aee-111">Для управляемых дисков поддерживаются только типы Standard_LRS и Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="99aee-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="99aee-112">В старой версии шаблона для создания имен учетных записей хранения использовались следующие компоненты: суффикс учетной записи хранения, уникальный строковый массив и счетчик учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="99aee-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span></span> <span data-ttu-id="99aee-113">Эти переменные в новой версии шаблона не нужны, так как управляемый диск автоматически создает для клиента учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="99aee-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span></span> <span data-ttu-id="99aee-114">Также теперь не нужно указывать контейнер виртуального жесткого диска и имя диска ОС, ведь управляемый диск автоматически присваивает имена базовым контейнерам больших двоичных объектов и дискам хранилища.</span><span class="sxs-lookup"><span data-stu-id="99aee-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="99aee-115">В следующем списке различий видно, что мы изменили версию вычислительного API до выпуска 2016-04-30-preview. Это самая ранняя версия, поддерживающая управляемые диски с масштабируемыми наборами.</span><span class="sxs-lookup"><span data-stu-id="99aee-115">In the diff below, we can see that we updated the compute api version to 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="99aee-116">Обратите внимание, что в новой версии API можно использовать и неуправляемые диски, сохранив старый синтаксис обращений.</span><span class="sxs-lookup"><span data-stu-id="99aee-116">Note that we could still use unmanaged disks in the new api version with the old syntax if desired.</span></span> <span data-ttu-id="99aee-117">Таким образом, если мы изменим только версию вычислительного API, а все остальное сохраним без изменений, то и работать все будет как прежде.</span><span class="sxs-lookup"><span data-stu-id="99aee-117">In other words, if we only update the compute api version and don't change anything else, the template should continue to work as before.</span></span>

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

<span data-ttu-id="99aee-118">В следующем списке с описанием различий видно, что мы полностью удалили из массива ресурс учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="99aee-118">In the diff below, we can see that we are removing the storage account resource from the resources array completely.</span></span> <span data-ttu-id="99aee-119">Он нам не нужен, так как управляемый диск автоматически создает учетные записи от нашего имени.</span><span class="sxs-lookup"><span data-stu-id="99aee-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="99aee-120">В следующем списке с описанием различий видно, что удалены зависимости от предложения со ссылкой от масштабируемого набора к циклу, создающему учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="99aee-120">In the diff below, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span></span> <span data-ttu-id="99aee-121">В старом шаблоне эта часть кода отвечала за то, чтобы учетные записи хранения обязательно создавались перед созданием масштабируемого набора. С управляемым диском это условие выполнять не нужно.</span><span class="sxs-lookup"><span data-stu-id="99aee-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="99aee-122">Мы также удалили свойство контейнера виртуальных жестких дисков и имени диска операционной системы, так как они автоматически и прозрачно обрабатываются управляемым диском.</span><span class="sxs-lookup"><span data-stu-id="99aee-122">We also remove the vhd containers property, and the os disk name property as these properties are automatically handled under the hood by managed disk.</span></span> <span data-ttu-id="99aee-123">Если нам нужны диски ОС класса Premium, мы можем добавить `"managedDisk": { "storageAccountType": "Premium_LRS" }` в конфигурацию osDisk.</span><span class="sxs-lookup"><span data-stu-id="99aee-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="99aee-124">Диски класса Premium могут использоваться только такими виртуальными машинами, в номере SKU которых есть заглавная или строчная буква s.</span><span class="sxs-lookup"><span data-stu-id="99aee-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

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

<span data-ttu-id="99aee-125">Для использования управляемого или неуправляемого диска не существует явным образом указанного свойства в конфигурации масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="99aee-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span></span> <span data-ttu-id="99aee-126">Масштабируемый набор выбирает, какой диск будет использоваться с учетом свойств, присутствующих в профиле хранилища.</span><span class="sxs-lookup"><span data-stu-id="99aee-126">The scale set knows which to use based on the properties that are present in the storage profile.</span></span> <span data-ttu-id="99aee-127">Поэтому при изменении шаблона важно обеспечить наличие правильных свойств в профиле хранения для масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="99aee-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="99aee-128">Диски данных</span><span class="sxs-lookup"><span data-stu-id="99aee-128">Data disks</span></span>

<span data-ttu-id="99aee-129">После внесения всех этих изменений масштабируемый набор будет использовать управляемые диски для операционной системы. Но что нам делать с дисками данных?</span><span class="sxs-lookup"><span data-stu-id="99aee-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span></span> <span data-ttu-id="99aee-130">Чтобы добавить диски данных, включите параметр dataDisks в раздел storageProfile на том же уровне, где расположен osDisk.</span><span class="sxs-lookup"><span data-stu-id="99aee-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span></span> <span data-ttu-id="99aee-131">Значение этого свойства содержит список объектов JSON, каждый из которых включает следующие свойства: lun (которое должно быть уникальным для каждого диска данных на виртуальной машине), createOption (сейчас поддерживается только значение empty) и diskSizeGB (размер диска в гигабайтах, допускаются значения в пределах от 0 до 1024). Ниже представлен пример такого списка:</span><span class="sxs-lookup"><span data-stu-id="99aee-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="99aee-132">Если в этот массив вы включите диски `n`, каждая виртуальная машина в масштабируемом наборе получит диски данных `n`.</span><span class="sxs-lookup"><span data-stu-id="99aee-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span></span> <span data-ttu-id="99aee-133">Но при этом не забывайте, что эти диски данных — необработанные устройства.</span><span class="sxs-lookup"><span data-stu-id="99aee-133">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="99aee-134">Они не отформатированы.</span><span class="sxs-lookup"><span data-stu-id="99aee-134">They are not formatted.</span></span> <span data-ttu-id="99aee-135">Все операции по подключению, разбиению и форматированию клиент должен выполнить самостоятельно, прежде чем использовать эти диски.</span><span class="sxs-lookup"><span data-stu-id="99aee-135">It is up to the customer to attach, paritition, and format the disks before using them.</span></span> <span data-ttu-id="99aee-136">При необходимости можно также настроить `"managedDisk": { "storageAccountType": "Premium_LRS" }` в каждом объекте диска данных использование дисков класса Premium.</span><span class="sxs-lookup"><span data-stu-id="99aee-136">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span></span> <span data-ttu-id="99aee-137">Диски класса Premium могут использоваться только такими виртуальными машинами, в номере SKU которых есть заглавная или строчная буква s.</span><span class="sxs-lookup"><span data-stu-id="99aee-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

<span data-ttu-id="99aee-138">Дополнительные сведения об использовании дисков данных с масштабируемыми наборами можно получить [в этой статье](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="99aee-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="99aee-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="99aee-139">Next steps</span></span>
<span data-ttu-id="99aee-140">Чтобы найти примеры шаблонов Resource Manager с использованием наборов масштабирования, выполните поиск строки "vmss" в [репозитории GitHub с шаблонами быстрого запуска Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="99aee-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="99aee-141">Общие сведения см. на [главной целевой странице по наборам масштабирования](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="99aee-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

