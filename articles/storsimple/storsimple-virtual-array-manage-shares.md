---
title: "Управление общими ресурсами виртуального массива StorSimple | Документация Майкрософт"
description: "В этой статье описывается диспетчер устройств StorSimple и способы его использования для управления общими папками в виртуальном массиве StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: e5c62689de36baa175001f5f4f70d87568876ef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-shares-on-the-storsimple-virtual-array"></a><span data-ttu-id="cc92d-103">Управление общими папками в виртуальном массиве StorSimple с помощью диспетчера устройств StorSimple</span><span class="sxs-lookup"><span data-stu-id="cc92d-103">Use the StorSimple Device Manager service to manage shares on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="cc92d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="cc92d-104">Overview</span></span>

<span data-ttu-id="cc92d-105">В этом руководстве объясняется, как использовать службу диспетчера устройств StorSimple для создания общих папок и управления ими в виртуальном массиве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cc92d-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="cc92d-106">Служба диспетчера устройств StorSimple — это расширение портала Azure, которое позволяет управлять решениями StorSimple с помощью единого веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="cc92d-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="cc92d-107">Кроме управления общими папками и томами, с помощью службы диспетчера устройств StorSimple можно просматривать устройства и управлять ими, просматривать оповещения, управлять политиками резервного копирования и каталогом резервных копий.</span><span class="sxs-lookup"><span data-stu-id="cc92d-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, manage backup policies, and manage the backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="cc92d-108">Типы общих папок</span><span class="sxs-lookup"><span data-stu-id="cc92d-108">Share Types</span></span>

<span data-ttu-id="cc92d-109">Есть два типа общих папок StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cc92d-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="cc92d-110">**Локально закрепленные** — данные в этих общих папках всегда остаются в массиве и не переносятся в облако.</span><span class="sxs-lookup"><span data-stu-id="cc92d-110">**Locally pinned**: Data in these shares stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="cc92d-111">**Многоуровневые** — данные в этих общих папках могут переноситься в облако.</span><span class="sxs-lookup"><span data-stu-id="cc92d-111">**Tiered**: Data in these shares can spill to the cloud.</span></span> <span data-ttu-id="cc92d-112">При создании многоуровневой общей папки подготавливается приблизительно 10 % пространства на локальном уровне и 90 % пространства в облаке.</span><span class="sxs-lookup"><span data-stu-id="cc92d-112">When you create a tiered share, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="cc92d-113">Например, если подготовлена общая папка объемом 1 ТБ, 100 ГБ будут находиться в локальном пространстве, а 900 ГБ будут использоваться в облаке для распределения данных по уровням.</span><span class="sxs-lookup"><span data-stu-id="cc92d-113">For example, if you provisioned a 1 TB share, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="cc92d-114">Это означает, что, если на устройстве не хватает локального пространства, то нельзя подготовить многоуровневую общую папку (так как 10 % места на локальном уровне не будут доступны).</span><span class="sxs-lookup"><span data-stu-id="cc92d-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="cc92d-115">Подготовленная емкость</span><span class="sxs-lookup"><span data-stu-id="cc92d-115">Provisioned capacity</span></span>

<span data-ttu-id="cc92d-116">В таблице ниже приведены значения максимальной подготовленной емкости для каждого типа общей папки.</span><span class="sxs-lookup"><span data-stu-id="cc92d-116">Refer to the following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="cc92d-117">**Идентификатор ограничения**</span><span class="sxs-lookup"><span data-stu-id="cc92d-117">**Limit identifier**</span></span> | <span data-ttu-id="cc92d-118">**Ограничение**</span><span class="sxs-lookup"><span data-stu-id="cc92d-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="cc92d-119">Минимальный размер многоуровневого общего файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="cc92d-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="cc92d-120">500 ГБ</span><span class="sxs-lookup"><span data-stu-id="cc92d-120">500 GB</span></span> |
| <span data-ttu-id="cc92d-121">Максимальный размер многоуровневого общего файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="cc92d-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="cc92d-122">20 TБ</span><span class="sxs-lookup"><span data-stu-id="cc92d-122">20 TB</span></span> |
| <span data-ttu-id="cc92d-123">Минимальный размер локально закрепленного общего файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="cc92d-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="cc92d-124">50 ГБ</span><span class="sxs-lookup"><span data-stu-id="cc92d-124">50 GB</span></span> |
| <span data-ttu-id="cc92d-125">Максимальный размер локально закрепленного общего файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="cc92d-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="cc92d-126">2 ТБ</span><span class="sxs-lookup"><span data-stu-id="cc92d-126">2 TB</span></span> |

## <a name="the-shares-blade"></a><span data-ttu-id="cc92d-127">Колонка "Общие папки"</span><span class="sxs-lookup"><span data-stu-id="cc92d-127">The Shares blade</span></span>

<span data-ttu-id="cc92d-128">Меню **Общие папки** в колонке сводки службы StorSimple отображает список общих папок хранилища в данном массиве StorSimple и позволяет управлять ими.</span><span class="sxs-lookup"><span data-stu-id="cc92d-128">The **Shares** menu on your StorSimple service summary blade displays the list of storage shares on a given StorSimple array and allows you to manage them.</span></span>

![Колонка "Общие папки"](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="cc92d-130">Общая папка обладает рядом атрибутов.</span><span class="sxs-lookup"><span data-stu-id="cc92d-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="cc92d-131">**Имя общей папки** — уникальное описательное имя, которое помогает идентифицировать общую папку.</span><span class="sxs-lookup"><span data-stu-id="cc92d-131">**Share Name** – A descriptive name that must be unique and helps identify the share.</span></span>
* <span data-ttu-id="cc92d-132">**Состояние** — том может быть включен или отключен.</span><span class="sxs-lookup"><span data-stu-id="cc92d-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="cc92d-133">Если общая папка находится в автономном режиме, пользователи не смогут получить к ней доступ.</span><span class="sxs-lookup"><span data-stu-id="cc92d-133">If a share is offline, users of the share will not be able to access it.</span></span>
* <span data-ttu-id="cc92d-134">**Тип** — указывает тип общей папки: **Многоуровневая** (по умолчанию) или **Локально закрепленная**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-134">**Type** – Indicates whether the share is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="cc92d-135">**Емкость** — используемый объем данных по сравнению с общим объемом данных, который может быть сохранен в общей папке.</span><span class="sxs-lookup"><span data-stu-id="cc92d-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored on the share.</span></span>
* <span data-ttu-id="cc92d-136">**Описание** — необязательный параметр, который помогает описать общую папку.</span><span class="sxs-lookup"><span data-stu-id="cc92d-136">**Description** – An optional setting that helps describe the share.</span></span>
* <span data-ttu-id="cc92d-137">**Разрешения** — разрешения NTFS для общей папки, которыми можно управлять в проводнике.</span><span class="sxs-lookup"><span data-stu-id="cc92d-137">**Permissions** - The NTFS permissions to the share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="cc92d-138">**Резервное копирование** — в виртуальном массиве StorSimple резервное копирование включено автоматически для всех общих папок.</span><span class="sxs-lookup"><span data-stu-id="cc92d-138">**Backup** – In case of the StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Сведения об общих папках](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="cc92d-140">В этом руководстве приведены инструкции по выполнению следующих задач:</span><span class="sxs-lookup"><span data-stu-id="cc92d-140">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="cc92d-141">добавление общей папки;</span><span class="sxs-lookup"><span data-stu-id="cc92d-141">Add a share</span></span>
* <span data-ttu-id="cc92d-142">изменение общей папки;</span><span class="sxs-lookup"><span data-stu-id="cc92d-142">Modify a share</span></span>
* <span data-ttu-id="cc92d-143">отключение общей папки;</span><span class="sxs-lookup"><span data-stu-id="cc92d-143">Take a share offline</span></span>
* <span data-ttu-id="cc92d-144">удаление общей папки.</span><span class="sxs-lookup"><span data-stu-id="cc92d-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="cc92d-145">Добавление общей папки</span><span class="sxs-lookup"><span data-stu-id="cc92d-145">Add a share</span></span>

1. <span data-ttu-id="cc92d-146">В колонке сводки службы StorSimple щелкните **+ Добавить общую папку** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="cc92d-146">From the StorSimple service summary blade, click **+ Add share** from the command bar.</span></span> <span data-ttu-id="cc92d-147">Откроется колонка **Добавить общую папку**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-147">This opens up the **Add share** blade.</span></span>

    ![Добавление общей папки](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="cc92d-149">В колонке **Добавить общую папку** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cc92d-149">In the **Add share** blade, do the following:</span></span>
   
    1. <span data-ttu-id="cc92d-150">В поле **Имя общей папки** введите уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="cc92d-150">In the **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="cc92d-151">Оно должно представлять собой строку длиной от 3 до 127 символов.</span><span class="sxs-lookup"><span data-stu-id="cc92d-151">The name must be a string that contains 3 to 127 characters.</span></span>

    2. <span data-ttu-id="cc92d-152">Необязательное **описание** общей папки.</span><span class="sxs-lookup"><span data-stu-id="cc92d-152">An optional **Description** for the share.</span></span> <span data-ttu-id="cc92d-153">Оно поможет определить ее владельцев.</span><span class="sxs-lookup"><span data-stu-id="cc92d-153">The description will help identify the share owners.</span></span>

    3. <span data-ttu-id="cc92d-154">В раскрывающемся списке **Тип** укажите, общую папку какого типа следует создать: **многоуровневую** или **локально закрепленную**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-154">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="cc92d-155">Для рабочих нагрузок, которые требуют локальных гарантий, низкой задержки и более высокой производительности, выберите тип **Локально закрепленная**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="cc92d-156">Для других данных выберите тип **Многоуровневая**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="cc92d-157">В поле **Емкость** укажите размер общей папки.</span><span class="sxs-lookup"><span data-stu-id="cc92d-157">In the **Capacity** field, specify the size of the share.</span></span> <span data-ttu-id="cc92d-158">Емкость многоуровневой общей папки должна составлять от 500 ГБ до 20 ТБ. Для локально закрепленных общих папок это значение должно быть в диапазоне от 50 ГБ до 2 ТБ.</span><span class="sxs-lookup"><span data-stu-id="cc92d-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="cc92d-159">В поле **Set default full permissions to** (Предоставить полные права по умолчанию) предоставьте разрешения пользователю или группе, которые будут обращаться к этой общей папке.</span><span class="sxs-lookup"><span data-stu-id="cc92d-159">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span></span> <span data-ttu-id="cc92d-160">Укажите имя пользователя или группы пользователей в формате _john@contoso.com_.</span><span class="sxs-lookup"><span data-stu-id="cc92d-160">Specify the name of the user or the user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="cc92d-161">Чтобы предоставить права администратора для доступа к этим общим папкам, рекомендуем использовать группы пользователей (вместо одного пользователя).</span><span class="sxs-lookup"><span data-stu-id="cc92d-161">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span></span> <span data-ttu-id="cc92d-162">Назначив разрешения здесь, вы сможете изменять их в проводнике.</span><span class="sxs-lookup"><span data-stu-id="cc92d-162">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span></span>
3. <span data-ttu-id="cc92d-163">После завершения настройки общей папки нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="cc92d-164">Будет создана общая папка с указанными настройками. Вы увидите соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="cc92d-164">A share will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="cc92d-165">По умолчанию для нее включено резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="cc92d-165">By default, backup will be enabled for the share.</span></span>
4. <span data-ttu-id="cc92d-166">Чтобы убедиться, что общая папка создана, перейдите в колонку **Общие папки**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-166">To confirm that the share was successfully created, go to the **Shares** blade.</span></span> <span data-ttu-id="cc92d-167">Общая папка должна отображаться в списке.</span><span class="sxs-lookup"><span data-stu-id="cc92d-167">You should see the share listed.</span></span>
   
    ![Общая папка успешно создана](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="cc92d-169">Изменение общей папки</span><span class="sxs-lookup"><span data-stu-id="cc92d-169">Modify a share</span></span>

<span data-ttu-id="cc92d-170">Вы можете изменить только описание общей папки.</span><span class="sxs-lookup"><span data-stu-id="cc92d-170">Modify a share when you need to change the description of the share.</span></span> <span data-ttu-id="cc92d-171">Другие свойства общей папки нельзя изменить после ее создания.</span><span class="sxs-lookup"><span data-stu-id="cc92d-171">No other share properties can be modified once the share is created.</span></span>

#### <a name="to-modify-a-share"></a><span data-ttu-id="cc92d-172">Изменение общей папки</span><span class="sxs-lookup"><span data-stu-id="cc92d-172">To modify a share</span></span>

1. <span data-ttu-id="cc92d-173">В разделе **Общие папки** в колонке сводки службы StorSimple выберите виртуальный массив, в котором находится нужная вам общая папка.</span><span class="sxs-lookup"><span data-stu-id="cc92d-173">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to modify resides.</span></span>
2. <span data-ttu-id="cc92d-174">**Выберите** общую папку, чтобы просмотреть текущее описание и изменить его.</span><span class="sxs-lookup"><span data-stu-id="cc92d-174">**Select** the share to view the current description and modify it.</span></span>
3. <span data-ttu-id="cc92d-175">Чтобы сохранить изменения, щелкните **Сохранить** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="cc92d-175">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="cc92d-176">Указанные параметры будут применены, и появится соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="cc92d-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="cc92d-177">Изменение общей папки</span><span class="sxs-lookup"><span data-stu-id="cc92d-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="cc92d-178">Отключение общей папки</span><span class="sxs-lookup"><span data-stu-id="cc92d-178">Take a share offline</span></span>

<span data-ttu-id="cc92d-179">Если общую папку необходимо изменить или удалить, ее нужно отключить.</span><span class="sxs-lookup"><span data-stu-id="cc92d-179">You may need to take a share offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="cc92d-180">Отключенная общая папка недоступна для чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="cc92d-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="cc92d-181">Отключать общую папку следует на узле и на устройстве.</span><span class="sxs-lookup"><span data-stu-id="cc92d-181">You will need to take the share offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-share-offline"></a><span data-ttu-id="cc92d-182">Отключение общей папки</span><span class="sxs-lookup"><span data-stu-id="cc92d-182">To take a share offline</span></span>

1. <span data-ttu-id="cc92d-183">Перед отключением общей папки убедитесь, что она не используется.</span><span class="sxs-lookup"><span data-stu-id="cc92d-183">Make sure that the share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="cc92d-184">Чтобы отключить общую папку, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cc92d-184">Take the share on the array offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="cc92d-185">В разделе **Общие папки** в колонке сводки службы StorSimple выберите виртуальный массив, в котором находится нужная общая папка.</span><span class="sxs-lookup"><span data-stu-id="cc92d-185">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to take offline resides.</span></span>

    2. <span data-ttu-id="cc92d-186">**Выберите** общую папку и нажмите кнопку **…** (или щелкните правой кнопкой мыши в этой строке). Затем в контекстном меню выберите **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-186">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Отключенная общая папка](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="cc92d-188">Просмотрите сведения в колонке **Отключение** и подтвердите операцию.</span><span class="sxs-lookup"><span data-stu-id="cc92d-188">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="cc92d-189">Щелкните **Отключить**, чтобы перевести общую папку в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="cc92d-189">Click **Take offline** to take the share offline.</span></span> <span data-ttu-id="cc92d-190">Появится уведомление о выполняющейся операции.</span><span class="sxs-lookup"><span data-stu-id="cc92d-190">You will see a notification of the operation in progress.</span></span>

    4. <span data-ttu-id="cc92d-191">Чтобы убедиться, что общая папка отключена, перейдите в колонку **Общие папки**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-191">To confirm that the share was successfully taken offline, go to the **Shares** blade.</span></span> <span data-ttu-id="cc92d-192">Состояние общей папки должно указывать, что она переведена в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="cc92d-192">You should see the status of the share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="cc92d-193">Удаление общей папки</span><span class="sxs-lookup"><span data-stu-id="cc92d-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc92d-194">Общую папку можно удалить только в том случае, если она отключена.</span><span class="sxs-lookup"><span data-stu-id="cc92d-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="cc92d-195">Вот как можно удалить общую папку.</span><span class="sxs-lookup"><span data-stu-id="cc92d-195">Complete the following steps to delete a share.</span></span>

#### <a name="to-delete-a-share"></a><span data-ttu-id="cc92d-196">Удаление общей папки</span><span class="sxs-lookup"><span data-stu-id="cc92d-196">To delete a share</span></span>

1. <span data-ttu-id="cc92d-197">В разделе **Общие папки** в колонке сводки службы StorSimple выберите виртуальный массив, в котором находится нужная общая папка.</span><span class="sxs-lookup"><span data-stu-id="cc92d-197">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish to delete resides.</span></span>
2. <span data-ttu-id="cc92d-198">**Выберите** общую папку и нажмите кнопку **…** (или щелкните правой кнопкой мыши в этой строке). Затем в контекстном меню выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-198">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Удаление папки](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="cc92d-200">Проверьте состояние общей папки, которую требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="cc92d-200">Check the status of the share you want to delete.</span></span> <span data-ttu-id="cc92d-201">Если общая папка, которую вы хотите удалить, не находится в автономном режиме, сначала отключите ее.</span><span class="sxs-lookup"><span data-stu-id="cc92d-201">If the share you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="cc92d-202">Следуйте указаниям по [отключению общей папки](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="cc92d-202">Follow the steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="cc92d-203">При появлении запроса на подтверждение в колонке **Удалить** подтвердите операцию и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="cc92d-203">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="cc92d-204">Общая папка будет удалена, и в колонке **Общие папки** появится обновленный список общих папок в виртуальном массиве.</span><span class="sxs-lookup"><span data-stu-id="cc92d-204">The share will now be deleted and the **Shares** blade shows the updated list of shares within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc92d-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc92d-205">Next steps</span></span>
<span data-ttu-id="cc92d-206">Узнайте, как [клонировать общую папку StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="cc92d-206">Learn how to [clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

