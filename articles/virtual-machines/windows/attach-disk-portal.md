---
title: "aaaAttach неуправляемых данных диска tooa виртуальной Машины. Windows Azure | Документы Microsoft"
description: "Как tooa диск tooattach новых или существующих неуправляемых данных виртуальной Машины Windows в Azure портала с помощью hello hello модели развертывания диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="d32da-103">Как tooattach неуправляемых данных на диске tooa виртуальной Машины Windows в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d32da-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="d32da-104">В этой статье рассказывается, как неуправляемый tooattach новые и существующие диски tooWindows виртуальных машин с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d32da-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="d32da-105">Вы также можете [присоединить диск данных с помощью PowerShell](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d32da-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="d32da-106">Перед этим ознакомьтесь со следующими советами:</span><span class="sxs-lookup"><span data-stu-id="d32da-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="d32da-107">размер Hello hello виртуальной машины определяет число дисков, можно присоединить.</span><span class="sxs-lookup"><span data-stu-id="d32da-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="d32da-108">Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="d32da-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="d32da-109">toouse хранилище Premium необходимо виртуальную машину серии DS или GS-series.</span><span class="sxs-lookup"><span data-stu-id="d32da-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="d32da-110">Эти виртуальные машины позволяют использовать диски из учетных записей хранения Premium и Standard.</span><span class="sxs-lookup"><span data-stu-id="d32da-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="d32da-111">Хранилище Premium доступно в определенных регионах.</span><span class="sxs-lookup"><span data-stu-id="d32da-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="d32da-112">Дополнительные сведения см. в разделе [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d32da-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="d32da-113">Для нового диска не требуется toocreate его первого, так как Azure создает при его подключении.</span><span class="sxs-lookup"><span data-stu-id="d32da-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="d32da-114">Вы также можете [присоединить диск данных с помощью Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d32da-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="d32da-115">Найти hello виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="d32da-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="d32da-116">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d32da-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d32da-117">В меню слева hello hello выберите **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="d32da-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="d32da-118">Выберите виртуальную машину hello из списка hello.</span><span class="sxs-lookup"><span data-stu-id="d32da-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="d32da-119">В колонке hello виртуальные машины, нажмите кнопку **дисков**.</span><span class="sxs-lookup"><span data-stu-id="d32da-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="d32da-120">Продолжайте, следуя указаниям по подключению [нового](#option-1-attach-a-new-disk) или [существующего диска](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="d32da-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="d32da-121">Вариант 1. Подключение и инициализация нового диска</span><span class="sxs-lookup"><span data-stu-id="d32da-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="d32da-122">На hello **дисков** колонка, щелкните **+ добавить диск данных**.</span><span class="sxs-lookup"><span data-stu-id="d32da-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="d32da-123">В hello **присоединить диск управляемого** колонки, введите имя диска hello в **имя** , а затем выберите **New (пустого диска)** в **тип источника**.</span><span class="sxs-lookup"><span data-stu-id="d32da-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="d32da-124">В разделе **контейнер хранилища**, нажмите кнопку hello **Обзор** кнопку и просматривать toohello учетной записи хранилища и контейнер, где вы бы hello toobe нового виртуального жесткого диска хранятся и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="d32da-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![Просмотр параметров диска](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="d32da-126">После завершения настройки hello для диска данных hello щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d32da-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="d32da-127">В hello **дисков** колонке нажмите кнопку **Сохранить** hello диск tooadd toohello-конфигурацию виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d32da-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="d32da-128">Инициализация нового диска данных</span><span class="sxs-lookup"><span data-stu-id="d32da-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="d32da-129">Подключение toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d32da-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="d32da-130">Инструкции см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d32da-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="d32da-131">Нажмите кнопку hello **запустить** меню внутри hello виртуальной Машины и тип **diskmgmt.msc** и нажмите кнопку **ввод**.</span><span class="sxs-lookup"><span data-stu-id="d32da-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="d32da-132">Это запускает оснастку управления дисками hello.</span><span class="sxs-lookup"><span data-stu-id="d32da-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="d32da-133">Управление дисками распознает, что имеется новый, неинициализированный диск, и появится всплывающее окно hello инициализация диска.</span><span class="sxs-lookup"><span data-stu-id="d32da-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="d32da-134">Убедитесь, что выбран новый диск hello и нажмите кнопку **ОК** tooinitialize его.</span><span class="sxs-lookup"><span data-stu-id="d32da-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="d32da-135">Hello новый диск теперь отображается в виде **нераспределенного**.</span><span class="sxs-lookup"><span data-stu-id="d32da-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="d32da-136">Щелкните правой кнопкой мыши в любом месте на диске hello и выберите **создать простой том**.</span><span class="sxs-lookup"><span data-stu-id="d32da-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="d32da-137">Hello **мастер создания простых томов** запускает.</span><span class="sxs-lookup"><span data-stu-id="d32da-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="d32da-138">Выполните мастер hello, хранит все значения по умолчанию hello, после этого выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="d32da-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="d32da-139">Закройте оснастку "Управление дисками".</span><span class="sxs-lookup"><span data-stu-id="d32da-139">Close Disk Management.</span></span>
7. <span data-ttu-id="d32da-140">Пользователь получает всплывающее окно, которое требуется tooformat hello новый диск перед его использованием.</span><span class="sxs-lookup"><span data-stu-id="d32da-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="d32da-141">Щелкните **Форматировать диск**.</span><span class="sxs-lookup"><span data-stu-id="d32da-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="d32da-142">В hello **новый диск в формате** диалогового окна, hello Проверьте параметры и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="d32da-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="d32da-143">Вы получите предупреждение, что форматирование дисков hello стирает все данные hello, нажав кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d32da-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="d32da-144">После завершения форматирования hello, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d32da-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="d32da-145">Вариант 2. Подключение существующего диска</span><span class="sxs-lookup"><span data-stu-id="d32da-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="d32da-146">На hello **дисков** колонка, щелкните **+ добавить диск данных**.</span><span class="sxs-lookup"><span data-stu-id="d32da-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="d32da-147">На hello **присоединить диск неуправляемые** колонки в **тип источника** выберите **существующие BLOB-объекта**.</span><span class="sxs-lookup"><span data-stu-id="d32da-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Просмотр параметров диска](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="d32da-149">Нажмите кнопку **Обзор** toonavigate toohello учетной записи хранилища и контейнер, где hello существующий виртуальный жесткий ДИСК.</span><span class="sxs-lookup"><span data-stu-id="d32da-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="d32da-150">Выберите и hello виртуальный жесткий ДИСК и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="d32da-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="d32da-151">Нажмите кнопку **ОК** в hello **присоединить диск неуправляемые** колонку.</span><span class="sxs-lookup"><span data-stu-id="d32da-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="d32da-152">В hello **дисков** колонка, щелкните **Сохранить** tooadd hello toohello конфигурации для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d32da-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="d32da-153">Использование функции TRIM в хранилище уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="d32da-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="d32da-154">Если вы используете хранилище уровня "Стандартный" (HDD), то следует включить функцию TRIM.</span><span class="sxs-lookup"><span data-stu-id="d32da-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="d32da-155">TRIM удаляет неиспользуемые блоки на диске hello, начисляется только для хранения данных, который фактически используется.</span><span class="sxs-lookup"><span data-stu-id="d32da-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="d32da-156">Это позволяет сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="d32da-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="d32da-157">Можно запустить это команда toocheck TRIM приветствия.</span><span class="sxs-lookup"><span data-stu-id="d32da-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="d32da-158">На виртуальной машине Windows откройте командную строку и введите:</span><span class="sxs-lookup"><span data-stu-id="d32da-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="d32da-159">Команда hello возвращает 0, Функция TRIM включения правильно.</span><span class="sxs-lookup"><span data-stu-id="d32da-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="d32da-160">Если он возвращает 1, выполните следующие команды tooenable TRIM hello:</span><span class="sxs-lookup"><span data-stu-id="d32da-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="d32da-161">После удаления данных с диска, можно обеспечить hello TRIM операций записи на диск правильно, запустив дефрагментации с УСЕЧЕНИЕМ:</span><span class="sxs-lookup"><span data-stu-id="d32da-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="d32da-162">Также можно обеспечить, что весь том hello усекается при форматировании тома hello.</span><span class="sxs-lookup"><span data-stu-id="d32da-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d32da-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d32da-163">Next steps</span></span>
<span data-ttu-id="d32da-164">Если после этого приложение должно данные toostore диска D: hello toouse, вы можете [изменить букву временного диска Windows hello hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d32da-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

