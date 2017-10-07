---
title: "aaaUsing управляемых диски с Azure наборы масштабирования виртуальных машин | Документы Microsoft"
description: "Узнайте, почему и как toouse управляемых дисках с наборы масштабирования виртуальных машин"
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
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="bcb38-103">Масштабируемые наборы виртуальных машин Azure и управляемые диски</span><span class="sxs-lookup"><span data-stu-id="bcb38-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="bcb38-104">[Масштабируемые наборы виртуальных машин](/azure/virtual-machine-scale-sets/) Azure теперь поддерживают виртуальные машины с управляемыми дисками.</span><span class="sxs-lookup"><span data-stu-id="bcb38-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="bcb38-105">Использование управляемых дисков с масштабируемыми наборами имеет ряд преимуществ, в частности следующие:</span><span class="sxs-lookup"><span data-stu-id="bcb38-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="bcb38-106">Больше не нужна toopre-Создание и управление ими диски hello ОС toostore учетных записей хранилища для виртуальных машин для набора масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="bcb38-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="bcb38-107">Можно присоединить управляемых дисков toohello шкалы набора данных.</span><span class="sxs-lookup"><span data-stu-id="bcb38-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="bcb38-108">благодаря управляемым дискам емкость масштабируемого набора может достигать 1000 виртуальных машин (на базе образа платформы) или 100 виртуальных машин (на базе пользовательского образа).</span><span class="sxs-lookup"><span data-stu-id="bcb38-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="bcb38-109">Начало работы</span><span class="sxs-lookup"><span data-stu-id="bcb38-109">Get started</span></span>

<span data-ttu-id="bcb38-110">Простой способ tooget работы с наборами шкалы управляемого диска — toodeploy один из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb38-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="bcb38-111">Дополнительные сведения см. в [этой статье](./virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="bcb38-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="bcb38-112">Другой простой способ запуска tooget — toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy в наборе.</span><span class="sxs-lookup"><span data-stu-id="bcb38-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="bcb38-113">Hello следующем примере показано, как набор масштабирования с 10 виртуальных машин, каждая из которых диск объемом 50 ГБ и 100 ГБ данных на основе toocreate Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="bcb38-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="bcb38-114">Кроме того, может выглядеть в hello [в репозитории GitHub шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates) для папок, содержащих `vmss` toosee готовые примеры шаблонов, развертываемые набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="bcb38-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="bcb38-115">tootell, какие шаблоны, использующих управляемый диски, можно ссылаться слишком[этот список](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="bcb38-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcb38-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bcb38-116">Next steps</span></span>

<span data-ttu-id="bcb38-117">Дополнительные сведения об управляемых дисках в целом см. в [этой статье](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcb38-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="bcb38-118">toosee tooconvert задает масштаб tooprovision шаблона диспетчера ресурсов с управляемых дисках, разделе [в этой статье](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="bcb38-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="bcb38-119">Hello шаблоны диспетчера ресурсов toohello же изменения применяются toohello Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="bcb38-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="bcb38-120">в разделе toolearn Подробнее об использовании дисков данных, управляемых с помощью набора масштабирования [в этой статье](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="bcb38-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="bcb38-121">Работа с наборами большого объема toobegin ссылаться слишком[в этой статье](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="bcb38-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


