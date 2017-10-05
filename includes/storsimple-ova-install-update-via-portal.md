<!--author=alkohli last changed: 09/02/16 -->

#### <a name="to-install-updates-via-the-azure-classic-portal"></a><span data-ttu-id="c8a70-101">Установка обновлений с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="c8a70-101">To install updates via the Azure classic portal</span></span>
1. <span data-ttu-id="c8a70-102">На странице **Устройства** выберите устройство, на котором требуется установить обновления.</span><span class="sxs-lookup"><span data-stu-id="c8a70-102">On the **Devices** page, select the device on which you want to install updates.</span></span>
2. <span data-ttu-id="c8a70-103">Перейдите в раздел **Устройства > Обслуживание > Обновления программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="c8a70-103">Navigate to **Devices > Maintenance > Software Updates**.</span></span>
   
    ![обновление устройства](../includes/media/storsimple-ova-install-update-via-portal/azupdate1m.png)  
3. <span data-ttu-id="c8a70-105">При наличии доступных обновлений вы увидите сообщение об этом.</span><span class="sxs-lookup"><span data-stu-id="c8a70-105">You see a message if the software updates are available.</span></span> <span data-ttu-id="c8a70-106">Для проверки наличия обновлений можно также нажать кнопку **Проверить обновления** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c8a70-106">To check for updates, you can also click **Scan Updates** at the bottom of the page.</span></span>
   
    ![обновление устройства](../includes/media/storsimple-ova-install-update-via-portal/azupdate2m.png)
4. <span data-ttu-id="c8a70-108">В нижней части страницы щелкните **Скачать обновления**.</span><span class="sxs-lookup"><span data-stu-id="c8a70-108">From the bottom of the page, click **Download Updates**.</span></span> <span data-ttu-id="c8a70-109">Появится диалоговое окно с сообщением о том, что обновление нарушит работу системы.</span><span class="sxs-lookup"><span data-stu-id="c8a70-109">A dialog notifies the user that the update is disruptive.</span></span> <span data-ttu-id="c8a70-110">Если виртуальный массив StorSimple является устройством с одним узлом, то после обновления он будет перезагружен.</span><span class="sxs-lookup"><span data-stu-id="c8a70-110">Given the StorSimple Virtual Array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="c8a70-111">Все текущие операции ввода-вывода будут прерваны.</span><span class="sxs-lookup"><span data-stu-id="c8a70-111">This disrupts any IO in progress.</span></span> <span data-ttu-id="c8a70-112">Щелкните значок галочки, чтобы запустить задание для скачивания доступных обновлений.</span><span class="sxs-lookup"><span data-stu-id="c8a70-112">Click the check icon to launch a job to download the available updates.</span></span> 
   
    ![обновление устройства](../includes/media/storsimple-ova-install-update-via-portal/azupdate3m.png)
5. <span data-ttu-id="c8a70-114">После окончания скачивания обновлений вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="c8a70-114">You are notified when the updates are downloaded.</span></span> 
   
    ![обновление устройства](../includes/media/storsimple-ova-install-update-via-portal/azupdate6m.png)
6. <span data-ttu-id="c8a70-116">Щелкните **Установить обновления** в нижней части страницы, чтобы начать обновление устройства.</span><span class="sxs-lookup"><span data-stu-id="c8a70-116">From the bottom of the page, click **Install Updates** to begin updating the device.</span></span> <span data-ttu-id="c8a70-117">На экране снова появится диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c8a70-117">The dialog is presented to you again.</span></span> <span data-ttu-id="c8a70-118">Щелкните значок галочки, чтобы запустить задание для установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="c8a70-118">Click the check icon to start a job to install the updates.</span></span> 
   
    ![обновление устройства](../includes/media/storsimple-ova-install-update-via-portal/azupdate7m.png) 
7. <span data-ttu-id="c8a70-120">После создания задания вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="c8a70-120">You are notified after the job is created.</span></span> 
   
    ![обновление устройства](../includes/media/storsimple-ova-install-update-via-portal/azupdate8m.png)
8. <span data-ttu-id="c8a70-122">Щелкните ссылку **Просмотреть задание** , чтобы перейти на страницу "Задания" и просмотреть состояние установки.</span><span class="sxs-lookup"><span data-stu-id="c8a70-122">Click **View Job** link to go to the Jobs page and monitor the install status.</span></span> <span data-ttu-id="c8a70-123">Чтобы получить подробные сведения о задании обновления, можно в любое время щелкнуть **Сведения** .</span><span class="sxs-lookup"><span data-stu-id="c8a70-123">You can click **Details** at any time to get detailed information about the update job.</span></span> 
   
    ![обновление устройства](../includes/media/storsimple-ova-install-update-via-portal/azupdate9m.png)

