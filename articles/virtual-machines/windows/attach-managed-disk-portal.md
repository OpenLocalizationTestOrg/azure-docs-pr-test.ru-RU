---
title: "aaaAttach tooa диска управляемых данных виртуальной Машины. Windows Azure | Документы Microsoft"
description: "Новый tooattach управляются tooa диска данных виртуальной Машины Windows в Azure портала с помощью hello hello модели развертывания диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="447f9-103">Как tooattach управляемые данные на диске tooa виртуальной Машины Windows в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="447f9-103">How tooattach a managed data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="447f9-104">В этой статье показано, как tooattach новые управляемые данные на диске tooWindows виртуальных машин с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="447f9-104">This article shows you how tooattach a new managed data disk tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="447f9-105">Перед этим ознакомьтесь со следующими советами:</span><span class="sxs-lookup"><span data-stu-id="447f9-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="447f9-106">размер Hello hello виртуальной машины определяет число дисков, можно присоединить.</span><span class="sxs-lookup"><span data-stu-id="447f9-106">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="447f9-107">Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="447f9-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="447f9-108">Для нового диска не требуется toocreate его первого, так как Azure создает при его подключении.</span><span class="sxs-lookup"><span data-stu-id="447f9-108">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="447f9-109">Вы также можете [присоединить диск данных с помощью Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="447f9-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="447f9-110">Добавление диска данных</span><span class="sxs-lookup"><span data-stu-id="447f9-110">Add a data disk</span></span>
1. <span data-ttu-id="447f9-111">В меню слева hello hello выберите **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="447f9-111">In hello menu on hello left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="447f9-112">Выберите виртуальную машину hello из списка hello.</span><span class="sxs-lookup"><span data-stu-id="447f9-112">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="447f9-113">В колонке hello виртуальной машины, нажмите кнопку **дисков**.</span><span class="sxs-lookup"><span data-stu-id="447f9-113">On hello virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="447f9-114">На hello **дисков** колонка, щелкните **+ добавить диск данных**.</span><span class="sxs-lookup"><span data-stu-id="447f9-114">On hello **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="447f9-115">В hello раскрывающийся список для hello новый диск, выберите **создать пустой**.</span><span class="sxs-lookup"><span data-stu-id="447f9-115">In hello drop-down for hello new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="447f9-116">В hello **Создание управляемого диска** колонки, введите имя для диска hello и настройте Здравствуйте другие параметры, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="447f9-116">In hello **Create managed disk** blade, type in a name for hello disk and adjust hello other settings as necessary.</span></span> <span data-ttu-id="447f9-117">Закончив, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="447f9-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="447f9-118">В hello **дисков** колонки, нажмите кнопку Сохранить toosave hello новой конфигурации для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="447f9-118">In hello **Disks** blade, click save toosave hello new disk configuration for hello VM.</span></span>
6. <span data-ttu-id="447f9-119">Azure создает диск hello и присоединяет его toohello виртуальной машины, новый диск hello указана в параметры диска hello виртуальной машины в группе **диски с данными**.</span><span class="sxs-lookup"><span data-stu-id="447f9-119">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="447f9-120">Инициализация нового диска данных</span><span class="sxs-lookup"><span data-stu-id="447f9-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="447f9-121">Подключите toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="447f9-121">Connect toohello VM.</span></span>
1. <span data-ttu-id="447f9-122">Пункт меню "Пуск" hello внутри hello виртуальной Машины и тип **diskmgmt.msc** и нажмите кнопку **ввод**.</span><span class="sxs-lookup"><span data-stu-id="447f9-122">Click hello start menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="447f9-123">Будет запущен оснастки управления дисками hello.</span><span class="sxs-lookup"><span data-stu-id="447f9-123">This will start hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="447f9-124">Управление дисками определяет, что у вас есть новый, отмена инициализации диска и появится всплывающее окно hello инициализация диска.</span><span class="sxs-lookup"><span data-stu-id="447f9-124">Disk Management will recognize that you have a new, un-initialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="447f9-125">Убедитесь, что выбран новый диск hello и нажмите кнопку **ОК** tooinitialize его.</span><span class="sxs-lookup"><span data-stu-id="447f9-125">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="447f9-126">новый диск Hello, теперь будет отображаться как **нераспределенного**.</span><span class="sxs-lookup"><span data-stu-id="447f9-126">hello new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="447f9-127">Щелкните правой кнопкой мыши в любом месте на диске hello и выберите **создать простой том**.</span><span class="sxs-lookup"><span data-stu-id="447f9-127">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="447f9-128">Hello **мастер создания простых томов** запускает.</span><span class="sxs-lookup"><span data-stu-id="447f9-128">hello **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="447f9-129">Выполните мастер hello, хранит все значения по умолчанию hello, после этого выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="447f9-129">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="447f9-130">Закройте оснастку "Управление дисками".</span><span class="sxs-lookup"><span data-stu-id="447f9-130">Close Disk Management.</span></span>
7. <span data-ttu-id="447f9-131">Появится всплывающее окно, необходимо tooformat hello новый диск перед его использованием.</span><span class="sxs-lookup"><span data-stu-id="447f9-131">You will get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="447f9-132">Щелкните **Форматировать диск**.</span><span class="sxs-lookup"><span data-stu-id="447f9-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="447f9-133">В hello **новый диск в формате** диалогового окна, hello Проверьте параметры и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="447f9-133">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="447f9-134">Вы получите предупреждение, что форматирование дисков hello приведет к удалению всех данных hello щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="447f9-134">You will get a warning that formatting hello disks will erase all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="447f9-135">После завершения форматирования hello, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="447f9-135">When hello format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="447f9-136">Использование функции TRIM в хранилище уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="447f9-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="447f9-137">Если вы используете хранилище уровня "Стандартный" (HDD), то следует включить функцию TRIM.</span><span class="sxs-lookup"><span data-stu-id="447f9-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="447f9-138">TRIM удаляет неиспользуемые блоки на диске hello, начисляется только для хранения данных, который фактически используется.</span><span class="sxs-lookup"><span data-stu-id="447f9-138">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="447f9-139">Это позволяет сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="447f9-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="447f9-140">Можно запустить это команда toocheck TRIM приветствия.</span><span class="sxs-lookup"><span data-stu-id="447f9-140">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="447f9-141">На виртуальной машине Windows откройте командную строку и введите:</span><span class="sxs-lookup"><span data-stu-id="447f9-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="447f9-142">Команда hello возвращает 0, Функция TRIM включения правильно.</span><span class="sxs-lookup"><span data-stu-id="447f9-142">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="447f9-143">Если он возвращает 1, выполните следующие команды tooenable TRIM hello:</span><span class="sxs-lookup"><span data-stu-id="447f9-143">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="447f9-144">После удаления данных с диска, можно обеспечить hello TRIM операций записи на диск правильно, запустив дефрагментации с УСЕЧЕНИЕМ:</span><span class="sxs-lookup"><span data-stu-id="447f9-144">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="447f9-145">Также можно обеспечить, что весь том hello усекается при форматировании тома hello.</span><span class="sxs-lookup"><span data-stu-id="447f9-145">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="447f9-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="447f9-146">Next steps</span></span>
<span data-ttu-id="447f9-147">Если после этого приложение должно данные toostore диска D: hello toouse, вы можете [изменить букву временного диска Windows hello hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="447f9-147">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
