<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="d22e9-101">tootake резервной копии</span><span class="sxs-lookup"><span data-stu-id="d22e9-101">tootake a backup</span></span>

1. <span data-ttu-id="d22e9-102">Перейдите в службе диспетчера StorSimple устройство tooyour.</span><span class="sxs-lookup"><span data-stu-id="d22e9-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="d22e9-103">Из hello табличный список устройств, выберите устройство и затем щелкните **все параметры**.</span><span class="sxs-lookup"><span data-stu-id="d22e9-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="d22e9-104">В hello **параметры** колонке go слишком**параметры > Управление > Политика архивации**.</span><span class="sxs-lookup"><span data-stu-id="d22e9-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="d22e9-106">В hello **политика архивации** колонка, щелкните **+ добавить политику**.</span><span class="sxs-lookup"><span data-stu-id="d22e9-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="d22e9-108">В hello **создать политику резервного копирования** колонки, укажите имя длиной от 3 до 150 символов для политики архивации.</span><span class="sxs-lookup"><span data-stu-id="d22e9-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="d22e9-109">Выберите toobe hello тома, резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="d22e9-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="d22e9-110">При выборе нескольких томов, эти тома являются сгруппированных вместе toocreate отказоустойчивое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="d22e9-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="d22e9-112">В колонке **Добавление первого расписания** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d22e9-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="d22e9-113">Выберите тип резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="d22e9-113">Select hello type of backup.</span></span> <span data-ttu-id="d22e9-114">Чтобы восстановление выполнялось быстрее, выберите **локальный** моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="d22e9-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="d22e9-115">Чтобы обеспечить устойчивость данных, выберите **облачный** моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="d22e9-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="d22e9-116">Укажите интервал резервного копирования hello в минутах, часы, дни или недели.</span><span class="sxs-lookup"><span data-stu-id="d22e9-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="d22e9-117">Выберите период удержания.</span><span class="sxs-lookup"><span data-stu-id="d22e9-117">Select a retention time.</span></span> <span data-ttu-id="d22e9-118">Выбор времени хранения Hello зависит от частоты резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="d22e9-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="d22e9-119">Например, для ежедневной политики hello хранения может задаваться в неделях, а для ежемесячной — в месяцах.</span><span class="sxs-lookup"><span data-stu-id="d22e9-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="d22e9-120">Выберите hello начала, время и дату для hello политики резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="d22e9-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="d22e9-121">Нажмите кнопку **ОК** политику резервного копирования toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="d22e9-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="d22e9-123">Нажмите кнопку **создать** создания политики резервного копирования toostart hello.</span><span class="sxs-lookup"><span data-stu-id="d22e9-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="d22e9-124">Получать уведомления при hello политику резервного копирования успешно создан.</span><span class="sxs-lookup"><span data-stu-id="d22e9-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="d22e9-125">Hello список политик резервного копирования также обновляется.</span><span class="sxs-lookup"><span data-stu-id="d22e9-125">hello list of backup policies is also updated.</span></span>
      
      ![Добавление политики резервного копирования](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="d22e9-127">Теперь у вас есть политика архивации, на основе которой выполняется резервное копирование данных тома по расписанию.</span><span class="sxs-lookup"><span data-stu-id="d22e9-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




