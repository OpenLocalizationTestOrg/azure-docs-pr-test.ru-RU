---
title: "Управление архивацией виртуальных машин, развернутых с помощью Resource Manager | Документация Майкрософт"
description: "Узнайте, как управлять резервными копиями виртуальных машин, развернутых с помощью Resource Manager, и осуществлять их мониторинг"
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
ms.openlocfilehash: 35a21cb99ca4bad124a9f764cef9da453e1fe47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="c312b-103">Управление резервным копированием виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="c312b-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c312b-104">Управление архивацией виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="c312b-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="c312b-105">Управление архивацией классических виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c312b-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="c312b-106">Эта статья содержит рекомендации по управлению резервным копированием виртуальных машин. Также здесь рассматриваются оповещения, связанные с резервным копированием данных, которые доступны на панели мониторинга портала.</span><span class="sxs-lookup"><span data-stu-id="c312b-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span></span> <span data-ttu-id="c312b-107">Приведенные здесь рекомендации применимы только к виртуальным машинам, для которых используются хранилища служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c312b-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span></span> <span data-ttu-id="c312b-108">В этой статье не рассматриваются вопросы создания и защиты виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c312b-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span></span> <span data-ttu-id="c312b-109">Сведения о защите виртуальных машин в Azure, развернутых с помощью Azure Resource Manager, с использованием хранилища служб восстановления см. в статье [Первое знакомство. Защита виртуальных машин Azure в хранилище служб восстановления](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c312b-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="c312b-110">Управление хранилищами и защищенными виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="c312b-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="c312b-111">На панели мониторинга хранилища служб восстановления на портале Azure предоставляются следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="c312b-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span></span>

* <span data-ttu-id="c312b-112">сведения о последнем моментальном снимке резервной копии, который также является последней точкой восстановления; <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-112">the most recent backup snapshot, which is also the latest restore point <br\></span></span>
* <span data-ttu-id="c312b-113">политика архивации; <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-113">the backup policy <br\></span></span>
* <span data-ttu-id="c312b-114">общий размер всех моментальных снимков резервной копии; <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="c312b-115">количество виртуальных машин, защищенных с помощью хранилища. <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-115">number of virtual machines that are protected with the vault <br\></span></span>

<span data-ttu-id="c312b-116">Чтобы управлять резервным копированием виртуальной машины, в большинстве случаев нужно открыть хранилище на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c312b-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span></span> <span data-ttu-id="c312b-117">Так как хранилища можно использовать для защиты нескольких элементов (или нескольких виртуальных машин), для просмотра сведений о конкретной виртуальной машине следует открыть панель мониторинга для этого элемента хранилища.</span><span class="sxs-lookup"><span data-stu-id="c312b-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span></span> <span data-ttu-id="c312b-118">Ниже приведены сведения о том, как открыть *панель мониторинга хранилища* и перейти к *панели мониторинга элемента хранилища*,</span><span class="sxs-lookup"><span data-stu-id="c312b-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span></span> <span data-ttu-id="c312b-119">а также советы по добавлению хранилища и элемента хранилища на панель мониторинга Azure с помощью команды "Закрепить на панели мониторинга".</span><span class="sxs-lookup"><span data-stu-id="c312b-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span></span> <span data-ttu-id="c312b-120">В результате выполнения этой команды создается ярлык для хранилища или элемента.</span><span class="sxs-lookup"><span data-stu-id="c312b-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span></span> <span data-ttu-id="c312b-121">Затем ярлык можно использовать для выполнения общих команд.</span><span class="sxs-lookup"><span data-stu-id="c312b-121">You can also execute common commands from the shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="c312b-122">Если открыто несколько панелей мониторинга или колонок, для переключения панелей мониторинга Azure можно использовать темно-синий ползунок в нижней части окна.</span><span class="sxs-lookup"><span data-stu-id="c312b-122">If you have multiple dashboards and blades open, use the dark-blue slider at the bottom of the window to slide the Azure dashboard back and forth.</span></span>
>
>

![Полное представление с ползунком](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-the-dashboard"></a><span data-ttu-id="c312b-124">Открытие хранилища службы восстановления на панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="c312b-124">Open a Recovery Services vault in the dashboard:</span></span>
1. <span data-ttu-id="c312b-125">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c312b-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c312b-126">В главном меню щелкните **Обзор**, а затем в списке ресурсов введите **Службы восстановления**.</span><span class="sxs-lookup"><span data-stu-id="c312b-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="c312b-127">Как только вы начнете вводить символы, список отфильтруется соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="c312b-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="c312b-128">Щелкните **Хранилище служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="c312b-128">Click **Recovery Services vault**.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="c312b-130">После этого отобразится список хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c312b-130">The list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="c312b-131">Список хранилищ служб восстановления</span><span class="sxs-lookup"><span data-stu-id="c312b-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="c312b-132">Если закрепить хранилище на панели мониторинга Azure, доступ к нему можно получить непосредственно при открытии портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c312b-132">If you pin a vault to the Azure Dashboard, that vault is immediately accessible when you open the Azure portal.</span></span> <span data-ttu-id="c312b-133">Чтобы закрепить хранилище на панели мониторинга, в списке хранилищ щелкните правой кнопкой мыши необходимое хранилище и выберите команду **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="c312b-133">To pin a vault to the dashboard, in the vault list, right-click the vault, and select **Pin to dashboard**.</span></span>
   >
   >
3. <span data-ttu-id="c312b-134">В списке выберите хранилище, чтобы открыть соответствующую панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c312b-134">From the list of vaults, select the vault to open its dashboard.</span></span> <span data-ttu-id="c312b-135">Когда вы выберете хранилище, для него откроется панель мониторинга и колонка **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="c312b-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span></span> <span data-ttu-id="c312b-136">На следующем рисунке панель мониторинга хранилища **Contoso-vault** выделена красным цветом.</span><span class="sxs-lookup"><span data-stu-id="c312b-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span></span>

    ![Открытые панели мониторинга хранилища и колонки "Параметры"](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="c312b-138">Открытие панели мониторинга элемента хранилища</span><span class="sxs-lookup"><span data-stu-id="c312b-138">Open a vault item dashboard</span></span>
<span data-ttu-id="c312b-139">При выполнении предыдущей процедуры вы открыли панель мониторинга хранилища.</span><span class="sxs-lookup"><span data-stu-id="c312b-139">In the previous procedure you opened the vault dashboard.</span></span> <span data-ttu-id="c312b-140">Чтобы открыть панель мониторинга элемента хранилища, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c312b-140">To open the vault item dashboard:</span></span>

1. <span data-ttu-id="c312b-141">На панели мониторинга хранилища на плитке **Архивные элементы** щелкните **Виртуальные машины Azure**.</span><span class="sxs-lookup"><span data-stu-id="c312b-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Открытие элемента "Архивируемые элементы"](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="c312b-143">В колонке **Архивируемые элементы** отображаются последние выполненные задания резервного копирования для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="c312b-143">The **Backup Items** blade lists the last backup job for each item.</span></span> <span data-ttu-id="c312b-144">В этом примере приведена одна виртуальная машина (demovm-markgal), защищенная с помощью этого хранилища.</span><span class="sxs-lookup"><span data-stu-id="c312b-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Элемент "Архивируемые элементы"](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="c312b-146">Для более удобного доступа элемент хранилища можно закрепить на панели мониторинга Azure.</span><span class="sxs-lookup"><span data-stu-id="c312b-146">For ease of access, you can pin a vault item to the Azure Dashboard.</span></span> <span data-ttu-id="c312b-147">Для этого в списке элементов хранилища щелкните правой кнопкой мыши необходимый элемент и выберите команду **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="c312b-147">To pin a vault item, in the vault item list, right-click the item and select **Pin to dashboard**.</span></span>
   >
   >
2. <span data-ttu-id="c312b-148">В колонке **Архивируемые элементы** щелкните элемент, для которого необходимо открыть панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c312b-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span></span>

    ![Элемент "Архивируемые элементы"](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="c312b-150">Откроется панель мониторинга для элемента хранилища и соответствующая колонка **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="c312b-150">The vault item dashboard and its **Settings** blade open.</span></span>

    ![Панель мониторинга архивируемого элемента с колонкой "Параметры"](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="c312b-152">На панели мониторинга элемента хранилища можно выполнять следующие основные задачи по управлению:</span><span class="sxs-lookup"><span data-stu-id="c312b-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="c312b-153">изменять и создавать политики архивации; <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="c312b-154">просматривать точки восстановления и их состояние согласованности; <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="c312b-155">запускать архивацию виртуальной машины по запросу; <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="c312b-156">отключать защиту виртуальных машин; <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="c312b-157">возобновлять защиту виртуальных машин; <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="c312b-158">удалять данные резервной копии (или точки восстановления); <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="c312b-159">[восстанавливать архивные диски](backup-azure-arm-restore-vms.md#restore-backed-up-disks).  <br\></span><span class="sxs-lookup"><span data-stu-id="c312b-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="c312b-160">Приведенные ниже процедуры выполняются на панели мониторинга элемента хранилища.</span><span class="sxs-lookup"><span data-stu-id="c312b-160">For the following procedures, the starting point is the vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="c312b-161">Управление политиками резервного копирования</span><span class="sxs-lookup"><span data-stu-id="c312b-161">Manage backup policies</span></span>
1. <span data-ttu-id="c312b-162">На [панели мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard) щелкните **Все параметры**, чтобы открыть колонку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="c312b-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span></span>

    ![Колонка "Политика архивации"](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="c312b-164">В колонке **Параметры** щелкните **Политика архивации**, чтобы открыть соответствующую колонку.</span><span class="sxs-lookup"><span data-stu-id="c312b-164">On the **Settings** blade, click **Backup policy** to open that blade.</span></span>

    <span data-ttu-id="c312b-165">В ней отображаются сведения о частоте резервного копирования и диапазоне хранения.</span><span class="sxs-lookup"><span data-stu-id="c312b-165">On the blade, the backup frequency and retention range details are shown.</span></span>

    ![Колонка "Политика архивации"](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="c312b-167">Используйте меню **Выбор политики архивации** , чтобы выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c312b-167">From the **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="c312b-168">Чтобы изменить политику, выберите необходимую политику и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c312b-168">To change policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="c312b-169">Новая политика будет немедленно применена к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="c312b-169">The new policy is immediately applied to the vault.</span></span> <span data-ttu-id="c312b-170"><br\></span><span class="sxs-lookup"><span data-stu-id="c312b-170"><br\></span></span>
   * <span data-ttu-id="c312b-171">Чтобы создать политику, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c312b-171">To create a policy, select **Create New**.</span></span>

     ![Резервное копирование виртуальной машины](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="c312b-173">Указания по созданию политики архивации см. в разделе [Определение политики архивации](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="c312b-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="c312b-174">При управлении политиками резервного копирования обязательно следуйте [рекомендациям](backup-azure-vms-introduction.md#best-practices) для достижения оптимальной производительности резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c312b-174">While managing backup policies, make sure to follow the [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="c312b-175">Резервное копирование виртуальной машины по запросу</span><span class="sxs-lookup"><span data-stu-id="c312b-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="c312b-176">Резервное копирование виртуальной машины по запросу можно выполнять, когда для нее настроена защита.</span><span class="sxs-lookup"><span data-stu-id="c312b-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="c312b-177">Если начальное резервное копирование находится в состоянии ожидания, процесс резервного копирования по запросу создает полную копию виртуальной машины в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c312b-177">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span></span> <span data-ttu-id="c312b-178">Если начальное резервное копирование уже завершено, процесс резервного копирования по запросу отправит в хранилище служб восстановления только те изменения, которые произошли со времени создания предыдущего моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="c312b-178">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span></span> <span data-ttu-id="c312b-179">Таким образом, все последующие резервные копии являются добавочными.</span><span class="sxs-lookup"><span data-stu-id="c312b-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="c312b-180">Для диапазона хранения резервных копий по запросу используется значение ежедневного сохранения, указанное в политике.</span><span class="sxs-lookup"><span data-stu-id="c312b-180">The retention range for an on-demand backup is the retention value specified for the Daily backup point in the policy.</span></span> <span data-ttu-id="c312b-181">Если значение ежедневного сохранения не выбрано, используется значение еженедельного сохранения.</span><span class="sxs-lookup"><span data-stu-id="c312b-181">If no Daily backup point is selected, then the weekly backup point is used.</span></span>
>
>

<span data-ttu-id="c312b-182">Чтобы выполнить резервное копирование виртуальной машины по запросу, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c312b-182">To trigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="c312b-183">На [панели мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard)щелкните **Создать резервную копию**.</span><span class="sxs-lookup"><span data-stu-id="c312b-183">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Кнопка "Создать резервную копию"](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="c312b-185">После этого откроется окно с запросом на подтверждение выполнения этой операции.</span><span class="sxs-lookup"><span data-stu-id="c312b-185">The portal makes sure that you want to start an on-demand backup job.</span></span> <span data-ttu-id="c312b-186">Чтобы запустить задание резервного копирования, нажмите кнопку **Да** .</span><span class="sxs-lookup"><span data-stu-id="c312b-186">Click **Yes** to start the backup job.</span></span>

    ![Кнопка "Создать резервную копию"](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="c312b-188">Задание резервного копирования создает точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="c312b-188">The backup job creates a recovery point.</span></span> <span data-ttu-id="c312b-189">Период хранения созданной точки восстановления указан в политике, связанной с этой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="c312b-189">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span></span> <span data-ttu-id="c312b-190">Чтобы отслеживать выполнение задания, на панели мониторинга хранилища щелкните плитку **Задания архивации** .</span><span class="sxs-lookup"><span data-stu-id="c312b-190">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="c312b-191">Отключение защиты виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c312b-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="c312b-192">При остановке защиты виртуальной машины появится запрос на сохранение точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="c312b-192">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="c312b-193">Есть два способа остановить защиту виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="c312b-193">There are two ways to stop protecting virtual machines:</span></span>

* <span data-ttu-id="c312b-194">остановить все будущие операции резервного копирования и удалить все точки восстановления;</span><span class="sxs-lookup"><span data-stu-id="c312b-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="c312b-195">остановить все будущие операции резервного копирования, но сохранить точки восстановления </span><span class="sxs-lookup"><span data-stu-id="c312b-195">stop all future backup jobs but leave the recovery points</span></span> <br/>

<span data-ttu-id="c312b-196">Сохранение точек восстановления в хранилище сопровождается определенными затратами.</span><span class="sxs-lookup"><span data-stu-id="c312b-196">There is a cost associated with leaving the recovery points in storage.</span></span> <span data-ttu-id="c312b-197">Однако позже с помощью этих точек при необходимости можно восстановить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c312b-197">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span></span> <span data-ttu-id="c312b-198">Дополнительные сведения о тарифах на хранение точек восстановления см. в [описании цен](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="c312b-198">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="c312b-199">Если вы удалите все точки восстановления, вы не сможете восстановить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c312b-199">If you choose to delete all recovery points, you cannot restore the virtual machine.</span></span>

<span data-ttu-id="c312b-200">Чтобы остановить защиту виртуальной машины, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c312b-200">To stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="c312b-201">На [панели мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard)щелкните **Остановить резервное копирование**.</span><span class="sxs-lookup"><span data-stu-id="c312b-201">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Кнопка "Прекратить резервное копирование"](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="c312b-203">Откроется колонка "Прекратить резервное копирование".</span><span class="sxs-lookup"><span data-stu-id="c312b-203">The Stop Backup blade opens.</span></span>

    ![Колонка "Прекратить резервное копирование"](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="c312b-205">В колонке **Остановка резервного копирования** укажите, будут ли данные резервного копирования сохранены или удалены.</span><span class="sxs-lookup"><span data-stu-id="c312b-205">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span></span> <span data-ttu-id="c312b-206">В поле сведений содержится информация о вариантах выбора и возможных последствиях.</span><span class="sxs-lookup"><span data-stu-id="c312b-206">The information box provides details about your choice.</span></span>

    ![Остановить защиту](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="c312b-208">Если вы решили сохранить данные резервного копирования, перейдите к шагу 4.</span><span class="sxs-lookup"><span data-stu-id="c312b-208">If you chose to retain the backup data, skip to step 4.</span></span> <span data-ttu-id="c312b-209">При удалении данных резервного копирования подтвердите остановку заданий резервного копирования и удалите точки восстановления (введите имя элемента).</span><span class="sxs-lookup"><span data-stu-id="c312b-209">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span></span>

    ![Остановить проверку](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="c312b-211">Если вы не помните имя элемента, чтобы просмотреть его, наведите указатель мыши на восклицательный знак.</span><span class="sxs-lookup"><span data-stu-id="c312b-211">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="c312b-212">Имя элемента также отображается в верхней части колонки **Остановка резервного копирования** .</span><span class="sxs-lookup"><span data-stu-id="c312b-212">Also, the name of the item is under **Stop Backup** at the top of the blade.</span></span>
4. <span data-ttu-id="c312b-213">При желании можно указать **причину** или добавить **комментарий**.</span><span class="sxs-lookup"><span data-stu-id="c312b-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="c312b-214">Чтобы остановить задание резервного копирования для текущего элемента, щелкните ![резервного копирования "Остановить"](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="c312b-214">To stop the backup job for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="c312b-215">После остановки отобразится сообщение с соответствующим уведомлением.</span><span class="sxs-lookup"><span data-stu-id="c312b-215">A notification message lets you know the backup jobs have been stopped.</span></span>

    ![Подтверждение остановки защиты](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="c312b-217">Возобновление защиты виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c312b-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="c312b-218">Если при остановке защиты **данные резервного копирования были сохранены** , их можно использовать для возобновления защиты виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c312b-218">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span></span> <span data-ttu-id="c312b-219">Если **данные резервного копирования были удалены** , защиту виртуальной машины восстановить невозможно.</span><span class="sxs-lookup"><span data-stu-id="c312b-219">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span></span>

<span data-ttu-id="c312b-220">Чтобы восстановить защиту виртуальной машины, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c312b-220">To resume protection for the virtual machine</span></span>

1. <span data-ttu-id="c312b-221">На [панели мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard)щелкните **Возобновить резервное копирование**.</span><span class="sxs-lookup"><span data-stu-id="c312b-221">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Возобновить защиту](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="c312b-223">После этого откроется колонка "Политика архивации".</span><span class="sxs-lookup"><span data-stu-id="c312b-223">The Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c312b-224">При повторной защите виртуальной машины можно выбрать другую политику, отличную от политики, с помощью которой виртуальная машина была защищена изначально.</span><span class="sxs-lookup"><span data-stu-id="c312b-224">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="c312b-225">Чтобы назначить политику для виртуальной машины, следуйте инструкциям в разделе [Управление политиками резервного копирования](backup-azure-manage-vms.md#manage-backup-policies).</span><span class="sxs-lookup"><span data-stu-id="c312b-225">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span></span>

    <span data-ttu-id="c312b-226">После применения политики к виртуальной машине вы увидите следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="c312b-226">Once the backup policy is applied to the virtual machine, you see the following message.</span></span>

    ![Защищенные виртуальные машины](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="c312b-228">данные резервного копирования были удалены</span><span class="sxs-lookup"><span data-stu-id="c312b-228">Delete Backup data</span></span>
<span data-ttu-id="c312b-229">Данные резервного копирования, связанные с виртуальной машиной, можно удалить при **остановке резервного копирования** или в любое время после завершения этой операции.</span><span class="sxs-lookup"><span data-stu-id="c312b-229">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span></span> <span data-ttu-id="c312b-230">Возможно, стоит подождать несколько дней или недель, прежде чем удалять точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="c312b-230">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="c312b-231">В отличие от восстановления точек восстановления при удалении данных резервного копирования нельзя выбрать определенные точки для удаления.</span><span class="sxs-lookup"><span data-stu-id="c312b-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span></span> <span data-ttu-id="c312b-232">При удалении данных резервного копирования удаляются все точки восстановления, связанные с этим элементом.</span><span class="sxs-lookup"><span data-stu-id="c312b-232">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="c312b-233">В следующей процедуре подразумевается, что задание резервного копирования для виртуальной машины остановлено или отключено.</span><span class="sxs-lookup"><span data-stu-id="c312b-233">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="c312b-234">Только после остановки этого задания на панели мониторинга элемента хранилища станут доступными параметры **Возобновить архивацию** и **Удаление архива**.</span><span class="sxs-lookup"><span data-stu-id="c312b-234">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span></span>

![Кнопки возобновления и удаления](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="c312b-236">Чтобы удалить данные резервного копирования на виртуальной машине с *отключенным заданием резервного копирования*, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="c312b-236">To delete backup data on a virtual machine with the *Backup disabled*:</span></span>

1. <span data-ttu-id="c312b-237">На [панели мониторинга элемента хранилища](backup-azure-manage-vms.md#open-a-vault-item-dashboard)щелкните **Delete backup**(Удалить резервную копию).</span><span class="sxs-lookup"><span data-stu-id="c312b-237">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Тип виртуальной машины](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="c312b-239">Откроется колонка **Удаление данных архивации** .</span><span class="sxs-lookup"><span data-stu-id="c312b-239">The **Delete Backup Data** blade opens.</span></span>

    ![Тип виртуальной машины](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="c312b-241">Чтобы подтвердить удаление точек восстановления, введите имя элемента.</span><span class="sxs-lookup"><span data-stu-id="c312b-241">Type the name of the item to confirm you want to delete the recovery points.</span></span>

    ![Остановить проверку](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="c312b-243">Если вы не помните имя элемента, чтобы просмотреть его, наведите указатель мыши на восклицательный знак.</span><span class="sxs-lookup"><span data-stu-id="c312b-243">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="c312b-244">Имя элемента также отображается в верхней части колонки **Удаление данных архивации** .</span><span class="sxs-lookup"><span data-stu-id="c312b-244">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span></span>
3. <span data-ttu-id="c312b-245">При желании можно указать **причину** или добавить **комментарий**.</span><span class="sxs-lookup"><span data-stu-id="c312b-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="c312b-246">Для удаления архивируемых данных для текущего элемента, нажмите кнопку ![резервного копирования "Остановить"](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="c312b-246">To delete the backup data for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="c312b-247">После удаления отобразится сообщение с соответствующим уведомлением.</span><span class="sxs-lookup"><span data-stu-id="c312b-247">A notification message lets you know the backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c312b-248">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c312b-248">Next steps</span></span>
<span data-ttu-id="c312b-249">Сведения о восстановлении виртуальных машин из точки восстановления см. в статье [Восстановление виртуальных машин в Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="c312b-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="c312b-250">Сведения о защите виртуальных машин см. в статье [Первое знакомство. Защита виртуальных машин Azure в хранилище служб восстановления](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c312b-250">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="c312b-251">Дополнительные сведения о мониторинге событий см. в статье [Мониторинг предупреждений в резервных копиях виртуальных машин Azure](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="c312b-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
