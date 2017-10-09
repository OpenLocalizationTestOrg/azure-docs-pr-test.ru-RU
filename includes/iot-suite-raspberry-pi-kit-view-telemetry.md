## <a name="view-hello-telemetry"></a><span data-ttu-id="29f45-101">Представление hello телеметрии</span><span class="sxs-lookup"><span data-stu-id="29f45-101">View hello telemetry</span></span>

<span data-ttu-id="29f45-102">Hello Raspberry Pi теперь отправляет данные телеметрии toohello удаленного решение для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="29f45-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="29f45-103">Hello телеметрии можно просмотреть на панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="29f45-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="29f45-104">Можно также отправлять сообщения tooyour Raspberry Pi из панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="29f45-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="29f45-105">Перейдите в панель мониторинга toohello решения.</span><span class="sxs-lookup"><span data-stu-id="29f45-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="29f45-106">Выберите устройство в hello **tooView устройства** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="29f45-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="29f45-107">Hello телеметрии из hello Raspberry Pi отображает на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="29f45-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Отобразить данные телеметрии из hello Raspberry Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a><span data-ttu-id="29f45-109">Действуют на устройстве hello</span><span class="sxs-lookup"><span data-stu-id="29f45-109">Act on hello device</span></span>

<span data-ttu-id="29f45-110">С панели мониторинга hello решение можно вызывать методы с вашей Raspberry пи.</span><span class="sxs-lookup"><span data-stu-id="29f45-110">From hello solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="29f45-111">Когда hello Raspberry Pi подключается toohello решение для удаленного мониторинга, она отправляет сведения о методах hello поддерживаемых им.</span><span class="sxs-lookup"><span data-stu-id="29f45-111">When hello Raspberry Pi connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span>

- <span data-ttu-id="29f45-112">В панели мониторинга hello решение, нажмите кнопку **устройств** toovisit hello **устройств** страницы.</span><span class="sxs-lookup"><span data-stu-id="29f45-112">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="29f45-113">Выберите ваш Pi Raspberry в hello **список устройств**.</span><span class="sxs-lookup"><span data-stu-id="29f45-113">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="29f45-114">Затем выберите **Методы**:</span><span class="sxs-lookup"><span data-stu-id="29f45-114">Then choose **Methods**:</span></span>

    ![Список устройств на панели мониторинга][img-list-devices]

- <span data-ttu-id="29f45-116">На hello **вызвать метод** выберите **LightBlink** в hello **метод** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="29f45-116">On hello **Invoke Method** page, choose **LightBlink** in hello **Method** dropdown.</span></span>

- <span data-ttu-id="29f45-117">Выберите **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="29f45-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="29f45-118">Hello Индикатор подключен toohello, Raspberry Pi мигает несколько раз.</span><span class="sxs-lookup"><span data-stu-id="29f45-118">hello LED connected toohello Raspberry Pi flashes several times.</span></span> <span data-ttu-id="29f45-119">приложение Hello на hello Raspberry Pi отправляет подтверждение задней toohello решений мониторинга:</span><span class="sxs-lookup"><span data-stu-id="29f45-119">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard:</span></span>

    ![Просмотр журнала методов][img-method-history]

- <span data-ttu-id="29f45-121">Можно переключиться Индикатор hello и отключать с помощью hello **ChangeLightStatus** метод с **LightStatusValue** значение слишком**1** для на или **0** для off.</span><span class="sxs-lookup"><span data-stu-id="29f45-121">You can switch hello LED on and off using hello **ChangeLightStatus** method with a **LightStatusValue** set too**1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="29f45-122">Если оставить hello удаленное наблюдение решение, работающее в учетной записи Azure, взимается плата за hello выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="29f45-122">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="29f45-123">Дополнительные сведения о снижения объема используемой при hello удаленное наблюдение выполняется решение в разделе [Настройка Azure IoT Suite предварительно настроенных решений в целях демонстрации][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="29f45-123">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="29f45-124">Удаление hello предварительно настроенное решение из учетной записи Azure, после завершения его использования.</span><span class="sxs-lookup"><span data-stu-id="29f45-124">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md