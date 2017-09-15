#### <a name="to-stop-and-start-a-cloud-appliance"></a><span data-ttu-id="c3632-101">Остановка и запуск облачного устройства</span><span class="sxs-lookup"><span data-stu-id="c3632-101">To stop and start a cloud appliance</span></span>

1. <span data-ttu-id="c3632-102">Чтобы остановить облачное устройство, перейдите к виртуальной машине данного устройства.</span><span class="sxs-lookup"><span data-stu-id="c3632-102">To stop a cloud appliance, go to the VM for your cloud appliance.</span></span>
    <span data-ttu-id="c3632-103">![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="c3632-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="c3632-104">На панели команд щелкните **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="c3632-104">From the command bar, click **Stop**.</span></span>

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="c3632-106">При появлении запроса на подтверждение нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="c3632-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="c3632-108">При остановке виртуальная машина освобождается.</span><span class="sxs-lookup"><span data-stu-id="c3632-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="c3632-109">Во время остановки облачное устройство переходит в состояние **Отмена выделения**.</span><span class="sxs-lookup"><span data-stu-id="c3632-109">While the cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="c3632-110">После остановки облачного устройства его состояние будет **Остановлено (освобождено)**.</span><span class="sxs-lookup"><span data-stu-id="c3632-110">After the cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="c3632-112">После остановки виртуальной машины нажмите кнопку **Запустить** (кнопка становится доступной), чтобы инициировать запуск.</span><span class="sxs-lookup"><span data-stu-id="c3632-112">Once a VM is stopped, click **Start** (button becomes available) to start the VM.</span></span> <span data-ttu-id="c3632-113">После запуска облачного устройства его состояние будет **Запущено**.</span><span class="sxs-lookup"><span data-stu-id="c3632-113">After the cloud appliance has started up, its status is **Started**.</span></span>

    ![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="c3632-115">Используйте следующие командлеты для остановки и запуска облачного устройства.</span><span class="sxs-lookup"><span data-stu-id="c3632-115">Use the following cmdlets to stop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-cloud-appliance"></a><span data-ttu-id="c3632-116">Перезапуск облачного устройства</span><span class="sxs-lookup"><span data-stu-id="c3632-116">To restart a cloud appliance</span></span>

<span data-ttu-id="c3632-117">Чтобы перезапустить облачное устройство, перейдите к виртуальной машине данного устройства.</span><span class="sxs-lookup"><span data-stu-id="c3632-117">To restart a cloud appliance, go to the VM for your cloud appliance.</span></span> <span data-ttu-id="c3632-118">На панели команд нажмите кнопку **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="c3632-118">From the command bar, click **Restart**.</span></span> <span data-ttu-id="c3632-119">При появлении запроса подтвердите перезапуск.</span><span class="sxs-lookup"><span data-stu-id="c3632-119">When prompted, confirm the restart.</span></span> <span data-ttu-id="c3632-120">Когда облачное устройство будет готово к использованию, его состояние будет **Работает**.</span><span class="sxs-lookup"><span data-stu-id="c3632-120">When the cloud appliance is ready for you to use, its status is **Running**.</span></span>

![Виртуальная машина облачного устройства StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="c3632-122">Используйте следующий командлет для перезапуска облачного устройства.</span><span class="sxs-lookup"><span data-stu-id="c3632-122">Use the following cmdlet to restart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

