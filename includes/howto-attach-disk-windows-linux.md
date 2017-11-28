


## <a name="attach-an-empty-disk"></a><span data-ttu-id="d5df1-101">Подключение пустого диска</span><span class="sxs-lookup"><span data-stu-id="d5df1-101">Attach an empty disk</span></span>
<span data-ttu-id="d5df1-102">Подключение пустого диска — это более простой способ добавления диска данных, так как Azure автоматически создает VHD-файл и сохраняет его в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d5df1-102">Attaching an empty disk is a simple way to add a data disk, because Azure creates the .vhd file for you and stores it in the storage account.</span></span>

1. <span data-ttu-id="d5df1-103">Щелкните **Виртуальные машины (классические)**, а затем выберите соответствующую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d5df1-103">Click **Virtual Machines (classic)**, and then select the appropriate VM.</span></span>

2. <span data-ttu-id="d5df1-104">В меню "Параметры" щелкните **Диски**.</span><span class="sxs-lookup"><span data-stu-id="d5df1-104">In the Settings menu, click **Disks**.</span></span>

   ![Присоединить новый пустой диск](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="d5df1-106">На панели команд щелкните **Подключить новый**.</span><span class="sxs-lookup"><span data-stu-id="d5df1-106">On the command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="d5df1-107">Откроется диалоговое окно **Подключение нового диска**.</span><span class="sxs-lookup"><span data-stu-id="d5df1-107">The **Attach new disk** dialog box appears.</span></span>

    ![Подключение нового диска](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="d5df1-109">Заполните следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="d5df1-109">Fill in the following information:</span></span>
    - <span data-ttu-id="d5df1-110">В поле **Имя файла**примите имя по умолчанию или введите другое имя VHD-файла на диске.</span><span class="sxs-lookup"><span data-stu-id="d5df1-110">In **File Name**, accept the default name or type another one for the .vhd file.</span></span> <span data-ttu-id="d5df1-111">Диск данных использует автоматически созданное имя, даже если для VHD-файла указано другое имя.</span><span class="sxs-lookup"><span data-stu-id="d5df1-111">The data disk uses an automatically generated name, even if you type another name for the .vhd file.</span></span>
    - <span data-ttu-id="d5df1-112">Выберите **тип** диска данных.</span><span class="sxs-lookup"><span data-stu-id="d5df1-112">Select the **Type** of the data disk.</span></span> <span data-ttu-id="d5df1-113">Все виртуальные машины поддерживают диски уровня Standard.</span><span class="sxs-lookup"><span data-stu-id="d5df1-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="d5df1-114">Большинство виртуальных машин также поддерживают диски уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="d5df1-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="d5df1-115">Выберите **размер (ГБ)** диска данных.</span><span class="sxs-lookup"><span data-stu-id="d5df1-115">Select the **Size (GB)** of the data disk.</span></span>
    - <span data-ttu-id="d5df1-116">Для **кэширования узла** выберите "Нет" или "Только для чтения".</span><span class="sxs-lookup"><span data-stu-id="d5df1-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="d5df1-117">Нажмите кнопку "ОК" для завершения.</span><span class="sxs-lookup"><span data-stu-id="d5df1-117">Click OK to finish.</span></span>

4. <span data-ttu-id="d5df1-118">После создания и подключения диска данных он отобразится в разделе дисков виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d5df1-118">After the data disk is created and attached, it's listed in the disks section of the VM.</span></span>

   ![Новый пустой диск данных успешно подключен](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="d5df1-120">Добавив диск данных, необходимо войти в систему на виртуальной машине и инициализировать его. После этого его можно будет использовать.</span><span class="sxs-lookup"><span data-stu-id="d5df1-120">After you add a data disk, you need to log on to the VM and initialize the disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="d5df1-121">Практическое руководство. Присоединение существующего диска</span><span class="sxs-lookup"><span data-stu-id="d5df1-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="d5df1-122">Для подключения существующего диска требуется VHD-файл в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d5df1-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="d5df1-123">Для загрузки VHD-файла учетной записи хранения используйте командлет [Добавить AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d5df1-123">Use the [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet to upload the .vhd file to the storage account.</span></span> <span data-ttu-id="d5df1-124">После создания и отправки VHD-файла можно подключить его к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d5df1-124">After you've created and uploaded the .vhd file, you can attach it to a VM.</span></span>

1. <span data-ttu-id="d5df1-125">Щелкните **Виртуальные машины (классические)**, а затем выберите соответствующую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d5df1-125">Click **Virtual Machines (classic)**, and then select the appropriate virtual machine.</span></span>

2. <span data-ttu-id="d5df1-126">В меню "Параметры" щелкните **Диски**.</span><span class="sxs-lookup"><span data-stu-id="d5df1-126">In the Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="d5df1-127">На панели команд щелкните **Подключить существующий**.</span><span class="sxs-lookup"><span data-stu-id="d5df1-127">On the command bar, click **Attach existing**.</span></span>

    ![Присоединение диска данных](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="d5df1-129">Щелкните **Расположение**.</span><span class="sxs-lookup"><span data-stu-id="d5df1-129">Click **Location**.</span></span> <span data-ttu-id="d5df1-130">Отобразится список доступных учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="d5df1-130">The available storage accounts display.</span></span> <span data-ttu-id="d5df1-131">Выберите нужную учетную запись хранения из этого списка.</span><span class="sxs-lookup"><span data-stu-id="d5df1-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Указание учетной записи хранения диска](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="d5df1-133">В **учетную запись хранения** входит один или несколько контейнеров, содержащих диски (VHD).</span><span class="sxs-lookup"><span data-stu-id="d5df1-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="d5df1-134">Выберите нужный контейнер из перечисленных.</span><span class="sxs-lookup"><span data-stu-id="d5df1-134">Select the appropriate container from those listed.</span></span>

    ![Указание контейнера виртуальных машин Windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="d5df1-136">На панели **Виртуальные жесткие диски** перечислены диски, содержащиеся в контейнере.</span><span class="sxs-lookup"><span data-stu-id="d5df1-136">The **vhds** panel lists the disk drives held in the container.</span></span> <span data-ttu-id="d5df1-137">Щелкните один из дисков и нажмите кнопку "Выбрать".</span><span class="sxs-lookup"><span data-stu-id="d5df1-137">Click one of the disks, and then click Select.</span></span>

    ![Указание образа диска для виртуальных машин Windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="d5df1-139">После этого снова отобразится панель **Подключение существующего диска** с расположением, содержащим учетную запись хранения, контейнер и выбранный жесткий диск (VHD), которые будут добавлены к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d5df1-139">The **Attach existing disk** panel displays again, with the location containing the storage account, container, and selected hard disk (vhd) to add to the virtual machine.</span></span>

  <span data-ttu-id="d5df1-140">Для **кэширования узла** задайте значение "Нет" или "Только для чтения", а затем нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="d5df1-140">Set **Host caching** to none or Read only, then click OK.</span></span>

    ![Диск данных успешно подключен](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
