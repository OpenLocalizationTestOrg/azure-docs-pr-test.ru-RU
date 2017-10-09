
<span data-ttu-id="0aec8-101">Дополнительные сведения о дисках см. в разделе [О дисках и виртуальных жестких дисках для виртуальных машин Azure](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0aec8-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="0aec8-102">Подключение пустого диска</span><span class="sxs-lookup"><span data-stu-id="0aec8-102">Attach an empty disk</span></span>
1. <span data-ttu-id="0aec8-103">Откройте Azure CLI 1.0 и [подключения tooyour подписки Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0aec8-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="0aec8-104">Убедитесь, что вы находитесь в режиме управления службами Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="0aec8-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="0aec8-105">Введите `azure vm disk attach-new` toocreate и присоединить новый диск, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="0aec8-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="0aec8-106">Замените *myVM* с именем hello вашей виртуальной машины Linux и укажите размер hello hello диска в ГБ, что является *100 ГБ* в этом примере:</span><span class="sxs-lookup"><span data-stu-id="0aec8-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="0aec8-107">После создания и присоединенного диска данных hello, это отображается в выходных данных hello `azure vm disk list <virtual-machine-name>` как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="0aec8-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="0aec8-108">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="0aec8-108">hello output is similar toohello following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="0aec8-109">Подключение существующего диска</span><span class="sxs-lookup"><span data-stu-id="0aec8-109">Attach an existing disk</span></span>
<span data-ttu-id="0aec8-110">Для подключения существующего диска требуется VHD-файл в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0aec8-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="0aec8-111">Откройте Azure CLI 1.0 и [подключения tooyour подписки Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0aec8-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="0aec8-112">Убедитесь, что вы находитесь в режиме управления службами Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="0aec8-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="0aec8-113">Проверьте, если hello VHD, вы хотите tooattach уже отправлен tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="0aec8-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="0aec8-114">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="0aec8-114">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="0aec8-115">Если не удается найти диск hello, требуется toouse, локальные подписки tooyour виртуального жесткого диска может быть отправлен с помощью `azure vm disk create` или `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="0aec8-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="0aec8-116">Пример `disk create` бы как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="0aec8-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="0aec8-117">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="0aec8-117">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="0aec8-118">Можно также использовать `azure vm disk upload` tooupload VHD tooa конкретной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0aec8-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="0aec8-119">Прочитать больше о hello команды toomanage диски данных Azure виртуальной машины [здесь](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="0aec8-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="0aec8-120">Теперь можно присоединить hello требуемого VHD tooyour виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="0aec8-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="0aec8-121">Убедитесь, что tooreplace *myVM* с именем hello вашей виртуальной машины и *myVHD* с вашего нужного виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="0aec8-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="0aec8-122">Вы можете проверить диск hello вложенного toohello виртуальную машину с `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="0aec8-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="0aec8-123">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="0aec8-123">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="0aec8-124">После добавления диска данных и вы перейдете требуется toolog на виртуальной машине toohello инициализировать диск hello hello виртуальная машина может использовать hello диска для хранения данных (см. шаги hello следующие дополнительные сведения на toodo инициализация диска hello).</span><span class="sxs-lookup"><span data-stu-id="0aec8-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 

