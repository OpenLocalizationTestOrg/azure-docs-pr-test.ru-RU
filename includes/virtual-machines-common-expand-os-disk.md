## <a name="overview"></a><span data-ttu-id="340d2-101">Обзор</span><span class="sxs-lookup"><span data-stu-id="340d2-101">Overview</span></span>
<span data-ttu-id="340d2-102">При создании новой виртуальной машины (VM) в группе ресурсов путем развертывания образа с [Azure Marketplace](https://azure.microsoft.com/marketplace/), диск операционной системы по умолчанию hello составляет 127 ГБ.</span><span class="sxs-lookup"><span data-stu-id="340d2-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="340d2-103">Хотя это toohello диски данных возможно tooadd виртуальной Машины (сколько зависимости hello SKU вы выбрали) и более того, это рекомендуемые tooinstall приложений и рабочих нагрузок интенсивных ЦП на этих дисках приложение, зачастую пользователи должны hello tooexpand ОС диск toosupport некоторых сценариев, таких как следующие:</span><span class="sxs-lookup"><span data-stu-id="340d2-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="340d2-104">Поддержка старых приложений, устанавливающих свои компоненты на диске с ОС.</span><span class="sxs-lookup"><span data-stu-id="340d2-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="340d2-105">Перенос локального физического компьютера или виртуальной машины с диском операционной системы большого размера.</span><span class="sxs-lookup"><span data-stu-id="340d2-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="340d2-106">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: модель Resource Manager и классическая модель.</span><span class="sxs-lookup"><span data-stu-id="340d2-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="340d2-107">В этой статье описан с помощью модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="340d2-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="340d2-108">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="340d2-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="340d2-109">Изменение размера диска hello ОС</span><span class="sxs-lookup"><span data-stu-id="340d2-109">Resize hello OS drive</span></span>
<span data-ttu-id="340d2-110">В этой статье мы выполнить задачу hello изменения размера диска hello операционной системы, с помощью модулей диспетчера ресурсов [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="340d2-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="340d2-111">Откройте интегрированную среду Сценариев Powershell или в окне Powershell в режиме администрирования и выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="340d2-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="340d2-112">Tooyour входа в Microsoft Azure учетной записи в режиме управления ресурсов и выберите подписку, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="340d2-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="340d2-113">Задайте имя группы ресурсов и имя виртуальной машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="340d2-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="340d2-114">Получите ссылку tooyour виртуальной Машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="340d2-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="340d2-115">Остановите hello виртуальной Машины перед изменением размера диска hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="340d2-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="340d2-116">И здесь мы ждать для момента hello!</span><span class="sxs-lookup"><span data-stu-id="340d2-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="340d2-117">Задать размер hello toohello требуемого значения hello ОС диска и обновить hello виртуальной Машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="340d2-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="340d2-118">новый размер Hello должен быть больше, чем размер существующего диска hello.</span><span class="sxs-lookup"><span data-stu-id="340d2-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="340d2-119">Максимальное допустимое Hello — 1023 ГБ.</span><span class="sxs-lookup"><span data-stu-id="340d2-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="340d2-120">Обновление hello виртуальной Машины может занять несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="340d2-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="340d2-121">После завершения выполнения команды hello перезапустите hello виртуальной Машины следующим образом:</span><span class="sxs-lookup"><span data-stu-id="340d2-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="340d2-122">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="340d2-122">And that’s it!</span></span> <span data-ttu-id="340d2-123">Теперь RDP в hello виртуальной Машины, откройте Управление компьютером (или «Управление дисками») и разверните hello диска, с помощью hello вновь выделенный размер.</span><span class="sxs-lookup"><span data-stu-id="340d2-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="340d2-124">Сводка</span><span class="sxs-lookup"><span data-stu-id="340d2-124">Summary</span></span>
<span data-ttu-id="340d2-125">В этой статье мы использовали модулей Powershell tooexpand hello диска операционной системы виртуальной машины IaaS Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="340d2-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="340d2-126">Воспроизвести ниже приведен hello полный скрипт в качестве справочной информации.</span><span class="sxs-lookup"><span data-stu-id="340d2-126">Reproduced below is hello complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="340d2-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="340d2-127">Next Steps</span></span>
<span data-ttu-id="340d2-128">Хотя в этой статье мы уделять расширяемый hello ОС диск из виртуальной Машины hello, hello разработаны скрипт может также использоваться для расширения hello данных дисков вложенного toohello ВМ путем изменения одной строки кода.</span><span class="sxs-lookup"><span data-stu-id="340d2-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="340d2-129">Например, сначала данные tooexpand hello диск toohello подключенных виртуальных Машин, замените hello ```OSDisk``` объект ```StorageProfile``` с ```DataDisks``` массива и использовать числовой индекс tooobtain ссылки toofirst подключенный диск данных, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="340d2-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="340d2-130">Аналогичным образом можно ссылаться на вложенное toohello каталога диски других данных виртуальной Машины, либо с помощью индекса, как показано выше или hello ```Name``` свойства hello диска, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="340d2-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="340d2-131">Если вы хотите toofind out как tooattach диски tooan виртуальной Машины диспетчера ресурсов Azure, установите этот флажок, [статьи](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="340d2-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

