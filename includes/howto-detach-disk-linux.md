<span data-ttu-id="b8c07-101">Если вам больше не требуется диск, который является вложенного tooa виртуальной машины (VM), можно легко отключить ее.</span><span class="sxs-lookup"><span data-stu-id="b8c07-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="b8c07-102">При отсоединении диска от виртуальной Машины hello hello диск не удалено из хранилища.</span><span class="sxs-lookup"><span data-stu-id="b8c07-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="b8c07-103">Если требуется toouse hello существующие данные на диске hello, вам может быть повторно присоединена toohello одной виртуальной Машины, так и любой другой.</span><span class="sxs-lookup"><span data-stu-id="b8c07-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="b8c07-104">Виртуальная машина в Azure использует различные типы дисков, такие как диск с операционной системой, локальный временный диск и дополнительные диски данных.</span><span class="sxs-lookup"><span data-stu-id="b8c07-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="b8c07-105">Дополнительные сведения см. в статье [О дисках и виртуальных жестких дисках для виртуальных машин Azure](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b8c07-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b8c07-106">Невозможно отсоединить диск операционной системы, пока не будут также удалены hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b8c07-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="b8c07-107">Найти диск hello</span><span class="sxs-lookup"><span data-stu-id="b8c07-107">Find hello disk</span></span>
<span data-ttu-id="b8c07-108">Перед тем как отсоединить диск от виртуальной Машины необходимо toofind out hello номер LUN, который является идентификатор hello диск toobe отсоединена.</span><span class="sxs-lookup"><span data-stu-id="b8c07-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="b8c07-109">toodo, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b8c07-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="b8c07-110">Откройте Azure CLI и [подключения tooyour подписки Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b8c07-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="b8c07-111">Убедитесь, что вы находитесь в режиме управления службами Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="b8c07-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="b8c07-112">Узнайте, какие диски, присоединенные tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b8c07-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="b8c07-113">Hello следующий пример выводит диски для виртуальной Машины с именем hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="b8c07-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="b8c07-114">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="b8c07-114">hello output is similar toohello following example:</span></span>

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. <span data-ttu-id="b8c07-115">Обратите внимание, hello LUN или hello **логический номер устройства** для нужных toodetach диска hello.</span><span class="sxs-lookup"><span data-stu-id="b8c07-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="b8c07-116">Удалите диск toohello ссылки операционной системы</span><span class="sxs-lookup"><span data-stu-id="b8c07-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="b8c07-117">Перед отсоединением hello диск от виртуальной машине Linux hello, следует убедиться, что все разделы на диске hello не используются.</span><span class="sxs-lookup"><span data-stu-id="b8c07-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="b8c07-118">Убедитесь в этой операционной системе и hello не пытаться tooremount их после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="b8c07-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="b8c07-119">Эти действия отменить конфигурации hello, скорее всего, созданной при [присоединение](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello диска.</span><span class="sxs-lookup"><span data-stu-id="b8c07-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="b8c07-120">Используйте hello `lsscsi` идентификатор диска hello toodiscover команды.</span><span class="sxs-lookup"><span data-stu-id="b8c07-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="b8c07-121">Вы можете установить `lsscsi` с помощью `yum install lsscsi` (в дистрибутивах на основе Red Hat) или `apt-get install lsscsi` (в дистрибутивах на основе Debian).</span><span class="sxs-lookup"><span data-stu-id="b8c07-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="b8c07-122">Можно найти идентификатор hello диска, который вы ищете, используя номер LUN hello.</span><span class="sxs-lookup"><span data-stu-id="b8c07-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="b8c07-123">Номер последней Hello в кортеже hello в каждой строке — hello LUN.</span><span class="sxs-lookup"><span data-stu-id="b8c07-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="b8c07-124">В следующий пример из hello `lsscsi`, LUN 0 соответствует слишком*иметь идентификатор/dev/sdc*</span><span class="sxs-lookup"><span data-stu-id="b8c07-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="b8c07-125">Используйте `fdisk -l <disk>` toodiscover hello секций, связанных с toobe диска hello отсоединена.</span><span class="sxs-lookup"><span data-stu-id="b8c07-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="b8c07-126">Hello следующий пример показывает hello выходные `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="b8c07-126">hello following example shows hello output for `/dev/sdc`:</span></span>

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. <span data-ttu-id="b8c07-127">Отключите каждой секции, перечисленные для hello диска.</span><span class="sxs-lookup"><span data-stu-id="b8c07-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="b8c07-128">Hello следующий пример отсоединяет диск `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="b8c07-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="b8c07-129">Используйте hello `blkid` команда toodiscovery hello UUID для всех секций.</span><span class="sxs-lookup"><span data-stu-id="b8c07-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="b8c07-130">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="b8c07-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="b8c07-131">Удалить записи из hello **/etc/fstab** файла, связанного с путей hello устройств или UUID для всех секций, toobe диск hello отсоединена.</span><span class="sxs-lookup"><span data-stu-id="b8c07-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="b8c07-132">Записи в этом примере могут быть такими:</span><span class="sxs-lookup"><span data-stu-id="b8c07-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="b8c07-133">или</span><span class="sxs-lookup"><span data-stu-id="b8c07-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="b8c07-134">Отсоединить диск hello</span><span class="sxs-lookup"><span data-stu-id="b8c07-134">Detach hello disk</span></span>
<span data-ttu-id="b8c07-135">Обнаружив hello номера LUN дисковых hello и ссылки на удаленные hello операционной системы, вы будете готовы toodetach его:</span><span class="sxs-lookup"><span data-stu-id="b8c07-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="b8c07-136">Отсоединение hello выбранный диск из виртуальной машины hello, выполнив команду hello `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="b8c07-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="b8c07-137">Hello следующий пример отсоединяет LUN `0` из виртуальной Машины с именем hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="b8c07-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="b8c07-138">Можно проверить, если диск hello получен отсоединяется, запустив `azure vm disk list` еще раз.</span><span class="sxs-lookup"><span data-stu-id="b8c07-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="b8c07-139">Следующий пример проверяет Hello hello виртуальной Машины с именем `myVM`:</span><span class="sxs-lookup"><span data-stu-id="b8c07-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="b8c07-140">Hello выходных данных примерно toohello следующий пример, в котором показано, что диск hello данных больше не подключен:</span><span class="sxs-lookup"><span data-stu-id="b8c07-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

<span data-ttu-id="b8c07-141">Hello отсоединить диск остается в хранилище, но больше не является tooa подключенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b8c07-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

