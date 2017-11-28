## <a name="view-the-telemetry"></a><span data-ttu-id="c98a5-101">Просмотр телеметрии</span><span class="sxs-lookup"><span data-stu-id="c98a5-101">View the telemetry</span></span>

<span data-ttu-id="c98a5-102">Теперь устройство Raspberry Pi может отправлять данные телеметрии в удаленное решение мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c98a5-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="c98a5-103">Эти данные можно просмотреть на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="c98a5-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="c98a5-104">Вы также можете использовать эту панель, чтобы отправлять сообщения в Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c98a5-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="c98a5-105">Перейдите к панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="c98a5-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="c98a5-106">Выберите устройство в раскрывающемся списке **Устройство для просмотра**.</span><span class="sxs-lookup"><span data-stu-id="c98a5-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="c98a5-107">Данные телеметрии из Raspberry Pi отобразятся на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c98a5-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![Отображение данных телеметрии из Raspberry Pi][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="c98a5-109">Выполнение действий на устройстве</span><span class="sxs-lookup"><span data-stu-id="c98a5-109">Act on the device</span></span>

<span data-ttu-id="c98a5-110">Используйте панель мониторинга решения для вызова методов на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c98a5-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="c98a5-111">Когда устройство Raspberry Pi подключается к решению для удаленного мониторинга, оно отправляет сведения о поддерживаемых методах.</span><span class="sxs-lookup"><span data-stu-id="c98a5-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="c98a5-112">На панели мониторинга решения щелкните **Устройства**, чтобы перейти на страницу **устройств**.</span><span class="sxs-lookup"><span data-stu-id="c98a5-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="c98a5-113">Выберите Raspberry Pi в **списке устройств**.</span><span class="sxs-lookup"><span data-stu-id="c98a5-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="c98a5-114">Затем выберите **Методы**:</span><span class="sxs-lookup"><span data-stu-id="c98a5-114">Then choose **Methods**:</span></span>

    ![Список устройств на панели мониторинга][img-list-devices]

- <span data-ttu-id="c98a5-116">На странице **Вызвать метод** в раскрывающемся списке **Метод** выберите **LightBlink**.</span><span class="sxs-lookup"><span data-stu-id="c98a5-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="c98a5-117">Щелкните **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="c98a5-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="c98a5-118">Симулятор выводит сообщение на консоли Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c98a5-118">The simulator prints a message in the console on the Raspberry Pi.</span></span> <span data-ttu-id="c98a5-119">Приложение на устройстве Raspberry Pi отправляет подтверждение обратно на панель мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="c98a5-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![Просмотр журнала методов][img-method-history]

- <span data-ttu-id="c98a5-121">Вы можете включить и отключить индикатор, используя метод **ChangeLightStatus** с параметром **LightStatusValue** со значением **1** (для включения) или **0** (для выключения).</span><span class="sxs-lookup"><span data-stu-id="c98a5-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="c98a5-122">Если не завершить выполнение решения удаленного мониторинга в учетной записи Azure, вам будет выставлен счет.</span><span class="sxs-lookup"><span data-stu-id="c98a5-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="c98a5-123">Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).</span><span class="sxs-lookup"><span data-stu-id="c98a5-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="c98a5-124">Удалите предварительно настроенное решение из учетной записи Azure, когда завершите его использование.</span><span class="sxs-lookup"><span data-stu-id="c98a5-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md