<span data-ttu-id="1ef7b-101">Когда диск данных, подключенный к виртуальной машине, больше не нужен, его можно легко отключить.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-101">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="1ef7b-102">При отключении диска происходит удаление диска из виртуальной машины, но не из учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-102">Detaching a disk removes the disk from the virtual machine, but doesn't delete the disk from the Azure storage account.</span></span>

<span data-ttu-id="1ef7b-103">Если вы хотите снова использовать существующие данные на диске, его можно легко повторно подключить как к той же самой, так и к другой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-103">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="1ef7b-104">Чтобы отключить диск операционной системы, сначала необходимо удалить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-104">To detach an operating system disk, you first need to delete the virtual machine.</span></span>
>

## <a name="find-the-disk"></a><span data-ttu-id="1ef7b-105">Поиск диска</span><span class="sxs-lookup"><span data-stu-id="1ef7b-105">Find the disk</span></span>
<span data-ttu-id="1ef7b-106">Если вы не знаете имени диска или хотите проверить его перед отсоединением, выполните следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-106">If you don't know the name of the disk or want to verify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="1ef7b-107">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ef7b-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="1ef7b-108">Нажмите кнопку **Виртуальные машины**, а затем выберите соответствующую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-108">Click **Virtual Machines**, and then select the appropriate VM.</span></span>

3. <span data-ttu-id="1ef7b-109">Возле левого края панели мониторинга виртуальной машины в разделе **Параметры** щелкните **Диски**.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-109">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="1ef7b-110">На панели мониторинга виртуальной машины перечисляются имена и типы всех подключенных дисков.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-110">The virtual machine dashboard lists the name and type of all attached disks.</span></span> <span data-ttu-id="1ef7b-111">Например, на следующем рисунке демонстрируется виртуальная машина, в которой имеется один диск с операционной системой (ОС) и один диск данных:</span><span class="sxs-lookup"><span data-stu-id="1ef7b-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Найти диск данных](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-the-disk"></a><span data-ttu-id="1ef7b-113">Отсоединить диск</span><span class="sxs-lookup"><span data-stu-id="1ef7b-113">Detach the disk</span></span>
1. <span data-ttu-id="1ef7b-114">На портале Azure выберите **Виртуальные машины**, а затем щелкните имя виртуальной машины, в которой находится отключаемый диск.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-114">From the Azure portal, click **Virtual Machines**, and then click the name of the virtual machine that has the data disk you want to detach.</span></span>

2. <span data-ttu-id="1ef7b-115">Возле левого края панели мониторинга виртуальной машины в разделе **Параметры** щелкните **Диски**.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-115">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="1ef7b-116">Выберите диск, который необходимо отключить.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-116">Click the disk you want to detach.</span></span>

  ![Определение диска для отключения](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="1ef7b-118">На панели команд нажмите кнопку **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-118">From the command bar, click **Detach**.</span></span>

  ![Поиск команды отключения](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="1ef7b-120">В окне подтверждения нажмите кнопку **Да**, чтобы отключить диск.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-120">In the confirmation window, click **Yes** to detach the disk.</span></span>

  ![Подтверждение отключение диска](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="1ef7b-122">Диск остается в хранилище, но более не подключен к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1ef7b-122">The disk remains in storage but is no longer attached to a virtual machine.</span></span>
