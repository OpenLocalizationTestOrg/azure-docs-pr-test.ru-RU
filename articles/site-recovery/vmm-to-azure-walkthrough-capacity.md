---
title: "Планирование ресурсов и масштабирование для репликации виртуальной машины Hyper-V (с VMM) в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "Используйте эту статью, чтобы запланировать ресурсы и масштабирование при репликации виртуальных машин Hyper-V в облаках VMM в Azure с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: ab1dc21a829140f8cd2e57837d83a05b0d71bcdf
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-to-azure-replication"></a><span data-ttu-id="dff95-103">Шаг 3. Планирование ресурсов и масштабирования для репликации из Hyper-V (с VMM) в Azure</span><span class="sxs-lookup"><span data-stu-id="dff95-103">Step 3: Plan capacity and scaling for Hyper-V (with VMM) to Azure replication</span></span>

<span data-ttu-id="dff95-104">Ознакомившись с [необходимыми условиями для развертывания](vmm-to-azure-walkthrough-prerequisites.md), прочтите эту статью, чтобы запланировать ресурсы и масштабирование при репликации локальных виртуальных машин Hyper-V в облаках VMM в Azure с помощью [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dff95-104">After you've reviewed the [deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md), use this article to figure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds to Azure, with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="dff95-105">Комментарии или вопросы технического характера можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="dff95-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="dff95-106">С чего начать планирование загрузки?</span><span class="sxs-lookup"><span data-stu-id="dff95-106">How do I start capacity planning?</span></span>


<span data-ttu-id="dff95-107">Необходимо собрать сведения о среде репликации, а затем запланировать ресурсы, используя эти данные и учитывая рекомендации, приведенные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="dff95-107">You gather information about your replication environment, and then plan capacity using the data, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="dff95-108">Сбор сведений</span><span class="sxs-lookup"><span data-stu-id="dff95-108">Gather information</span></span>

1. <span data-ttu-id="dff95-109">Соберите сведения о среде репликации, включая информацию о виртуальных машинах, количестве дисков на виртуальную машину и объеме хранилища на диск.</span><span class="sxs-lookup"><span data-stu-id="dff95-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="dff95-110">Определите частоту ежедневных изменений (обновлений) реплицированных данных.</span><span class="sxs-lookup"><span data-stu-id="dff95-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="dff95-111">Скачайте [инструмент планирования ресурсов Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057), чтобы получить сведения о частоте изменений.</span><span class="sxs-lookup"><span data-stu-id="dff95-111">Download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="dff95-112">Мы советует использовать это средство в течение недели, чтобы получить средние значения.</span><span class="sxs-lookup"><span data-stu-id="dff95-112">We recommend you run this tool over a week to capture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="dff95-113">Планирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="dff95-113">Figure out capacity</span></span>

<span data-ttu-id="dff95-114">На основе полученной информации используйте [планировщик ресурсов Site Recovery](http://aka.ms/asr-capacity-planner-excel), чтобы проанализировать исходную среду и рабочие нагрузки и оценить требования к пропускной способности, а также определить объем ресурсов сервера для исходного расположения и ресурсы (виртуальные машины, хранилища и т. д.), требуемые для целевого расположения.</span><span class="sxs-lookup"><span data-stu-id="dff95-114">Based on the information you've gather, you run the [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) to analyze your source environment and workloads, estimate bandwidth needs and server resources for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span> <span data-ttu-id="dff95-115">Его можно использовать в нескольких режимах:</span><span class="sxs-lookup"><span data-stu-id="dff95-115">You can run the tool in a couple of modes:</span></span>

- <span data-ttu-id="dff95-116">Быстрое планирование. Запустите инструмент в этом режиме, чтобы получить проекции сети и сервера на основе среднего числа виртуальных машин, дисков, объема хранилища и частоты изменений.</span><span class="sxs-lookup"><span data-stu-id="dff95-116">Quick planning: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="dff95-117">Детальное планирование. Запустите инструмент в этом режиме, чтобы задать сведения о каждой рабочей нагрузке на уровне виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dff95-117">Detailed planning: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="dff95-118">Проанализируйте совместимость виртуальной машины и получите проекции сети и сервера.</span><span class="sxs-lookup"><span data-stu-id="dff95-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="dff95-119">Теперь запустите инструмент.</span><span class="sxs-lookup"><span data-stu-id="dff95-119">Now run the tool:</span></span>

1. <span data-ttu-id="dff95-120">Скачайте [инструмент](http://aka.ms/asr-capacity-planner-excel).</span><span class="sxs-lookup"><span data-stu-id="dff95-120">Download the [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="dff95-121">Чтобы запустить инструмент быстрого планирования, выполните [эти инструкции](site-recovery-capacity-planner.md#run-the-quick-planner) и выберите сценарий **Hyper-V в Azure**.</span><span class="sxs-lookup"><span data-stu-id="dff95-121">To run the quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select the scenario **Hyper-V to Azure**.</span></span>
3. <span data-ttu-id="dff95-122">Чтобы запустить инструмент детального планирования, выполните [эти инструкции](site-recovery-capacity-planner.md#run-the-detailed-planner) и выберите сценарий **Hyper-V в Azure**.</span><span class="sxs-lookup"><span data-stu-id="dff95-122">To run the detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select the scenario **Hyper-V to Azure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="dff95-123">Управление пропускной способностью сети</span><span class="sxs-lookup"><span data-stu-id="dff95-123">Control network bandwidth</span></span>

<span data-ttu-id="dff95-124">После вычисления необходимой пропускной способности у вас есть несколько вариантов управления объемом пропускной способности, используемой для репликации:</span><span class="sxs-lookup"><span data-stu-id="dff95-124">After you've calculated the bandwidth you need, you have a couple of options for controlling the amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="dff95-125">**Регулирование пропускной способности.** Трафик Hyper-V, который реплицируется в Azure, проходит через определенный узел Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="dff95-125">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="dff95-126">Пропускную способность можно регулировать на сервере этого узла.</span><span class="sxs-lookup"><span data-stu-id="dff95-126">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="dff95-127">**Изменение пропускной способности.** Пропускную способность, используемую для репликации, можно изменить с помощью нескольких ключей реестра.</span><span class="sxs-lookup"><span data-stu-id="dff95-127">**Influence bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="dff95-128">Регулирование пропускной способности</span><span class="sxs-lookup"><span data-stu-id="dff95-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="dff95-129">Откройте на сервере узла Hyper-V оснастку MMC в службе архивации Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dff95-129">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="dff95-130">По умолчанию ярлык для службы архивации Microsoft Azure доступен на рабочем столе или в папке C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="dff95-130">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="dff95-131">В оснастке щелкните **Изменить свойства**.</span><span class="sxs-lookup"><span data-stu-id="dff95-131">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="dff95-132">На вкладке **Регулирование** установите флажок **Разрешить регулирование пропускной способности интернет-канала для операций архивации** и задайте ограничения для рабочего и нерабочего времени.</span><span class="sxs-lookup"><span data-stu-id="dff95-132">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="dff95-133">Допустимы значения в диапазоне от 512 Кбит/с до 102 Мбит/с.</span><span class="sxs-lookup"><span data-stu-id="dff95-133">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![Регулирование пропускной способности](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

<span data-ttu-id="dff95-135">Чтобы настроить регулирование, можно также использовать командлет [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) .</span><span class="sxs-lookup"><span data-stu-id="dff95-135">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="dff95-136">Рассмотрим пример:</span><span class="sxs-lookup"><span data-stu-id="dff95-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="dff95-137">**Set-OBMachineSetting -NoThrottle** указывает, что регулирование не требуется.</span><span class="sxs-lookup"><span data-stu-id="dff95-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="dff95-138">Изменение пропускной способности сети</span><span class="sxs-lookup"><span data-stu-id="dff95-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="dff95-139">В реестре перейдите в раздел **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="dff95-139">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="dff95-140">Чтобы изменить скорость передачи данных при репликации диска, задайте новое значение для раздела **UploadThreadsPerVM**или создайте его, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="dff95-140">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="dff95-141">Чтобы изменить скорость передачи данных при восстановлении размещения из Azure, задайте новое значение для раздела **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="dff95-141">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="dff95-142">Значение по умолчанию — 4.</span><span class="sxs-lookup"><span data-stu-id="dff95-142">The default value is 4.</span></span> <span data-ttu-id="dff95-143">В сети со значительным избыточным резервом для этих разделов реестра необходимо изменить значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dff95-143">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="dff95-144">Максимальное значение — 32.</span><span class="sxs-lookup"><span data-stu-id="dff95-144">The maximum is 32.</span></span> <span data-ttu-id="dff95-145">Следите за трафиком для оптимизации значения.</span><span class="sxs-lookup"><span data-stu-id="dff95-145">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dff95-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dff95-146">Next steps</span></span>

<span data-ttu-id="dff95-147">Перейдите к статье [Шаг 4. Планирование сетей для репликации физического сервера в Azure](vmm-to-azure-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="dff95-147">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md).</span></span>
