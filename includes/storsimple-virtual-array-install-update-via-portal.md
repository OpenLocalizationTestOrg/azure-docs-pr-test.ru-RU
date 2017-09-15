<!--author=alkohli last changed: 11/07/16 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="15ec1-101">Установка обновлений с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="15ec1-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="15ec1-102">Откройте диспетчер устройств StorSimple и выберите **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="15ec1-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="15ec1-103">Из списка устройств, подключенных к службе, выберите то, которое требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="15ec1-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate1m.png) 

2. <span data-ttu-id="15ec1-105">В колонке **Параметры** щелкните **Обновления устройства**.</span><span class="sxs-lookup"><span data-stu-id="15ec1-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate2m.png)  

3. <span data-ttu-id="15ec1-107">При наличии доступных обновлений вы увидите сообщение об этом.</span><span class="sxs-lookup"><span data-stu-id="15ec1-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="15ec1-108">Чтобы проверить наличие обновлений, можно щелкнуть элемент **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="15ec1-108">To check for updates, you can also click **Scan**.</span></span>

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate3m.png)

    <span data-ttu-id="15ec1-110">Вы получите уведомления о начале и успешном завершении проверки.</span><span class="sxs-lookup"><span data-stu-id="15ec1-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate5m.png)

4. <span data-ttu-id="15ec1-112">После проверки наличия обновлений щелкните **Скачать обновления**.</span><span class="sxs-lookup"><span data-stu-id="15ec1-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate6m.png)

5. <span data-ttu-id="15ec1-114">В колонке **Свежие обновления** просмотрите сообщение о подтверждении установки после загрузки обновлений.</span><span class="sxs-lookup"><span data-stu-id="15ec1-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="15ec1-115">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="15ec1-115">Click **OK**.</span></span>

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate7m.png)

6. <span data-ttu-id="15ec1-117">Вы получите уведомления о начале и успешном завершении загрузки.</span><span class="sxs-lookup"><span data-stu-id="15ec1-117">You are notified when the upload starts and completes successfully.</span></span>

     ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate8m.png)

5. <span data-ttu-id="15ec1-119">В колонке **Обновления устройства** щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="15ec1-119">In the **Device updates** blade, click **Install**.</span></span>

     ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate11m.png)   

6. <span data-ttu-id="15ec1-121">В колонке **Свежие обновления** вы увидите предупреждение о том, что обновление нарушит работу.</span><span class="sxs-lookup"><span data-stu-id="15ec1-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="15ec1-122">Так как виртуальный массив является устройством с одним узлом, после обновления он будет перезагружен.</span><span class="sxs-lookup"><span data-stu-id="15ec1-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="15ec1-123">Все текущие операции ввода-вывода будут прерваны.</span><span class="sxs-lookup"><span data-stu-id="15ec1-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="15ec1-124">Щелкните **ОК**, чтобы установить обновления.</span><span class="sxs-lookup"><span data-stu-id="15ec1-124">Click **OK** to install the updates.</span></span> 

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate12m.png) 

7. <span data-ttu-id="15ec1-126">Вы получите уведомление о запуске задания установки.</span><span class="sxs-lookup"><span data-stu-id="15ec1-126">You are notified when the install job starts.</span></span> 

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate13m.png)

8.  <span data-ttu-id="15ec1-128">Когда задание установки успешно завершится, выберите ссылку **Просмотреть задание** в колонке **Обновление устройства**, чтобы проверить выполнение установки.</span><span class="sxs-lookup"><span data-stu-id="15ec1-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate15m.png)

    <span data-ttu-id="15ec1-130">Вы перейдете к колонке **Установка обновлений**.</span><span class="sxs-lookup"><span data-stu-id="15ec1-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="15ec1-131">Здесь вы увидите подробные сведения о выполненном задании.</span><span class="sxs-lookup"><span data-stu-id="15ec1-131">You can view detailed information about the job here.</span></span>

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate16m.png)

9. <span data-ttu-id="15ec1-133">После успешной установки обновлений вы увидите сообщение об этом в колонке обновлений устройства.</span><span class="sxs-lookup"><span data-stu-id="15ec1-133">After the updates are successfully installed, you see a message to this effect in the Device updates blade.</span></span> <span data-ttu-id="15ec1-134">Также изменится версия программного обеспечения на **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="15ec1-134">The software version also changes to **10.0.10288.0**.</span></span> 

    ![обновление устройства](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate17m.png)