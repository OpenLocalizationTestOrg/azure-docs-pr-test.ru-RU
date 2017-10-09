---
title: "резервные копии развертывания диспетчера ресурсов виртуальной машины aaaManage | Документы Microsoft"
description: "Узнайте, как монитор и toomanage резервных копий развертывания диспетчера ресурсов виртуальной машины"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="27da9-103">Управление резервным копированием виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="27da9-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27da9-104">Управление архивацией виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="27da9-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="27da9-105">Управление архивацией классических виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="27da9-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="27da9-106">В этой статье представлены рекомендации по управлению резервных копий виртуальной Машины и объясняется hello оповещения резервного копирования данных на панели мониторинга портала hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="27da9-107">руководство Hello в данной статье применяется toousing виртуальных машин с хранилищами служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="27da9-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="27da9-108">Данная статья не охватывает hello Создание виртуальных машин, а также объясняются его как tooprotect виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="27da9-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="27da9-109">Базовые сведения о защите развертывания диспетчера ресурсов Azure виртуальные машины в Azure в хранилище служб восстановления, в разделе [первый взгляд: резервное копирование виртуальных машин tooa хранилище служб восстановления](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="27da9-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="27da9-110">Управление хранилищами и защищенными виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="27da9-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="27da9-111">В hello портал Azure панель мониторинга хранилища служб восстановления hello предоставляет доступ tooinformation о hello хранилища, включая:</span><span class="sxs-lookup"><span data-stu-id="27da9-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="27da9-112">Hello самой последней резервной копии моментальных снимков, который также является последней точки восстановления hello < br\></span><span class="sxs-lookup"><span data-stu-id="27da9-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="27da9-113">Здравствуйте, политику резервного копирования < br\></span><span class="sxs-lookup"><span data-stu-id="27da9-113">hello backup policy <br\></span></span>
* <span data-ttu-id="27da9-114">общий размер всех моментальных снимков резервной копии; <br\></span><span class="sxs-lookup"><span data-stu-id="27da9-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="27da9-115">число виртуальных машин, которые защищены с помощью хранилища hello < br\></span><span class="sxs-lookup"><span data-stu-id="27da9-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="27da9-116">Многие задачи управления с помощью резервной копии виртуальной машины начинаются с открытия хранилища hello в панель мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="27da9-117">Тем не менее поскольку хранилищ могут быть используется tooprotect нескольких элементов (или несколько виртуальных машин) tooview сведений о конкретной виртуальной Машины, откройте панель мониторинга элемента хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="27da9-118">Hello следующей процедуре показано, как tooopen hello *мониторинга хранилища* и продолжите toohello *панель мониторинга элемента хранилища*.</span><span class="sxs-lookup"><span data-stu-id="27da9-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="27da9-119">В обе процедуры, которые определяют как tooadd hello хранилище и хранилище toohello элемента Панель мониторинга Azure с помощью команды toodashboard ПИН-кода hello есть «рекомендации».</span><span class="sxs-lookup"><span data-stu-id="27da9-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="27da9-120">Toodashboard ПИН-код — это способ создания ярлыка toohello хранилища или элемента.</span><span class="sxs-lookup"><span data-stu-id="27da9-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="27da9-121">Стандартные команды также можно выполнить с помощью ярлыка hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="27da9-122">Если у вас есть несколько панелей мониторинга и открыть колонках, используйте ползунок шкалы темный синий hello внизу hello hello tooslide окно hello панель мониторинга Azure и обратно.</span><span class="sxs-lookup"><span data-stu-id="27da9-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![Полное представление с ползунком](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="27da9-124">Откройте хранилище служб восстановления hello информационной панели:</span><span class="sxs-lookup"><span data-stu-id="27da9-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="27da9-125">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="27da9-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="27da9-126">Hello концентратора меню **Обзор** и введите в список ресурсов hello, **службы восстановления**.</span><span class="sxs-lookup"><span data-stu-id="27da9-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="27da9-127">Началом ввода hello список фильтров на основе ввода.</span><span class="sxs-lookup"><span data-stu-id="27da9-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="27da9-128">Щелкните **Хранилище служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="27da9-128">Click **Recovery Services vault**.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="27da9-130">отображается список Hello хранилищами служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="27da9-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="27da9-131">Список хранилищ служб восстановления</span><span class="sxs-lookup"><span data-stu-id="27da9-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="27da9-132">Если закрепить хранилище toohello панель мониторинга Azure, хранилище сразу доступны при открытии hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="27da9-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="27da9-133">Щелкните правой кнопкой мыши хранилище hello toopin мониторинга toohello хранилища, в списке хранилище hello и выберите **toodashboard ПИН-кода**.</span><span class="sxs-lookup"><span data-stu-id="27da9-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="27da9-134">Hello выберите из списка хранилищ tooopen хранилище hello ее панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="27da9-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="27da9-135">При выборе хранилища hello, панель мониторинга хранилища hello и hello **параметры** откройте колонку.</span><span class="sxs-lookup"><span data-stu-id="27da9-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="27da9-136">В следующие изображения hello, hello **хранилище Contoso** панель мониторинга, выделяется.</span><span class="sxs-lookup"><span data-stu-id="27da9-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![Открытые панели мониторинга хранилища и колонки "Параметры"](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="27da9-138">Открытие панели мониторинга элемента хранилища</span><span class="sxs-lookup"><span data-stu-id="27da9-138">Open a vault item dashboard</span></span>
<span data-ttu-id="27da9-139">В предыдущей процедуре Привет открыть панель мониторинга хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="27da9-140">панель мониторинга элемента хранилища hello tooopen:</span><span class="sxs-lookup"><span data-stu-id="27da9-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="27da9-141">В панели мониторинга хранилища hello на hello **резервное копирование элементов** эскиза, щелкните **виртуальных машинах Azure**.</span><span class="sxs-lookup"><span data-stu-id="27da9-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Открытие элемента "Архивируемые элементы"](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="27da9-143">Hello **архивных элементов** колонке перечислены hello задания последнего резервного копирования для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="27da9-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="27da9-144">В этом примере приведена одна виртуальная машина (demovm-markgal), защищенная с помощью этого хранилища.</span><span class="sxs-lookup"><span data-stu-id="27da9-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Элемент "Архивируемые элементы"](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="27da9-146">Для упрощения доступа можно закрепить toohello элемента хранилища Azure панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="27da9-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="27da9-147">элемент хранилища в список элементов хранилища hello, hello элемент правой кнопкой мыши и выберите toopin **toodashboard ПИН-кода**.</span><span class="sxs-lookup"><span data-stu-id="27da9-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="27da9-148">В hello **резервное копирование элементов** колонка, щелкните панель мониторинга элемента хранилища hello, tooopen элемент hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![Элемент "Архивируемые элементы"](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="27da9-150">панель мониторинга элемента хранилища Hello и его **параметры** откройте колонку.</span><span class="sxs-lookup"><span data-stu-id="27da9-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![Панель мониторинга архивируемого элемента с колонкой "Параметры"](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="27da9-152">Hello хранилище элемента панели мониторинга можно выполнять многие задачи управления ключами, например:</span><span class="sxs-lookup"><span data-stu-id="27da9-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="27da9-153">изменять и создавать политики архивации; <br\></span><span class="sxs-lookup"><span data-stu-id="27da9-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="27da9-154">просматривать точки восстановления и их состояние согласованности; <br\></span><span class="sxs-lookup"><span data-stu-id="27da9-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="27da9-155">запускать архивацию виртуальной машины по запросу; <br\></span><span class="sxs-lookup"><span data-stu-id="27da9-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="27da9-156">отключать защиту виртуальных машин; <br\></span><span class="sxs-lookup"><span data-stu-id="27da9-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="27da9-157">возобновлять защиту виртуальных машин; <br\></span><span class="sxs-lookup"><span data-stu-id="27da9-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="27da9-158">удалять данные резервной копии (или точки восстановления); <br\></span><span class="sxs-lookup"><span data-stu-id="27da9-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="27da9-159">[восстанавливать архивные диски](backup-azure-arm-restore-vms.md#restore-backed-up-disks).  <br\></span><span class="sxs-lookup"><span data-stu-id="27da9-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="27da9-160">Для следующих процедур hello hello, начальная точка является hello панель мониторинга элемента хранилища.</span><span class="sxs-lookup"><span data-stu-id="27da9-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="27da9-161">Управление политиками резервного копирования</span><span class="sxs-lookup"><span data-stu-id="27da9-161">Manage backup policies</span></span>
1. <span data-ttu-id="27da9-162">На hello [панель мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard), нажмите кнопку **все параметры** tooopen hello **параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="27da9-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![Колонка "Политика архивации"](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="27da9-164">На hello **параметры** колонка, щелкните **политика архивации** tooopen этой колонке.</span><span class="sxs-lookup"><span data-stu-id="27da9-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="27da9-165">В колонке hello отображаются hello резервного копирования частоты и хранения сведения диапазона.</span><span class="sxs-lookup"><span data-stu-id="27da9-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![Колонка "Политика архивации"](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="27da9-167">Из hello **выберите политику резервного копирования** меню:</span><span class="sxs-lookup"><span data-stu-id="27da9-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="27da9-168">Выберите другой политике политики toochange и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="27da9-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="27da9-169">Новая политика Hello такое хранилище toohello сразу же применен.</span><span class="sxs-lookup"><span data-stu-id="27da9-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="27da9-170"><br\></span><span class="sxs-lookup"><span data-stu-id="27da9-170"><br\></span></span>
   * <span data-ttu-id="27da9-171">Выберите политику, toocreate **создать новый**.</span><span class="sxs-lookup"><span data-stu-id="27da9-171">toocreate a policy, select **Create New**.</span></span>

     ![Резервное копирование виртуальной машины](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="27da9-173">Указания по созданию политики архивации см. в разделе [Определение политики архивации](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="27da9-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="27da9-174">При управлении политиками резервного копирования, убедитесь, что hello toofollow [рекомендации](backup-azure-vms-introduction.md#best-practices) для достижения оптимальной производительности резервного копирования</span><span class="sxs-lookup"><span data-stu-id="27da9-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="27da9-175">Резервное копирование виртуальной машины по запросу</span><span class="sxs-lookup"><span data-stu-id="27da9-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="27da9-176">Резервное копирование виртуальной машины по запросу можно выполнять, когда для нее настроена защита.</span><span class="sxs-lookup"><span data-stu-id="27da9-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="27da9-177">Если ожидается hello начальной резервной копии, резервное копирование по требованию создает полную копию hello виртуальной машины в hello в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="27da9-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="27da9-178">Если выполнена hello начальной резервной копии, резервное копирование по требованию будет отправлять изменения из предыдущего снимка hello, toohello хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="27da9-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="27da9-179">Таким образом, все последующие резервные копии являются добавочными.</span><span class="sxs-lookup"><span data-stu-id="27da9-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="27da9-180">диапазон хранения Hello резервное копирование по требованию — hello значение срока хранения, указанное для hello точки ежедневного резервного копирования в политике hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="27da9-181">При выборе Нет точки ежедневного резервного копирования используется hello точки еженедельного резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="27da9-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="27da9-182">резервное копирование по требованию tootrigger виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="27da9-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="27da9-183">На hello [панель мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard), нажмите кнопку **Архивировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="27da9-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Кнопка "Создать резервную копию"](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="27da9-185">портал Hello упрощает действительно toostart задание резервного копирования по запросу.</span><span class="sxs-lookup"><span data-stu-id="27da9-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="27da9-186">Нажмите кнопку **Да** задание резервного копирования toostart hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-186">Click **Yes** toostart hello backup job.</span></span>

    ![Кнопка "Создать резервную копию"](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="27da9-188">задание резервного копирования Hello создает точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="27da9-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="27da9-189">Hello диапазона хранения точек восстановления hello hello совпадает с диапазоном хранения, указанным в политике hello, связанных с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="27da9-190">Ход выполнения hello tootrack для задания hello в панель мониторинга хранилища hello, щелкните hello **заданий резервного копирования** плитки.</span><span class="sxs-lookup"><span data-stu-id="27da9-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="27da9-191">Отключение защиты виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="27da9-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="27da9-192">При выборе toostop защиту виртуальной машины, будет предложено, следует ли точек восстановления tooretain hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="27da9-193">Существует два способа toostop защиту виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="27da9-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="27da9-194">остановить все будущие операции резервного копирования и удалить все точки восстановления;</span><span class="sxs-lookup"><span data-stu-id="27da9-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="27da9-195">Остановка всех последующих заданий резервного копирования, но оставьте hello точек восстановления</span><span class="sxs-lookup"><span data-stu-id="27da9-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="27da9-196">Нет затраты, связанные с выходом из hello точек восстановления в хранилище.</span><span class="sxs-lookup"><span data-stu-id="27da9-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="27da9-197">Однако hello преимущество покидая hello точки восстановления — hello виртуальной машины можно восстановить в более поздней версии, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="27da9-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="27da9-198">Сведения о стоимости hello оставить hello точек восстановления см. в разделе hello [сведения о ценах](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="27da9-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="27da9-199">При выборе toodelete все точки восстановления, нельзя восстановить hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27da9-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="27da9-200">toostop защиты для виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="27da9-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="27da9-201">На hello [панель мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard), нажмите кнопку **остановить архивацию**.</span><span class="sxs-lookup"><span data-stu-id="27da9-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Кнопка "Прекратить резервное копирование"](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="27da9-203">Открывает колонку Hello остановка резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="27da9-203">hello Stop Backup blade opens.</span></span>

    ![Колонка "Прекратить резервное копирование"](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="27da9-205">На hello **остановка резервного копирования** колонке выберите hello ли tooretain или удаления резервных копий данных.</span><span class="sxs-lookup"><span data-stu-id="27da9-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="27da9-206">Hello «сведения» содержит сведения о вашему выбору.</span><span class="sxs-lookup"><span data-stu-id="27da9-206">hello information box provides details about your choice.</span></span>

    ![остановка защиты;](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="27da9-208">Если вы выбрали tooretain hello резервных копий данных, пропустите toostep 4.</span><span class="sxs-lookup"><span data-stu-id="27da9-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="27da9-209">Если вы выбрали toodelete резервных копий данных, убедитесь, задания резервного копирования toostop hello и удалите точек восстановления hello - hello имя типа элемента hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![Остановить проверку](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="27da9-211">Если вы не уверены в правильности имени элемента hello, наведите указатель мыши tooview hello hello восклицательный знак имени.</span><span class="sxs-lookup"><span data-stu-id="27da9-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="27da9-212">Кроме того, испытывает hello имя элемента hello **остановка резервного копирования** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="27da9-213">При желании можно указать **причину** или добавить **комментарий**.</span><span class="sxs-lookup"><span data-stu-id="27da9-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="27da9-214">щелкните задание резервного копирования hello toostop для текущего элемента hello, ![резервного копирования "Остановить"](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="27da9-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="27da9-215">Сообщение уведомления позволяет узнать, что задания резервного копирования hello были остановлены.</span><span class="sxs-lookup"><span data-stu-id="27da9-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![Подтверждение остановки защиты](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="27da9-217">Возобновление защиты виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="27da9-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="27da9-218">Если hello **сохранить данные резервной копии** параметр был выбран при остановке защиты для виртуальной машины hello, то возможно tooresume защиты.</span><span class="sxs-lookup"><span data-stu-id="27da9-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="27da9-219">Если hello **удаление данных резервного копирования** был выбран параметр, то нельзя возобновить защиту для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="27da9-220">tooresume защиты для виртуальной машины hello</span><span class="sxs-lookup"><span data-stu-id="27da9-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="27da9-221">На hello [панель мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard), нажмите кнопку **возобновить резервное копирование**.</span><span class="sxs-lookup"><span data-stu-id="27da9-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Возобновить защиту](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="27da9-223">Открывает колонку Hello политику резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="27da9-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="27da9-224">При повторная защита виртуальной машины hello, можно выбрать различные политики, чем политика hello, с которой изначально было защиту виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27da9-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="27da9-225">Следуйте указаниям hello [Управление политиками резервного копирования](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello политики для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27da9-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="27da9-226">После резервного копирования политика hello не применен toohello виртуальной машины, можно увидеть следующие сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![Защищенные виртуальные машины](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="27da9-228">Удаление данных резервных копий</span><span class="sxs-lookup"><span data-stu-id="27da9-228">Delete Backup data</span></span>
<span data-ttu-id="27da9-229">Можно удалить hello резервного копирования данных, связанных с виртуальной машины во время hello **остановить архивацию** задания, либо в любое время после hello завершения задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="27da9-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="27da9-230">Она может быть полезным toowait дней или недель перед удалением hello точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="27da9-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="27da9-231">В отличие от точек восстановления, восстановление, при удалении резервной копии данных, нельзя выбрать отдельные точки toodelete.</span><span class="sxs-lookup"><span data-stu-id="27da9-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="27da9-232">Если выбрать toodelete данные резервной копии, необходимо удалить все точки восстановления, связанные с элементом hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="27da9-233">Hello ниже процедура предполагает hello задание архивации для виртуальной машины hello была остановлена или отключена.</span><span class="sxs-lookup"><span data-stu-id="27da9-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="27da9-234">После отключения задания резервного копирования hello hello **возобновить резервное копирование** и **резервного копирования Delete** параметры доступны в панель мониторинга элемента хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![Кнопки возобновления и удаления](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="27da9-236">toodelete резервного копирования данных на виртуальной машине с hello *резервное копирование отключено*:</span><span class="sxs-lookup"><span data-stu-id="27da9-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="27da9-237">На hello [панель мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard), нажмите кнопку **резервного копирования Delete**.</span><span class="sxs-lookup"><span data-stu-id="27da9-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Тип виртуальной машины](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="27da9-239">Hello **удаление данных резервного копирования** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="27da9-239">hello **Delete Backup Data** blade opens.</span></span>

    ![Тип виртуальной машины](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="27da9-241">Имя типа hello hello элемента tooconfirm нужно точек восстановления toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![Остановить проверку](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="27da9-243">Если вы не уверены в правильности имени элемента hello, наведите указатель мыши tooview hello hello восклицательный знак имени.</span><span class="sxs-lookup"><span data-stu-id="27da9-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="27da9-244">Кроме того, испытывает hello имя элемента hello **удаление данных резервного копирования** hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="27da9-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="27da9-245">При желании можно указать **причину** или добавить **комментарий**.</span><span class="sxs-lookup"><span data-stu-id="27da9-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="27da9-246">toodelete hello резервного копирования данных для текущего элемента hello, нажмите кнопку ![резервного копирования "Остановить"](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="27da9-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="27da9-247">Сообщение уведомления позволяет узнать, что hello резервных копий данных был удален.</span><span class="sxs-lookup"><span data-stu-id="27da9-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27da9-248">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27da9-248">Next steps</span></span>
<span data-ttu-id="27da9-249">Сведения о восстановлении виртуальных машин из точки восстановления см. в статье [Восстановление виртуальных машин в Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="27da9-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="27da9-250">Если вам нужна информация о защите виртуальных машин, см. раздел [первый взгляд: резервное копирование виртуальных машин tooa хранилище служб восстановления](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="27da9-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="27da9-251">Дополнительные сведения о мониторинге событий см. в статье [Мониторинг предупреждений в резервных копиях виртуальных машин Azure](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="27da9-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
