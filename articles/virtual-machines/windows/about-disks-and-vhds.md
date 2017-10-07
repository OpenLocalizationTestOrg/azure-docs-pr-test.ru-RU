---
title: "aaaAbout дисков и виртуальных жестких дисков для виртуальных машин Windows Azure Майкрософт | Документы Microsoft"
description: "Дополнительные сведения об основах hello дисков и виртуальных жестких дисков для виртуальных машинах в Azure."
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
ms.openlocfilehash: 1b0d6bf05237bb3d1497b2c60f79a0159b730108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="1733c-103">Сведения о дисках и VHD для виртуальных машин Azure под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="1733c-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="1733c-104">Так же, как и любой другой компьютер виртуальные машины в Azure используют дисков, когда toostore месте операционной системы, приложений и данных.</span><span class="sxs-lookup"><span data-stu-id="1733c-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="1733c-105">Все виртуальные машины Azure имеют как минимум два диска — диск операционной системы Windows и временный диск.</span><span class="sxs-lookup"><span data-stu-id="1733c-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="1733c-106">Hello диск операционной системы создается из образа, а hello диска операционной системы и образа hello, виртуальные жесткие диски (VHD) хранятся в учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1733c-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="1733c-107">Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках.</span><span class="sxs-lookup"><span data-stu-id="1733c-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="1733c-108">В этой статье мы поговорим о различных вариантах hello для дисков hello и затем рассматриваются различные типы дисков можно создавать и использовать hello.</span><span class="sxs-lookup"><span data-stu-id="1733c-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="1733c-109">Также доступна версия этой статьи для [виртуальных машин Linux](about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="1733c-109">This article is also available for [Linux virtual machines](about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="1733c-110">Диски, используемые виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="1733c-110">Disks used by VMs</span></span>

<span data-ttu-id="1733c-111">Давайте рассмотрим, как используются диски hello в hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="1733c-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="1733c-112">Диск операционной системы</span><span class="sxs-lookup"><span data-stu-id="1733c-112">Operating system disk</span></span>
<span data-ttu-id="1733c-113">У каждой виртуальной машины есть один подключенный диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="1733c-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="1733c-114">Зарегистрирован как диск SATA и помечены как диск C: hello по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1733c-114">It's registered as a SATA drive and labeled as hello C: drive by default.</span></span> <span data-ttu-id="1733c-115">Максимальная емкость этого диска составляет 2048 гигабайта (ГБ).</span><span class="sxs-lookup"><span data-stu-id="1733c-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="1733c-116">Временный диск</span><span class="sxs-lookup"><span data-stu-id="1733c-116">Temporary disk</span></span>
<span data-ttu-id="1733c-117">У каждой виртуальной машины есть временный диск.</span><span class="sxs-lookup"><span data-stu-id="1733c-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="1733c-118">временный диск Hello предоставляет краткосрочного хранения приложениями и процессами и предполагаемого tooonly хранения данных, таких как страница или файлы подкачки.</span><span class="sxs-lookup"><span data-stu-id="1733c-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="1733c-119">Данные на временном диске hello могут быть потеряны во время [события обслуживания](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) или если вы [повторного развертывания виртуальной Машины](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1733c-119">Data on hello temporary disk may be lost during a [maintenance event](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1733c-120">Во время стандартной перезагрузки hello ВМ должен сохранять hello данные на временном диске hello.</span><span class="sxs-lookup"><span data-stu-id="1733c-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="1733c-121">временный диск Hello обозначается как диск D: hello по умолчанию и он используется для хранения pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="1733c-121">hello temporary disk is labeled as hello D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="1733c-122">tooremap этот диск tooa другой буквой диска, в разделе [изменений hello букву временного диска Windows hello](change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="1733c-122">tooremap this disk tooa different drive letter, see [Change hello drive letter of hello Windows temporary disk](change-drive-letter.md).</span></span> <span data-ttu-id="1733c-123">размер Hello hello временного диска зависит от размера hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1733c-123">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="1733c-124">Чтобы узнать больше, ознакомьтесь с [размерами виртуальных машин Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="1733c-124">For more information, see [Sizes for Windows virtual machines](sizes.md).</span></span>

<span data-ttu-id="1733c-125">Дополнительные сведения об использовании hello временный диск Azure см. в разделе [основные сведения о временном диске hello на виртуальных машинах Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="1733c-125">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="1733c-126">Диск данных</span><span class="sxs-lookup"><span data-stu-id="1733c-126">Data disk</span></span>
<span data-ttu-id="1733c-127">Диск с данными — данные приложения toostore вложенного tooa виртуальной машины или другие данные, необходимые tookeep виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="1733c-127">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="1733c-128">Диски данных регистрируются как диски SCSI и обозначаются любой указанной буквой.</span><span class="sxs-lookup"><span data-stu-id="1733c-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="1733c-129">Максимальная емкость каждого диска составляет 4095 ГБ.</span><span class="sxs-lookup"><span data-stu-id="1733c-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="1733c-130">Hello размер hello виртуальной машины определяет число дисков, можно присоединить tooit и hello тип хранилища, можно использовать toohost hello дисков.</span><span class="sxs-lookup"><span data-stu-id="1733c-130">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="1733c-131">Дополнительные сведения о емкости виртуальных машин см. в статье [Размеры виртуальных машин Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="1733c-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](sizes.md).</span></span>
> 

<span data-ttu-id="1733c-132">Azure создает диск операционной системы при создании виртуальной машины из образа.</span><span class="sxs-lookup"><span data-stu-id="1733c-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="1733c-133">При использовании образа, включающее диски данных Azure также создает hello диски с данными при создании виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="1733c-133">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="1733c-134">В противном случае диски с данными добавляются после создания виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="1733c-134">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="1733c-135">Виртуальная машина tooa диски данных в любое время можно добавить путем **присоединение** hello диск toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1733c-135">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="1733c-136">Можно использовать VHD, который вы загруженный или скопированный tooyour учетной записи хранилища или один, Azure создает для вас.</span><span class="sxs-lookup"><span data-stu-id="1733c-136">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="1733c-137">При подключении диска данных связывает hello VHD-файл с hello виртуальной Машины, размещая аренды в hello виртуального жесткого диска, поэтому его нельзя удалить из хранилища, когда он присоединен по-прежнему.</span><span class="sxs-lookup"><span data-stu-id="1733c-137">Attaching a data disk associates hello VHD file with hello VM by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="1733c-138">Последняя рекомендация. Использование TRIM с неуправляемыми дисками уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="1733c-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="1733c-139">Если вы используете неуправляемые диски уровня "Стандартный", то следует включить функцию TRIM.</span><span class="sxs-lookup"><span data-stu-id="1733c-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="1733c-140">TRIM удаляет неиспользуемые блоки на диске hello, начисляется только для хранения данных, который фактически используется.</span><span class="sxs-lookup"><span data-stu-id="1733c-140">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="1733c-141">Это позволяет сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="1733c-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="1733c-142">Можно запустить это команда toocheck TRIM приветствия.</span><span class="sxs-lookup"><span data-stu-id="1733c-142">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="1733c-143">На виртуальной машине Windows откройте командную строку и введите:</span><span class="sxs-lookup"><span data-stu-id="1733c-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="1733c-144">Команда hello возвращает 0, Функция TRIM включения правильно.</span><span class="sxs-lookup"><span data-stu-id="1733c-144">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="1733c-145">Если он возвращает 1, выполните следующие команды tooenable TRIM hello:</span><span class="sxs-lookup"><span data-stu-id="1733c-145">If it returns 1, run hello following command tooenable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="1733c-146">Примечание: Поддержка функции Trim начинается с Windows Server 2012 или Windows 8 и более поздних версий, см. в разделе [новый интерфейс API позволяет приложениям toosend «ОБРЕЗАТЬ и отменить сопоставление» подсказки toostorage мультимедиа](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span><span class="sxs-lookup"><span data-stu-id="1733c-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps toosend "TRIM and Unmap" hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="1733c-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1733c-147">Next steps</span></span>
* <span data-ttu-id="1733c-148">[Присоединить диск](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd дополнительное хранилище для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1733c-148">[Attach a disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="1733c-149">[Изменение буквы диска hello временного диска Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) , приложение может использовать диск D: hello для данных.</span><span class="sxs-lookup"><span data-stu-id="1733c-149">[Change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use hello D: drive for data.</span></span>

