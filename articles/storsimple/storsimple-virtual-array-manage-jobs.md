---
title: "Просмотр заданий виртуального массива StorSimple и управление ими | Документация Майкрософт"
description: "Описывается страница \"Задания\" службы диспетчера устройств StorSimple и способы ее использования для отслеживания недавних и текущих заданий для виртуального массива StorSimple."
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
ms.openlocfilehash: 3fd1c262a8ce94d8e98f2b066a8028d974b15b1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a><span data-ttu-id="62bd1-103">Использование службы диспетчера устройств StorSimple для просмотра заданий виртуального массива StorSimple</span><span class="sxs-lookup"><span data-stu-id="62bd1-103">Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="62bd1-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="62bd1-104">Overview</span></span>
<span data-ttu-id="62bd1-105">Колонка **Задания** — это единый центральный портал для просмотра заданий, которые были запущены на виртуальных массивах, подключенных к службе диспетчера устройств StorSimple, и управления ими.</span><span class="sxs-lookup"><span data-stu-id="62bd1-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="62bd1-106">Вы можете просматривать запущенные, завершенные и невыполненные задания для нескольких виртуальных устройств.</span><span class="sxs-lookup"><span data-stu-id="62bd1-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="62bd1-107">Результаты представляются в табличном формате.</span><span class="sxs-lookup"><span data-stu-id="62bd1-107">Results are presented in a tabular format.</span></span>

![Колонка "Задания"](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="62bd1-109">Вы можете быстро найти задания, которые вам нужны, фильтруя данные по следующим полям:</span><span class="sxs-lookup"><span data-stu-id="62bd1-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="62bd1-110">**Диапазон времени** — задания можно фильтровать по диапазону даты и времени.</span><span class="sxs-lookup"><span data-stu-id="62bd1-110">**Time range** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="62bd1-111">**Устройства** — задания инициируются на конкретном устройстве, подключенном к службе.</span><span class="sxs-lookup"><span data-stu-id="62bd1-111">**Devices** – Jobs are initiated on a specific device connected to your service.</span></span> <span data-ttu-id="62bd1-112">Затем отфильтрованные задания будут представлены в табличной форме на основе следующих атрибутов.</span><span class="sxs-lookup"><span data-stu-id="62bd1-112">The filtered jobs are then tabulated based on the following attributes:</span></span>
  
  * <span data-ttu-id="62bd1-113">**Имя** — имя задания: **Все**, **Резервное копирование**, **Клонирование**, **Отработка отказа**, а также **Скачивание обновлений** или **Установка обновлений**.</span><span class="sxs-lookup"><span data-stu-id="62bd1-113">**Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="62bd1-114">**Состояние** — задания могут находиться в следующих состояниях: **Все**, **Выполняется**, **Успешно**, **Сбой** или **Отменено**.</span><span class="sxs-lookup"><span data-stu-id="62bd1-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="62bd1-115">**Сущность** — задания могут быть связаны с томом, общей папкой или устройством.</span><span class="sxs-lookup"><span data-stu-id="62bd1-115">**Entity** – The jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="62bd1-116">**Устройство** — имя устройства, на котором запущено задание.</span><span class="sxs-lookup"><span data-stu-id="62bd1-116">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="62bd1-117">**Время запуска** — время начала задания.</span><span class="sxs-lookup"><span data-stu-id="62bd1-117">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="62bd1-118">**Длительность** — период, в течение которого выполнялось задание.</span><span class="sxs-lookup"><span data-stu-id="62bd1-118">**Duration** – The duration for on which the job was run.</span></span>
* <span data-ttu-id="62bd1-119">**Состояние** — можно выполнять поиск по всем заданиям, запущенным и завершенным заданиям, а также заданиям, завершившихся сбоем.</span><span class="sxs-lookup"><span data-stu-id="62bd1-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="62bd1-120">**Тип задания** — тип задания: все, резервное копирование, восстановление, отработка отказа, а также загрузка или установка обновлений.</span><span class="sxs-lookup"><span data-stu-id="62bd1-120">**Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="62bd1-121">Список заданий обновляется каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="62bd1-121">The list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="62bd1-122">Просмотр сведений о задании</span><span class="sxs-lookup"><span data-stu-id="62bd1-122">View job details</span></span>
<span data-ttu-id="62bd1-123">Выполните следующие действия для просмотра сведений о любом задании.</span><span class="sxs-lookup"><span data-stu-id="62bd1-123">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="62bd1-124">Просмотр сведений о задании</span><span class="sxs-lookup"><span data-stu-id="62bd1-124">To view job details</span></span>
1. <span data-ttu-id="62bd1-125">В колонке **Задания** можно отобразить интересующие вас задания, выполнив запрос с соответствующими фильтрами.</span><span class="sxs-lookup"><span data-stu-id="62bd1-125">On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="62bd1-126">Можно выполнять поиск по завершенным или выполняющимся заданиям.</span><span class="sxs-lookup"><span data-stu-id="62bd1-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="62bd1-127">Выберите задание из табличного списка заданий.</span><span class="sxs-lookup"><span data-stu-id="62bd1-127">Select a job from the tabular list of jobs.</span></span>
   
    ![Колонка "Задание"](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="62bd1-129">В нижней части страницы нажмите кнопку **Сведения**.</span><span class="sxs-lookup"><span data-stu-id="62bd1-129">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="62bd1-130">В диалоговом окне **Сведения** можно просмотреть состояние, сведения и статистику по времени.</span><span class="sxs-lookup"><span data-stu-id="62bd1-130">In the **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="62bd1-131">Ниже отображено диалоговое окно **Сведения о задании резервного копирования** .</span><span class="sxs-lookup"><span data-stu-id="62bd1-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span></span>
   
    ![Сведения о задании](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a><span data-ttu-id="62bd1-133">Сбои заданий при приостановке виртуальной машины в гипервизоре</span><span class="sxs-lookup"><span data-stu-id="62bd1-133">Job failures when the virtual machine is paused in the hypervisor</span></span>
<span data-ttu-id="62bd1-134">Если задание выполняется в виртуальном массиве StorSimple и устройство (виртуальная машина, подготовленная в гипервизоре) приостанавливается более чем на 15 минут, задание завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="62bd1-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails.</span></span> <span data-ttu-id="62bd1-135">Это происходит из-за нарушения синхронизации времени виртуального массива StorSimple и Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="62bd1-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span></span> 

<span data-ttu-id="62bd1-136">Отобразится следующая ошибка: Your device time is out of sync with the Microsoft Azure time by more than 15 minutes (Время на устройстве и время Microsoft Azure отличаются более чем на 15 минут).</span><span class="sxs-lookup"><span data-stu-id="62bd1-136">You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="62bd1-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier (Убедитесь, что время гипервизора и устройства синхронизировано с сервером NTP).</span><span class="sxs-lookup"><span data-stu-id="62bd1-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="62bd1-138">Verify that there are no connectivity issues (Проверьте наличие проблем с подключением).</span><span class="sxs-lookup"><span data-stu-id="62bd1-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="62bd1-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device (Чтобы устранить проблемы с подключением, выполните диагностические тесты в локальном веб-интерфейсе виртуального устройства).</span><span class="sxs-lookup"><span data-stu-id="62bd1-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."</span></span>

<span data-ttu-id="62bd1-140">Эти ошибки свойственны заданиям резервного копирования, восстановления, обновления и отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="62bd1-140">These failures apply to backup, restore, update, and failover jobs.</span></span> <span data-ttu-id="62bd1-141">Если виртуальная машина подготовлена в Hyper-V, она в конечном итоге синхронизирует время с гипервизором.</span><span class="sxs-lookup"><span data-stu-id="62bd1-141">If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="62bd1-142">После этого можно перезапустить задание.</span><span class="sxs-lookup"><span data-stu-id="62bd1-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62bd1-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62bd1-143">Next steps</span></span>
<span data-ttu-id="62bd1-144">[Узнайте, как с помощью локального веб-интерфейса администрировать виртуальный массив StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="62bd1-144">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

