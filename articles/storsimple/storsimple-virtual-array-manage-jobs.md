---
title: "aaaView StorSimple Virtual Array задания и управлять ими | Документы Microsoft"
description: "Описывает hello устройство страница службы диспетчера StorSimple заданий и как toouse его tootrack недавно и текущего задания для hello StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="55a03-103">Используйте задания tooview службы диспетчера StorSimple устройство hello для hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="55a03-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="55a03-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="55a03-104">Overview</span></span>
<span data-ttu-id="55a03-105">Hello **заданий** колонке предоставляет один центральный портал для просмотра и управления заданиями, запущенными на виртуальных массивов, подключенный tooyour службы диспетчера StorSimple устройство.</span><span class="sxs-lookup"><span data-stu-id="55a03-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="55a03-106">Вы можете просматривать запущенные, завершенные и невыполненные задания для нескольких виртуальных устройств.</span><span class="sxs-lookup"><span data-stu-id="55a03-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="55a03-107">Результаты представляются в табличном формате.</span><span class="sxs-lookup"><span data-stu-id="55a03-107">Results are presented in a tabular format.</span></span>

![Колонка "Задания"](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="55a03-109">Можно быстро найти hello заданий, которые вам нужны путем фильтрации по полям, такие как:</span><span class="sxs-lookup"><span data-stu-id="55a03-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="55a03-110">**Временной диапазон** — задания могут быть отфильтрованный на основе hello диапазон дат и времени.</span><span class="sxs-lookup"><span data-stu-id="55a03-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="55a03-111">**Устройства** — задания инициируются на службы tooyour конкретного устройства подключены.</span><span class="sxs-lookup"><span data-stu-id="55a03-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="55a03-112">Hello отфильтрованные задания Далее помещаются в зависимости от hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="55a03-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="55a03-113">**Имя** — имя задания hello может быть **все**, **резервного копирования**, **клон**, **отработки отказа**, **загрузки обновлений** , или **установить обновления**.</span><span class="sxs-lookup"><span data-stu-id="55a03-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="55a03-114">**Состояние** — задания могут находиться в следующих состояниях: **Все**, **Выполняется**, **Успешно**, **Сбой** или **Отменено**.</span><span class="sxs-lookup"><span data-stu-id="55a03-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="55a03-115">**Сущность** — hello задания могут быть связаны с тома, папки или устройства.</span><span class="sxs-lookup"><span data-stu-id="55a03-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="55a03-116">**Устройство** — hello именем hello устройства, на какие hello задание было запущено.</span><span class="sxs-lookup"><span data-stu-id="55a03-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="55a03-117">**Запущен на** — hello время начала задания hello.</span><span class="sxs-lookup"><span data-stu-id="55a03-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="55a03-118">**Длительность** — hello длительность задания hello была запущена.</span><span class="sxs-lookup"><span data-stu-id="55a03-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="55a03-119">**Состояние** — можно выполнять поиск по всем заданиям, запущенным и завершенным заданиям, а также заданиям, завершившихся сбоем.</span><span class="sxs-lookup"><span data-stu-id="55a03-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="55a03-120">**Тип задания** — тип задания hello можно все содержимое, резервное копирование, восстановление, переход на другой ресурс, загружать обновления или установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="55a03-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="55a03-121">Hello список заданий обновляется каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="55a03-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="55a03-122">Просмотреть сведения о задании</span><span class="sxs-lookup"><span data-stu-id="55a03-122">View job details</span></span>
<span data-ttu-id="55a03-123">Выполните следующие шаги tooview hello сведения о любом задании hello.</span><span class="sxs-lookup"><span data-stu-id="55a03-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="55a03-124">сведения о задании tooview</span><span class="sxs-lookup"><span data-stu-id="55a03-124">tooview job details</span></span>
1. <span data-ttu-id="55a03-125">На hello **заданий** колонки, отображения hello заданий необходимо выполнить в результате выполнения запроса с подходящими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="55a03-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="55a03-126">Можно выполнять поиск по завершенным или выполняющимся заданиям.</span><span class="sxs-lookup"><span data-stu-id="55a03-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="55a03-127">Выберите задание из hello табличный список заданий.</span><span class="sxs-lookup"><span data-stu-id="55a03-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![Колонка "Задание"](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="55a03-129">Внизу hello страницы приветствия щелкните **сведения**.</span><span class="sxs-lookup"><span data-stu-id="55a03-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="55a03-130">В hello **сведения** диалоговое окно, можно просмотреть состояние, сведения и статистические данные о времени.</span><span class="sxs-lookup"><span data-stu-id="55a03-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="55a03-131">Hello следующей иллюстрации показан пример hello **сведений о задании резервного копирования** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="55a03-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![Сведения о задании](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="55a03-133">Сбои заданий при приостановке hello виртуальной машины в низкоуровневой оболочке hello</span><span class="sxs-lookup"><span data-stu-id="55a03-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="55a03-134">Если задание находится в хода выполнения на устройстве hello (виртуальная машина подготовлены в низкоуровневой оболочке) и StorSimple Virtual Array приостанавливается на более 15 минут, hello задание завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="55a03-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="55a03-135">Это время tooyour StorSimple Virtual Array, не синхронизировано с временем hello Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="55a03-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="55a03-136">Вы увидите hello следующая ошибка: «время на вашем устройстве не синхронизирован с временем hello Microsoft Azure с более чем за 15 минут.</span><span class="sxs-lookup"><span data-stu-id="55a03-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="55a03-137">Убедитесь, что hello низкоуровневой оболочки и время устройства hello синхронизируются с сервер NTP.</span><span class="sxs-lookup"><span data-stu-id="55a03-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="55a03-138">Verify that there are no connectivity issues (Проверьте наличие проблем с подключением).</span><span class="sxs-lookup"><span data-stu-id="55a03-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="55a03-139">tootroubleshoot проблемы с подключением, запустите диагностические тесты из hello локального пользовательского веб-интерфейса виртуального устройства.»</span><span class="sxs-lookup"><span data-stu-id="55a03-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="55a03-140">Эти ошибки применить задания toobackup, восстановление, обновление и переход на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="55a03-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="55a03-141">Если подготовки виртуальной машины в Hyper-V hello machine со временем синхронизирует время вашего низкоуровневой оболочки.</span><span class="sxs-lookup"><span data-stu-id="55a03-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="55a03-142">После этого можно перезапустить задание.</span><span class="sxs-lookup"><span data-stu-id="55a03-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55a03-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55a03-143">Next steps</span></span>
<span data-ttu-id="55a03-144">[Узнайте, как toouse hello tooadminister пользовательского интерфейса локального web виртуального массива StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="55a03-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

