---
title: "тома StorSimple Virtual Array aaaManage | Документы Microsoft"
description: "Описывает hello устройства StorSimple и объясняет, как toouse его toomanage тома виртуального массива StorSimple."
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
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a><span data-ttu-id="1b00b-103">С помощью диспетчера устройств StorSimple службы toomanage томов на hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="1b00b-103">Use StorSimple Device Manager service toomanage volumes on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="1b00b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="1b00b-104">Overview</span></span>

<span data-ttu-id="1b00b-105">Этот учебник объясняется, как toouse hello toocreate службы диспетчера StorSimple устройств и управление томами на ваш StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="1b00b-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="1b00b-106">службе диспетчера StorSimple устройство Hello — это расширение в hello портал Azure, которая позволяет управлять решения StorSimple из одного веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1b00b-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="1b00b-107">В дополнение toomanaging ресурсами и томами можно использовать tooview службы диспетчера StorSimple устройство hello и управления устройствами, просматривать оповещения и также просматривать и управлять политик резервного копирования и каталога резервных копий hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="1b00b-108">Типы томов</span><span class="sxs-lookup"><span data-stu-id="1b00b-108">Volume Types</span></span>

<span data-ttu-id="1b00b-109">Тома StorSimple могут относиться к таким типам:</span><span class="sxs-lookup"><span data-stu-id="1b00b-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="1b00b-110">**Локально закрепленный**: данные в эти тома остается в массиве hello в любое время и не допускайте toohello облака.</span><span class="sxs-lookup"><span data-stu-id="1b00b-110">**Locally pinned**: Data in these volumes stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="1b00b-111">**Многоуровневого**: данные в этих томах может сбрасывать toohello облака.</span><span class="sxs-lookup"><span data-stu-id="1b00b-111">**Tiered**: Data in these volumes can spill toohello cloud.</span></span> <span data-ttu-id="1b00b-112">При создании многоуровневого тома Подготовка приблизительно 10% hello пространства на локальном уровне hello и 90% пространства hello подготавливается в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-112">When you create a tiered volume, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="1b00b-113">Например если подготовить том 1 ТБ, располагается в локальное пространство hello 100 ГБ и 900 ГБ будет использоваться в облаке hello при hello уровни данных.</span><span class="sxs-lookup"><span data-stu-id="1b00b-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="1b00b-114">В свою очередь, это означает, что при выходе за пределы все hello Локальное пространство на устройстве hello, вы не можете подготавливать многоуровневого тома (поскольку уровень не будут доступны на локальном hello необходимые hello 10%).</span><span class="sxs-lookup"><span data-stu-id="1b00b-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered volume (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="1b00b-115">Подготовленная емкость</span><span class="sxs-lookup"><span data-stu-id="1b00b-115">Provisioned capacity</span></span>
<span data-ttu-id="1b00b-116">См. в следующей таблице для максимальной емкости, подготовленных для каждого типа тома toohello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-116">Refer toohello following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="1b00b-117">**Идентификатор ограничения**</span><span class="sxs-lookup"><span data-stu-id="1b00b-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="1b00b-118">**Ограничение**</span><span class="sxs-lookup"><span data-stu-id="1b00b-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="1b00b-119">Минимальный размер многоуровневого тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="1b00b-120">500 ГБ</span><span class="sxs-lookup"><span data-stu-id="1b00b-120">500 GB</span></span>        |
| <span data-ttu-id="1b00b-121">Максимальный размер многоуровневого тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="1b00b-122">5 ТБ</span><span class="sxs-lookup"><span data-stu-id="1b00b-122">5 TB</span></span>          |
| <span data-ttu-id="1b00b-123">Минимальный размер локально закрепленного тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="1b00b-124">50 ГБ</span><span class="sxs-lookup"><span data-stu-id="1b00b-124">50 GB</span></span>         |
| <span data-ttu-id="1b00b-125">Максимальный размер локально закрепленного тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="1b00b-126">500 ГБ</span><span class="sxs-lookup"><span data-stu-id="1b00b-126">500 GB</span></span>        |

## <a name="hello-volumes-blade"></a><span data-ttu-id="1b00b-127">Hello тома колонку</span><span class="sxs-lookup"><span data-stu-id="1b00b-127">hello Volumes blade</span></span>
<span data-ttu-id="1b00b-128">Hello **тома** меню к колонке сводки службы StorSimple отображение hello список томов хранения данных в заданном массиве StorSimple и toomanage их.</span><span class="sxs-lookup"><span data-stu-id="1b00b-128">hello **Volumes** menu on your StorSimple service summary blade displays hello list of storage volumes on a given StorSimple array and allows you toomanage them.</span></span>

![Колонка "Тома"](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="1b00b-130">Том обладает рядом атрибутов.</span><span class="sxs-lookup"><span data-stu-id="1b00b-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="1b00b-131">**Имя тома** — описательное имя, которое должно быть уникальным и помогает идентифицировать тома hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-131">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span>
* <span data-ttu-id="1b00b-132">**Состояние** — том может быть включен или отключен.</span><span class="sxs-lookup"><span data-stu-id="1b00b-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="1b00b-133">Если том находится в автономном режиме, не видны tooinitiators (серверы), разрешается доступ toouse hello тома.</span><span class="sxs-lookup"><span data-stu-id="1b00b-133">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="1b00b-134">**Тип** — указывает, является ли том hello **многоуровневый** (hello по умолчанию) или **локально закрепленный**.</span><span class="sxs-lookup"><span data-stu-id="1b00b-134">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="1b00b-135">**Емкость** — задает hello объем данных, используется в качестве сравниваемых toohello общий объем данных, которые могут быть сохранены на hello инициатора (сервера).</span><span class="sxs-lookup"><span data-stu-id="1b00b-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored by hello initiator (server).</span></span>
* <span data-ttu-id="1b00b-136">**Резервного копирования** — в случае, если для hello StorSimple Virtual Array, все тома автоматически включается для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="1b00b-136">**Backup** – In case of hello StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="1b00b-137">**Подключение узлов** — указывает hello инициаторов (серверов), которые могут доступа toothis тома.</span><span class="sxs-lookup"><span data-stu-id="1b00b-137">**Connected hosts** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span>

![Сведения о томах](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="1b00b-139">Используйте инструкции hello в этот учебник tooperform hello, следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="1b00b-139">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="1b00b-140">Добавление тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-140">Add a volume</span></span>
* <span data-ttu-id="1b00b-141">Изменение тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-141">Modify a volume</span></span>
* <span data-ttu-id="1b00b-142">Отключение тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-142">Take a volume offline</span></span>
* <span data-ttu-id="1b00b-143">Удаление тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="1b00b-144">Добавление тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-144">Add a volume</span></span>

1. <span data-ttu-id="1b00b-145">Hello StorSimple службы сводки колонка, щелкните **+ добавить тома** hello командной строке.</span><span class="sxs-lookup"><span data-stu-id="1b00b-145">From hello StorSimple service summary blade, click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="1b00b-146">Это открывает hello **добавления тома** колонку.</span><span class="sxs-lookup"><span data-stu-id="1b00b-146">This opens up hello **Add volume** blade.</span></span>
   
    ![Добавить том](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="1b00b-148">В hello **добавления тома** колонке hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1b00b-148">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="1b00b-149">В hello **имя тома** введите уникальное имя для тома.</span><span class="sxs-lookup"><span data-stu-id="1b00b-149">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="1b00b-150">Hello имя должно быть строкой длиной 3 too127 символов.</span><span class="sxs-lookup"><span data-stu-id="1b00b-150">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="1b00b-151">В hello **тип** раскрывающийся список, укажите, является ли toocreate **многоуровневый** или **локально закрепленный** тома.</span><span class="sxs-lookup"><span data-stu-id="1b00b-151">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="1b00b-152">Для рабочих нагрузок, которые требуют доступности в локальной среде, низкой задержки и более высокой производительности, выберите **Локально закрепленный том**.</span><span class="sxs-lookup"><span data-stu-id="1b00b-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="1b00b-153">Для любых других типов данных выберите **Многоуровневый том**.</span><span class="sxs-lookup"><span data-stu-id="1b00b-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="1b00b-154">В hello **емкость** укажите размер тома, hello hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-154">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="1b00b-155">Емкость многоуровневого тома должна составлять от 500 ГБ до 5 ТБ. Для локально закрепленного тома это значение должно быть в диапазоне от 50 до 500 ГБ.</span><span class="sxs-lookup"><span data-stu-id="1b00b-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="1b00b-156">Нажмите кнопку **узлы подключены**, выберите доступ управления записи (ACR), соответствующий toohello инициатор iSCSI требуется tooconnect toothis тома и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="1b00b-156">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span>
3. <span data-ttu-id="1b00b-157">Щелкните tooadd новый подключенный узел **добавить новую**, введите имя для узла hello и его iSCSI полное имя (IQN), а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="1b00b-157">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Добавить том](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="1b00b-159">После завершения настройки тома нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1b00b-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="1b00b-160">Том будет создан с hello указано параметров и вы увидите уведомление на hello при успешном создании hello таким же.</span><span class="sxs-lookup"><span data-stu-id="1b00b-160">A volume will be created with hello specified settings and you will see a notification on hello successful creation of hello same.</span></span> <span data-ttu-id="1b00b-161">По умолчанию резервное копирование будет включена для тома hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-161">By default backup will be enabled for hello volume.</span></span>
5. <span data-ttu-id="1b00b-162">tooconfirm, hello тома был успешно создан, выберите toohello **тома** колонку.</span><span class="sxs-lookup"><span data-stu-id="1b00b-162">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="1b00b-163">Должны появиться в списке томов hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-163">You should see hello volume listed.</span></span>
   
    ![Том успешно создан](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="1b00b-165">Изменение тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-165">Modify a volume</span></span>

<span data-ttu-id="1b00b-166">Изменение тома при toochange hello узлов, которые обращаются к hello тома может потребоваться.</span><span class="sxs-lookup"><span data-stu-id="1b00b-166">Modify a volume when you need toochange hello hosts that access hello volume.</span></span> <span data-ttu-id="1b00b-167">Hello другие атрибуты тома нельзя изменить после создания тома hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-167">hello other attributes of a volume cannot be modified once hello volume has been created.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="1b00b-168">toomodify тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-168">toomodify a volume</span></span>

1. <span data-ttu-id="1b00b-169">Из hello **тома** выберите задание в колонке сводки службы StorSimple hello hello виртуального массива, на какие hello находится тома, которые вы хотите toomodify.</span><span class="sxs-lookup"><span data-stu-id="1b00b-169">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toomodify resides.</span></span>
2. <span data-ttu-id="1b00b-170">**Выберите** hello тома и нажмите кнопку **узлы подключены** tooview hello подключенного узла и измените его tooa другой сервер.</span><span class="sxs-lookup"><span data-stu-id="1b00b-170">**Select** hello volume and click **Connected hosts** tooview hello currently connected host and modify it tooa different server.</span></span>
   
    ![Редактирование тома](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="1b00b-172">Сохранить изменения, нажав кнопку hello **Сохранить** панели команд.</span><span class="sxs-lookup"><span data-stu-id="1b00b-172">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="1b00b-173">Указанные параметры будут применены, и появится соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="1b00b-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="1b00b-174">Отключение тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-174">Take a volume offline</span></span>

<span data-ttu-id="1b00b-175">Может потребоваться tootake том в автономный режим при планировании toomodify или удалить его.</span><span class="sxs-lookup"><span data-stu-id="1b00b-175">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="1b00b-176">Если том отключен, он недоступен для чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="1b00b-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="1b00b-177">Вам потребуется tootake hello том в автономный режим на узле hello, а также на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-177">You will need tootake hello volume offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="1b00b-178">tootake том в автономный режим</span><span class="sxs-lookup"><span data-stu-id="1b00b-178">tootake a volume offline</span></span>

1. <span data-ttu-id="1b00b-179">Убедитесь, что hello тома не используется перед выключением.</span><span class="sxs-lookup"><span data-stu-id="1b00b-179">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="1b00b-180">Отключите hello том в автономный режим на узле hello сначала.</span><span class="sxs-lookup"><span data-stu-id="1b00b-180">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="1b00b-181">Это исключит любой потенциальный риск повреждения данных в томе hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-181">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="1b00b-182">Конкретные шаги см. инструкции toohello по операционной системе узла.</span><span class="sxs-lookup"><span data-stu-id="1b00b-182">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="1b00b-183">После hello тома на узле hello находится в автономном режиме, принимать тома hello hello массива в автономный режим, выполнив следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-183">After hello volume on hello host is offline, take hello volume on hello array  offline by performing hello following steps:</span></span>
   
   * <span data-ttu-id="1b00b-184">Из hello **тома** выберите задание в колонке сводки службы StorSimple hello hello виртуального массива, на какие hello находится тома, которые вы хотите tootake в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="1b00b-184">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you tootake offline resides.</span></span>
   * <span data-ttu-id="1b00b-185">**Выберите** hello тома и нажмите кнопку **...**  (либо щелкните правой кнопкой мыши в этой строке) и в контекстном меню hello выберите **перевод в автономный режим**.</span><span class="sxs-lookup"><span data-stu-id="1b00b-185">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Отключенный том](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="1b00b-187">Просмотрите сведения о hello в hello **перевод в автономный режим** колонки и подтвердить свое согласие с hello операции.</span><span class="sxs-lookup"><span data-stu-id="1b00b-187">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="1b00b-188">Нажмите кнопку **перевод в автономный режим** tootake том hello в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="1b00b-188">Click **Take offline** tootake hello volume offline.</span></span> <span data-ttu-id="1b00b-189">Вы увидите уведомление выполняется операция hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-189">You will see a notification of hello operation in progress.</span></span>
   * <span data-ttu-id="1b00b-190">tooconfirm, hello тома успешно переводится в автономный режим, перейдите в раздел toohello **тома** колонку.</span><span class="sxs-lookup"><span data-stu-id="1b00b-190">tooconfirm that hello volume was successfully taken offline, go toohello **Volumes** blade.</span></span> <span data-ttu-id="1b00b-191">Вы увидите состояние hello тома hello как вне сети.</span><span class="sxs-lookup"><span data-stu-id="1b00b-191">You should see hello status of hello volume as offline.</span></span>
     
       ![Подтверждение отключения тома](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="1b00b-193">Удаление тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b00b-194">Том можно удалить только в том случае, если он отключен.</span><span class="sxs-lookup"><span data-stu-id="1b00b-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="1b00b-195">Выполните следующие шаги toodelete тома hello.</span><span class="sxs-lookup"><span data-stu-id="1b00b-195">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="1b00b-196">toodelete тома</span><span class="sxs-lookup"><span data-stu-id="1b00b-196">toodelete a volume</span></span>

1. <span data-ttu-id="1b00b-197">Из hello **тома** выберите задание в колонке сводки службы StorSimple hello hello виртуального массива, на какие hello находится тома, которые вы хотите toodelete.</span><span class="sxs-lookup"><span data-stu-id="1b00b-197">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toodelete resides.</span></span>
2. <span data-ttu-id="1b00b-198">**Выберите** hello тома и нажмите кнопку **...**  (либо щелкните правой кнопкой мыши в этой строке) и в контекстном меню hello выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="1b00b-198">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Удаление тома](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="1b00b-200">Проверьте состояние hello hello тома требуется toodelete.</span><span class="sxs-lookup"><span data-stu-id="1b00b-200">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="1b00b-201">При hello тома требуется toodelete не находится в автономном режиме, выполните его автономного hello во-первых, следующие действия [перевести том в автономный режим](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="1b00b-201">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="1b00b-202">При появлении запроса на подтверждение в hello **удаление** колонке примите hello подтверждения и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="1b00b-202">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="1b00b-203">Hello тома будут удалены и hello **тома** колонке покажет hello обновить список томов в hello виртуального массива.</span><span class="sxs-lookup"><span data-stu-id="1b00b-203">hello volume will now be deleted and hello **Volumes** blade will show hello updated list of volumes within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b00b-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b00b-204">Next steps</span></span>

<span data-ttu-id="1b00b-205">Узнайте, каким образом слишком[клонирование тома StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="1b00b-205">Learn how too[clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

