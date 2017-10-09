#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="26ede-101">toostop и запуск виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="26ede-101">toostop and start a virtual device</span></span>
<span data-ttu-id="26ede-102">toostop виртуального устройства, щелкните ее имя и нажмите кнопку **завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="26ede-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="26ede-103">Пока виртуальное устройство hello завершает работу, она находится в состоянии **остановка**.</span><span class="sxs-lookup"><span data-stu-id="26ede-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="26ede-104">После остановки hello виртуального устройства, его состояние — **остановлена**.</span><span class="sxs-lookup"><span data-stu-id="26ede-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="26ede-105">Используйте следующие командлеты toostop hello и запуск виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="26ede-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="26ede-106">toorestart виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="26ede-106">toorestart a virtual device</span></span>
<span data-ttu-id="26ede-107">Запуск виртуального устройства, если необходимо toorestart его, щелкните ее имя и нажмите кнопку **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="26ede-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="26ede-108">Во время перезапуска виртуального устройства hello, она находится в состоянии **перезапуск**.</span><span class="sxs-lookup"><span data-stu-id="26ede-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="26ede-109">Когда hello виртуального устройства готов для вас toouse, она находится в состоянии **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="26ede-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="26ede-110">Используйте следующий командлет toorestart виртуальное устройство hello.</span><span class="sxs-lookup"><span data-stu-id="26ede-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

