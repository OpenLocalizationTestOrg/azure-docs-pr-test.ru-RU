---
title: "Установка Azure Backup Server версии 2 | Документация Майкрософт"
description: "Azure Backup Server версии 2 предоставляет расширенные возможности резервного копирования для защиты виртуальных машин, файлов и папок, рабочих нагрузок и т. д. Узнайте, как установить Azure Backup Server версии 2 или выполнить обновление до этой версии."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 1bbb16afef7940933b4c3ae23873f212770137e0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="6bccf-104">Установка Azure Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="6bccf-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="6bccf-105">Azure Backup Server обеспечивает защиту виртуальных машин, рабочих нагрузок, файлов, папок и т. д.</span><span class="sxs-lookup"><span data-stu-id="6bccf-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="6bccf-106">Компонент Azure Backup Server версии 2 основан на Azure Backup Server версии 1 и предоставляет новые функции, недоступные в версии 1.</span><span class="sxs-lookup"><span data-stu-id="6bccf-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="6bccf-107">Сравнение функций версии 1 и версии 2 см. в [таблице поддержки защиты Azure Backup Server](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="6bccf-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="6bccf-108">Дополнительные функции Backup Server версии 2 представляют собой обновление Backup Server версии 1.</span><span class="sxs-lookup"><span data-stu-id="6bccf-108">The additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="6bccf-109">Тем не менее Backup Server версии 1 не является необходимым компонентом для установки Backup Server версии 2.</span><span class="sxs-lookup"><span data-stu-id="6bccf-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="6bccf-110">Чтобы обновить Backup Server версии 1 до версии 2, установите Backup Server версии 2 на сервере защиты Backup Server.</span><span class="sxs-lookup"><span data-stu-id="6bccf-110">If you want to upgrade from Backup Server v1 to Backup Server v2, install Backup Server v2 on the Backup Server protection server.</span></span> <span data-ttu-id="6bccf-111">Существующие параметры Backup Server останутся неизменными.</span><span class="sxs-lookup"><span data-stu-id="6bccf-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="6bccf-112">Backup Server версии 2 можно установить на сервере Windows Server 2012 R2 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6bccf-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="6bccf-113">Чтобы воспользоваться преимуществами новых функций, например Modern Backup Storage в System Center 2016 Data Protection Manager, необходимо установить Backup Server версии 2 на сервере Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6bccf-113">To take advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="6bccf-114">Прежде чем установить Backup Server версии 2 или выполнить обновление до этой версии, ознакомьтесь с [необходимыми для установки компонентами](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="6bccf-114">Before you upgrade to or install Backup Server v2, read about the [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="6bccf-115">База кода Azure Backup Server такая же, как и в System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="6bccf-115">Azure Backup Server has the same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="6bccf-116">Backup Server версии 1 является аналогом Data Protection Manager 2012 R2, а Backup Server версии 2 — аналогом Data Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="6bccf-116">Backup Server v1 is equivalent to Data Protection Manager 2012 R2, and Backup Server v2 is equivalent to Data Protection Manager 2016.</span></span> <span data-ttu-id="6bccf-117">В некоторых разделах этой статьи содержатся ссылки на документацию по Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="6bccf-117">This article occasionally references the Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-to-v2"></a><span data-ttu-id="6bccf-118">Обновление Backup Server до версии 2</span><span class="sxs-lookup"><span data-stu-id="6bccf-118">Upgrade Backup Server to v2</span></span>
<span data-ttu-id="6bccf-119">Чтобы обновить Backup Server версии 1 до версии 2, убедитесь, что для установки имеются необходимые обновления:</span><span class="sxs-lookup"><span data-stu-id="6bccf-119">To upgrade from Backup Server v1 to Backup Server v2, make sure your installation has the required updates:</span></span>

- <span data-ttu-id="6bccf-120">[обновление агентов защиты](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) на защищенных серверах;</span><span class="sxs-lookup"><span data-stu-id="6bccf-120">[Update the protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on the protected servers.</span></span>
- <span data-ttu-id="6bccf-121">обновление Windows Server 2012 R2 до Windows Server 2016;</span><span class="sxs-lookup"><span data-stu-id="6bccf-121">Upgrade Windows Server 2012 R2 to Windows Server 2016.</span></span>
- <span data-ttu-id="6bccf-122">обновление удаленного администратора Azure Backup Server на всех рабочих серверах;</span><span class="sxs-lookup"><span data-stu-id="6bccf-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="6bccf-123">резервные копии продолжают создаваться без перезагрузки рабочего сервера.</span><span class="sxs-lookup"><span data-stu-id="6bccf-123">Ensure that backups are set to continue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="6bccf-124">Действия по обновлению до Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="6bccf-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="6bccf-125">В Центре загрузки [скачайте установщик обновления](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="6bccf-125">In the Download Center, [download the upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="6bccf-126">После извлечения мастера установки установите флажок **Execute setup.exe** (Выполнить setup.exe) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-126">After you extract the setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Установщик — выполнение установки](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="6bccf-128">В разделе **Установка** мастера Microsoft Azure Backup Server выберите **Сервер службы архивации Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-128">In the Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Установщик — выбор установки](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="6bccf-130">На странице **приветствия** ознакомьтесь с предупреждениями и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-130">On the **Welcome** page, review the warnings, and then select **Next**.</span></span>

  ![Установщик — страница приветствия](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="6bccf-132">Мастер установки выполнит проверку на наличие необходимых компонентов, чтобы убедиться в готовности среды к установке обновления.</span><span class="sxs-lookup"><span data-stu-id="6bccf-132">The setup wizard performs prerequisite checks to make sure your environment can upgrade.</span></span> <span data-ttu-id="6bccf-133">На странице **Проверки на наличие необходимых компонентов** нажмите кнопку **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-133">On the **Prerequisite Checks** page, select **Check**.</span></span>

  ![Установщик — страница "Проверки на наличие необходимых компонентов"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="6bccf-135">Среда должна пройти проверки на наличие необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="6bccf-135">Your environment must pass the prerequisite checks.</span></span> <span data-ttu-id="6bccf-136">Если она не прошла проверки, обратите внимание на проблемы и устраните их.</span><span class="sxs-lookup"><span data-stu-id="6bccf-136">If your environment doesn't pass the checks, note the issues and fix them.</span></span> <span data-ttu-id="6bccf-137">Затем нажмите кнопку **Повторить проверку**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-137">Then, select **Check Again**.</span></span> <span data-ttu-id="6bccf-138">После прохождения проверок на наличие необходимых компонентов нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-138">After you pass the prerequisite checks, select **Next**.</span></span>

  ![Установщик — кнопка "Повторить проверку"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="6bccf-140">На странице **Настройки SQL** выберите соответствующий параметр для установки SQL и нажмите кнопку **Проверить и установить**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-140">On the **SQL Settings** page, select the relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Установщик — страница "Настройки SQL"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="6bccf-142">Проверка может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6bccf-142">The checks might take a few minutes.</span></span> <span data-ttu-id="6bccf-143">По завершении проверки нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-143">When the checks are finished, select **Next**.</span></span>

  ![Установщик — кнопка "Проверить и установить" на странице "Настройки SQL"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="6bccf-145">На странице **Параметры установки** измените расположение файлов установки Backup Server или вспомогательное расположение.</span><span class="sxs-lookup"><span data-stu-id="6bccf-145">On the **Installation Settings** page, make any changes to the location where Backup Server is installed, or to the Scratch Location.</span></span> <span data-ttu-id="6bccf-146">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-146">Select **Next**.</span></span>

  ![Установщик — страница "Параметры установки"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="6bccf-148">Чтобы завершить работу мастера установки, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-148">To finish the setup wizard, select **Finish**.</span></span>

  ![Установщик — кнопка "Готово"](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="6bccf-150">Добавление хранилища для Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="6bccf-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="6bccf-151">Чтобы повысить эффективность хранилища резервных копий, в Backup Server версии 2 добавлена поддержка томов.</span><span class="sxs-lookup"><span data-stu-id="6bccf-151">To improve backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="6bccf-152">Как и Backup Server версии 1, Backup Server версии 2 поддерживает диски.</span><span class="sxs-lookup"><span data-stu-id="6bccf-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="6bccf-153">Добавление томов и дисков</span><span class="sxs-lookup"><span data-stu-id="6bccf-153">Add volumes and disks</span></span>
<span data-ttu-id="6bccf-154">Если компонент Backup Server версии 2 запущен на сервере Windows Server 2016, вы можете использовать тома для хранения данных резервных копий.</span><span class="sxs-lookup"><span data-stu-id="6bccf-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes to store backup data.</span></span> <span data-ttu-id="6bccf-155">Тома обеспечивают экономию места в хранилище и более быстрое создание резервных копий.</span><span class="sxs-lookup"><span data-stu-id="6bccf-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="6bccf-156">Тома — это новая функция в Backup Server, поэтому их необходимо добавить.</span><span class="sxs-lookup"><span data-stu-id="6bccf-156">Because volumes are new to Backup Server, you must add them.</span></span> 

<span data-ttu-id="6bccf-157">При добавлении тома в Backup Server вы можете присвоить ему понятное имя.</span><span class="sxs-lookup"><span data-stu-id="6bccf-157">When you add a volume to Backup Server, you can give the volume a friendly name.</span></span> <span data-ttu-id="6bccf-158">Щелкните столбец **Понятное имя** для тома, которому необходимо присвоить имя.</span><span class="sxs-lookup"><span data-stu-id="6bccf-158">Click the **Friendly Name** column of the volume you want to name.</span></span> <span data-ttu-id="6bccf-159">При необходимости имя можно изменить позже.</span><span class="sxs-lookup"><span data-stu-id="6bccf-159">You can change the name later, if necessary.</span></span> <span data-ttu-id="6bccf-160">Вы также можете использовать PowerShell, чтобы добавлять или изменять понятные имена томов.</span><span class="sxs-lookup"><span data-stu-id="6bccf-160">You also can use PowerShell to add or change friendly names for volumes.</span></span>

<span data-ttu-id="6bccf-161">Чтобы добавить том, в консоли администратора сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="6bccf-161">To add a volume in the Administrator Console:</span></span>

1. <span data-ttu-id="6bccf-162">В консоли администратора Azure Backup Server последовательно выберите **Управление** > **Дисковый накопитель** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-162">In the Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Открытие мастера добавления дискового накопителя](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="6bccf-164">Откроется мастер добавления дискового накопителя.</span><span class="sxs-lookup"><span data-stu-id="6bccf-164">This opens the Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="6bccf-165">На странице **Добавить дисковый накопитель** в области **Доступные тома** выберите том и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-165">On the **Add Disk Storage** page, in the **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="6bccf-166">В области **Выбранные тома** введите понятное имя для тома и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-166">In the **Selected volumes** box, enter a friendly name for the volume, and then select **OK**.</span></span>

      ![Мастер добавления дискового накопителя — добавление тома](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="6bccf-168">Если необходимо добавить диск, он должен входить в группу защиты с хранилищем прежней версии.</span><span class="sxs-lookup"><span data-stu-id="6bccf-168">If you want to add a disk, the disk must belong to a protection group that has legacy storage.</span></span> <span data-ttu-id="6bccf-169">Такие диски можно использовать только для этих групп защиты.</span><span class="sxs-lookup"><span data-stu-id="6bccf-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="6bccf-170">Если в Backup Server нет источников с защитой прежней версии, диск не будет отображаться в списке.</span><span class="sxs-lookup"><span data-stu-id="6bccf-170">If Backup Server doesn't have sources that have legacy protection, the disk isn't listed.</span></span>

  <span data-ttu-id="6bccf-171">Дополнительные сведения о добавлении дисков см. в разделе [Adding disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage) (Добавление дисков для увеличения хранилища прежней версии).</span><span class="sxs-lookup"><span data-stu-id="6bccf-171">For more information about adding disks, see [Adding disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="6bccf-172">Диску нельзя присвоить понятное имя.</span><span class="sxs-lookup"><span data-stu-id="6bccf-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-to-volumes"></a><span data-ttu-id="6bccf-173">Назначение рабочих нагрузок для томов</span><span class="sxs-lookup"><span data-stu-id="6bccf-173">Assign workloads to volumes</span></span>

<span data-ttu-id="6bccf-174">В Backup Server вы указываете тома и рабочие нагрузки, которые им назначаются.</span><span class="sxs-lookup"><span data-stu-id="6bccf-174">In Backup Server, you specify which workloads are assigned to which volumes.</span></span> <span data-ttu-id="6bccf-175">Например, можно указать ресурсоемкие тома, которые поддерживают большое количество операций ввода-вывода в секунду, для хранения только рабочих нагрузок, требующих частого создания резервных копий большого объема.</span><span class="sxs-lookup"><span data-stu-id="6bccf-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="6bccf-176">Примером может быть SQL Server с журналами транзакций.</span><span class="sxs-lookup"><span data-stu-id="6bccf-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="6bccf-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="6bccf-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="6bccf-178">Чтобы обновить свойства тома в пуле носителей Backup Server, используйте командлет PowerShell Update-DPMDiskStorage.</span><span class="sxs-lookup"><span data-stu-id="6bccf-178">To update the properties of a volume in the storage pool in Backup Server, use the PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="6bccf-179">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="6bccf-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="6bccf-180">Все изменения, внесенные с помощью PowerShell, отражаются в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="6bccf-180">All changes that you make by using PowerShell are reflected in the UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="6bccf-181">Защита источников данных</span><span class="sxs-lookup"><span data-stu-id="6bccf-181">Protect data sources</span></span>
<span data-ttu-id="6bccf-182">Чтобы обеспечить защиту источников данных, создайте группу защиты.</span><span class="sxs-lookup"><span data-stu-id="6bccf-182">To begin protecting data sources, create a protection group.</span></span> <span data-ttu-id="6bccf-183">В следующих шагах продемонстрированы изменения или дополнения в мастере создания групп защиты.</span><span class="sxs-lookup"><span data-stu-id="6bccf-183">The following steps highlight changes or additions to the New Protection Group wizard.</span></span>

<span data-ttu-id="6bccf-184">Чтобы создать группу защиты, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="6bccf-184">To create a protection group:</span></span>

1. <span data-ttu-id="6bccf-185">В консоли администратора Backup Server выберите **Защита**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-185">In the Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="6bccf-186">На ленте инструментов щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-186">On the tool ribbon, select **New**.</span></span>

    <span data-ttu-id="6bccf-187">Откроется мастер создания групп защиты.</span><span class="sxs-lookup"><span data-stu-id="6bccf-187">This opens the Create New Protection Group wizard.</span></span>

  ![Создание мастера создания новой группы защиты](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="6bccf-189">На странице **приветствия** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-189">On the **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="6bccf-190">На странице **Выбор типа группы защиты** выберите тип группы защиты, которую необходимо создать, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-190">On the **Select Protection Group Type** page, select the type of protection group you want to create, and then select **Next**.</span></span>

  ![Страница "Выбор типа группы защиты"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="6bccf-192">На странице **Выбор элементов группы** в области **Доступные элементы** перечислены элементы с агентами защиты.</span><span class="sxs-lookup"><span data-stu-id="6bccf-192">On the **Select Group Members** page, in the **Available members** pane, the members with protection agents are listed.</span></span> <span data-ttu-id="6bccf-193">Для этого примера выберите тома D:\ и E:\ и добавьте их в область **Выбранные элементы**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-193">For this example, select volume D:\ and E:\ and add them to the **Selected members** pane.</span></span> <span data-ttu-id="6bccf-194">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-194">Select **Next**.</span></span>

  ![Страница "Выбор элементов группы"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="6bccf-196">На странице **Выбор метода защиты данных** введите имя в поле **Имя группы защиты**, выберите необходимый метод защиты и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-196">On the **Select Data Protection Method** page, enter a **Protection group name**, select the protection method, and then select **Next**.</span></span> <span data-ttu-id="6bccf-197">Если требуется краткосрочная защита, необходимо выбрать метод резервного копирования с помощью **диска**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-197">If you want short-term protection, you must select the **Disk** backup method.</span></span>

  ![Страница "Выбор метода защиты данных"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="6bccf-199">На странице **Выбор краткосрочных целей** задайте значения для параметров **Диапазон хранения** и **Частота синхронизации**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-199">On the **Specify Short-Term Goals** page, select the details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="6bccf-200">Затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-200">Then, select **Next**.</span></span> <span data-ttu-id="6bccf-201">Если потребуется изменить расписание для создания точек восстановления, нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-201">Optionally, to change the schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Страница "Выбор краткосрочных целей"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="6bccf-203">На странице **Проверка выделения дискового накопителя** просмотрите сведения о выбранных источниках данных: их размер, значения для подготавливаемого пространства и целевой том хранилища.</span><span class="sxs-lookup"><span data-stu-id="6bccf-203">On the **Review Disk Storage Allocation** page, review details about the data sources you selected, their size, and  values for the space to be provisioned and the target storage volume.</span></span>

  ![Страница "Проверка выделения дискового накопителя"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="6bccf-205">Тома хранилища предоставляются с учетом выделения томов для рабочих нагрузок (задаются с помощью PowerShell) и доступного объема хранилища.</span><span class="sxs-lookup"><span data-stu-id="6bccf-205">Storage volumes are based on the workload volume allocation (set by using PowerShell) and the available storage.</span></span> <span data-ttu-id="6bccf-206">Тома хранилища можно изменить, выбрав другие в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="6bccf-206">You can change the storage volumes by selecting other volumes in the drop-down menu.</span></span> <span data-ttu-id="6bccf-207">Если изменить значение параметра **Целевой накопитель**, значения в таблице **Доступный дисковый накопитель** динамически изменятся. Это будет отражено в столбцах **Свободное пространство** и **Underprovisioned Space** (Неподготовленное пространство).</span><span class="sxs-lookup"><span data-stu-id="6bccf-207">If you change the value for **Target Storage**, the value for **Available disk storage** dynamically changes to reflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="6bccf-208">Если источники данных увеличиваются согласно плану, значение в столбце **Underprovisioned Space** (Неподготовленное пространство) таблицы **Доступный дисковый накопитель** будет отражать требуемый объем для дополнительного хранилища.</span><span class="sxs-lookup"><span data-stu-id="6bccf-208">If the data sources grow as planned, the value for the **Underprovisioned Space** column in **Available disk storage** reflects the amount of additional storage that's needed.</span></span> <span data-ttu-id="6bccf-209">Используйте это значение, чтобы учитывать потребности в объеме хранилища при планировании бесперебойного резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="6bccf-209">Use this value to help plan your storage needs for smooth backups.</span></span> <span data-ttu-id="6bccf-210">Если значение равно нулю, потенциальные проблемы с хранилищем не предвидятся в ближайшем будущем.</span><span class="sxs-lookup"><span data-stu-id="6bccf-210">If the value is zero, there are no potential problems with storage in the foreseeable future.</span></span> <span data-ttu-id="6bccf-211">Если значение отлично от нуля, то места в хранилище недостаточно (с учетом политики защиты и размера данных защищенных элементов).</span><span class="sxs-lookup"><span data-stu-id="6bccf-211">If the value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and the data size of your protected members).</span></span>

  ![Неподготовленное дисковое пространство](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="6bccf-213">Чтобы завершить создание группы защиты, завершите работу мастера.</span><span class="sxs-lookup"><span data-stu-id="6bccf-213">To finish creating your protection group, complete the wizard.</span></span>

## <a name="migrate-legacy-storage-to-modern-backup-storage"></a><span data-ttu-id="6bccf-214">Перенос хранилища прежней версии в Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="6bccf-214">Migrate legacy storage to Modern Backup Storage</span></span>
<span data-ttu-id="6bccf-215">После установки Backup Server версии 2 или обновления до этой версии, а также обновления операционной системы до Windows Server 2016 обновите группы защиты, чтобы использовать Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="6bccf-215">After you upgrade to or install Backup Server v2 and upgrade the operating system to Windows Server 2016, update your protection groups to use Modern Backup Storage.</span></span> <span data-ttu-id="6bccf-216">По умолчанию группы защиты не изменяются.</span><span class="sxs-lookup"><span data-stu-id="6bccf-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="6bccf-217">Они будут работать согласно изначальным настройкам.</span><span class="sxs-lookup"><span data-stu-id="6bccf-217">They continue to function as they were initially set up.</span></span> 

<span data-ttu-id="6bccf-218">Обновлять группы защиты, чтобы использовать Modern Backup Storage, необязательно.</span><span class="sxs-lookup"><span data-stu-id="6bccf-218">Updating protection groups to use Modern Backup Storage is optional.</span></span> <span data-ttu-id="6bccf-219">Чтобы обновить группу защиты, остановите защиту всех источников данных, используя параметр сохранения данных.</span><span class="sxs-lookup"><span data-stu-id="6bccf-219">To update the protection group, stop protection of all data sources by using the retain data option.</span></span> <span data-ttu-id="6bccf-220">Затем добавьте источники данных в новую группу защиты.</span><span class="sxs-lookup"><span data-stu-id="6bccf-220">Then, add the data sources to a new protection group.</span></span>

1. <span data-ttu-id="6bccf-221">В консоли администратора выберите функцию **Защита**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-221">In the Administrator Console, select the **Protection** feature.</span></span> <span data-ttu-id="6bccf-222">В списке **Член группы защиты** щелкните элемент правой кнопкой мыши и выберите пункт **Остановить защиту элемента**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-222">In the **Protection Group Member** list, right-click the member, and then select **Stop protection of member**.</span></span>

  ![Остановка защиты элемента](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="6bccf-224">В диалоговом окне **Удалить из группы** проверьте используемый объем дискового пространства и объем доступного свободного пространства для пула носителей.</span><span class="sxs-lookup"><span data-stu-id="6bccf-224">In the **Remove from Group** dialog box, review the used disk space and the available free space for the storage pool.</span></span> <span data-ttu-id="6bccf-225">По умолчанию точки восстановления остаются на диске, а их срок хранения истекает согласно связанной политике хранения.</span><span class="sxs-lookup"><span data-stu-id="6bccf-225">The default is to leave the recovery points on the disk and allow them to expire per their associated retention policy.</span></span> <span data-ttu-id="6bccf-226">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-226">Click **OK**.</span></span>

  <span data-ttu-id="6bccf-227">Если необходимо сразу освободить используемое дисковое пространство для пула носителей, установите флажок **Удалить реплику на диске**, чтобы удалить данные резервных копий (и точки восстановления), связанные с этим элементом.</span><span class="sxs-lookup"><span data-stu-id="6bccf-227">If you want to immediately return the used disk space to the free storage pool, select the **Delete replica on disk** check box to delete the backup data (and recovery points) associated with that member.</span></span>

  ![Диалоговое окно "Удалить из группы"](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="6bccf-229">Создайте группу защиты, которая использует Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="6bccf-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="6bccf-230">Добавьте незащищенные источники данных.</span><span class="sxs-lookup"><span data-stu-id="6bccf-230">Include the unprotected data sources.</span></span>


## <a name="add-disks-to-increase-legacy-storage"></a><span data-ttu-id="6bccf-231">Добавление дисков для увеличения хранилища прежней версии</span><span class="sxs-lookup"><span data-stu-id="6bccf-231">Add disks to increase legacy storage</span></span>

<span data-ttu-id="6bccf-232">Если необходимо использовать хранилище прежней версии на Backup Server, может потребоваться добавить диски, чтобы увеличить это хранилище.</span><span class="sxs-lookup"><span data-stu-id="6bccf-232">If you want to use legacy storage with Backup Server, you might need to add disks to increase legacy storage.</span></span> 

<span data-ttu-id="6bccf-233">Чтобы добавить дисковый накопитель, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="6bccf-233">To add disk storage:</span></span>

1. <span data-ttu-id="6bccf-234">В консоли администратора последовательно выберите **Управление** > **Дисковый накопитель** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-234">In the Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Диалоговое окно "Добавить дисковый накопитель"](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="6bccf-236">В диалоговом окне **Добавить дисковый накопитель** щелкните **Добавить диски**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-236">In the **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="6bccf-237">В списке доступных дисков выберите диски, которые требуется добавить, нажмите кнопку **Добавить** и кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-237">In the list of available disks, select the disks you want to add, select **Add**, and then select **OK**.</span></span>

## <a name="update-the-data-protection-manager-protection-agent"></a><span data-ttu-id="6bccf-238">Обновление агента защиты Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="6bccf-238">Update the Data Protection Manager protection agent</span></span>

<span data-ttu-id="6bccf-239">Для обновлений Backup Server используется агент защиты System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="6bccf-239">Backup Server uses the System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="6bccf-240">При обновлении агента защиты, не подключенного к сети, вы не сможете завершить обновление подключенного агента с помощью консоли администрирования Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="6bccf-240">If you are upgrading a protection agent that is not connected to the network, you cannot use the Data Protection Manager Administrator Console to complete a connected agent upgrade.</span></span> <span data-ttu-id="6bccf-241">Агент защиты необходимо обновить в неактивной доменной среде.</span><span class="sxs-lookup"><span data-stu-id="6bccf-241">You must upgrade the protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="6bccf-242">Если клиентский компьютер не подключен к сети, в консоли администрирования Data Protection Manager отображается сообщение о том, что ожидается обновление агента защиты.</span><span class="sxs-lookup"><span data-stu-id="6bccf-242">Until the client computer is connected to the network, the Data Protection Manager Administrator Console shows that the protection agent update is pending.</span></span>

<span data-ttu-id="6bccf-243">В следующих разделах объясняется, как обновить агенты защиты на клиентских компьютерах, подключенных и не подключенных к сети.</span><span class="sxs-lookup"><span data-stu-id="6bccf-243">The following sections describe how to update protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="6bccf-244">Обновление агента защиты на клиентском компьютере, подключенном к сети</span><span class="sxs-lookup"><span data-stu-id="6bccf-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="6bccf-245">В консоли администратора Backup Server выберите **Управление** > **Агенты**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-245">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="6bccf-246">На панели отображения выберите клиентские компьютеры, на которых требуется обновить агент защиты.</span><span class="sxs-lookup"><span data-stu-id="6bccf-246">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6bccf-247">В столбце **Обновления агентов** отображаются сведения о доступности обновлений агента защиты для каждого защищенного компьютера.</span><span class="sxs-lookup"><span data-stu-id="6bccf-247">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="6bccf-248">Действие **Обновить** доступно в области **Действия**, только если защищенный компьютер выбран и обновления доступны.</span><span class="sxs-lookup"><span data-stu-id="6bccf-248">In the **Actions** pane, the **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="6bccf-249">Чтобы установить обновленные агенты защиты на выбранных компьютерах, в области **Действия** выберите **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-249">To install updated protection agents on the selected computers, in the **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="6bccf-250">Обновление агента защиты на клиентском компьютере, не подключенном к сети</span><span class="sxs-lookup"><span data-stu-id="6bccf-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="6bccf-251">В консоли администратора Backup Server выберите **Управление** > **Агенты**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-251">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="6bccf-252">На панели отображения выберите клиентские компьютеры, на которых требуется обновить агент защиты.</span><span class="sxs-lookup"><span data-stu-id="6bccf-252">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="6bccf-253">В столбце **Обновления агентов** отображаются сведения о доступности обновлений агента защиты для каждого защищенного компьютера.</span><span class="sxs-lookup"><span data-stu-id="6bccf-253">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="6bccf-254">Действие **Обновить** недоступно в области **Действия**, если защищенный компьютер выбран, но обновления недоступны.</span><span class="sxs-lookup"><span data-stu-id="6bccf-254">In the **Actions** pane, the **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="6bccf-255">Чтобы установить обновленные агенты защиты на выбранных компьютерах, выберите **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-255">To install updated protection agents on the selected computers, select **Update**.</span></span>

4. <span data-ttu-id="6bccf-256">На клиентском компьютере, не подключенном к сети, в столбце **Состояние агента** будет отображаться элемент **Обновить ожидание**, пока компьютер не подключится к сети.</span><span class="sxs-lookup"><span data-stu-id="6bccf-256">For a client computer that is not connected to the network, until the computer is connected to the network, the **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="6bccf-257">После подключения клиентского компьютера к сети в столбце **Обновления агентов** для клиентского компьютера отобразится состояние **Обновление**.</span><span class="sxs-lookup"><span data-stu-id="6bccf-257">After a client computer is connected to the network, the **Agent Updates** column for the client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-the-new-version-with-azure"></a><span data-ttu-id="6bccf-258">Перемещение старых групп защиты из старой версии и синхронизация новой версии с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="6bccf-258">Move legacy Protection groups from old version and sync the new version with Azure</span></span>

<span data-ttu-id="6bccf-259">После обновления Azure Backup Server и операционной системы все готово для защиты новых источников данных с помощью Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="6bccf-259">Once Azure Backup Server and the OS are both updated, you are ready to protect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="6bccf-260">Однако защищенные источники данных будут продолжать использовать старую модель защиты в Azure Backup Server, а все новые элементы защиты будут использовать Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="6bccf-260">However already protected data sources will continue to be protected in the legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="6bccf-261">Шаги, описанные ниже, позволяют перенести источники данных из устаревшего режима защиты в Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="6bccf-261">Below steps are to migrate data sources from legacy  mode of protection to Modern backup storage.</span></span>

<span data-ttu-id="6bccf-262">• Добавьте новые тома в пул хранилища DPM и при необходимости назначьте понятные имена и теги источников данных.</span><span class="sxs-lookup"><span data-stu-id="6bccf-262">• Add the new volume(s) to the DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="6bccf-263">• Остановите защиту каждого источника данных, который находится в старом режиме, и сохраните защищенные данные.</span><span class="sxs-lookup"><span data-stu-id="6bccf-263">• For each data source that is in legacy mode, stop protection of the data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="6bccf-264">Так вы сможете восстановить старые точки восстановления после миграции.</span><span class="sxs-lookup"><span data-stu-id="6bccf-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="6bccf-265">• Создайте группу защиты и выберите источники данных, которые нужно сохранить, с использованием нового формата.</span><span class="sxs-lookup"><span data-stu-id="6bccf-265">• Create a new PG and select the data sources that are to be stored using new format.</span></span>
<span data-ttu-id="6bccf-266">• DPM создаст локальную копию реплики старого хранилища резервных копий на томе Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="6bccf-266">• DPM will do a replica copy from the legacy backup storage into the Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="6bccf-267">Примечание. Это будет рассматриваться как задания операций, выполняемых после восстановления. • Все новые точки синхронизации и восстановления будут храниться в Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="6bccf-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="6bccf-268">• После истечения срока действия старые точки восстановления будут удалены, освобождая место на диске.</span><span class="sxs-lookup"><span data-stu-id="6bccf-268">• Old recovery points will be pruned out as they expire and eventually free up the disk space.</span></span>
<span data-ttu-id="6bccf-269">• После удаления всех старых томов из старого хранилища диск можно удалить из Azure Backup и из системы.</span><span class="sxs-lookup"><span data-stu-id="6bccf-269">• Once all the legacy volumes are deleted from the old storage, the disk can be removed from Azure backup and the system.</span></span>
<span data-ttu-id="6bccf-270">• Создайте резервную копию Azure DPMDB.</span><span class="sxs-lookup"><span data-stu-id="6bccf-270">• Take a backup of the  Azure DPMDB.</span></span>

<span data-ttu-id="6bccf-271">Часть 2. Важные элементы > Новому серверу нужно присвоить то же имя, что и исходному серверу Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="6bccf-271">Part 2: -Important items> The new server will need to be named same as the original Azure Backup server.</span></span> <span data-ttu-id="6bccf-272">Невозможно изменить имя нового сервера Azure Backup Server, если вы хотите использовать старый пул носителей и DPMDB для хранения точек восстановления. Нужна резервная копия DPMDB, так как потребуется восстановление.</span><span class="sxs-lookup"><span data-stu-id="6bccf-272">You cannot change the name of the new Azure backup server if you want to use old storage pool and DPMDB to retain recovery points -Must have backup of DPMDB  as it will need to be restored</span></span>

1) <span data-ttu-id="6bccf-273">Завершите работу исходного сервера Azure Backup Server или отключите его от сети.</span><span class="sxs-lookup"><span data-stu-id="6bccf-273">Shutdown the original Azure backup server or take it off the wire.</span></span>
2) <span data-ttu-id="6bccf-274">Сбросьте учетную запись компьютера в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6bccf-274">Reset the machine account in active directory.</span></span>
3) <span data-ttu-id="6bccf-275">Установите Server 2016 на новом компьютере и присвойте ему имя, совпадающее с именем компьютера исходного сервера Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="6bccf-275">Install Server 2016 on new machine and name it the same machine name as the original Azure Backup server.</span></span>
4) <span data-ttu-id="6bccf-276">Присоединитесь к домену.</span><span class="sxs-lookup"><span data-stu-id="6bccf-276">Join the Domain</span></span>
5) <span data-ttu-id="6bccf-277">Установите Azure Backup Server V2 (переместите диски пула хранилища DPM со старого сервера и выполните импорт).</span><span class="sxs-lookup"><span data-stu-id="6bccf-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="6bccf-278">Восстановите DPMDB, полученную в конце части 2.</span><span class="sxs-lookup"><span data-stu-id="6bccf-278">Restore the DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="6bccf-279">Подключите хранилища из исходного сервера Backup Server к новому серверу.</span><span class="sxs-lookup"><span data-stu-id="6bccf-279">Attach the storage from the original backup server to the new server.</span></span>
8) <span data-ttu-id="6bccf-280">Из SQL восстановите DPMDB.</span><span class="sxs-lookup"><span data-stu-id="6bccf-280">From SQL Restore the DPMDB</span></span>
9) <span data-ttu-id="6bccf-281">Из командной строки администратора на компакт-диске нового сервера в Microsoft Azure Backup установите расположение и папку bin.</span><span class="sxs-lookup"><span data-stu-id="6bccf-281">From admin command line on new server cd to Microsoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="6bccf-282">Пример пути: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="6bccf-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="6bccf-283">В Azure Backup выполните команду DPMSYNC-SYNC.</span><span class="sxs-lookup"><span data-stu-id="6bccf-283">to Azure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="6bccf-284">Выполните команду DPMSYNC-SYNC. Примечание. При добавлении новых дисков в пул хранилища DPM вместо перемещения старых дисков выполните команду DPMSYNC - Reallocatereplica.</span><span class="sxs-lookup"><span data-stu-id="6bccf-284">Run DPMSYNC -SYNC Note If you have added NEW disks to the DPM Storage pool instead of moving the old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="6bccf-285">Новые командлеты PowerShell в версии 2</span><span class="sxs-lookup"><span data-stu-id="6bccf-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="6bccf-286">При установке Azure Backup Server версии 2 доступны два новых командлета:</span><span class="sxs-lookup"><span data-stu-id="6bccf-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* <span data-ttu-id="6bccf-287">[Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx);</span><span class="sxs-lookup"><span data-stu-id="6bccf-287">[Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)</span></span>
* <span data-ttu-id="6bccf-288">[Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bccf-288">[Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bccf-289">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6bccf-289">Next steps</span></span>

<span data-ttu-id="6bccf-290">Узнайте, как подготовить сервер или обеспечить защиту рабочей нагрузки:</span><span class="sxs-lookup"><span data-stu-id="6bccf-290">Learn how to prepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="6bccf-291">Подготовка к резервному копированию рабочих нагрузок с использованием Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="6bccf-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="6bccf-292">Резервное копирование сервера VMware в Azure</span><span class="sxs-lookup"><span data-stu-id="6bccf-292">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="6bccf-293">Архивация баз данных SQL Server в Azure с помощью Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="6bccf-293">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- <span data-ttu-id="6bccf-294">[Add storage to Azure Backup Server v2](backup-mabs-add-storage.md) (Добавление хранилища к Azure Backup Server версии 2)</span><span class="sxs-lookup"><span data-stu-id="6bccf-294">[Use Modern Backup Storage with Backup Server](backup-mabs-add-storage.md)</span></span>

