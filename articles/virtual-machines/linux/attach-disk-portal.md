---
title: "Подключение диска данных к виртуальной машине Linux | Документация Майкрософт"
description: "Подключение нового или существующего диска данных к виртуальной машине Linux на портале Azure с помощью модели развертывания на основе диспетчера ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 1599ee241c3d9fb3623ebd89ae30f2795cae1930
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a><span data-ttu-id="f3839-103">Подключение диска данных к виртуальной машине Linux на портале Azure</span><span class="sxs-lookup"><span data-stu-id="f3839-103">How to attach a data disk to a Linux VM in the Azure portal</span></span>
<span data-ttu-id="f3839-104">В этой статье показано, как подключить новый и существующий диски к виртуальной машине Linux на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f3839-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span></span> <span data-ttu-id="f3839-105">Вы также можете [подключить диск данных к виртуальной машине Windows на портале Azure](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3839-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f3839-106">Вы можете использовать Управляемые диски Azure или неуправляемые диски.</span><span class="sxs-lookup"><span data-stu-id="f3839-106">You can choose to use either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="f3839-107">Управляемые диски полностью контролируются платформой Azure и не требуют никакой подготовки или выделения места.</span><span class="sxs-lookup"><span data-stu-id="f3839-107">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="f3839-108">Неуправляемые диски требуют учетную запись хранения и применения некоторых [квот и ограничений](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="f3839-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="f3839-109">Дополнительные сведения об Управляемых дисках Azure см. в [обзоре Управляемых дисков Azure](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f3839-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="f3839-110">Прежде чем подключить диски к виртуальной машине, ознакомьтесь со следующими советами:</span><span class="sxs-lookup"><span data-stu-id="f3839-110">Before you attach disks to your VM, review these tips:</span></span>

* <span data-ttu-id="f3839-111">Размер виртуальной машины определяет, сколько дисков данных к ней можно подключить.</span><span class="sxs-lookup"><span data-stu-id="f3839-111">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="f3839-112">Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3839-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="f3839-113">Для использования хранилища класса Premium вам необходимо будет использовать виртуальную машину серии DS или GS.</span><span class="sxs-lookup"><span data-stu-id="f3839-113">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="f3839-114">Эти виртуальные машины позволяют использовать диски уровня "Премиум" и "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="f3839-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="f3839-115">Хранилище Premium доступно в определенных регионах.</span><span class="sxs-lookup"><span data-stu-id="f3839-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="f3839-116">Дополнительные сведения см. в разделе [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3839-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="f3839-117">На самом деле диски, подключенные к виртуальным машинам, — это VHD-файлы, хранящиеся в Azure.</span><span class="sxs-lookup"><span data-stu-id="f3839-117">Disks attached to virtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="f3839-118">Дополнительную информацию см. в статье [О дисках и виртуальных жестких дисках для виртуальных машин](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3839-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="f3839-119">Поиск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f3839-119">Find the virtual machine</span></span>
1. <span data-ttu-id="f3839-120">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f3839-120">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f3839-121">В главном меню щелкните **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="f3839-121">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="f3839-122">Затем выберите виртуальную машину из списка.</span><span class="sxs-lookup"><span data-stu-id="f3839-122">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="f3839-123">В колонке "Виртуальные машины" в разделе **Основные компоненты** щелкните **Диски**.</span><span class="sxs-lookup"><span data-stu-id="f3839-123">To the Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Открытие параметров диска](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="f3839-125">Продолжайте, следуя указаниям по подключению [управляемого](#use-azure-managed-disks) или [неуправляемого диска](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="f3839-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="f3839-126">Использование Управляемых дисков Azure</span><span class="sxs-lookup"><span data-stu-id="f3839-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="f3839-127">Подключение нового диска</span><span class="sxs-lookup"><span data-stu-id="f3839-127">Attach a new disk</span></span>

1. <span data-ttu-id="f3839-128">В колонке **Диски** щелкните **+ Add data disk** (+ Добавить диск данных).</span><span class="sxs-lookup"><span data-stu-id="f3839-128">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="f3839-129">Щелкните раскрывающееся меню **Имя** и выберите пункт **Создать диск**:</span><span class="sxs-lookup"><span data-stu-id="f3839-129">Click the drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Создание управляемого диска Azure](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="f3839-131">Введите имя управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="f3839-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="f3839-132">Просмотрите параметры по умолчанию, при необходимости измените их, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f3839-132">Review the default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Просмотр параметров диска](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="f3839-134">Щелкните **Сохранить**, чтобы создать управляемый диск и обновить конфигурацию виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="f3839-134">Click **Save** to create the managed disk and update the VM configuration:</span></span>

   ![Сохранение нового управляемого диска Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="f3839-136">После того как Azure создаст диск и подключит его к виртуальной машине, он появится в параметрах дисков виртуальной машины в разделе **Диски данных**.</span><span class="sxs-lookup"><span data-stu-id="f3839-136">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="f3839-137">Так как управляемые диски являются ресурсами верхнего уровня, диск отображается в корне группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="f3839-137">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span></span>

   ![Управляемый диск Azure в группе ресурсов](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="f3839-139">Подключение существующего диска</span><span class="sxs-lookup"><span data-stu-id="f3839-139">Attach an existing disk</span></span>
1. <span data-ttu-id="f3839-140">В колонке **Диски** щелкните **+ Add data disk** (+ Добавить диск данных).</span><span class="sxs-lookup"><span data-stu-id="f3839-140">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="f3839-141">Щелкните раскрывающееся меню **Имя**, чтобы просмотреть список имеющихся управляемых дисков, доступных для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="f3839-141">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span></span> <span data-ttu-id="f3839-142">Выберите управляемый диск, который следует подключить:</span><span class="sxs-lookup"><span data-stu-id="f3839-142">Select the managed disk to attach:</span></span>

   ![Подключение имеющегося управляемого диска Azure](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="f3839-144">Щелкните **Сохранить**, чтобы подключить имеющийся управляемый диск и обновить конфигурацию виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="f3839-144">Click **Save** to attach the existing managed disk and update the VM configuration:</span></span>
   
   ![Сохранение обновлений управляемого диска Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="f3839-146">После того как Azure подключит диск к виртуальной машине, он будет отображаться в параметрах дисков виртуальной машины в разделе **Диски данных**.</span><span class="sxs-lookup"><span data-stu-id="f3839-146">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="f3839-147">Использование неуправляемых дисков</span><span class="sxs-lookup"><span data-stu-id="f3839-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="f3839-148">Подключение нового диска</span><span class="sxs-lookup"><span data-stu-id="f3839-148">Attach a new disk</span></span>

1. <span data-ttu-id="f3839-149">В колонке **Диски** щелкните **+ Add data disk** (+ Добавить диск данных).</span><span class="sxs-lookup"><span data-stu-id="f3839-149">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="f3839-150">Просмотрите параметры по умолчанию, при необходимости измените их, затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f3839-150">Review the default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Просмотр параметров диска](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="f3839-152">После того как Azure создаст диск и подключит его к виртуальной машине, он появится в параметрах дисков виртуальной машины в разделе **Диски данных**.</span><span class="sxs-lookup"><span data-stu-id="f3839-152">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="f3839-153">Подключение существующего диска</span><span class="sxs-lookup"><span data-stu-id="f3839-153">Attach an existing disk</span></span>
1. <span data-ttu-id="f3839-154">В колонке **Диски** щелкните **+ Add data disk** (+ Добавить диск данных).</span><span class="sxs-lookup"><span data-stu-id="f3839-154">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="f3839-155">В разделе **Подключение существующего диска** щелкните **VHD-файл**.</span><span class="sxs-lookup"><span data-stu-id="f3839-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Подключение существующего диска](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="f3839-157">В разделе **Учетные записи хранения**выберите учетную запись и контейнер, который содержит VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="f3839-157">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>
   
   ![Поиск расположения VHD](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="f3839-159">Выберите VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="f3839-159">Select the .vhd file.</span></span>
5. <span data-ttu-id="f3839-160">В разделе **Подключение существующего диска** выбранный вами файл отображается в списке, расположенном в разделе **VHD-файл**.</span><span class="sxs-lookup"><span data-stu-id="f3839-160">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="f3839-161">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f3839-161">Click **OK**.</span></span>
6. <span data-ttu-id="f3839-162">После того как Azure подключит диск к виртуальной машине, он будет отображаться в параметрах дисков виртуальной машины в разделе **Диски данных**.</span><span class="sxs-lookup"><span data-stu-id="f3839-162">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f3839-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3839-163">Next steps</span></span>
<span data-ttu-id="f3839-164">После добавления диска его необходимо подготовить для использования.</span><span class="sxs-lookup"><span data-stu-id="f3839-164">After the disk is added, you need to prepare it for use.</span></span> <span data-ttu-id="f3839-165">Дополнительные сведения см. в разделе [Инициализация нового диска данных в Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="f3839-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
