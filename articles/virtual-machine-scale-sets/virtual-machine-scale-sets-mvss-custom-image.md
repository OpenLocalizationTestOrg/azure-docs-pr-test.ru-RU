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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="68b80-103">Добавить пользовательский образ tooan масштабирование Azure задать шаблон</span><span class="sxs-lookup"><span data-stu-id="68b80-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="68b80-104">В этой статье показано, как toomodify hello [Минимальный масштаб допустимого шаблона набора](./virtual-machine-scale-sets-mvss-start.md) toodeploy из пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="68b80-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="68b80-105">Измените определение шаблона hello</span><span class="sxs-lookup"><span data-stu-id="68b80-105">Change hello template definition</span></span>

<span data-ttu-id="68b80-106">Наш шаблон Минимальный масштаб допустимого набора может видеть [здесь](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), и можно будет увидеть нашей шаблон для развертывания набора с помощью пользовательского образа шкалы hello [здесь](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="68b80-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="68b80-107">Давайте рассмотрим toocreate hello diff использовать этот шаблон (`git diff minimum-viable-scale-set custom-image`) по частям:</span><span class="sxs-lookup"><span data-stu-id="68b80-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="68b80-108">Создание образа управляемого диска</span><span class="sxs-lookup"><span data-stu-id="68b80-108">Creating a managed disk image</span></span>

<span data-ttu-id="68b80-109">Если вы уже создали настраиваемый образ управляемого диска (ресурс типа `Microsoft.Compute/images`), можете пропустить этот раздел.</span><span class="sxs-lookup"><span data-stu-id="68b80-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="68b80-110">Во-первых, мы добавляем `sourceImageVhdUri` параметра, который является hello URI toohello обобщенный blob в хранилище Azure, содержащий toodeploy hello пользовательского образа из.</span><span class="sxs-lookup"><span data-stu-id="68b80-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


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

<span data-ttu-id="68b80-111">Далее добавим ресурс типа `Microsoft.Compute/images`, который основан на hello обобщенный большой двоичный объект, расположенный в URI изображения hello управляемого диска `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="68b80-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="68b80-112">Этот образ должен находиться в hello же регионе, что набор масштабирования hello, который его использует.</span><span class="sxs-lookup"><span data-stu-id="68b80-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="68b80-113">В свойствах образа hello hello мы укажите тип hello ОС, расположение hello hello BLOB-объекта (из hello `sourceImageVhdUri` параметра) и тип учетной записи хранения hello:</span><span class="sxs-lookup"><span data-stu-id="68b80-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

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

<span data-ttu-id="68b80-114">В hello набора масштабирования ресурсов, мы добавим `dependsOn` предложение ссылается toomake пользовательского образа toohello убедиться, что изображение hello создается до набора масштабирования hello пытается toodeploy из этого образа:</span><span class="sxs-lookup"><span data-stu-id="68b80-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="68b80-115">Изменение масштаба задать свойства toouse hello управляемого диска изображение</span><span class="sxs-lookup"><span data-stu-id="68b80-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="68b80-116">В hello `imageReference` шкалы hello задать `storageProfile`, вместо указания hello издателя, предложение, sku и версия образа платформы, мы указываем hello `id` из hello `Microsoft.Compute/images` ресурсов:</span><span class="sxs-lookup"><span data-stu-id="68b80-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="68b80-117">В этом примере мы используем hello `resourceId` созданные tooget функции hello идентификатор ресурса изображения hello в hello же шаблона.</span><span class="sxs-lookup"><span data-stu-id="68b80-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="68b80-118">Если заранее после создания образа управляемого диска hello, необходимо предоставить идентификатор hello этого образа вместо.</span><span class="sxs-lookup"><span data-stu-id="68b80-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="68b80-119">Этот идентификатор должен иметь форму hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="68b80-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="68b80-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68b80-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
