<!--author=alkohli last changed: 01/12/17-->

### <a name="to-take-a-backup"></a><span data-ttu-id="60ed0-101">Создание резервной копии</span><span class="sxs-lookup"><span data-stu-id="60ed0-101">To take a backup</span></span>

1. <span data-ttu-id="60ed0-102">Откройте службу диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="60ed0-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="60ed0-103">Выберите устройство в таблице со списком устройств, а затем щелкните **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="60ed0-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="60ed0-104">В колонке **Параметры** выберите **Параметры > Управление > Политика архивации**.</span><span class="sxs-lookup"><span data-stu-id="60ed0-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span></span>

    ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="60ed0-106">В колонке **Политика архивации** щелкните **+ Add policy** (+ Добавить политику).</span><span class="sxs-lookup"><span data-stu-id="60ed0-106">In the **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="60ed0-108">В колонке **Создать политику архивации** введите имя политики архивации длиной от 3 до 150 символов.</span><span class="sxs-lookup"><span data-stu-id="60ed0-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="60ed0-109">Выберите тома для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="60ed0-109">Select the volumes to be backed up.</span></span> <span data-ttu-id="60ed0-110">При выборе нескольких томов эти тома группируются вместе для создания отказоустойчивой резервной копии.</span><span class="sxs-lookup"><span data-stu-id="60ed0-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span></span>

    ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="60ed0-112">В колонке **Добавление первого расписания** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="60ed0-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="60ed0-113">Выберите тип резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="60ed0-113">Select the type of backup.</span></span> <span data-ttu-id="60ed0-114">Чтобы восстановление выполнялось быстрее, выберите **локальный** моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="60ed0-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="60ed0-115">Чтобы обеспечить устойчивость данных, выберите **облачный** моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="60ed0-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="60ed0-116">Укажите интервал резервного копирования в минутах, часах, днях или неделях.</span><span class="sxs-lookup"><span data-stu-id="60ed0-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="60ed0-117">Выберите период удержания.</span><span class="sxs-lookup"><span data-stu-id="60ed0-117">Select a retention time.</span></span> <span data-ttu-id="60ed0-118">Возможные периоды удержания зависят от частоты резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="60ed0-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="60ed0-119">Например, для политики ежедневного резервного копирования период удержания можно указать в неделях, а для политики ежемесячного резервного копирования — в месяцах.</span><span class="sxs-lookup"><span data-stu-id="60ed0-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="60ed0-120">Выберите время и дату начала применения политики резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="60ed0-120">Select the starting time and date for the backup policy.</span></span>
    5. <span data-ttu-id="60ed0-121">Нажмите кнопку **ОК**, чтобы создать политику архивации.</span><span class="sxs-lookup"><span data-stu-id="60ed0-121">Click **OK** to create the backup policy.</span></span>

        ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="60ed0-123">Щелкните **Создать**, чтобы приступить к созданию политики архивации.</span><span class="sxs-lookup"><span data-stu-id="60ed0-123">Click **Create** to start the backup policy creation.</span></span> <span data-ttu-id="60ed0-124">После ее создания вы получите соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="60ed0-124">You are notified when the backup policy is successfully created.</span></span> <span data-ttu-id="60ed0-125">Список политик архивации также обновится.</span><span class="sxs-lookup"><span data-stu-id="60ed0-125">The list of backup policies is also updated.</span></span>
      
      ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="60ed0-127">Теперь у вас есть политика архивации, на основе которой выполняется резервное копирование данных тома по расписанию.</span><span class="sxs-lookup"><span data-stu-id="60ed0-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




