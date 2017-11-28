---
title: "набор масштабирования виртуальной машины Azure aaaUpgrade | Документы Microsoft"
description: "Обновление масштабируемого набора виртуальных машин Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="218c3-103">Обновление набора масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="218c3-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="218c3-104">В этой статье описывается, как развертывание операционной системы обновления tooan Azure набор масштабирования виртуальных машин без простоев.</span><span class="sxs-lookup"><span data-stu-id="218c3-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="218c3-105">В этом контексте обновление операционной системы включает в себя изменение версии hello или номера SKU hello ОС или hello URI пользовательского изображения.</span><span class="sxs-lookup"><span data-stu-id="218c3-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="218c3-106">Обновление без простоя означает обновление виртуальных машин по одной или группами (например, по одному домену сбоя), а не всех сразу.</span><span class="sxs-lookup"><span data-stu-id="218c3-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="218c3-107">В этом случае виртуальные машины, которые не обновляются, могут продолжать работу.</span><span class="sxs-lookup"><span data-stu-id="218c3-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="218c3-108">tooavoid неоднозначности, давайте отличить четыре типа обновления ОС, может потребоваться tooperform:</span><span class="sxs-lookup"><span data-stu-id="218c3-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="218c3-109">Изменение версии hello или номера SKU образа платформы.</span><span class="sxs-lookup"><span data-stu-id="218c3-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="218c3-110">Например, изменение Ubuntu версии 14.04.2-LTS из 14.04.201506100 too14.04.201507060 или изменение too16.04.0-LTS/latest SKU 15.10 или последний Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="218c3-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="218c3-111">Этот сценарий описан в данной статье.</span><span class="sxs-lookup"><span data-stu-id="218c3-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="218c3-112">Изменение hello URI, указывающий tooa новую версию пользовательского образа сборки (**свойства** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **изображения** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="218c3-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="218c3-113">Этот сценарий описан в данной статье.</span><span class="sxs-lookup"><span data-stu-id="218c3-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="218c3-114">Изменяется ссылка на изображение hello набора масштабирования, созданную с помощью управляемых дисков Azure.</span><span class="sxs-lookup"><span data-stu-id="218c3-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="218c3-115">Установка исправлений hello ОС из виртуальной машине (в качестве примера описывается установка исправления безопасности и запуска центра обновления Windows).</span><span class="sxs-lookup"><span data-stu-id="218c3-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="218c3-116">Этот сценарий поддерживается, но не описан в данной статье.</span><span class="sxs-lookup"><span data-stu-id="218c3-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="218c3-117">В этой статье не рассматриваются наборы масштабирования виртуальных машин, которые развернуты как часть кластера [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) .</span><span class="sxs-lookup"><span data-stu-id="218c3-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="218c3-118">Дополнительные сведения об исправлении Service Fabric см. в разделе [Исправление ОС Windows в кластере Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application).</span><span class="sxs-lookup"><span data-stu-id="218c3-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="218c3-119">Hello основные версии ОС или SKU образа платформы hello последовательности для изменения или hello URI пользовательского изображения выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="218c3-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="218c3-120">Получение модели набор масштабирования виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="218c3-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="218c3-121">Изменить версию hello, SKU, ссылка на изображение или значение URI в модели hello.</span><span class="sxs-lookup"><span data-stu-id="218c3-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="218c3-122">Обновление модели hello.</span><span class="sxs-lookup"><span data-stu-id="218c3-122">Update hello model.</span></span>
4. <span data-ttu-id="218c3-123">Сделать *manualUpgrade* вызова на виртуальных машинах hello в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="218c3-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="218c3-124">Этот шаг применяется только если *upgradePolicy* задано слишком**ручной** в шкалу.</span><span class="sxs-lookup"><span data-stu-id="218c3-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="218c3-125">Если задано слишком**автоматического**, все виртуальные машины hello будут обновлены одновременно, тем самым вызывая время простоя.</span><span class="sxs-lookup"><span data-stu-id="218c3-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="218c3-126">С этой информацией в виду давайте посмотрим, как удалось обновить версию hello наборе в PowerShell, а также с помощью API-интерфейса REST hello масштабирования.</span><span class="sxs-lookup"><span data-stu-id="218c3-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="218c3-127">Эти примеры охватывают hello регистр образ платформы, но в этой статье предоставляет достаточно сведений, чтобы вы tooadapt tooa пользовательского образа этот процесс.</span><span class="sxs-lookup"><span data-stu-id="218c3-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="218c3-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="218c3-128">PowerShell</span></span>
<span data-ttu-id="218c3-129">В этом примере обновляется набора масштабирования виртуальных машин Windows (Создание toohello новая версия 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="218c3-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="218c3-130">После обновления модели hello, это происходит во время обновления один экземпляр виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="218c3-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="218c3-131">При обновлении hello URI для пользовательского изображения вместо изменения указана версия образа платформы, замените hello «набор hello новую версию» строки с помощью команды, которое будет обновлять hello URI источника изображения.</span><span class="sxs-lookup"><span data-stu-id="218c3-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="218c3-132">Например если без использования управляемых дисков Azure был создан набор масштабирования hello, hello обновления будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="218c3-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="218c3-133">Если пользовательский образ на основе набора масштабирования был создан с помощью управляемых дисков Azure hello ссылка на изображение будет обновляться.</span><span class="sxs-lookup"><span data-stu-id="218c3-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="218c3-134">Например:</span><span class="sxs-lookup"><span data-stu-id="218c3-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="218c3-135">Hello REST API</span><span class="sxs-lookup"><span data-stu-id="218c3-135">hello REST API</span></span>
<span data-ttu-id="218c3-136">Ниже приведено несколько примеров Python, использующих tooroll Azure REST API hello ожидания обновления версии ОС.</span><span class="sxs-lookup"><span data-stu-id="218c3-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="218c3-137">Оба используют облегченного hello [azurerm](https://pypi.python.org/pypi/azurerm) библиотеку toodo функции оболочки Azure REST API GET на шкале hello установить модель, следуют PUT с обновленной модели.</span><span class="sxs-lookup"><span data-stu-id="218c3-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="218c3-138">Они также рассмотрим представления экземпляров виртуальных машин tooidentify hello виртуальных машин, домен обновления.</span><span class="sxs-lookup"><span data-stu-id="218c3-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="218c3-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="218c3-139">Vmssupgrade</span></span>
 <span data-ttu-id="218c3-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) сценарий Python, который использовал tooroll out ОС обновления tooa масштабирования виртуальных машин под управлением набор в одном домене обновления за раз.</span><span class="sxs-lookup"><span data-stu-id="218c3-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![Сценарий Vmssupgrade для выбора виртуальных машин или домена обновления](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="218c3-142">Этот сценарий позволяет выбрать tooupdate виртуальными машинами или указать домен обновления.</span><span class="sxs-lookup"><span data-stu-id="218c3-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="218c3-143">Он поддерживает изменение указана версия образа платформы или hello URI пользовательского изображения.</span><span class="sxs-lookup"><span data-stu-id="218c3-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="218c3-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="218c3-144">Vmsseditor</span></span>
<span data-ttu-id="218c3-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) — это универсальный редактор наборов масштабирования виртуальных машин, отображающий состояние виртуальных машин в виде тепловой карты, в которой каждая строка представляет один домен обновления.</span><span class="sxs-lookup"><span data-stu-id="218c3-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="218c3-146">Помимо прочего можно обновить модель hello для набора масштабирования с новой версией, SKU или пользовательского образа URI, а затем выбрать tooupgrade домены сбоя.</span><span class="sxs-lookup"><span data-stu-id="218c3-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="218c3-147">После этого, все виртуальные машины hello в этом домене обновления, обновленного toohello новой модели.</span><span class="sxs-lookup"><span data-stu-id="218c3-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="218c3-148">Кроме того можно выполнить последовательное обновление на основе размера пакета hello по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="218c3-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="218c3-149">Hello следующем снимке экрана показана модель наборе для Ubuntu 14.04-2LTS версии 14.04.201507060 масштабирования.</span><span class="sxs-lookup"><span data-stu-id="218c3-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="218c3-150">Многие другие параметры были добавлены средства toothis со времени на этом снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="218c3-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Модель Vmsseditor для домена обновления с ОС Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="218c3-152">После нажатия кнопки **обновление** и затем **получение сведений о**, tooupdate запуск виртуальных машин в UD 0.</span><span class="sxs-lookup"><span data-stu-id="218c3-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![Отображение процесса обновления в Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

