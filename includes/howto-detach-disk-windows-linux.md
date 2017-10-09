<span data-ttu-id="5ea89-101">Если диск данных, вложенные tooa виртуальной машины больше не нужен, можно легко отключить ее.</span><span class="sxs-lookup"><span data-stu-id="5ea89-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="5ea89-102">Отсоединение диска удаляет hello диск из виртуальной машины hello, но не удаляет hello диска с hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea89-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="5ea89-103">Если требуется toouse hello существующие данные на диске hello, вам может быть повторно присоединена toohello одной виртуальной машине, так и любой другой.</span><span class="sxs-lookup"><span data-stu-id="5ea89-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="5ea89-104">toodetach диск операционной системы, необходимо сначала toodelete hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5ea89-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="5ea89-105">Найти диск hello</span><span class="sxs-lookup"><span data-stu-id="5ea89-105">Find hello disk</span></span>
<span data-ttu-id="5ea89-106">Если вы не знаете hello имя диска hello, или хотите tooverify его, прежде чем отключить ее, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5ea89-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="5ea89-107">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ea89-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="5ea89-108">Нажмите кнопку **виртуальные машины**, а затем выберите hello соответствующие виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5ea89-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="5ea89-109">Нажмите кнопку **дисков** вдоль hello левого края панели мониторинга виртуальной машины hello, в разделе **параметры**.</span><span class="sxs-lookup"><span data-stu-id="5ea89-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="5ea89-110">панели мониторинга виртуальной машины Hello перечислены hello имя и тип все присоединенные диски.</span><span class="sxs-lookup"><span data-stu-id="5ea89-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="5ea89-111">Например, на следующем рисунке демонстрируется виртуальная машина, в которой имеется один диск с операционной системой (ОС) и один диск данных:</span><span class="sxs-lookup"><span data-stu-id="5ea89-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Найти диск данных](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="5ea89-113">Отсоединить диск hello</span><span class="sxs-lookup"><span data-stu-id="5ea89-113">Detach hello disk</span></span>
1. <span data-ttu-id="5ea89-114">Hello портал Azure, щелкните **виртуальные машины**и щелкните имя hello hello виртуальной машиной, содержащей hello требуется toodetach диска с данными.</span><span class="sxs-lookup"><span data-stu-id="5ea89-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="5ea89-115">Нажмите кнопку **дисков** вдоль hello левого края панели мониторинга виртуальной машины hello, в разделе **параметры**.</span><span class="sxs-lookup"><span data-stu-id="5ea89-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="5ea89-116">Щелкните диск hello, который будет toodetach.</span><span class="sxs-lookup"><span data-stu-id="5ea89-116">Click hello disk you want toodetach.</span></span>

  ![Определите toodetach диска hello](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="5ea89-118">На панели команд hello, нажмите кнопку **отсоединения**.</span><span class="sxs-lookup"><span data-stu-id="5ea89-118">From hello command bar, click **Detach**.</span></span>

  ![Найдите hello detach, команда](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="5ea89-120">В окне подтверждения hello, щелкните **Да** toodetach hello диска.</span><span class="sxs-lookup"><span data-stu-id="5ea89-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Подтвердите отсоединение диска hello](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="5ea89-122">Hello диск остается в хранилище, но больше не tooa подключенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5ea89-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
