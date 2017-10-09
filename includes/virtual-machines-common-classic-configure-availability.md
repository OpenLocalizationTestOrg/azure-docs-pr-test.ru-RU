


<span data-ttu-id="d0efa-101">Группа доступности позволяет поддерживать доступность виртуальных машин во время простоев, например связанных с обслуживанием.</span><span class="sxs-lookup"><span data-stu-id="d0efa-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="d0efa-102">Помещение двух или более аналогичным образом настроенные виртуальные машины в наборе доступности создает hello доступность toomaintain дублирования hello приложения или службы, выполняемые на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d0efa-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="d0efa-103">Дополнительные сведения о том, как это работает. в разделе [Управление доступностью виртуальных машин hello][Manage hello availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="d0efa-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="d0efa-104">Это наиболее toouse рекомендаций группы доступности и балансировки нагрузки toohelp конечные точки убедитесь, что приложение будет всегда доступен и работает эффективно.</span><span class="sxs-lookup"><span data-stu-id="d0efa-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="d0efa-105">См. дополнительные сведения о [балансировке нагрузки для служб инфраструктуры Azure][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="d0efa-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="d0efa-106">Добавлять классические виртуальные машины в группы доступности можно одним из двух способов.</span><span class="sxs-lookup"><span data-stu-id="d0efa-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="d0efa-107">[Вариант 1: Создание виртуальной машины и набор доступности в hello же время][Option 1: Create a virtual machine and an availability set at hello same time].</span><span class="sxs-lookup"><span data-stu-id="d0efa-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="d0efa-108">Затем можно добавьте новые виртуальные машины toohello, при создании этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d0efa-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="d0efa-109">[Вариант 2: Добавить существующую группу доступности виртуальной машины tooan][Option 2: Add an existing virtual machine tooan availability set].</span><span class="sxs-lookup"><span data-stu-id="d0efa-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="d0efa-110">В классической модели hello, виртуальные машины, которые нужно tooput в hello же группу доступности должен принадлежать toohello же облачной службе.</span><span class="sxs-lookup"><span data-stu-id="d0efa-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="d0efa-111"><a id="createset"></a>Вариант 1: создайте виртуальную машину и набор доступности в hello же времени</span><span class="sxs-lookup"><span data-stu-id="d0efa-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="d0efa-112">Можно использовать либо hello портал Azure или Azure PowerShell команды toodo это.</span><span class="sxs-lookup"><span data-stu-id="d0efa-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="d0efa-113">hello toouse портала Azure:</span><span class="sxs-lookup"><span data-stu-id="d0efa-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="d0efa-114">Если это еще не сделано, войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d0efa-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d0efa-115">Hello концентратора меню **+ создать**, а затем нажмите кнопку **виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="d0efa-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="d0efa-117">Выберите образ виртуальной машины Marketplace hello, нужно toouse.</span><span class="sxs-lookup"><span data-stu-id="d0efa-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="d0efa-118">Вы можете toocreate виртуальной машины Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="d0efa-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="d0efa-119">Для виртуальной машины, выбранного hello, убедитесь, эту модель развертывания hello слишком**классический** и нажмите кнопку **создать**</span><span class="sxs-lookup"><span data-stu-id="d0efa-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="d0efa-121">Введите имя виртуальной машины, имя пользователя и пароль (для компьютеров Windows) или открытый ключ SSH (для компьютеров Linux).</span><span class="sxs-lookup"><span data-stu-id="d0efa-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="d0efa-122">Выберите размер виртуальной Машины hello и нажмите кнопку **выберите** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d0efa-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="d0efa-123">Выберите **необязательная конфигурация > Группа доступности**и выберите набор доступности hello нужно tooadd hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d0efa-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="d0efa-125">Проверьте настройки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d0efa-125">Review your configuration settings.</span></span> <span data-ttu-id="d0efa-126">Когда все будет готово, нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d0efa-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="d0efa-127">Пока Azure создает виртуальную машину, вы можете отслеживать ход выполнения hello в **виртуальные машины** в главном меню hello.</span><span class="sxs-lookup"><span data-stu-id="d0efa-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="d0efa-128">toouse Azure PowerShell команды toocreate виртуальной машине Azure и добавьте его tooa новый или существующую группу доступности см. в разделе [toocreate использование Azure PowerShell и предварительной настройки виртуальных машин под управлением Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d0efa-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="d0efa-129"><a id="addmachine"></a>Вариант 2: добавить существующую группу доступности виртуальной машины tooan</span><span class="sxs-lookup"><span data-stu-id="d0efa-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="d0efa-130">В hello портал Azure можно добавить существующие tooan классических виртуальных машин в существующей группе доступности или создайте новую для них.</span><span class="sxs-lookup"><span data-stu-id="d0efa-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="d0efa-131">(Помните, hello, hello виртуальных машин в одной группе доступности должны принадлежать toohello же облачной службе.) Hello действия являются почти hello же.</span><span class="sxs-lookup"><span data-stu-id="d0efa-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="d0efa-132">С помощью Azure PowerShell можно добавить существующую группу доступности hello виртуальной машины tooan.</span><span class="sxs-lookup"><span data-stu-id="d0efa-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="d0efa-133">Если вы еще не сделали, войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d0efa-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d0efa-134">Hello концентратора меню **виртуальные машины (классические)**.</span><span class="sxs-lookup"><span data-stu-id="d0efa-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="d0efa-136">Hello список виртуальных машин выберите имя hello hello виртуальной машины, что требуется, чтобы набор toohello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d0efa-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="d0efa-137">Выберите **набор доступности** из виртуальной машины hello **параметры**.</span><span class="sxs-lookup"><span data-stu-id="d0efa-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="d0efa-139">Выберите набор доступности hello которых надо tooadd hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d0efa-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="d0efa-140">Hello виртуальной машины должны принадлежать toohello же облачную службу как набор доступности hello.</span><span class="sxs-lookup"><span data-stu-id="d0efa-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="d0efa-142">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d0efa-142">Click **Save**.</span></span>

<span data-ttu-id="d0efa-143">toouse команд Azure PowerShell, откройте сеанс Azure PowerShell правами администратора и запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="d0efa-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="d0efa-144">Местозаполнители hello (такие как &lt;VmCloudServiceName&gt;), замените весь код внутри кавычек hello, включая hello < и > символы, с hello исправления имен.</span><span class="sxs-lookup"><span data-stu-id="d0efa-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="d0efa-145">Hello виртуальной машине может быть toofinish toobe перезапуска, добавив его в группу доступности toohello.</span><span class="sxs-lookup"><span data-stu-id="d0efa-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

