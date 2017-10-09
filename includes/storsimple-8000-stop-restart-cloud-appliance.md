#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="095b5-101">toostop и начала облачному устройству</span><span class="sxs-lookup"><span data-stu-id="095b5-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="095b5-102">toostop устройством облака перейдите toohello виртуальной Машины для вашего устройства облака.</span><span class="sxs-lookup"><span data-stu-id="095b5-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="095b5-103">![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="095b5-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="095b5-104">На панели команд hello, нажмите кнопку **остановить**.</span><span class="sxs-lookup"><span data-stu-id="095b5-104">From hello command bar, click **Stop**.</span></span>

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="095b5-106">При появлении запроса на подтверждение нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="095b5-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="095b5-108">При остановке виртуальная машина освобождается.</span><span class="sxs-lookup"><span data-stu-id="095b5-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="095b5-109">Во время остановки hello облачному устройству, она находится в состоянии **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="095b5-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="095b5-110">После остановки hello облачному устройству, она находится в состоянии **остановлена (освобождена)**.</span><span class="sxs-lookup"><span data-stu-id="095b5-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="095b5-112">Когда виртуальная машина остановлена, щелкните **запустить** (становится доступной кнопка) toostart hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="095b5-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="095b5-113">После запуска hello облачному устройству она находится в состоянии **Started**.</span><span class="sxs-lookup"><span data-stu-id="095b5-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="095b5-115">Используйте следующие командлеты toostop hello и запустите облачному устройству.</span><span class="sxs-lookup"><span data-stu-id="095b5-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="095b5-116">toorestart облачному устройству</span><span class="sxs-lookup"><span data-stu-id="095b5-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="095b5-117">toorestart устройством облака перейдите toohello виртуальной Машины для вашего устройства облака.</span><span class="sxs-lookup"><span data-stu-id="095b5-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="095b5-118">На панели команд hello, нажмите кнопку **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="095b5-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="095b5-119">При появлении запроса подтвердите hello перезапуска.</span><span class="sxs-lookup"><span data-stu-id="095b5-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="095b5-120">При готовности для вас toouse облачному устройству hello она находится в состоянии **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="095b5-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="095b5-122">Используйте следующий командлет toorestart облачному устройству hello.</span><span class="sxs-lookup"><span data-stu-id="095b5-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

