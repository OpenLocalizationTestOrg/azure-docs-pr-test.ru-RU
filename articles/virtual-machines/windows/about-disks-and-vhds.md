---
title: "Сведения о дисках и виртуальных жестких дисках для виртуальных машин Microsoft Azure под управлением Windows | Документация Майкрософт"
description: "Информация об основах использования дисков и виртуальных жестких дисков для виртуальных машин Windows в Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: c194ca0f31d077ffa998764b9d63b12dd596ac32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="959a7-103">Сведения о дисках и VHD для виртуальных машин Azure под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="959a7-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="959a7-104">Как и любой другой компьютер, виртуальные машины в Azure используют диски как место хранения операционной системы, приложений и данных.</span><span class="sxs-lookup"><span data-stu-id="959a7-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="959a7-105">Все виртуальные машины Azure имеют как минимум два диска — диск операционной системы Windows и временный диск.</span><span class="sxs-lookup"><span data-stu-id="959a7-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="959a7-106">Диск операционной системы создается из образа, при этом и диск операционной системы, и образ являются виртуальными жесткими дисками (VHD), расположенными в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="959a7-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="959a7-107">Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках.</span><span class="sxs-lookup"><span data-stu-id="959a7-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="959a7-108">В этой статье рассматриваются различные варианты применения дисков и сведения о том, как создать и использовать различные типы дисков.</span><span class="sxs-lookup"><span data-stu-id="959a7-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="959a7-109">Также доступна версия этой статьи для [виртуальных машин Linux](about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="959a7-109">This article is also available for [Linux virtual machines](about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="959a7-110">Диски, используемые виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="959a7-110">Disks used by VMs</span></span>

<span data-ttu-id="959a7-111">Давайте рассмотрим, как виртуальные машины используют диски.</span><span class="sxs-lookup"><span data-stu-id="959a7-111">Let's take a look at how the disks are used by the VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="959a7-112">Диск операционной системы</span><span class="sxs-lookup"><span data-stu-id="959a7-112">Operating system disk</span></span>
<span data-ttu-id="959a7-113">У каждой виртуальной машины есть один подключенный диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="959a7-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="959a7-114">Он зарегистрирован как диск SATA и обозначается буквой C: по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="959a7-114">It's registered as a SATA drive and labeled as the C: drive by default.</span></span> <span data-ttu-id="959a7-115">Максимальная емкость этого диска составляет 2048 гигабайта (ГБ).</span><span class="sxs-lookup"><span data-stu-id="959a7-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="959a7-116">Временный диск</span><span class="sxs-lookup"><span data-stu-id="959a7-116">Temporary disk</span></span>
<span data-ttu-id="959a7-117">У каждой виртуальной машины есть временный диск.</span><span class="sxs-lookup"><span data-stu-id="959a7-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="959a7-118">Он выступает в качестве временного хранилища для приложений и процессов и предназначен только для хранения данных, таких как страничные файлы или файлы подкачки.</span><span class="sxs-lookup"><span data-stu-id="959a7-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="959a7-119">Данные на временном диске могут быть потеряны во время [обслуживания](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) или при [повторном развертывании виртуальной машины](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="959a7-119">Data on the temporary disk may be lost during a [maintenance event](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="959a7-120">Во время обычной перезагрузки виртуальной машины данные на временном диске должны сохраниться.</span><span class="sxs-lookup"><span data-stu-id="959a7-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="959a7-121">Временный диск обозначается буквой D: по умолчанию и используется для хранения файла подкачки pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="959a7-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="959a7-122">Сведения о переназначении буквы этого диска см. в статье [Изменение буквы диска для временного диска Windows](change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="959a7-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](change-drive-letter.md).</span></span> <span data-ttu-id="959a7-123">Размер временного диска зависит от размера виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="959a7-123">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="959a7-124">Чтобы узнать больше, ознакомьтесь с [размерами виртуальных машин Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="959a7-124">For more information, see [Sizes for Windows virtual machines](sizes.md).</span></span>

<span data-ttu-id="959a7-125">Дополнительные сведения об использовании временного диска в Azure см. в статье [Общие сведения о временном диске на виртуальных машинах Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="959a7-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="959a7-126">Диск данных</span><span class="sxs-lookup"><span data-stu-id="959a7-126">Data disk</span></span>
<span data-ttu-id="959a7-127">Диск данных — виртуальный жесткий диск, подключенный к виртуальной машине для хранения данных приложений или других необходимых данных.</span><span class="sxs-lookup"><span data-stu-id="959a7-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="959a7-128">Диски данных регистрируются как диски SCSI и обозначаются любой указанной буквой.</span><span class="sxs-lookup"><span data-stu-id="959a7-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="959a7-129">Максимальная емкость каждого диска составляет 4095 ГБ.</span><span class="sxs-lookup"><span data-stu-id="959a7-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="959a7-130">Размер виртуальной машины определяет, сколько дисков данных можно подключить и какой тип хранилища можно использовать для размещения дисков.</span><span class="sxs-lookup"><span data-stu-id="959a7-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="959a7-131">Дополнительные сведения о емкости виртуальных машин см. в статье [Размеры виртуальных машин Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="959a7-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](sizes.md).</span></span>
> 

<span data-ttu-id="959a7-132">Azure создает диск операционной системы при создании виртуальной машины из образа.</span><span class="sxs-lookup"><span data-stu-id="959a7-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="959a7-133">Если используется образ, включающий диски данных, при создании виртуальной машины Azure также создает диски данных.</span><span class="sxs-lookup"><span data-stu-id="959a7-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="959a7-134">В противном случае диски данных добавляются после создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="959a7-134">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="959a7-135">Диски данных можно добавить в виртуальную машину в любое время, **подключив** их к ней.</span><span class="sxs-lookup"><span data-stu-id="959a7-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="959a7-136">Можно использовать виртуальный жесткий диск, отправленный или скопированный в учетную запись хранения или созданный Azure.</span><span class="sxs-lookup"><span data-stu-id="959a7-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="959a7-137">Подключая диск данных, вы связываете VHD-файл с виртуальной машиной. VHD-файл "берется в аренду", поэтому его невозможно удалить из хранилища, пока он подключен.</span><span class="sxs-lookup"><span data-stu-id="959a7-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="959a7-138">Последняя рекомендация. Использование TRIM с неуправляемыми дисками уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="959a7-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="959a7-139">Если вы используете неуправляемые диски уровня "Стандартный", то следует включить функцию TRIM.</span><span class="sxs-lookup"><span data-stu-id="959a7-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="959a7-140">TRIM удаляет неиспользуемые блоки на диске, таким образом плата взимается только за ту часть хранилища, которая используется.</span><span class="sxs-lookup"><span data-stu-id="959a7-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="959a7-141">Это позволяет сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="959a7-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="959a7-142">Вы можете выполнить эту команду, чтобы проверить состояние функции TRIM.</span><span class="sxs-lookup"><span data-stu-id="959a7-142">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="959a7-143">На виртуальной машине Windows откройте командную строку и введите:</span><span class="sxs-lookup"><span data-stu-id="959a7-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="959a7-144">Если команда возвращает значение 0, то функция TRIM включена правильно.</span><span class="sxs-lookup"><span data-stu-id="959a7-144">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="959a7-145">Если она возвращает значение 1, то для включения TRIM выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="959a7-145">If it returns 1, run the following command to enable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="959a7-146">Примечание. Поддержка функции Trim начинается с Windows Server 2012 или Windows 8 и более поздних версий. Дополнительные сведения см. в статье [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints) (Новый API позволяет приложением отправлять подсказки (TRIM и Unmap) на носитель данных).</span><span class="sxs-lookup"><span data-stu-id="959a7-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="959a7-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="959a7-147">Next steps</span></span>
* <span data-ttu-id="959a7-148">[Подключите диск](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) , чтобы увеличить емкость хранилища для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="959a7-148">[Attach a disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="959a7-149">[Измените букву временного диска Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) , чтобы приложение могло использовать диск D для данных.</span><span class="sxs-lookup"><span data-stu-id="959a7-149">[Change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span></span>

