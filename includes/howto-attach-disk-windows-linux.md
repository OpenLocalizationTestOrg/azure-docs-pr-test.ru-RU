


## <a name="attach-an-empty-disk"></a><span data-ttu-id="36c35-101">Подключение пустого диска</span><span class="sxs-lookup"><span data-stu-id="36c35-101">Attach an empty disk</span></span>
<span data-ttu-id="36c35-102">Присоединение пустого диска является простым способом tooadd, данных на диске, так как Azure hello VHD-файл будет создан и сохраняет его в учетную запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="36c35-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="36c35-103">Нажмите кнопку **виртуальные машины (классические)**, а затем выберите hello соответствующие виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="36c35-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="36c35-104">В меню "настройки" hello, щелкните **дисков**.</span><span class="sxs-lookup"><span data-stu-id="36c35-104">In hello Settings menu, click **Disks**.</span></span>

   ![Присоединить новый пустой диск](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="36c35-106">На панели команд hello, нажмите кнопку **присоединения новой**.</span><span class="sxs-lookup"><span data-stu-id="36c35-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="36c35-107">Hello **присоединить новый диск** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="36c35-107">hello **Attach new disk** dialog box appears.</span></span>

    ![Подключение нового диска](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="36c35-109">Заполните hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="36c35-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="36c35-110">В **имя файла**, примите имя по умолчанию hello, или ввести еще один — для hello VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="36c35-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="36c35-111">диск данных Hello использует использованием автоматически созданного имени, даже если введите другое имя для hello VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="36c35-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="36c35-112">Выберите hello **тип** hello диска данных.</span><span class="sxs-lookup"><span data-stu-id="36c35-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="36c35-113">Все виртуальные машины поддерживают диски уровня Standard.</span><span class="sxs-lookup"><span data-stu-id="36c35-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="36c35-114">Большинство виртуальных машин также поддерживают диски уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="36c35-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="36c35-115">Выберите hello **размер (ГБ)** hello диска данных.</span><span class="sxs-lookup"><span data-stu-id="36c35-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="36c35-116">Для **кэширования узла** выберите "Нет" или "Только для чтения".</span><span class="sxs-lookup"><span data-stu-id="36c35-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="36c35-117">Нажмите кнопку ОК toofinish.</span><span class="sxs-lookup"><span data-stu-id="36c35-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="36c35-118">После создания и присоединенного диска данных hello, он будет отображен в раздел дисков hello hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="36c35-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![Новый пустой диск данных успешно подключен](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="36c35-120">После добавления диска данных требуется toolog на toohello ВМ и инициализировать диск hello таким образом, чтобы он может использоваться.</span><span class="sxs-lookup"><span data-stu-id="36c35-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="36c35-121">Практическое руководство. Присоединение существующего диска</span><span class="sxs-lookup"><span data-stu-id="36c35-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="36c35-122">Для подключения существующего диска требуется VHD-файл в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="36c35-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="36c35-123">Используйте hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) командлет tooupload hello .vhd файл toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="36c35-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="36c35-124">После создания и отправки hello VHD-файл, его можно присоединить tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="36c35-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="36c35-125">Нажмите кнопку **виртуальные машины (классические)**, а затем выберите hello соответствующую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="36c35-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="36c35-126">В меню "настройки" hello, щелкните **дисков**.</span><span class="sxs-lookup"><span data-stu-id="36c35-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="36c35-127">На панели команд hello, нажмите кнопку **присоединения существующего**.</span><span class="sxs-lookup"><span data-stu-id="36c35-127">On hello command bar, click **Attach existing**.</span></span>

    ![Присоединение диска данных](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="36c35-129">Щелкните **Расположение**.</span><span class="sxs-lookup"><span data-stu-id="36c35-129">Click **Location**.</span></span> <span data-ttu-id="36c35-130">Отображение Hello доступных учетных записей хранилища.</span><span class="sxs-lookup"><span data-stu-id="36c35-130">hello available storage accounts display.</span></span> <span data-ttu-id="36c35-131">Выберите нужную учетную запись хранения из этого списка.</span><span class="sxs-lookup"><span data-stu-id="36c35-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Указание учетной записи хранения диска](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="36c35-133">В **учетную запись хранения** входит один или несколько контейнеров, содержащих диски (VHD).</span><span class="sxs-lookup"><span data-stu-id="36c35-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="36c35-134">Выберите соответствующий контейнер hello от перечисленных.</span><span class="sxs-lookup"><span data-stu-id="36c35-134">Select hello appropriate container from those listed.</span></span>

    ![Указание контейнера виртуальных машин Windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="36c35-136">Hello **виртуальные жесткие диски** панели перечислены hello жестких дисков, которые содержатся в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="36c35-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="36c35-137">Выберите один из дисков hello и нажмите кнопку Выбрать.</span><span class="sxs-lookup"><span data-stu-id="36c35-137">Click one of hello disks, and then click Select.</span></span>

    ![Указание образа диска для виртуальных машин Windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="36c35-139">Hello **подключить существующий диск** панели отображаются снова с расположением hello, содержащий hello учетной записи хранилища, контейнера и выбранный жесткий диск (vhd) tooadd toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="36c35-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="36c35-140">Задать **кэширование узла** toonone или чтения, нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="36c35-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![Диск данных успешно подключен](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
