---
title: "aaaAttach tooa диска данных виртуальной Машины с Linux | Документы Microsoft"
description: "Как tooa диск tooattach новых или существующих данных виртуальных Машин Linux в Azure портала с помощью hello hello модели развертывания диспетчера ресурсов."
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
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a><span data-ttu-id="292df-103">Как tooattach данных на диске tooa виртуальных Машин Linux в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="292df-103">How tooattach a data disk tooa Linux VM in hello Azure portal</span></span>
<span data-ttu-id="292df-104">В этой статье показано, как tooattach новые и существующие диски виртуальной машины через портал Azure hello tooa Linux.</span><span class="sxs-lookup"><span data-stu-id="292df-104">This article shows you how tooattach both new and existing disks tooa Linux virtual machine through hello Azure portal.</span></span> <span data-ttu-id="292df-105">Вы также можете [присоединения tooa диска данных виртуальной Машины Windows в hello портал Azure](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="292df-105">You can also [attach a data disk tooa Windows VM in hello Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="292df-106">Вы можете toouse либо дисков Azure управляемых или неуправляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="292df-106">You can choose toouse either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="292df-107">Управляемый диски обрабатываются hello платформы Azure и не требуют toostore любые предварительные и расположение их.</span><span class="sxs-lookup"><span data-stu-id="292df-107">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="292df-108">Неуправляемые диски требуют учетную запись хранения и применения некоторых [квот и ограничений](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="292df-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="292df-109">Дополнительные сведения об Управляемых дисках Azure см. в [обзоре Управляемых дисков Azure](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="292df-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="292df-110">Прежде чем присоединять tooyour дисков виртуальной Машины, ознакомьтесь со следующими советами:</span><span class="sxs-lookup"><span data-stu-id="292df-110">Before you attach disks tooyour VM, review these tips:</span></span>

* <span data-ttu-id="292df-111">размер Hello hello виртуальной машины определяет число дисков, можно присоединить.</span><span class="sxs-lookup"><span data-stu-id="292df-111">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="292df-112">Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="292df-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="292df-113">toouse хранилище Premium необходимо виртуальную машину серии DS или GS-series.</span><span class="sxs-lookup"><span data-stu-id="292df-113">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="292df-114">Эти виртуальные машины позволяют использовать диски уровня "Премиум" и "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="292df-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="292df-115">Хранилище Premium доступно в определенных регионах.</span><span class="sxs-lookup"><span data-stu-id="292df-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="292df-116">Дополнительные сведения см. в разделе [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="292df-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="292df-117">Машины toovirtual присоединенные диски находятся фактически VHD-файлов, хранящихся в Azure.</span><span class="sxs-lookup"><span data-stu-id="292df-117">Disks attached toovirtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="292df-118">Дополнительную информацию см. в статье [О дисках и виртуальных жестких дисках для виртуальных машин](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="292df-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="292df-119">Найти hello виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="292df-119">Find hello virtual machine</span></span>
1. <span data-ttu-id="292df-120">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="292df-120">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="292df-121">Hello концентратора меню **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="292df-121">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="292df-122">Выберите виртуальную машину hello из списка hello.</span><span class="sxs-lookup"><span data-stu-id="292df-122">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="292df-123">toohello виртуальной машины, в колонке **Essentials**, нажмите кнопку **дисков**.</span><span class="sxs-lookup"><span data-stu-id="292df-123">toohello Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Открытие параметров диска](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="292df-125">Продолжайте, следуя указаниям по подключению [управляемого](#use-azure-managed-disks) или [неуправляемого диска](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="292df-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="292df-126">Использование Управляемых дисков Azure</span><span class="sxs-lookup"><span data-stu-id="292df-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="292df-127">Подключение нового диска</span><span class="sxs-lookup"><span data-stu-id="292df-127">Attach a new disk</span></span>

1. <span data-ttu-id="292df-128">На hello **дисков** колонка, щелкните **+ добавить диск данных**.</span><span class="sxs-lookup"><span data-stu-id="292df-128">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="292df-129">Щелкните раскрывающееся меню hello для **имя** и выберите **создать диск**:</span><span class="sxs-lookup"><span data-stu-id="292df-129">Click hello drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Создание управляемого диска Azure](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="292df-131">Введите имя управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="292df-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="292df-132">Просмотрите параметры по умолчанию hello, обновление при необходимости и щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="292df-132">Review hello default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Просмотр параметров диска](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="292df-134">Нажмите кнопку **Сохранить** toocreate hello управляемого диска и обновление конфигурации виртуальной Машины hello:</span><span class="sxs-lookup"><span data-stu-id="292df-134">Click **Save** toocreate hello managed disk and update hello VM configuration:</span></span>

   ![Сохранение нового управляемого диска Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="292df-136">Azure создает диск hello и присоединяет его toohello виртуальной машины, новый диск hello указана в параметры диска hello виртуальной машины в группе **диски с данными**.</span><span class="sxs-lookup"><span data-stu-id="292df-136">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="292df-137">Как управляемый дисков в ресурсе верхнего уровня, диск hello появится в корне hello группа ресурсов «hello»:</span><span class="sxs-lookup"><span data-stu-id="292df-137">As managed disks are a top-level resource, hello disk appears at hello root of hello resource group:</span></span>

   ![Управляемый диск Azure в группе ресурсов](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="292df-139">Подключение существующего диска</span><span class="sxs-lookup"><span data-stu-id="292df-139">Attach an existing disk</span></span>
1. <span data-ttu-id="292df-140">На hello **дисков** колонка, щелкните **+ добавить диск данных**.</span><span class="sxs-lookup"><span data-stu-id="292df-140">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="292df-141">Щелкните раскрывающееся меню hello для **имя** tooview список существующих управляемых диски доступны tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="292df-141">Click hello drop-down menu for **Name** tooview a list of existing managed disks accessible tooyour Azure subscription.</span></span> <span data-ttu-id="292df-142">Выберите hello управляемый tooattach диска.</span><span class="sxs-lookup"><span data-stu-id="292df-142">Select hello managed disk tooattach:</span></span>

   ![Подключение имеющегося управляемого диска Azure](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="292df-144">Нажмите кнопку **Сохранить** существующие tooattach hello управляемого диска и обновление конфигурации виртуальной Машины hello:</span><span class="sxs-lookup"><span data-stu-id="292df-144">Click **Save** tooattach hello existing managed disk and update hello VM configuration:</span></span>
   
   ![Сохранение обновлений управляемого диска Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="292df-146">После Azure присоединяет hello диск toohello виртуальной машины, он будет отображен в параметры диска hello виртуальной машины в группе **диски с данными**.</span><span class="sxs-lookup"><span data-stu-id="292df-146">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="292df-147">Использование неуправляемых дисков</span><span class="sxs-lookup"><span data-stu-id="292df-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="292df-148">Подключение нового диска</span><span class="sxs-lookup"><span data-stu-id="292df-148">Attach a new disk</span></span>

1. <span data-ttu-id="292df-149">На hello **дисков** колонка, щелкните **+ добавить диск данных**.</span><span class="sxs-lookup"><span data-stu-id="292df-149">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="292df-150">Просмотрите параметры по умолчанию hello, обновление при необходимости и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="292df-150">Review hello default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Просмотр параметров диска](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="292df-152">Azure создает диск hello и присоединяет его toohello виртуальной машины, новый диск hello указана в параметры диска hello виртуальной машины в группе **диски с данными**.</span><span class="sxs-lookup"><span data-stu-id="292df-152">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="292df-153">Подключение существующего диска</span><span class="sxs-lookup"><span data-stu-id="292df-153">Attach an existing disk</span></span>
1. <span data-ttu-id="292df-154">На hello **дисков** колонка, щелкните **+ добавить диск данных**.</span><span class="sxs-lookup"><span data-stu-id="292df-154">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="292df-155">В разделе **Подключение существующего диска** щелкните **VHD-файл**.</span><span class="sxs-lookup"><span data-stu-id="292df-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Подключение существующего диска](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="292df-157">В разделе **учетные записи хранения**, выберите учетную запись hello и контейнер, хранящий hello VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="292df-157">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>
   
   ![Поиск расположения VHD](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="292df-159">Выберите VHD-файл hello.</span><span class="sxs-lookup"><span data-stu-id="292df-159">Select hello .vhd file.</span></span>
5. <span data-ttu-id="292df-160">В разделе **подключить существующий диск**, файл hello, выбранной в списке под **VHD-файл**.</span><span class="sxs-lookup"><span data-stu-id="292df-160">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="292df-161">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="292df-161">Click **OK**.</span></span>
6. <span data-ttu-id="292df-162">После Azure присоединяет hello диск toohello виртуальной машины, он будет отображен в параметры диска hello виртуальной машины в группе **диски с данными**.</span><span class="sxs-lookup"><span data-stu-id="292df-162">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="292df-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="292df-163">Next steps</span></span>
<span data-ttu-id="292df-164">После добавления hello диска необходимо tooprepare его для использования.</span><span class="sxs-lookup"><span data-stu-id="292df-164">After hello disk is added, you need tooprepare it for use.</span></span> <span data-ttu-id="292df-165">Дополнительные сведения см. в разделе [Инициализация нового диска данных в Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="292df-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
