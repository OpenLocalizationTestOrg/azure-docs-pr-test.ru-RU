---
title: "Масштабируемые наборы виртуальных машин Azure и подключенные диски данных | Документация Майкрософт"
description: "Сведения об использовании дисков данных с масштабируемыми наборами виртуальных машин"
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
ms.openlocfilehash: 22c7e589efa9a9f401549ec9b95c58c4eaf07b94
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="29820-103">Масштабируемые наборы ВМ Azure и подключенные диски данных</span><span class="sxs-lookup"><span data-stu-id="29820-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="29820-104">[Масштабируемые наборы виртуальных машин](/azure/virtual-machine-scale-sets/) Azure теперь поддерживают виртуальные машины с подключенными дисками данных.</span><span class="sxs-lookup"><span data-stu-id="29820-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="29820-105">Диски данных можно определить в профиле хранилища для масштабируемых наборов, созданных с использованием управляемых дисков Azure.</span><span class="sxs-lookup"><span data-stu-id="29820-105">Data disks can be defined in the storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="29820-106">Ранее единственными непосредственно подключаемыми хранилищами, доступными для виртуальных машин в масштабируемых наборах, были временные диски и диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="29820-106">Previously the only directly attached storage options available with VMs in scale sets were the OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="29820-107">При создании масштабируемого набора с определенными подключенными дисками данных для их использования вам по-прежнему необходимо подключать и форматировать диски в виртуальной машине (точно так же, как и для автономных виртуальных машин Azure).</span><span class="sxs-lookup"><span data-stu-id="29820-107">When you create a scale set with attached data disks defined, you still need to mount and format the disks from within a VM to use them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="29820-108">Для этого удобно использовать расширение пользовательских скриптов, вызывающее стандартный скрипт, чтобы секционировать и форматировать все диски данных на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="29820-108">A convenient way to do this is to use a custom script extension which calls a standard script to partition and format all the data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="29820-109">Создание масштабируемого набора с подключенными дисками данных</span><span class="sxs-lookup"><span data-stu-id="29820-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="29820-110">Простым способом создания масштабируемого набора с подключенными дисками является использование команды [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_.</span><span class="sxs-lookup"><span data-stu-id="29820-110">A simple way to create a scale set with attached disks is to use the [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="29820-111">В следующем примере создается группа ресурсов Azure и масштабируемый набор, состоящий из 10 виртуальных машин Ubuntu, каждая из которых содержит 2 подключенных диска данных объемом 50 и 100 ГБ соответственно.</span><span class="sxs-lookup"><span data-stu-id="29820-111">The following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="29820-112">Обратите внимание, что команда _vmss create_ задаст определенные значения конфигурации по умолчанию, если их не указать.</span><span class="sxs-lookup"><span data-stu-id="29820-112">Note that the _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="29820-113">Чтобы узнать, как параметры можно переопределить, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="29820-113">To see the available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="29820-114">Другой способ создания масштабируемого набора с подключенными дисками данных — это определение данного набора в шаблоне Azure Resource Manager, добавление раздела _dataDisks_ в профиле _storageProfile_ и развертывание шаблона.</span><span class="sxs-lookup"><span data-stu-id="29820-114">Another way to create a scale set with attached data disks is to define a scale set in an Azure Resource Manager template, include a _dataDisks_ section in the _storageProfile_, and deploy the template.</span></span> <span data-ttu-id="29820-115">Диски объемом 50 и 100 ГБ, приведенные в примере выше, должны быть определены в шаблоне следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29820-115">The 50 GB and 100 GB disk example above would be defined like this in the template:</span></span>
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
<span data-ttu-id="29820-116">Вы можете увидеть полный, готовый к развертыванию пример шаблона масштабируемого набора с подключенным диском здесь: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="29820-116">You can see a complete, ready to deploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-to-an-existing-scale-set"></a><span data-ttu-id="29820-117">Добавление диска данных к имеющемуся масштабируемому набору</span><span class="sxs-lookup"><span data-stu-id="29820-117">Adding a data disk to an existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="29820-118">Диски данных можно подключать только для масштабируемого набора, созданного с помощью [управляемых дисков Azure](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="29820-118">You can only attach data disks to a scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="29820-119">Вы можете добавить диск данных в масштабируемый набор виртуальных машин, используя команду Azure CLI _az vmss disk attach_.</span><span class="sxs-lookup"><span data-stu-id="29820-119">You can add a data disk to a VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="29820-120">Обязательно укажите логический номер устройства (LUN), который еще не используется.</span><span class="sxs-lookup"><span data-stu-id="29820-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="29820-121">В следующем примере с использованием интерфейса командной строки добавляется диск размером 50 ГБ в LUN 3.</span><span class="sxs-lookup"><span data-stu-id="29820-121">The following CLI example adds a 50 GB drive to lun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="29820-122">В следующем примере с использованием PowerShell добавляется диск размером 50 ГБ в LUN 3.</span><span class="sxs-lookup"><span data-stu-id="29820-122">The following PowerShell example adds a 50 GB drive to lun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="29820-123">Виртуальные машины разных размеров имеют различные ограничения на количество подключенных дисков, которые они поддерживают.</span><span class="sxs-lookup"><span data-stu-id="29820-123">Different VM sizes have different limits on the numbers of attached drives they support.</span></span> <span data-ttu-id="29820-124">Прежде чем добавлять новый диск, просмотрите [характеристики размеров виртуальных машин](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="29820-124">Check the [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="29820-125">Еще один способ добавить диск — добавить новую запись в свойство _dataDisks_ в _storageProfile_ определения масштабируемого набора и применить это изменение.</span><span class="sxs-lookup"><span data-stu-id="29820-125">You can also add a disk by adding a new entry to the _dataDisks_ property in the _storageProfile_ of a scale set definition and applying the change.</span></span> <span data-ttu-id="29820-126">Чтобы проверить это, найдите имеющееся определение масштабируемого набора в [обозревателе ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="29820-126">To test this, find an existing scale set definition in the [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="29820-127">Выберите _Изменить_ и добавьте новый диск в список дисков данных</span><span class="sxs-lookup"><span data-stu-id="29820-127">Select _Edit_ and add a new disk to the list of data disks.</span></span> <span data-ttu-id="29820-128">(например,</span><span class="sxs-lookup"><span data-stu-id="29820-128">E.g.</span></span> <span data-ttu-id="29820-129">используя приведенный выше пример).</span><span class="sxs-lookup"><span data-stu-id="29820-129">using the example above:</span></span>
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

<span data-ttu-id="29820-130">Затем выберите _PUT_ для применения изменений к масштабируемому набору.</span><span class="sxs-lookup"><span data-stu-id="29820-130">Then select _PUT_ to apply the changes to your scale set.</span></span> <span data-ttu-id="29820-131">Этот пример будет работать, если вы используете размер виртуальной машины, который поддерживает более двух подключенных дисков данных.</span><span class="sxs-lookup"><span data-stu-id="29820-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="29820-132">При внесении изменений в определение масштабируемого набора, таких как добавление или удаление диска данных, они применяются ко всем недавно созданным виртуальным машинам. Что же касается имеющихся виртуальных машин, изменения будут применены, только если свойству _upgradePolicy_ присвоено значение Automatic.</span><span class="sxs-lookup"><span data-stu-id="29820-132">When you make a change to a scale set definition such as adding or removing a data disk, it applies to all newly created VMs, but only applies to existing VMs if the _upgradePolicy_ property is set to "Automatic".</span></span> <span data-ttu-id="29820-133">Если задано значение Manual, необходимо вручную применить новую модель к имеющимся виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="29820-133">If it is set to "Manual", you need to manually apply the new model to existing VMs.</span></span> <span data-ttu-id="29820-134">Это можно сделать на портале, с помощью команды PowerShell _Update-AzureRmVmssInstance_ или с помощью команды CLI _az vmss update-instances_.</span><span class="sxs-lookup"><span data-stu-id="29820-134">You can do this in the portal, using the _Update-AzureRmVmssInstance_ PowerShell command, or using the _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-to-an-existent-scale-set"></a><span data-ttu-id="29820-135">Добавление предварительно заполненных дисков данных в существующий масштабируемый набор</span><span class="sxs-lookup"><span data-stu-id="29820-135">Adding pre-populated data disks to an existent scale set</span></span> 
> <span data-ttu-id="29820-136">Диски, добавляемые в существующую модель масштабируемого набора, по умолчанию всегда будут пустыми.</span><span class="sxs-lookup"><span data-stu-id="29820-136">When you add disks to an existent scale set model, by design, the disk will always be created empty.</span></span> <span data-ttu-id="29820-137">Это также касается экземпляров, создаваемых в этом наборе.</span><span class="sxs-lookup"><span data-stu-id="29820-137">This scenario also includes new instances created by the scale set.</span></span> <span data-ttu-id="29820-138">Такое поведение связано с тем, что в определении масштабируемого набора указан пустой диск данных.</span><span class="sxs-lookup"><span data-stu-id="29820-138">This behaviour is because the scaleset definition has an empty data disk.</span></span> <span data-ttu-id="29820-139">Чтобы создать предварительно заполненный диск данных для существующего масштабируемого набора, выберите один из двух способов:</span><span class="sxs-lookup"><span data-stu-id="29820-139">In order to create pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="29820-140">Скопируйте данные из нулевого экземпляра виртуальной машины на диски данных других виртуальных машин, используя пользовательский скрипт.</span><span class="sxs-lookup"><span data-stu-id="29820-140">Copy data from the instance 0 VM to the data disk(s) in the other VMs by running a custom script.</span></span>
* <span data-ttu-id="29820-141">Создайте управляемый образ диска ОС и диска данных (с необходимыми данными), а затем создайте масштабируемый набор с этим образом.</span><span class="sxs-lookup"><span data-stu-id="29820-141">Create a managed image with the OS disk plus data disk (with the required data) and create a new scaleset with the image.</span></span> <span data-ttu-id="29820-142">Таким образом, каждая новая виртуальная машина будет создаваться с диском данных, указанном в определении масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="29820-142">This way every new VM created will have a data disk that that is provided in the definition of the scaleset.</span></span> <span data-ttu-id="29820-143">Так как это определение ссылается на образ диска данных с необходимыми данными, каждая виртуальная машина в масштабируемом наборе автоматически создается с этими изменениями.</span><span class="sxs-lookup"><span data-stu-id="29820-143">Since this definition will refer to an image with a data disk that has customized data, every virtual machine on the scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="29820-144">Сведения о способе создания настраиваемого образа см. в статье [Создание управляемого образа универсальной виртуальной машины в Azure](/azure/virtual-machines/windows/capture-image-resource/).</span><span class="sxs-lookup"><span data-stu-id="29820-144">The way to create a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="29820-145">Пользователь должен создать нулевой экземпляр виртуальной машины с необходимыми данными, а затем использовать виртуальный жесткий диск в определении образа.</span><span class="sxs-lookup"><span data-stu-id="29820-145">The user needs to capture the instance 0 VM which has the required data, and then use that vhd for the image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="29820-146">Удаление диска данных из масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="29820-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="29820-147">Вы можете удалить диск данных в масштабируемом наборе виртуальных машин, используя команду Azure CLI _az vmss disk detach_.</span><span class="sxs-lookup"><span data-stu-id="29820-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="29820-148">Например, следующая команда удаляет диск, определенный в LUN 2:</span><span class="sxs-lookup"><span data-stu-id="29820-148">For example the following command removes the disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="29820-149">Еще один способ удалить диск в масштабируемом наборе — удалить запись из свойства _dataDisks_ в _storageProfile_ и применить изменения.</span><span class="sxs-lookup"><span data-stu-id="29820-149">Similarly you can also remove a disk from a scale set by removing an entry from the _dataDisks_ property in the _storageProfile_ and applying the change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="29820-150">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="29820-150">Additional notes</span></span>
<span data-ttu-id="29820-151">Поддержка Управляемых дисков Azure и дисков данных, подключенных к масштабируемым наборам, доступны в версии API [_30-04-2016-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) или более поздней версии API Microsoft.Compute.</span><span class="sxs-lookup"><span data-stu-id="29820-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of the Microsoft.Compute API.</span></span>

<span data-ttu-id="29820-152">В начальной реализации поддержки подключенных дисков для масштабируемых наборов нельзя подключать или отключать диски данных в отдельных виртуальных машинах масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="29820-152">In the initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="29820-153">Изначально поддержка портала Azure для подключенных дисков данных в масштабируемых наборах ограничена.</span><span class="sxs-lookup"><span data-stu-id="29820-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="29820-154">В зависимости от требований для управления подключенными дисками можно использовать шаблоны Azure, интерфейс командной строки, PowerShell, пакеты SDK и REST API.</span><span class="sxs-lookup"><span data-stu-id="29820-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API to manage attached disks.</span></span>


