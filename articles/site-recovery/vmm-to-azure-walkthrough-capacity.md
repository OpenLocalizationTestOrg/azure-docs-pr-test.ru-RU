---
title: "aaaPlan емкости и масштабирования для tooAzure репликации (с помощью VMM) виртуальных Машин Hyper-V с помощью Azure Site Recovery | Документы Microsoft"
description: "Использовать статьи tooplan емкости и масштабирования при репликации виртуальных машин Hyper-V в VMM облаков tooAzure с Azure Site Recovery"
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
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a><span data-ttu-id="b61e2-103">Шаг 3: Планирование емкости и масштабирования для tooAzure репликации Hyper-V (с помощью VMM)</span><span class="sxs-lookup"><span data-stu-id="b61e2-103">Step 3: Plan capacity and scaling for Hyper-V (with VMM) tooAzure replication</span></span>

<span data-ttu-id="b61e2-104">После знакомства hello [необходимые условия для развертывания](vmm-to-azure-walkthrough-prerequisites.md), использовать этот toofigure статьи о планировании емкости и масштабирования, при репликации локальных виртуальных машин Hyper-V в tooAzure облаках диспетчера виртуальных машин System Center (VMM), с [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b61e2-104">After you've reviewed hello [deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md), use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="b61e2-105">После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b61e2-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="b61e2-106">С чего начать планирование загрузки?</span><span class="sxs-lookup"><span data-stu-id="b61e2-106">How do I start capacity planning?</span></span>


<span data-ttu-id="b61e2-107">Можно собирать сведения о вашей среды репликации, а затем емкость плана с использованием данных hello, а также вопросы hello выделено в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b61e2-107">You gather information about your replication environment, and then plan capacity using hello data, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="b61e2-108">Сбор сведений</span><span class="sxs-lookup"><span data-stu-id="b61e2-108">Gather information</span></span>

1. <span data-ttu-id="b61e2-109">Соберите сведения о среде репликации, включая информацию о виртуальных машинах, количестве дисков на виртуальную машину и объеме хранилища на диск.</span><span class="sxs-lookup"><span data-stu-id="b61e2-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="b61e2-110">Определите частоту ежедневных изменений (обновлений) реплицированных данных.</span><span class="sxs-lookup"><span data-stu-id="b61e2-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="b61e2-111">Загрузите hello [средства планирования емкости Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) скорость изменения tooget hello.</span><span class="sxs-lookup"><span data-stu-id="b61e2-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="b61e2-112">Мы рекомендуем установить это средство по toocapture недели средние значения.</span><span class="sxs-lookup"><span data-stu-id="b61e2-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="b61e2-113">Планирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="b61e2-113">Figure out capacity</span></span>

<span data-ttu-id="b61e2-114">На основании hello информации после сбора сведений запустите hello [планировщика емкости восстановления сайта](http://aka.ms/asr-capacity-planner-excel) tooanalyze исходной среде и рабочих нагрузок, Оценка требований к пропускной способности и ресурсов сервера для расположения источника hello и hello ресурсы (виртуальные машины и хранилища и т. д), необходимые в целевом расположении hello.</span><span class="sxs-lookup"><span data-stu-id="b61e2-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="b61e2-115">Можно запустить средство hello в нескольких режимах.</span><span class="sxs-lookup"><span data-stu-id="b61e2-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="b61e2-116">Быстрый планирования: запустите средство hello в этом режиме tooget сети и серверов проекции, основанные на среднее количество виртуальных машин, диски, хранилища и скорость изменения.</span><span class="sxs-lookup"><span data-stu-id="b61e2-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="b61e2-117">Подробные планирования: запустите средство hello в этом режиме и укажите сведения о каждой рабочей нагрузки на уровне виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b61e2-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="b61e2-118">Проанализируйте совместимость виртуальной машины и получите проекции сети и сервера.</span><span class="sxs-lookup"><span data-stu-id="b61e2-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="b61e2-119">Теперь запустите средство hello.</span><span class="sxs-lookup"><span data-stu-id="b61e2-119">Now run hello tool:</span></span>

1. <span data-ttu-id="b61e2-120">Загрузите hello [средства](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="b61e2-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="b61e2-121">Быстрый планировщик toorun hello, выполните [эти инструкции](site-recovery-capacity-planner.md#run-the-quick-planner)и выберите hello сценарий **tooAzure Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="b61e2-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="b61e2-122">toorun Здравствуйте подробные планировщик, выполните [эти инструкции](site-recovery-capacity-planner.md#run-the-detailed-planner)и выберите hello сценарий **tooAzure Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="b61e2-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="b61e2-123">Управление пропускной способностью сети</span><span class="sxs-lookup"><span data-stu-id="b61e2-123">Control network bandwidth</span></span>

<span data-ttu-id="b61e2-124">После вычисляемых hello пропускной способности, необходимые, у вас есть два способа управления hello объем пропускной способности, используемой для репликации:</span><span class="sxs-lookup"><span data-stu-id="b61e2-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="b61e2-125">**Регулирование полосы пропускания**: Hyper-V реплицирует tooAzure трафик проходит через конкретного узла Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b61e2-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="b61e2-126">Можно отрегулировать пропускной способности на сервере узла hello.</span><span class="sxs-lookup"><span data-stu-id="b61e2-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="b61e2-127">**Повлиять на пропускную способность**: вы можете влиять hello пропускной способности, используемой для репликации несколько разделов реестра.</span><span class="sxs-lookup"><span data-stu-id="b61e2-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="b61e2-128">Регулирование пропускной способности</span><span class="sxs-lookup"><span data-stu-id="b61e2-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="b61e2-129">Откройте hello Microsoft Azure Backup MMC оснастку на сервере узла Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="b61e2-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="b61e2-130">По умолчанию для быстрого архивации Microsoft Azure доступна на рабочем столе hello, или в C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="b61e2-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="b61e2-131">В оснастке hello щелкните **изменить свойства**.</span><span class="sxs-lookup"><span data-stu-id="b61e2-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="b61e2-132">На hello **регулирование** выберите **включить регулирования для операций резервного копирования использование пропускной способности Интернета**и ограничить hello для рабочих и нерабочих часов.</span><span class="sxs-lookup"><span data-stu-id="b61e2-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="b61e2-133">Допустимые диапазоны: от 512 Кбит/с too102 Мбит/с в секунду.</span><span class="sxs-lookup"><span data-stu-id="b61e2-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![Регулирование пропускной способности](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

<span data-ttu-id="b61e2-135">Можно также использовать hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) регулирования tooset командлета.</span><span class="sxs-lookup"><span data-stu-id="b61e2-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="b61e2-136">Рассмотрим пример:</span><span class="sxs-lookup"><span data-stu-id="b61e2-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="b61e2-137">**Set-OBMachineSetting -NoThrottle** указывает, что регулирование не требуется.</span><span class="sxs-lookup"><span data-stu-id="b61e2-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="b61e2-138">Изменение пропускной способности сети</span><span class="sxs-lookup"><span data-stu-id="b61e2-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="b61e2-139">В реестре hello перейдите слишком**Backup\Replication Azure параметру**.</span><span class="sxs-lookup"><span data-stu-id="b61e2-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="b61e2-140">tooinfluence hello пропускную способность трафика репликации диска изменить значение hello hello **UploadThreadsPerVM**, или создать ключ hello в том случае, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="b61e2-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="b61e2-141">пропускная способность hello tooinfluence для восстановления размещения трафик из Azure, измените значение hello **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="b61e2-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="b61e2-142">значение по умолчанию Hello — 4.</span><span class="sxs-lookup"><span data-stu-id="b61e2-142">hello default value is 4.</span></span> <span data-ttu-id="b61e2-143">В сети «избыточная Подготовка» следует изменить эти разделы реестра из значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="b61e2-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="b61e2-144">Hello максимальное — 32.</span><span class="sxs-lookup"><span data-stu-id="b61e2-144">hello maximum is 32.</span></span> <span data-ttu-id="b61e2-145">Мониторинг трафика toooptimize hello значение.</span><span class="sxs-lookup"><span data-stu-id="b61e2-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b61e2-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b61e2-146">Next steps</span></span>

<span data-ttu-id="b61e2-147">Go слишком[шаг 4: Планирование сети](vmm-to-azure-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="b61e2-147">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md).</span></span>
