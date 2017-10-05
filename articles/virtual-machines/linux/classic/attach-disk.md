---
title: "Подключение диска к виртуальной машине Linux в Azure | Документация Майкрософт"
description: "Узнайте, как подключить диск данных к виртуальной машине Linux, используя классическую модель развертывания, и инициализировать его, чтобы подготовить к использованию."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 017ba7197e11c2b222082833d5acabb9e542b762
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-virtual-machine"></a><span data-ttu-id="c760a-103">Подключение диска данных к виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="c760a-103">How to Attach a Data Disk to a Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="c760a-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c760a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c760a-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="c760a-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c760a-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c760a-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c760a-107">См. статью о том, как [присоединить диск данных, используя модель развертывания с помощью Resource Manager](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c760a-107">See how to [attach a data disk using the Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c760a-108">К виртуальным машинам Azure можно присоединять пустые диски и диски с данными.</span><span class="sxs-lookup"><span data-stu-id="c760a-108">You can attach both empty disks and disks that contain data to your Azure VMs.</span></span> <span data-ttu-id="c760a-109">В обоих случаях диски — это VHD-файлы, которые размещаются в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="c760a-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="c760a-110">Как и при добавлении диска к машине Linux, после присоединения диск нужно инициализировать и отформатировать, чтобы подготовить его к использованию.</span><span class="sxs-lookup"><span data-stu-id="c760a-110">As with adding any disk to a Linux machine, after you attach the disk you need to initialize and format it so it's ready for use.</span></span> <span data-ttu-id="c760a-111">В этой статье подробно описывается присоединение пустых дисков и дисков с данными к виртуальным машинам, а также рассматривается, как затем инициализировать и отформатировать новый диск.</span><span class="sxs-lookup"><span data-stu-id="c760a-111">This article details attaching both empty disks and disks already containing data to your VMs, as well as how to then initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="c760a-112">Рекомендуется использовать один или несколько отдельных дисков для хранения данных виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c760a-112">It's a best practice to use one or more separate disks to store a virtual machine's data.</span></span> <span data-ttu-id="c760a-113">При создании виртуальной машины Azure у нее есть диск для операционной системы и временный диск.</span><span class="sxs-lookup"><span data-stu-id="c760a-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="c760a-114">**Не используйте для постоянного хранения данных временный диск.**</span><span class="sxs-lookup"><span data-stu-id="c760a-114">**Do not use the temporary disk to store persistent data.**</span></span> <span data-ttu-id="c760a-115">Как и предполагает его имя, он предназначен только для временного хранения.</span><span class="sxs-lookup"><span data-stu-id="c760a-115">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="c760a-116">Этот диск не обеспечивает избыточности или резервного копирования, поскольку он не размещается в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="c760a-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="c760a-117">Временный диск обычно управляется агентом Azure для Linux и автоматически подключается к **/mnt/resource** (или **/mnt** в образах Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c760a-117">The temporary disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="c760a-118">Однако в некоторых случаях диск данных может получить от ядра Linux обозначение вида `/dev/sdc`, и тогда вам необходимо самостоятельно разделить, отформатировать и подключить этот ресурс.</span><span class="sxs-lookup"><span data-stu-id="c760a-118">On the other hand, a data disk might be named by the Linux kernel something like `/dev/sdc`, and you need to partition, format, and mount this resource.</span></span> <span data-ttu-id="c760a-119">Дополнительные сведения см. в [руководстве пользователя агента Linux для Azure][Agent].</span><span class="sxs-lookup"><span data-stu-id="c760a-119">See the [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="c760a-120">Инициализация нового диска данных в Linux</span><span class="sxs-lookup"><span data-stu-id="c760a-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="c760a-121">Установите SSH-подключение к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c760a-121">SSH to your VM.</span></span> <span data-ttu-id="c760a-122">Дополнительные сведения см. в статье [Создание пары из открытого и закрытого ключей SSH для виртуальных машин Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="c760a-122">For more information, see [How to log on to a virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="c760a-123">Далее вам необходимо найти идентификатор устройства для инициализации диска данных.</span><span class="sxs-lookup"><span data-stu-id="c760a-123">Next you need to find the device identifier for the data disk to initialize.</span></span> <span data-ttu-id="c760a-124">Это можно осуществить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="c760a-124">There are two ways to do that:</span></span>
   
    <span data-ttu-id="c760a-125">а) примените функцию grep для устройств SCSI в журналах, например, как в следующей команде:</span><span class="sxs-lookup"><span data-stu-id="c760a-125">a) Grep for SCSI devices in the logs, such as in the following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="c760a-126">Для установки последних дистрибутивов Ubuntu вам может потребоваться использовать `sudo grep SCSI /var/log/syslog`, так как вход в `/var/log/messages` может быть отключен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c760a-126">For recent Ubuntu distributions, you may need to use `sudo grep SCSI /var/log/syslog` because logging to `/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="c760a-127">Идентификатор последнего добавленного диска данных можно найти в отображаемых сообщениях.</span><span class="sxs-lookup"><span data-stu-id="c760a-127">You can find the identifier of the last data disk that was added in the messages that are displayed.</span></span>
   
    ![Получение сообщений диска](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="c760a-129">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="c760a-129">OR</span></span>
   
    <span data-ttu-id="c760a-130">б) Используйте команду `lsscsi` , чтобы узнать идентификатор устройства.</span><span class="sxs-lookup"><span data-stu-id="c760a-130">b) Use the `lsscsi` command to find out the device id.</span></span> <span data-ttu-id="c760a-131">Вы можете установить `lsscsi` с помощью `yum install lsscsi` (в дистрибутивах на основе Red Hat) или `apt-get install lsscsi` (в дистрибутивах на основе Debian).</span><span class="sxs-lookup"><span data-stu-id="c760a-131">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="c760a-132">Нужный вам диск вы можете найти по его *LUN* ( **логическому номеру устройства**).</span><span class="sxs-lookup"><span data-stu-id="c760a-132">You can find the disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="c760a-133">Например, для подключенных вами дисков *LUN* можно легко получить, выполнив команду `azure vm disk list <virtual-machine>`.</span><span class="sxs-lookup"><span data-stu-id="c760a-133">For example, the *lun* for the disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="c760a-134">Выход аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="c760a-134">The output is similar to the following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="c760a-135">Сравните эти данные с выводом команды `lsscsi` для той же виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c760a-135">Compare this data with the output of `lsscsi` for the same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="c760a-136">Последний номер в кортеже в каждой строке и есть номер *LUN*.</span><span class="sxs-lookup"><span data-stu-id="c760a-136">The last number in the tuple in each row is the *lun*.</span></span> <span data-ttu-id="c760a-137">Дополнительные сведения см. в `man lsscsi`.</span><span class="sxs-lookup"><span data-stu-id="c760a-137">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="c760a-138">В командной строке введите следующую команду, чтобы создать устройство:</span><span class="sxs-lookup"><span data-stu-id="c760a-138">At the prompt, type the following command to create your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="c760a-139">При появлении запроса введите  **n**  для создания секции.</span><span class="sxs-lookup"><span data-stu-id="c760a-139">When prompted, type **n** to create a partition.</span></span>

    ![Создание устройства](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="c760a-141">При появлении запроса введите **p** , чтобы сделать раздел основным (primary).</span><span class="sxs-lookup"><span data-stu-id="c760a-141">When prompted, type **p** to make the partition the primary partition.</span></span> <span data-ttu-id="c760a-142">Введите **1** , чтобы сделать его первым разделом, а затем нажмите клавишу ВВОД, чтобы принять значение по умолчанию для цилиндра.</span><span class="sxs-lookup"><span data-stu-id="c760a-142">Type **1** to make it the first partition, and then type enter to accept the default value for the cylinder.</span></span> <span data-ttu-id="c760a-143">В некоторых системах в первом и последнем секторах вместо цилиндра могут отображаться значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c760a-143">On some systems, it can show the default values of the first and the last sectors, instead of the cylinder.</span></span> <span data-ttu-id="c760a-144">При желании вы можете их принять.</span><span class="sxs-lookup"><span data-stu-id="c760a-144">You can choose to accept these defaults.</span></span>

    ![Создание раздела](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="c760a-146">Введите **p** , чтобы просмотреть сведения о диске, на котором создаются разделы.</span><span class="sxs-lookup"><span data-stu-id="c760a-146">Type **p** to see the details about the disk that is being partitioned.</span></span>

    ![Просмотр сведений о диске](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="c760a-148">Введите **w** , чтобы записать параметры данного диска.</span><span class="sxs-lookup"><span data-stu-id="c760a-148">Type **w** to write the settings for the disk.</span></span>

    ![Запись изменений на диске](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="c760a-150">Теперь можно создать файловую систему в новом разделе.</span><span class="sxs-lookup"><span data-stu-id="c760a-150">Now you can create the file system on the new partition.</span></span> <span data-ttu-id="c760a-151">Добавьте номер раздела в код устройства (в примере ниже это `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="c760a-151">Append the partition number to the device ID (in the following example `/dev/sdc1`).</span></span> <span data-ttu-id="c760a-152">В следующем примере создается раздел ext4 в устройстве /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="c760a-152">The following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Создание файловой системы](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="c760a-154">Системы SuSE Linux Enterprise 11 поддерживают доступ только для чтения в файловых системах ext4.</span><span class="sxs-lookup"><span data-stu-id="c760a-154">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="c760a-155">Для этих систем рекомендуется форматировать новую файловую систему как ext3, а не ext4.</span><span class="sxs-lookup"><span data-stu-id="c760a-155">For these systems, it is recommended to format the new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="c760a-156">Создайте каталог для подключения новой файловой системы с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="c760a-156">Make a directory to mount the new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="c760a-157">Теперь вы можете подключить диск с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="c760a-157">Finally you can mount the drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="c760a-158">Диск данных теперь готов для использования как **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="c760a-158">The data disk is now ready to use as **/datadrive**.</span></span>
   
    ![Создание каталога и подключение диска](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="c760a-160">Добавьте новый диск в /etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="c760a-160">Add the new drive to /etc/fstab:</span></span>
   
    <span data-ttu-id="c760a-161">Чтобы обеспечить автоматическое повторное подключение диска после перезагрузки, его необходимо добавить в файл /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="c760a-161">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="c760a-162">Кроме того, для ссылки на диск настоятельно рекомендуется использовать идентификатор UUID (глобально уникальный идентификатор) в /etc/fstab, а не просто имя устройства (т. е. /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="c760a-162">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="c760a-163">Использование идентификатора UUID позволяет избежать подключения неправильного диска к нужному расположению, если операционная система обнаруживает сбой диска во время загрузки, а остальные диски с данными связываются с этими идентификаторами устройств.</span><span class="sxs-lookup"><span data-stu-id="c760a-163">Using the UUID avoids the incorrect disk being mounted to a given location if the OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="c760a-164">Чтобы найти идентификатор UUID нового диска, можно использовать служебную программу **blkid**:</span><span class="sxs-lookup"><span data-stu-id="c760a-164">To find the UUID of the new drive, you can use the **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="c760a-165">Результат должен быть аналогичным приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="c760a-165">The output looks similar to the following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="c760a-166">Некорректное изменение файла **/etc/fstab** может привести к невозможности загрузить систему.</span><span class="sxs-lookup"><span data-stu-id="c760a-166">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="c760a-167">Если у вас есть сомнения, см. инструкции по правильному изменению этого файла в документации дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="c760a-167">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="c760a-168">Также рекомендуется перед внесением изменений создать резервную копию файла /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="c760a-168">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="c760a-169">Затем откройте файл **/etc/fstab** в текстовом редакторе:</span><span class="sxs-lookup"><span data-stu-id="c760a-169">Next, open the **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="c760a-170">В этом примере мы используем значение UUID для нового устройства **/dev/sdc1**, созданного на предыдущих шагах, и точку подключения **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="c760a-170">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="c760a-171">Добавьте следующую строку в конец файла **/etc/fstab** :</span><span class="sxs-lookup"><span data-stu-id="c760a-171">Add the following line to the end of the **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="c760a-172">В системах на базе SUSE Linux может потребоваться использовать другой формат:</span><span class="sxs-lookup"><span data-stu-id="c760a-172">Or, on systems based on SuSE Linux you may need to use a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="c760a-173">Параметр `nofail` гарантирует, что виртуальная машина запустится, даже если файловая система повреждена или отсутствует диск во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="c760a-173">The `nofail` option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="c760a-174">Без этого параметра может возникнуть ситуация, описанная в записи блога [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/) (Не удается подключиться к виртуальной машине Linux по протоколу SSH из-за ошибок FSTAB).</span><span class="sxs-lookup"><span data-stu-id="c760a-174">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="c760a-175">Теперь можно проверить, правильно ли подключена файловая система, отключив и повторно подключив файловую систему, т. е.</span><span class="sxs-lookup"><span data-stu-id="c760a-175">You can now test that the file system is mounted properly by unmounting and then remounting the file system, i.e.</span></span> <span data-ttu-id="c760a-176">используя типовую точку подключения `/datadrive`, созданную на предыдущих этапах:</span><span class="sxs-lookup"><span data-stu-id="c760a-176">using the example mount point `/datadrive` created in the earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="c760a-177">Если команда `mount` приводит к ошибке, проверьте правильность синтаксиса в файле /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="c760a-177">If the `mount` command produces an error, check the /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="c760a-178">При создании дополнительных дисков данных и разделов также введите их в файл /etc/fstab отдельно.</span><span class="sxs-lookup"><span data-stu-id="c760a-178">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="c760a-179">Сделайте диск доступным для записи, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c760a-179">Make the drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="c760a-180">Последующее удаление диска данных без редактирования fstab может привести к тому, что виртуальная машина не загрузится.</span><span class="sxs-lookup"><span data-stu-id="c760a-180">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="c760a-181">Если это происходит часто, то большинство дистрибутивов предоставляют варианты `nofail` и/или `nobootwait` fstab, которые позволяют системе загружаться, даже если диск не подключается во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="c760a-181">If this is a common occurrence, most distributions provide either the `nofail` and/or `nobootwait` fstab options that allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="c760a-182">Дополнительные сведения об этих параметрах см. в документации дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="c760a-182">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="c760a-183">Поддержка операций TRIM и UNMAP для Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="c760a-183">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="c760a-184">Некоторые ядра Linux поддерживают операции TRIM и UNMAP для отмены неиспользуемых блоков на диске.</span><span class="sxs-lookup"><span data-stu-id="c760a-184">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="c760a-185">Эти операции особенно удобно использовать в хранилище уровня "Стандартный", чтобы сообщать Azure о том, что удаленные страницы больше не действительны и могут быть удалены.</span><span class="sxs-lookup"><span data-stu-id="c760a-185">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="c760a-186">Удаление страниц позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="c760a-186">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="c760a-187">Существует два способа включить поддержку операций TRIM в виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="c760a-187">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="c760a-188">Как обычно, обратитесь к документации дистрибутива, чтобы выбрать рекомендуемый метод.</span><span class="sxs-lookup"><span data-stu-id="c760a-188">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="c760a-189">Используйте параметр подключения `discard` в `/etc/fstab`. Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="c760a-189">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="c760a-190">В некоторых случаях параметр `discard` может негативно влиять на производительность.</span><span class="sxs-lookup"><span data-stu-id="c760a-190">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="c760a-191">Кроме того, вы можете вручную выполнить команду `fstrim` из командной строки или добавить ее в crontab для регулярного выполнения.</span><span class="sxs-lookup"><span data-stu-id="c760a-191">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="c760a-192">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="c760a-192">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="c760a-193">**RHEL или CentOS**</span><span class="sxs-lookup"><span data-stu-id="c760a-193">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="c760a-194">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="c760a-194">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="c760a-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c760a-195">Next Steps</span></span>
<span data-ttu-id="c760a-196">Узнать больше об использовании виртуальной машины Linux можно в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="c760a-196">You can read more about using your Linux VM in the following articles:</span></span>

* <span data-ttu-id="c760a-197">[Вход в виртуальную машину под управлением ОС Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="c760a-197">[How to log on to a virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="c760a-198">Отсоединение диска от виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="c760a-198">How to detach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="c760a-199">Команды Azure CLI в режиме управления службами Azure (ASM)</span><span class="sxs-lookup"><span data-stu-id="c760a-199">Using the Azure CLI with the Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="c760a-200">Настройка программного RAID-массива в Linux</span><span class="sxs-lookup"><span data-stu-id="c760a-200">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="c760a-201">Настройка диспетчера логических томов на виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="c760a-201">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
