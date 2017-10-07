---
title: "Учебник резервного копирования Azure StorSimple Virtual Array aaaMicrosoft | Документы Microsoft"
description: "Описывает, как tooback копирование StorSimple Virtual Array общих папок и томов."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="dcfc4-103">Архивация общих ресурсов или томов на виртуальном массиве StorSimple</span><span class="sxs-lookup"><span data-stu-id="dcfc4-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="dcfc4-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="dcfc4-104">Overview</span></span>

<span data-ttu-id="dcfc4-105">Hello StorSimple Virtual Array является гибридного облака хранилища локального виртуального устройства, можно настроить в качестве файлового сервера или сервера iSCSI.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="dcfc4-106">виртуальный массив Hello позволяет toocreate пользователя hello запланированное и ручное резервное копирование всех hello папок или томов на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="dcfc4-107">Кроме того, при настройке в качестве файлового сервера устройство обеспечивает восстановление на уровне элементов.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="dcfc4-108">Этот учебник описывает, как планируется toocreate и резервных копий вручную и выполнять восстановление на уровне элементов toorestore удаленных файлов в виртуального массива.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="dcfc4-109">Этот учебник относится toohello StorSimple виртуальных массивов только.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="dcfc4-110">Сведения о серии 8000 go слишком[создается резервная копия для устройства серии 8000](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="dcfc4-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="dcfc4-111">Архивация общих папок и томов</span><span class="sxs-lookup"><span data-stu-id="dcfc4-111">Back up shares and volumes</span></span>

<span data-ttu-id="dcfc4-112">Резервные копии позволяют восстанавливать данные на определенный момент времени, улучшают их защиту и одновременно снижают время восстановления томов и общих папок.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="dcfc4-113">Архивировать общую папку или том на устройстве StorSimple можно двумя способами: **по расписанию** или **вручную**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="dcfc4-114">Каждый из методов hello рассматривается в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="dcfc4-115">Изменить время начала резервного копирования hello</span><span class="sxs-lookup"><span data-stu-id="dcfc4-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="dcfc4-116">В этом выпуске запланированные резервные копии создаются политикой по умолчанию, которая выполняется ежедневно в указанное время и создает резервную копию всех hello папок или томов на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="dcfc4-117">Это не возможные toocreate пользовательских политик для архивации по расписанию в данный момент.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="dcfc4-118">Виртуальный массив StorSimple имеет политику резервного копирования по умолчанию, который начинается в указанное время суток (22:30) и создает резервную копию всех hello папок или томов на устройстве hello один раз в день.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="dcfc4-119">Можно изменить время hello, на какие hello запуска архивации, но частота hello и hello хранения (который указывает hello количество резервных копий tooretain) нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="dcfc4-120">Во время этих резервных копий hello всего виртуального устройства резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="dcfc4-121">Потенциально это может повлиять на производительность hello устройства hello и влияет на hello рабочих нагрузок, развернутых на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="dcfc4-122">Поэтому мы рекомендуем планировать архивацию на время наименьшей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="dcfc4-123">резервное копирование по умолчанию hello toochange время начала, выполните следующие шаги в hello hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dcfc4-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="dcfc4-124">toochange hello время начала для политики резервного копирования по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="dcfc4-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="dcfc4-125">Go слишком**устройств**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-125">Go too**Devices**.</span></span> <span data-ttu-id="dcfc4-126">отображается список устройств, зарегистрированные в службе диспетчера StorSimple устройство Hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![Перейдите toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="dcfc4-128">Выберите и щелкните свое устройство.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-128">Select and click your device.</span></span> <span data-ttu-id="dcfc4-129">Hello **параметры** отображается колонку.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="dcfc4-130">Go слишком**Управление > политики резервного копирования,**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-130">Go too**Manage > Backup policies**.</span></span>
   
    ![выбор устройства](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="dcfc4-132">В hello **политики резервного копирования,** колонке hello время начала по умолчанию — 22:30.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="dcfc4-133">Можно указать новое время начала hello для ежедневного расписания hello в часовой пояс устройства.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![Перейдите toobackup политики](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="dcfc4-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="dcfc4-136">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="dcfc4-136">Take a manual backup</span></span>

<span data-ttu-id="dcfc4-137">В дополнение к этому tooscheduled резервных копий, вы сможете вручную (по запросу) резервная копия данных устройства в любое время.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="dcfc4-138">toocreate архивации вручную</span><span class="sxs-lookup"><span data-stu-id="dcfc4-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="dcfc4-139">Go слишком**устройств**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-139">Go too**Devices**.</span></span> <span data-ttu-id="dcfc4-140">Выберите устройство и щелкните правой кнопкой мыши **...**  в крайнем правом hello в выбранную строку hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="dcfc4-141">Hello контекстном меню, выберите **создайте резервную копию**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-141">From hello context menu, select **Take backup**.</span></span>
   
    ![Перейдите tootake резервной копии](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="dcfc4-143">В hello **создайте резервную копию** колонка, щелкните **создайте резервную копию**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="dcfc4-144">Это будет создана резервная копия все hello общие папки на файловом сервере hello или все тома hello iSCSI-сервера.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![запуск резервного копирования](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="dcfc4-146">Запустится архивация по требованию и начнет выполняться задание архивации.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![запуск резервного копирования](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="dcfc4-148">После успешного завершения задания hello, вы будете оповещены еще раз.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="dcfc4-149">Запускает процесс резервного копирования Hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-149">hello backup process then starts.</span></span>
   
    ![задание резервного копирования создано](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="dcfc4-151">Ход выполнения hello tootrack резервных копий hello и просмотрите сведения о задании hello, щелкните уведомление hello.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="dcfc4-152">Это занимает слишком **сведения о задании**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-152">This takes you too **Job details**.</span></span>
   
     ![сведения о задании архивации](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="dcfc4-154">После завершения резервного копирования hello go слишком**управления > каталог резервных копий**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="dcfc4-155">Вы увидите все общие папки hello (или томов) облачного моментального снимка на устройстве.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![Завершенное резервное копирование](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="dcfc4-157">Просмотр существующих резервных копий</span><span class="sxs-lookup"><span data-stu-id="dcfc4-157">View existing backups</span></span>
<span data-ttu-id="dcfc4-158">tooview hello существующие резервные копии, выполнять hello шагов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="dcfc4-159">tooview существующие резервные копии</span><span class="sxs-lookup"><span data-stu-id="dcfc4-159">tooview existing backups</span></span>

1. <span data-ttu-id="dcfc4-160">Go слишком**устройств** колонку.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-160">Go too**Devices** blade.</span></span> <span data-ttu-id="dcfc4-161">Выберите и щелкните свое устройство.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-161">Select and click your device.</span></span> <span data-ttu-id="dcfc4-162">В hello **параметры** колонке go слишком**управления > каталог резервных копий**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Перейдите в каталог toobackup](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="dcfc4-164">Укажите следующие критерии toobe, используемое для фильтрации hello:</span><span class="sxs-lookup"><span data-stu-id="dcfc4-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="dcfc4-165">**Диапазон времени** — **За последний час**, **За последние 24 часа**, **За последние 7 дней**, **За последние 30 дней**, **За последний год** и **Настраиваемая дата**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="dcfc4-166">**Устройства** — выберите из списка hello файловых серверов или серверов iSCSI, зарегистрированные в службе диспетчера StorSimple устройство.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="dcfc4-167">**Инициировано** — автоматически **Запланировано** (политикой архивации) или инициировано **Вручную** (пользователем).</span><span class="sxs-lookup"><span data-stu-id="dcfc4-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Фильтрация резервных копий](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="dcfc4-169">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-169">Click **Apply**.</span></span> <span data-ttu-id="dcfc4-170">Hello отфильтрованный список резервных копий отображается в hello **каталог резервных копий** колонку.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="dcfc4-171">Обратите внимание, что в определенный момент времени может отображаться только 100 резервных копий.</span><span class="sxs-lookup"><span data-stu-id="dcfc4-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Обновленный каталог резервных копий](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="dcfc4-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dcfc4-173">Next steps</span></span>

<span data-ttu-id="dcfc4-174">Дополнительные сведения см. в статье [Использование пользовательского веб-интерфейса для администрирования виртуального массива StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="dcfc4-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

