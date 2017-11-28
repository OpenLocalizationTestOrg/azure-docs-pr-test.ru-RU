
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="382d7-101">Создание резервной копии вручную</span><span class="sxs-lookup"><span data-stu-id="382d7-101">To create a manual backup</span></span>

1. <span data-ttu-id="382d7-102">В службе диспетчера устройств StorSimple выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="382d7-102">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="382d7-103">Выберите устройство в таблице со списком устройств.</span><span class="sxs-lookup"><span data-stu-id="382d7-103">From the tabular listing of devices, select your device.</span></span> <span data-ttu-id="382d7-104">Щелкните **Параметры > Управление > Политики архивации**.</span><span class="sxs-lookup"><span data-stu-id="382d7-104">Go to **Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="382d7-105">В колонке **Политики архивации** приведен список всех политик резервного копирования в табличном формате, включая политику для тома, резервную копию которого требуется создать.</span><span class="sxs-lookup"><span data-stu-id="382d7-105">The **Backup policies** blade lists all the backup policies in a tabular format, including the policy for the volume that you want to back up.</span></span> <span data-ttu-id="382d7-106">Выберите политику, связанную с томом, резервную копию которого требуется создать, и щелкните его правой кнопкой мыши, чтобы вызвать контекстное меню.</span><span class="sxs-lookup"><span data-stu-id="382d7-106">Select the policy associated with the volume you want to back up and right-click to invoke the context menu.</span></span> <span data-ttu-id="382d7-107">В раскрывающемся списке выберите **Выполнить моментальную архивацию**.</span><span class="sxs-lookup"><span data-stu-id="382d7-107">From the dropdown list, select **Back up now**.</span></span>

    ![Создание резервной копии вручную](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="382d7-109">В колонке **Выполнить моментальную архивацию** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="382d7-109">In the **Back up now** blade, do the following steps:</span></span>

    1. <span data-ttu-id="382d7-110">В раскрывающемся списке выберите соответствующий **тип моментального снимка**: **локальный** или **облачный**.</span><span class="sxs-lookup"><span data-stu-id="382d7-110">Choose the appropriate **Snapshot type** from the dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="382d7-111">Выбирайте локальный моментальный снимок для быстрой архивации или восстановления, а облачный — для обеспечения устойчивости данных.</span><span class="sxs-lookup"><span data-stu-id="382d7-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![Создание резервной копии вручную](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="382d7-113">Щелкните **ОК** для запуска задания по созданию моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="382d7-113">Click **OK** to start a job to create a snapshot.</span></span> <span data-ttu-id="382d7-114">После успешного создания задания в верхней части страницы отобразится уведомление.</span><span class="sxs-lookup"><span data-stu-id="382d7-114">You will see a notification at the top of the page after the job is successfully created.</span></span>

        ![Создание резервной копии вручную](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="382d7-116">Чтобы отслеживать ход выполнения задания, щелкните это уведомление.</span><span class="sxs-lookup"><span data-stu-id="382d7-116">To monitor the job, click the notification.</span></span> <span data-ttu-id="382d7-117">Вы перейдете к колонке **заданий**, в которой можно просмотреть ход выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="382d7-117">This takes you to the **Jobs** blade where you can view the job progress.</span></span>


5. <span data-ttu-id="382d7-118">После выполнения задания архивации перейдите на вкладку **Каталог резервного копирования** .</span><span class="sxs-lookup"><span data-stu-id="382d7-118">After the backup job is finished, go to the **Backup catalog** tab.</span></span>

6. <span data-ttu-id="382d7-119">С помощью фильтров отобразите нужное устройство, политику резервного копирования и диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="382d7-119">Set the filter selections to the appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="382d7-120">Резервная копия должна появиться в списке резервных наборов данных, которые отображаются в каталоге.</span><span class="sxs-lookup"><span data-stu-id="382d7-120">The backup should appear in the list of backup sets that is displayed in the catalog.</span></span>

