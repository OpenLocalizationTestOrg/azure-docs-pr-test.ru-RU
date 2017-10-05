---
title: "Клонирование тома устройства StorSimple серии 8000 | Документация Майкрософт"
description: "Здесь описываются различные типы клонирования и потребления, а также объясняется, как использовать резервный набор данных для клонирования отдельного тома на устройстве StorSimple серии 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 70c85bcb2c26d2ad3d0515d24e028f84495634c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-clone-a-volume"></a><span data-ttu-id="50cb0-103">Использование службы диспетчера устройств StorSimple на портале Azure для клонирования тома</span><span class="sxs-lookup"><span data-stu-id="50cb0-103">Use the StorSimple Device Manager service in Azure portal to clone a volume</span></span>

## <a name="overview"></a><span data-ttu-id="50cb0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="50cb0-104">Overview</span></span>

<span data-ttu-id="50cb0-105">В этом руководстве описывается, как можно использовать резервный набор данных для клонирования отдельного тома с помощью колонки **каталога резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="50cb0-105">This tutorial describes how you can use a backup set to clone an individual volume via the **Backup catalog** blade.</span></span> <span data-ttu-id="50cb0-106">Также объясняется разница между *временным* и *постоянным* клонированием.</span><span class="sxs-lookup"><span data-stu-id="50cb0-106">It also explains the difference between *transient* and *permanent* clones.</span></span> <span data-ttu-id="50cb0-107">Рекомендации в этом руководстве относятся ко всем устройствам StorSimple серии 8000 с обновлением 3 и более поздними.</span><span class="sxs-lookup"><span data-stu-id="50cb0-107">The guidance in this tutorial applies to all the StorSimple 8000 series device running Update 3 or later.</span></span>

<span data-ttu-id="50cb0-108">На странице **каталога резервного копирования** службы диспетчера устройств StorSimple находятся все резервные наборы данных, созданные во время автоматической или ручной архивации.</span><span class="sxs-lookup"><span data-stu-id="50cb0-108">The StorSimple Device Manager service **Backup catalog** blade displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="50cb0-109">Затем можно выбрать том в резервном наборе данных для клонирования.</span><span class="sxs-lookup"><span data-stu-id="50cb0-109">You can then select a volume in a backup set to clone.</span></span>

 ![Список резервных наборов данных](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a><span data-ttu-id="50cb0-111">Рекомендации для клонирования тома</span><span class="sxs-lookup"><span data-stu-id="50cb0-111">Considerations for cloning a volume</span></span>

<span data-ttu-id="50cb0-112">Обратите внимание на следующую информацию при клонировании тома.</span><span class="sxs-lookup"><span data-stu-id="50cb0-112">Consider the following information when cloning a volume.</span></span>

- <span data-ttu-id="50cb0-113">Клон ведет себя аналогично обычному тому.</span><span class="sxs-lookup"><span data-stu-id="50cb0-113">A clone behaves in the same way as a regular volume.</span></span> <span data-ttu-id="50cb0-114">Любая операция, которая возможна в томе, доступна для клона.</span><span class="sxs-lookup"><span data-stu-id="50cb0-114">Any operation that is possible on a volume is available for the clone.</span></span>

- <span data-ttu-id="50cb0-115">Мониторинг и резервное копирование отключены по умолчанию для клонированного тома.</span><span class="sxs-lookup"><span data-stu-id="50cb0-115">Monitoring and default backup are automatically disabled on a cloned volume.</span></span> <span data-ttu-id="50cb0-116">Необходимо настроить клонированный том для всех резервных копий.</span><span class="sxs-lookup"><span data-stu-id="50cb0-116">You would need to configure a cloned volume for any backups.</span></span>

- <span data-ttu-id="50cb0-117">Локально закрепленный том клонируется как многоуровневый том.</span><span class="sxs-lookup"><span data-stu-id="50cb0-117">A locally pinned volume is cloned as a tiered volume.</span></span> <span data-ttu-id="50cb0-118">Если требуется, чтобы клонированный том был закреплен локально, можно преобразовать клон в локально закрепленный том после успешного завершения операции клонирования.</span><span class="sxs-lookup"><span data-stu-id="50cb0-118">If you need the cloned volume to be locally pinned, you can convert the clone to a locally pinned volume after the clone operation is successfully completed.</span></span> <span data-ttu-id="50cb0-119">Подробнее о преобразовании многоуровневого тома в локально закрепленный том см. в разделе [Изменение типа тома](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span><span class="sxs-lookup"><span data-stu-id="50cb0-119">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>

- <span data-ttu-id="50cb0-120">При попытке преобразовать клонированный том из многоуровневого в локально закрепленный сразу после клонирования (пока он остается временным клоном) произойдет следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="50cb0-120">If you try to convert a cloned volume from tiered to locally pinned immediately after cloning (when it is still a transient clone), the conversion fails with the following error message:</span></span>

    `Unable to modify the usage type for volume {0}. This can happen if the volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry the modify operation.`

    <span data-ttu-id="50cb0-121">Эта ошибка возникает только в том случае, если выполняется клонирование на другое устройство.</span><span class="sxs-lookup"><span data-stu-id="50cb0-121">This error is received only if you are cloning on to a different device.</span></span> <span data-ttu-id="50cb0-122">Вы можете преобразовать том в локально закрепленный, если сначала преобразуете временный клон в постоянный клон.</span><span class="sxs-lookup"><span data-stu-id="50cb0-122">You can successfully convert the volume to locally pinned if you first convert the transient clone to a permanent clone.</span></span> <span data-ttu-id="50cb0-123">Чтобы преобразовать временный клон в постоянный, создайте для него облачный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="50cb0-123">Take a cloud snapshot of the transient clone to convert it to a permanent clone.</span></span>

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="50cb0-124">Создание клона тома</span><span class="sxs-lookup"><span data-stu-id="50cb0-124">Create a clone of a volume</span></span>

<span data-ttu-id="50cb0-125">С помощью локального или облачного моментального снимка можно создать клон на том же устройстве, другом устройстве или даже на облачном устройстве.</span><span class="sxs-lookup"><span data-stu-id="50cb0-125">You can create a clone on the same device, another device, or even a cloud appliance by using a local or cloud snapshot.</span></span>

<span data-ttu-id="50cb0-126">Ниже описана процедура создания клона из каталога резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="50cb0-126">The procedure below describes how to create a clone from the backup catalog.</span></span>  <span data-ttu-id="50cb0-127">Еще один способ запустить клонирование — перейти в раздел **Тома**, выбрать том, а затем щелкнуть правой кнопкой мыши для вызова контекстного меню и выбрать **Клонировать**.</span><span class="sxs-lookup"><span data-stu-id="50cb0-127">An alternative method to initiate clone is to go to **Volumes**, select a volume, then right-click to invoke the context menu and select **Clone**.</span></span>

<span data-ttu-id="50cb0-128">Выполните следующие действия, чтобы создать клон тома из каталога резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="50cb0-128">Perform the following steps to create a clone of your volume from the backup catalog.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="50cb0-129">Клонирование тома</span><span class="sxs-lookup"><span data-stu-id="50cb0-129">To clone a volume</span></span>

1. <span data-ttu-id="50cb0-130">В службе диспетчера устройств StorSimple выберите **Каталог резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="50cb0-130">Go to your StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="50cb0-131">Выберите резервный набор данных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="50cb0-131">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="50cb0-132">Выберите подходящее устройство.</span><span class="sxs-lookup"><span data-stu-id="50cb0-132">Select the appropriate device.</span></span>
   2. <span data-ttu-id="50cb0-133">В раскрывающемся списке выберите том или политику резервного копирования для той резервной копии, которую нужно выбрать.</span><span class="sxs-lookup"><span data-stu-id="50cb0-133">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="50cb0-134">Укажите интервал времени.</span><span class="sxs-lookup"><span data-stu-id="50cb0-134">Specify the time range.</span></span>
   4. <span data-ttu-id="50cb0-135">Щелкните **Применить**, чтобы выполнить этот запрос.</span><span class="sxs-lookup"><span data-stu-id="50cb0-135">Click **Apply** to execute this query.</span></span>

    <span data-ttu-id="50cb0-136">В списке резервных наборов данных должны отобразиться резервные копии, связанные с выбранным томом или политикой резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="50cb0-136">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
   
    ![Список резервных наборов данных](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. <span data-ttu-id="50cb0-138">Разверните резервный набор данных для просмотра связанных томов.</span><span class="sxs-lookup"><span data-stu-id="50cb0-138">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="50cb0-139">Перед восстановлением эти тома необходимо отключить на узле и устройстве.</span><span class="sxs-lookup"><span data-stu-id="50cb0-139">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="50cb0-140">Откройте колонку **Тома** со списком томов устройства, а затем следуйте указаниям, описанным в разделе [Отключение тома](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline), чтобы отключить том.</span><span class="sxs-lookup"><span data-stu-id="50cb0-140">Access the volumes on the **Volumes** blade of your device, and then follow the steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) to take them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="50cb0-141">Прежде чем отключать том на устройстве, сначала отключите его на узле.</span><span class="sxs-lookup"><span data-stu-id="50cb0-141">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="50cb0-142">Если тома на узле не переведены в автономный режим, это может привести к повреждению данных.</span><span class="sxs-lookup"><span data-stu-id="50cb0-142">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   
4. <span data-ttu-id="50cb0-143">Вернитесь к **каталогу резервного копирования** и выберите том в резервном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="50cb0-143">Navigate back to the **Backup catalog** and select a volume in a backup set.</span></span> <span data-ttu-id="50cb0-144">Щелкните правой кнопкой мыши, а затем в контекстном меню выберите **Клонировать**.</span><span class="sxs-lookup"><span data-stu-id="50cb0-144">Right-click and then from the context menu, select **Clone**.</span></span>

   ![Список резервных наборов данных](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. <span data-ttu-id="50cb0-146">В колонке **Клонировать** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="50cb0-146">In the **Clone** blade, do the following steps:</span></span>
   
    1. <span data-ttu-id="50cb0-147">Укажите целевое устройство.</span><span class="sxs-lookup"><span data-stu-id="50cb0-147">Identify a target device.</span></span> <span data-ttu-id="50cb0-148">Это расположение, где будет создана копия.</span><span class="sxs-lookup"><span data-stu-id="50cb0-148">This is the location where the clone will be created.</span></span> <span data-ttu-id="50cb0-149">Можно выбрать одно устройство или указать другое устройство.</span><span class="sxs-lookup"><span data-stu-id="50cb0-149">You can choose the same device or specify another device.</span></span>

      > [!NOTE]
      > <span data-ttu-id="50cb0-150">Убедитесь, что на целевом устройстве достаточно места для клонирования.</span><span class="sxs-lookup"><span data-stu-id="50cb0-150">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
       
    2. <span data-ttu-id="50cb0-151">Укажите уникальное имя для клона.</span><span class="sxs-lookup"><span data-stu-id="50cb0-151">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="50cb0-152">Имя должно содержать от 3 до 127 символов.</span><span class="sxs-lookup"><span data-stu-id="50cb0-152">The name must contain between 3 and 127 characters.</span></span>
      
        > [!NOTE]
        > <span data-ttu-id="50cb0-153">В поле **Клонировать том как** будет стоять значение **Многоуровневый**, даже если вы клонируете локально закрепленный том.</span><span class="sxs-lookup"><span data-stu-id="50cb0-153">The **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="50cb0-154">Этот параметр изменить нельзя. Если же вы хотите, чтобы клонированный том также был локально закреплен, то клон можно преобразовать в локально закрепленный том после того, как вы успешно завершите клонирование.</span><span class="sxs-lookup"><span data-stu-id="50cb0-154">You cannot change this setting; however, if you need the cloned volume to be locally pinned as well, you can convert the clone to a locally pinned volume after you successfully create the clone.</span></span> <span data-ttu-id="50cb0-155">Подробнее о преобразовании многоуровневого тома в локально закрепленный том см. в разделе [Изменение типа тома](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span><span class="sxs-lookup"><span data-stu-id="50cb0-155">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>
          
    3. <span data-ttu-id="50cb0-156">В разделе **Connected hosts** (Соединенные узлы) укажите запись контроля доступа (ACR) для клона.</span><span class="sxs-lookup"><span data-stu-id="50cb0-156">Under **Connected hosts**, specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="50cb0-157">Можно добавить новую запись ACR или выбрать из существующего списка.</span><span class="sxs-lookup"><span data-stu-id="50cb0-157">You can add a new ACR or choose from the existing list.</span></span> <span data-ttu-id="50cb0-158">Запись контроля доступа определит, какие узлы могут получать доступ к этому клону.</span><span class="sxs-lookup"><span data-stu-id="50cb0-158">The ACR will determine which hosts can access this clone.</span></span>
      
        ![Список резервных наборов данных](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. <span data-ttu-id="50cb0-160">Щелкните **Клонировать**, чтобы завершить операцию.</span><span class="sxs-lookup"><span data-stu-id="50cb0-160">Click **Clone** to complete the operation.</span></span>

4. <span data-ttu-id="50cb0-161">Инициируется задание клонирования, и после успешного создания клона появится уведомление.</span><span class="sxs-lookup"><span data-stu-id="50cb0-161">A clone job is initiated and you are notified when the clone is successfully created.</span></span> <span data-ttu-id="50cb0-162">Щелкните уведомление о задании или перейдите в колонку **Задания**, чтобы отслеживать задание клонирования.</span><span class="sxs-lookup"><span data-stu-id="50cb0-162">Click the job notification or go to **Jobs** blade to monitor the clone job.</span></span>

    ![Список резервных наборов данных](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. <span data-ttu-id="50cb0-164">После завершения задания клонирования перейдите в раздел устройства и щелкните **Тома**.</span><span class="sxs-lookup"><span data-stu-id="50cb0-164">After the clone job is complete, go to your device and then click **Volumes**.</span></span> <span data-ttu-id="50cb0-165">В списке томов вы увидите только что созданный том клон в том же контейнере томов, что и исходный том.</span><span class="sxs-lookup"><span data-stu-id="50cb0-165">In the list of volumes, you should see the clone that was just created in the same volume container that has the source volume.</span></span>

    ![Список резервных наборов данных](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

<span data-ttu-id="50cb0-167">Клон, созданный таким способом, является временным.</span><span class="sxs-lookup"><span data-stu-id="50cb0-167">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="50cb0-168">Дополнительные сведения о типах клонов см. в разделе [Сравнение временных и постоянных клонов](#transient-vs-permanent-clones).</span><span class="sxs-lookup"><span data-stu-id="50cb0-168">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>


## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="50cb0-169">Сравнение временных и постоянных клонов</span><span class="sxs-lookup"><span data-stu-id="50cb0-169">Transient vs. permanent clones</span></span>
<span data-ttu-id="50cb0-170">Временные клоны создаются только при клонировании на другое устройство.</span><span class="sxs-lookup"><span data-stu-id="50cb0-170">Transient clones are created only when you clone to another device.</span></span> <span data-ttu-id="50cb0-171">Можно клонировать определенный том из резервного набора данных на другое устройство, управляемое диспетчером устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="50cb0-171">You can clone a specific volume from a backup set to a different device managed by the StorSimple Device Manager.</span></span> <span data-ttu-id="50cb0-172">Временный клон будет содержать ссылки на данные в исходном томе и использовать эти данные для локальных операций чтения и записи с целевым устройством.</span><span class="sxs-lookup"><span data-stu-id="50cb0-172">The transient clone has references to the data in the original volume and uses that data to read and write locally on the target device.</span></span>

<span data-ttu-id="50cb0-173">После создания облачного моментального снимка временного клона полученная копия станет *постоянным* клоном.</span><span class="sxs-lookup"><span data-stu-id="50cb0-173">After you take a cloud snapshot of a transient clone, the resulting clone is a *permanent* clone.</span></span> <span data-ttu-id="50cb0-174">В ходе этого процесса в облаке создается копия данных, и время копирования данных зависит от размера данных и задержек среды Azure (это копирование из Azure в Azure).</span><span class="sxs-lookup"><span data-stu-id="50cb0-174">During this process, a copy of the data is created on the cloud and the time to copy this data is determined by the size of the data and the Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="50cb0-175">Данный процесс может длиться от считанных дней до нескольких недель.</span><span class="sxs-lookup"><span data-stu-id="50cb0-175">This process can take days to weeks.</span></span> <span data-ttu-id="50cb0-176">Таким образом временный клон становится постоянным и не имеет ссылок на данные в исходном томе, с которого он был клонирован.</span><span class="sxs-lookup"><span data-stu-id="50cb0-176">The transient clone becomes a permanent clone and doesn’t have any references to the original volume data that it was cloned from.</span></span>

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="50cb0-177">Сценарии для временных и постоянных клонов</span><span class="sxs-lookup"><span data-stu-id="50cb0-177">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="50cb0-178">В следующих разделах рассматриваются ситуации использования временных и постоянных клонов.</span><span class="sxs-lookup"><span data-stu-id="50cb0-178">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="50cb0-179">Восстановление на уровне элементов с помощью временного клона</span><span class="sxs-lookup"><span data-stu-id="50cb0-179">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="50cb0-180">Необходимо восстановить файл презентации Microsoft PowerPoint, созданный один год назад.</span><span class="sxs-lookup"><span data-stu-id="50cb0-180">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="50cb0-181">ИТ-администратор определяет резервную копию из этого времени и выбирает том.</span><span class="sxs-lookup"><span data-stu-id="50cb0-181">Your IT administrator identifies the specific backup from that time, and then filters the volume.</span></span> <span data-ttu-id="50cb0-182">Затем администратор создает точную копию тома, находит нужный файл и предоставляет его вам.</span><span class="sxs-lookup"><span data-stu-id="50cb0-182">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="50cb0-183">В этом сценарии используется временный клон.</span><span class="sxs-lookup"><span data-stu-id="50cb0-183">In this scenario, a transient clone is used.</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="50cb0-184">Тестирование в рабочей среде с помощью постоянного клона</span><span class="sxs-lookup"><span data-stu-id="50cb0-184">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="50cb0-185">Необходимо проверить ошибки в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="50cb0-185">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="50cb0-186">Создайте клон тома в рабочей среде, а затем создайте облачный моментальный снимок этого клона, чтобы создать независимый клонированный том.</span><span class="sxs-lookup"><span data-stu-id="50cb0-186">You create a clone of the volume in the production environment and then take a cloud snapshot of this clone to create an independent cloned volume.</span></span> <span data-ttu-id="50cb0-187">В этом сценарии используется постоянный клон.</span><span class="sxs-lookup"><span data-stu-id="50cb0-187">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50cb0-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50cb0-188">Next steps</span></span>
* <span data-ttu-id="50cb0-189">Узнайте, как [восстановить том StorSimple из резервного набора данных](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="50cb0-189">Learn how to [restore a StorSimple volume from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="50cb0-190">Узнайте, как [использовать службу диспетчера устройств StorSimple для администрирования устройства StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="50cb0-190">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

