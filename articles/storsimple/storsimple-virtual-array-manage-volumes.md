---
title: "Управление томами в виртуальном массиве StorSimple | Документация Майкрософт"
description: "В статье описывается диспетчер устройств StorSimple и способы его использования для управления томами в виртуальном массиве StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: a507bf1866952cb79fa6334fed80c88cd207cd0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-service-to-manage-volumes-on-the-storsimple-virtual-array"></a><span data-ttu-id="3d060-103">Управление томами в виртуальном массиве StorSimple с помощью службы диспетчера устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="3d060-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="3d060-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="3d060-104">Overview</span></span>

<span data-ttu-id="3d060-105">В этом руководстве объясняется, как использовать службу диспетчера устройств StorSimple для создания томов и управления ими в виртуальном массиве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3d060-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="3d060-106">Служба диспетчера устройств StorSimple — это расширение портала Azure, которое позволяет управлять решениями StorSimple с помощью единого веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="3d060-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="3d060-107">Кроме управления общими ресурсами и томами, с помощью службы диспетчера устройств StorSimple можно просматривать оповещения, а также просматривать устройства, политики резервного копирования, каталог резервных копий и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="3d060-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="3d060-108">Типы томов</span><span class="sxs-lookup"><span data-stu-id="3d060-108">Volume Types</span></span>

<span data-ttu-id="3d060-109">Тома StorSimple могут относиться к таким типам:</span><span class="sxs-lookup"><span data-stu-id="3d060-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="3d060-110">**Локально закрепленные** — данные в этих томах всегда остаются в массиве и не переносятся в облако.</span><span class="sxs-lookup"><span data-stu-id="3d060-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="3d060-111">**Многоуровневые** — данные в этих томах могут переноситься в облако.</span><span class="sxs-lookup"><span data-stu-id="3d060-111">**Tiered**: Data in these volumes can spill to the cloud.</span></span> <span data-ttu-id="3d060-112">При создании многоуровневого тома подготавливается приблизительно 10 % пространства на локальном уровне и 90 % пространства в облаке.</span><span class="sxs-lookup"><span data-stu-id="3d060-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="3d060-113">Например, если подготовлен том объемом 1 ТБ, 100 ГБ будут находиться в локальном пространстве, а 900 ГБ — использоваться в облаке для распределения данных по уровням.</span><span class="sxs-lookup"><span data-stu-id="3d060-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="3d060-114">Это означает, что если на устройстве не хватает локального пространства, то нельзя подготовить многоуровневый том (так как 10 % места на локальном уровне не будет доступно).</span><span class="sxs-lookup"><span data-stu-id="3d060-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="3d060-115">Подготовленная емкость</span><span class="sxs-lookup"><span data-stu-id="3d060-115">Provisioned capacity</span></span>
<span data-ttu-id="3d060-116">В таблице ниже приведены значения максимальной подготовленной емкости для каждого типа тома.</span><span class="sxs-lookup"><span data-stu-id="3d060-116">Refer to the following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="3d060-117">**Идентификатор ограничения**</span><span class="sxs-lookup"><span data-stu-id="3d060-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="3d060-118">**Ограничение**</span><span class="sxs-lookup"><span data-stu-id="3d060-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="3d060-119">Минимальный размер многоуровневого тома</span><span class="sxs-lookup"><span data-stu-id="3d060-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="3d060-120">500 ГБ</span><span class="sxs-lookup"><span data-stu-id="3d060-120">500 GB</span></span>        |
| <span data-ttu-id="3d060-121">Максимальный размер многоуровневого тома</span><span class="sxs-lookup"><span data-stu-id="3d060-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="3d060-122">5 ТБ</span><span class="sxs-lookup"><span data-stu-id="3d060-122">5 TB</span></span>          |
| <span data-ttu-id="3d060-123">Минимальный размер локально закрепленного тома</span><span class="sxs-lookup"><span data-stu-id="3d060-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="3d060-124">50 ГБ</span><span class="sxs-lookup"><span data-stu-id="3d060-124">50 GB</span></span>         |
| <span data-ttu-id="3d060-125">Максимальный размер локально закрепленного тома</span><span class="sxs-lookup"><span data-stu-id="3d060-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="3d060-126">500 ГБ</span><span class="sxs-lookup"><span data-stu-id="3d060-126">500 GB</span></span>        |

## <a name="the-volumes-blade"></a><span data-ttu-id="3d060-127">Колонка "Тома"</span><span class="sxs-lookup"><span data-stu-id="3d060-127">The Volumes blade</span></span>
<span data-ttu-id="3d060-128">Меню **Тома** в колонке сводных данных о службе StorSimple отображает список томов хранилища в данном массиве StorSimple и позволяет управлять ими.</span><span class="sxs-lookup"><span data-stu-id="3d060-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span></span>

![Колонка "Тома"](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="3d060-130">Том обладает рядом атрибутов.</span><span class="sxs-lookup"><span data-stu-id="3d060-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="3d060-131">**Имя тома** — уникальное описательное имя, которое помогает идентифицировать том.</span><span class="sxs-lookup"><span data-stu-id="3d060-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span>
* <span data-ttu-id="3d060-132">**Состояние** — том может быть включен или отключен.</span><span class="sxs-lookup"><span data-stu-id="3d060-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="3d060-133">Если том отключен, он не виден инициаторам (серверам), которым разрешен к нему доступ.</span><span class="sxs-lookup"><span data-stu-id="3d060-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="3d060-134">**Тип** — указывает тип тома: **Многоуровневый** (по умолчанию) или **Локально закрепленный**.</span><span class="sxs-lookup"><span data-stu-id="3d060-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="3d060-135">**Емкость** — используемый объем данных по сравнению с общим объемом данных, который может быть сохранен инициатором (сервером).</span><span class="sxs-lookup"><span data-stu-id="3d060-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span></span>
* <span data-ttu-id="3d060-136">**Резервное копирование** — в виртуальном массиве StorSimple резервное копирование включено автоматически для всех томов.</span><span class="sxs-lookup"><span data-stu-id="3d060-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="3d060-137">**Соединенные узлы** — определяют инициаторы (серверы), которым разрешен доступ к этому тому.</span><span class="sxs-lookup"><span data-stu-id="3d060-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span></span>

![Сведения о томах](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="3d060-139">В этом руководстве приведены инструкции по выполнению следующих задач:</span><span class="sxs-lookup"><span data-stu-id="3d060-139">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="3d060-140">Добавление тома</span><span class="sxs-lookup"><span data-stu-id="3d060-140">Add a volume</span></span>
* <span data-ttu-id="3d060-141">Изменение тома</span><span class="sxs-lookup"><span data-stu-id="3d060-141">Modify a volume</span></span>
* <span data-ttu-id="3d060-142">Отключение тома</span><span class="sxs-lookup"><span data-stu-id="3d060-142">Take a volume offline</span></span>
* <span data-ttu-id="3d060-143">Удаление тома</span><span class="sxs-lookup"><span data-stu-id="3d060-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="3d060-144">Добавление тома</span><span class="sxs-lookup"><span data-stu-id="3d060-144">Add a volume</span></span>

1. <span data-ttu-id="3d060-145">В колонке сводных данных о службе StorSimple щелкните **+ Добавить том** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="3d060-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="3d060-146">Откроется колонка **Добавить том**.</span><span class="sxs-lookup"><span data-stu-id="3d060-146">This opens up the **Add volume** blade.</span></span>
   
    ![Добавить том](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="3d060-148">В колонке **Добавить том** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3d060-148">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="3d060-149">В поле **Имя тома** введите уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="3d060-149">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="3d060-150">Оно должно представлять собой строку длиной от 3 до 127 символов.</span><span class="sxs-lookup"><span data-stu-id="3d060-150">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="3d060-151">В раскрывающемся списке **Тип** укажите, том какого типа следует создать: **многоуровневый** или **локально закрепленный**.</span><span class="sxs-lookup"><span data-stu-id="3d060-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="3d060-152">Для рабочих нагрузок, которые требуют доступности в локальной среде, низкой задержки и более высокой производительности, выберите **Локально закрепленный том**.</span><span class="sxs-lookup"><span data-stu-id="3d060-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="3d060-153">Для любых других типов данных выберите **Многоуровневый том**.</span><span class="sxs-lookup"><span data-stu-id="3d060-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="3d060-154">В поле **Емкость** укажите размер тома.</span><span class="sxs-lookup"><span data-stu-id="3d060-154">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="3d060-155">Емкость многоуровневого тома должна составлять от 500 ГБ до 5 ТБ. Для локально закрепленного тома это значение должно быть в диапазоне от 50 до 500 ГБ.</span><span class="sxs-lookup"><span data-stu-id="3d060-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="3d060-156">Щелкните **Соединенные узлы**, выберите запись контроля доступа, соответствующую инициатору iSCSI, который требуется подключить к тому, и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3d060-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span>
3. <span data-ttu-id="3d060-157">Чтобы добавить новый подключенный узел, щелкните **Добавить**, введите обычное имя и полное имя iSCSI узла, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3d060-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Добавить том](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="3d060-159">После завершения настройки тома нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3d060-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="3d060-160">Будет создан том с указанными настройками, и вы увидите соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="3d060-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span></span> <span data-ttu-id="3d060-161">По умолчанию для тома включено резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="3d060-161">By default backup will be enabled for the volume.</span></span>
5. <span data-ttu-id="3d060-162">Чтобы убедиться, что том был создан, перейдите к колонке **Тома**.</span><span class="sxs-lookup"><span data-stu-id="3d060-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="3d060-163">Том должен отображаться в списке.</span><span class="sxs-lookup"><span data-stu-id="3d060-163">You should see the volume listed.</span></span>
   
    ![Том успешно создан](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="3d060-165">Изменение тома</span><span class="sxs-lookup"><span data-stu-id="3d060-165">Modify a volume</span></span>

<span data-ttu-id="3d060-166">Измените том, если необходимо изменить узлы, у которых есть доступ к нему.</span><span class="sxs-lookup"><span data-stu-id="3d060-166">Modify a volume when you need to change the hosts that access the volume.</span></span> <span data-ttu-id="3d060-167">Другие атрибуты тома нельзя изменить после его создания.</span><span class="sxs-lookup"><span data-stu-id="3d060-167">The other attributes of a volume cannot be modified once the volume has been created.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="3d060-168">Изменение тома</span><span class="sxs-lookup"><span data-stu-id="3d060-168">To modify a volume</span></span>

1. <span data-ttu-id="3d060-169">В разделе **Тома** в колонке сводных данных о службе StorSimple выберите виртуальный массив, в котором находится нужный том.</span><span class="sxs-lookup"><span data-stu-id="3d060-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span></span>
2. <span data-ttu-id="3d060-170">Чтобы просмотреть подключенный узел и изменить его на другой сервер, **выберите** том и щелкните **Соединенные узлы**.</span><span class="sxs-lookup"><span data-stu-id="3d060-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span></span>
   
    ![Редактирование тома](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="3d060-172">Чтобы сохранить изменения, щелкните **Сохранить** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="3d060-172">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="3d060-173">Указанные параметры будут применены, и появится соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="3d060-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="3d060-174">Отключение тома</span><span class="sxs-lookup"><span data-stu-id="3d060-174">Take a volume offline</span></span>

<span data-ttu-id="3d060-175">Если том необходимо изменить или удалить, его нужно отключить.</span><span class="sxs-lookup"><span data-stu-id="3d060-175">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="3d060-176">Если том отключен, он недоступен для чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="3d060-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="3d060-177">Отключать том следует на узле и на устройстве.</span><span class="sxs-lookup"><span data-stu-id="3d060-177">You will need to take the volume offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="3d060-178">Отключение тома</span><span class="sxs-lookup"><span data-stu-id="3d060-178">To take a volume offline</span></span>

1. <span data-ttu-id="3d060-179">Перед отключением тома убедитесь, что он не используется.</span><span class="sxs-lookup"><span data-stu-id="3d060-179">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="3d060-180">Сначала отключите том на узле.</span><span class="sxs-lookup"><span data-stu-id="3d060-180">Take the volume offline on the host first.</span></span> <span data-ttu-id="3d060-181">Это устранит потенциальный риск повреждения данных в томе.</span><span class="sxs-lookup"><span data-stu-id="3d060-181">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="3d060-182">Конкретные указания см. в инструкциях для вашей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="3d060-182">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="3d060-183">После перевода тома на узле в автономный режим отключите том на массиве, сделав следующее.</span><span class="sxs-lookup"><span data-stu-id="3d060-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span></span>
   
   * <span data-ttu-id="3d060-184">В разделе **Тома** в колонке сводных данных о службе StorSimple выберите виртуальный массив, где находится нужный том.</span><span class="sxs-lookup"><span data-stu-id="3d060-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span></span>
   * <span data-ttu-id="3d060-185">**Выберите** том и щелкните **…** (или щелкните правой кнопкой мыши в этой строке). Затем в контекстном меню выберите **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="3d060-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Отключенный том](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="3d060-187">Просмотрите сведения в колонке **Отключение** и подтвердите операцию.</span><span class="sxs-lookup"><span data-stu-id="3d060-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="3d060-188">Щелкните **Отключить**, чтобы перевести том в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="3d060-188">Click **Take offline** to take the volume offline.</span></span> <span data-ttu-id="3d060-189">Появится уведомление о выполняющейся операции.</span><span class="sxs-lookup"><span data-stu-id="3d060-189">You will see a notification of the operation in progress.</span></span>
   * <span data-ttu-id="3d060-190">Чтобы убедиться, что том был отключен, перейдите к колонке **Тома**.</span><span class="sxs-lookup"><span data-stu-id="3d060-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span></span> <span data-ttu-id="3d060-191">Состояние тома должно указывать, что он переведен в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="3d060-191">You should see the status of the volume as offline.</span></span>
     
       ![Подтверждение отключения тома](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="3d060-193">Удаление тома</span><span class="sxs-lookup"><span data-stu-id="3d060-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d060-194">Том можно удалить только в том случае, если он отключен.</span><span class="sxs-lookup"><span data-stu-id="3d060-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="3d060-195">Вот как можно удалить том.</span><span class="sxs-lookup"><span data-stu-id="3d060-195">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="3d060-196">Удаление тома</span><span class="sxs-lookup"><span data-stu-id="3d060-196">To delete a volume</span></span>

1. <span data-ttu-id="3d060-197">В разделе **Тома** в колонке сводных данных о службе StorSimple выберите виртуальный массив, в котором находится нужный том.</span><span class="sxs-lookup"><span data-stu-id="3d060-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span></span>
2. <span data-ttu-id="3d060-198">**Выберите** том и щелкните **…** (или щелкните правой кнопкой мыши в этой строке). Затем в контекстном меню выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="3d060-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Удаление тома](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="3d060-200">Проверьте состояние тома, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="3d060-200">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="3d060-201">Если требуется удалить том, который не отключен, сначала отключите его, а затем выполните указания в разделе [Отключение тома](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="3d060-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="3d060-202">При появлении запроса на подтверждение в колонке **Удалить** подтвердите операцию и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="3d060-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="3d060-203">Том будет удален, и в колонке **Тома** будет отображаться обновленный список томов в виртуальном массиве.</span><span class="sxs-lookup"><span data-stu-id="3d060-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d060-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3d060-204">Next steps</span></span>

<span data-ttu-id="3d060-205">Информация о [Клонировании тома StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="3d060-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

