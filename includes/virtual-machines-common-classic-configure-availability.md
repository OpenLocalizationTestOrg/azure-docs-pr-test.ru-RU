


<span data-ttu-id="f9019-101">Группа доступности позволяет поддерживать доступность виртуальных машин во время простоев, например связанных с обслуживанием.</span><span class="sxs-lookup"><span data-stu-id="f9019-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="f9019-102">Размещение двух или более одинаково настроенных виртуальных машин в группе доступности создает избыточность, необходимую для обеспечения доступности приложений или служб, выполняемых на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f9019-102">Placing two or more similarly configured virtual machines in an availability set creates the redundancy needed to maintain availability of the applications or services that your virtual machine runs.</span></span> <span data-ttu-id="f9019-103">См. дополнительные сведения об [управлении доступностью виртуальных машин][Manage the availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="f9019-103">For details about how this works, see [Manage the availability of virtual machines][Manage the availability of virtual machines].</span></span>

<span data-ttu-id="f9019-104">Чтобы обеспечить постоянную доступность и эффективность работы приложения, рекомендуется использовать и группы доступности, и балансировку нагрузки конечных точек.</span><span class="sxs-lookup"><span data-stu-id="f9019-104">It's a best practice to use both availability sets and load-balancing endpoints to help ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="f9019-105">См. дополнительные сведения о [балансировке нагрузки для служб инфраструктуры Azure][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="f9019-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="f9019-106">Добавлять классические виртуальные машины в группы доступности можно одним из двух способов.</span><span class="sxs-lookup"><span data-stu-id="f9019-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="f9019-107">[Вариант 1. Одновременное создание виртуальной машины и группы доступности][Option 1: Create a virtual machine and an availability set at the same time].</span><span class="sxs-lookup"><span data-stu-id="f9019-107">[Option 1: Create a virtual machine and an availability set at the same time][Option 1: Create a virtual machine and an availability set at the same time].</span></span> <span data-ttu-id="f9019-108">Затем добавляйте создаваемые виртуальные машины в эту группу.</span><span class="sxs-lookup"><span data-stu-id="f9019-108">Then, add new virtual machines to the set when you create those virtual machines.</span></span>
* <span data-ttu-id="f9019-109">[Вариант 2. Добавление существующей виртуальной машины к группе доступности][Option 2: Add an existing virtual machine to an availability set].</span><span class="sxs-lookup"><span data-stu-id="f9019-109">[Option 2: Add an existing virtual machine to an availability set][Option 2: Add an existing virtual machine to an availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="f9019-110">В классической модели виртуальные машины, которые вы хотите поместить в одну группу доступности, должны относиться к одной облачной службе.</span><span class="sxs-lookup"><span data-stu-id="f9019-110">In the classic model, virtual machines that you want to put in the same availability set must belong to the same cloud service.</span></span>
> 
> 

## <span data-ttu-id="f9019-111"><a id="createset"> </a>Вариант 1. Одновременное создание виртуальной машины и группы доступности</span><span class="sxs-lookup"><span data-stu-id="f9019-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="f9019-112">Для этого можно использовать портал Azure или команды Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9019-112">You can use either the Azure portal or Azure PowerShell commands to do this.</span></span>

<span data-ttu-id="f9019-113">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="f9019-113">To use the Azure portal:</span></span>

1. <span data-ttu-id="f9019-114">Перейдите на [портал Azure](https://portal.azure.com), если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="f9019-114">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f9019-115">В главном меню щелкните **Создать**, а затем — **Виртуальная машина**.</span><span class="sxs-lookup"><span data-stu-id="f9019-115">On the hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="f9019-117">Выберите нужный образ виртуальной машины Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9019-117">Select the Marketplace virtual machine image you wish to use.</span></span> <span data-ttu-id="f9019-118">Можно создать виртуальную машину Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="f9019-118">You can choose to create a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="f9019-119">После выбора виртуальной машины проверьте, что задана **классическая** модель развертывания, и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f9019-119">For the selected virtual machine, verify that the deployment model is set to **Classic** and then click **Create**</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="f9019-121">Введите имя виртуальной машины, имя пользователя и пароль (для компьютеров Windows) или открытый ключ SSH (для компьютеров Linux).</span><span class="sxs-lookup"><span data-stu-id="f9019-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="f9019-122">Укажите размер виртуальной машины и нажмите кнопку **Выбрать** , чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="f9019-122">Choose the VM size and then click **Select** to continue.</span></span>
7. <span data-ttu-id="f9019-123">Выберите пункты **Дополнительная настройка > Группа доступности**, а затем укажите группу доступности, в которую нужно добавить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f9019-123">Choose **Optional Configuration > Availability set**, and select the availability set you wish to add the virtual machine to.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="f9019-125">Проверьте настройки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f9019-125">Review your configuration settings.</span></span> <span data-ttu-id="f9019-126">Когда все будет готово, нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f9019-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="f9019-127">Процесс создания виртуальной машины в Azure можно отслеживать в разделе **Виртуальные машины** , который можно выбрать в главном меню.</span><span class="sxs-lookup"><span data-stu-id="f9019-127">While Azure creates your virtual machine, you can track the progress under **Virtual Machines** in the hub menu.</span></span>

<span data-ttu-id="f9019-128">Чтобы использовать команды Azure PowerShell для создания виртуальной машины Azure и добавления ее в новую или существующую группу доступности, ознакомьтесь со статьей [Создание виртуальной машины Windows с использованием PowerShell и классической модели развертывания](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9019-128">To use Azure PowerShell commands to create an Azure virtual machine and add it to a new or existing availability set, see [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="f9019-129"><a id="addmachine"> </a>Вариант 2. Добавление существующей виртуальной машины к группе доступности</span><span class="sxs-lookup"><span data-stu-id="f9019-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine to an availability set</span></span>
<span data-ttu-id="f9019-130">На портале Azure можно добавить существующие классические виртуальные машины к существующей группе доступности либо создать для них новую.</span><span class="sxs-lookup"><span data-stu-id="f9019-130">In the Azure portal, you can add existing classic virtual machines to an existing availability set or create a new one for them.</span></span> <span data-ttu-id="f9019-131">(Учитывайте, что виртуальные машины из одной группы доступности должны входить в одну облачную службу.) Выполняемые действия практически идентичны.</span><span class="sxs-lookup"><span data-stu-id="f9019-131">(Keep in mind that the virtual machines in the same availability set must belong to the same cloud service.) The steps are almost the same.</span></span> <span data-ttu-id="f9019-132">С помощью Azure PowerShell можно добавить виртуальную машину к существующей группе доступности.</span><span class="sxs-lookup"><span data-stu-id="f9019-132">With Azure PowerShell, you can add the virtual machine to an existing availability set.</span></span>

1. <span data-ttu-id="f9019-133">Войдите на [портал Azure](https://portal.azure.com), если вы еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="f9019-133">If you have not already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f9019-134">В главном меню щелкните **Виртуальные машины (классические)**.</span><span class="sxs-lookup"><span data-stu-id="f9019-134">On the Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="f9019-136">Выберите из списка имя виртуальной машины, которую хотите добавить к группе.</span><span class="sxs-lookup"><span data-stu-id="f9019-136">From the list of virtual machines, select the name of the virtual machine that you want to add to the set.</span></span>
4. <span data-ttu-id="f9019-137">Выберите пункт **Группа доступности** в **параметрах** виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f9019-137">Choose **Availability set** from the virtual machine **Settings**.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="f9019-139">Выберите группу доступности, в которую нужно добавить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f9019-139">Select the availability set you wish to add the virtual machine to.</span></span> <span data-ttu-id="f9019-140">Виртуальная машина должна находиться в той же облачной службе, что и группа доступности.</span><span class="sxs-lookup"><span data-stu-id="f9019-140">The virtual machine must belong to the same cloud service as the availability set.</span></span>
   
    ![Замещающий текст](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="f9019-142">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f9019-142">Click **Save**.</span></span>

<span data-ttu-id="f9019-143">Чтобы использовать команды Azure PowerShell, откройте сеанс Azure PowerShell уровня администратора и выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f9019-143">To use Azure PowerShell commands, open an administrator-level Azure PowerShell session and run the following command.</span></span> <span data-ttu-id="f9019-144">Для заполнителей (таких как &lt;VmCloudServiceName&gt;) замените все содержимое внутри кавычек, включая символы, на правильные имена.</span><span class="sxs-lookup"><span data-stu-id="f9019-144">For the placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="f9019-145">Возможно, вам нужно будет перезапустить виртуальную машину, чтобы завершить ее добавление к группе доступности.</span><span class="sxs-lookup"><span data-stu-id="f9019-145">The virtual machine might have to be restarted to finish adding it to the availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at the same time]: #createset
[Option 2: Add an existing virtual machine to an availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage the availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

