
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="fa17b-101">toocreate архивации вручную</span><span class="sxs-lookup"><span data-stu-id="fa17b-101">toocreate a manual backup</span></span>

1. <span data-ttu-id="fa17b-102">Перейдите в службе диспетчера StorSimple устройство tooyour и нажмите кнопку **устройств**.</span><span class="sxs-lookup"><span data-stu-id="fa17b-102">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="fa17b-103">Hello табличный список устройств, выберите устройство.</span><span class="sxs-lookup"><span data-stu-id="fa17b-103">From hello tabular listing of devices, select your device.</span></span> <span data-ttu-id="fa17b-104">Go слишком**параметры > Управление > политики резервного копирования,**.</span><span class="sxs-lookup"><span data-stu-id="fa17b-104">Go too**Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="fa17b-105">Hello **политики резервного копирования,** колонке перечисляет все политики резервного копирования hello в табличном формате, включая hello политику для hello тома, необходимо tooback.</span><span class="sxs-lookup"><span data-stu-id="fa17b-105">hello **Backup policies** blade lists all hello backup policies in a tabular format, including hello policy for hello volume that you want tooback up.</span></span> <span data-ttu-id="fa17b-106">Выберите политику hello, связанные с hello тома, который необходимо tooback и tooinvoke hello контекстного меню.</span><span class="sxs-lookup"><span data-stu-id="fa17b-106">Select hello policy associated with hello volume you want tooback up and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="fa17b-107">В раскрывающемся списке «hello» выберите **создать резервную копию**.</span><span class="sxs-lookup"><span data-stu-id="fa17b-107">From hello dropdown list, select **Back up now**.</span></span>

    ![Создание резервной копии вручную](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="fa17b-109">В hello **Архивировать** колонке hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fa17b-109">In hello **Back up now** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="fa17b-110">Выберите соответствующий hello **снимков** hello в раскрывающемся списке: **локального** моментального снимка или **облака** моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="fa17b-110">Choose hello appropriate **Snapshot type** from hello dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="fa17b-111">Выбирайте локальный моментальный снимок для быстрой архивации или восстановления, а облачный — для обеспечения устойчивости данных.</span><span class="sxs-lookup"><span data-stu-id="fa17b-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![Создание резервной копии вручную](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="fa17b-113">Нажмите кнопку **ОК** toostart toocreate задания моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="fa17b-113">Click **OK** toostart a job toocreate a snapshot.</span></span> <span data-ttu-id="fa17b-114">После успешного создания задания hello, вы увидите уведомление в начале hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="fa17b-114">You will see a notification at hello top of hello page after hello job is successfully created.</span></span>

        ![Создание резервной копии вручную](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="fa17b-116">toomonitor hello задания, щелкните уведомление hello.</span><span class="sxs-lookup"><span data-stu-id="fa17b-116">toomonitor hello job, click hello notification.</span></span> <span data-ttu-id="fa17b-117">После этого вы перейдете toohello **заданий** колонки, где можно просмотреть ход выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="fa17b-117">This takes you toohello **Jobs** blade where you can view hello job progress.</span></span>


5. <span data-ttu-id="fa17b-118">После завершения задания резервного копирования hello go toohello **каталог резервных копий** вкладки.</span><span class="sxs-lookup"><span data-stu-id="fa17b-118">After hello backup job is finished, go toohello **Backup catalog** tab.</span></span>

6. <span data-ttu-id="fa17b-119">Задать hello фильтра выбор toohello соответствующие устройства, политики резервного копирования и диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="fa17b-119">Set hello filter selections toohello appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="fa17b-120">резервная копия Hello должна появиться в списке hello резервных наборов данных, который отображается в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="fa17b-120">hello backup should appear in hello list of backup sets that is displayed in hello catalog.</span></span>

