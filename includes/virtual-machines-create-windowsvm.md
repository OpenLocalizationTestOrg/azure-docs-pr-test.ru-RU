1. <span data-ttu-id="88f8c-101">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="88f8c-101">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="88f8c-102">Начав работу с левого верхнего угла, щелкните **Создать > Вычисления > Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="88f8c-102">Starting in the upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Переход к образам виртуальных машин Azure на портале](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="88f8c-104">В Windows Server 2016 Datacenter выберите классическую модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="88f8c-104">On the Windows Server 2016 Datacenter, select the Classic deployment model.</span></span> <span data-ttu-id="88f8c-105">Щелкните Создать.</span><span class="sxs-lookup"><span data-stu-id="88f8c-105">Click Create.</span></span>

    ![Снимок экрана с доступными на портале образами виртуальных машин Azure](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="88f8c-107">1. Колонка «Основные»</span><span class="sxs-lookup"><span data-stu-id="88f8c-107">1. Basics blade</span></span>

<span data-ttu-id="88f8c-108">В колонке "Основные" указываются административные сведения о виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="88f8c-108">The Basics blade requests administrative information for the virtual machine.</span></span>

1. <span data-ttu-id="88f8c-109">Введите **имя** виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="88f8c-109">Enter a **Name** for the virtual machine.</span></span> <span data-ttu-id="88f8c-110">В этом примере _HeroVM_ — это имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="88f8c-110">In the example, _HeroVM_ is the name of the virtual machine.</span></span> <span data-ttu-id="88f8c-111">Оно должно содержать от 1 до 15 знаков и не может включать специальные знаки.</span><span class="sxs-lookup"><span data-stu-id="88f8c-111">The name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="88f8c-112">Введите в соответствующих полях **имя пользователя** и надежный **пароль**, которые будут использоваться для создания локальной учетной записи на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="88f8c-112">Enter a **User name** and a strong **Password** that are used to create a local account on the VM.</span></span> <span data-ttu-id="88f8c-113">Локальная учетная запись используется для входа на виртуальную машину и управления ею.</span><span class="sxs-lookup"><span data-stu-id="88f8c-113">The local account is used to sign in to and manage the VM.</span></span> <span data-ttu-id="88f8c-114">В этом примере _azureuser_ — это имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="88f8c-114">In the example, _azureuser_ is the user name.</span></span>

 <span data-ttu-id="88f8c-115">Пароль должен содержать от 8 до 123 символов и включать по меньшей мере три из следующих символов: одна строчная буква, одна прописная буква, одна цифра и один специальный символ.</span><span class="sxs-lookup"><span data-stu-id="88f8c-115">The password must be 8-123 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="88f8c-116">См. дополнительные сведения о [требованиях к имени пользователя и паролю](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="88f8c-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="88f8c-117">**Подписку** указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="88f8c-117">The **Subscription** is optional.</span></span> <span data-ttu-id="88f8c-118">Часто используется параметр "Оплата по мере использования".</span><span class="sxs-lookup"><span data-stu-id="88f8c-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="88f8c-119">Выберите существующую **группу ресурсов** или укажите имя, чтобы создать новую.</span><span class="sxs-lookup"><span data-stu-id="88f8c-119">Select an existing **Resource group** or type the name for a new one.</span></span> <span data-ttu-id="88f8c-120">В этом примере _HeroVMRG_ — это имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="88f8c-120">In the example, _HeroVMRG_ is the name of the resource group.</span></span>

5. <span data-ttu-id="88f8c-121">Выберите **расположение** центра обработки данных Azure, в котором будет выполняться виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="88f8c-121">Select an Azure datacenter **Location** where you want the VM to run.</span></span> <span data-ttu-id="88f8c-122">В этом примере в качестве расположения выбрана **Восточная часть США**.</span><span class="sxs-lookup"><span data-stu-id="88f8c-122">In the example, **East US** is the location.</span></span>

6. <span data-ttu-id="88f8c-123">Когда все поля заполнены, нажмите кнопку **Далее**, чтобы перейти к следующей колонке.</span><span class="sxs-lookup"><span data-stu-id="88f8c-123">When you are done, click **Next** to continue to the next blade.</span></span>

    ![Снимок экрана: параметры в колонке "Основные сведения" для настройки виртуальной машины Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="88f8c-125">2) Колонка "Размер"</span><span class="sxs-lookup"><span data-stu-id="88f8c-125">2. Size blade</span></span>

<span data-ttu-id="88f8c-126">В колонке "Размер" определяется конфигурация виртуальной машины, а также выбираются различные параметры, такие как операционная система, количество процессоров, тип дискового накопителя и предполагаемые ежемесячные затраты на использование.</span><span class="sxs-lookup"><span data-stu-id="88f8c-126">The Size blade identifies the configuration details of the VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="88f8c-127">Выберите размер виртуальной машины и нажмите кнопку **Выбрать**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="88f8c-127">Choose a VM size, and then click **Select** to continue.</span></span> <span data-ttu-id="88f8c-128">В этом примере _DS1_\__V2 Standard_ — это размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="88f8c-128">In this example, _DS1_\__V2 Standard_ is the VM size.</span></span>

  ![Снимок экрана: колонка выбора размера с доступными размерами виртуальной машины Azure](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="88f8c-130">3. Колонка "Настройки"</span><span class="sxs-lookup"><span data-stu-id="88f8c-130">3. Settings blade</span></span>

<span data-ttu-id="88f8c-131">В колонке "Параметры" указываются параметры хранилища и сети.</span><span class="sxs-lookup"><span data-stu-id="88f8c-131">The Settings blade requests storage and network options.</span></span> <span data-ttu-id="88f8c-132">Вы можете принять настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="88f8c-132">You can accept the default settings.</span></span> <span data-ttu-id="88f8c-133">Azure автоматически создаст необходимые записи.</span><span class="sxs-lookup"><span data-stu-id="88f8c-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="88f8c-134">Если вы выбрали размер виртуальной машины, который поддерживает хранилище Azure уровня "Премиум", то можете опробовать его, выбрав для параметра "Тип диска" значение "Премиум (SSD)".</span><span class="sxs-lookup"><span data-stu-id="88f8c-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="88f8c-135">После внесения изменений нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="88f8c-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="88f8c-136">4. Колонка "Сводка"</span><span class="sxs-lookup"><span data-stu-id="88f8c-136">4. Summary blade</span></span>

<span data-ttu-id="88f8c-137">В колонке "Сводка" собраны параметры, указанные в предыдущих колонках.</span><span class="sxs-lookup"><span data-stu-id="88f8c-137">The Summary blade lists the settings specified in the previous blades.</span></span> <span data-ttu-id="88f8c-138">Когда будете готовы создать образ, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="88f8c-138">Click **OK** when you're ready to make the image.</span></span>

 ![Колонка "Сводка" с указанными настройками виртуальной машины](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="88f8c-140">После создания виртуальная машина отображается на портале в разделе **Все ресурсы**. А также на панели мониторинга отображается элемент этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="88f8c-140">After the virtual machine is created, the portal lists the new virtual machine under **All resources**, and displays a tile of the virtual machine on the dashboard.</span></span> <span data-ttu-id="88f8c-141">Также создаются и отображаются в списке соответствующие облачная служба и учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="88f8c-141">The corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="88f8c-142">Виртуальная машина и облачная служба запускаются автоматически, после чего для них отображается состояние **Работает**.</span><span class="sxs-lookup"><span data-stu-id="88f8c-142">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Настройка агента и конечных точек виртуальной машины](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
