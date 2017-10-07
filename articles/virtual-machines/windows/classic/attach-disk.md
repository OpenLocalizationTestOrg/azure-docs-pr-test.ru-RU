---
title: "aaaAttach tooa диска классической виртуальной Машине Azure | Документы Microsoft"
description: "Присоединение данных диска tooa Windows виртуальную машину, созданную с помощью hello классической модели развертывания и инициализировать его."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="05e05-103">Присоединение данных диска tooa Windows виртуальную машину, созданную с помощью hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="05e05-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="05e05-104">В этой статье показано, как новые и существующие диски tooattach созданы с hello классического развертывания модели tooa виртуальной машины Windows с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="05e05-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="05e05-105">Вы также можете [присоединения tooa диска данных виртуальной Машины с Linux в hello портал Azure](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="05e05-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="05e05-106">Прежде чем подключить диск, ознакомьтесь со следующими советами.</span><span class="sxs-lookup"><span data-stu-id="05e05-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="05e05-107">размер Hello hello виртуальной машины определяет число дисков, можно присоединить.</span><span class="sxs-lookup"><span data-stu-id="05e05-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="05e05-108">Дополнительную информацию см. в статье [Размеры виртуальных машин](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05e05-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="05e05-109">toouse хранилище Premium необходимо виртуальную машину серии DS или GS-series.</span><span class="sxs-lookup"><span data-stu-id="05e05-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="05e05-110">Эти виртуальные машины позволяют использовать диски из учетных записей хранения Premium и Standard.</span><span class="sxs-lookup"><span data-stu-id="05e05-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="05e05-111">Хранилище Premium доступно в определенных регионах.</span><span class="sxs-lookup"><span data-stu-id="05e05-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="05e05-112">Дополнительные сведения см. в разделе [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05e05-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="05e05-113">Для нового диска не требуется toocreate его первого, так как Azure создает при его подключении.</span><span class="sxs-lookup"><span data-stu-id="05e05-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="05e05-114">Вы также можете [присоединить диск данных с помощью Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="05e05-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05e05-115">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="05e05-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="05e05-116">Найти hello виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="05e05-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="05e05-117">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="05e05-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="05e05-118">Выберите hello виртуальную машину из ресурсов hello в списке на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="05e05-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="05e05-119">В левой области hello в разделе **параметры**, нажмите кнопку **дисков**.</span><span class="sxs-lookup"><span data-stu-id="05e05-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![Открытие параметров диска](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="05e05-121">Продолжайте, следуя указаниям по подключению [нового](#option-1-attach-a-new-disk) или [существующего диска](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="05e05-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="05e05-122">Вариант 1. Подключение и инициализация нового диска</span><span class="sxs-lookup"><span data-stu-id="05e05-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="05e05-123">На hello **дисков** колонка, щелкните **присоединения новой**.</span><span class="sxs-lookup"><span data-stu-id="05e05-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="05e05-124">Просмотрите параметры по умолчанию hello, обновление при необходимости и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="05e05-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![Просмотр параметров диска](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="05e05-126">Azure создает диск hello и присоединяет его toohello виртуальной машины, новый диск hello указана в параметры диска hello виртуальной машины в группе **диски с данными**.</span><span class="sxs-lookup"><span data-stu-id="05e05-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="05e05-127">Инициализация нового диска данных</span><span class="sxs-lookup"><span data-stu-id="05e05-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="05e05-128">Подключение toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="05e05-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="05e05-129">Инструкции см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05e05-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="05e05-130">После входа в систему виртуальной машины toohello откройте **диспетчера сервера**.</span><span class="sxs-lookup"><span data-stu-id="05e05-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="05e05-131">Выберите в левой области hello **файловых служб и служб хранилища**.</span><span class="sxs-lookup"><span data-stu-id="05e05-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![Откройте диспетчер сервера.](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="05e05-133">Выберите **Диски**.</span><span class="sxs-lookup"><span data-stu-id="05e05-133">Select **Disks**.</span></span>
4. <span data-ttu-id="05e05-134">Hello **дисков** разделе перечислены диски hello.</span><span class="sxs-lookup"><span data-stu-id="05e05-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="05e05-135">Чаще всего виртуальная машина содержит диск 0, диск 1 и диск 2.</span><span class="sxs-lookup"><span data-stu-id="05e05-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="05e05-136">На диске 0 — диск операционной системы hello и диск 1 является hello временный диск 2 — диск данных hello вновь подключен toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="05e05-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="05e05-137">Hello списки диска данных hello раздел как **Неизвестный**.</span><span class="sxs-lookup"><span data-stu-id="05e05-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="05e05-138">Щелкните правой кнопкой мыши диск hello и выберите **инициализировать**.</span><span class="sxs-lookup"><span data-stu-id="05e05-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="05e05-139">В случае получения уведомления, что при инициализации hello диска будут удалены все данные.</span><span class="sxs-lookup"><span data-stu-id="05e05-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="05e05-140">Нажмите кнопку **Да** tooacknowledge hello предупреждение и инициализируйте hello диска.</span><span class="sxs-lookup"><span data-stu-id="05e05-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="05e05-141">После завершения hello секции будут указаны как **GPT**.</span><span class="sxs-lookup"><span data-stu-id="05e05-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="05e05-142">Щелкните правой кнопкой мыши диск hello и выберите **новый том**.</span><span class="sxs-lookup"><span data-stu-id="05e05-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="05e05-143">Выполните мастер hello, используя значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="05e05-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="05e05-144">По завершении мастер hello hello **тома** разделе перечислены hello новый том.</span><span class="sxs-lookup"><span data-stu-id="05e05-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="05e05-145">Hello диск больше не подключен и готов toostore данных.</span><span class="sxs-lookup"><span data-stu-id="05e05-145">hello disk is now online and ready toostore data.</span></span>

    ![Том успешно инициализирован](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="05e05-147">Вариант 2. Подключение существующего диска</span><span class="sxs-lookup"><span data-stu-id="05e05-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="05e05-148">На hello **дисков** колонка, щелкните **присоединения существующего**.</span><span class="sxs-lookup"><span data-stu-id="05e05-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="05e05-149">В разделе **Подключение существующего диска** щелкните **Расположение**.</span><span class="sxs-lookup"><span data-stu-id="05e05-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Подключение существующего диска](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="05e05-151">В разделе **учетные записи хранения**, выберите учетную запись hello и контейнер, хранящий hello VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="05e05-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![Поиск расположения VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="05e05-153">Выберите VHD-файл hello.</span><span class="sxs-lookup"><span data-stu-id="05e05-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="05e05-154">В разделе **подключить существующий диск**, файл hello, выбранной в списке под **VHD-файл**.</span><span class="sxs-lookup"><span data-stu-id="05e05-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="05e05-155">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="05e05-155">Click **OK**.</span></span>
6. <span data-ttu-id="05e05-156">После Azure присоединяет hello диск toohello виртуальной машины, он будет отображен в параметры диска hello виртуальной машины в группе **диски с данными**.</span><span class="sxs-lookup"><span data-stu-id="05e05-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="05e05-157">Использование функции TRIM в хранилище уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="05e05-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="05e05-158">Если вы используете хранилище уровня "Стандартный" (HDD), то следует включить функцию TRIM.</span><span class="sxs-lookup"><span data-stu-id="05e05-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="05e05-159">TRIM удаляет неиспользуемые блоки на диске hello, начисляется только для хранения данных, который фактически используется.</span><span class="sxs-lookup"><span data-stu-id="05e05-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="05e05-160">Использование функции TRIM может уменьшить затраты, включая затраты на неиспользуемые блоки, возникающие в результате удаления больших файлов.</span><span class="sxs-lookup"><span data-stu-id="05e05-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="05e05-161">Можно запустить это команда toocheck TRIM приветствия.</span><span class="sxs-lookup"><span data-stu-id="05e05-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="05e05-162">На виртуальной машине Windows откройте командную строку и введите:</span><span class="sxs-lookup"><span data-stu-id="05e05-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="05e05-163">Команда hello возвращает 0, Функция TRIM включения правильно.</span><span class="sxs-lookup"><span data-stu-id="05e05-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="05e05-164">Если он возвращает 1, выполните следующие команды tooenable TRIM hello:</span><span class="sxs-lookup"><span data-stu-id="05e05-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="05e05-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05e05-165">Next steps</span></span>
<span data-ttu-id="05e05-166">Если приложению требуются данные toostore диска D: hello toouse, вы можете [изменить букву временного диска Windows hello hello](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="05e05-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05e05-167">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="05e05-167">Additional resources</span></span>
[<span data-ttu-id="05e05-168">О дисках и виртуальных жестких дисках для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="05e05-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
