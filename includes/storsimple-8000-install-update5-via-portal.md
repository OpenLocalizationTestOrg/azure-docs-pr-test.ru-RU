<!--author=alkohli last changed: 08/04/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a><span data-ttu-id="1f659-101">tooinstall обновление от hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1f659-101">tooinstall an update from hello Azure portal</span></span>

1. <span data-ttu-id="1f659-102">На странице службы StorSimple hello выберите устройство.</span><span class="sxs-lookup"><span data-stu-id="1f659-102">On hello StorSimple service page, select your device.</span></span>

    ![Выбор устройства](./media/storsimple-8000-install-update5-via-portal/update1.png)

2. <span data-ttu-id="1f659-104">Перейдите в слишком**параметры устройства** > **обновления устройства**.</span><span class="sxs-lookup"><span data-stu-id="1f659-104">Navigate too**Device settings** > **Device updates**.</span></span>

    ![Выбор параметра "Обновления устройства"](./media/storsimple-8000-install-update5-via-portal/update2.png)

2. <span data-ttu-id="1f659-106">Если доступны новые обновления, появится уведомление.</span><span class="sxs-lookup"><span data-stu-id="1f659-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="1f659-107">Кроме того, в hello **обновления устройства** колонке нажмите кнопку **сканирования обновлений**.</span><span class="sxs-lookup"><span data-stu-id="1f659-107">Alternatively, in hello **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="1f659-108">Задание создается tooscan наличие доступных обновлений.</span><span class="sxs-lookup"><span data-stu-id="1f659-108">A job is created tooscan for available updates.</span></span> <span data-ttu-id="1f659-109">Вы будете оповещены, после успешного завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="1f659-109">You are notified when hello job completes successfully.</span></span>

    ![Выбор параметра "Обновления устройства"](./media/storsimple-8000-install-update5-via-portal/update3.png)

3. <span data-ttu-id="1f659-111">Рекомендуется просмотреть hello заметки о выпуске перед установкой обновления на устройстве.</span><span class="sxs-lookup"><span data-stu-id="1f659-111">We recommend that you review hello release notes before you apply an update on your device.</span></span> <span data-ttu-id="1f659-112">Нажмите кнопку обновления tooapply **установить обновления**.</span><span class="sxs-lookup"><span data-stu-id="1f659-112">tooapply updates, click **Install updates**.</span></span> <span data-ttu-id="1f659-113">В hello **подтверждение регулярные обновления** колонке toocomplete предварительные требования hello проверки перед установкой обновлений.</span><span class="sxs-lookup"><span data-stu-id="1f659-113">In hello **Confirm regular updates** blade, review hello prerequisites toocomplete before you apply updates.</span></span> <span data-ttu-id="1f659-114">Выберите tooindicate флажок hello готов tooupdate hello устройства и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="1f659-114">Select hello checkbox tooindicate that you are ready tooupdate hello device and then click **Install**.</span></span>

    ![Выбор параметра "Обновления устройства"](./media/storsimple-8000-install-update5-via-portal/update4.png)

6. <span data-ttu-id="1f659-116">Начинается выполнение ряда предварительных проверок.</span><span class="sxs-lookup"><span data-stu-id="1f659-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="1f659-117">Эти проверки включают в себя:</span><span class="sxs-lookup"><span data-stu-id="1f659-117">These checks include:</span></span>
   
   * <span data-ttu-id="1f659-118">**Проверка работоспособности контроллера** tooverify, что оба hello контроллеров устройств работоспособен и документации.</span><span class="sxs-lookup"><span data-stu-id="1f659-118">**Controller health checks** tooverify that both hello device controllers are healthy and online.</span></span>
   * <span data-ttu-id="1f659-119">**Проверка работоспособности компонента оборудования** tooverify, что все hello аппаратных компонентов на устройстве StorSimple находятся в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="1f659-119">**Hardware component health checks** tooverify that all hello hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="1f659-120">**DATA 0 проверяет** tooverify включения DATA 0 на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="1f659-120">**DATA 0 checks** tooverify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="1f659-121">Если этот интерфейс не включен, его следует включить и повторить проверку.</span><span class="sxs-lookup"><span data-stu-id="1f659-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="1f659-122">Обновление Hello загружается и устанавливается только в том случае, если все проверки hello завершаются успешно.</span><span class="sxs-lookup"><span data-stu-id="1f659-122">hello update is downloaded and installed only if all hello checks are successfully completed.</span></span> <span data-ttu-id="1f659-123">Получать уведомления при hello проверки находятся в процессе выполнения.</span><span class="sxs-lookup"><span data-stu-id="1f659-123">You are notified when hello checks are in progress.</span></span> <span data-ttu-id="1f659-124">При сбое hello prechecks затем вам будут предоставлены hello причины сбоя.</span><span class="sxs-lookup"><span data-stu-id="1f659-124">If hello prechecks fail, then you will be provided with hello reasons for failure.</span></span> <span data-ttu-id="1f659-125">Решения этих проблем, а затем повторите операцию hello.</span><span class="sxs-lookup"><span data-stu-id="1f659-125">Address those issues and then retry hello operation.</span></span> <span data-ttu-id="1f659-126">Toocontact технической поддержки Майкрософт может понадобиться, если не удается решения этих проблем самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="1f659-126">You may need toocontact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="1f659-127">После успешного завершения hello prechecks создается задание обновления.</span><span class="sxs-lookup"><span data-stu-id="1f659-127">After hello prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="1f659-128">Вы будете оповещены после успешного создания задания обновления hello.</span><span class="sxs-lookup"><span data-stu-id="1f659-128">You are notified when hello update job is successfully created.</span></span>
   
    ![Создание задания обновления](./media/storsimple-8000-install-update5-via-portal/update6.png)
   
    <span data-ttu-id="1f659-130">Обновление Hello, применяется на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="1f659-130">hello update is then applied on your device.</span></span>

9. <span data-ttu-id="1f659-131">Обновление Hello занимает несколько часов toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1f659-131">hello update takes a few hours toocomplete.</span></span> <span data-ttu-id="1f659-132">Задание обновления hello и нажмите кнопку **сведения** tooview сведения hello hello задания в любое время.</span><span class="sxs-lookup"><span data-stu-id="1f659-132">Select hello update job and click **Details** tooview hello details of hello job at any time.</span></span>

    ![Создание задания обновления](./media/storsimple-8000-install-update5-via-portal/update8.png)

     <span data-ttu-id="1f659-134">Также можно отслеживать ход выполнения задания обновления hello из hello **параметры устройства > задания**.</span><span class="sxs-lookup"><span data-stu-id="1f659-134">You can also monitor hello progress of hello update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="1f659-135">На hello **заданий** колонку, вы увидите hello ход выполнения обновления.</span><span class="sxs-lookup"><span data-stu-id="1f659-135">On hello **Jobs** blade, you can see hello update progress.</span></span>

     ![Создание задания обновления](./media/storsimple-8000-install-update5-via-portal/update7.png)

10. <span data-ttu-id="1f659-137">После завершения задания hello перейдите toohello **параметры устройства > обновления устройства**.</span><span class="sxs-lookup"><span data-stu-id="1f659-137">After hello job is complete, navigate toohello **Device settings > Device updates**.</span></span> <span data-ttu-id="1f659-138">версия программного обеспечения Hello теперь должен быть обновлен.</span><span class="sxs-lookup"><span data-stu-id="1f659-138">hello software version should now be updated.</span></span>

