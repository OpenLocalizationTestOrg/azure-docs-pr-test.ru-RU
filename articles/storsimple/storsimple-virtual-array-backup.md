---
title: "Руководство по архивации виртуального массива Microsoft Azure StorSimple | Документация Майкрософт"
description: "В этой статье описано резервное копирование общих папок и томов виртуального массива StorSimple."
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
ms.openlocfilehash: c926f0c80ce56cac3106ad97ec3ec2e18a8e2cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="5a214-103">Архивация общих ресурсов или томов на виртуальном массиве StorSimple</span><span class="sxs-lookup"><span data-stu-id="5a214-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="5a214-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="5a214-104">Overview</span></span>

<span data-ttu-id="5a214-105">Виртуальный массив StorSimple — это локальное виртуальное устройство для гибридного облачного хранилища. Устройство может быть настроено в качестве файлового сервера или сервера iSCSI.</span><span class="sxs-lookup"><span data-stu-id="5a214-105">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="5a214-106">Виртуальный массив позволяет пользователю выполнять плановую архивацию и создавать резервные копии всех общих ресурсов или томов на устройстве вручную.</span><span class="sxs-lookup"><span data-stu-id="5a214-106">The virtual array allows the user to create scheduled and manual backups of all the shares or volumes on the device.</span></span> <span data-ttu-id="5a214-107">Кроме того, при настройке в качестве файлового сервера устройство обеспечивает восстановление на уровне элементов.</span><span class="sxs-lookup"><span data-stu-id="5a214-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="5a214-108">В этом руководстве описывается, как выполнять плановую архивацию и создавать резервные копии вручную, а также как выполнить восстановление на уровне элементов для восстановления удаленных файлов в виртуальном массиве.</span><span class="sxs-lookup"><span data-stu-id="5a214-108">This tutorial describes how to create scheduled and manual backups and perform item-level recovery to restore a deleted file on your virtual array.</span></span>

<span data-ttu-id="5a214-109">Это руководство относится только к виртуальным массивам StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5a214-109">This tutorial applies to the StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="5a214-110">Сведения об устройствах серии 8000 см. в статье о [создании резервной копии для устройства серии 8000](storsimple-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="5a214-110">For information on 8000 series, go to [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="5a214-111">Архивация общих папок и томов</span><span class="sxs-lookup"><span data-stu-id="5a214-111">Back up shares and volumes</span></span>

<span data-ttu-id="5a214-112">Резервные копии позволяют восстанавливать данные на определенный момент времени, улучшают их защиту и одновременно снижают время восстановления томов и общих папок.</span><span class="sxs-lookup"><span data-stu-id="5a214-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="5a214-113">Архивировать общую папку или том на устройстве StorSimple можно двумя способами: **по расписанию** или **вручную**.</span><span class="sxs-lookup"><span data-stu-id="5a214-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="5a214-114">Каждый метод описан в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="5a214-114">Each of the methods is discussed in the following sections.</span></span>

## <a name="change-the-backup-start-time"></a><span data-ttu-id="5a214-115">Изменение времени начала архивации</span><span class="sxs-lookup"><span data-stu-id="5a214-115">Change the backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="5a214-116">В этом выпуске резервные копии создаются по расписанию стандартной политикой. Политика запускается ежедневно в указанное время и выполняет резервное копирование общих папок или томов на устройстве.</span><span class="sxs-lookup"><span data-stu-id="5a214-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span></span> <span data-ttu-id="5a214-117">Создание пользовательских политик для резервного копирования по расписанию в данный момент не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5a214-117">It is not possible to create custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="5a214-118">В виртуальном массиве StorSimple есть политика архивации по умолчанию, которая запускается ежедневно в указанное время суток (22:30) и выполняет архивацию общих ресурсов или томов на устройстве.</span><span class="sxs-lookup"><span data-stu-id="5a214-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span></span> <span data-ttu-id="5a214-119">Вы можете изменить время начала резервного копирования. Частота и параметры хранения (определяют число хранимых резервных копий) изменению не подлежат.</span><span class="sxs-lookup"><span data-stu-id="5a214-119">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span></span> <span data-ttu-id="5a214-120">При этом архивируется все виртуальное устройство.</span><span class="sxs-lookup"><span data-stu-id="5a214-120">During these backups, the entire virtual device is backed up.</span></span> <span data-ttu-id="5a214-121">Это может повлиять на производительность устройства и рабочие нагрузки, развернутые на устройстве.</span><span class="sxs-lookup"><span data-stu-id="5a214-121">This could potentially impact the performance of the device and affect the workloads deployed on the device.</span></span> <span data-ttu-id="5a214-122">Поэтому мы рекомендуем планировать архивацию на время наименьшей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5a214-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="5a214-123">Чтобы изменить стандартное время начала архивации, выполните на [портале Azure](https://portal.azure.com/) указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5a214-123">To change the default backup start time, perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-change-the-start-time-for-the-default-backup-policy"></a><span data-ttu-id="5a214-124">Изменение времени запуска стандартной политики резервного копирования</span><span class="sxs-lookup"><span data-stu-id="5a214-124">To change the start time for the default backup policy</span></span>

1. <span data-ttu-id="5a214-125">Откройте колонку **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="5a214-125">Go to **Devices**.</span></span> <span data-ttu-id="5a214-126">Отобразится список устройств, зарегистрированных в службе диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5a214-126">The list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![переход в колонку "Устройства"](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="5a214-128">Выберите и щелкните свое устройство.</span><span class="sxs-lookup"><span data-stu-id="5a214-128">Select and click your device.</span></span> <span data-ttu-id="5a214-129">Откроется колонка **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="5a214-129">The **Settings** blade will be displayed.</span></span> <span data-ttu-id="5a214-130">Перейдите в колонку **Управление > Политики архивации**.</span><span class="sxs-lookup"><span data-stu-id="5a214-130">Go to **Manage > Backup policies**.</span></span>
   
    ![выбор устройства](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="5a214-132">В колонке **Политики архивации** указано время начала по умолчанию — 22:30.</span><span class="sxs-lookup"><span data-stu-id="5a214-132">In the **Backup policies** blade, the default start time is 22:30.</span></span> <span data-ttu-id="5a214-133">Вы можете указать новое время начала в поле "Ежедневное расписание по часовому поясу устройства".</span><span class="sxs-lookup"><span data-stu-id="5a214-133">You can specify the new start time for the daily schedule in device time zone.</span></span>
   
    ![переход к политикам архивации](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="5a214-135">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5a214-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="5a214-136">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="5a214-136">Take a manual backup</span></span>

<span data-ttu-id="5a214-137">В дополнение к архивации по расписанию вы можете в любое время создавать резервные копии данных устройства вручную (архивация по запросу).</span><span class="sxs-lookup"><span data-stu-id="5a214-137">In addition to scheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="5a214-138">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="5a214-138">To create a manual backup</span></span>

1. <span data-ttu-id="5a214-139">Откройте колонку **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="5a214-139">Go to **Devices**.</span></span> <span data-ttu-id="5a214-140">Выберите свое устройство и щелкните правой кнопкой мыши **...** в дальней правой части выделенной строки.</span><span class="sxs-lookup"><span data-stu-id="5a214-140">Select your device and right-click **...** at the far right in the selected row.</span></span> <span data-ttu-id="5a214-141">В контекстном меню выберите пункт **Сделать архив**.</span><span class="sxs-lookup"><span data-stu-id="5a214-141">From the context menu, select **Take backup**.</span></span>
   
    ![переход к пункту "Сделать архив"](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="5a214-143">В колонке **Сделать архив** щелкните **Сделать архив**.</span><span class="sxs-lookup"><span data-stu-id="5a214-143">In the **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="5a214-144">После этого будут созданы резервные копии всех общих ресурсов на файловом сервере или всех томов на сервере iSCSI.</span><span class="sxs-lookup"><span data-stu-id="5a214-144">This will backup all the shares on the file server or all the volumes on your iSCSI server.</span></span> 
   
    ![запуск резервного копирования](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="5a214-146">Запустится архивация по требованию и начнет выполняться задание архивации.</span><span class="sxs-lookup"><span data-stu-id="5a214-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![запуск резервного копирования](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="5a214-148">После успешного завершения задания снова отобразиться уведомление.</span><span class="sxs-lookup"><span data-stu-id="5a214-148">Once the job has successfully completed, you are notified again.</span></span> <span data-ttu-id="5a214-149">После этого начнется процесс архивации.</span><span class="sxs-lookup"><span data-stu-id="5a214-149">The backup process then starts.</span></span>
   
    ![задание резервного копирования создано](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="5a214-151">Чтобы отслеживать ход выполнения архивации и просмотреть сведения о задании, щелкните уведомление.</span><span class="sxs-lookup"><span data-stu-id="5a214-151">To track the progress of the backups and look at the job details, click the notification.</span></span> <span data-ttu-id="5a214-152">Отобразится вкладка **Сведения о задании**.</span><span class="sxs-lookup"><span data-stu-id="5a214-152">This takes you to  **Job details**.</span></span>
   
     ![сведения о задании архивации](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="5a214-154">После завершения архивации щелкните **Управление > Каталог архивов**.</span><span class="sxs-lookup"><span data-stu-id="5a214-154">After the backup is complete, go to **Management > Backup catalog**.</span></span> <span data-ttu-id="5a214-155">Появится облачный моментальный снимок всех общих ресурсов (или томов) на устройстве.</span><span class="sxs-lookup"><span data-stu-id="5a214-155">You will see a cloud snapshot of all the shares (or volumes) on your device.</span></span>
   
    ![Завершенное резервное копирование](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="5a214-157">Просмотр существующих резервных копий</span><span class="sxs-lookup"><span data-stu-id="5a214-157">View existing backups</span></span>
<span data-ttu-id="5a214-158">Чтобы просмотреть существующие резервные копии, выполните на портале Azure указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5a214-158">To view the existing backups, perform the following steps in the Azure portal.</span></span>

#### <a name="to-view-existing-backups"></a><span data-ttu-id="5a214-159">Просмотр списка существующих резервных копий</span><span class="sxs-lookup"><span data-stu-id="5a214-159">To view existing backups</span></span>

1. <span data-ttu-id="5a214-160">Откройте колонку **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="5a214-160">Go to **Devices** blade.</span></span> <span data-ttu-id="5a214-161">Выберите и щелкните свое устройство.</span><span class="sxs-lookup"><span data-stu-id="5a214-161">Select and click your device.</span></span> <span data-ttu-id="5a214-162">В колонке **Параметры** выберите **Управление > Каталог архивов**.</span><span class="sxs-lookup"><span data-stu-id="5a214-162">In the **Settings** blade, go to **Management > Backup Catalog**.</span></span>
   
    ![Переход к каталогу архивов](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="5a214-164">Укажите следующие критерии для фильтрации:</span><span class="sxs-lookup"><span data-stu-id="5a214-164">Specify the following criteria to be used for filtering:</span></span>
   
    - <span data-ttu-id="5a214-165">**Диапазон времени** — **За последний час**, **За последние 24 часа**, **За последние 7 дней**, **За последние 30 дней**, **За последний год** и **Настраиваемая дата**.</span><span class="sxs-lookup"><span data-stu-id="5a214-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="5a214-166">**Устройства.** Выберите в списке файловых серверов или серверов iSCSI, зарегистрированных в вашей службе диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5a214-166">**Devices** – select from the list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="5a214-167">**Инициировано** — автоматически **Запланировано** (политикой архивации) или инициировано **Вручную** (пользователем).</span><span class="sxs-lookup"><span data-stu-id="5a214-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Фильтрация резервных копий](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="5a214-169">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="5a214-169">Click **Apply**.</span></span> <span data-ttu-id="5a214-170">В колонке **Каталог архивов** отобразится отфильтрованный список резервных копий.</span><span class="sxs-lookup"><span data-stu-id="5a214-170">The filtered list of backups is displayed in the **Backup catalog** blade.</span></span> <span data-ttu-id="5a214-171">Обратите внимание, что в определенный момент времени может отображаться только 100 резервных копий.</span><span class="sxs-lookup"><span data-stu-id="5a214-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Обновленный каталог резервных копий](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="5a214-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a214-173">Next steps</span></span>

<span data-ttu-id="5a214-174">Дополнительные сведения см. в статье [Использование пользовательского веб-интерфейса для администрирования виртуального массива StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="5a214-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

