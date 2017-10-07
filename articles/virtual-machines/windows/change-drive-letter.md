---
title: "Сделать hello диск D: диска данных виртуальной машины | Документы Microsoft"
description: "Описывает, как диск toochange буквы для ВМ Windows, чтобы вы могли использовать диск D: hello как диск с данными."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="08cda-103">Использовать диск D: hello в качестве диска с данными на виртуальной Машине Windows</span><span class="sxs-lookup"><span data-stu-id="08cda-103">Use hello D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="08cda-104">Если приложению hello toouse данные toostore диска D, выполните эти инструкции toouse другой буквой диска для временного диска hello.</span><span class="sxs-lookup"><span data-stu-id="08cda-104">If your application needs toouse hello D drive toostore data, follow these instructions toouse a different drive letter for hello temporary disk.</span></span> <span data-ttu-id="08cda-105">Никогда не используйте hello временный диск toostore данные, которые требуются tookeep.</span><span class="sxs-lookup"><span data-stu-id="08cda-105">Never use hello temporary disk toostore data that you need tookeep.</span></span>

<span data-ttu-id="08cda-106">При изменении размера или **остановки (освобождения)** виртуальную машину, это может быть выдано размещения виртуальной машины hello tooa новый низкоуровневой оболочки.</span><span class="sxs-lookup"><span data-stu-id="08cda-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of hello virtual machine tooa new hypervisor.</span></span> <span data-ttu-id="08cda-107">Запланированное или незапланированное событие технического обслуживания также может вызвать такое перемещение.</span><span class="sxs-lookup"><span data-stu-id="08cda-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="08cda-108">В этом сценарии hello временный диск будет переназначенные toohello первая доступная буква диска.</span><span class="sxs-lookup"><span data-stu-id="08cda-108">In this scenario, hello temporary disk will be reassigned toohello first available drive letter.</span></span> <span data-ttu-id="08cda-109">Если у вас есть приложение, требующее диск D: hello в частности, необходимо toofollow эти действия tootemporarily перемещения hello pagefile.sys, подключить новый диск данных и назначьте его hello буквы D, а затем обратно временный диск toohello pagefile.sys hello перемещения.</span><span class="sxs-lookup"><span data-stu-id="08cda-109">If you have an application that specifically requires hello D: drive, you need toofollow these steps tootemporarily move hello pagefile.sys, attach a new data disk and assign it hello letter D and then move hello pagefile.sys back toohello temporary drive.</span></span> <span data-ttu-id="08cda-110">После завершения Azure не будет обратно hello D: Если hello виртуальная машина перемещается tooa другой низкоуровневой оболочки.</span><span class="sxs-lookup"><span data-stu-id="08cda-110">Once complete, Azure will not take back hello D: if hello VM moves tooa different hypervisor.</span></span>

<span data-ttu-id="08cda-111">Дополнительные сведения об использовании hello временный диск Azure см. в разделе [основные сведения о временном диске hello на виртуальных машинах Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="08cda-111">For more information about how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-hello-data-disk"></a><span data-ttu-id="08cda-112">Присоединить диск данных hello</span><span class="sxs-lookup"><span data-stu-id="08cda-112">Attach hello data disk</span></span>
<span data-ttu-id="08cda-113">Во-первых вам потребуется hello tooattach данных toohello диска виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="08cda-113">First, you'll need tooattach hello data disk toohello virtual machine.</span></span> <span data-ttu-id="08cda-114">toodo этого с помощью портала hello, в разделе [tooattach управляемых данных места на диске в hello портал Azure](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08cda-114">toodo this using hello portal, see [How tooattach a managed data disk in hello Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-tooc-drive"></a><span data-ttu-id="08cda-115">Временно переместить файл подкачки pagefile.sys tooC диска</span><span class="sxs-lookup"><span data-stu-id="08cda-115">Temporarily move pagefile.sys tooC drive</span></span>
1. <span data-ttu-id="08cda-116">Подключение toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="08cda-116">Connect toohello virtual machine.</span></span> 
2. <span data-ttu-id="08cda-117">Щелкните правой кнопкой мыши hello **запустить** и выбрать пункт **системы**.</span><span class="sxs-lookup"><span data-stu-id="08cda-117">Right-click hello **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="08cda-118">Выберите в меню слева hello, **расширенных параметров системы**.</span><span class="sxs-lookup"><span data-stu-id="08cda-118">In hello left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="08cda-119">В hello **производительности** выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="08cda-119">In hello **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="08cda-120">Выберите hello **Дополнительно** вкладки.</span><span class="sxs-lookup"><span data-stu-id="08cda-120">Select hello **Advanced** tab.</span></span>
6. <span data-ttu-id="08cda-121">В hello **виртуальной памяти** выберите **изменений**.</span><span class="sxs-lookup"><span data-stu-id="08cda-121">In hello **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="08cda-122">Выберите hello **C** диск и нажмите кнопку **размер по выбору системы** и нажмите кнопку **задать**.</span><span class="sxs-lookup"><span data-stu-id="08cda-122">Select hello **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="08cda-123">Выберите hello **D** диск и нажмите кнопку **без файла подкачки** и нажмите кнопку **задать**.</span><span class="sxs-lookup"><span data-stu-id="08cda-123">Select hello **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="08cda-124">Нажмите кнопку "Применить".</span><span class="sxs-lookup"><span data-stu-id="08cda-124">Click Apply.</span></span> <span data-ttu-id="08cda-125">Вы получите предупреждение hello компьютера необходимо перезапустить hello изменения tootake влияет toobe.</span><span class="sxs-lookup"><span data-stu-id="08cda-125">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
10. <span data-ttu-id="08cda-126">Перезапустите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="08cda-126">Restart hello virtual machine.</span></span>

## <a name="change-hello-drive-letters"></a><span data-ttu-id="08cda-127">Изменение буквы диска hello</span><span class="sxs-lookup"><span data-stu-id="08cda-127">Change hello drive letters</span></span>
1. <span data-ttu-id="08cda-128">После перезапуска ВМ hello повторного выполнения входа toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08cda-128">Once hello VM restarts, log back on toohello VM.</span></span>
2. <span data-ttu-id="08cda-129">Нажмите кнопку hello **запустить** меню и введите **diskmgmt.msc** и нажмите ВВОД.</span><span class="sxs-lookup"><span data-stu-id="08cda-129">Click hello **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="08cda-130">Запускается компонент "Управление дисками".</span><span class="sxs-lookup"><span data-stu-id="08cda-130">Disk Management will start.</span></span>
3. <span data-ttu-id="08cda-131">Щелкните правой кнопкой мыши **D**, hello диск временного хранилища, а затем выберите **изменить букву диска или пути**.</span><span class="sxs-lookup"><span data-stu-id="08cda-131">Right-click on **D**, hello Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="08cda-132">В поле буквы диска выберите новый диск, например **T**, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="08cda-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="08cda-133">Щелкните правой кнопкой мыши на диске данных hello и выберите **изменить букву диска или пути**.</span><span class="sxs-lookup"><span data-stu-id="08cda-133">Right-click on hello data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="08cda-134">В поле буквы диска выберите диск **D** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="08cda-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a><span data-ttu-id="08cda-135">Переместите диск временного хранилища pagefile.sys toohello назад</span><span class="sxs-lookup"><span data-stu-id="08cda-135">Move pagefile.sys back toohello temporary storage drive</span></span>
1. <span data-ttu-id="08cda-136">Щелкните правой кнопкой мыши hello **запустить** и выбрать пункт **системы**</span><span class="sxs-lookup"><span data-stu-id="08cda-136">Right-click hello **Start** menu and select **System**</span></span>
2. <span data-ttu-id="08cda-137">Выберите в меню слева hello, **расширенных параметров системы**.</span><span class="sxs-lookup"><span data-stu-id="08cda-137">In hello left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="08cda-138">В hello **производительности** выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="08cda-138">In hello **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="08cda-139">Выберите hello **Дополнительно** вкладки.</span><span class="sxs-lookup"><span data-stu-id="08cda-139">Select hello **Advanced** tab.</span></span>
5. <span data-ttu-id="08cda-140">В hello **виртуальной памяти** выберите **изменений**.</span><span class="sxs-lookup"><span data-stu-id="08cda-140">In hello **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="08cda-141">Выберите диск ОС hello **C** и нажмите кнопку **без файла подкачки** и нажмите кнопку **задать**.</span><span class="sxs-lookup"><span data-stu-id="08cda-141">Select hello OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="08cda-142">Выберите диск временного хранилища hello **T** и нажмите кнопку **размер по выбору системы** и нажмите кнопку **задать**.</span><span class="sxs-lookup"><span data-stu-id="08cda-142">Select hello temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="08cda-143">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="08cda-143">Click **Apply**.</span></span> <span data-ttu-id="08cda-144">Вы получите предупреждение hello компьютера необходимо перезапустить hello изменения tootake влияет toobe.</span><span class="sxs-lookup"><span data-stu-id="08cda-144">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
9. <span data-ttu-id="08cda-145">Перезапустите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="08cda-145">Restart hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08cda-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="08cda-146">Next steps</span></span>
* <span data-ttu-id="08cda-147">Hello хранилища доступных tooyour виртуальной машины, можно увеличить [при подключении диска дополнительных данных](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08cda-147">You can increase hello storage available tooyour virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

