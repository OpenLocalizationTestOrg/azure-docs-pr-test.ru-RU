---
title: "использует StorSimple Virtual Array aaaManage | Документы Microsoft"
description: "Описывает hello устройства StorSimple и объясняет, как toouse его toomanage общих папок на ваш StorSimple Virtual Array."
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
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="62824-103">Использовать общих папках toomanage службы диспетчера StorSimple устройство hello на hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="62824-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="62824-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="62824-104">Overview</span></span>

<span data-ttu-id="62824-105">Этот учебник объясняется, как toouse hello toocreate службы диспетчера StorSimple устройств и управление общими папками на ваш StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="62824-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="62824-106">службе диспетчера StorSimple устройство Hello — это расширение в hello портал Azure, которая позволяет управлять решения StorSimple из одного веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="62824-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="62824-107">В добавление toomanaging ресурсами и томами к нему можно использовать tooview службы диспетчера StorSimple устройство hello и управлять устройствами, просматривать оповещения, управлять политиками резервного копирования и управлять hello каталога резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="62824-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="62824-108">Типы общих папок</span><span class="sxs-lookup"><span data-stu-id="62824-108">Share Types</span></span>

<span data-ttu-id="62824-109">Есть два типа общих папок StorSimple.</span><span class="sxs-lookup"><span data-stu-id="62824-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="62824-110">**Локально закрепленный**: данные в этих ресурсах остается в массиве hello в любое время и не допускайте toohello облака.</span><span class="sxs-lookup"><span data-stu-id="62824-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="62824-111">**Многоуровневого**: данные в эти папки можно сбрасывать toohello облака.</span><span class="sxs-lookup"><span data-stu-id="62824-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="62824-112">При создании многоуровневого общего файлового ресурса, Подготовка приблизительно 10% hello пространства на локальном уровне hello и 90% пространства hello подготавливается в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="62824-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="62824-113">Например если подготовить общую папку 1 ТБ, располагается в локальное пространство hello 100 ГБ и 900 ГБ будет использоваться в облаке hello при hello уровни данных.</span><span class="sxs-lookup"><span data-stu-id="62824-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="62824-114">В свою очередь, это означает, что при выходе за пределы все hello Локальное пространство на устройстве hello, вы не можете подготавливать многоуровневого общего файлового ресурса (поскольку уровень не будут доступны на локальном hello необходимые hello 10%).</span><span class="sxs-lookup"><span data-stu-id="62824-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="62824-115">Подготовленная емкость</span><span class="sxs-lookup"><span data-stu-id="62824-115">Provisioned capacity</span></span>

<span data-ttu-id="62824-116">См. в следующей таблице для максимальной емкости, подготовленных для каждого общего ресурса типа toohello.</span><span class="sxs-lookup"><span data-stu-id="62824-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="62824-117">**Идентификатор ограничения**</span><span class="sxs-lookup"><span data-stu-id="62824-117">**Limit identifier**</span></span> | <span data-ttu-id="62824-118">**Ограничение**</span><span class="sxs-lookup"><span data-stu-id="62824-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="62824-119">Минимальный размер многоуровневого общего файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="62824-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="62824-120">500 ГБ</span><span class="sxs-lookup"><span data-stu-id="62824-120">500 GB</span></span> |
| <span data-ttu-id="62824-121">Максимальный размер многоуровневого общего файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="62824-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="62824-122">20 TБ</span><span class="sxs-lookup"><span data-stu-id="62824-122">20 TB</span></span> |
| <span data-ttu-id="62824-123">Минимальный размер локально закрепленного общего файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="62824-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="62824-124">50 ГБ</span><span class="sxs-lookup"><span data-stu-id="62824-124">50 GB</span></span> |
| <span data-ttu-id="62824-125">Максимальный размер локально закрепленного общего файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="62824-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="62824-126">2 ТБ</span><span class="sxs-lookup"><span data-stu-id="62824-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="62824-127">Hello колонке общих папок</span><span class="sxs-lookup"><span data-stu-id="62824-127">hello Shares blade</span></span>

<span data-ttu-id="62824-128">Hello **долей** меню к колонке сводки службы StorSimple отображение hello список общих ресурсов хранения в заданном массиве StorSimple и toomanage их.</span><span class="sxs-lookup"><span data-stu-id="62824-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![Колонка "Общие папки"](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="62824-130">Общая папка обладает рядом атрибутов.</span><span class="sxs-lookup"><span data-stu-id="62824-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="62824-131">**Имя общего ресурса** — описательное имя, которое должно быть уникальным и помогает определить общую папку hello.</span><span class="sxs-lookup"><span data-stu-id="62824-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="62824-132">**Состояние** — том может быть включен или отключен.</span><span class="sxs-lookup"><span data-stu-id="62824-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="62824-133">Если ресурс находится в автономном режиме, пользователи hello общей папки не будут может tooaccess его.</span><span class="sxs-lookup"><span data-stu-id="62824-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="62824-134">**Тип** — указывает, является ли папки hello **многоуровневый** (hello по умолчанию) или **локально закрепленный**.</span><span class="sxs-lookup"><span data-stu-id="62824-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="62824-135">**Емкость** — задает hello объем данных, используется в качестве сравниваемых toohello общий объем данных, которые могут храниться в общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="62824-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="62824-136">**Описание** — необязательный параметр, содержащий помогает описать hello общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="62824-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="62824-137">**Разрешения** -hello разрешения NTFS toohello папки, можно управлять с помощью проводника Windows.</span><span class="sxs-lookup"><span data-stu-id="62824-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="62824-138">**Резервного копирования** — в случае, если для hello StorSimple Virtual Array, все общие папки автоматически включается для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="62824-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Сведения об общих папках](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="62824-140">Используйте инструкции hello в этот учебник tooperform hello, следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="62824-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="62824-141">Добавление общей папки</span><span class="sxs-lookup"><span data-stu-id="62824-141">Add a share</span></span>
* <span data-ttu-id="62824-142">изменение общей папки;</span><span class="sxs-lookup"><span data-stu-id="62824-142">Modify a share</span></span>
* <span data-ttu-id="62824-143">отключение общей папки;</span><span class="sxs-lookup"><span data-stu-id="62824-143">Take a share offline</span></span>
* <span data-ttu-id="62824-144">удаление общей папки.</span><span class="sxs-lookup"><span data-stu-id="62824-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="62824-145">Добавление общей папки</span><span class="sxs-lookup"><span data-stu-id="62824-145">Add a share</span></span>

1. <span data-ttu-id="62824-146">Hello StorSimple службы сводки колонка, щелкните **+ добавить общую папку** hello командной строке.</span><span class="sxs-lookup"><span data-stu-id="62824-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="62824-147">Это открывает hello **добавить общую папку** колонку.</span><span class="sxs-lookup"><span data-stu-id="62824-147">This opens up hello **Add share** blade.</span></span>

    ![Добавление общей папки](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="62824-149">В hello **добавить общую папку** колонке hello следующие:</span><span class="sxs-lookup"><span data-stu-id="62824-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="62824-150">В hello **имя общего ресурса** введите уникальное имя для общей папки.</span><span class="sxs-lookup"><span data-stu-id="62824-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="62824-151">Hello имя должно быть строкой длиной 3 too127 символов.</span><span class="sxs-lookup"><span data-stu-id="62824-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="62824-152">Необязательный **описание** для общей папки hello.</span><span class="sxs-lookup"><span data-stu-id="62824-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="62824-153">Описание Hello помогает выявить владельцев hello общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="62824-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="62824-154">В hello **тип** раскрывающемся списке укажите ли toocreate **многоуровневый** или **локально закрепленный** совместного использования.</span><span class="sxs-lookup"><span data-stu-id="62824-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="62824-155">Для рабочих нагрузок, которые требуют локальных гарантий, низкой задержки и более высокой производительности, выберите тип **Локально закрепленная**.</span><span class="sxs-lookup"><span data-stu-id="62824-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="62824-156">Для других данных выберите тип **Многоуровневая**.</span><span class="sxs-lookup"><span data-stu-id="62824-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="62824-157">В hello **емкость** укажите размер общей папки hello hello.</span><span class="sxs-lookup"><span data-stu-id="62824-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="62824-158">Емкость многоуровневой общей папки должна составлять от 500 ГБ до 20 ТБ. Для локально закрепленных общих папок это значение должно быть в диапазоне от 50 ГБ до 2 ТБ.</span><span class="sxs-lookup"><span data-stu-id="62824-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="62824-159">В hello **значение по умолчанию полные права доступа** поле, назначьте hello разрешения toohello пользователя или группы hello, который обращается к этой общей папке.</span><span class="sxs-lookup"><span data-stu-id="62824-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="62824-160">Укажите имя hello hello пользователя или группы пользователей hello в  _john@contoso.com_  формат.</span><span class="sxs-lookup"><span data-stu-id="62824-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="62824-161">Мы рекомендуем использовать tooaccess права группы (вместо одного пользователя) tooallow пользователя admin этих общих папок.</span><span class="sxs-lookup"><span data-stu-id="62824-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="62824-162">После присвоения hello разрешения доступа, воспользуйтесь toomodify проводнике эти разрешения.</span><span class="sxs-lookup"><span data-stu-id="62824-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="62824-163">После завершения настройки общей папки нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="62824-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="62824-164">Ресурс будет создан с hello указано параметров и вы увидите уведомление.</span><span class="sxs-lookup"><span data-stu-id="62824-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="62824-165">По умолчанию резервное копирование будет включена для общей папки hello.</span><span class="sxs-lookup"><span data-stu-id="62824-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="62824-166">tooconfirm, hello общий ресурс был toohello успешно создан, выберите **долей** колонку.</span><span class="sxs-lookup"><span data-stu-id="62824-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="62824-167">Вы увидите совместного использования перечисленных hello.</span><span class="sxs-lookup"><span data-stu-id="62824-167">You should see hello share listed.</span></span>
   
    ![Общая папка успешно создана](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="62824-169">Изменение общей папки</span><span class="sxs-lookup"><span data-stu-id="62824-169">Modify a share</span></span>

<span data-ttu-id="62824-170">Изменение общей папки при необходимости описание hello toochange папки hello.</span><span class="sxs-lookup"><span data-stu-id="62824-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="62824-171">Никакие другие свойства общего ресурса можно изменить после создания общего ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="62824-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="62824-172">toomodify общей папки</span><span class="sxs-lookup"><span data-stu-id="62824-172">toomodify a share</span></span>

1. <span data-ttu-id="62824-173">Из hello **долей** выберите задание в колонке сводки службы StorSimple hello hello виртуального массива, на какие hello находится общей папки, которые вы хотите toomodify.</span><span class="sxs-lookup"><span data-stu-id="62824-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="62824-174">**Выберите** hello текущее описание общего ресурса tooview hello и измените его.</span><span class="sxs-lookup"><span data-stu-id="62824-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="62824-175">Сохранить изменения, нажав кнопку hello **Сохранить** панели команд.</span><span class="sxs-lookup"><span data-stu-id="62824-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="62824-176">Указанные параметры будут применены, и появится соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="62824-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="62824-177">Изменение общей папки</span><span class="sxs-lookup"><span data-stu-id="62824-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="62824-178">Отключение общей папки</span><span class="sxs-lookup"><span data-stu-id="62824-178">Take a share offline</span></span>

<span data-ttu-id="62824-179">Может потребоваться tootake общего ресурса в автономный режим при планировании toomodify или удалить его.</span><span class="sxs-lookup"><span data-stu-id="62824-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="62824-180">Отключенная общая папка недоступна для чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="62824-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="62824-181">Вам потребуется tootake hello общей папки автономный режим на узле hello, а также на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="62824-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="62824-182">tootake общего ресурса в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="62824-182">tootake a share offline</span></span>

1. <span data-ttu-id="62824-183">Убедитесь, что не используется перед выключением, совместно использующие hello в вопросе.</span><span class="sxs-lookup"><span data-stu-id="62824-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="62824-184">Принимать папки hello hello массива в автономный режим, выполнив следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="62824-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="62824-185">Из hello **долей** выберите задание в колонке сводки службы StorSimple hello hello виртуального массива, на какие hello находится общей папки, которые вы хотите tootake в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="62824-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="62824-186">**Выберите** hello общую папку и нажмите кнопку **...**  (либо щелкните правой кнопкой мыши в этой строке) и в контекстном меню hello выберите **перевод в автономный режим**.</span><span class="sxs-lookup"><span data-stu-id="62824-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Отключенная общая папка](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="62824-188">Просмотрите сведения о hello в hello **перевод в автономный режим** колонки и подтвердить свое согласие с hello операции.</span><span class="sxs-lookup"><span data-stu-id="62824-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="62824-189">Нажмите кнопку **перевод в автономный режим** tootake общего ресурса hello вне сети.</span><span class="sxs-lookup"><span data-stu-id="62824-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="62824-190">Вы увидите уведомление выполняется операция hello.</span><span class="sxs-lookup"><span data-stu-id="62824-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="62824-191">tooconfirm, hello общей папки успешно сделана toohello вне сети, выберите **долей** колонку.</span><span class="sxs-lookup"><span data-stu-id="62824-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="62824-192">Вы увидите состояние hello hello общей папки в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="62824-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="62824-193">Удаление общей папки</span><span class="sxs-lookup"><span data-stu-id="62824-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62824-194">Общую папку можно удалить только в том случае, если она отключена.</span><span class="sxs-lookup"><span data-stu-id="62824-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="62824-195">Выполните следующие шаги toodelete общую папку hello.</span><span class="sxs-lookup"><span data-stu-id="62824-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="62824-196">toodelete общей папки</span><span class="sxs-lookup"><span data-stu-id="62824-196">toodelete a share</span></span>

1. <span data-ttu-id="62824-197">Из hello **долей** выберите задание в колонке сводки службы StorSimple hello hello виртуального массива, в какой папке hello нужно toodelete находится.</span><span class="sxs-lookup"><span data-stu-id="62824-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="62824-198">**Выберите** hello общую папку и нажмите кнопку **...**  (либо щелкните правой кнопкой мыши в этой строке) и в контекстном меню hello выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="62824-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Удаление папки](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="62824-200">Проверьте состояние hello hello общей папки требуется toodelete.</span><span class="sxs-lookup"><span data-stu-id="62824-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="62824-201">Если требуется toodelete папки hello не находится в автономном режиме, отключите его сначала.</span><span class="sxs-lookup"><span data-stu-id="62824-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="62824-202">Следуйте указаниям hello [перевести ресурс в автономный режим](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="62824-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="62824-203">При появлении запроса на подтверждение в hello **удаление** колонке примите hello подтверждения и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="62824-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="62824-204">Hello общий ресурс будет удален и hello **долей** колонке показывает hello обновить список общих ресурсов в пределах виртуального массива hello.</span><span class="sxs-lookup"><span data-stu-id="62824-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62824-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62824-205">Next steps</span></span>
<span data-ttu-id="62824-206">Узнайте, каким образом слишком[клонировать общую папку StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="62824-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

