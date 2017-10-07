---
title: "aaaAttach tooa диска виртуальной Машины Linux в Azure | Документы Microsoft"
description: "Узнайте, как tooattach данных на диске tooa виртуальных Машин Linux с помощью hello классического развертывания модели и инициализируется hello диск, поэтому он будет готов к использованию"
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
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="af81f-103">Как tooAttach tooa диска данных виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="af81f-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="af81f-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="af81f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="af81f-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="af81f-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="af81f-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="af81f-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="af81f-107">В разделе как слишком[присоединить диск данных с помощью модели развертывания диспетчера ресурсов hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af81f-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="af81f-108">Можно присоединить пустые диски и диски, содержащие данные tooyour виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="af81f-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="af81f-109">В обоих случаях диски — это VHD-файлы, которые размещаются в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="af81f-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="af81f-110">Как и при добавлении любой компьютер Linux tooa диска после присоединения диска hello требуется tooinitialize и отформатировать его, поэтому он будет готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="af81f-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="af81f-111">Этой статьи описаны присоединении пустые диски и диски, уже содержащий данных tooyour виртуальные машины, а также как toothen инициализация и форматирование нового диска.</span><span class="sxs-lookup"><span data-stu-id="af81f-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="af81f-112">Это лучший подход toouse, один или несколько разделения toostore дисков данных виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="af81f-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="af81f-113">При создании виртуальной машины Azure у нее есть диск для операционной системы и временный диск.</span><span class="sxs-lookup"><span data-stu-id="af81f-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="af81f-114">**Не используйте hello временный диск toostore постоянных данных.**</span><span class="sxs-lookup"><span data-stu-id="af81f-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="af81f-115">Как hello названия, он предоставляет только временное хранилище.</span><span class="sxs-lookup"><span data-stu-id="af81f-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="af81f-116">Этот диск не обеспечивает избыточности или резервного копирования, поскольку он не размещается в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="af81f-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="af81f-117">временный диск Hello обычно управляется hello Azure Linux Agent и автоматическое подключение слишком**/mnt/resource** (или **/mnt** Ubuntu изображений).</span><span class="sxs-lookup"><span data-stu-id="af81f-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="af81f-118">На Здравствуйте другой стороны, диск данных может называться ядре Linux hello примерно `/dev/sdc`, и необходимо toopartition, форматирования и подключить этот ресурс.</span><span class="sxs-lookup"><span data-stu-id="af81f-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="af81f-119">В разделе hello [руководство пользователя агента Azure Linux] [ Agent] подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="af81f-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="af81f-120">Инициализация нового диска данных в Linux</span><span class="sxs-lookup"><span data-stu-id="af81f-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="af81f-121">Tooyour SSH виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="af81f-121">SSH tooyour VM.</span></span> <span data-ttu-id="af81f-122">Дополнительные сведения см. в разделе [как toolog на tooa виртуальной машине под управлением Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="af81f-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="af81f-123">Затем следует записать идентификатор устройства hello toofind для tooinitialize диска данных hello.</span><span class="sxs-lookup"><span data-stu-id="af81f-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="af81f-124">Существует два способа toodo:</span><span class="sxs-lookup"><span data-stu-id="af81f-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="af81f-125">) Grep для устройств SCSI в hello записывает в журнал, например, как hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="af81f-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="af81f-126">Для последних Ubuntu распределений, может потребоваться toouse `sudo grep SCSI /var/log/syslog` так, как ведение журнала слишком`/var/log/messages` могут быть отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="af81f-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="af81f-127">Можно определить идентификатор hello hello последний диск, который был добавлен в отображаемые сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="af81f-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Получение сообщений hello диска](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="af81f-129">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="af81f-129">OR</span></span>
   
    <span data-ttu-id="af81f-130">b) используйте hello `lsscsi` toofind команду out hello идентификатор устройства. `lsscsi` можно установить с помощью `yum install lsscsi` (Red Hat в основе распределения) или `apt-get install lsscsi` (Debian в основе распределения).</span><span class="sxs-lookup"><span data-stu-id="af81f-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="af81f-131">Можно найти диск hello, вы ищете, его *lun* или **логический номер устройства**.</span><span class="sxs-lookup"><span data-stu-id="af81f-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="af81f-132">Например, hello *lun* для hello дисков вы можете легко увидеть из `azure vm disk list <virtual-machine>` как:</span><span class="sxs-lookup"><span data-stu-id="af81f-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="af81f-133">Hello выходные данные выглядят аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="af81f-133">hello output is similar toohello following:</span></span>

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
   
    <span data-ttu-id="af81f-134">Сравнение этих данных с помощью hello выходные данные `lsscsi` hello же образцы виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="af81f-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="af81f-135">Номер последней Hello в кортеже hello в каждой строке — hello *lun*.</span><span class="sxs-lookup"><span data-stu-id="af81f-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="af81f-136">Дополнительные сведения см. в `man lsscsi`.</span><span class="sxs-lookup"><span data-stu-id="af81f-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="af81f-137">В строке приветствия типа hello следующая команда toocreate устройства:</span><span class="sxs-lookup"><span data-stu-id="af81f-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="af81f-138">При появлении запроса введите  **n**  toocreate секции.</span><span class="sxs-lookup"><span data-stu-id="af81f-138">When prompted, type **n** toocreate a partition.</span></span>

    ![Создание устройства](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="af81f-140">При появлении запроса введите **p** toomake hello секции hello основного раздела.</span><span class="sxs-lookup"><span data-stu-id="af81f-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="af81f-141">Тип **1** toomake его hello первую секцию, а затем введите введите значение по умолчанию hello tooaccept цилиндр hello.</span><span class="sxs-lookup"><span data-stu-id="af81f-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="af81f-142">В некоторых системах можно отображать значения по умолчанию hello hello первым и hello последнего секторов, вместо цилиндр hello.</span><span class="sxs-lookup"><span data-stu-id="af81f-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="af81f-143">Вы можете tooaccept эти значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="af81f-143">You can choose tooaccept these defaults.</span></span>

    ![Создание раздела](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="af81f-145">Тип **p** toosee hello сведения о диске hello, во время разбиения.</span><span class="sxs-lookup"><span data-stu-id="af81f-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![Просмотр сведений о диске](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="af81f-147">Тип **w** toowrite параметрах hello hello диска.</span><span class="sxs-lookup"><span data-stu-id="af81f-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Запись изменений на дисках hello](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="af81f-149">Теперь можно создавать на новую секцию hello hello файловой системы.</span><span class="sxs-lookup"><span data-stu-id="af81f-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="af81f-150">Добавьте код номеров устройства toohello hello секции (в следующий пример hello `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="af81f-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="af81f-151">Hello следующий пример создает ext4 раздел на /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="af81f-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Создание файловой системы](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="af81f-153">Системы SuSE Linux Enterprise 11 поддерживают доступ только для чтения в файловых системах ext4.</span><span class="sxs-lookup"><span data-stu-id="af81f-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="af81f-154">Для этих систем рекомендуется tooformat hello новая файловая система ext3 вместо ext4.</span><span class="sxs-lookup"><span data-stu-id="af81f-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="af81f-155">Сделайте каталог toomount hello новая файловая система, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="af81f-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="af81f-156">Наконец можно подключить диск hello, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="af81f-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="af81f-157">Hello диск данных становится готова toouse как **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="af81f-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Создать диск hello hello каталога и подключения](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="af81f-159">Добавьте hello нового диска слишком/и т. д/fstab:</span><span class="sxs-lookup"><span data-stu-id="af81f-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="af81f-160">tooensure hello диск будет подключена снова автоматически, после перезагрузки, он должен быть добавлен файл/etc/fstab toohello.</span><span class="sxs-lookup"><span data-stu-id="af81f-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="af81f-161">Кроме того настоятельно рекомендуется этого hello UUID (глобально уникальный идентификатор) используется в/etc/fstab toorefer toohello диск, а не просто имя (т. е. /dev/sdc1) устройства hello.</span><span class="sxs-lookup"><span data-stu-id="af81f-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="af81f-162">Использование hello UUID позволяет избежать hello неправильной диска, подключенного tooa заданное место в случае, если hello ОС обнаружении ошибки во время загрузки и все остальные диски с данными, затем назначено их идентификаторы устройств.</span><span class="sxs-lookup"><span data-stu-id="af81f-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="af81f-163">toofind Здравствуйте UUID hello новый диск, можно использовать hello **блок идентификатором blkid** программы:</span><span class="sxs-lookup"><span data-stu-id="af81f-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="af81f-164">Hello выходные данные выглядят аналогично toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="af81f-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="af81f-165">Неправильное редактирование hello **/etc/fstab** файла может привести к невозможности загрузки системы.</span><span class="sxs-lookup"><span data-stu-id="af81f-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="af81f-166">Если нет уверенности, сведения о этот файл, как изменять tooproperly см toohello распространения документации.</span><span class="sxs-lookup"><span data-stu-id="af81f-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="af81f-167">Также рекомендуется, прежде чем изменять создается резервная копия файл/etc/fstab hello.</span><span class="sxs-lookup"><span data-stu-id="af81f-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="af81f-168">Затем откройте hello **/etc/fstab** файл в текстовом редакторе:</span><span class="sxs-lookup"><span data-stu-id="af81f-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="af81f-169">В этом примере мы используем значение hello UUID для hello новый **/dev/sdc1** устройства, который был создан в предыдущих шагах hello и hello монтирования **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="af81f-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="af81f-170">Добавьте следующие строки toohello конец hello hello **/etc/fstab** файла:</span><span class="sxs-lookup"><span data-stu-id="af81f-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="af81f-171">Или в системах на базе ОС SuSE Linux, может потребоваться toouse немного другой формат:</span><span class="sxs-lookup"><span data-stu-id="af81f-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="af81f-172">Hello `nofail` параметр гарантирует, что hello, Виртуальная машина, даже если hello файловой системы повреждены или hello диск не существует во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="af81f-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="af81f-173">Без этого параметра могут возникнуть поведение, как описано в [нельзя SSH tooLinux виртуальной Машины из-за ошибки tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="af81f-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="af81f-174">Теперь можно проверить, что подключено hello файловой системе надлежащим образом отключением и затем снова подключать hello файловой системы, т. е. При использовании точки подключения пример hello `/datadrive` в hello ранее шаги:</span><span class="sxs-lookup"><span data-stu-id="af81f-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="af81f-175">Если hello `mount` команда выведет сообщение об ошибке, проверьте hello файле/etc/fstab для правильного синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="af81f-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="af81f-176">При создании дополнительных дисков данных и разделов также введите их в файл /etc/fstab отдельно.</span><span class="sxs-lookup"><span data-stu-id="af81f-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="af81f-177">Сделать доступным для записи hello диска с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="af81f-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="af81f-178">Впоследствии удалении диска данных без необходимости редактирования fstab может привести к tooboot toofail hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="af81f-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="af81f-179">Если это обычное дело большинством дистрибутивов предоставляют либо hello `nofail` и/или `nobootwait` fstab параметры, позволяющие tooboot системы даже в случае сбоя диска hello toomount во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="af81f-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="af81f-180">Дополнительные сведения об этих параметрах см. в документации дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="af81f-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="af81f-181">Поддержка операций TRIM и UNMAP для Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="af81f-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="af81f-182">Некоторые версии Linux ядра поддержки TRIM и отмене СОПОСТАВЛЕНИЯ операций toodiscard неиспользуемые блоки на диске hello.</span><span class="sxs-lookup"><span data-stu-id="af81f-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="af81f-183">Эти операции, в первую очередь используются в tooinform стандартное хранилище Azure, которая удалена страницы становятся недействительными и может быть удален.</span><span class="sxs-lookup"><span data-stu-id="af81f-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="af81f-184">Удаление страниц позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="af81f-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="af81f-185">Существует два способа tooenable TRIM поддержки в ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="af81f-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="af81f-186">Как обычно см. на распределение hello рекомендованный подход:</span><span class="sxs-lookup"><span data-stu-id="af81f-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="af81f-187">Используйте hello `discard` подключить параметр в `/etc/fstab`, например:</span><span class="sxs-lookup"><span data-stu-id="af81f-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="af81f-188">В некоторых случаях hello `discard` параметра может негативно сказаться на производительности.</span><span class="sxs-lookup"><span data-stu-id="af81f-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="af81f-189">Кроме того, можно запустить hello `fstrim` вручную команды из командной строки hello, или добавьте его tooyour crontab toorun регулярно:</span><span class="sxs-lookup"><span data-stu-id="af81f-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="af81f-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="af81f-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="af81f-191">**RHEL или CentOS**</span><span class="sxs-lookup"><span data-stu-id="af81f-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="af81f-192">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="af81f-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="af81f-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af81f-193">Next Steps</span></span>
<span data-ttu-id="af81f-194">Можно прочитать подробнее об использовании ВМ Linux в hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="af81f-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="af81f-195">[Как toolog на tooa виртуальной машине под управлением Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="af81f-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="af81f-196">Как toodetach диск от виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="af81f-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="af81f-197">С помощью Azure CLI hello hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="af81f-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="af81f-198">Настройка программного RAID-массива в Linux</span><span class="sxs-lookup"><span data-stu-id="af81f-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="af81f-199">Настройка диспетчера логических томов на виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="af81f-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
