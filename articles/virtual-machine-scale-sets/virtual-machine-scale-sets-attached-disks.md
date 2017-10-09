---
title: "aaaAzure виртуальной машины шкалы наборов присоединенные диски с данными | Документы Microsoft"
description: "Узнайте, как toouse присоединенных дисков с данными с наборы масштабирования виртуальных машин"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="dfe57-103">Масштабируемые наборы ВМ Azure и подключенные диски данных</span><span class="sxs-lookup"><span data-stu-id="dfe57-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="dfe57-104">[Масштабируемые наборы виртуальных машин](/azure/virtual-machine-scale-sets/) Azure теперь поддерживают виртуальные машины с подключенными дисками данных.</span><span class="sxs-lookup"><span data-stu-id="dfe57-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="dfe57-105">Диски данных можно определить в профиле хранилища hello для набора масштабирования, которые были созданы с управлять дисками Azure.</span><span class="sxs-lookup"><span data-stu-id="dfe57-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="dfe57-106">Ранее hello только непосредственно подключенного хранилища варианты с виртуальными машинами в наборы масштабирования были диск ОС hello и временные диски.</span><span class="sxs-lookup"><span data-stu-id="dfe57-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="dfe57-107">При создании наборе с подключенными дисками данных определен масштабирования, по-прежнему нужна toomount и формат hello диски из внутри toouse ВМ их (как для автономных виртуальных машинах Azure).</span><span class="sxs-lookup"><span data-stu-id="dfe57-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="dfe57-108">Toodo удобный способ это toouse расширение пользовательского скрипта, которая вызывает toopartition стандартного скрипта и форматировать все диски с данными hello на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="dfe57-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="dfe57-109">Создание масштабируемого набора с подключенными дисками данных</span><span class="sxs-lookup"><span data-stu-id="dfe57-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="dfe57-110">Простой способ toocreate, задать шкалу с подключенными дисками — toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss создания_ команды.</span><span class="sxs-lookup"><span data-stu-id="dfe57-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="dfe57-111">Следующий пример Hello создает группы ресурсов Azure и набора масштабирования виртуальных Машин 10 Ubuntu виртуальных машин, каждая из которых 2 подключенные диски данных, 50 ГБ и 100 ГБ соответственно.</span><span class="sxs-lookup"><span data-stu-id="dfe57-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="dfe57-112">Обратите внимание, что hello _vmss создания_ команды по умолчанию определенные значения конфигурации, если они не указаны.</span><span class="sxs-lookup"><span data-stu-id="dfe57-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="dfe57-113">toosee hello доступные параметры, можно переопределить try:</span><span class="sxs-lookup"><span data-stu-id="dfe57-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="dfe57-114">Другой способ toocreate, наборе с подключенными дисками данных масштабирования является toodefine шкалу, задайте в шаблоне диспетчера ресурсов Azure, включают _dataDisks_ раздела hello _storageProfile_и развертывание hello шаблон.</span><span class="sxs-lookup"><span data-stu-id="dfe57-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="dfe57-115">Hello 50 ГБ до 100 ГБ дискового приведенном выше примере должны быть определены следующим образом в hello шаблона:</span><span class="sxs-lookup"><span data-stu-id="dfe57-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="dfe57-116">Пример завершения, готовая toodeploy шаблон набора масштабирования можно увидеть на подключенный диск, определенные здесь: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="dfe57-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="dfe57-117">Добавление существующих шкалу tooan диск данных набора</span><span class="sxs-lookup"><span data-stu-id="dfe57-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="dfe57-118">Можно присоединить только набор масштабирования tooa диски данных которого был создан с [управляемых дисков Azure](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="dfe57-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="dfe57-119">Можно добавить данные диск tooa масштабирования виртуальных Машин с помощью Azure CLI _присоединить диск vmss az_ команды.</span><span class="sxs-lookup"><span data-stu-id="dfe57-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="dfe57-120">Обязательно укажите логический номер устройства (LUN), который еще не используется.</span><span class="sxs-lookup"><span data-stu-id="dfe57-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="dfe57-121">Следующий пример CLI Hello добавляет toolun диск 50 ГБ 3:</span><span class="sxs-lookup"><span data-stu-id="dfe57-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="dfe57-122">Следующий пример PowerShell Hello добавляет toolun диск 50 ГБ 3:</span><span class="sxs-lookup"><span data-stu-id="dfe57-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="dfe57-123">Различные размеры виртуальной Машины имеют различные ограничения на hello количество подключенных дисков, которые они поддерживают.</span><span class="sxs-lookup"><span data-stu-id="dfe57-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="dfe57-124">Проверьте hello [характеристики размер виртуальной машины](../virtual-machines/windows/sizes.md) перед добавлением нового диска.</span><span class="sxs-lookup"><span data-stu-id="dfe57-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="dfe57-125">Можно также добавить диск, добавив новый toohello входа _dataDisks_ свойство в hello _storageProfile_ шкалы задать определения и применения изменений hello.</span><span class="sxs-lookup"><span data-stu-id="dfe57-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="dfe57-126">tootest, найти существующее определение набора масштабирования hello [обозревателя ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dfe57-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="dfe57-127">Выберите _изменить_ и добавьте новый диск toohello список дисков данных.</span><span class="sxs-lookup"><span data-stu-id="dfe57-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="dfe57-128">Например: </span><span class="sxs-lookup"><span data-stu-id="dfe57-128">E.g.</span></span> <span data-ttu-id="dfe57-129">Используя пример hello выше:</span><span class="sxs-lookup"><span data-stu-id="dfe57-129">using hello example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="dfe57-130">Выберите _ПОМЕСТИТЬ_ tooapply hello изменяет набор tooyour масштабирования.</span><span class="sxs-lookup"><span data-stu-id="dfe57-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="dfe57-131">Этот пример будет работать, если вы используете размер виртуальной машины, который поддерживает более двух подключенных дисков данных.</span><span class="sxs-lookup"><span data-stu-id="dfe57-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="dfe57-132">При внесении изменений tooa набора масштабирования определения, такие как добавление или удаление диска с данными, он применяет tooall вновь созданные виртуальные машины, но применяется tooexisting виртуальных машин, только если hello _upgradePolicy_ задано слишком «Automatic».</span><span class="sxs-lookup"><span data-stu-id="dfe57-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="dfe57-133">Если задано слишком «Manual», необходимо toomanually применить hello новой модели tooexisting виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="dfe57-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="dfe57-134">Это можно сделать на портале hello помощью hello _обновление AzureRmVmssInstance_ PowerShell команды или hello _обновление vmss az-экземпляры_ команду CLI.</span><span class="sxs-lookup"><span data-stu-id="dfe57-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="dfe57-135">Добавление данных предварительно заполненных дисков tooan существующая масштабного набора</span><span class="sxs-lookup"><span data-stu-id="dfe57-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="dfe57-136">При добавлении дисков tooan существующие модели набора масштабирования намеренно, hello диск будет создана пустая.</span><span class="sxs-lookup"><span data-stu-id="dfe57-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="dfe57-137">Этот сценарий также включает новые экземпляры, созданные набором масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="dfe57-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="dfe57-138">Это поведение связано определение scaleset hello имеет пустой диск данных.</span><span class="sxs-lookup"><span data-stu-id="dfe57-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="dfe57-139">В порядок toocreate предварительно заполненных дисков с данными для модели набор существующих шкалы можно выбрать любой из следующих двух параметров:</span><span class="sxs-lookup"><span data-stu-id="dfe57-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="dfe57-140">Копирование данных из диски с данными toohello ВМ hello экземпляр 0 hello других виртуальных машин с помощью пользовательского скрипта.</span><span class="sxs-lookup"><span data-stu-id="dfe57-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="dfe57-141">Создайте управляемый образ с диска hello ОС, а также диск данных (с данными требуется hello) и новый scaleset с изображением hello.</span><span class="sxs-lookup"><span data-stu-id="dfe57-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="dfe57-142">Таким образом, в каждой новой созданной виртуальной Машине будет иметь данных на диске, указанным в определении hello hello scaleset.</span><span class="sxs-lookup"><span data-stu-id="dfe57-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="dfe57-143">Поскольку это определение ссылается tooan изображения с диска данных, который изменил данные, каждой виртуальной машины на hello scaleset автоматически запустится с этих изменений.</span><span class="sxs-lookup"><span data-stu-id="dfe57-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="dfe57-144">Здравствуйте, toocreate способом пользовательского изображения можно найти здесь: [создать управляемый образ универсальной ВМ в Azure](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="dfe57-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="dfe57-145">Hello пользователь должен toocapture hello экземпляр 0 виртуальную Машину, которая имеет hello необходимых данных, а затем использовать виртуального жесткого диска для определения образа hello.</span><span class="sxs-lookup"><span data-stu-id="dfe57-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="dfe57-146">Удаление диска данных из масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="dfe57-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="dfe57-147">Вы можете удалить диск данных в масштабируемом наборе виртуальных машин, используя команду Azure CLI _az vmss disk detach_.</span><span class="sxs-lookup"><span data-stu-id="dfe57-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="dfe57-148">Пример hello следующая команда удаляет диск hello, определенный в lun 2:</span><span class="sxs-lookup"><span data-stu-id="dfe57-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="dfe57-149">Аналогичным образом можно также удалить диск из наборе, удаляя запись из hello масштабирования _dataDisks_ свойство в hello _storageProfile_ и применения изменений hello.</span><span class="sxs-lookup"><span data-stu-id="dfe57-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="dfe57-150">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="dfe57-150">Additional notes</span></span>
<span data-ttu-id="dfe57-151">Поддержка для дисков Azure управляемых и масштаб задайте подключенные диски данных доступна в версии API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) или более поздней hello Microsoft.Compute API.</span><span class="sxs-lookup"><span data-stu-id="dfe57-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="dfe57-152">В реализации начальной hello подключенный диск поддержка набора масштабирования нельзя присоединять или отсоединять диски с данными из отдельных виртуальных машин в наборе масштабирования.</span><span class="sxs-lookup"><span data-stu-id="dfe57-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="dfe57-153">Изначально поддержка портала Azure для подключенных дисков данных в масштабируемых наборах ограничена.</span><span class="sxs-lookup"><span data-stu-id="dfe57-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="dfe57-154">В зависимости от требований, которые можно использовать шаблоны Azure CLI, пакеты SDK, PowerShell и API-интерфейса REST toomanage подключенные диски.</span><span class="sxs-lookup"><span data-stu-id="dfe57-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


